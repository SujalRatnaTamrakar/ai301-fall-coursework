# Rubric: is this implementation plan ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | Candidate plan diagnosis, issue context, thread, and reproduction evidence | The plan identifies a plausible cause or mechanism that is supported by the reproduction evidence and does not contradict known behavior. If the exact cause is still uncertain, the plan distinguishes the hypothesis from confirmed observations. | required |
| scope-bounded | Candidate plan scope, non-goals, files/areas, and issue request | The plan describes one bounded change that addresses the issue, identifies what is in scope and what is intentionally out of scope, and does not expand into unrelated refactoring or features. | required |
| approach-executable | Candidate plan files/areas, implementation approach, and order of work | The plan identifies the relevant files or code areas and describes concrete implementation steps with enough detail that another contributor could begin the work without inventing a major design decision. Exact line numbers or final code are not required. | required |
| test-plan-decisive | Candidate plan test plan compared with the reproduction evidence and repository requirements | The plan explains how the original reproduction or an equivalent real-code check will be rerun after the change and states the expected post-fix behavior. It also includes any additional testing explicitly required by the repository or by the proposed change. | required |
| uncertainty-honest | Risks, unknowns, assumptions, diagnosis wording, and available evidence | The plan distinguishes confirmed evidence from assumptions or unresolved questions and does not present a hypothesis as established fact. Meaningful risks or unknowns that could change implementation are stated. | required |
| thread-and-conventions | Candidate plan comment compared with the issue thread, repo facts, contribution instructions, templates, and AI-use policy | The comment accurately represents the plan, responds to relevant maintainer guidance, follows explicit repository contribution requirements, and does not make claims contradicted by the issue thread or reproduction evidence. Required AI-use disclosure or other repository-specific conventions must be followed when applicable. | required |

## Verdict rule

Accept only if every required check passes.

A required check graded unclear counts as a failure, so the verdict is
reject. Accept only when the available plan package contains enough evidence
to grade every required condition as pass.
