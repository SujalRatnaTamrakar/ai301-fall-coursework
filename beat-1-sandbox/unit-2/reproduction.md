# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**sujalratnatamrakar**

---

## Posted upstream

Picking this up: `KeywordSearcher.index([])` is reported to raise a
`ZeroDivisionError` instead of handling an empty index cleanly.

I'll reproduce it locally first and post the environment, exact steps,
and observed output before attempting a fix. This is my first contribution
to this sandbox repo.

[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5988905102]

**Reproduction comment**

[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5989336216]

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

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Initial full run: 17/20.
   Disagreements were pkg-05, pkg-10, and pkg-16.

2. I revised `steps-rerunnable` and `environment-matches`.

3. Targeted rerun of pkg-05, pkg-10, and pkg-16: 3/3 agreement.

4. Because I loosened `steps-rerunnable`, I ran pkg-06, pkg-18, and
   pkg-19 as `unfollowable-comms` canaries. The combined targeted run
   produced 6/6 agreement.

5. Confirming full run: __/20.

### Package analysis

Package: `pkg-10`

My initial verdict: `reject`
Gold verdict: `accept`

My original `steps-rerunnable` check was too strict. pkg-10 honestly
reported that the issue could not be reproduced on Linux + zsh and
explicitly documented how that environment differed from the reported
macOS + fish environment.

The commands were sufficient for another contributor to repeat the same
attempt and observe the same result. My original rule incorrectly treated
"steps sufficient to reproduce the attempted test" as "steps that must
successfully reproduce the original bug."

I changed the rule so that an evidenced cannot-reproduce can pass when
another contributor can repeat the documented attempt and verify the
reported outcome.

**Check rationale**

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-matches | Repro report environment record compared with the issue context, repo-facts block, and any repository requirements about versions or platforms | The report identifies the tested version or commit and relevant OS/runtime environment, and that environment supports the conclusion being claimed. A successful reproduction must use the issue's relevant target version/commit, including latest/main when the repository explicitly requires it, unless the report gives a concrete reason the difference does not affect the claim. A cannot-reproduce report may use a different environment if the differences are explicitly stated and the conclusion is limited to that tested environment. | required |
| steps-rerunnable | Repro report's setup and reproduction steps, commands, inputs, and starting state | A stranger can repeat the documented attempt from the stated starting state without inventing any detail essential to triggering or observing the target behavior. Incidental input details and standard setup already established by the report or repository documentation do not need to be repeated. For a cannot-reproduce report, the steps need to reproduce the attempted test and observed result, not the original bug itself. | required |
| behavior-faithful | The issue's described behavior compared with the report's actual result and supporting artifact such as terminal output, traceback, test output, or screenshot | The evidence demonstrates the same target behavior described by the issue. A different error or adjacent failure does not count as reproducing the issue. An evidenced cannot-reproduce may still pass when the observed behavior is clearly shown. | required |
| outcome-honest | The report's conclusion read against its steps and artifacts | The report claims only what its evidence demonstrates. It may honestly say reproduced or could-not-reproduce, but it fails if it calls a different failure a successful reproduction or otherwise overstates the evidence. | required |
| repo-conventions | Claim and repro comments compared with repo contribution docs, issue/PR templates, AI-use policy, and other stated contribution requirements | The comments comply with explicit repository requirements, including any required AI-assistance disclosure. Absence of an AI ban does not require inventing a disclosure requirement. | required |

## Verdict rule

Accept only if every required check passes. A required check graded unclear
counts as fail and the package is rejected. An honest cannot-reproduce can
still be accepted when its environment, steps, observed behavior, and
supporting evidence satisfy the required checks.

### Trade-offs

Loosening `steps-rerunnable` risks accepting reports that leave out
information another contributor actually needs.

To test that trade-off, I reran the three `unfollowable-comms` packages
that my initial rubric had correctly rejected: pkg-06, pkg-18, and pkg-19.

All three remained rejected after the revision. The complete targeted run
of pkg-05, pkg-06, pkg-10, pkg-16, pkg-18, and pkg-19 matched the gold
labels 6/6.

This gave me evidence that the revision removed unnecessary strictness
without allowing the known unfollowable reports to pass.

### Initial full eval

Provider: Codex
Model: gpt-5.6-luna

Agreement: 17/20

Disagreements:
- pkg-05: gold `accept`, rubric `reject`
- pkg-10: gold `accept`, rubric `reject`
- pkg-16: gold `reject`, rubric `accept`

Category results:
- clear-accept: 6/8
- disclosure: 1/1
- no-evidence: 4/4
- unfollowable-comms: 3/3
- wrong-target: 3/4

Result: below the 18/20 bar.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
