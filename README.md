# FallClaimOnboard

**Sovereign FCA CMR + AML client onboarding for UK claims firms.**
Single HTML file. IDB-only. Device-local. Mobile-first. Forkable. MIT.

Prime **821** · v**1.0.0** · part of the `fallclaim` bundle (anchor 811, paper 823, practice 827).

---

## For UK claims firms (CMC + SRA-regulated)

You onboard a new claimant. The clock starts on a 14-day FCA CMR cooling-off period. You must:

- Identify the client (or their litigation friend / deputy)
- Assess mental capacity (Mental Capacity Act 2005)
- Disclose your **referral source** and any **referral fee** (post-LASPO ban for PI)
- Run CDD (identity + address evidence under MLR 2017)
- Issue the cooling-off notice (or capture a waiver if work must start immediately)
- Issue the complaints-handling notice (FOS route)
- Disclose fee structure (CFA / DBA / hourly · damages-based caps)
- Disclose ATE insurance position
- Run a conflict check (cross-tool broadcast on `fall-claim`)
- Capture documents (passport / driving licence / proof of address / photo evidence)
- Confirm + commit (writes Client, broadcasts `client.created`, appends audit entry)

FallClaimOnboard walks you through all 13 steps, keeps the **cooling-off register**, the **complaints register**, and the **conflict register**, and exposes an offline T0 Q&A for FCA CMR / LASPO / MCA / FOS / damages-based caps.

Everything stays on the device. No telemetry. No analytics. No server.

## For developers / forkers

- One `index.html`, **< 400KB**, vanilla JS, no build step, no framework
- IDB primary (`fallclaimonboard.v1`) with localStorage mirror fallback
- 7 IDB stores: `state`, `audit`, `documents`, `coolingOffRegister`, `complaintsRegister`, `conflictRegister`, `signingKeys`
- BroadcastChannel mesh: `fall-claim` (anchor + paper + practice) + `fall-signal` (estate)
- KONOMI sovereign-tier shim (`window.KONOMI`) and `window.FALLCLAIMONBOARD` console handle
- PWA manifest as `data:` URL — installable from any static host
- Aesthetic: oxblood `#8b1a1a` / brass `#b8974a` / cream `#e6e1d6` / void `#0b0a0f`
- T0 cascade with 13 CMR-tuned rules · T3 BYOK (Anthropic / Gemini free / OpenAI / OpenRouter)
- Audit chain (Mansoor P3): `prevHash` chained, 50k cap, SHA-256, FCA CMR 6yr retention

## 14-pt gate

1. ✓ Single HTML, <400KB
2. ✓ IDB primary, localStorage fallback
3. ✓ KONOMI sovereign shim
4. ✓ fall-claim mesh + fall-signal estate ping
5. ✓ PWA manifest (data: URL)
6. ✓ Mobile-first responsive
7. ✓ MIT LICENSE
8. ✓ Two-audience README
9. ✓ `.nojekyll` for GitHub Pages
10. ✓ Audit chain on by default
11. ✓ Sovereign disclaimer per shared schema
12. ✓ T0 offline + T3 BYOK cascade
13. ✓ Forkable engine name override
14. ✓ Demo seed (auto-purges on first real client)

## Deploy

Static host. Push to GitHub Pages with `build_type=legacy` and the `.nojekyll` file at root. No CI, no Actions.

## Cross-tool mesh

On boot the tool broadcasts `{type:'sync.request'}` on `fall-claim`. Sibling tools (`fallclaim`, `fallclaimpaper`, `fallclaimpractice`) respond with their snapshot. Conflict checks broadcast `conflict.check.request` — any tool with matching case/client records responds with hits.

## Disclaimer

> FallClaim is a tool for UK claims firms (CMC and solicitor practices). It assists with case management, fee tracking, regulated document generation, and FCA CMR / SRA compliance. It is not court filing software; pleadings and submissions remain the firm's responsibility. Sovereign — client data never leaves the device unless exported.

---

Built sovereign. Built complete. Built to last.
