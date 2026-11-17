# Removing a dead feature flag from Open edX, and fixing the tool that chose the issue

## Overview

This term I contributed to openedx/edx-ora2, the open-response assessment engine behind Open edX courses, by removing the retired `enhanced_staff_grader` feature flag and its demo code, as proposed in deprecation ticket #2250. The issue was chosen by a tool I built, issue-scout: a rubric-based checker assembled by overlaying the Unit 5 starter's skill and scope files onto my Unit 1 issue-select skill, keeping my own rubric and evidence guide — the rubric, fit profile, and search strategy are the parts I wrote. The scout's first two picks were wrong in a way that taught me more than the fix did: both already had open pull requests implementing them. I patched the rubric check that had failed, re-screened every candidate under the corrected gate, and the surviving pick became the contribution. I opened the fix as draft pull request #2483 on November 9, 2026 (https://github.com/openedx/edx-ora2/pull/2483); it is still open today, awaiting maintainer review and my signed contributor agreement.

## What happened

### The scout, and its first failure

I built the scout in Unit 5 and ran it two ways: broad GitHub scans over newcomer labels, and direct grading of candidates from organizations on the course's Issue Selection site. The broad scans mostly surfaced noise (repositories a day old wearing good-first-issue labels, a bot-task farm), and the scan friction produced the first rubric patches, logged in my scan notes: `repo-in-use` gained a 30-day minimum repo age, and a ranking filter dropped results labelled `no-code-needed`.

The direct grading then produced two confident accepts: AcademySoftwareFoundation/dna#255 and dna#254. I claimed #255 on the selection site. The grades were wrong. Both issues already had open pull requests from October 31 implementing exactly what they asked for — PR #264 for #255, PR #262 for #254. My evidence for the `unclaimed` check had said "no linked PR," and I had never searched for one. I caught it by opening one of the issues on GitHub myself and seeing the pull request the checker had missed.

### The change: a check that has to be verified, not asserted

The rubric's `unclaimed` row already named linked pull requests; what it did not do was force the grader to look. I patched the row the same day. Before:

> unclaimed — There is no current assignee, no open linked pull request implementing the issue, and no fresh claim showing that another contributor is actively working on it. Old claims that were explicitly released or abandoned do not fail this check.

After:

> unclaimed — There is no current assignee, no open linked pull request implementing the issue, and no fresh claim showing that another contributor is actively working on it. This must be verified, not assumed: search the repo's pull requests for the issue number and read the issue's timeline cross-references — an issue can show no assignee and zero comments while an open PR already implements it. Old claims that were explicitly released or abandoned do not fail this check.

I released the site claim on dna#255, corrected the verdicts in my scan output, and re-screened everything under the patched gate. That re-screen is where the patch paid off immediately: the corrected check killed four more candidates that looked clean on the surface — openedx/openedx-platform#37611 (open PR #39045), OpenCue#2536 and #2538 (PRs already sent), and OpenTimelineIO#2042 (PRs sent). The tool's next run caught, four times, exactly what its first version had missed.

### The contribution the corrected scout found

edx-ora2#2250 passed every check, including the patched `unclaimed` (a pull-request search for the issue number returned zero). The thread also carried the strongest signal a deprecation ticket can have, from a maintainer on October 29, 2026:

> This code is dead and can be removed at any time by any interested contributor!

I claimed the issue with a comment linking my course repo, forked, and set the project up locally. Before touching code I baselined the three test files that exercise the flag: 241 tests passing (108 in `test_config_mixin.py`, 133 across `test_staff_area.py` and `test_openassessment.py`). The removal then followed the ticket's checklist, adjusted to the current `src/` layout: the flag constant, its registry entry, and the `is_enhanced_staff_grader_enabled` property out of `config_mixin.py`; the staff-area context cleaned up; the listing view's JavaScript context slimmed; and the staff-area template switched to the shape the ticket itself proposed, with the demo link deleted:

```diff
-            {% if is_enhanced_staff_grader_enabled and enhanced_staff_grader_url %}
+            {% if not is_team_assignment and enhanced_staff_grader_url %}
                 <a href="{{enhanced_staff_grader_url}}" class="ui-staff__button button-enhanced-staff-grader" aria-expanded="false">{% trans "Grade Available Responses" %} <span class="icon fa fa-external-link" aria-hidden="true"></span></a>
             {% else %}
                 <button class="ui-staff__button button-staff-grading" aria-expanded="false" data-panel="openassessment__staff-grading">{% trans "Grade Available Responses" %}</button>
-                {% comment %} Remove if block in AU-617 {% endcomment %}
-                {% if not is_team_assignment and enhanced_staff_grader_url %}
-                    <a href="{{enhanced_staff_grader_url}}" class="ui-staff__button button-enhanced-staff-grader button-enhanced-staff-grader-demo" aria-expanded="false">{% trans "Demo the new Grading Experience" %} <span class="icon fa fa-external-link" aria-hidden="true"></span></a>
-                {% endif %}
             {% endif %}
```

The build produced a second change of my own work. My first JavaScript edit removed the flag variable from the course-listing code, and a tree-wide sweep for the flag's name, run as a pre-PR gate, caught a second consumer I had missed — `StaffCell.shouldShowLink`, still reading the variable I had deleted. I fixed it to key on team assignments only. The test updates held one more surprise: the upstream listing test's "assertion" about the flag turned out to assign into the parsed JSON instead of asserting anything, so I replaced it with a real assertion that the flag is absent from the context and the grading URL is present.

The ship evidence, before the PR opened: the three flag suites pass 212 tests with the change (241 before; the 29 difference is exactly the deleted flag-parameterized cases), and the full Python suite produced an identical failure count on my branch and on unmodified master in the same environment:

```
408 failed, 1406 passed, 1 skipped   (unmodified master)
408 failed, 1377 passed, 1 skipped   (this change)
```

The 408 are pre-existing environment failures, proven pre-existing by the stashed baseline run rather than asserted to be. I opened draft PR #2483 that evening. In Unit 8 I wrote a monitoring playbook for it (check every 3 days, respond to feedback within one business day, no ping before 14 days of silence) and ran the first check the same night: draft, no reviews, one automated comment, decision — wait.

## Limitations and what's next

The honest limits are these. The pull request is still a draft and unmerged a week later; no maintainer has reviewed it yet, the project's CI has not run a single job on it ("workflow runs completed with no jobs"), and my local test evidence, however carefully baselined, is not a green build. The Open edX contributor agreement the project requires is still unsigned — that step is mine alone, and until it is done the PR cannot merge however good the code is. The JavaScript changes were never run under the project's karma suite in my environment; they are syntax-checked and mirror the tested Python behavior, nothing more. And the scout's patched check still depends on the grader actually performing the PR search: the rubric describes the verification, but nothing enforces it mechanically, which is how the original failure happened.

Next, in order: sign the contributor agreement, mark PR #2483 ready for review, and keep it under the playbook until a maintainer engages. For the scout, the follow-up I owe it is a scripted PR-search step, so the `unclaimed` verdict is produced by a query result pasted into the scan output rather than by a grader's say-so. The second contribution the scout found, OpenCue#2540, is implemented and pushed to my fork; its pull request waits until I have tested the change myself — a rule I set after the dna miss, and one I intend to keep.
