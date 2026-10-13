# PROMPTS.md: Living Prompt Pack

> Module 3 · Prompt Chaining. Re-architect the build with prompt chains; capture the reusable ones here.

## How to use this pack

_Each prompt is a reusable step. Chain them: the output of one becomes the input to the next._

## Prompt chain: The Trust-to-Conversion Chain

### Step 1: Expand, build new screens in a strict sequence
```
Build the next phase of this app in a strict sequence:
1. Add a screen "Trust Verification Modal".
2. Add a screen "Schedule 10-Min Intro Call".
3. Navigation: write the logic so the Trust Verification Modal links to the Schedule 10-Min Intro Call.
Build these in order so the Trust Verification Modal is the anchor for the booking flow.
```

### Step 2: Behavior, hard-code the states
```
Apply the following logic constraints to the provider profile and booking flow:
- Use skeleton screens for external reviews and portfolio asset loading states.
- If no data is present, show the empty state: "Early Adopter Perks: Be among the first to book this verified new provider and lock in introductory rates.".
- On fetch failure, trigger the error state: "Unable to verify external credentials right now. Platform-backed Alloy Trust Guarantee still applies.".
Maintain the same design language throughout and tether all behavior strictly to these rules.
```

### Step 3: Refine, one surgical polish
```
The Sticky Trust & Conversion Bar needs a professional modern marketplace polish.
1. Start by listing the 3 biggest gaps in typography and spacing compared to top conversion benchmarks.
2. Once you've identified those, resize the headers and update the primary CTA and live proxy trust metrics (e.g., '14 people safely booked this month · Verified ID') to match.
Don't change anything else in the project or touch the underlying logic.
```

## Reusable techniques learned

- _____
- _____

## What broke (and the fix)

_Where a single mega-prompt failed and chaining fixed it._

_____
