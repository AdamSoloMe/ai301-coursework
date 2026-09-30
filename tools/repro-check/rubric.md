# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment record (OS, language/runtime version, dependency versions, commit SHA or release tag) | Every version detail relevant to the issue's stated target is named explicitly, or a mismatch from the issue's target is called out rather than silently assumed | required |
| Steps followable | The repro report's numbered steps, from starting state to trigger | A stranger with a clean checkout could execute the steps as written and reach the same trigger point. Precise values (exact input, exact flags/options) may be given by reference to the issue's own stated inputs rather than re-pasted, as long as every value needed to reconstruct the trigger is stated somewhere precisely, not left to guesswork. No step may depend on unstated prior state, an unshared private environment, or an implicit action | required |
| Behavior matches issue | The output excerpt, log, or screenshot artifact, read against the exact behavior the issue describes | Passes in either of two cases: (1) the artifact shows the same failure/behavior named in the issue (same error, same symptom), not a different or merely adjacent one; or (2) the report explicitly states it could not trigger that behavior, backed by an artifact from an attempt using the issue's exact inputs/config, with any deviation from the issue's stated environment or version named rather than silently substituted. A non-matching artifact narrated as if it confirms the issue's behavior fails this check under case (1) and does not qualify for case (2) either | required |
| Honest outcome | The report's stated conclusion, read against the artifacts that back it | The conclusion claims no more than the evidence shows: an evidenced cannot-reproduce (with the attempted steps and result shown) passes; a confident claim of reproduction with no matching artifact fails | required |
| Claim scope | The claim comment's stated commitments | The claim promises only investigation and a forthcoming report; it does not promise a fix, a timeline, or a root cause it has not yet shown | required |
| Repo conventions | The claim and repro comments, read against the repo's stated contribution policy (template, tone norms, and any AI-assistance disclosure requirement) | The comments follow the repo's stated posting conventions; where the repo's policy requires disclosing AI assistance, the comment discloses it | required |
| Report concision | The repro report's overall length and structure | The report covers environment, steps, and behavior without padding, repeated restatement, or unrelated detail | preferred |

## Verdict rule

Accept only if every `required` check grades `pass`. Any `required` check graded `fail` or `unclear` holds the package as `reject`. `preferred` checks are reported but never change the verdict. `unclear` is never treated as a pass: evidence the grader cannot verify is evidence that is not ready to post.
