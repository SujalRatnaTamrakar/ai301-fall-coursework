# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

### Where it lives

In eval mode, read the candidate plan's diagnosis together with the issue
context, thread highlights, and repro-evidence block.

In live mode, read the diagnosis in plan.md against the issue thread and the
student's posted Unit 2 reproduction comment.

### What good looks like

The stated cause or mechanism explains behavior that the reproduction
evidence actually shows. A hypothesis may remain uncertain, but the plan
must distinguish that hypothesis from confirmed observations and must not
contradict the evidence.


## Scope

### Where it lives

Read the candidate plan's in-scope and out-of-scope statements, named files
or code areas, implementation approach, and the original issue request.

### What good looks like

The plan addresses one bounded issue. The proposed work and named files are
consistent with that issue, and unrelated refactors or features are excluded
or explicitly identified as out of scope.


## Executability

### Where it lives

Read the files/areas section, implementation approach, and proposed order of
work in the candidate plan.

### What good looks like

Another contributor could begin implementing the plan without first
inventing a major product or architectural decision. The plan names the
relevant code area and describes concrete changes, but it does not need to
contain final code or exact line numbers.


## Test plan

### Where it lives

Read the plan's test-plan section and compare it with the original
reproduction steps, observed artifacts, and any repository testing
requirements.

### What good looks like

The plan states how the original reproduction, or an equivalent check
through the real code path, will be rerun after the fix and what successful
post-fix behavior should look like. Repository-required tests or additional
tests needed by the proposed change are included when applicable.


## Honesty

### Where it lives

Read the diagnosis wording, risks, unknowns, assumptions, and any Deviations
section that is present.

### What good looks like

Confirmed evidence is separated from hypotheses and unknowns. The plan does
not claim certainty that the reproduction evidence does not support.
Meaningful risks or unresolved questions that could affect implementation
are stated rather than hidden.


## Comms

### Where it lives

In eval mode, read the candidate plan comment against the issue thread,
repo-facts block, contribution policy, templates, and candidate plan.

In live mode, compare comment.md with the live issue thread, repository
documentation and contribution requirements, and plan.md.

### What good looks like

The comment is specific to the issue, accurately summarizes the proposed
work, responds to relevant maintainer guidance, and does not overstate what
has been established. Explicit repository conventions, including required
AI-use disclosure when applicable, are followed.