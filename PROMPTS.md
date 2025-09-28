# Base44 Prompts (final, human-style)

## Prompt 1 — Project setup & data model
“Let’s set up **Campus Shareable Kits — Hub-first Aggregator**. The idea: students can borrow easily from official hubs (libraries/makerspaces) or from peers as a fallback, so the sustainable choice is the easiest one. Create these collections:

- users: email, name, photo, dorm, reputation (default 80), is_verified (bool)
- orgs: name, type (library/makerspace/tool_library/other), address, hours_json, policy_url, contact
- org_items: org (ref), title, category (charger/tools/av/party/other), photos[], status (available/checked_out/maintenance), notes
- kits (peer): title, category, photos[], owner (ref users), status (available/reserved/out), location_text, notes, deposit_required (bool)
- requests: kit (ref), borrower (ref), owner (ref), org_item (ref optional), start_ts, end_ts, status (pending/approved/declined/collected/returned/late), message, created_at
- reviews: request (ref), rater (ref), ratee (ref), stars (1–5), comment
- impact_logs: request (ref), kit (ref), org_item (ref optional), avoided_purchase_prob (0–1), co2e_saved_kg, money_saved_usd, created_at

Confirm when ready.”

## Prompt 2 — Pages & UI (with styling)
“Create these pages with mobile-first, accessible Glassmorphism UI (teal/green accents, rounded cards, subtle blur/shadow, blue badge=Official, green=Peer; pills: green=Available, orange=Reserved, gray=Out). Pages:
1) Home/Discover: search, category chips, list/grid with badges; skeletons + empty state.
2) Item Details: hero photo, owner/org chip, status, policy chip, primary CTA that changes (Go to Hub vs Request to Borrow), Similar items.
3) My Requests: tabs Incoming/Outgoing with lifecycle actions.
4) Add Kit: form for peer items.
5) Impact: CO₂e avoided, items borrowed, $ saved; info modal explains factors.
6) Orgs Admin (demo): view/edit orgs + org_items.
Freeze the design system after creation.”

## Prompt 3 — Flows & lifecycle
“Add small, transparent flows:
- BestSource: decide hub vs peer using hours/availability; return JSON {source, id, reason}
- PolicyExplainer: short readable summary with source link
- BorrowVsBuy: borrow if uses/term < 5; return reason + $ estimate
- ImpactEstimator: fixed factors (Chargers 2, Tools 8, AV 50, Party 5, Other 3) × avoided_purchase_prob
- SimilarKits: up to 3 related items

Add server actions with role checks:
- create_request → pending
- owner_approve / owner_decline
- mark_collected (borrower)
- mark_returned (owner) → call ImpactEstimator → write impact_logs → open Review modal”

## Prompt 4 — Demo data & automations (with UMBC link)
“Seed demo:
- Org: ‘AOK Library — Digital Media Lab (DML)’; hours: weekdays 8–22, weekends 10–18; policy_url: https://library.umbc.edu/media/dml.php#dml_equip; contact: dml@umbc.edu
- Org_items: Projector, DSLR Camera, Tripod, Lapel Mic, HDMI Cable (available)
- Users: Vishal (borrower; verified true), UMBC Org Desk (manager; verified true)
- Peer kits: Phone Charger, Tool Kit, Bluetooth Speaker, Mini Projector, Power Strip, Party Kit (available)
- Requests: #1 approved (org projector) + #2 pending (peer mini projector)
Automations: toast on new request & on approve; reputation = clamp(avg(stars)*20, 40..100); CSV export; ‘How we estimate’ modal.
Styling: keep Glassmorphism consistency.”

## Prompt 5 — Finalize demo mode, intro & tutorial (with working controls)
“Finalize in demo mode:
- Public reads for orgs, org_items, kits, requests, reviews, impact_logs (no owner filters). Writes require sign-in; unauthenticated ‘Request to Borrow’ opens sign-in modal.
- Discover: don’t wait on auth; load org_items + kits immediately. If empty, call ensureDemoSeed (DML org + 5 org_items + 6 peer kits + demo user) then re-query. Impact: if empty, seed one demo impact log (e.g., projector, 50 kg CO₂e * 0.5) then render totals.

Onboarding polish:
- Intro card at top of Home with glassmorphism, teal accents:
  Title: ‘Campus Shareable Kits’
  Tagline: ‘Borrow smarter, waste less.’
  One-liner: ‘Connects official hubs and peer items, recommends the best source, and shows your sustainability impact.’
  A small illustration and a ‘Get started’ button that scrolls to the list.

- Tutorial overlay with working controls:
  State: { isOpen, stepIndex, steps[] }
  ‘Got it’ → next step; on last step, close overlay and persist dismissal.
  ‘Skip tutorial’ → close overlay and persist dismissal.
  Persist with users.has_seen_tour (if signed-in) or localStorage key (if not).
  Ensure buttons are clickable (no disabled/blocked events), Esc closes, and overlay doesn’t block data loading.

Republish so a new visitor sees the Intro card, can skip/complete the tutorial, and can browse items without login.”
