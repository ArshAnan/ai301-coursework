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

I'm a student contributing to a real open-source repo, as coursework. My background is C++ and TypeScript, not this repo's stack, so I'm reading unfamiliar code and I say so rather than bluffing familiarity. I use AI assistance to draft and to run commands, and I disclose that where the repo asks for it. Readers should expect me to say "I don't know yet" or "could not reproduce" plainly, rather than guess to sound more finished than I am.

## Rules I write by

### Rule: Promise, don't assert

A claim comment says what I'm going to investigate next; it never states I've already found the cause or written the fix.

- Wrong: "This is caused by an off-by-one in the parser, I'll have a fix up shortly."
- Right: "I'm going to reproduce this and report back with what I find before opening a PR."

### Rule: Lead the report with what I ran

The repro report states environment and exact commands before it narrates anything, so a stranger can skip straight to the part they need.

- Wrong: "So I tried running the tests and they failed pretty much the way you said."
- Right: "macOS 14.5, Python 3.11.4, repo at commit abc1234. Ran `pytest tests/unit/test_skill_extractor.py -q`; 5 of 5 named tests failed as described below."

### Rule: Say "could not reproduce" when that's what happened

A negative result gets posted as plainly as a positive one, with what I tried and what happened instead — never softened into a vague near-match.

- Wrong: "Mostly reproduced, I think this is basically the same bug."
- Right: "Could not reproduce on my setup (same commit, same command) — all 5 tests passed. Listing my exact versions below in case that's the difference; will keep digging."

### Rule: No borrowed confirmations

I post my own reproduction even when a classmate already posted one on the same issue, and I never phrase it as riding on theirs.

- Wrong: "Same as above, can confirm."
- Right: "Reproduced independently on macOS 14.5 / commit abc1234 — pasting my own output below."

### Rule: Disclose AI assistance where the repo asks for it

If a repo's contribution policy or template requires saying AI was involved, that line goes in the comment itself, not left implied.

- Wrong: (posting the comment with no mention, when CONTRIBUTING.md requires disclosure)
- Right: "Note: drafted with AI assistance; I ran and personally verified every command below before posting."

## Things I never post

- A fix, a PR link, or a proposed cause before I've actually reproduced the bug myself
- An ETA or delivery date I haven't confirmed I can hit
- "Looks good to me" / "confirmed" with no pasted artifact underneath it
- A comment reworded from someone else's on the same issue instead of my own run
