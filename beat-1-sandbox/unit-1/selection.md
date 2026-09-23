# Unit 1 — Issue Selection

## Chosen Issue

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68

Verdict: accept

## Why I Chose It

I selected issue #68 because it passed every required check in my
issue-selection rubric. The repository is actively maintained, the issue
has a coherent and implementation-ready scope, there is no blocking
linked pull request, and the repository does not prohibit AI-assisted
contributions.

The issue is also a good fit for my background because it is a bounded
Python/RAG debugging task. The expected behavior is clearly described,
the relevant implementation and test files are identified, and an
existing regression test provides a concrete way to verify the fix.

I also evaluated issue #67, which was accepted by my rubric as a focused
Python/API authorization bug. I chose #68 because its reproduction,
implementation location, expected behavior, and regression-test path are
more explicitly defined.

## Eval Iterations

### Initial Full Eval

Provider: Codex  
Model: gpt-5.6-luna

Agreement: 16/20

Disagreements:
- issue-04
- issue-15
- issue-19
- issue-20

My initial rubric used a single `scope-bounded` check. The evaluation
showed that this check was too strict for some coherent issues while also
failing to detect hidden implementation complexity in other issues.

### Rubric Revision

I replaced the single scope check with two required checks:

- `scope-coherent`: determines whether the issue describes one coherent
  problem or outcome while allowing multiple related causes or
  implementation steps.
- `implementation-ready`: determines whether implementation can begin
  without unresolved product/design decisions, missing critical inputs,
  or strong evidence of hidden complexity.

I also clarified the `unclaimed` check so that old claims that were
explicitly released or abandoned do not count as active claims.

### Targeted Re-evaluation

I reran:

- issue-04
- issue-15
- issue-19
- issue-20

Result: 4/4 matched the gold labels.

### Final Full Eval

Provider: Codex  
Model: gpt-5.6-luna

Agreement: 19/20

Category results:

- claimed: 4/4
- clear-accept: 7/8
- dead-repo: 3/3
- policy: 1/1
- scope: 4/4

Result: PASS

### Eval Environment Note

The course evaluation harness was originally configured for Claude
Sonnet. My Claude course credit was exhausted, so I performed my later
rubric iterations and final evaluation using Codex with
`gpt-5.6-luna`. I kept the provided issue snapshots, gold labels, skill
instructions, and rubric evaluation logic unchanged.

## Live Issue Evaluation

### Issue #67

URL: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/67

Verdict: accept

The skill found that the repository was active, the issue represented a
focused authorization bug, the implementation area was identifiable,
and there was no blocking claim or contribution-policy issue.

### Issue #68

URL: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68

Verdict: accept

The skill found that the issue was a bounded Python/RAG bug with clearly
defined expected behavior, named implementation and testing locations,
and an existing regression test.

I selected issue #68.