# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

This is a front-end-only, clickable React prototype. It tests one bet: a trust panel on zero-review provider profiles (verification badges, borrowed Google/Facebook reviews, booking counts, demand signals) increases first bookings. It runs a simulated A/B test: arm A is a plain profile, arm B adds the trust panel. Arm B also has a booking path that goes from the Trust Verification Modal to a Schedule 10-Min Intro Call. A kill-switch tracker compares arm B to a 4% first-booking line (the baseline is 2.3%). There is no backend. Provider data, external reviews, verification statuses, availability and the experiment results are all hard-coded mocks. The loading, empty and error states of the "fetch" are simulated with a timer. Session counters (views, modal opens, intro calls, bookings) live in React state and reset on reload. Treat the UI, component boundaries and data shapes as the spec. Treat everything that looks like real data as made up.

## Architecture (plain language)

- **Frontend:** Stack: React 19, TypeScript, Vite 7. Charts use Recharts and icons use lucide-react. All styling is inline styles reading from src/shared/theme.ts. Tailwind is installed but these screens don't use it. No router. App.tsx holds a screen value and renders one screen at a time. The modal sits on top of the profile. Layout: files are grouped by feature under src/features/. Each feature has a *Data.ts file (mock content and pure functions) and screens/components that only display it.
- **Backend / data:** None exists. These are the mocks that stand in for future services: providerData.ts: profile, platform verifications, demand signals, portfolio, imported reviews. Future provider profile, trust/verification and review-import services. browseData.ts: search results. Future search service. introCallData.ts: availability, generated deterministically by slotState(). Future scheduling/availability service. killSwitchData.ts: fake 14-day rate curves for "lift" and "flat". Future experiment/analytics service. useExternalDataFetch(): a 1.4 s setTimeout that resolves to whatever outcome is picked in the on-screen control. Future review-import API call. Data rule already built in. Platform data always shows: ID, background check, license, insurance, booking count, demand signals. External data (Google/Facebook reviews, portfolio photos, endorsement) is gated on the fetch status. Keep that split when wiring real APIs.
- **Key flows:** Main path:
Problem screen → Browse.
Clicking Maya's card opens the profile and counts one view for the current arm.
The profile triggers the external data load: skeletons, then success, empty or error.
Arm B booking path:
Profile → "See verification details" (or a verified badge) opens the Trust Verification Modal and counts a modal open.
"Schedule a 10-min intro call" → pick a slot → confirm. This counts an intro call, not a first booking.
"Book Maya now" counts a booking for the current arm.
Direct booking: Profile → "Book Maya · $116" counts a booking for the current arm. This works in both arms.
Kill switch: the status bar, or tab 4, shows A vs. B, the arm B funnel, the daily chart and a continue/pivot verdict. "Simulate outcome" switches between the fake curves.

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Feature folders | solid | Screen and component names match the PRD, and data is separated from display. |
| Hard-coded booking details | rough | The date, time and job in the booking card are fixed. There is no payment, which is out of scope per the PRD. |

## Risks & assumptions for the team

- External reviews can be legally and reliably imported and attributed (Google/Facebook terms of service and rate limits).
- Real verification vendors exist: ID (selfie match), background check (Checkr is shown in the copy), license lookup (CSLB) and an insurance certificate.
- "First-booking rate" is defined per new provider and per buyer session on that provider's profile. A 4% kill line by day 14 has enough statistical power at real traffic levels. This has not been calculated.
- The "people booked" count is an acceptable stand-in for reviews and won't be read as completed jobs. The copy says "upcoming jobs".

## How to run it

```
npm install          # or: bun install (bun.lock present)
npm run dev          # Vite dev server, open the printed localhost URL
npm run build        # production build to dist/
npm run check-types  # note: template files under src/base_components have type errors
```
