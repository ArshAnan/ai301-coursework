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

Where it lives: in an eval bundle, the repro report's own "Environment" or "Setup" section, usually a few lines near the top before the steps. In live mode, the same section inside the student's own draft — there's nothing to look up on GitHub for this family, since it's a claim about the student's own machine, not a fact the repo publishes.

What good looks like: names the OS (e.g. "macOS 14.5", "Ubuntu 22.04 in a sandbox container"), the language/runtime version actually used (e.g. "Python 3.11.4", not "Python 3"), and the exact code state run against (a commit SHA, or a branch name plus a capture/clone date). Also check this version/commit against whatever the issue itself targets (its own "confirmed on version X" or "latest/main" language, found in the issue context / repo-facts block): the versions named match what the issue targets, or the difference is called out by the report itself. "Ran on my machine" or "latest version" is not sufficient; a version a stranger could match against their own setup is, and a silent, undisclosed version gap is the same failure as no environment record at all.

## Steps

Where it lives: the repro report's numbered steps or fenced command block, in both the bundle and the student's draft.

What good looks like: states the starting point (a fresh clone at a named commit, or "clean venv, `pip install -r requirements.txt`"), then every command actually run, in order, with any input files, fixtures, or flags named explicitly rather than assumed. A stranger holding only the report text should be able to type the same commands and land in the same state — no "then I set it up the usual way," and no reference to a private repo, unshared config, or local-only fixture the report never includes.

## Behavior shown

Where it lives: pasted output, a stack trace, or named failing test IDs inside the repro report; compare against the issue body's own description of the bug **and its exact trigger** — the specific input, flag, or syntax the issue names — plus, in live mode, any linked test names or error text quoted in the issue thread itself (fetch the issue live; in eval mode this is the "issue context" section of the bundle).

What good looks like: the artifact contains the same failure signature the issue names — the same exception type, the same failing test IDs, the same wrong output — produced by running the same trigger the issue describes, not a different or nearby-looking trigger (a changed flag, a swapped character, a different code path) that happens to also error. A report that pastes a real stack trace but never connects it back to what the issue described, or that quietly used a different input than the issue names, is missing the part this check actually grades. The one exception: an honest "could not reproduce" report still needs a real attempted-trigger artifact (showing what was tried and what came back instead), even though that artifact by definition won't show the bug.

## Honesty

Where it lives: the report's own concluding sentence(s), read directly against the artifact pasted just above them, in both bundle and live mode.

What good looks like: the stated outcome is exactly what the artifact supports. "Reproduced: <artifact showing the full symptom>" passes; so does "Could not reproduce on <environment>: ran the same command, all tests passed instead — possible version mismatch, my versions listed above," stated plainly with no spin. Fails are reports that say "confirmed" or "reproduced" while the pasted output shows something partial, adjacent, or absent entirely.

## Comms

Where it lives: the repo's CONTRIBUTING.md / AI_POLICY.md / issue or PR template — named under "contribution policy" in the repo-facts block in eval mode, or found in the repo root / `.github/` in live mode — read against the actual text of the claim comment and repro comment.

What good looks like: if the repo's policy requires disclosing AI assistance, the comment says so plainly, not buried in a footnote or omitted; if the policy is silent, no disclosure is required and silence passes. Separately, the comment text speaks to the issue's own specifics (names the function, the behavior, the failing test) rather than reusing boilerplate generic enough to paste onto any issue in the repo.
