---
title: 'Capstone team pitch website — second build (light portfolio vibe)'
type: 'feature'
ticket: ''
created: '2026-11-18'
status: 'built'
baseline_revision: 'b7f4d4b7dfae06ca869ef925c3ce77f6b6c4a6a8'
route: 'full'
route_source: 'auto'
risk: 'low'
review: 'quick'
review_source: 'pinned'
lenses_ran: [quick]
review_loop_iteration: 0
context: []
---

<frozen-after-approval reason="human-owned intent — do not modify unless human renegotiates">

## Intent

**Problem:** The group has one dark-themed site draft and wants a second, visually distinct build to compare: a company-facing pitch page that turns cold-email readers into a short call.

**Approach:** Build a new standalone static site in `site-v2/` that follows the brainstorm story arc and placeholder rules, styled after the clean light portfolio mood board, using only real facts from the brief and member assets.

## Boundaries & Constraints

**Always:** original wording throughout (no lines or structure from any example site); story arc hook → bet → proof-as-method → people → offer + ask; `[fill in with details later]` for any unconfirmed fact, never invented detail; no IP or budget content anywhere on the page; `site/` left untouched; the new build serves on its own port.

**Never:** modify anything under `site/`; add a fixed project list (the site universalizes, the email personalizes); add a backend, forms, JS frameworks, or tracking; commit anything.

## I/O & Edge-Case Matrix

| Scenario | Input / State | Expected Output / Behavior | Error Handling |
|----------|--------------|---------------------------|----------------|
| Page load | GET / on the new server | 200 with the full pitch page | No error expected |
| Missing page | GET /nope | 404 plain-text | No error expected |
| Path escape | GET /../secret | 403 Forbidden | No error expected |
| Narrow screen | viewport ~390px wide | single column, no sideways scroll | No error expected |

## Decisions

- **Cold open: proof moment first.** The hero opens on a proof moment (hackathon win / on-site line), then the claim. Chosen by random draw at the user's request; first draft, open to change.
- **Lead proof: Mangrover first.** The Mangrover cross-member build story anchors the proof section, followed by the bicycle-rack story. Chosen by random draw at the user's request; first draft, open to change.

</frozen-after-approval>

## Code Map

- `_bmad-output/brainstorm-capstone-website/handoff-brief.md` — the spec: story arc, tagline, proof blocks, locked decisions, placeholder convention
- `_bmad-output/brainstorm-capstone-website/.memlog.md` — rationale: email/site split, original-wording rule, story-driven reveal
- `Assets/info.docx` — identity draft, per-member roles and evidence, working terms (kickoff, check-ins, handover)
- `Assets/Capstone Placeholder.pdf` — real member profiles; fills people detail plus Mangrover, KABAM, Murata, and rack facts
- `Mood board/photo_2026-11-17_22-28-05.jpg` — the chosen vibe: clean light product-design portfolio
- `Mood board/Capstone Placeholder.png`, `Mood board/Capstone Placeholder (1).png` — CAD renders reused as placeholder imagery
- `site/index.html`, `site/styles.css`, `site/server.js`, `site/package.json`, `site/assets/*` — READ ONLY, never modify; shows the prior arc mapping and the server pattern to mirror on a new port

## Tasks & Acceptance

**Execution:**
- [x] `site-v2/index.html` — write the pitch page on the story arc with real facts and visible brackets — the deliverable
- [x] `site-v2/styles.css` — light portfolio styling per Design Notes with a narrow-screen layout — the chosen vibe
- [x] `site-v2/server.js` — static server mirroring `site/server.js` on port 3001 — local preview without touching v1
- [x] `site-v2/package.json` — package with a start script — run parity with v1
- [x] `site-v2/assets/chassis.png`, `site-v2/assets/component.png` — copies of the mood-board CAD renders — placeholder imagery until real photos exist

**Acceptance Criteria:**
- Given the page loads, when a reader scrolls top to bottom, then they meet the claim, the thesis plus method, proof stories, the five people, and the call ask in that order.
- Given any fact the group has not confirmed, when it appears on the page, then it shows exactly `[fill in with details later]` instead of invented detail.
- Given a company reader skims for IP terms, budget, or a fixed project list, when they read the whole page, then none of the three appears.
- Given the v1 folder, when this work is done, then every file under `site/` is byte-identical to the baseline revision.
- Given a phone-width viewport, when the page renders, then all text stays readable with no horizontal scrolling.
- Given the new server running, when a visitor opens its URL, then the pitch page loads with styling and images intact.

## Implementation Notes

- Subagent wrote all `site-v2/` files from the plan, then stalled on a package-install approval; parent cancelled it and took over (no installs used anywhere).
- Parent enriched proof with real PDF facts (Mangrover wheels/probe roles, rack event name + hardware credit, KABAM/Murata one-liners) and removed the builder's scratch screenshot `_tmppdf.png` from the repo root.
- Verification: live `server.js` on 3001 → `/` 200 html, `/styles.css` 200 css, `/assets/chassis.png` 200 png, `/nope` 404, `/../secret` 403; content rules pass (tagline, Mangrover lead, event name, 10 brackets, no budget/IP terms); 860px media query collapses all grids to one column; `site/` untouched.

## Plan Change Log

## Review Triage Log

Pass 1 (quick): high 0, medium 1, low 2, false 1, maybe-false 0.
- F1 `low`, patch — `.team` stayed 2-up at 390px while the matrix says single column; narrow but readable, so cosmetic; fixed to `1fr`.
- F2 `medium`, patch — `GET /%` throws in `decodeURIComponent` and kills the preview server; real crash on a dev server, restart recovers; guarded with a 400 branch.
- F3 `false`, rejected — `startsWith` guard is sound because `path.join(root, …)` can only yield root or paths under it, never an extended sibling; live `/../secret` returns 403.
- F4 `low`, patch — 403 lacked the `Content-Type` the 404 branch sets; harmless inconsistency; header added.

## Design Notes

Vibe: the clean light portfolio board (`photo_2026-11-17_22-28-05.jpg`), per Clarice's "simple modern, not cluttered, for tech/engineering companies" steer — and maximally distinct from the dark v1. Light ground, near-black ink, one restrained accent, generous whitespace, card-based proof, quiet top bar with anchor links, one closing ask panel.

Token sketch: bg `#f7f7f5`, surface `#ffffff`, ink `#16181a`, muted `#5c6468`, line `#e2e5e7`, accent deep teal `#0f766e`. System font stack, no webfonts (offline-safe).

Arc mapping: hero claim + subline + ask strip → thesis + 3-step method → lead proof story with further-applications line + proof cards (Mangrover / KABAM / Murata with real one-liners from the PDF where known, brackets elsewhere) → five people with role plus one real evidence line each → working-together terms + short-call ask panel → footer with the bracket legend.

Cold open and lead proof follow the Open Questions decisions below.

## Verification

**Commands:**
- `node site-v2/server.js` with `PORT=3001`, then `curl` `/` (expect 200), `/nope` (expect 404), `/../secret` (expect 403)
- `git status --short site/` shows no modifications under `site/`

**Manual checks (if no CLI):**
- Open the page and compare the feel against the chosen mood board; check ~390px width; confirm brackets visible wherever facts are missing.

