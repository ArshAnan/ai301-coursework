# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Claim promises, doesn't assert | The claim comment's text | Pass if the claim comment names the specific issue behavior being investigated and states an intent to investigate/reproduce, with no assertion that the fix is already known or done, and no delivery date/ETA. Fail if it asserts a cause or fix as settled fact, commits to a date, or is generic boilerplate ("I'll take this") with no issue-specific detail | required |
| Contribution conventions followed | The claim comment and, if present, the repro report, checked against the repo's stated contribution policy / AI-disclosure requirement (CONTRIBUTING.md, AI_POLICY.md, issue or PR template — named in the repo-facts block, or found via the evidence guide's locations) | Fail if the repo's stated policy requires disclosing AI assistance and no comment discloses it, or a comment ignores an explicit stated convention (e.g. a required template field). Pass if the repo states no such requirement, or it does and the comment discloses as required | required |
| Environment recorded | The repro report's environment/setup section, read against any version/platform the issue itself targets | Pass if it names the OS, the language/runtime version actually used, and the code state run against (a commit SHA, or a branch plus "as of" date), AND, when that version/platform differs from what the issue targets (e.g. issue confirmed on latest/main, report ran on an old pinned version), the report says so out loud. Fail if any of the three is missing, is a vague stand-in ("latest version", "my machine"), or a version/platform deviation from the issue's target is left unacknowledged | required |
| Steps are complete and followable | The repro report's steps or command block | Pass if it states a starting point (fresh clone at a named commit, or a stated clean-environment setup) and then every command run, in order, with no un-named input file, flag, or intermediate action a stranger would have to guess, using only what the report itself shares (not a private/unshared config or repo). Fail if a step assumes context the report never shares, or a stranger literally could not reach the same starting point from the report alone | required |
| Behavior shown matches the issue | The report's pasted artifact (output excerpt, stack trace, or named failing test IDs), read against the issue's own description of the bug and its exact trigger (the specific input, flag, or syntax the issue names) | Pass if either: (a) the report claims reproduction and the artifact shows the same failure signature the issue names (same exception type, same failing tests, same wrong output), produced by the same trigger the issue describes, not a substituted or adjacent one; or (b) the report honestly states it could not reproduce and shows a real attempted-trigger artifact instead (even though it doesn't show the bug). Fail if it claims reproduction with no artifact quoted, with an artifact showing an unrelated/adjacent failure, or with steps that silently swap in a different trigger than the issue names | required |
| Outcome stated honestly | The report's concluding statement, read against the artifact pasted just above it | Pass if the stated outcome (reproduced / partially reproduced / could not reproduce) follows exactly from what that artifact itself shows — an evidenced, plainly-stated "could not reproduce" passes in full. Fail if the report claims a stronger result than its own artifact supports (e.g. "confirmed crash" over an artifact showing the process still alive), asserts a root cause the artifacts don't establish, or states a conclusion with no artifact backing it at all | required |
| Report is independently runnable | Environment + steps + artifact, taken together | Pass if someone with no other context could take only the report's text, land in the same environment, run the same commands, and reasonably expect the same artifact | preferred |

## Verdict rule

Accept (ready to post) only if every required check that currently applies grades pass; unclear counts as fail.

In a claim-only draft, only "Claim promises, doesn't assert" and "Contribution conventions followed" are in scope — the checks whose evidence is the repro report are not-yet-applicable and excluded from the verdict, per the claim-only rule in SKILL.md. In a full package, all required checks apply, including the two claim-only checks re-applied against the final claim comment. Preferred checks never change the verdict; they only note extra polish in the summary.
