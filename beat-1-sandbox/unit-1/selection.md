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

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61

**Verdict output**

```
Ranked read-out (all three accepted, tied on preferred checks — the fit profile in
scope.md breaks the tie toward #61, a backend Python/SQL bug):

- #61 — Health check DB probe passes a raw SQL string — bounded one-file bug with an
  exact error message and repro; unclaimed; maintainer-filed.
- #47 — API docs don't include example curl commands — bounded docs task with a stated
  effort estimate; unclaimed; maintainer-filed.
- #56 — Structural chunker silently drops documents that contain no headings — bounded
  one-function bug with a runnable repro and a named failing test; unclaimed;
  maintainer-filed.

All three: not archived, pushed 3 days ago (well within 180 days), maintainer response
sample shows a COLLABORATOR (Aburke225) replying within 6 days on a same-batch issue, no
stated AI policy (silence passes), no assignee, no comments, no linked PRs. They tie on
preferred checks too — all good-first-issue-labeled and maintainer-filed (pass), but the
repo has only 2 stars and 0 releases (fail both scale checks) since it's a classroom
fork, not a real OSS project by those metrics.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61",
    "checks": [
      {"name": "Not archived", "grade": "pass", "evidence": "repo archived: false"},
      {"name": "Recent push", "grade": "pass", "evidence": "repo pushed_at 2026-09-16, 3 days before today (2026-09-19)"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "issue #52 (opened 2026-09-10) got a COLLABORATOR (Aburke225) reply on 2026-09-16, 6.0 days -- 1 of 5 recently-updated issues sampled"},
      {"name": "Bounded scope", "grade": "pass", "evidence": "single-file bug in api/routes/health.py with exact error message and repro steps; not an umbrella, no design debate, no linked PRs"},
      {"name": "Unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; no linked PRs found"},
      {"name": "AI-contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI/generated-code statement -- silence passes"},
      {"name": "Newcomer-friendly signal", "grade": "pass", "evidence": "labeled 'good first issue'; opened by Aburke225 (COLLABORATOR)"},
      {"name": "Adoption scale", "grade": "fail", "evidence": "2 stars, below 500-star threshold (preferred, does not affect verdict)"},
      {"name": "Release cadence", "grade": "fail", "evidence": "0 releases published (preferred, does not affect verdict)"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/47",
    "checks": [
      {"name": "Not archived", "grade": "pass", "evidence": "repo archived: false"},
      {"name": "Recent push", "grade": "pass", "evidence": "repo pushed_at 2026-09-16, 3 days before today"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "issue #52 got a COLLABORATOR reply within 6.0 days -- same repo-level sample"},
      {"name": "Bounded scope", "grade": "pass", "evidence": "docs-only task naming the exact file (docs/API.md) and endpoints to add; stated effort estimate 2-3 hours; not an umbrella, no unresolved design question"},
      {"name": "Unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; no linked PRs found"},
      {"name": "AI-contribution policy", "grade": "pass", "evidence": "no stated AI policy -- silence passes"},
      {"name": "Newcomer-friendly signal", "grade": "pass", "evidence": "labeled 'good first issue'; opened by Aburke225 (COLLABORATOR)"},
      {"name": "Adoption scale", "grade": "fail", "evidence": "2 stars, below 500-star threshold (preferred)"},
      {"name": "Release cadence", "grade": "fail", "evidence": "0 releases published (preferred)"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/56",
    "checks": [
      {"name": "Not archived", "grade": "pass", "evidence": "repo archived: false"},
      {"name": "Recent push", "grade": "pass", "evidence": "repo pushed_at 2026-09-16, 3 days before today"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "issue #52 got a COLLABORATOR reply within 6.0 days -- same repo-level sample"},
      {"name": "Bounded scope", "grade": "pass", "evidence": "single-function bug in StructuralChunker.chunk() with a runnable repro snippet and a named failing test; not an umbrella, no design debate"},
      {"name": "Unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; no linked PRs found"},
      {"name": "AI-contribution policy", "grade": "pass", "evidence": "no stated AI policy -- silence passes"},
      {"name": "Newcomer-friendly signal", "grade": "pass", "evidence": "labeled 'good first issue'; opened by Aburke225 (COLLABORATOR)"},
      {"name": "Adoption scale", "grade": "fail", "evidence": "2 stars, below 500-star threshold (preferred)"},
      {"name": "Release cadence", "grade": "fail", "evidence": "0 releases published (preferred)"}
    ],
    "verdict": "accept"
  }
]
```
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Full run (20 issues), before any revision: **16/20 scored items agree**. Disagreed on
   issue-14, issue-15, issue-19, issue-20. Category floor was already met, but total
   agreement was below the 18/20 bar.
2. Partial run, `--only issue-14,issue-15,issue-19,issue-20` after revising two checks:
   **4/4 agree**.
3. Full confirming run, `--save-run eval-run.txt`: **20/20 scored items agree**
   (`categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4`).
   This is the run committed in `eval-run.txt`.

**Issue analysis**

Issue: **issue-20** (`excalidraw/excalidraw#11811`), category `scope`. Gold label:
`reject`. My rubric's final verdict: `reject` — the two agree.

My rubric reads this issue as a feature request ("Add company logo shape to the
toolbar") whose own text leaves a core implementation choice unresolved: it says "Logo
asset TBD" and carves out "Out of scope for v1: custom logo upload / branding settings"
without a maintainer ever weighing in (0 comments, opened by `cursor[bot]`). My rubric's
"Bounded scope" check has a specific fail condition for exactly this: "the thread shows
an unresolved design/product decision with no maintainer sign-off, including a feature
request whose own text leaves a core implementation choice open (e.g. 'TBD', an
unspecified format or asset) with no maintainer reply settling it." That condition is
what produces the reject — the repo itself is extremely healthy (128,988 stars, commits
daily), so every other required check passes; scope is the only thing that sinks it. My
first-draft rubric did not have this condition and wrongly accepted the issue, treating
"no maintainer said this touches internals" as sufficient for a scope pass. Comparing my
rubric's error against the gold note ("one-line feature wish with no spec and a product
decision hiding inside") is what showed me the check needed to look for unresolved
decisions inside the reporter's own text, not just maintainer statements.

**Check rationale**

Quoted from the `Bounded scope` row in `rubric.md`, as uploaded:

> Fail if any of: (a) the issue is self-described as an umbrella/tracking issue — an
> explicit list of sub-items meant to be split into separate issues/PRs; (b) it is a
> pure usage/support question, not a change request; (c) a maintainer states in the
> thread that the fix touches core internals; (d) the thread shows an unresolved
> design/product decision with no maintainer sign-off, including a feature request
> whose own text leaves a core implementation choice open (e.g. "TBD", an unspecified
> format or asset) with no maintainer reply settling it; (e) 2 or more of this issue's
> linked PRs are listed as closed/unmerged (repeated failed attempts). Otherwise pass.

Condition (d) exists because my first draft only caught scope failures that were
*structurally* obvious (an explicit umbrella list) or *explicitly stated* by a
maintainer (touches core internals). It missed a feature request that looks bounded on
the surface but is quietly unresolved because the reporter themself left a design
question open and nobody with authority closed it. Condition (e) exists separately,
with a specific countable threshold (2+ closed/unmerged linked PRs) rather than a vague
"has been abandoned before" — I picked that threshold, instead of a looser "old issue
with any history," because a different accept-labeled issue in the set (issue-09, ~8
years old with exactly one closed linked PR and a stale claim) needed to keep passing;
a threshold of 1 would have wrongly rejected it.

**Trade-offs**

Condition (d) is more subjective than the rest of the table, and it can over-reject: any
feature request that happens to phrase an implementation detail as "TBD" or leaves one
small decision open will fail this check even if the ask is otherwise perfectly
scoped and a newcomer could safely make a reasonable call themselves. I accept this
false-negative risk on purpose — the failure mode I'm avoiding (a newcomer discovering
mid-PR that "asset TBD" hides a real product decision nobody signed off on) costs more
than skipping an issue that might have actually been fine. I checked the trade-off is
narrow rather than sweeping: after adding condition (e)'s 2+-closed-PR threshold, I
re-ran `--only issue-09` as a canary specifically because it is the one other issue in
the set with a long history and a closed linked PR, and confirmed it still grades
`accept` (1 closed PR, below the threshold) — so the new condition doesn't quietly
reject every issue with any PR history, only the ones with a repeated pattern of failed
attempts.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit and time.** #61 matches what I actually want to practice — backend Python and
   SQL — more than the docs task (#47) or the ingestion bug (#56). I have enough time
   available this week to look into the SQLAlchemy 2.x migration properly rather than
   just patching the symptom, which is the kind of depth I want out of this first issue
   rather than the fastest possible merge.
2. **What the verdict identified vs. what I weighed.** The rubric correctly confirmed
   the mechanics that make an issue safe to take: #61 is unclaimed (no assignee, no
   comments, no linked PRs), bounded (one file, one exact error message, no design
   debate), and the repo is alive (pushed 3 days ago, a maintainer replied to a
   same-batch issue within 6 days). What the rubric can't see, because fit never
   changes a verdict, is that #61 specifically lines up with my own Python/SQL
   background better than the other two accepted candidates — that's a judgment call I
   made on top of the rubric's accept, not something it could rank for me on its own
   (all three tied on preferred checks).
3. **Anticipated difficulty.** The code change itself looks small — wrap the literal
   `"SELECT 1"` in `sqlalchemy.text()` — so I don't expect the fix to be the hard part.
   I expect the real work to be process: following the repo's branch-naming and
   Conventional Commits conventions, getting all five CI jobs green (`lint`,
   `typecheck`, `test-unit`, `test-integration`, `frontend`), and writing a PR
   description that meets the template.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
