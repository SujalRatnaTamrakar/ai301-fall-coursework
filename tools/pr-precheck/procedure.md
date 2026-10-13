# Procedure: how this tool grades a PR package

Grade exactly one PR package per run. The package is graded
side by side: the diff against the plan, the test evidence against the
test plan, the description against the diff and the issue. Read the
plan before the diff and the description last, so the plan sets the
expected boundary and the description is judged against what the diff
actually does, not the other way round.

## Read order

1. Determine the mode. A supplied package bundle (a markdown file with
   Repo facts, Issue, Plan context, and Candidate PR blocks) means eval
   mode. The student's own branch, draft, and issue means live mode. If
   it is unclear which, stop and ask; never guess.
2. **Live mode only**: the first file read is `scope.md`, before any
   other component. If its `Repo:` line is an unfilled placeholder,
   stop without grading and tell the student to fill the `Repo:` line
   in `scope.md` with their section's Path Review repo. If the PR's repo
   is not the scoped repo, refuse to grade. Never guess a scope. Note
   the house rules for later.
3. Check the components. Open `rubric.md` and this file. If `rubric.md`
   has no filled checks table, or this file has no written steps (a
   template with only comments does not count), refuse to grade, say
   which is empty, and stop.
4. **Live mode only**, continuing in this order:
   1. Read `voice-guide.md`. Note its rules for the title and
      description check at the end.
   2. Read `plan.md`, including Deviations. List the plan's steps,
      files, non-goals, and test plan cases. House-chain students read
      the house plan and house repro package instead.
   3. Run `git diff main...HEAD` (three dots) and list every changed
      file and hunk. Read the relevant commits with `git log main..HEAD`.
   4. Read `pr_draft.md` (title and description), then
      `test_evidence.md`.
   5. Read the issue and its discussion thread.
   6. Read `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.
5. **Eval mode only**: the bundle is the whole world. Never read
   `scope.md` or `voice-guide.md`. Do not fetch any URL and do not read
   repository files. Read in this order: Repo facts, Issue and thread,
   Plan context (including repro evidence), then Candidate PR in the
   order Diff, Commits, Test evidence, Title and Description.
6. While reading, write down: the plan's files and non-goals, the plan's
   test cases and controls, every changed file and hunk, every claim the
   description makes, and every repo ask.

## Evidence gathering

1. **Diff against plan.** Go hunk by hunk. For each hunk, tag it as
   covered by a named plan step, covered by a Deviations entry, a
   repo-required companion (tests, changelog, regenerated files), or
   uncovered. Also list any plan step with no hunk. Record the file and
   hunk for each uncovered item.
2. **Tests against test plan.** List every test case and control in the
   plan's test plan. For each, find the command and the observed
   after-change output in the test evidence. Record "shown",
   "asserted without output", "disclosed as not run", or "absent".
3. **Repo-required checks.** From the repo asks (contributing docs,
   template checklist, plan's test plan), list each required check.
   Record its command and recorded outcome. Record any failure or skip
   and whether the PR explains it.
4. **Description against diff and issue.** List each claim the
   description makes (what changed, fidelity claims such as "exactly the
   plan", test claims). Mark each as confirmed, contradicted, or
   unsupported by the diff and evidence. List each material diff change
   the description does not mention. Confirm the issue is referenced and
   that the diff addresses what the issue reports.
5. **Repo conventions.** List the template sections or checklist items
   and mark each as filled with substance, not applicable with a stated
   reason, or ignored. Check the AI-use policy or disclosure section if
   the repo states one, and any AI mention in the PR text. Check the
   changelog, test, and issue-reference asks.
6. **Debris and noise.** Mark unrelated hunks, formatting or
   restructuring outside the plan's files, stray files, debug output,
   and unexplained generated or lock files.
7. **Facts versus assumptions.** Keep two lists: observed facts (a
   quoted hunk, a command with output, a repo ask stated in the repo
   facts) and assumptions (anything inferred). Grade only on facts. Do
   not invent repo requirements or missing evidence, and in eval mode do
   not look anything up.
8. **Contradictions.** Where the description and the artifact disagree,
   the artifact wins. Record both sides.

## Check execution

1. Execute every check in `rubric.md`, required and preferred, in table
   order. Do not skip a check and do not add one.
2. Grade each check against the rubric's pass condition, word for word.
   Do not substitute a stricter or looser test of your own. Judge the
   artifact (what the diff does, what the output shows), never the
   writing polish.
3. Assign `pass` when the pass condition is supported by recorded
   facts. Assign `fail` when the package violates the condition or the
   required evidence is clearly absent. Assign `unclear` when evidence
   exists but cannot decide the condition without guessing.
4. Apply the rubric's rules for disclosed shortfalls, missing evidence,
   contradictory evidence, unverifiable claims, and non-applicable
   asks. A check with no applicable repo ask passes, and its evidence
   line says the repo states none.
5. Write one concrete evidence line per check: the specific hunk,
   command, output, or quote that decided it. "Looks fine" is not
   evidence.
6. A check may be graded from the notes in Evidence gathering without
   re-reading the whole package, as long as the deciding fact is
   recorded. Re-read the source when a note is ambiguous.
7. If the procedure gives no step for something a check needs, record a
   procedure gap. Do not invent a step.
8. **Live mode only**: hold the PR title and description against each
   rule in `voice-guide.md`. Record each rule the draft breaks, quoting
   the rule and the offending text. This never changes a grade unless a
   rubric check reads the voice guide.

## Verdict assembly

1. Collect the grade of every required check.
2. If any required check is `fail`, the verdict is `reject`.
3. If any required check is `unclear`, treat it as a failure and the
   verdict is `reject`.
4. Return `accept` only when every required check is `pass`.
5. Preferred checks may add notes but never change the verdict.
6. When more than one required check failed or was unclear, name the
   first one in rubric order as the deciding check and quote its
   evidence line first in the summary.
7. Print a readable per-check summary: one line per check with its
   name, grade, and evidence. In live mode, add the voice-guide
   violations (rule and offending text) and any procedure gaps after
   the check lines.
8. End the reply with the fenced JSON block exactly as in `SKILL.md`
   and `CONTRACT.md`: `item` (PR URL or bundle id), `checks` (every
   rubric check, in table order, each with `name`, `grade`, and a
   one-line `evidence`), and `verdict`. The block must be valid and
   last, with nothing after it.
9. Grade exactly one PR package per run.
