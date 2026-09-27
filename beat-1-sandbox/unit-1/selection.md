# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/55

**Verdict output**

```
Evidence gathered

Repo-level (applies to all three):
- Not archived; pushed_at 2026-09-16 (11 days before today, 2026-09-27); last 5 commits all by human Aburke225 (COLLABORATOR on the repo, opened all three issues) — Maintainer alive: pass, Repo in active use: pass
- docs/CONTRIBUTING.md covers branch naming, commits, CI, xfail-removal conventions but says nothing about AI-assisted contributions — silence passes → Allowed contribution workflow: pass
- House rule in scope.md: ignore claim comments from other students in this classroom repo.

#72 — verify_password raises on malformed hash: labels bug, good first issue, api, tier-1; single function, named xfail test (H-05), 1–2h estimate. No assignee; the only cross-reference is a closed PR in an unrelated repo (ohsono/ai301-coursework, a classmate's own coursework write-up), not a real fix PR here. 8 students posted claim/repro comments — exempted by house rule.
→ Scope: pass, Not claimed: pass, labels/criteria (preferred): pass/pass. Accept.

#68 — KeywordSearcher.index() ZeroDivisionError on empty index: labels bug, good first issue, rag, tier-1; bounded, xfail H-01, 2–4h estimate. But PR #74 ("fix: handle empty keyword search indexes", by Momik-jpg, state=open, body says "Fixes #68") is a formally linked, currently-open PR — this is not a comment, so the house rule doesn't excuse it; it fails "Not already claimed" as written.
→ Reject (required check fail).

#55 — Skill extractor misses JS/TS and tech mentions: labels bug, ingestion, tier-1 (no good-first-issue label); no assignee, zero comments, empty timeline (no linked PRs). Describes one underlying weakness (name-only matching) surfacing across _detect_languages/_detect_tools/_detect_databases, with explicit repro command naming 5 failing tests — not framed as a tracking/meta issue, no maintainer scope objection.
→ Accept, but broader/less-scoped than #72 (3 functions, no effort estimate, no good-first-issue label).

Fit note: the fit profile asks for C++ practice; this repo is entirely Python (backend) + TypeScript (frontend) — there is no C++ anywhere, so neither accepted issue truly serves that goal. Both are backend-Python bug fixes, so at least neither trips the "avoid web-dev/frontend" preference. Between the two, #72 outranks #55 on the preferred checks (good-first-issue label + tighter, single-function scope with a time estimate).

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Last 5 default-branch commits (2026-08-24 to 2026-09-16) all by human Aburke225 (COLLABORATOR), within 90 days of 2026-09-27"},
      {"name": "Repo in active use", "grade": "pass", "evidence": "Not archived; last push 2026-09-16, 11 days ago"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded bug in core/security.py, named xfail test H-05, estimated effort 1-2h"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "No assignee; only cross-ref is a closed PR in an unrelated repo (ohsono/ai301-coursework); classroom claim comments exempted by house rule"},
      {"name": "Allowed contribution workflow", "grade": "pass", "evidence": "docs/CONTRIBUTING.md states no AI-contribution ban; silence passes"},
      {"name": "Has good first issue style label", "grade": "pass", "evidence": "Labels include 'good first issue'"},
      {"name": "Reproducible / concrete acceptance criteria", "grade": "pass", "evidence": "Named xfail test H-05, specific files, 1-2h estimate"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/55",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Last 5 default-branch commits (2026-08-24 to 2026-09-16) all by human Aburke225 (COLLABORATOR), within 90 days of 2026-09-27"},
      {"name": "Repo in active use", "grade": "pass", "evidence": "Not archived; last push 2026-09-16, 11 days ago"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "One described weakness (name-only matching) across _detect_languages/_detect_tools/_detect_databases; not framed as a tracking/meta issue, no maintainer objection on scope"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "No assignee, 0 comments, empty cross-reference timeline"},
      {"name": "Allowed contribution workflow", "grade": "pass", "evidence": "docs/CONTRIBUTING.md states no AI-contribution ban; silence passes"},
      {"name": "Has good first issue style label", "grade": "fail", "evidence": "Labels are bug, ingestion, tier-1 only — no good-first-issue-style label"},
      {"name": "Reproducible / concrete acceptance criteria", "grade": "pass", "evidence": "Body gives exact pytest command and 5 named failing tests"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Last 5 default-branch commits (2026-08-24 to 2026-09-16) all by human Aburke225 (COLLABORATOR), within 90 days of 2026-09-27"},
      {"name": "Repo in active use", "grade": "pass", "evidence": "Not archived; last push 2026-09-16, 11 days ago"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded bug in rag/retriever/keyword_search.py, named xfail test H-01, estimated effort 2-4h"},
      {"name": "Not already claimed", "grade": "fail", "evidence": "PR #74 'fix: handle empty keyword search indexes' by Momik-jpg is open and its body says 'Fixes #68'"},
      {"name": "Allowed contribution workflow", "grade": "pass", "evidence": "docs/CONTRIBUTING.md states no AI-contribution ban; silence passes"},
      {"name": "Has good first issue style label", "grade": "pass", "evidence": "Labels include 'good first issue'"},
      {"name": "Reproducible / concrete acceptance criteria", "grade": "pass", "evidence": "Named xfail test H-01, specific files, 2-4h estimate"}
    ],
    "verdict": "reject"
  }
]
```

**The verdict must record `accept` for this issue.** Confirmed above: issue #55 is graded `"verdict": "accept"` in the fenced JSON block.

---

## Eval iterations

**Run history**

1. Smoke run (`--limit 3`, first 3 bundles): 2/3 agreement. Miss: `issue-01` (gold `accept`, my rubric graded `reject` on "Scope fits a newcomer").
2. Revised the "Scope fits a newcomer" check and re-ran `--only issue-01`: 1/1 agreement.
3. First full run (20 bundles): 18/20 agreement — bar met (18/20: PASS), but `scope 2/4` on the category tally. Misses: `issue-10`, `issue-15`, both false accepts on "Scope fits a newcomer."
4. Revised "Scope fits a newcomer" again (to catch megaissue-style index issues and years-open issues with abandoned-attempt histories) and re-ran `--only issue-01,issue-10,issue-15`: 3/3 agreement.
5. Confirming full run with `--save-run eval-run.txt`: **18/20 agreement — bar met (18/20: PASS)**, `categories: claimed 4/4 clear-accept 6/8 dead-repo 3/3 policy 1/1 scope 4/4`. Misses this run: `issue-09`, `issue-19` (see Trade-offs below). This is the run committed in `eval-run.txt`.

**Issue analysis**

Issue: `issue-01`. Gold label: `accept`. My rubric's final decision: `accept` (agree).

On the first smoke run my rubric rejected `issue-01` on "Scope fits a newcomer." The bundle's issue body asks for several related edits — "Create a new task page... Update `manage-pkgs.rst`... Update `pip-interoperability.rst`... Update `new-features.md`... Consider a global `troubleshooting.rst` entry" — and my first check wording failed anything that "spans multiple files," reading that checklist as an umbrella issue meant to be split into separate work. It isn't: every item implements one described change (documenting a single new `conda install` workflow), the issue has zero comments (no unresolved debate), and it was opened by a `CONTRIBUTOR` with concrete, specific requirements for each section. I rewrote the check to explicitly say a checklist of edits that together implement one concretely-described change still passes scope, however many files it touches — after that, `issue-01` graded `accept`, matching gold.

**Check rationale**

The current "Scope fits a newcomer" row in `rubric.md`:

> "Fail if any of: (a) the issue's body is primarily an index/list of links to many other separate issues meant to be picked from independently (a "megaissue"), rather than describing one change; (b) the comment thread shows maintainers still debating unsettled design decisions; (c) it's a pure usage/support question; (d) a maintainer states the fix requires deep core-internals changes; (e) the issue has been open more than 2 years and shows a history of multiple abandoned attempts (closed-unmerged linked PRs, or repeated claim-then-auto-unassign cycles), signaling real difficulty beyond what a "good first issue" label suggests. A checklist of edits across multiple files implementing one concretely-described change does not itself fail scope, however long. Otherwise pass"

I wrote it this way because a single "is this too broad" test kept collapsing two different failure modes into one rule. Condition (a) exists because of `issue-10`, literally titled "Documentation request megaissue," whose entire body is ~120 links to separate issues — a real tracking issue with no maintainer debate at all, so a rule keyed only on "unsettled debate" (my first rewrite) missed it. Condition (e) exists because of `issue-15`, a "good first issue"-labeled bug open since 2021 with 97 comments of contributors repeatedly claiming it and going quiet, plus two closed/unmerged linked PRs — the evidence guide names this exact pattern ("an issue open for years with several abandoned attempts... is telling you something about its real difficulty") as a scope signal my rubric wasn't checking at all.

**Trade-offs**

Broadening the check to catch `issue-10` and `issue-15` is not free. In the confirming run, two issues newly failed "Scope fits a newcomer": `issue-09` and `issue-19`, both gold `accept`, both graded `reject` by my rubric (the run's `note` column reads `failed: Scope fits a newcomer` for both). I accept this trade-off: before the fix, `scope` category agreement was `2/4` (missing the category on two issues, `issue-10` and `issue-15`); after it, `scope` is `4/4`, at the cost of two different, more arguable false rejects elsewhere, and the overall bar stayed the same (18/20). I did not re-tune the check further, since the assignment notes that several of the 20 scored issues are genuinely arguable scope calls, and chasing a perfect score by re-fitting to individual issues risks a rule that only works on this fixed eval set rather than one I'd trust on a new issue.

---

## Selection rationale

**Selection rationale**

1. Fit to interests and time: my background is C++ and TypeScript, and I wanted to avoid frontend/web-dev work for this first contribution. This repo (PathReview) has no C++ at all, so that preference couldn't be served here regardless of which issue I picked; but issue #55 is a backend Python bug in `ingestion/parsers/skill_extractor.py`, not frontend work, and it happens to be about detecting JavaScript/TypeScript in resumes and repos — a language I actually know, even though the fix itself is Python. The scope (three related functions, no time estimate) is a bit more open-ended than a single-function fix, but still small enough to fit around coursework.

2. The verdict correctly identified that #55 is genuinely unclaimed — zero comments, no assignee, no linked PRs — and reproducible, since the issue body names an exact command (`pytest tests/unit/test_skill_extractor.py -q`) and five specific failing tests. What the rubric can't weigh is that #55 is uncontested while my other accepted option, #72, already has eight classmates' claim/repro comments on it; picking #55 means doing independent work rather than following a well-trodden path, which matters to me for the experience even though it doesn't affect grading either way.

3. Anticipated difficulty in claiming: since no one has claimed or commented on #55, claiming it should be uncomplicated under the course's house rules. The real difficulty is scoping the fix myself before I start: the issue touches three functions (`_detect_languages`, `_detect_tools`, `_detect_databases`) with no maintainer-given time estimate, so going into Unit 2 I'll need to decide up front how much of that surface to fix in one PR rather than discovering the boundary mid-way.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.