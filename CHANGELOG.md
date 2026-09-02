# Changelog

Every entry cites its source. Undated or unsourced claims do not belong here.

---

## 2026-08-25

### Corrected — errors found by checking Gmail against the SoS transcripts

- **AI Individualize was not "awaiting Ali."** Ali Lootah signed off the UAT
  build on 24 Aug: *"The build looks good overall. The Activations team will
  share a few copy updates, but from our side, we are happy to proceed with the
  closed-group testing."* PROD Closed Group setup is underway; only copy updates
  from Activations remain. The dashboard had been showing a 29–30 Jul
  "awaiting Ali" state.
  *Source: Gmail — "AI-Individualised Offer – UAT Testing & Handback File", 20–24 Aug.*

- **Infinity was not stalled.** The 17 Aug alignment call went ahead, a
  discovery-led approach was agreed, and the proposal was sent on 21 Aug — a
  four-week Discovery & Scoping engagement concluding in an agreed Scope of
  Work, a confirmed mobile technology direction, and a Build-phase plan. Awaiting
  Chris Gale's response.
  *Source: Gmail — "Emirates-Juggernaut Connect on Infinity Strategy", 17–21 Aug.*

- **27 Aug is an internal rehearsal, not a client call.** Calendar:
  "[Placeholder] Agentic Journey MVP Demo – Rehearsal", 17:00–17:45 IST, Teams.
  Previously recorded as "Call with Anita."

### Added

- **Emirates** — Sept 2 agentic journey demo to Dr. Najjib, a negotiated hard
  date. UAT deployment (`215-compass`), TestFlight v2217, opt-in flow complete,
  partner coverage 25 → 95 confirmed URLs → ~200+ processing. Open blocker:
  Octa JWT vs Gravity JWT mismatch. Privilege-code duplication capped at 256
  affecting ~12,000–15,000 members, run as a separate serialised track.
  *Source: AI SoS 11, 18, 19, 20, 21, 24 Aug.*
- **WestJet** — moved off On Track. Client rejected a search solution proposed
  two months prior and refuses the rate-return approach for bonus offers,
  insisting on full in-system simulation. 15 API calls per flight search;
  promotional rules at segment level; GDPR transaction-deletion unresolved.
  *Source: AI SoS 20–21 Aug.*
- **Sunrise** — newsletter detail (7 blocks, up to 10 items each, "baskets" of
  offers, 1.4M members) and the competitive risk: Sunrise has an in-house team
  ready to build it, validated internally as competent.
  *Source: AI SoS 11, 19, 20, 21 Aug.*
- **Deutsche Telekom** — AI Translate discussions resuming after the World Cup
  pause; call expected this week, date not fixed. DT runs its own in-house
  recommendation model and data system (DDDL) rather than GRAVTY®.
  *Source: AI SoS 11 Aug + internal update 25 Aug.*
- **GHA** — batch alert volume too high, requirements needed from client.
  AI Trust "on hold" threshold defect capturing scores of exactly 0.5.
  *Source: AI SoS 11, 21 Aug.*
- **Jumeirah** — AI Recommend attribute seeding (check-in/checkout), point
  balance filtering with comparison operators, geo-location filtering requested
  and challenged pending data validation. Targeting the 261 release.
  *Source: AI SoS 11, 24 Aug.*
- **Mashreq Bank** — portfolio table row added; it had an attention card but no
  row. Built from existing data, no new facts.

### Changed

- Agentic AI Compass → On Hold. Scoped as a proof of concept; POC complete, no
  further next steps. Jira AT-115 transitioned to On Hold.
- AI Sense owner → Monika Upadhayaya. Jira AT-3 reassigned from Vishnu Sankar.
- KPI tiles recomputed from actual card data rather than left hardcoded:
  Active 9, Require Attention 5, On Hold 8, On Track 0.

### Removed

- Qatar — added then removed at the user's request.

---

## Known gaps

- Commercial items from the 24 Aug SoS — a $3,000 flat-fee AI recommendation
  module and 10 requested changes under analysis — are **not** in the dashboard.
  The transcript does not name the client and the attribution was not guessed.
- Kalpak's directive to Kapileswar to stand up a Google Sheet AI adoption
  tracker is not reflected. In that same discussion the active AI client count
  was given as **three — GHA, Emirates, Jumeirah**, against nine here. The two
  are counting different things; the discrepancy is unreconciled.
