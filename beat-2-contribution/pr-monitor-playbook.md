# PR Monitor Playbook — openedx/edx-ora2 PR #2483

Scope: draft PR https://github.com/openedx/edx-ora2/pull/2483
("refactor: remove enhanced_staff_grader waffle flag and demo code", fixes #2250),
opened 2026-11-09 from fork branch `remove-enhanced-staff-grader-flag`.

## Check cadence

- On any GitHub notification for the PR (review, comment, check failure): same day.
- Otherwise: every 3 days while the PR is open and unreviewed.
- After a maintainer engages: daily until merge or close.

## Thresholds and decisions

| Signal | Threshold | Decision |
| --- | --- | --- |
| CI check fails | Failure is in code this PR touched | Fix on the fork branch within 1 day, push, note the fix in the story |
| CI check fails | Failure matches the pre-existing baseline set (identical failures on unmodified master in the same environment) | Comment on the PR with the before/after evidence; do not chase unrelated failures |
| No CI jobs run | Still true after 3 days | Note it in the next monitor entry; Open edX fork PRs often wait on maintainer-approved runs, so no action beyond recording |
| Reviewer comment or change request | Any | Respond within 1 business day; accept or decline each point with a reason, mirroring the Unit 7 peer-review habit |
| CLA check pending/failing | Any | The signature is Sujal's own account step; flag it, never work around it |
| Silence (no human comment, no review) | 14 days from opening | One polite ping comment on the PR tagging the maintenance team named in the repo's welcome comment (`@openedx/openedx-unmaintained`) |
| PR approved | Any | Move it out of draft ("Ready for Review") if not already; say thanks; record the outcome in the story |
| PR closed without merge | Any | Record the reason in the story; the contribution is graded as opened, so no re-attempt without a new decision |

## Escalation

Nothing in this playbook sends a message on its own. Any ping, reply, or
status change is drafted first and goes out only as a deliberate action,
consistent with how the claim comments and this PR were handled.
