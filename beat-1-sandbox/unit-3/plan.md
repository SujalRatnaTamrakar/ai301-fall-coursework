# Plan for issue #68

## Diagnosis

### Reproduction evidence

> `E       ZeroDivisionError: division by zero`

Observed behavior:

Calling `KeywordSearcher.index([])` with an empty corpus raises a
`ZeroDivisionError` before a subsequent search can run. The reproduction
traceback shows `KeywordSearcher.index()` passing the empty tokenized corpus
to `BM25Okapi`, where `rank_bm25` attempts to calculate average document
length using a corpus size of zero.

Likely cause:

`KeywordSearcher.index()` constructs `BM25Okapi(tokenized_corpus)`
unconditionally after tokenizing the supplied chunks. When `chunks` is empty,
`tokenized_corpus` is also empty, and `BM25Okapi` does not handle that empty
corpus without raising.

Confirmed:

- The existing `test_empty_index` calls `searcher.index([])`, then searches
  for `"python"` and expects an empty list.
- `KeywordSearcher.index()` assigns the supplied chunks and then constructs
  `BM25Okapi(tokenized_corpus)` without first guarding the empty-corpus case.
- The reproduction fails at `searcher.index([])` with
  `ZeroDivisionError: division by zero`.
- `KeywordSearcher.__init__()` represents the no-index state with
  `self.bm25 = None` and `self.chunks = []`.
- `KeywordSearcher.search()` already returns an empty list when there is no
  BM25 index or when `self.chunks` is empty.
- The existing `test_empty_index` is marked with a strict xfail for issue #68,
  which must be removed once the regression passes.

Still uncertain:

- Chunks whose text tokenizes to an empty token list may expose different
  `rank_bm25` behavior. That case has not been established by issue #68 or
  the current reproduction and is outside this fix.

## Scope

### In scope

- Guard the empty-corpus case in `KeywordSearcher.index()` so `index([])`
  does not construct `BM25Okapi` with an empty corpus.
- Ensure indexing an empty corpus leaves the searcher in the established
  empty-index state with `self.chunks == []` and `self.bm25 is None`.
- Remove the issue #68 strict xfail marker from the existing
  `test_empty_index` regression test while keeping its test behavior and
  assertion unchanged.

### Out of scope

- Changes to `HybridRetriever`.
- Changes to keyword tokenization.
- Refactoring unrelated retrieval code.
- Changes to behavior for non-empty corpora.
- Handling chunks whose text tokenizes to an empty token list.
- Unrelated seeded issues or repository cleanup.

## Files / Areas

- `rag/retriever/keyword_search.py` — update `KeywordSearcher.index()` to
  handle an empty corpus without constructing `BM25Okapi` and explicitly
  clear `self.bm25` so the object remains in a consistent empty-index state.
- `tests/unit/test_keyword_search.py` — remove the issue #68 strict xfail
  marker from `test_empty_index`; keep the existing test body and assertion
  unchanged.

## Approach

1. Keep assigning the supplied chunks to `self.chunks` in
   `KeywordSearcher.index()`, preserving the method's current full-rebuild
   behavior.
2. Before constructing `BM25Okapi`, detect an empty `chunks` collection. For
   that case, set `self.bm25 = None`, log the empty index build consistently
   with the existing keyword-search logging convention, and return without
   constructing `BM25Okapi`.
3. Preserve the existing tokenization and BM25 construction path for
   non-empty corpora. Remove the strict issue #68 xfail marker from
   `test_empty_index` without changing its existing body or expected result.
4. Rerun the original Unit 2 reproduction, the issue #68 regression test,
   and the repository validation commands to confirm the empty-corpus
   failure is resolved without introducing regressions.

## Test Plan

### Original reproduction

```text
.venv/Scripts/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -q -rxX

.venv/Scripts/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -q --runxfail
```

Before the fix:

```text
XFAIL tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index - issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index
1 xfailed in 1.50s

FAILED tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index
E       ZeroDivisionError: division by zero
1 failed in 0.31s
```

### Expected after the fix

`KeywordSearcher.index([])` should complete without raising an exception and
leave the searcher in an empty-index state. The existing `test_empty_index`
body should then reach `search("python", top_k=10)` and receive an empty list,
allowing the regression test to pass normally after its strict xfail marker
is removed.

Rerunning the original reproduction with `--runxfail` should no longer
produce the `ZeroDivisionError`.

### Additional validation

```text
.venv/Scripts/python -m pytest tests/unit/test_keyword_search.py -q
make check
make test-unit
```

## Risks and Unknowns

- Explicitly clearing `self.bm25` is important if a `KeywordSearcher` that
  previously indexed a non-empty corpus is later given `index([])`;
  otherwise the BM25 object could remain associated with the previous corpus
  while `self.chunks` is empty. No existing test specifically covers that
  re-indexing sequence, so this state-consistency behavior is inferred from
  the class's existing no-index state and full-rebuild behavior.
- Chunks whose text tokenizes to an empty token list are an unconfirmed edge
  case and will not be addressed as part of issue #68.

## Deviations

None. The implementation followed the accepted plan.