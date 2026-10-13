# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/176

**Branch**

`fix/68-empty-keyword-index`

## Eval iterations

**Run history**

1. Initial full evaluation: **16/20** agreement.
2. Targeted evaluation after revising the rubric: **7/8** agreement. Packages `pkg-05`, `pkg-13`, and `pkg-19` were corrected; `pkg-08` remained a mismatch.
3. Final full evaluation: **18/20** agreement — **PASS**. This matches the agreement line in the submitted `eval-run.txt`.

Final category results: clear-accept 6/7, not-tested 4/4, silent-drift 4/4, standards-wall 1/2, unreviewable 3/3.

**Package analysis**

I analyzed **`pkg-08`**, concerning `jesseduffield/lazygit` issue #5883.

- **Gold label:** `accept`
- **My rubric's decision:** `reject`
- **Failed check:** `repo-checks-run`

The candidate PR fixes a confusing stash interaction involving untracked files. Its test evidence states:

> Integration test `stash_untracked_only_errors` passes; `go test ./...` passes; `go generate ./...` produces no cheatsheet diff.

However, the PR requirements section only states:

> code formatted

My rubric requires evidence that each repository-requested check was actually performed, with an identifiable outcome. It interpreted the formatting statement as insufficient evidence of a completed formatting check, so `repo-checks-run` failed and the overall verdict was `reject`.

The gold label was `accept`, making this a false rejection. The package provides substantial evidence that the fix works, but my rubric applied a stricter standard to the formatting evidence.

**Check rationale**

The following is an exact quotation from my final `rubric.md`, under `repro-rerun`:

> A test that covers only the unchanged or control path, or only one of several named failure modes, does not stand in for a missing failure mode, and a passing general test suite never substitutes for an untested central failure mode.

I revised this check after the initial evaluation because the rubric needed to distinguish between the **central failure mode** the PR was supposed to fix and **secondary tests or controls**. A PR should not pass merely because its general test suite succeeds if the actual reported bug has not been verified after the change.

At the same time, the final rubric allows secondary behaviors to be supported by named tests and passing suite results, rather than requiring a separate pasted reproduction for every control. This adjustment helped improve the evaluation from 16/20 to 18/20.

**Trade-offs**

My rubric prioritizes evidence that the reported bug was fixed and that the repository's required checks were completed. This reduces the risk of accepting PRs that merely claim success without demonstrating it.

The trade-off is that the rubric can be too strict about how evidence is presented. **`pkg-08` is a concrete example:** its gold label was `accept`, but my rubric rejected it because the formatting check was not documented clearly enough.

I accepted this trade-off rather than weakening the rule to accept vague claims that all checks were completed. The final evaluation still passed at **18/20**, with at least one correct match in every category. The remaining mismatches were `pkg-08` and `pkg-20`.