# Voice guide

## Rules

### Rule: Promise the investigation, not the fix

A claim commits only to what I will do next and to posting a repro report. No fix, no PR, no date.

- Wrong: "I'll have a PR up fixing this by Friday."
- Right: "I'm going to reproduce this from a clean setup following the README and will post a repro report here."

### Rule: Name the specifics

Every comment names the exact files, keys, or behavior in the issue, so it can't be pasted onto a different issue.

- Wrong: "Looks like a config problem, I'll take a look."
- Right: "The README says to set one API key and .env.example lists a different one. I'll check which one the app actually reads."

### Rule: Show, don't assert

A repro comment shows the environment and the observed output. It never just says it happened.

- Wrong: "Reproduced, the key is wrong."
- Right: "On macOS 15, Python 3.12, fresh clone at <commit>: after following the README, the app fails with <exact error>. Output below."

### Rule: Own words, even on a shared issue

I never piggyback on someone else's repro. My proof goes up in full, written by me.

- Wrong: "Same as above, can confirm."
- Right: "I reproduced this independently. My environment and steps are below."

### Rule: Follow the repo's disclosure policy

If the repo requires disclosing AI assistance, every comment I post discloses it.

- Wrong: (a comment with no mention of AI help on a repo that requires it)
- Right: "Disclosure: I used Claude Code to help draft this comment and set up the repro."

## Things I never post

- A fix, PR, or date promised in a claim
- "Same as above" or "+1" in place of my own repro
- "Reproduced" without the environment and the observed output
- Guesses at the root cause stated as fact
- Anything that skips the repo's AI-disclosure requirement
