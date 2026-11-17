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

**Claiming difficulty I anticipated**

I anticipated two difficulties in claiming #68. First, it sits in a
shared course repository that the whole section selects from, and it was
one of the most clearly scoped issues in the pool. My `unclaimed` check
was only a snapshot at evaluation time, not a reservation: while I
weighed #67 against #68, another student could have claimed #68 first,
and the selection work would have had to restart from a weaker pick.

Second, claiming was a public commitment made before reproduction. The
claim comment promised a local reproduction with the environment, the
exact steps, and the observed output, at a point when I did not yet know
whether `KeywordSearcher.index([])` would reproduce on my Windows setup.
If it had not reproduced, I would have had to post that honestly and
release the issue. I claimed it anyway because the downside was bounded:
the existing `test_empty_index`, already marked as a strict xfail for
this issue, gave me a concrete first check to run, so a cannot-reproduce
result would have shown up quickly rather than after days of work.

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

The two replacement checks, quoted word-for-word from the rubric now
uploaded at `tools/issue-select/rubric.md` (the summaries above are my
paraphrase; these are the current wording the skill actually executes):

> `scope-coherent` — Evidence: `Issue title, issue body, and maintainer comments` — Pass condition: `The issue describes one coherent problem or outcome that a contributor can work toward. Multiple related substeps, causes, or implementation suggestions are allowed when they all address the same outcome. Exhaustive acceptance criteria are not required.` — Weight: `required`

> `implementation-ready` — Evidence: `Issue body, maintainer comments, prior claim/PR history, and unresolved TODO/TBD items` — Pass condition: `The issue contains enough information to begin implementation without first resolving a major product/design decision or obtaining a missing critical input. Fail if required behavior, assets, APIs, or design decisions are still explicitly TBD, or if repeated abandoned implementations/closed unmerged PRs provide strong evidence that the issue has substantial hidden complexity for a first contribution.` — Weight: `required`

And the verdict rule it feeds, also quoted verbatim:

> Accept only if every required check passes. A required check graded unclear counts as a failure and the issue is rejected. Preferred checks never change an accept/reject verdict; they are used only to rank issues that have already passed all required checks.

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

### Issue Analysis

Issue: `issue-04` (category: clear-accept)

- **Gold label:** `accept`
- **My rubric's verdict in the committed final run:** `reject`
- **Failed check:** `implementation-ready`
- **Agreement in `eval-run.txt`:** `NO`

The four disagreements from the initial run, stated per issue (gold
labels and final-run verdicts are read from the committed
`eval-run.txt`; each initial-run verdict was the opposite of its gold
label, which is what made it a disagreement):

| Issue | Gold label | Initial run verdict (16/20) | Final run verdict (19/20) |
| --- | --- | --- | --- |
| issue-04 | accept | reject | reject |
| issue-15 | reject | accept | reject |
| issue-19 | accept | reject | accept |
| issue-20 | reject | accept | reject |

In the committed final run, `issue-04` is the single disagreement behind
the 19/20 agreement line: every other issue, including the other three
initial disagreements (issue-15, issue-19, issue-20), agrees with gold.
My revised `implementation-ready` check still graded this clear-accept
issue more strictly than the gold label did, failing it where gold
accepts it. That is the revised rubric's known remaining weakness, and
it is the same check quoted verbatim in the Rubric Revision section
above.

One inconsistency between this write-up and the committed record, stated
explicitly rather than smoothed over: the Targeted Re-evaluation section
above reports 4/4 agreement on issue-04, issue-15, issue-19, and
issue-20, but the harness-written `eval-run.txt` from the final full run
still shows `issue-04` as a disagreement. Both records stand as they
were produced: the targeted re-run passed all four issues in isolation,
and the later full run flipped `issue-04` back to `reject`. I did not
edit either number to make them agree; the difference is run-to-run
variation between the targeted and full evaluations under the same
rubric, and the committed full run — the artifact of record — is the
19/20 one.

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

Live-mode output, pasted as produced in the September 23, 2026 session:

**Accept.** All required checks pass, along with the preferred response check. This focused Python/API authorization fix fits your backend and debugging experience. [Issue #67](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/67)

The evidence includes [recent human commits](https://github.com/codepath/pathreview-ai301-fa26-s1/commits/main), a [collaborator response within six days](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/52#issuecomment-5705076836), and [contribution rules](https://github.com/codepath/pathreview-ai301-fa26-s1/blob/main/docs/CONTRIBUTING.md) and [PR requirements](https://github.com/codepath/pathreview-ai301-fa26-s1/blob/main/.github/PULL_REQUEST_TEMPLATE.md) without an AI prohibition.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/67",
  "checks": [
    {
      "name": "maintainer-alive",
      "grade": "pass",
      "evidence": "All five latest main-branch commits are by human contributor Aburke225: three dated 2026-09-16 and two dated 2026-08-24, within 90 days of 2026-09-23."
    },
    {
      "name": "responds-to-issues",
      "grade": "pass",
      "evidence": "Among ten recently updated issues sampled, #52 opened on 2026-09-10 and received its first COLLABORATOR comment from Aburke225 on 2026-09-16, within 30 days."
    },
    {
      "name": "repo-in-use",
      "grade": "pass",
      "evidence": "No releases, tags, or changelog were found; this classroom repository has continuing development through 2026-09-16, satisfying the non-release-project exception."
    },
    {
      "name": "scope-coherent",
      "grade": "pass",
      "evidence": "The issue describes one outcome: enforce profile ownership when creating a review through POST /reviews."
    },
    {
      "name": "implementation-ready",
      "grade": "pass",
      "evidence": "The issue identifies core/services/review_service.py, the ignored authenticated user ID, a triggering request, and existing ownership checks in get_review/list_reviews; no explicit TBDs or abandoned PR history were found."
    },
    {
      "name": "unclaimed",
      "grade": "pass",
      "evidence": "The issue is open with no assignees, zero comments, and no linked branches or PRs; the repository's only PR concerns #60. Student claim comments would be ignored under the house rule."
    },
    {
      "name": "contribution-policy",
      "grade": "pass",
      "evidence": "README, CONTRIBUTING, linked setup instructions, and all issue/PR templates contain no AI-assisted contribution ban; the repository tree contains no dedicated AI policy."
    }
  ],
  "verdict": "accept"
}
```

### Issue #68

URL: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68

Verdict: accept

The skill found that the issue was a bounded Python/RAG bug with clearly
defined expected behavior, named implementation and testing locations,
and an existing regression test.

Live-mode output, pasted as produced in the September 23, 2026 session:

**Accept.** All seven checks pass. This bounded Python/RAG bug fits your debugging and data tooling background, with named files and an existing regression test. [Issue #68](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68)

A [student claim](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5752945639) exists, but your Path Review house rule explicitly allows shared issues. Repository evidence also passes: [recent commits](https://github.com/codepath/pathreview-ai301-fa26-s1/commits/main), a [six-day collaborator response](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/52#issuecomment-5705076836), and [contribution rules without an AI prohibition](https://github.com/codepath/pathreview-ai301-fa26-s1/blob/main/docs/CONTRIBUTING.md). The response check is a preferred positive signal.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
  "checks": [
    {
      "name": "maintainer-alive",
      "grade": "pass",
      "evidence": "All five latest main-branch commits are by Aburke225: three on 2026-09-16 and two on 2026-08-24, within 90 days of 2026-09-23."
    },
    {
      "name": "responds-to-issues",
      "grade": "pass",
      "evidence": "In the ten-issue recent-update sample, #52 opened on 2026-09-10 and received its first COLLABORATOR comment on 2026-09-16, within 30 days."
    },
    {
      "name": "repo-in-use",
      "grade": "pass",
      "evidence": "No releases, tags, or changelog were found; continuing classroom development through 2026-09-16 satisfies the non-release-project exception."
    },
    {
      "name": "scope-coherent",
      "grade": "pass",
      "evidence": "One outcome: prevent KeywordSearcher.index([]) from raising ZeroDivisionError while preserving empty-search behavior."
    },
    {
      "name": "implementation-ready",
      "grade": "pass",
      "evidence": "The issue specifies expected behavior, implementation and test files, and removal of the H-01 xfail marker; the thread supplies a reproduction, with no unresolved TBDs or abandoned implementation history."
    },
    {
      "name": "unclaimed",
      "grade": "pass",
      "evidence": "No assignee or linked implementing PR exists; yulijasso's 2026-09-20 claim is ignored under the classroom house rule, and referenced commits document coursework rather than an implementing PR."
    },
    {
      "name": "contribution-policy",
      "grade": "pass",
      "evidence": "README, CONTRIBUTING, linked setup instructions, and issue/PR templates contain no AI-assisted contribution ban; no dedicated AI policy was found."
    }
  ],
  "verdict": "accept"
}
```

I selected issue #68.