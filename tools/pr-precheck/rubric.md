# Rubric: is this pull request ready to submit?

Every check reads the artifact itself (the diff, the test output, the
repo's stated asks), never the write-up's length, tone, or formatting.
"Plan" below means the accepted plan plus any Deviations recorded in it
(live: `plan.md`; eval: the bundle's Plan context block). "Repo asks"
means the repo's stated template, contribution policy, and AI policy
(live: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`; eval:
the bundle's Repo facts block). Do not invent repo requirements: a
requirement exists only if the repo evidence states it.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | The diff's changed files and hunks, read hunk by hunk against the plan's stated steps, files, and non-goals, and against its Deviations section (live) or Plan context (eval). Also the description's fidelity claims ("implements the plan exactly", "no other changes"). | Every hunk that changes behavior, dependencies, or code outside the plan's stated files is either (a) covered by a plan step or (b) recorded and justified in Deviations. Nothing the plan promises is missing from the diff. If the description claims fidelity or "no other changes", the diff does not contradict it. Fail on any silent extra change (dependency bump, refactor, drive-by cleanup) or silent omitted plan step. Tests, fixtures, and changelog entries the plan or repo asks for are in-plan. A deviation that is recorded and justified passes even if the diff differs from the original plan. | required |
| repro-rerun | Test evidence read against the plan's test plan and the original reproduction. Look for each reproduction command (or an equivalent real-code check), the observed output after the change, and the expected post-fix behavior. | Central failure modes: every failure mode the issue reports and the plan's test plan names (the behavior the fix exists to change) has an after-change result matching the plan's expected behavior, shown as a command with observed output, a quoted observed result, or a named real-code test that exercises that same failure condition with its passing result. A test that covers only the unchanged or control path, or only one of several named failure modes, does not stand in for a missing failure mode, and a passing general test suite never substitutes for an untested central failure mode. Secondary cases: controls and secondary behaviors the plan names (unchanged controls, added warnings, regression guards) are satisfied by an explicit observed result stated in the test evidence, or by a named test in the diff plus a passing suite run; they need not be reproduced with pasted output. Fail if any central failure mode has no after-change result, if a central result is only an assertion ("tested, works", "verified in daily use") with no command, output, or named test, if any output contradicts the expected behavior, or if a named secondary case is neither stated nor covered by a test. A plainly stated inability to run a nonessential case (a control, another platform, a check unrelated to the central behavior), with the reason, passes. An inability to run a central case fails. | required |
| repo-checks-run | Test evidence read against the repo's test and check asks (contributing docs, template checklist, and the plan's test plan): test suite, formatter, linter, generated files, as the repo states them. | Each check the repo asks for or the plan names was run, and the evidence identifies which check was performed and its outcome (for example "fmt and clippy clean", "go generate produces no diff", "`cargo test` passes (312 tests)"); the verbatim command line is not required when the check is identifiable. A vague claim ("everything looks good", "all checks pass" with no check named) is insufficient, and a check that appears only as an unfilled or self-ticked item in the PR checklist, with no stated outcome in the evidence, is not evidence that it was run. A failing or skipped check does not fail this check when the evidence names the failure or skip, states the cause or why it is unrelated to the change, and the PR does not claim it passed. Fail if a required repo check has no evidence of being run, if a failure is hidden or contradicted by the description, or if the evidence is "(none provided)". If the repo states no check, a run of the project's own test command on the touched area passes. | required |
| diff-reviewable | The diff's file list and hunks, the commit list, and the changed-files set read against the plan's scope. | A maintainer can review the change without separating it from noise: no unrelated hunks (reformatting, renames, or restructuring of code the plan does not touch), no debris (stray files, debug output, commented-out code, generated or lock files without a stated reason), and no bundled second change. A change that the repo requires alongside the fix (tests, changelog, regenerated files) is not debris. Fail when unrelated or unexplained hunks are present, even if small. Commit count, commit message style, and diff size alone never fail this check. | required |
| change-explained | The PR title and description read against the diff: does the text tell a maintainer what changed, why, and where, and does it account for every material part of the diff? | The title and description together state what the PR changes and the reason, name the issue it addresses, and account for every material part of the diff: behavior changes, dependency changes, configuration changes, and any change outside the plan's files, so no change is hidden. Routine tests, fixtures, and changelog entries that directly accompany the described fix need not be separately itemized. Plain or terse text passes if it is accurate and complete. Fail if a material diff change goes unmentioned, if the description misstates what the diff does, or if the text is too vague to tell what changed (for example, a title and body that never say what the fix does). Tone, capitalization, and length do not matter. | required |
| repo-conventions | The repo asks (PR template sections and checklist, contribution policy, required testing or changelog asks, issue-reference convention) read against the PR description, diff, and test evidence. | Each ask the repo explicitly states is met in substance: template sections or checklist items are present with real content or a stated reason they do not apply; required artifacts (changelog entry, tests, docs, regenerated files) appear in the diff; the issue is referenced the way the repo asks. Substance over format: a section that is merged, renamed, or reordered passes if its content is present. Fail if a stated ask is ignored (template dropped, checklist unfilled, required changelog or tests missing from the diff). If the repo states no template and no asks, pass. | required |
| ai-disclosure | The repo's AI policy (Repo facts or contributing docs) and any signs of AI assistance in the PR text, commits, or evidence. | If the repo states an AI-use policy or a template disclosure section, the PR follows it: required disclosure is present and specific enough to say what AI did. If the repo states no AI policy, pass unless the PR text claims or implies no AI involvement while the package shows otherwise. Any AI use the PR itself mentions counts as disclosed. Fail only when a stated disclosure ask is unmet or the PR's own statements about AI use are contradicted by the package. | required |
| issue-alignment | The issue's report and expected behavior, the plan's problem statement, and the PR's diff and description. | The PR addresses the problem the claimed issue reports and the plan scoped, and does not silently change what is being solved: no narrowing that leaves part of the reported problem unaddressed without saying so, no widening to a different problem. The PR references the issue it claims. If the PR deliberately changes the problem, that change is recorded in Deviations and explained. Fail if the diff solves something other than the issue (or only part of it, undisclosed), or if the claimed issue is wrong or missing. | required |
| commit-and-title-polish | Commit messages and the PR title. | Title and commits are accurate and descriptive of the change. Report vague or misleading ones as a note. | preferred |
| honest-limits-noted | The description and test evidence for stated limitations, untested platforms, or open risks. | Any limitation, untested condition, or open risk that the package itself reveals (in the plan, issue, diff, or evidence) is stated by the PR rather than implied away. If the package reveals none, pass; the absence of a limitations statement is not itself a failure. Report a note only when the package reveals a limitation or untested condition that the PR does not state. | preferred |

## Grading rules for missing, contradictory, or unverifiable evidence

- **Missing**: if the evidence a check names is absent from the package
  (no test evidence, no diff, no plan context), the check is `fail`
  when the absence itself proves the pass condition cannot hold (for
  example "(none provided)" test evidence), and `unclear` when the
  package is silent on something the check needs but could plausibly
  contain. Say which in the evidence line.
- **Contradictory**: when two parts of the package disagree (the
  description says "no other changes" but the diff shows an extra
  hunk), the artifact wins over the claim. Grade by the diff and the
  test output, and cite the contradiction in the evidence line.
- **Unverifiable**: a claim the package cannot support (a test result
  stated without output, a command never shown) is not evidence. Grade
  it `unclear` if the claim is plausible and checkable in principle, and
  `fail` if the package's own text undercuts it.
- **Not applicable**: a check whose precondition is absent (no AI
  policy, no template, no changelog ask) passes with an evidence line
  saying the repo states no such ask.
- **Disclosed shortfalls**: a failing check, an unrun case, or a known
  limitation that the PR states plainly and explains does not by
  itself fail `repo-checks-run` or `repro-rerun`, per their pass
  conditions. A shortfall that is hidden, or that leaves the fix's
  central behavior unverified, does.
- **Evidence lines**: each check's evidence is one line naming the
  specific hunk, command, quote, or repo ask that decided it.

## Verdict rule

Accept only if every `required` check is graded `pass`.

A `required` check graded `unclear` counts as a failure, so the verdict
is `reject`. Accept only when the package contains enough evidence to
grade every required condition as `pass`.

`preferred` checks never change the verdict. Report their grade and a
short note in the summary and the JSON, but a `fail` or `unclear` on a
preferred check does not reject a package on its own.

Reservations about an accepted package go in the check evidence lines,
not in a third verdict.
