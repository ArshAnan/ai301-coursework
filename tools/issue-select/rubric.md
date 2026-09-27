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
| Maintainer alive | Repo-facts "last 5 default-branch commits" (author + date) and, for this issue, whether any commenter carries an Owner/Member/Collaborator badge | Pass if at least one of the last 5 default-branch commits is authored by a human (not a `[bot]` account) within 90 days of the capture/today date, OR a maintainer (Owner/Member/Collaborator) commented anywhere in this issue's thread within the last 90 days | required |
| Repo in active use | Repo-facts "archived" flag and "latest release" date | Fail immediately if `archived: yes`. Otherwise pass if the latest release is within the last 12 months OR "last push to any branch" is within the last 90 days | required |
| Scope fits a newcomer | Issue title, body, labels, age (opened date vs. today), and any closed/abandoned linked PRs or repeated claim-then-unassign cycles in the thread | Fail if any of: (a) the issue's body is primarily an index/list of links to many other separate issues meant to be picked from independently (a "megaissue"), rather than describing one change; (b) the comment thread shows maintainers still debating unsettled design decisions; (c) it's a pure usage/support question; (d) a maintainer states the fix requires deep core-internals changes; (e) the issue has been open more than 2 years and shows a history of multiple abandoned attempts (closed-unmerged linked PRs, or repeated claim-then-auto-unassign cycles in the thread), signaling real difficulty beyond what a "good first issue" label suggests. A checklist of edits across multiple files implementing one concretely-described change does not itself fail scope, however long. Otherwise pass | required |
| Not already claimed | "this issue: assignees" and "linked PRs" in repo-facts, plus claim comments in the thread | Fail if an assignee is currently set, OR an open linked PR exists, OR someone wrote a claim comment ("I'll take this" / "working on this") within the last 30 days with no sign they abandoned it. Otherwise pass | required |
| Allowed contribution workflow | Repo's stated contribution policy (repo-facts "contribution policy" line, or CONTRIBUTING.md / AI_POLICY.md / AGENTS.md in live mode) | Fail only on an outright ban on AI-assisted contributions. Conditions (disclosure, human review, testing requirements) pass. Silence (no policy found) passes | required |
| Has a "good first issue" style label | Issue labels | Pass if the issue carries a label like `good first issue`, `help wanted`, `beginner-friendly`, or similar | preferred |
| Reproducible / concrete acceptance criteria | Issue body | Pass if the issue includes clear repro steps (for a bug) or a concrete acceptance checklist (for a feature/doc request) | preferred |

## Verdict rule

Accept only if every `required` check grades `pass`. A `required` check graded `fail` or `unclear` rejects the issue (unclear counts as fail — a first issue you can't verify isn't a first issue to take). `preferred` checks never affect the verdict; they only rank accepted issues against the fit profile in `scope.md`.
