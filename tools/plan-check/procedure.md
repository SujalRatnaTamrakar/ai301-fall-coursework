# Procedure: how to grade a plan package

## Read order

1. Read the repository facts and contribution/convention information first.
2. Read the issue description and thread highlights to identify the requested behavior and maintainer guidance.
3. Read the reproduction evidence and note the observed behavior that the plan must explain and eventually validate.
4. Read the complete candidate plan: diagnosis, scope, files, approach, test plan, and risks or unknowns.
5. Read the candidate plan comment last and compare it with both the plan and the issue thread.

## Evidence gathering

1. For each rubric check, locate evidence only in the package sources identified by the evidence guide.
2. Compare the diagnosis against the reproduction evidence instead of judging whether the diagnosis merely sounds plausible.
3. Compare the proposed scope and approach against the actual issue request and any maintainer guidance.
4. Compare the proposed test plan with the reproduction steps and observable failure.
5. Compare the plan comment with the plan, issue thread, and repository conventions.
6. Do not invent missing information. In eval mode, do not fetch outside evidence.

## Check execution

1. Grade each rubric check independently.
2. Mark a check pass only when its stated pass condition is supported by evidence in the package.
3. Mark a check fail when the package directly violates the pass condition or required evidence is clearly absent.
4. Mark a check unclear when relevant evidence exists but is insufficient to decide the condition without guessing.
5. Record the specific evidence that determined each grade.

## Verdict assembly

1. Collect the grades for every required check.
2. If any required check is fail, return reject.
3. If any required check is unclear, treat it as a failure and return reject.
4. Return accept only when every required check passes.
5. Produce the per-check evidence and final structured output required by SKILL.md.
