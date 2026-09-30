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

AdamSoloMe

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61#issuecomment-5903374751

I'd like to claim this issue as my first contribution.

My plan: check out the current commit, confirm that `await db.execute("SELECT 1")` in `api/routes/health.py` raises the `ArgumentError` the issue describes under SQLAlchemy 2.x (textual SQL needing `sqlalchemy.text()`), and post a reproduction report with the environment, exact steps, and the observed output.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61#issuecomment-5903518943

Reproduced.

**Environment:** PathReview at commit `2f4e82f` (clean tracked tree). macOS 27.0 (Darwin 27.0.0, arm64), Python 3.12.9, SQLAlchemy 2.1.1, asyncpg 0.31.0, FastAPI 0.142.1. Database: PostgreSQL 13.17, run locally via Homebrew rather than the repo's `docker-compose` Postgres, since Docker wasn't available in my environment — noting the deviation rather than silently substituting it. I don't believe it affects this bug: a separate direct call showed the `ArgumentError` is raised inside SQLAlchemy's statement-coercion layer (`sqlalchemy/sql/coercions.py`, `_no_text_coercion`) before any driver-level I/O happens, so it doesn't depend on the Postgres version or backend.

**Steps** (from the repo root, clean checkout of `2f4e82f`):

1. Start a throwaway local Postgres and create the app's database:
   ```
   initdb -D ./pgdata -U pathreview_repro --auth=trust
   pg_ctl -D ./pgdata -o "-p 55432 -k /tmp/pgrepro61" start
   psql -h /tmp/pgrepro61 -p 55432 -U pathreview_repro -d postgres -c "CREATE DATABASE pathreview_dev;"
   ```
2. Confirm the database is independently reachable:
   ```
   psql -h /tmp/pgrepro61 -p 55432 -U pathreview_repro -d pathreview_dev -c "SELECT 1;"
   ```
   (returns one row, `1`).
3. Install the subset of `pyproject.toml`'s dependencies needed to import `api/routes/health.py` and `core/database.py`:
   ```
   python3 -m venv .venv && source .venv/bin/activate
   pip install "sqlalchemy>=2.0.0" "asyncpg>=0.29.0" "fastapi>=0.109.0" "structlog>=24.1.0" "pydantic[email]>=2.5.0" "pydantic-settings>=2.1.0" "redis>=5.0.0" "httpx>=0.26.0" "greenlet>=3.0.0"
   ```
4. Save as `repro61_http.py` in the repo root and run `python repro61_http.py`. It mounts the repo's unmodified `health` router and sends `GET /health`:
   ```python
   import os, sys
   sys.path.insert(0, ".")
   os.environ["DATABASE_URL"] = "postgresql+asyncpg://pathreview_repro@localhost:55432/pathreview_dev"

   from fastapi import FastAPI
   from fastapi.testclient import TestClient
   from api.routes.health import router

   app = FastAPI()
   app.include_router(router)
   resp = TestClient(app).get("/health")
   print("HTTP status:", resp.status_code)
   print("Body:", resp.json())
   ```
5. Immediately afterwards, rerun the step 2 `psql ... -c "SELECT 1;"` check.

**Output: psql before, `GET /health`, psql after (one run, in order):**
```
== before ==
1
== GET /health ==
HTTP status: 503
Body: {'detail': {'status': 'unhealthy', 'dependencies': {'postgres': 'unhealthy', 'redis': 'unhealthy', 'vector_db': 'healthy'}, 'safety_events_last_hour': 0, 'timestamp': '2026-09-30T01:30:13.969427'}}
== after ==
1
```

**Server-side log at the moment of the postgres check:**
```
postgres_health_check_failed   error="Textual SQL expression 'SELECT 1' should be explicitly declared as text('SELECT 1')"
```

**Traceback (from a separate, isolated call to `session.execute("SELECT 1")`), showing where it actually raises:**
```
  File ".../sqlalchemy/orm/session.py", line 2212, in _execute_internal
    statement = coercions.expect(roles.StatementRole, statement)
  File ".../sqlalchemy/sql/coercions.py", line 631, in _literal_coercion
    return self._text_coercion(element, argname, **kw)
  File ".../sqlalchemy/sql/coercions.py", line 594, in _no_text_coercion
    raise exc_cls(
sqlalchemy.exc.ArgumentError: Textual SQL expression 'SELECT 1' should be explicitly declared as text('SELECT 1')
```

**Expected (per the issue):** the health check reports postgres as healthy, since the database is reachable.

**Actual:** `GET /health` returns 503 with `"postgres": "unhealthy"`, and the error message matches the issue's report verbatim. The `psql` checks just before and just after the request both returned `1`, so the database was answering queries on either side of the failed probe.

**Aside, not part of this issue:** the `redis` check in the same response also fails, but with an unrelated error (`'Settings' object has no attribute 'redis_host'`) — a separate, pre-existing gap in this route's Redis check, not something this reproduction speaks to. Flagging it so it isn't mistaken for evidence about #61.

**Conclusion:** the postgres probe fails exactly as the issue describes: a raw SQL string rejected by SQLAlchemy 2.x's textual-SQL coercion, which the broad `except Exception` in `health_check` catches and reports as the database being down, even though `psql` reached it right before and right after. The fix implied by the issue (`sqlalchemy.text("SELECT 1")`) is not applied here; this comment only reports the reproduction, not a fix.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

0. Warm-up, no credit: I graded `calib-02` by hand against my first rubric and got
   `reject`. That matched its gold label (`"worksheet clear reject: emphatic me-too with
   zero evidence and a cause asserted from vibes"`).
1. Full run (20 packages), first rubric: `agreement: 19/20 scored items  (bar: 18/20: PASS)`.
   The one disagreement was `pkg-12  accept  reject  NO  failed: Steps followable`.
2. Partial run after revising "Steps followable":
   `--only pkg-12,pkg-06,pkg-18,pkg-19,calib-04 --include-calibration` →
   `agreement: 4/4 scored items`. pkg-12 flipped to `accept`, and all three
   `unfollowable-comms` canaries plus `calib-04` still rejected.
3. Full run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`. The disagreement moved
   to `pkg-10  accept  reject  NO  failed: Behavior matches issue`.
4. Partial run after revising "Behavior matches issue":
   `--only pkg-10,pkg-02,pkg-04,pkg-08,pkg-13,pkg-14,pkg-15,pkg-16,pkg-17,calib-02,calib-03 --include-calibration`
   → `agreement: 9/9 scored items`. pkg-10 flipped to `accept`, and every
   `wrong-target` and `no-evidence` canary still rejected.
5. Full confirming run with `--save-run eval-run.txt`:
   `agreement: 20/20 scored items  (bar: 18/20: PASS)`, with
   `categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`.
   This is the run committed in `eval-run.txt`.

**Package analysis**

Package: **pkg-10** (`starship/starship#7648`), category `clear-accept`. Gold label:
`accept`. My final rubric's verdict: `accept`, so the two agree. In run 3 my earlier rubric
rejected it (`failed: Behavior matches issue`).

The package is an honest cannot-reproduce. The report opens with "Result: cannot reproduce
on Linux + zsh with the report's exact layout and config". It uses the issue's exact symlink
layout and `repo_root_style = "bold red"` config, and it shows the prompt it actually got
(`monorepo/packages/app-dir on  master`). It also names the gap: "The report is macOS +
fish 4.7.1; shell and OS both differ, starship version matches."

The old "Behavior matches issue" check only had one way to pass: "the artifact shows the
same failure/behavior named in the issue (same error, same symptom), not a different or
merely adjacent one." A cannot-reproduce shows the bug not happening, so that condition
could never pass it, and the required check sank the whole package. The gold note says what
my rubric was missing: "honest cannot-reproduce: exact layout and config, prompt artifact
shown, names the environment differences (Linux+zsh vs macOS+fish)". My current rubric
accepts it under the check's case (2). The report "explicitly states it could not trigger
that behavior". It is "backed by an artifact from an attempt using the issue's exact
inputs/config". And the OS/shell deviation is "named rather than silently substituted."

A clue that this was a gap in the rubric and not bad luck: pkg-10 was graded `accept` in
run 1 and `reject` in run 3, with no change to the check between those runs. A check with
no real pass path for a package leaves the grader guessing, so the result flips between runs.

**Check rationale**

Quoted from the `Behavior matches issue` row in `tools/repro-check/rubric.md`, as uploaded:

> | Behavior matches issue | The output excerpt, log, or screenshot artifact, read against the exact behavior the issue describes | Passes in either of two cases: (1) the artifact shows the same failure/behavior named in the issue (same error, same symptom), not a different or merely adjacent one; or (2) the report explicitly states it could not trigger that behavior, backed by an artifact from an attempt using the issue's exact inputs/config, with any deviation from the issue's stated environment or version named rather than silently substituted. A non-matching artifact narrated as if it confirms the issue's behavior fails this check under case (1) and does not qualify for case (2) either | required |

My first draft had only case (1). That meant any honest cannot-reproduce failed a required
check. It also contradicted my own "Honest outcome" check, which says "an evidenced
cannot-reproduce (with the attempted steps and result shown) passes." I added case (2) so
that a faithful non-reproduction has a way to pass.

I rejected the simpler fix of just deleting "same symptom" and letting any non-matching
artifact through. That would have opened the door to wrong-target packages: a package that
shows a different error and narrates it as confirmation. So case (2) has three gates. The
report has to *say* it did not reproduce. It has to use the issue's *exact* inputs/config.
And it has to *name* any environment or version deviation. The last sentence closes the
loophole explicitly: a non-matching artifact "narrated as if it confirms the issue's
behavior" qualifies for neither case. Each gate matches one wrong-target pattern in the set.
pkg-16 tested an old pandas version "without acknowledging the deviation". pkg-02 and
calib-03 changed the input syntax. pkg-08 and pkg-17 narrated a different artifact as a
confirmed crash.

**Trade-offs**

Loosening this check was exactly the case where a package that already agreed could flip.
So before the confirming full run, I re-ran every `wrong-target` package (`pkg-02`,
`pkg-08`, `pkg-16`, `pkg-17`) and every `no-evidence` package (`pkg-04`, `pkg-13`,
`pkg-14`, `pkg-15`) as canaries with `--only`. I added `calib-02` and `calib-03` as free
trap checks. All ten still rejected (`agreement: 9/9 scored items`, calibration packages
also `reject`). The full run then held `wrong-target 4/4` and `no-evidence 4/4`.

The cost I accept: case (2) requires "the issue's exact inputs/config". A real
cannot-reproduce that had a good reason to change an input will fail this check even if it
is honest. An example is an issue whose repro depends on a file that no longer exists. I
would rather hold that report and make its author explain the change than let adapted
inputs through, because adapted inputs are how the wrong-target packages in this set fooled
a reader.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
