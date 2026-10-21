# Working Notes — How This List Was Assembled

Rough notes on how STARS.md was produced. Kept on the feature branch for
transparency; not intended to ship with the final repo.

## Method

1. Queried the live GitHub starred-repositories endpoint for the authenticated user
   (HeziLiu) — no caching, no guessing.
2. Paged through the results carefully: the first attempt with a large page size was
   truncated by the enormous description of `fighting41love/funNLP`, so the lookup was
   redone in smaller pages and cross-checked item-by-item.
3. Pagination checks performed:
   - `perPage=15, page=1` → items 1-5 visible (5 items confirmed)
   - `perPage=5, page=2` → item 6 (996.ICU)
   - `perPage=5, page=3` → empty (end of list)
   - `perPage=3, page=2` → items 4-6 (confirms boundary: last item is #6)
   - `perPage=1, page=6` → 996.ICU (item 6 is the final one)
   - `perPage=1, page=7` → empty (confirms no more items)
   → Final count: **6 starred repositories**.
4. Recorded `owner/name` + `html_url` for each repo in the STARS.md table, in the
   order returned by the API (newest-starred first).

## Observations about the list

- All six repos are public, non-fork, non-archived.
- Heavily NLP/ML-flavoured: 4 of 6 are NLP/LLM-related (AgentCPM, ERNIE, fastNLP,
  funNLP), 1 is ML coursework (NTU ML2017 homework), 1 is a cultural/movement repo
  (996.ICU, "Repo for counting stars and contributing").
- Dominant languages: Python (5 of 6 repos; the coursework repo is Jupyter Notebook).
- Star counts on the upstream projects range from 833 (AgentCPM) to 277,149 (996.ICU).

## Quirks worth noting

- `fighting41love/funNLP` has an enormous, ever-growing description — it's an
  aggregator of Chinese/English NLP resources.
- `PaddlePaddle/ERNIE`'s default branch is `release/v1.5`, not `main`/`master`.
- The starred list is ordered most-recently-starred first, which is how the table is
  ordered here.

## Not done

- No dedup or filtering was applied: the table reflects exactly what the live lookup
  returned, nothing added or removed.
