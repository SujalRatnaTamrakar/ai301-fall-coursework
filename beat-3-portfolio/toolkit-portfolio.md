# Toolkit Portfolio

**Student:** Sujal Ratna Tamrakar

## Featured Tools

I am featuring the four tools that changed the most through use. issue-select and
issue-scout both had a check fail in the real world and were rewritten because of
it; pr-precheck and pr-monitor are here because each one caught, or was built to
catch, a problem that a checklist alone would have missed.

**issue-select**

**What it is, and the judgment hole I wrote:** A skill that grades a candidate
issue against a rubric I wrote — seven checks (maintainer-alive,
responds-to-issues, repo-in-use, scope-coherent, implementation-ready,
unclaimed, contribution-policy) plus a verdict rule: accept only if every
required check passes, and a required check graded unclear counts as a failure.
The judgment is in the pass conditions: each one names a source and a countable
threshold, like maintainer-alive's "at least 2 of the last 5 human commits
within 90 days."

**How it evolved, dated:** The first version (September 2026) had a single
`scope-bounded` check. The first full harness eval scored 16/20 agreement with
the gold labels, disagreeing on issue-04, issue-15, issue-19, and issue-20: the
one check was too strict for some coherent issues and too loose to catch hidden
complexity in others. I replaced it with two required checks, `scope-coherent`
and `implementation-ready`, and clarified `unclaimed` so explicitly released or
abandoned claims do not count as active. The targeted re-run of the four
disagreements matched gold 4/4; the final full eval scored 19/20 PASS, with
issue-04 the one remaining disagreement (gold accept, my verdict reject, failed
on `implementation-ready`).

**Evidence:** The final run's own table, from the committed eval-run.txt
(2026-09-23): "issue-04 accept reject NO failed: implementation-ready" and
"agreement: 19/20 scored items (bar: 18/20: PASS)". The replacement check as it
now stands in the rubric: "The issue describes one coherent problem or outcome
that a contributor can work toward. Multiple related substeps, causes, or
implementation suggestions are allowed when they all address the same outcome."

**issue-scout**

**What it is, and the judgment hole I wrote:** The Beat 2 overlay of
issue-select for finding a real open-source contribution: the course starter's
SKILL.md and real-world scope with my fit profile pasted in, my own search
strategy (one `gh search issues` command per profile sentence, `--state open`,
`--limit 100`), and my Beat 1 rubric carried over unchanged at first. The
judgment is the same rubric, now applied to live repositories instead of
snapshots.

**How it evolved, dated:** On 2026-11-09 the scout graded two
AcademySoftwareFoundation/dna issues ACCEPT, and I claimed one on the selection
site — then spotted on GitHub that both already had open PRs implementing them
(PR #264 fixes #255; PR #262 fixes #254). The issues showed no assignee and
zero comments, and my `unclaimed` check had asserted "no linked PR" without
ever searching pull requests. I released the claim, strengthened `unclaimed`
with an explicit verification method (search the repo's PRs for the issue
number and read the issue's timeline cross-references), added a
`repo-in-use` condition that the repo be at least 30 days old after the first
scan's top hits were days-old throwaway repos, and re-screened every remaining
candidate under the corrected gate.

**Evidence:** The `unclaimed` row, before: "The issue is open and has no
assignee, claim comment, linked branch, or linked PR indicating that another
contributor is actively working on it." After (2026-11-09): "This must be
verified, not assumed: search the repo's pull requests for the issue number and
read the issue's timeline cross-references — an issue can show no assignee and
zero comments while an open PR already implements it." Under the corrected
gate the scout rejected openedx/openedx-platform#37611 (open PR #39045),
OpenCue#2536 (closed PR #2550), OpenCue#2538 (open PR #2547), and
OpenTimelineIO#2042 (PRs already sent), and accepted edx-ora2#2250 and
OpenCue#2540, both verified PR-free.

**pr-precheck**

**What it is, and the judgment hole I wrote:** A pre-submission check for a
pull request: it sweeps the change for leftover references, scope creep, and
unverified claims before the PR goes up. The judgment is in what counts as
blocking — a dangling reference to a removed symbol blocks; a build artifact
containing the same string does not.

**How it evolved, dated:** Built in Unit 4 (October 2026) and graded by the
harness at 18/20 PASS on its first full eval (2026-10-13), the only Beat 1 tool
that passed cleanly as first written, so it changed the least of the featured
four. Its real test came on 2026-11-09, when the same sweep discipline applied
to the edx-ora2 removal caught a second JS consumer of the flag,
`StaffCell.shouldShowLink`, still reading the removed context key — a reference
the ticket's own checklist never mentioned.

**Evidence:** Harness eval for Unit 4: 18/20 PASS (2026-10-13). The catch it
generalized from, in the shipped diff: `StaffCell.shouldShowLink` returned
`team_assignment || !esgEnabled`; after the sweep it depends only on the
team-assignment check, and the "Remove this in AU-617" comment went with it.

**pr-monitor**

**What it is, and the judgment hole I wrote:** A monitoring routine plus a
playbook I wrote for a submitted PR: check on any notification the same day,
otherwise every three days; fix my own CI failures within one day; respond to
reviewer comments within one business day; never ping before 14 days of
silence, and then one polite ping. The judgment is the thresholds — they are
mine, set before the first run, so the run's decision follows the playbook
instead of my mood that day.

**How it evolved, dated:** Written and first run on 2026-11-09, the day PR
#2483 opened as a draft. It has had one real decision so far: Run 1 found the
PR draft and open, zero reviews, one bot comment (the Open edX CLA notice —
signing the CLA is my step, not something the monitor can do), and checks that
ran with no jobs, so the playbook's answer was WAIT with the next check on
2026-11-12. A manual recheck on 2026-11-16 found the same state; no ping was
sent, because the 14-day threshold had not been reached.

**Evidence:** Run 1, recorded 2026-11-09 in pr-monitor-output.md: "PR
#2483 — draft/open, 0 reviews, 1 bot comment (CLA), checks ran with no jobs;
decision: WAIT; next check 2026-11-12."

## Inventory

- repro-check: Beat 1 reproduction skill — documents an issue's failure with environment, exact steps, and observed output before any fix is planned; harness eval 20/20 PASS.
- plan-check: Beat 1 planning skill — turns a reproduced issue into a bounded, file-level fix plan traced to the issue; completed late in Unit 3 after the graded snapshot caught template files in place of the finished skill.

## The Arc

**Beat 1**
Date: September 2026
Friction: My single scope-bounded check disagreed with the gold labels on 4 of 20 eval issues — too strict for some coherent issues, too loose on hidden complexity.
Change: Split it into two required checks, scope-coherent and implementation-ready, and clarified the unclaimed check's treatment of released claims.
Result: Final full eval 19/20 PASS; the four disagreements re-run in isolation matched gold 4/4, and issue-04 remains the documented single miss.

**Beat 2**
Date: 2026-11-09
Friction: The scout accepted two dna issues that already had open PRs implementing them; I had claimed one before noticing, because unclaimed was asserted from the issue page alone.
Change: Patched unclaimed to require a PR search for the issue number plus a timeline read, added a 30-day minimum repo age to repo-in-use, released the claim, and re-screened all candidates.
Result: The corrected gate rejected four more already-claimed or already-implemented candidates and accepted edx-ora2#2250 and OpenCue#2540, both of which I claimed for real.

**Beat 3**
Date: 2026-11-09
Friction: A draft PR can sit unreviewed indefinitely, and checking it by feel either nags maintainers too early or notices a review too late.
Change: Wrote the pr-monitor playbook with fixed thresholds (same-day on notification, otherwise every 3 days; respond within 1 business day; no ping before 14 days of silence) and ran it the day the PR opened.
Result: Run 1 decided WAIT with a dated next check; the 2026-11-16 recheck confirmed no change and no premature ping was sent.

## Limitations and What's Next

The toolkit's checks are only as strong as their verification steps, and two of
mine are still manual. The scout's patched `unclaimed` check says to search PRs
and read the timeline, but nothing enforces that the search actually ran — the
dna mistake is prevented by discipline, not by mechanism. issue-select's
`implementation-ready` still bundles several failure modes into one check,
which is exactly why issue-04 still disagrees with gold: two reviewers can
apply it differently. pr-monitor's thresholds are only as good as the checks
behind them, and PR #2483's CI ran with no jobs, so the monitor has never yet
seen a real failing check to route. Next I would split `implementation-ready`
into separate countable checks the way `scope-bounded` was split, script the
scout's PR-search step so the output is pasted into the grading record
automatically, and give pr-monitor a PR whose CI actually runs, so its failure
path gets exercised at least once.

**Tool limits.** One line per featured tool, in the same order as the entries above.

issue-select: implementation-ready still compounds several failure modes into one pass condition, so borderline issues like issue-04 can flip between runs.
issue-scout: the PR-search verification for unclaimed is a written instruction, not an enforced step — skip it and the tool repeats the dna mistake.
pr-precheck: its sweep follows names I give it; a symbol renamed as it crosses into a template or JS context is caught only if I think to grep the second name too.
pr-monitor: it can only report and wait — the CLA signature, the review, and the merge are all human steps it cannot move.
