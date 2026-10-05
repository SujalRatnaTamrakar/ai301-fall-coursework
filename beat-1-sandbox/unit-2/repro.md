## Environment

Repository commit: `f89c06fc3ff292df2a04a39ac51319d32a76b779`

OS:

```text
Windows-11-10.0.26200-SP0
```

Python:

```text
Python 3.14.4
```

## Steps to reproduce

From the repository root, I first ran the existing regression test normally:

```bash
.venv/Scripts/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -q -rxX
```

Output:

```text
x                                                                        [100%]
=========================== short test summary info ===========================
XFAIL tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index - issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index
1 xfailed in 1.50s
```

I then reran the same test with pytest's xfail behavior disabled:

```bash
.venv/Scripts/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -q --runxfail
```

## Expected behavior

Calling `KeywordSearcher.index([])` should handle an empty corpus without raising an exception.

## Actual behavior

The call reaches `BM25Okapi` with an empty corpus. `rank_bm25` then computes the average document length by dividing by a corpus size of zero, causing a `ZeroDivisionError`.

Relevant output:

```text
____________________ TestKeywordSearcher.test_empty_index _____________________

    def test_empty_index(self, searcher):
        """Test searching on empty index."""
>       searcher.index([])

tests\unit\test_keyword_search.py:140:
rag\retriever\keyword_search.py:25: in index
    self.bm25 = BM25Okapi(tokenized_corpus)

.venv\Lib\site-packages\rank_bm25.py:52:
>       self.avgdl = num_doc / self.corpus_size
E       ZeroDivisionError: division by zero

=========================== short test summary info ===========================
FAILED tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index
1 failed in 0.31s
```

## Result

Reproduced.

The observed failure matches issue #68: `KeywordSearcher.index([])` passes an empty corpus into `BM25Okapi`, which raises `ZeroDivisionError`.