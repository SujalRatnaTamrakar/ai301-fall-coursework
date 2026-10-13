# Evidence guide: where evidence lives in a PR package

This guide maps each kind of evidence the rubric's checks name to where
it lives and what reliable evidence looks like. It adds no checks and
changes no pass conditions or verdict rules; `rubric.md` decides, this
file only locates.

**Eval mode.** The package bundle is the whole world. Every fact comes
from the bundle text. Never fetch a URL and never inspect the local
repository. An eval bundle has these parts, in this order:

- Header lines: `source`, `captured`, `calibration`.
- `## Repo facts`: bullets for `repo`, `description`, `latest release`,
  `pull requests` (the template and PR asks, or "no PR template" plus
  any contribution-doc asks), and `contribution policy` (including any
  stated AI policy).
- `## Issue`: the issue title and number, opener, state, labels, and
  body.
- `## Thread highlights`: the comment count and the comments quoted.
- `## Plan context`: the accepted plan excerpt, with the repro evidence
  it built on, the plan steps, scope and non-goals, files, and the test
  plan.
- `## Candidate PR`, with `### Title`, `### Description`, `### Commits`,
  `### Diff`, and `### Test evidence`.

Do not assume a field the bundle lacks. A bundle has no separate
Deviations section unless the Plan context quotes one; if none is
quoted, treat the plan as having no recorded deviations.

**Live mode.** Use these sources: `plan.md` (including its Deviations),
`git diff main...HEAD`, `git log main..HEAD`, `pr_draft.md` (title and
description), `test_evidence.md`, the real issue thread,
`.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md`. Read
the repo's stated asks only from those files and the thread; do not
invent a requirement that none of them states.

Across all families: reliable evidence is an observable fact (a quoted
hunk, a command with its output, a repo ask stated in the repo facts or
a doc). A claim without such support is an assumption, not evidence.
When a claim and the artifact disagree, the artifact wins.

## Plan fidelity (harness category: silent-drift)

Feeds the rubric checks `plan-fidelity` and `issue-alignment`.

### Issue report and maintainer discussion

**Where it lives.** Eval: `## Issue` (title, body, expected behavior) and
`## Thread highlights`. Live: the real issue thread (issue body and
comments); read the opener's report and any maintainer direction.

**Reliable evidence.** The issue states the reported problem and the
expected behavior in its own words, and the PR's diff and description
address that problem and reference the issue number.

**Missing, contradictory, or insufficient.** The PR references no
issue, or a different one. The diff solves a different or narrower
problem than the issue reports. A maintainer comment in the thread
directs a different approach and the PR ignores it. A thread reading "(no
comments)" is not a gap; it means there is no maintainer direction to
engage.

### Accepted plan, test plan, non-goals, and Deviations

**Where it lives.** Eval: `## Plan context`: the plan's steps, `Scope`,
`Not in scope` (the non-goals), `Files`, and `Test plan` sentences.
Live: `plan.md`, including any Deviations section, which records what
changed from the posted plan and why.

**Reliable evidence.** The plan names the files it will touch, what is
out of scope, and the test cases to rerun. A deviation, when the
build diverged, is recorded in the plan with its reason; a recorded,
justified deviation re-ties a diff that differs from the original plan.

**Missing, contradictory, or insufficient.** The plan lists no files or
non-goals, so no boundary can be read. A change appears in the diff but
in neither the plan nor Deviations (silent drift, too much). A planned
step has no hunk and no note (silent drift, too little). The
description claims "implements the plan exactly" while the diff
contradicts it.

### Actual code diff and relevant commits (fidelity use)

**Where it lives.** Eval: `### Diff` and `### Commits` under
`## Candidate PR`. Live: `git diff main...HEAD` (three dots, run from
the working copy) and `git log main..HEAD`.

**Reliable evidence.** Every file header and hunk is readable, so each
hunk can be tagged to a plan step, a Deviations entry, a repo-required
companion (tests, changelog, regenerated files), or none.

**Missing, contradictory, or insufficient.** A hunk that fits none of
those tags (for example, a dependency bump or an unrelated source
refactor in a file the plan never names). A diff cut off so hunks
cannot be read is unverifiable: grade `unclear`, per the rubric.

## Test evidence (harness category: not-tested)

Feeds the rubric checks `repro-rerun`, `repo-checks-run`, and the
preferred check `honest-limits-noted`.

### Before/after reproduction and repository-required checks

**Where it lives.** Eval: `### Test evidence` under `## Candidate PR`,
read against the plan's `Test plan` and the `Repro evidence` in
`## Plan context`; the repo's own checks come from the `pull requests`
and `contribution policy` bullets in `## Repo facts`. Live:
`test_evidence.md`, read against the test plan in `plan.md`, the
original reproduction, and the checks that `docs/CONTRIBUTING.md` and
`.github/PULL_REQUEST_TEMPLATE.md` ask for.

**Central failure evidence.** A central failure mode is a behavior the
issue reports and the fix exists to change; the plan's test plan names
it. Reliable evidence is the observed after-change result for that
failure mode: a command with its output, a quoted observed result, or a
named real-code test that exercises that same failure condition, with
its passing result. The result matches the expected behavior the plan
named. A passing general suite does not count for a central failure mode
it does not exercise.

**Secondary regression evidence.** Controls and secondary behaviors the
plan names (an unchanged control, an added warning, a regression guard)
are reliable when the test evidence states an explicit observed result
for them, or a named test in the diff covers them and the suite run
passes. Pasted output is not required.

**Repo-required checks.** Each check the repo asks for (test suite,
formatter, linter, generated files) is reliable when the evidence
identifies the check and its outcome, for example "fmt and clippy
clean" or "`cargo test` passes (312 tests)". The verbatim command is not
required. A checklist item ticked in the PR text with no stated outcome
does not show the check was run. A failure or skip is reliable when the
evidence names it and explains the cause, even though the check did not
pass.

**Missing, contradictory, or insufficient.** The section reads
"(none provided)". A central result is asserted ("tested, works",
"verified in daily use") with no output, command, or named test. A
central failure mode named in the plan has no after-change result (for
example, one unit test covers only the first of two named failure
modes, or only the unchanged path). The output contradicts the plan's
expected behavior. A secondary case named in the plan is neither stated
nor covered by a test. A check is claimed in vague terms ("everything
looks good") with no check named. A failure is hidden or the description
claims it passed. A nonessential case the author says they could not run
is a disclosure: grade it by the rubric's rules; an inability to run a
central case is a failure.

## Diff quality (harness category: unreviewable)

Feeds the rubric checks `diff-reviewable` and `commit-and-title-polish`.

### Actual code diff and relevant commits (reviewability use)

**Where it lives.** Eval: `### Diff` (file list and hunks) and
`### Commits`. Live: `git diff main...HEAD` and `git log main..HEAD`.

**Reliable evidence.** The fix is visible in the hunks, and the only
other changes are repo-required companions. Commit messages, if
checked, describe the change they contain.

**Missing, contradictory, or insufficient.** Debris tells: formatting
churn or restructuring in code the plan does not touch, stray files,
debug output, dead or commented-out code, generated or lock files with
no stated reason, and a bundled second change. Commit count, message
style, and diff size alone are not debris and do not fail the check.

## Standards and comms (harness category: standards-wall)

Feeds the rubric checks `change-explained`, `repo-conventions`, and
`ai-disclosure`.

### PR title, description, and template sections

**Where it lives.** Eval: `### Title` and `### Description` under
`## Candidate PR`; the template asks are in the `pull requests` bullet
of `## Repo facts`. Live: `pr_draft.md` for the title and description,
and `.github/PULL_REQUEST_TEMPLATE.md` for the sections to fill.

**Reliable evidence.** The title and description say what changed and
why, name the issue, and account for each material part of the diff.
Each template section or checklist item the repo states is present with
real content or a stated reason it does not apply. A terse but accurate
description counts; a merged or renamed section counts if its content
is present.

**Missing, contradictory, or insufficient.** A material diff change the
description never mentions (for example, a dependency bump or a style
rewrite). A description that misstates the diff. A title or description
too vague to say what the fix does. A stated template section or
checklist left empty or dropped. If the repo facts say "no PR template",
there is no template ask to fail.

### Repository contribution rules and AI-use disclosure

**Where it lives.** Eval: the `pull requests` and `contribution
policy (CONTRIBUTING.md)` bullets in `## Repo facts`, which also say
whether an AI policy is stated ("no stated AI policy" is a stated
absence). Live: `docs/CONTRIBUTING.md` for contribution asks (tests,
changelog, issue reference, AI policy) and
`.github/PULL_REQUEST_TEMPLATE.md` for any disclosure section.

**Reliable evidence.** Each ask the repo states (for example a
changelog entry, tests with behavior changes, an issue reference) is
met in the diff or description. If a policy or template section asks
for AI-use disclosure, the PR discloses it and says what the AI did.
If the repo states no AI policy and the PR text mentions AI use, that
mention counts as disclosed.

**Missing, contradictory, or insufficient.** A stated ask is unmet
(required changelog or tests absent from the diff, template checklist
ignored, required AI disclosure missing). The PR text denies AI
involvement while the package shows otherwise. If the repo evidence
states no ask, there is no ask to fail; do not invent one.
