---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: is this ready to submit?

A PR package is a candidate pull request (title, description, commits, diff, test evidence), read against the plan it claims to implement, the issue that plan belongs to, and the repository's stated rules. Never answer a different question. Never grade more than one package per run. Never answer from gut feel: execute the components in this directory.

## Inputs and modes

Run in exactly one of two modes.

**Live mode**: the student's own submission, checked before it goes out. Read:

- `plan.md`, including its Deviations section.
- The branch diff: run `git diff main...HEAD` (three dots) from the working copy. This is everything the branch changes relative to the default branch.
- `pr_draft.md`: the draft PR title and description.
- `test_evidence.md`.
- The issue and its discussion thread.
- `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.
- The relevant commits on the branch.

Gather issue-side evidence from the real repo. For a house-chain student, read the house plan and the house reproduction package in place of the student's own plan and repro; the same checks grade the same things.

**Eval mode**: the package bundle is the whole world. Read ONLY the supplied bundle text. Do not fetch anything. Do not read local repo files. Always grade a complete package: every check, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. Apply its house rules when reading evidence.

- If the `Repo:` line still carries an unfilled placeholder, stop without grading. Tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope.
- If the PR targets a repo outside the scoped repo, refuse to grade it.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after scope. Hold the outgoing PR title and description against its rules. Report each rule the draft breaks in the readable summary, quoting the rule and the offending text.

Voice never changes the verdict on its own. It affects the verdict only if a rubric check explicitly reads it.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

- `rubric.md` defines the checks and the verdict rule.
- `procedure.md` defines the execution order. Execute it exactly as written.
- `references/evidence-guide.md` defines where each evidence family lives in a PR package.

If the procedure is silent on a step, report the gap in the summary. Never invent or improvise a step.

Before grading, confirm `rubric.md` and `procedure.md` each contain substantive written content (comments and empty templates do not count). If either has none, refuse to grade, say which is empty, and stop. Never invent checks or steps at runtime.

## Verdict and output

The verdict is binary: `accept` (ready to submit) or `reject` (hold). There is no third verdict, no score, and no "accept with reservations". Put reservations in check evidence lines.

Reply with a readable per-check summary first (one line per check, plus voice notes and procedure gaps in live mode). Then end with the fenced JSON block below, valid and last, with nothing after it. Every check entry needs a `name`, a `grade` of `pass`, `fail`, or `unclear`, and a one-line factual `evidence` statement (the fact or quote that decided it). Do not alter, extend, or reorder the schema.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the actual PR, not the polish: a terse complete PR can be ready, and a polished confident one can hide drift. Read the artifact against the plan, the issue, and the stated standards.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary; the fix belongs in the rubric.
- The procedure decides how, not you: follow `procedure.md` as written and report its gaps.
- Treat `unclear` as the rubric's verdict rule directs. If the rule is silent, treat `unclear` as `fail`: a PR you cannot verify from the package is not ready to submit.
