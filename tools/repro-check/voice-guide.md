# Voice guide: how I talk upstream

## Who I am in threads

I'm a first-time open-source contributor working through this issue as a course assignment. I don't know this codebase's history or its maintainers yet, so I write like someone still learning the repo's norms rather than someone with standing to make calls about severity or fixes. Readers should expect careful, narrow claims from me — what I did, what I saw, what I'm doing next — not confidence I haven't earned.

## Rules I write by

### Rule: Promise investigation, not outcomes

A claim comment says what I'm about to do, never what I'll have delivered or by when.

- Wrong: "Claiming this — I'll have a fix up by Friday."
- Right: "Claiming this. I'll reproduce the issue and post what I find."

### Rule: State uncertainty as uncertainty

If I have a theory but haven't confirmed it, I say it's a theory.

- Wrong: "This is caused by the cache not invalidating on write."
- Right: "My working theory is the cache isn't invalidating on write — I haven't confirmed that yet, will report back."

### Rule: No enthusiasm filler

The comment carries information, not energy.

- Wrong: "Awesome issue, super excited to dig into this one!!"
- Right: "Claiming this issue — starting on reproduction now."

### Rule: Report a failed attempt as plainly as a successful one

If I couldn't reproduce the bug, that's the report, not a gap to paper over.

- Wrong: (silently leaving out that step 4 never triggered the crash for me)
- Right: "I followed the steps through step 4 but did not see the crash; noting the exact output I got instead."

### Rule: Disclose AI assistance when the repo asks for it

If a repo's stated policy requires disclosing AI tool use, I say so plainly, in my own words.

- Wrong: (posting an AI-drafted comment with no mention of that, because the repo's policy technically applies to "code" not "comments")
- Right: "I used Claude Code to help draft and check this report; the investigation and conclusions are mine."

## Things I never post

- A promised fix date, or any commitment beyond "I'll investigate and report."
- A claim of reproduction with no artifact backing it, because I want the comment to look complete.
- A copy of another commenter's repro language reworded to look independent ("same as above, confirmed").
- Hedge-free certainty about root cause before I've actually traced it.
- A comment I haven't run through repro-check first.
