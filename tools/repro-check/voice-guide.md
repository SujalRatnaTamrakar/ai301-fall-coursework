# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a student contributor with professional software development experience
who is learning the workflow of contributing to an unfamiliar open-source
codebase.

I want my comments to be specific, evidence-based, and clear about what I
have actually verified. Maintainers should be able to distinguish what I
observed from what I plan to investigate next.


## Rules I write by

### Rule: Name the exact behavior

I name the specific behavior, command, error, or version instead of referring
generically to "the bug" or "the issue."

- Wrong: "I reproduced the bug and will work on it."
- Right: "`KeywordSearcher.index([])` raises `ZeroDivisionError`; I'll document the exact reproduction before attempting a fix."


### Rule: Promise investigation, not success

I can state what I will investigate or document next, but I do not promise a
fix, merge, or completion date before I understand the problem.

- Wrong: "I'll definitely fix this by tomorrow."
- Right: "I'll reproduce this locally first and post the environment, steps, and observed output before attempting a fix."


### Rule: Say only what the evidence shows

I do not call something reproduced merely because a command failed. I state
the observed result precisely, including when I cannot reproduce the reported
behavior.

- Wrong: "Confirmed, reproduced!" when my run produced a different exception.
- Right: "I could trigger a failure, but it is not the reported `ZeroDivisionError`, so I have not reproduced the issue yet."


### Rule: Write like myself

I keep comments direct and professional without exaggerated praise,
boilerplate enthusiasm, or assistant-like filler.

- Wrong: "I am very excited to contribute to this amazing project and resolve this issue!"
- Right: "I'm picking this up and will start by reproducing the reported empty-index failure."


## Things I never post

- A completion date I have not verified I can meet.
- A promise that I will definitely fix or merge something.
- "Reproduced" without evidence showing the reported behavior.
- Generic praise that could be pasted into any repository.
- A claim that hides a different error or failed reproduction.