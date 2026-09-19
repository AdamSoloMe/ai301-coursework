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
| Not archived | The repo line / repo-facts block: "archived:" flag | Pass if archived is no or absent | required |
| Recent push | Repo facts: "last push to any branch" (live mode: measure from today; eval mode: measure from the bundle's captured date) | Pass if the last push was within 180 days of the measurement date | required |
| Maintainer responds | Repo facts: "maintainer first-response sample" (recently updated issues); if that sample is empty or all-negative, fall back to "last 5 default-branch commits" (author names) | Pass if at least 1 sampled issue shows a first reply from an Owner/Member/Collaborator. If none do (including a thin sample, e.g. only 1 issue sampled), pass instead if at least 2 of the last 5 default-branch commits are authored by distinct non-bot usernames (a bot account ends in `[bot]`) and the newest of those commits falls within the same recency window used for the Recent push check. | required |
| Bounded scope | Issue body and thread; repo-facts "linked PRs" line for this issue | Fail if any of: (a) the issue is self-described as an umbrella/tracking issue — an explicit list of sub-items meant to be split into separate issues/PRs; (b) it is a pure usage/support question, not a change request; (c) a maintainer states in the thread that the fix touches core internals; (d) the thread shows an unresolved design/product decision with no maintainer sign-off, including a feature request whose own text leaves a core implementation choice open (e.g. "TBD", an unspecified format or asset) with no maintainer reply settling it; (e) 2 or more of this issue's linked PRs are listed as closed/unmerged (repeated failed attempts). Otherwise pass. A bug report that names multiple candidate root causes or lists several implementation suggestions for one stated symptom is still bounded — the deliverable is fixing that one behavior, not splitting into separate projects. A terse body or missing repro steps is not itself a fail. | required |
| Unclaimed | Repo facts: "this issue: assignees" and "linked PRs"; issue thread comments | Fail if an assignee is set, or any linked/mentioned PR is open, or a maintainer has confirmed someone's "I'll take this" claim comment. An unanswered claim comment alone, or a closed/abandoned linked PR, does not fail this check. | required |
| AI-contribution policy | Repo facts: "contribution policy" line (CONTRIBUTING.md / AI_POLICY.md / templates) | Fail only on an outright ban on AI-assisted or AI-generated contributions. Conditions (disclosure, human review, testing) pass. Silence (no stated policy) passes. | required |
| Newcomer-friendly signal | Issue labels, and who opened the issue | Prefer issues labeled "good first issue"/"good-first-issue"/"help wanted", or filed by a maintainer (Owner/Member/Collaborator) | preferred |
| Adoption scale | Repo facts: star count | Prefer repos with 500+ stars | preferred |
| Release cadence | Repo facts: "latest release" date | Prefer a release within the last 180 days of the measurement date | preferred |

## Verdict rule

Accept only if every `required` check passes. A single required-check
fail rejects the issue, regardless of how the others grade. `unclear` on
a required check counts as a fail (the evidence needed to verify it is
genuinely missing, so it cannot be trusted for a first contribution).
`preferred` checks never affect the verdict; they only order the issues
that are accepted (more preferred passes ranks higher; ties broken by
whichever preferred check most closely matches the fit profile in
`scope.md`).
