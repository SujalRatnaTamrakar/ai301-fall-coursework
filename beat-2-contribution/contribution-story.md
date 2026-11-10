# Contribution: [DEPR]: Remove enhanced staff grader demo code

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Sujal Ratna Tamrakar
**GitHub Username:** SujalRatnaTamrakar
**Issue:** https://github.com/openedx/edx-ora2/issues/2250
**Pull Request:** Not yet opened. The draft PR is Unit 7 work; this line gets the link the day it opens.

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout from the Unit 5 starter over my Unit 1 rubric, wrote my search strategy, and ran two scans**

I installed the scout as the starter directs: the staff SKILL.md and the real-world scope.md (with my Unit 1 fit profile pasted back in) over my issue-select, keeping my own rubric.md and evidence guide, and I wrote a search strategy whose four queries trace to sentences in my fit profile. The first scan's top five were dominated by repositories created in the previous 48 hours, because ranking fresh, quiet, labelled issues first is exactly how brand-new projects surface, and my repo-in-use check could not tell a one-day-old bot-task farm from an established project; I patched repo-in-use to require a repository at least 30 days old, added a ranking drop for `no-code-needed` labels, and replaced the combined `--owner` query (which returned 0) with one repo-scoped query per project. The second scan's best candidate, a pyspedas refactoring issue, then failed `unclaimed` for the right reason: a volunteer had claimed it in the comments with no assignee anywhere, which the classroom house rule would have waved through.

**Unit 6: Claimed two issues, stood up edx-ora2 locally, and ran its test suites as the reproduction baseline**

This week's tool work was repo familiarization plus baseline evidence. I cloned edx-ora2, installed it into a virtualenv with its test dependency group, and ran the three test files that exercise the enhanced_staff_grader flag: 241 tests pass on the unmodified code (108 in test_config_mixin.py, 133 across test_staff_area.py and test_openassessment.py), which is the before picture the removal has to preserve. One honest gap: the Unit 6 voice-guard install (the starter's checker plus hook for outgoing posts) is not done yet. My two claim comments went out through the browser before the guard was in place, so they never got its draft check; the catch-up is to run the guard's draft check on my next upstream post, starting with the Unit 7 PR description, and to say so here rather than pretend the check ran.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I built my Unit 5 scout by overlaying the starter's SKILL.md and real-world scope onto my Unit 1 issue-select, keeping my own rubric and evidence guide, and ran it in two modes: broad scans over GitHub's newcomer labels, and direct grading of candidates from the organizations on the AI301 Issue Selection site. The broad scans mostly surfaced noise (brand-new repositories wearing good-first-issue labels), but the direct grading found this issue: a deprecation ticket in openedx/edx-ora2 asking for the `openresponseassessment.enhanced_staff_grader` waffle flag and its demo code to be removed. My scout's verdict was accept, and the thread backed it up in the best possible way: on October 29 a maintainer wrote "This code is dead and can be removed at any time by any interested contributor!" It fits my profile directly: Python and Django work in a production codebase, a removal with a checklist instead of an open design question, and a test suite I can run locally to prove nothing else depended on the flag. What I hope to learn is the unglamorous half of real maintenance: how a feature flag is wired through Python, templates, and JavaScript context, and how to take one out cleanly.

The honest read of the scout is that it failed once, badly, before it succeeded. My first two picks, a pair of issues in AcademySoftwareFoundation/dna, came back accept with "no linked PR" written in the evidence, and I had never actually searched for PRs: both issues already had open pull requests implementing them, one labelled "awaiting merge". I caught it only because I opened one issue on GitHub myself. The rubric's unclaimed check already named linked PRs; my grading had asserted the evidence instead of verifying it. I patched the check to require a PR search for the issue number plus a read of the issue's timeline, released the site claim I had placed on one of the dna issues, and re-screened every remaining candidate under the corrected gate. Four more candidates died on that gate (an openedx-platform test issue, two OpenCue issues, an OpenTimelineIO docs issue) before edx-ora2#2250 and OpenCue#2540 passed it. One more wrinkle worth recording: neither of my final picks appears on the Issue Selection site at all (its snapshot carries no edx-ora2 or OpenCue repositories), so both claims rest on the GitHub threads, which is also where Unit 6 says the real claim lives.

Claim comment: https://github.com/openedx/edx-ora2/issues/2250#issuecomment-6756880456 (posted 2026-11-09). Fork: https://github.com/SujalRatnaTamrakar/edx-ora2

**Toolkit**

- Tool: issue-scout, run as direct grading on candidates from the selection site's organizations after the broad label scans proved too noisy, with each verdict's evidence pulled from the issue, its comments, and the repo.
- What it produced: An accept verdict on edx-ora2#2250 backed by a maintainer's open invitation in the thread, and, just as valuable, rejects on six other candidates that looked clean at first glance.
- Difficulties: The first grading round asserted "no linked PR" for two dna issues without searching PRs; both already had open PRs, one awaiting merge. The evidence step, not the rubric text, is what failed.
- What changed: The unclaimed check now requires a PR search for the issue number and a timeline read before it can pass, and every candidate in this story was re-screened under that gate; the mis-claimed site hold was released the same evening.

---

## Understanding the Issue

**Problem Description**

The Open Response Assessment block still carries the `openresponseassessment.enhanced_staff_grader` waffle flag and the demo path it was created to protect. The enhanced staff grader is the microfrontend grader that replaced the legacy in-page staff grader. While it was rolling out, the flag decided which experience staff saw. That rollout is long over, but the flag, its settings plumbing, and the demo link are still in the code, and the deprecation ticket (open since November 2024, targeting the Teak release) asks for them to be removed so the enhanced grader is simply the default.

**Expected Behavior**

For a non-team assignment with the grading microfrontend URL configured, staff should get the "Grade Available Responses" link to the enhanced grader directly, with no flag consulted and no demo link offered. Team assignments keep the legacy grader, because the enhanced grader does not support team assignments. Nothing about grading itself changes; only the flag and the demo path go away.

**Current Behavior**

`ConfigMixin.is_enhanced_staff_grader_enabled` reads the waffle flag (default off). In the staff area, when the flag is off, staff see the legacy "Grade Available Responses" button plus a second link, "Demo the new Grading Experience", which opens the enhanced grader as a demo they cannot actually grade from. When the flag is on, they get the enhanced grader link instead. The flag is also passed into the course listing block's JavaScript context as `ENHANCED_STAFF_GRADER`.

**Affected Components**

- `src/openassessment/xblock/config_mixin.py`: the `ENHANCED_STAFF_GRADER` constant, its entry in `FEATURE_TOGGLES_BY_FLAG_NAME`, and the `is_enhanced_staff_grader_enabled` property with its toggle annotations.
- `src/openassessment/xblock/staff_area_mixin.py`: the staff-info context that sets `is_enhanced_staff_grader_enabled` and `enhanced_staff_grader_url` (carrying a "TODO: Remove in AU-617" note).
- `src/openassessment/xblock/openassessmentblock.py`: the listing view's JavaScript context passing `ENHANCED_STAFF_GRADER`.
- `src/openassessment/templates/legacy/staff_area/oa_staff_area.html`: the conditional that renders either the enhanced link, or the legacy button plus the demo link.
- Tests: `test_config_mixin.py`, `test_staff_area.py`, `test_openassessment.py`, plus the JS template fixtures that snapshot the flag.

**Toolkit**

- Tool: The issue thread itself plus direct code inspection of my clone: the DEPR's removal checklist mapped onto the current tree, every `enhanced_staff_grader` reference found by search.
- What it produced: The four-field picture above, with each claim tied to a file and line I opened, not just to the ticket text.
- Difficulties: The ticket's links point at pre-2025 paths (`openassessment/xblock/...`); the code now lives under `src/openassessment/...`, so every checklist line had to be re-located by search rather than followed.
- What changed: Nothing in the tools; the plan below uses the current `src/` paths throughout.

---

## Reproduction Process

**Environment Setup**

Linux (Ubuntu) virtual machine, Python 3.12. I cloned openedx/edx-ora2 (my fork: SujalRatnaTamrakar/edx-ora2), created a virtualenv, installed the project editable (`pip install -e .`), then added the test dependency group from pyproject.toml (pytest, pytest-django, pytest-cov, ddt, factory-boy, freezegun, moto, testfixtures, xblock-sdk, celery). Tests run with the repo's own pytest.ini, which sets `--ds=settings.base`. Two setup challenges: the first test run failed on a missing `workbench` module (xblock-sdk not yet installed), and the coverage options in pytest.ini need pytest-cov present even for a quick run. Both were solved by installing the full test group rather than guessing package by package.

**Steps to Reproduce**

A deprecation has no crash to trigger, so reproduction means demonstrating the flag-gated demo behavior the ticket wants gone, at the level the repo itself tests it:

1. With the unmodified code, run the three test files that exercise the flag: `pytest src/openassessment/xblock/test/test_config_mixin.py src/openassessment/xblock/test/test_staff_area.py src/openassessment/xblock/test/test_openassessment.py`.
2. Read `test_enhanced_staff_grader_enabled` in test_config_mixin.py: it parameterizes the waffle flag and settings inputs and shows the property following the flag.
3. Read the staff-area context tests and the legacy template: with the flag off, the context and template produce the legacy grading button plus the "Demo the new Grading Experience" link; with it on, the enhanced grader link.
4. Observed result: the demo path is real, reachable, and covered by tests, exactly as the ticket describes.

**Reproduction Evidence**

- **Commit showing reproduction:** No fork commit yet; the baseline was run on a clean clone of upstream master and the removal branch is Unit 7 work. The baseline numbers below are the reproduction record for this week.
- **Screenshots/logs:** Baseline run, 2026-11-09: `test_config_mixin.py` 108 passed; `test_staff_area.py` + `test_openassessment.py` 133 passed (241 total across the flag's test surface, unmodified code).
- **My findings:** The flag's footprint is exactly where the ticket says, plus two places the ticket does not list: the JS template fixtures that snapshot it, and the listing view's JavaScript context. The staff-area mixin even carries the maintainers' own "TODO: Remove in AU-617" over the flag check. The one judgment call the removal forces: `is_enhanced_staff_grader_enabled` is also forced to False for team assignments in the staff context, so the removal has to preserve the team exception while deleting the flag, which the ticket's replacement template does by keying on the team flag and the grader URL instead.

**Toolkit**

- Tool: repro-check, used in its real-repo form: reproduce the reported behavior on the unmodified project and record observable evidence before planning the change.
- What it produced: A green 241-test baseline across the flag's three test files, plus a complete reference map of the flag (code, template, JS context, fixtures, tests).
- Difficulties: A removal has no failing case to reproduce; the honest equivalent is showing the gated behavior exists and is exercised, which is what the baseline and the template read establish.
- What changed: Nothing in the tool. The reproduction steps above are written so they can be re-run verbatim after the removal, when the same suites must pass with the flag-specific tests deleted or rewritten.

---

## Solution Approach

**Analysis**

The "bug" is a finished rollout that never got cleaned up. The flag lives in `ConfigMixin` (constant, toggle registry, and the `is_enhanced_staff_grader_enabled` property), and three consumers read it: the staff-area context (which also special-cases team assignments to False), the legacy staff template (which turns the flag plus the microfrontend URL into one of three renderings: enhanced link, or legacy button, or legacy button plus demo link), and the course listing view (which passes the flag into JavaScript). Removing the flag means each consumer collapses to its post-rollout behavior: enhanced link whenever the assignment is not a team assignment and the URL is configured, legacy button otherwise, demo link gone.

**Proposed Solution**

Delete the flag and make the enhanced grader unconditional, following the ticket's own replacement snippet for the template. Deliberately NOT changing: the legacy staff grader itself (it stays for team assignments and for courses without the microfrontend URL configured), the `enhanced_staff_grader_url` context value (still built from `ORA_GRADING_MICROFRONTEND_URL`), and any grading logic. This is a removal, not a redesign: if a line is not about the flag or the demo path, it does not move.

**Implementation Plan**

1. `config_mixin.py`: remove the `ENHANCED_STAFF_GRADER` constant, its `FEATURE_TOGGLES_BY_FLAG_NAME` entry, and the `is_enhanced_staff_grader_enabled` property with its toggle annotation block.
2. `staff_area_mixin.py`: stop setting `is_enhanced_staff_grader_enabled` in the staff-info context (resolving the AU-617 TODO); keep setting `enhanced_staff_grader_url`.
3. `oa_staff_area.html`: replace the flag conditional with the ticket's replacement shape, keyed on the existing context variables: enhanced link when the assignment is not a team assignment and the URL is set, legacy button otherwise; delete the demo link block.
4. `openassessmentblock.py`: remove `ENHANCED_STAFF_GRADER` from the listing view's JavaScript context, and check the listing JavaScript for reads of it before deciding whether a JS change rides along.
5. Tests: delete the flag parameterization in `test_config_mixin.py`'s toggle test (or reduce it to the remaining toggles), rewrite the staff-area context tests that patch `is_enhanced_staff_grader_enabled`, update `test_openassessment.py`'s two patch sites, and refresh the JS template fixtures.
6. Re-run the three baseline suites, then the full Python test suite, and finish with a tree-wide search for `enhanced_staff_grader` / `ENHANCED_STAFF_GRADER` / `ENABLE_ENHANCED_STAFF_GRADER` showing only historical docs, if any.

Deviation recorded at planning time, before any code moved: the ticket's checklist uses pre-2025 paths without the `src/` prefix and its template snippet names the variable `team_assignment`, where the current template uses `is_team_assignment`. The plan follows the current tree, not the ticket's snapshot of it.

**Toolkit**

- Tool: plan-check, used in its real-repo form: the plan is traced line by line against the ticket's removal checklist and against the reference map from reproduction.
- What it produced: The six-step plan above, including the two consumers the ticket does not mention (JavaScript context, fixtures) that the reference map caught.
- Difficulties: The ticket's paths and template snippet are a release old; planning against them literally would have edited files that no longer exist at those paths.
- What changed: Nothing in the tool. The deviation is recorded in the plan itself, where the rubric can see it, instead of being discovered during the build.

---

## Testing Strategy

Before and after, same commands. Before (done, 2026-11-09): the three flag test files pass 241 tests on unmodified code. After the removal: (1) the same three files, with the flag-specific tests deleted or rewritten, must pass; (2) the full Python suite (`pytest` at the repo root, per tox.ini's quality env minus lint) must show no new failures against the baseline; (3) a tree-wide search for the flag's three names must return no live code references; (4) the staff-area context tests must show the context no longer carries `is_enhanced_staff_grader_enabled` while still carrying `enhanced_staff_grader_url`; (5) if the listing JavaScript reads the removed context key, the JS tests (`karma`) for the listing block get run too, otherwise the removal of the key is justified in the PR description.

**Toolkit**

- Tool: The repo's own pytest suite under its shipped pytest.ini (Django settings `settings.base`), used as the measuring instrument.
- What it produced: A named, countable baseline (241 tests over three files) and a five-point after-check that a reviewer can re-run exactly.
- Difficulties: The suite needs the full test dependency group (including xblock-sdk and pytest-cov) before it runs at all; a partial install fails in confusing places.
- What changed: Nothing yet; the strategy is written to be executed in Unit 7 and its results recorded in Implementation Notes as they land.

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**2026-11-09**

Claimed the issue (comment linked in Why I Chose This Issue), forked the repo, stood it up locally, and ran the baseline: 241 tests passing across the three files that exercise the flag. Mapped every `enhanced_staff_grader` reference in the tree and wrote the removal plan against the current `src/` layout. No upstream code changed yet; the removal itself is Unit 7.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]

---

# Contribution 2: [cueweb] Scope the Stuck Frames page to a single show

**Contribution Number:** 2
**Student:** Sujal Ratna Tamrakar
**GitHub Username:** SujalRatnaTamrakar
**Issue:** https://github.com/AcademySoftwareFoundation/OpenCue/issues/2540
**Pull Request:** Not yet opened. Claimed 2026-11-09; the build follows the edx-ora2 contribution above.

## Why I Chose This Issue

My scout's second accept under the corrected no-PR gate. OpenCue is the Academy Software Foundation's production render manager (originally Sony Pictures Imageworks), and this issue is a scoped enhancement in its web UI, CueWeb: the Stuck Frames page currently reports stuck frames across every show at once, and the issue asks for it to default to a single selected show, with a selector at the top and the selection persisting across visits. It graded accept on a detailed body that names the exact files (`cueweb/app/stuck-frames/page.tsx`, `cueweb/app/api/stuck-frames/route.ts`) and the docs and screenshot updates expected. One soft spot, recorded rather than smoothed over: a newcomer commented on 2026-10-16 asking to take it on, received no reply, and sent no PR; my claim comment acknowledges that comment explicitly and offers to coordinate or step aside.

Like the edx-ora2 pick, this issue does not appear on the Issue Selection site (its snapshot has no OpenCue repository), so the claim rests on the GitHub thread.

Claim comment: https://github.com/AcademySoftwareFoundation/OpenCue/issues/2540#issuecomment-6756889763 (posted 2026-11-09). Fork: https://github.com/SujalRatnaTamrakar/OpenCue

## Understanding the Issue

**Problem Description**

Production support staff work one show at a time, but the Stuck Frames page aggregates stuck frames from every show on the farm, so staff page through other shows' frames to find their own, and every refresh makes the server scan every show's jobs.

**Expected Behavior**

The page defaults to one selected show, offers a show selector at the top, remembers the selection across visits, and the API route scopes its scan to the selected show. Showing all shows at once should at most be an explicit opt-in.

**Current Behavior**

The API route (`cueweb/app/api/stuck-frames/route.ts`, 163 lines) lists unfinished jobs across all shows and fans out per job for frames and layers; the page (`cueweb/app/stuck-frames/page.tsx`, 622 lines) renders everything it receives. There is no show selector and no show parameter anywhere in the flow.

**Affected Components**

`cueweb/app/stuck-frames/page.tsx` (selector UI, persisted selection, filtering), `cueweb/app/api/stuck-frames/route.ts` (show-scoped query), plus the CueWeb docs pages and screenshots the issue lists.

## Status

Claimed and understood; reproduction, plan, and build are sequenced after Contribution 1 and will be recorded here as they happen, with dated Implementation Notes, before the Unit 8 submission.
