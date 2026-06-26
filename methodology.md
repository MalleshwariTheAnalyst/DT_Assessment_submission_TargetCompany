# Target Company Research — Methodology

**Candidate:**  Kajana Malleshwari
**Segment focus:** Basket B — Industrial sensors & instrumentation (pivoted from Basket A — Specialty diagnostics & life-science tools, see "Pivot Rationale" below)
**City:** Hyderabad

---

## 1. Honest Status of This Submission

This submission does not contain the full 25 scored companies the assignment specifies. It contains **6 fully-sourced, evidence-backed companies** — 2 that pass eligibility gates with partial scores, 1 with a confirmed score in the C-band, and 3 that fail with documented reasoning — researched within the available time window using live web research (Tofler, Zauba/ZaubaCorp, Tracxn, MCA-adjacent registries, company websites, and press coverage).

I am submitting this as-is rather than padding the list with under-researched rows, because the assignment explicitly grades evidence quality over volume, and because **fabricating or thinly guessing at scores for 19 more companies would not be defensible if asked about them directly in a follow-up conversation.** I would rather show fewer companies researched honestly than 25 where most cannot withstand a follow-up question.

---

## 2. Process Used

**Tools and sources:**

- Web search across Tofler, ZaubaCorp, Tracxn, IndiaMART, company websites, and press/industry coverage (Scispot, BioSpectrum, regional tech press)
- I used Claude (Anthropic's AI assistant) as a research and drafting partner — it ran the searches, surfaced candidate companies, and helped structure evidence into the required rubric format. **All eligibility judgments, scoring decisions, and the decision to fail or pass a company were made by me after reviewing the evidence**, not generated automatically.
- A small Python toolkit (included in this submission) was used to validate the CSV schema and compute the Federer Score consistently from the Weak/Moderate/Strong ratings, so the arithmetic is consistent across rows and not manually summed by hand.

**What I did NOT use AI for:** the hand-drawn sketch of my thought process (submitted separately, per the assignment rules), and I did not let any tool auto-generate evidence text without me reviewing the underlying source first.

---

## 3. Pivot Rationale: Why I Moved from Basket A to Basket B

I initially targeted **Basket A — Specialty diagnostics & life-science tools**, given Hyderabad's strong reputation as a life-sciences hub (Genome Valley, 200+ companies). After researching 4 candidates in depth (D-NOME, Genomix Molecular Diagnostics, Empe Diagnostics, Megsan Diagnostics), I found a consistent pattern:

- **D-NOME**: excellent founder pedigree (ex-NIH/CDC-adjacent science, patent-pending tech, government recognition) but only ~Rs.1.22Cr revenue — too early-stage
- **Genomix Molecular Diagnostics**: genuinely strong certifications (ISO 13485, GMP/GLP) and a founder with NIH/CDC/Homeland Security background, but revenue has stayed under Rs.3Cr for over 18 years — never scaled past micro-enterprise size
- **Empe Diagnostics**: real manufacturing scale in Hyderabad (9-24 million kits/year capacity) but the actual decision-makers and company HQ are in Sweden — fails the "founder accessible in Hyderabad" requirement
- **Megsan Diagnostics**: a diagnostic *services* lab (testing/pathology), not a product manufacturer — fails the producer gate entirely

**The pattern I observed:** Hyderabad's diagnostics/life-science ecosystem is bimodal — either tiny founder-led R&D-stage companies (under Rs.5Cr revenue) or large/foreign-controlled entities, with very few companies in the Rs.50-500Cr founder-led "missing middle" that the Federer profile targets. This is itself a finding worth noting: the segment may be earlier in its maturity curve in Hyderabad specifically, compared to more industrially mature clusters elsewhere in India.

I pivoted to **Basket B — Industrial sensors & instrumentation**, reasoning that Hyderabad's broader electronics/EMS manufacturing base (driven by Telangana's ESDM policy push and defence/aerospace supply chains) would have a thicker population of mid-size, founder-led manufacturers. This pivot did surface one stronger candidate (Bhagyashree Industries) within the available time, though full validation was not completed.

---

## 4. Funnel Summary

| Stage                                    | Count                                                                                                                                        |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Companies fully researched               | 6                                                                                                                                            |
| Failed eligibility gates (E1/E2)         | 2 (Megsan Diagnostics — not a producer; Empe Diagnostics — decision-making not in Hyderabad)                                               |
| Passed gates, scored D-band              | 1 (Srilin Electronics — real manufacturer, but contract EMS with weak product differentiation and a financial stress signal worth flagging) |
| Passed gates, scored C-band (borderline) | 3 (D-NOME 42.5, Genomix 50.0, Bhagyashree Industries 42.5)                                                                                   |
| **Yield toward A/B band**          | **0 of 6 (0%)** — reflects genuine difficulty of this search, not a representative sample                                             |

**Note on Bhagyashree Industries — a verification correction worth flagging:** During research, an early lead (RocketReach profile for "Shridayal Suresh") incorrectly suggested this person was the founder. On closer verification against Tata Nexarc, Kompass, and the MSME/Udyam registry, this profile actually belonged to an unrelated home-appliances business in Salem, Tamil Nadu — a data error in a third-party directory, not a real connection to the Hyderabad company. I caught this before finalizing the score and corrected the decision-maker field accordingly (now pointing to Raghu Ram Patalay / Rohan Patalay, confirmed via Tata Nexarc and Kompass listings). I'm flagging this explicitly because it's a real example of why every fact needs a second, independent source before it goes into a score — a single directory listing is not enough.

After correction, Bhagyashree Industries scored **42.5/100 (C-band)**. This is held down mainly by two gaps: C4 (no public evidence of the decision-maker's systems-thinking, beyond confirming who they are) and C8 (succession status is genuinely unconfirmed — there are signs of possibly two related names at the company, but I could not verify a clear generational handover). With those two filled in, this could plausibly move into B-band, but I scored only what I could confirm rather than estimate upward. What is confirmed and strong: a 30-year operating history, real ISO 9001:2015/ISO 14001:2015 (TUV NORD) certification, a 21,000 sq ft dedicated facility, MSME "Medium Enterprise" classification (an upgrade tier, not just Small), and a product line that has expanded into EV chargers, Battery Management Systems, and smart locks — real evidence of capability investment, not just legacy products.

---

## 5. What I Would Do With More Time

1. Complete Bhagyashree Industries' remaining four criteria (LinkedIn search for founder/family background, hiring signals, ERP evidence)
2. Source candidates through the Telangana ESDM cluster directory and EEPC India's Hyderabad sub-regional office member list, which I identified as relevant but did not have time to fully mine
3. Cross-check more candidates against Tofler's Rs.50-500Cr revenue filter directly (rather than discovering companies first and checking revenue after) to reduce wasted research on companies that fail on scale alone
4. Investigate the Srilin Electronics bank-charge/net-worth-decline signal further before finalizing its score, since a financial distress signal materially affects the Federer fit

---

## 6. Files in This Submission

- `target_companies_scored.csv` — all 6 researched companies with full evidence and computed Federer Scores
- `target_companies_eligible.csv` — the subset that passed eligibility gates, sorted by score
