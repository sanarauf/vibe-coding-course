# Full-Stack: Data, Access Rules, Edge Cases, Deploy

> Module 5 · Full-Stack. Add data schemas, access rules, and edge cases; stress-test and deploy.

## Deployed link

_The working, shareable link that survives real users._

https://genuine-sable-2e756b.netlify.app

## Data schema

| Entity | Key fields | Notes |
|---|---|---|
| providers | id, slug, category_id, area_id, status, rating | Catalog. Only active rows are listed. Views provider_trust_summary and provider_monthly_bookings provide public counts. |
| bookings | provider_id, buyer_id, scheduled_for, status, idempotency_key | Unique index blocks duplicate requested or confirmed bookings for the same provider, buyer and time. |

## Access rules

_Who can see / do what? Where are the auth boundaries?_

- Anonymous visitors can read the catalog and the public count views. They cannot write to tables directly.
- Booking, intro calls, and event logging go through security definer functions (create_booking, schedule_intro_call, log_event, ensure_buyer). The old prototype’s open anon insert policies were dropped.
- Invites: a sender can read only their own rows (RLS). Insert, update and delete are revoked for signed-in users. Writes go through send_invite and accept_invite, which check the caller’s identity on the server. accept_invite requires the signed-in email to match the recipient.
- anon cannot run the invite functions.

## Edge cases hardened

| Case | Before | After |
|---|---|---|
| Empty / first-run state | Prototype accepted any insert from anon; no duplicate checks | Category with no pros shows a message and a Get Started button. Invites list shows “Send your first invite.” |
| Bad / malicious input | Prototype accepted any insert from anon; no duplicate checks | Server validates email format, lowercases it, rejects self-invites, rate-limits to 20 invites/hour. Duplicate bookings and intro calls are rejected by unique indexes. |
| Failure / offline | Catalog silently fell back to mock data; booking errors were silent | Catalog shows an error with Retry. Booking failure shows an alert. Invite and intro call errors show inline messages. |

## Stress test results

_What you threw at it, and what held / broke._

When I went "Offline", the site showed a native "no internet" error. I can build that out further for a better UX. And then when I attempted to rage-click the "book" button, I got another native error informing me I cannot submit more than once. It was functional, but the next step would be to update the UI for a cohesive UX.
