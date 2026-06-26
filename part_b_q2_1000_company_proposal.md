# The 1000-Company Proposal

**Goal:** Build a list of 1000 genuinely ICP-qualified ("Federer") companies within one month.
**Assumption:** Full access to AI tools (Claude/Gemini/Copilot), scraping infrastructure, paid database licences (Tofler Pro, Tracxn, ZoomInfo, etc.), and API credits.

---

## Grounding This Proposal in Real Experience

During my own Part A research (25-company target, ~48 hours, manual search only), I directly experienced the bottlenecks this proposal needs to solve:

1. **Identity confusion is a real risk at scale.** I initially attributed a company's founder profile from a directory site (RocketReach) that turned out to belong to an unrelated company with a similar name. At 1000-company scale, this kind of error will happen constantly unless cross-verification is built into the pipeline, not left to manual spot-checks.
2. **Revenue data is often missing for non-Pvt-Ltd entities.** Several genuine mid-size Hyderabad manufacturers are structured as Partnership Firms, which don't file MCA financials the way Pvt Ltds do. A scale pipeline needs a fallback (MSME/Udyam tier) rather than treating "no Tofler revenue" as automatic disqualification.
3. **General B2B directories (IndiaMART-style) have a high false-positive rate** — service providers and traders get mislabeled as manufacturers. Any scraper drawing from these sources needs a producer-vs-service classifier before companies even reach the scoring stage.
4. **Manual evidence-gathering is slow.** Even with AI search assistance, getting genuinely defensible evidence (not just a plausible-sounding paragraph) for one company across 6 criteria took multiple search rounds. At 1000-company scale this must be parallelized and partially automated, while keeping a human in the loop for judgment calls.

---

## Step 1: Where to Source the Initial Universe

Don't start from Google. Start from structured sources that already cluster companies by the right characteristics, then merge and deduplicate:

| Source | What it gives | Est. companies (India-wide) |
|---|---|---|
| Tofler/Tracxn bulk export, filtered by revenue band (Rs.50-500Cr) and NIC/industry codes matching Basket A/B/C | Pre-filtered by the single hardest criterion (revenue) | ~15,000-25,000 |
| MSME/Udyam registry, filtered to "Medium" tier + relevant NIC codes | Catches partnership firms/proprietorships Tofler misses | ~5,000-10,000 (with overlap) |
| Industry association member directories (ADMI, Pharmexcil, EEPC India, CII/FICCI state chapters, sector-specific bodies for each Basket) | Self-selected legitimacy signal | ~3,000-5,000 across associations |
| DSIR-recognized in-house R&D unit list (government, public) | Direct, audited C3 (Differentiated) proxy | ~2,000-3,000 relevant entries |
| State Invest-portal cluster directories (Genome Valley, ESDM clusters, industrial corridors) | Geographic + sector clustering | ~1,000-2,000 per major cluster |
| Trade expo exhibitor lists (INDEE, IESS, sector expos) for the last 2-3 years | Growth/export-orientation signal | ~500-1,000 per expo per year |
| Export Promotion Council member lists (Pharmexcil, EEPC, etc.) | Export orientation = often correlates with quality systems | ~5,000-8,000 |

**Merged and deduplicated universe estimate: 30,000-50,000 candidate companies** across all target cities and segments before any qualification filtering.

---

## Step 2: Automating the Qualification Step

This is a multi-stage funnel, not a single AI call. Each stage should mechanically eliminate the easy fails before spending expensive AI/human time on borderline cases.

**Stage 1 — Mechanical filters (no AI needed, pure data filtering):**
- Revenue band: keep only Rs.50-500Cr (from Tofler/Tracxn) OR MSME "Medium" tier (for partnership firms)
- City filter: target cities only
- NIC/SIC code filter: match against Basket A/B/C industry codes
- Status filter: exclude "Strike Off," "Dissolved," "Under Liquidation"
- Ownership filter: flag (don't necessarily exclude) companies with PE/institutional majority shareholding visible in Tofler's shareholding data, for manual review

This stage alone, done programmatically against bulk exports, should cut 30,000-50,000 down to roughly 8,000-12,000 in days, not weeks.

**Stage 2 — AI-assisted evidence gathering (the core automation):**
For each surviving company, an AI agent (Claude with web search/computer use) runs a structured research pipeline:
- Fetches company website, LinkedIn, recent news mentions
- Extracts: certifications (ISO/DSIR/GMP), product description, decision-maker name + designation, any visible hiring signals (ERP/systems roles), any visible succession signals (gen-2 mentions)
- **Critical guardrail, learned directly from my own mistake above:** every extracted "fact" (especially decision-maker identity) must be cross-confirmed against at least 2 independent sources before being trusted. A single-source claim gets flagged "unverified" rather than accepted.
- Outputs a structured evidence record per company (not a free-text paragraph) — same schema as the Part A CSV (E1/E2 gates, C3-C8 with evidence strings)

**Stage 3 — AI-assisted scoring, human-reviewed:**
- AI proposes a Weak/Moderate/Strong rating per criterion *with the evidence string visible alongside it*
- A human reviewer (or a small team, at this scale) spot-checks a sample (e.g. 20%) of each AI-scored batch, and reviews 100% of anything the AI flags as "borderline" or "evidence insufficient"
- This mirrors what I did manually in Part A — I personally decided every Pass/Fail and rating, AI helped surface and structure evidence

---

## Step 3: Quality Control

Three concrete failure modes, and the control for each:

1. **False positives (AI over-scores a weak company):** Require every Strong/Moderate rating to cite a specific, checkable fact (a certification number, a named executive, a specific revenue figure with source) — not a vague claim. Any rating without a checkable fact auto-downgrades to "needs human review."
2. **Missing/contradictory data (e.g. revenue band conflicts between Tofler and MSME registry):** Default to the more conservative (lower) estimate, and flag the conflict explicitly in the evidence record rather than silently picking one.
3. **Borderline cases (40-59 score range):** Route to a dedicated weekly human review session rather than letting them silently fall into either "include" or "exclude" — this is where judgment matters most and where I personally spent the most time in Part A (e.g. the Srilin Electronics financial-stress signal, which needed a human decision about whether it was disqualifying).

**Identity-verification step (directly from my own error):** Before any company enters the scored dataset, cross-check the decision-maker name against at least two independent sources (e.g. company's own website/MCA filing AND a separate directory). If they don't match or can't be cross-confirmed, mark "decision-maker unverified" rather than scoring C4/C8 on a guess.

---

## Week-by-Week Plan

| Week | Focus | Activities | Expected output |
|---|---|---|---|
| **Week 1** | Universe building + mechanical filtering | Pull bulk exports from Tofler/Tracxn/MSME registry/association directories; merge, dedupe, apply revenue/city/NIC-code/status filters | ~8,000-12,000 mechanically-filtered candidates |
| **Week 2** | AI-assisted evidence gathering at scale | Run the AI research pipeline across the full filtered list; build the structured evidence database; begin cross-verification of decision-maker identities | ~8,000-12,000 companies with structured (if uneven-quality) evidence records |
| **Week 3** | AI-assisted scoring + first-pass human review | Score all companies against C3-C8; human reviewers spot-check 20% of clear passes/fails and 100% of borderline (40-59) cases; re-run evidence gathering for any company flagged "insufficient evidence" | ~2,500-3,500 companies scoring 40+ (C-band or above) after review |
| **Week 4** | Final QC, deduplication, and packaging | Final human pass on all A/B band companies (the ones that matter most); resolve any remaining identity/data conflicts; deduplicate across segments/cities; package into final deliverable with full evidence trail | **Final target: 1000 companies, weighted toward A/B band, each with a defensible evidence record** |

---

## Realistic Yield Expectations at Each Stage

Based on the assignment's own stated ~30% yield benchmark, and my own experience where my actual yield was 0% in a small, difficult sample (6 companies, 2 segments) — which itself is a useful data point about how hard high-quality sourcing really is:

| Stage | Input | Output | Yield |
|---|---|---|---|
| Raw universe → mechanically filtered | ~40,000 | ~10,000 | ~25% |
| Mechanically filtered → evidence-gathered | ~10,000 | ~10,000 | ~100% (every company gets researched, not eliminated yet) |
| Evidence-gathered → scored 40+ (C-band or above) | ~10,000 | ~3,000 | ~30% (matches the assignment's stated benchmark) |
| Scored 40+ → final A/B-band-weighted 1000 | ~3,000 | 1000 | Take the top ~1000 by score, prioritizing A/B band, filling remainder with strong C-band if A/B band alone is insufficient |

**Honest caveat:** my own Part A experience suggests the 30% yield benchmark is optimistic for some segments (I found 0 of 6 in two segments) and likely needs segment-by-segment recalibration — some Basket categories (e.g. mature engineering/instrumentation clusters) will yield better than others (e.g. early-stage-heavy biotech clusters like Hyderabad's diagnostics scene). Week 1's mechanical filtering should track yield by segment in real time so the team can reallocate sourcing effort toward higher-yield segments by Week 2, rather than spreading effort evenly and discovering the imbalance only at the end.
