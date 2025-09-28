# Campus Shareable Kits — Hub-first Aggregator

> Built at **hackUMBC 2025** for the **Base44 Sustainable Tech** challenge.  
> **One-liner:** Borrow smarter, waste less. The app routes students to the *best* borrowing option — **official library hubs first**, **peer fallback** when needed — and shows the sustainability impact of choosing not to buy.

## 🌍 Problem
Campus hubs lend gear, but hours, stock, and scope are limited. When a hub is closed or out of stock, people default to buying items they’ll rarely use. That creates waste, duplicate spend, and makes the green choice harder than it should be.

## 💡 What the app does
- **Unified search:** Official hubs + peer kits in one place.
- **BestSource routing:** Hub first if open/stocked; otherwise peer fallback.
- **Policy summaries:** Plain-English rules with a direct link to the official page.
- **Borrow lifecycle:** request → approve/decline → collected → returned → review.
- **Impact dashboard:** CO₂e avoided, items borrowed, and money saved (simple, transparent math).
- **Onboarding:** Intro card on Home + a first-time tutorial overlay (works with “Got it” / “Skip”).

## ⚙️ Tech (Base44)
Collections: `users`, `orgs`, `org_items`, `kits`, `requests`, `reviews`, `impact_logs`  
AI flows (deterministic): `BestSource`, `PolicyExplainer`, `ImpactEstimator`, `BorrowVsBuy`, `SimilarKits`  
Server actions: request lifecycle + impact logging  
Design: Glassmorphism, teal/green accents, clear badges/pills, micro-animations

## 🔐 Demo vs Production login
- **Demo:** Public **read** so judges can browse instantly; **writes** (request/approve/return/review) require sign-in.
- **Production plan:** Campus SSO + strict Row Level Security (roles: Student, Peer Owner, Org Manager, Admin), deposits/holds for high-value items, late-return safeguards.

## 🌱 Impact math (transparent factors)
- Chargers: **2 kg CO₂e**  
- Tools: **8 kg CO₂e**  
- AV gear: **50 kg CO₂e**  
- Party: **5 kg CO₂e**  
- Other: **3 kg CO₂e**  
Formula: `co2e_saved = factor × avoided_purchase_prob (default 0.5)`

## 🔗 Links
Live App: _[Campus Shareable kit](https://campus-shareable-kits-38799360.base44.app)_

## 🖼 Screenshots
<img width="2179" height="1386" alt="image" src="https://github.com/user-attachments/assets/4e3802b7-757e-4269-a60f-a01a7e8aed29" />

<img width="2056" height="1066" alt="image" src="https://github.com/user-attachments/assets/a0a3a2f9-0cc0-43b4-83e4-c02f7efd730d" />

<img width="2083" height="1391" alt="image" src="https://github.com/user-attachments/assets/25b7c633-c126-4221-a1c6-2c7853223dcf" />





