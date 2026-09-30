# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: in an eval bundle, the repro report section usually labeled "Environment" or "Setup" (OS, runtime/language version, package/dependency versions, commit SHA). In live mode, this is the corresponding section of the student's draft repro report; cross-check the versions named there against whatever the issue itself states it was filed against (issue body, linked release, or "Affected version" field).

What good looks like: the versions that actually matter for this bug are named (not a generic "works on my machine"), and if the reproduction environment differs from the issue's stated target, the report says so explicitly rather than leaving the reader to notice the gap.

## Steps

Where it lives: the repro report's numbered or ordered step list, in the bundle or the student's draft. The starting state (fresh clone, specific branch/tag, seed data) should appear before step 1, not be assumed.

What makes steps followable: each step is a concrete action (a command run, a file edited, a button clicked) rather than a restated goal ("reproduce the crash"); the sequence starts from a named, reachable starting state; nothing between two steps requires knowledge the report never gave the reader. A step may point back at precise values already stated in the issue itself (an exact input string, exact range/flags) instead of re-pasting them, as long as those values are precise enough to reconstruct the trigger with no guesswork — that is different from a step that depends on a private, unshared environment or an omitted detail (a missing driver/profile/flag) the reader has no way to recover.

## Behavior shown

Where it lives: pasted output, a log excerpt, a stack trace, or a screenshot description embedded in the repro report — in the bundle this is usually a fenced block or an explicit "Observed" section; in live mode it's whatever the student's draft quotes or attaches.

What it means to show the issue's behavior: the artifact's content (the specific error message, exit code, visual glitch, or wrong value) matches what the issue describes as broken — same symptom, same code path if named — not a different error the repro happened to hit, and not a success case dressed up as a failure.

An honest cannot-reproduce is the other passing shape, and looks different from a wrong-target failure: it uses the issue's exact inputs/config (not a swapped operator, a different range, or an older version presented as current), it shows an artifact from that exact attempt (not merely a claim), and it names any environment or version difference from the issue's stated target rather than letting the reader assume a match. A wrong-target package instead narrates a different artifact as if it confirms the issue, or substitutes a different environment/version without saying so — that still fails this check.

## Honesty

Where it lives: the report's concluding statement or summary line, read next to the artifacts a few lines above it. In the bundle, this is often the last paragraph of the repro report; in live mode, the closing lines of the draft.

What separates an honest report from an overclaiming one: an honest report's conclusion is a direct restatement of what the artifacts showed, including "I could not trigger the behavior after N attempts" when that's true. An overclaiming report asserts reproduction, root cause, or severity beyond what any quoted artifact demonstrates.

## Comms

Where it lives: the claim comment and repro comment text themselves, read against the issue's own body/title (for specificity) and the repo's CONTRIBUTING file, issue template, or stated contribution policy (for conventions, including any line requiring AI-assistance disclosure). In the bundle, the repo-facts block usually carries the relevant policy excerpt; in live mode, check the repo's actual CONTRIBUTING.md / README / issue template.

What specific-and-honest looks like next to boilerplate: the claim comment names the specific issue and what will be investigated next, not a generic "I'll take this." The repro comment follows whatever structure the repo's template asks for, and if the repo's stated policy requires disclosing AI tool use, the comment contains that disclosure in plain language rather than omitting it.
