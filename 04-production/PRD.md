# Living PRD

> Module 4 · Production Specs. Refactor for readability; extract a living PRD that stays true as the build evolves.

## Problem

_What user problem does this solve? Tie to the validated hypothesis._

Marketplace bookings have flattened because buyers hesitate to take a chance on zero-review providers, creating a trust barrier that blocks new providers from getting started. This directly ties to our validated hypothesis: We believe a trust panel, verification badges plus early social proof, on new-provider profiles will cause more first bookings for zero-review providers for buyers browsing new providers.

(Note: In this prototype, verification badges, external reviews, and booking counters are mocked/simulated to test user conversion behavior before building real automated verification pipelines.)

## Users & jobs

- **Primary user:** Buyers browsing new marketplace providers, and zero-review providers needing a first booking.
- **Job to be done:** Give hesitant buyers immediate confidence through alternate verification, social proof, and a clear introductory booking path so they can safely convert on new providers.

## Scope

- **In:** Verified trust panels, external review placeholders (Google/Facebook imports), introductory rate perks, skeleton loading states, empty states, and the 10-minute intro call booking flow.
- **Out (explicitly):** Full automated payment processing, production-grade identity verification APIs, real-time messaging infrastructure, and multi-vendor dispute management workflows.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Trust Verification & Social Proof Panel | Must | Display external credentials, verification badges, and borrowed social proof prominently on zero-review profiles. |
| 2 | Schedule 10-Min Intro Call Flow | Should | Provide a seamless modal navigation path from trust verification directly to scheduling an introductory call. |

## Data & events

_What gets stored, what gets tracked._

- What gets stored: Mock provider verification statuses, profile metrics (booking counts, borrowed review aggregates), and simulated intro call booking requests.
- What gets tracked: Search-to-profile conversion rates, drop-off points at zero-review profiles, and click-through rates on trust verification badges and booking CTAs.

## Open questions

How will we scale automated external review imports without manual verification overhead once the marketplace expands beyond the MVP?
