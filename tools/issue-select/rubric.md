# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | Last 5 human commits or merges to the default branch | At least 2 of the last 5 human commits or merges occurred within the last 90 days | required |
| responds-to-issues | Maintainer first-response sample for recently updated issues | At least one sampled issue received a maintainer response within 30 days | preferred |
| repo-in-use | Latest release, tags, changelog, and recent development activity | The project shipped a release or version within the last 12 months; if the project clearly does not use releases, continuing recent development may satisfy this check | required |
| scope-coherent | Issue title, issue body, and maintainer comments | The issue describes one coherent problem or outcome that a contributor can work toward. Multiple related substeps, causes, or implementation suggestions are allowed when they all address the same outcome. Exhaustive acceptance criteria are not required. | required |
| implementation-ready | Issue body, maintainer comments, prior claim/PR history, and unresolved TODO/TBD items | The issue contains enough information to begin implementation without first resolving a major product/design decision or obtaining a missing critical input. Fail if required behavior, assets, APIs, or design decisions are still explicitly TBD, or if repeated abandoned implementations/closed unmerged PRs provide strong evidence that the issue has substantial hidden complexity for a first contribution. | required |
| unclaimed | Assignees, linked pull requests, development sidebar, and issue comments | There is no current assignee, no open linked pull request implementing the issue, and no fresh claim showing that another contributor is actively working on it. Old claims that were explicitly released or abandoned do not fail this check. | required |
| contribution-policy | CONTRIBUTING.md, README, issue/PR templates, and any repository AI/contribution policy | There is no explicit policy prohibiting AI-assisted contributions. Policies requiring disclosure, contributor understanding, testing, or review still pass. | required |

## Verdict rule

Accept only if every required check passes. A required check graded unclear counts as a failure and the issue is rejected. Preferred checks never change an accept/reject verdict; they are used only to rank issues that have already passed all required checks.
