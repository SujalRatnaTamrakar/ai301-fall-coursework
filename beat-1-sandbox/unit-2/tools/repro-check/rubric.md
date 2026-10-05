# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

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
