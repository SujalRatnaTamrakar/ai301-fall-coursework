# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

### Where it lives

In eval mode, read the repro report's environment record and compare it
with the issue context, repo-facts block, and any repository requirement
about testing a particular version, release, branch, platform, or runtime.

In live mode, compare the student's recorded environment with the issue,
repository setup documentation, contribution instructions, and bug-report
template.

### What good looks like

The tested software version or commit and relevant OS/runtime environment
are identifiable, and they support the conclusion the report makes.

For a successful reproduction, explicit repository or issue requirements
such as testing the latest release or current main branch must be satisfied
unless the report gives a concrete reason the difference does not affect
the conclusion.

For a cannot-reproduce result, a different environment can still be useful
evidence when the differences are clearly stated and the conclusion is
limited to that tested environment.


## Steps

### Where it lives

In eval mode, use the setup/reproduction instructions, command blocks,
inputs, and stated starting conditions in the repro report.

In live mode, use the student's reproduction steps together with any
standard setup already documented by the repository.

### What good looks like

Another contributor can repeat the documented attempt without inventing
a detail that is essential to triggering or observing the target behavior.

The report does not need to spell out incidental file contents or repeat
ordinary setup that is already established by the environment record or
repository documentation.

For a cannot-reproduce report, the steps are sufficient when another
contributor could repeat the same test and verify the reported observed
result. They do not have to reproduce the original bug.


## Behavior shown

### Where it lives

Compare the original issue's described failure with the repro report's
expected behavior, actual behavior, terminal output, traceback, tests,
screenshots, logs, or other attached evidence.

### What good looks like

The artifact directly supports the behavior the report says occurred and
targets the same behavior described by the issue.

A different error is not treated as successful reproduction merely because
something failed. A cannot-reproduce result is valid when its observed
behavior is shown clearly.


## Honesty

### Where it lives

Read the report's conclusion and reproduction claim against the steps and
supporting artifacts.

### What good looks like

The wording does not claim more than the evidence demonstrates.

"Reproduced" is used only when the target behavior was actually observed.
If the target behavior was not reproduced, the report says so and records
what happened instead.


## Comms

### Where it lives

In eval mode, read the claim comment and repro comment against repository
contribution policies and templates.

In live mode, compare the student's draft comments with the issue thread,
CONTRIBUTING/README instructions, templates, and any AI-use policy.

### What good looks like

The claim names the specific issue behavior and states the next concrete
step without promising a fix or completion date.

The repro comment is specific to the issue, accurately describes the
evidence, and satisfies explicit repository requirements, including
AI-assistance disclosure when the repository requires it.
