# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

ArshAnan

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/55#issuecomment-5862880385

Hi — I'd like to work on this one. I'm going to reproduce the JS/TS and tech-mention detection gaps in `skill_extractor.py` (the `_detect_languages`, `_detect_tools`, and `_detect_databases` functions) using the failing tests in `tests/unit/test_skill_extractor.py`, and report back with what I find before opening a PR.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/55#issuecomment-5863049550

**Environment**

- OS: macOS 27.0 (Darwin)
- Python: 3.13.7 (venv), pytest 9.0.2
- Repo: fork of `codepath/pathreview-ai301-fa26-s3`, `main` branch, commit `2f4e82f` (2026-09-16) — same commit the issue's own repo-facts were captured against

**Steps**

```bash
git clone https://github.com/ArshAnan/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -e ".[dev]"
pytest tests/unit/test_skill_extractor.py -v --runxfail
```

(`--runxfail` is needed because all five are marked `@pytest.mark.xfail(strict=True, reason="issue #55: ...")` — without it they report as `XFAIL`/green, not as failures.)

**Observed**

5 failed, 13 passed — the same 5 tests named in the issue's xfail markers:

```
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_text_with_typescript_files - assert False
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_database_technology_detection - assert False
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_devops_tool_detection - assert False
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_javascript_detection - assert False
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_docker_compose_detection - assert False
5 failed, 13 passed in 0.10s
```

<details>
<summary>Full failure output (assertion + traceback for each)</summary>

```
______________ TestSkillExtractor.test_text_with_typescript_files ______________
>       assert any("typescript" in s.lower() for s in skill_names)
E       assert False
tests/unit/test_skill_extractor.py:65: AssertionError

____________ TestSkillExtractor.test_database_technology_detection _____________
>       assert any("postgres" in s.lower() or "sql" in s.lower() for s in skill_names)
E       assert False
tests/unit/test_skill_extractor.py:146: AssertionError

________________ TestSkillExtractor.test_devops_tool_detection _________________
>       assert any("docker" in s.lower() for s in skill_names)
E       assert False
tests/unit/test_skill_extractor.py:162: AssertionError

_________________ TestSkillExtractor.test_javascript_detection _________________
>       assert any("javascript" in s.lower() or "js" in s.lower() for s in skill_names)
E       assert False
tests/unit/test_skill_extractor.py:195: AssertionError

_______________ TestSkillExtractor.test_docker_compose_detection _______________
>       assert any("docker" in s.lower() for s in skill_names)
E       assert False
tests/unit/test_skill_extractor.py:213: AssertionError
```

</details>

**Root cause (read directly from `ingestion/parsers/skill_extractor.py`)**

Not one bug but the same shape of bug in three places — keyword/substring matching with no real syntax awareness:

- `_detect_languages`'s JS/TS check is `re.search(r"\b(import|require)\s+", text)` — it requires whitespace *after* `require`, but real JS is `require('fs')` with no space, so it never matches. TypeScript's `export interface`/`export class` syntax isn't checked for at all, so a file with zero `import`/`require` lines (like the test's) can't be detected as TS regardless.
- `_detect_databases` and `_detect_tools` only match the literal engine/tool name as a substring (`"postgresql"`, `"docker"`). A `psycopg2` import or a raw Dockerfile (`FROM`/`RUN`/`EXPOSE`) never spells out "postgresql" or "docker" anywhere, so both go undetected even though they're unambiguous signals to a human reader.

**Conclusion**

Reproduced all 5 tests named in the issue's xfail markers, on the commit the issue was filed against. This matches the issue's description exactly — no adjacent or substituted behavior. Root cause above; will scope a fix (likely: fix the `require` regex, add an `export`/`interface` TS signal, and extend the DB/tool matchers to recognize driver-library names and Dockerfile/compose syntax, not just the bare product name) in the PR.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Confirming full run (`--save-run eval-run.txt`), first and only run: **19/20 agreement — bar met (18/20: PASS)**, `categories: clear-accept 7/8 disclosure 1/1 no-evidence 4/4 unfollowable-comms 3/3 wrong-target 4/4` — every category matched, including the 1-package `disclosure` floor. Single miss: `pkg-05` (see Package analysis below). This is the run committed in `eval-run.txt`; no revisions or `--only` re-runs were needed since the bar and category floor were both cleared on the first full run.

**Package analysis**

Issue: `pkg-05` (conda/conda#16543). Gold label: `accept`. My rubric's decision: `reject`, on "Steps are complete and followable."

The candidate report describes writing "a minimal `env.yml` containing a valid `dependencies:` list plus a `category:` section (the section conda does not recognize)" but never pastes the literal YAML file contents — only a description of its shape. My rubric's check reads: "Fail if a step assumes context the report never shares, or a stranger literally could not reach the same starting point from the report alone." My grader took the undisclosed exact dependency list as exactly that kind of gap: a stranger cannot byte-for-byte recreate the input file, so they "have to guess." Gold treats this package as a clean accept anyway, because the *only* undisclosed detail (which specific packages sit under `dependencies:`) is inconsequential to the bug — the trigger is the presence of an unrecognized `category:` key alongside a valid `dependencies:` list, and that trigger is stated in full, exact prose. Any `env.yml` with those two properties reproduces the same `EnvironmentSectionNotValid`-on-stdout behavior regardless of which packages are named. My check's wording doesn't distinguish "a stranger can't recreate this literally" from "a stranger can't recreate whatever actually matters," and conflating the two is what cost this package.

**Check rationale**

The current "Behavior shown matches the issue" row in `rubric.md`:

> "Pass if either: (a) the report claims reproduction and the artifact shows the same failure signature the issue names (same exception type, same failing tests, same wrong output), produced by the same trigger the issue describes, not a substituted or adjacent one; or (b) the report honestly states it could not reproduce and shows a real attempted-trigger artifact instead (even though it doesn't show the bug). Fail if it claims reproduction with no artifact quoted, with an artifact showing an unrelated/adjacent failure, or with steps that silently swap in a different trigger than the issue names"

I wrote it this way because my first draft only had branch (a) — pass if the artifact shows the issue's failure signature. That wording would have failed every honest "could not reproduce" report by construction, since a report that didn't reproduce the bug has no artifact showing the bug's failure signature to point to. The eval set's `clear-accept` category includes exactly this case twice (`pkg-09`, `pkg-10`: both gold `accept`, both honest cannot-reproduce reports with a real attempted-trigger artifact and a stated hypothesis for the mismatch). I added branch (b) specifically so an evidenced, plainly-stated non-reproduction passes on its own terms, rather than being punished for not showing something that, by its own honest account, never happened.

**Trade-offs**

I accepted the `pkg-05` miss rather than loosen "Steps are complete and followable" to pass it. Loosening that check to accept a described-but-not-pasted input file risks passing reports in the `unfollowable-comms` category that lean on the same excuse for details that *do* matter (private configs, unshared fixtures) — that category is exactly the trap the eval set builds for a check phrased too permissively. With the bar (18/20) and the category floor (at least one match everywhere, including the 1-item `disclosure` trap) both already cleared on this first full run, spending a second $4 confirming run to chase one arguable point felt like the wrong trade against the assignment's own guidance that "a first run that already agrees... is a complete answer, and loses nothing." Nothing else changed as a result: the check keeps failing genuinely unfollowable reports, at the cost of also failing the rare report where the omitted detail happens not to matter.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
