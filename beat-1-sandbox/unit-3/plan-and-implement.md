# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

sujalratnatamrakar

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5989736738

I reproduced issue #68 locally. `KeywordSearcher.index([])` passes an empty
tokenized corpus to `BM25Okapi`, which raises a `ZeroDivisionError` during
initialization.

My plan is to keep the fix scoped to the empty-index behavior:

- Guard the empty-corpus case in `KeywordSearcher.index()` and leave the
  searcher in its existing empty-index state (`chunks == []` and
  `bm25 is None`) instead of constructing `BM25Okapi`.
- Preserve the current indexing behavior for non-empty corpora.
- Remove the strict issue #68 xfail marker from the existing
  `test_empty_index` regression test while keeping its test body unchanged.
- Rerun the original reproduction, the keyword-search unit tests, and the
  repository checks after the change.

I do not plan to change `HybridRetriever`, tokenization, or unrelated
retrieval behavior.

---

## Your branch

**Branch**

fix/68-empty-keyword-index

**Evidence**

Before:

```text
F                                                                        [100%]
================================== FAILURES ===================================
____________________ TestKeywordSearcher.test_empty_index _____________________

self = <tests.unit.test_keyword_search.TestKeywordSearcher object at 0x00000204E710E150>
searcher = <rag.retriever.keyword_search.KeywordSearcher object at 0x00000204E70A2CF0>

    @pytest.mark.xfail(
        strict=True,
        reason="issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index",
    )
    def test_empty_index(self, searcher):
        """Test searching on empty index."""
>       searcher.index([])

tests\unit\test_keyword_search.py:140: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
rag\retriever\keyword_search.py:25: in index
    self.bm25 = BM25Okapi(tokenized_corpus)
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^
.venv\Lib\site-packages\rank_bm25.py:83: in __init__
    super().__init__(corpus, tokenizer)
.venv\Lib\site-packages\rank_bm25.py:27: in __init__
    nd = self._initialize(corpus)
         ^^^^^^^^^^^^^^^^^^^^^^^^
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

self = <rank_bm25.BM25Okapi object at 0x00000204E70A2E40>, corpus = []

    def _initialize(self, corpus):
        nd = {}  # word -> number of documents with word
        num_doc = 0
        for document in corpus:
            self.doc_len.append(len(document))
            num_doc += len(document)
    
            frequencies = {}
            for word in document:
                if word not in frequencies:
                    frequencies[word] = 0
                frequencies[word] += 1
            self.doc_freqs.append(frequencies)
    
            for word, freq in frequencies.items():
                try:
                    nd[word]+=1
                except KeyError:
                    nd[word] = 1
    
            self.corpus_size += 1
    
>       self.avgdl = num_doc / self.corpus_size
                     ^^^^^^^^^^^^^^^^^^^^^^^^^^
E       ZeroDivisionError: division by zero

.venv\Lib\site-packages\rank_bm25.py:52: ZeroDivisionError
=========================== short test summary info ===========================
FAILED tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index
1 failed in 0.29s

```

After:

```text
$ .venv/Scripts/python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -q --runxfail
.                                                                        [100%]
1 passed
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

18/20

This was my complete scored evaluation run. The final run matched 18 of 20 scored packages and passed the required bar. The two disagreements were pkg-09 and pkg-14, both clear-accept packages that my rubric rejected.

**Package analysis**

Package: `pkg-09`

My rubric verdict: `reject`

Gold verdict: `accept`

My rubric rejected pkg-09 because it failed `uncertainty-honest`. The candidate plan states the diagnosis confidently: the glob-derived regex expects `/` separators but is matched against raw Windows paths containing `\` because the normalization performed by `Candidate::new` is skipped. My check required the plan to distinguish confirmed evidence from assumptions or unresolved questions and not present a hypothesis as established fact.

I can see why the gold label accepts this plan. The diagnosis is strongly grounded in the reproduction controls, the issue report, and the maintainer discussion. The regex-mode control demonstrates that candidate paths still contain backslashes, and the thread discusses the same separator-normalization problem and proposes normalization as a fix. The plan also identifies a concrete risk involving `\` being a legal Unix filename character and limits the normalization to Windows. My rubric therefore treated the remaining diagnostic inference more strictly than the gold label did.

**Check rationale**

Current check from my rubric:

> `uncertainty-honest` — Evidence: `Risks, unknowns, assumptions, diagnosis wording, and available evidence` — Pass condition: `The plan distinguishes confirmed evidence from assumptions or unresolved questions and does not present a hypothesis as established fact. Meaningful risks or unknowns that could change implementation are stated.`

I kept this check because an implementation plan should not turn a plausible diagnosis into a confirmed fact when the available reproduction only establishes the observed behavior. The wording intentionally considers both diagnosis language and the available evidence, rather than requiring every plan to contain a generic "unknowns" section. A well-supported diagnosis can therefore pass, while an unsupported causal claim should not. The pkg-09 result shows that this check can still be stricter than the gold labels when the evidence strongly supports a diagnosis without proving every part of the mechanism directly.

**Trade-offs**

The trade-off is visible in `pkg-09` and `pkg-14`. Both have a gold verdict of `accept`, but my rubric rejected them, and both failed `uncertainty-honest`. For pkg-09 specifically, the reproduction, issue discussion, and maintainer comments provide strong evidence for the proposed separator-normalization diagnosis, but my check interpreted the plan's confident causal wording as insufficiently separated from what had been directly confirmed.

I accept that this makes the rubric somewhat conservative: it may reject a plan whose diagnosis is strongly supported but not directly proven. Weakening the check further could improve agreement on clear-accept cases such as pkg-09, but it could also allow plans to state evidence-supported hypotheses as established facts. I kept the stricter wording because preserving the distinction between evidence and inference is useful when deciding whether a plan is ready to implement.
