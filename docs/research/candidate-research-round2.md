# Razorpay AI Buildathon 2026 — Open Track, Round 2 Research
### (Candidate A — MSME 45-day payment compliance — set aside unchanged, used only for final comparison)

**Method note:** Problem-first. I searched regulatory filings, news, and industry commentary — not "AI hackathon ideas." Every candidate below is graded on the 13 axes you specified. To keep 20–30 candidates readable, I give the **full 13-field profile** to every candidate that survives an initial sanity check (real + not obviously track-overlapping + not obviously saturated), and a **compressed one-line verdict** to candidates that fail that sanity check immediately — forcing full analysis on a dead idea wastes your time more than it proves rigor. Unverified reasoning is marked **(assumption)**.

---

## Headline finding, upfront

While researching payment-aggregator regulation, I found something time-sensitive enough that it changes the shape of this whole round: **RBI's deadline for payment aggregators to complete merchant re-KYC is 15 September 2026 — eleven days from today** — and payment aggregators are, as of today, publicly asking RBI for more time because they can't finish in time [BusinessToday, published 2026-09-04](https://www.businesstoday.in/latest/corporate/story/payment-aggregators-seek-more-time-from-rbi-to-complete-merchant-re-kyc-report-553334-2026-09-04). That became Candidate B below, and it reshapes the top 5.

---

## The Candidate List (26 problems)

### 🅱️ Candidate B — Merchant re-KYC completion crisis for Payment Aggregators
*Full profile below in the Top 5 section — this is the strongest finding of this round.*

### Candidate D — Merchant category/classification integrity for Payment Aggregators
*Full profile below.*

### Candidate E — TReDS/invoice-discounting platform fragmentation for MSME sellers
*Full profile below.*

### Candidate C — SME import/export FX-hedging decision support
*Full profile below.*

### Candidate F — Ongoing UBO / beneficial-ownership change monitoring for merchant portfolios
*Full profile below.*

### The remaining 21 candidates (sanity-checked and eliminated immediately)

| # | Problem | One-line verdict |
|---|---|---|
| 7 | RPT (related-party transaction) pre-payment approval gating (Companies Act §188 / SEBI LODR) | Real regulatory mechanism **(assumption — only explainer sources found, no evidence of acute current pain)**; weak "why now"; likely reads as Finance Controller (books/approvals). 🔴 |
| 8 | GST scrutiny-notice response automation for SMEs | Real, but already actively served — open.money and aiaccountant.com both sell this today [open.money](https://open.money/blog/automating-gst-notice-tracking-and-response-management/). 🟠 saturated. |
| 9 | Cross-border D2C customs/duty checkout friction (DDP vs DDU) | Real, but a heavily saturated global category — ShipBob, Portless, Cahoot, SellAbroad, nshift all sell this today. 🔥 saturated; also reads as Growth/Agentic Commerce (checkout conversion). |
| 10 | Gig/quick-commerce delivery-partner onboarding compliance drift | Real labor-market trend **(assumption)**, but weak/no direct payments-fintech angle found; more HR-tech than fintech. |
| 11 | Cost-of-acceptance / blended MDR analytics across multiple PSPs | Real gap **(assumption)**, but the value proposition ("save on payment costs") reads directly as Agentic Commerce ("grow the merchant's revenue"). 🔴 |
| 12 | Milestone-based B2B/freelance escrow payment release | Real need, but heavily saturated — Escrow.com, Upwork, Paysprint SprintEscrow all already do this [paysprint.in](https://www.paysprint.in/excrow.html). 🔥 saturated. |
| 13 | Nodal/escrow account RBI PA-PG compliance monitoring (from Round 1) | Already assessed — overlaps reconciliation (excluded) and is deep infra plumbing, hard to demo. 🔴 |
| 14 | Payment orchestration/PSP failover during outages (from Round 1) | Already assessed — saturated, and Razorpay itself already publishes this narrative. 🔥 |
| 15 | AP duplicate-invoice fraud detection (from Round 1) | Already assessed — globally saturated (Ramp, Precoro, Tipalti) and reads as Finance Controller/Risk Manager. 🔴 |
| 16 | Vendor/business identity verification at onboarding (from Round 1) | Already assessed — served by AuthBridge/Veridion/OnGrid. 🟠 |
| 17 | Buyer credit-risk score for MSME suppliers extending trade credit (from Round 1) | Already assessed — Recordent's KnowYourBusinessScore already owns this framing. 🔴 |
| 18 | UPI/payment-infra resilience observability | Already assessed — SRE problem, not a demoable product; also close to Risk Manager. 🔴 |
| 19 | Multi-entity treasury cash pooling | Already assessed — literally "run the cash position," Razorpay's own Finance Controller wording. 🔴 |
| 20 | Employee/vendor T&E and corporate-card compliance | Already assessed — one of the most saturated fintech categories in India (Ramp, Zaggle, Enkash, Happay). 🔥 |
| 21 | Warranty/AMC/service-contract payment lifecycle tracking | Weak evidence of acute pain, still true this round. Rejected for evidence weakness. |
| 22 | E-invoicing threshold expansion (₹1 crore AATO from Apr 2025) onboarding burden | Real and current [gimbooks.com](https://www.gimbooks.com/blog/e-invoice-applicability-limit-in-2025-latest-rules-threshold-who-must-comply/), but the natural solution (real-time IRN generation at POS) drifts into checkout/Growth territory, and ITC-matching drifts into excluded reconciliation. 🟡 |
| 23 | Digital lending co-lending settlement mismatch between banks/NBFCs | Real **(assumption)** but requires institutional data access no student team can get; also reconciliation-flavored. Unbuildable MVP. |
| 24 | Beneficiary/payee name-mismatch in high-value B2B transfers | Already assessed (Round 1) — reads as payment-failure recovery, explicitly excluded. 🔴 |
| 25 | Marketplace COD/reverse-logistics return fraud | Already assessed — directly named in Razorpay's own Risk Manager description ("fraud, returns and chargebacks"). 🔴 |
| 26 | Merchant category-code (MCC) misclassification / interchange arbitrage by PAs | Real and very current — RBI is actively investigating this, ₹5,000+ crore/month in flagged volume [business-standard.com](https://www.business-standard.com/amp/finance/news/rbi-lens-on-payments-fintechs-over-misclassified-merchants-125052901817_1.html) — **but this specific framing (aggregators deliberately gaming interchange for margin) is closer to fraud/regulatory-arbitrage than an "AI-solvable operational pain," and reads as Risk Manager.** I kept the *defensive/compliance-integrity* reframing of this as Candidate D below, which is meaningfully different from the arbitrage-detection framing rejected here. |

---

## Elimination Summary

Of 26 candidates, 21 are eliminated outright (saturated, track-overlapping, weak evidence, or unbuildable). **5 survive** for full profiling: **B, D, E, C, F.**

---

## Top 5 — Full 13-Field Profiles

### 🥇 Candidate B — Merchant Re-KYC Completion & Field-Verification Triage for Payment Aggregators

| Field | Assessment |
|---|---|
| **Problem** | Under RBI's Payment Aggregator Master Directions 2025, every PA (online, offline, cross-border — a category that now explicitly includes payment-gateway players, not just wallet apps) must complete full re-KYC of its **existing** merchant base by **15 September 2026**, and RBI mandates that in-person verification be done by the **PA's own employees**, not third-party agencies [ikigailaw.com](https://www.ikigailaw.com/article/639/rbi-rewrites-the-payment-aggregator-rulebook). With days remaining, PAs are asking RBI for an extension, expecting to reach only ~80% completion, with industry estimates that **30–35% of small informal offline merchants may not complete verification in time** [freepressjournal.in](https://www.freepressjournal.in/business/payment-aggregators-seek-rbi-extension-for-merchant-re-kyc-deadline). |
| **Who suffers** | Payment aggregators' own compliance/ops teams (workforce-constrained field agents), and the merchants themselves — missing the deadline risks losing digital payment acceptance entirely [businesstoday.in](https://www.businesstoday.in/latest/corporate/story/payment-aggregators-seek-more-time-from-rbi-to-complete-merchant-re-kyc-report-553334-2026-09-04). |
| **Existing solutions/competitors** | Generic Video-KYC vendors (HyperVerge, Signzy, PayU) handle the *digital capture* step; generic field-service route-optimization tools (Salesforce Field Service, Domo, Praxedo) exist for logistics. **No vendor found combining regulatory-deadline-aware risk triage + document-completeness prediction + field-agent dispatch specifically for this PA re-KYC exercise** — because the exercise itself is brand new (first-ever cycle under the 2025 Directions). |
| **Why current solutions insufficient** | Video-KYC tools solve capture, not *prioritization under a hard deadline and a fixed, RBI-mandated (own-employee-only) workforce* — the actual bottleneck named in the press coverage is staffing capacity and revisit rates, not the capture technology itself. Generic route-optimization tools have no notion of "regulatory risk weight" or "which merchants can legally use the lighter remote path" (RBI's Directions allow a 4-step lighter process for merchants under ₹40 lakh turnover). |
| **Why now** | The deadline is 11 days away as of today, and this is literally breaking news — published the same day as this research. This is not a recurring, well-worn pain (like AP fraud); it's a first-cycle, acute, dated crisis. |
| **3+ solution approaches** | (1) **Predictive triage + dispatch optimization** — score each unverified merchant on reachability, business impact, and regulatory risk, then generate an optimized daily field-agent route plan (a genuine constrained-optimization problem). (2) **On-device document/quality copilot** — vision-LLM checks document completeness/quality at the point of capture so agents don't need return visits (directly attacks the "revisit rate" bottleneck). (3) **Compliant-path classifier** — automatically route eligible small merchants to the RBI-permitted lighter remote/video path instead of an in-person visit, cutting field-visit volume at the source. (4) **Backlog/ETA forecaster** — models completion rate and produces a defensible, data-backed number for exactly the kind of extension request PAs are making to RBI right now. |
| **Where AI adds genuine value** | The triage/dispatch step is a real prioritization-under-constraint problem (not a chatbot); the document copilot is a genuine vision/extraction task with a clear before/after metric (revisit rate); the path-classifier is a policy-eligibility reasoning task over RBI's own published rules. |
| **Razorpay fit** | Razorpay is itself an RBI-authorized Payment Aggregator under the same Master Directions — this tool is something Razorpay's own compliance/ops org plausibly needs *this month*, not a hypothetical future integration. It could also become an internal ops tool Razorpay offers to smaller/partner PAs and banks who face the same structural, recurring problem (RBI has forced banks through near-identical periodic-KYC crises before, e.g., the long-running inoperative/frozen-account saga [moneylife.in](https://www.moneylife.in/article/rbi-asks-banks-to-enable-seamless-kyc-updation-urgently-bring-down-number-of-inoperative-or-frozen-accounts/75768.html)). |
| **Demo feasibility** | High — synthesize a merchant portfolio (location, turnover, transaction volume, document status), simulate a fixed field-agent capacity, show the optimizer's completion-rate curve vs. a naive FIFO baseline, and demo the document-quality copilot on sample images. All buildable with synthetic data in a hackathon window. |
| **Measurable impact** | % increase in on-time re-KYC completion, reduction in field-agent revisit rate (direct cost per merchant verified), number of merchants (and their transaction volume) saved from suspension. |
| **Why outside the 4 tracks** | Not Growth/Agentic Commerce (no merchant revenue angle). Not Revenue Recovery (nothing owed, nothing being chased). Not Finance Controller (no books, no cash position). The one real risk is Risk Manager — addressed explicitly in the stress test below. |
| **Saturation** | 💎 Highly differentiated — the underlying regulatory exercise is less than a year old and hits its first deadline in 11 days; no existing vendor has had time to build for this specific combination. |
| **Track-overlap risk** | 🟡 Moderate, on Risk Manager only — mitigated by framing (see stress test). |

### Candidate D — Merchant Classification Integrity & Audit Copilot for Payment Aggregators

| Field | Assessment |
|---|---|
| **Problem** | RBI is actively investigating payment aggregators for misclassifying retail merchants under lower-cost "utility" interchange categories — flagged transaction volume exceeds **₹5,000 crore/month** [business-standard.com](https://www.business-standard.com/amp/finance/news/rbi-lens-on-payments-fintechs-over-misclassified-merchants-125052901817_1.html). |
| **Who suffers** | PAs facing regulatory action and card-network rate hikes; honest PAs competitively undercut by those gaming the system. |
| **Existing solutions/competitors** | Generic MCC-lookup/reference tools exist (Cashfree, EnKash, PXP glossary pages) but these are reference databases, not compliance-audit systems. |
| **Why current solutions insufficient** | Reference tools tell you what an MCC *means*; none audit a PA's live merchant book against actual business activity to flag likely misclassification before a regulator does. |
| **Why now** | Active, ongoing RBI scrutiny as of 2025, with card networks already responding by raising utility interchange rates — the arbitrage window is closing and enforcement risk is rising in real time. |
| **3+ solution approaches** | (1) Classify true merchant business activity from transaction patterns/website content and flag MCC mismatches. (2) Portfolio-level audit scoring to prioritize manual review. (3) Self-correcting onboarding — validate MCC against business description at merchant sign-up. |
| **Where AI adds value** | Business-activity classification from unstructured signals (website, transaction descriptors) is a real NLP/classification task. |
| **Razorpay fit** | Direct — Razorpay assigns MCCs to its own merchants and carries the same regulatory exposure named in the RBI scrutiny. |
| **Demo feasibility** | Medium — needs synthetic merchant + transaction-pattern data; classification accuracy is harder to prove convincingly in 5 minutes than Candidate B's optimizer. |
| **Measurable impact** | ₹ interchange-margin risk exposure identified per audit run; % of book flagged for review. |
| **Why outside the 4 tracks** | Not Growth, Revenue Recovery, or Finance Controller. |
| **Saturation** | 🟢 Uncommon — but this is largely because it's a narrow, somewhat obscure regulatory-arbitrage story most teams won't stumble on. |
| **Track-overlap risk** | 🔴 High — this is fundamentally a fraud/gaming-detection story about protecting the PA from loss (regulatory penalty), which reads very close to Risk Manager's "detectors... for financial losses" framing, more so than Candidate B. |

### Candidate E — TReDS/Invoice-Discounting Platform Fragmentation for MSME Sellers

| Field | Assessment |
|---|---|
| **Problem** | MSME sellers seeking to discount receivables must manually choose and bid across multiple, non-interoperable TReDS platforms (RXIL, M1xchange, Invoicemart, C2FO/C2treds), each with different financier pools, fee structures, and turnaround times [karboncard.com](https://www.karboncard.com/blog/treds-platforms-in-india-compared-rxil-m1xchange), [finnovaadvisory.com](https://finnovaadvisory.com/insights/which-treds-platform-is-best). |
| **Who suffers** | MSME sellers (worse financing rates from not shopping the whole market) and the buyers/anchor corporates managing multiple TReDS relationships. |
| **Existing solutions/competitors** | Comparison/review content exists (invoicefollowups.com, karboncard.com) but no automated cross-platform bid-routing tool was found. |
| **Why current solutions insufficient** | Comparison articles are static and manual; sellers still have to separately register, upload, and bid on each platform themselves. |
| **Why now** | RBI has been actively pushing to expand TReDS participation and ease onboarding [m1xchange.com](https://www.m1xchange.com/treds-platform-operators-welcome-rbis-directive-to-ease-msme-invoice-discounting-boost-liquidity/), increasing the population of sellers who'd benefit from cross-platform optimization. |
| **3+ solution approaches** | (1) Cross-platform bid aggregator/router that submits one invoice across multiple TReDS platforms and recommends the best financier offer. (2) Eligibility pre-screening to avoid wasted platform-specific onboarding effort. (3) Predictive discount-rate benchmarking so sellers know if an offer is fair. |
| **Where AI adds value** | Offer comparison/ranking and eligibility prediction are genuine modeling tasks. |
| **Razorpay fit** | Indirect — Razorpay doesn't currently operate in TReDS; would be a new-ish adjacency rather than a natural product extension. |
| **Demo feasibility** | Medium — plausible with synthetic invoice/financier data. |
| **Measurable impact** | ₹ saved in discount-rate spread per invoice, time-to-financing reduction. |
| **Why outside the 4 tracks** | This is the weakest point — receivables financing sits uncomfortably close to "receivables chasing," which you explicitly excluded, even though the mechanism (getting *paid early by a financier*, not chasing a debtor) is technically different. |
| **Saturation** | 🟢 Uncommon as a hackathon idea, but real fintech players (KredX, Cashinvoice, Vayana) already operate adjacent to this space. |
| **Track-overlap risk** | 🟡–🔴 Borderline-to-high on Revenue Recovery, given the "receivables" framing risk. |

### Candidate C — SME Import/Export FX-Hedging Decision Support

| Field | Assessment |
|---|---|
| **Problem** | Indian importers hedge heavily while exporters remain reluctant/under-hedged, leaving a structural "hedging gap" that increases SME exposure to rupee volatility and, in aggregate, raises reliance on RBI intervention [marketscreener.com](https://www.marketscreener.com/news/yawning-gulf-in-importer-exporter-hedging-heightens-indian-rupee-s-reliance-on-rbi-ce7d5fdedd8af721). |
| **Who suffers** | SME importers/exporters without in-house treasury expertise. |
| **Existing solutions/competitors** | Dedicated SME FX platforms already exist — CorpHedge, xFlowPay [xflowpay.com/blog/forex-risk-management] — this space is being actively built out. |
| **Why current solutions insufficient** | Existing platforms provide hedging execution/access; fewer provide *decision support* (when/how much to hedge) tailored to an SME's specific cash-flow timing — but this gap is narrowing, not wide open. |
| **Why now** | Ongoing rupee volatility and RBI's evolving posture on market intervention, per late-2025/early-2026 coverage. |
| **3+ solution approaches** | (1) Cash-flow-timed hedge-ratio recommender. (2) Scenario simulator showing P&L impact of hedged vs. unhedged positions. (3) Auto-triggered forward-booking suggestions tied to invoice due dates. |
| **Where AI adds value** | Personalized hedge-ratio recommendation conditioned on a company's actual receivable/payable timing is a genuine forecasting/decision problem. |
| **Razorpay fit** | Weak-to-moderate — Razorpay has no current FX/treasury product; this would be a bigger strategic leap than Candidates A, B, or D. |
| **Demo feasibility** | Medium — needs believable synthetic cash-flow + FX-rate scenario data; harder to make the "aha" moment concrete in 5 minutes than a compliance-deadline story. |
| **Measurable impact** | ₹ P&L variance reduction from following recommended hedge ratio vs. no hedging, backtested on historical rates. |
| **Why outside the 4 tracks** | Genuinely outside all four — this is real strategic risk management, not bookkeeping, growth, recovery, or fraud. |
| **Saturation** | 🟠 Moderately common — several funded platforms already target this exact SME gap. |
| **Track-overlap risk** | 🟢 Low. |

### Candidate F — Ongoing UBO / Beneficial-Ownership Change Monitoring for Merchant Portfolios

| Field | Assessment |
|---|---|
| **Problem** | Regulated entities (banks, NBFCs, PAs) must maintain current Ultimate Beneficial Owner records for corporate customers under PMLA, but ownership structures change continuously (director changes, shareholding transfers) — most monitoring is periodic/reactive, not continuous [lexology.com](https://www.lexology.com/library/detail.aspx?g=7f996a69-f427-46a8-86de-973a2265a114), [authbridge.com](https://authbridge.com/blog/what-is-ultimate-beneficial-ownership-ubo-complete-guide/). |
| **Who suffers** | Compliance teams at banks/NBFCs/PAs (including Razorpay itself, as a regulated PA with corporate merchants). |
| **Existing solutions/competitors** | UBO verification vendors exist for point-in-time checks (NameScan, AuthBridge, SpringVerify) — but these are largely one-time/periodic checks, not continuous monitoring products, per the sourced material. |
| **Why current solutions insufficient** | Point-in-time UBO checks go stale the moment ownership changes; existing vendors don't appear to offer continuous drift-detection tied automatically to re-verification triggers. |
| **Why now** | Same regulatory environment driving Candidate B (PA-PG 2025 tightening) also raises the bar on ongoing beneficial-ownership diligence, not just one-time onboarding. |
| **3+ solution approaches** | (1) Continuous MCA/registry-change monitoring that flags drift and auto-triggers re-verification. (2) Risk-weighted re-verification prioritization (similar engine to Candidate B, different trigger). (3) UBO-network graph analysis to catch layered/complex ownership structures. |
| **Where AI adds value** | Change-detection and entity-resolution across registry filings is a genuine data/graph problem. |
| **Razorpay fit** | Direct, and complementary to Candidate B — same underlying compliance function, different trigger event (ownership change vs. time-based renewal). |
| **Demo feasibility** | Medium-low — requires modeling registry-change data, which is harder to synthesize convincingly than Candidate B's field-ops data. |
| **Measurable impact** | Reduction in average "staleness" of UBO records; number of drift events caught before a regulator would. |
| **Why outside the 4 tracks** | Outside all four, similar reasoning to B. |
| **Saturation** | 🟢 Uncommon. |
| **Track-overlap risk** | 🟡 Moderate — same Risk-Manager-adjacent "verifier" framing risk as B, arguably worse since "beneficial ownership" sounds more explicitly AML/fraud-flavored. |

---

## Judge-Perspective Stress Test — Top 5

**On Candidate B:** A judge's first instinct might be "isn't KYC just Risk Manager?" The rebuttal has to be immediate and precise: Risk Manager's stated scope is financial-loss prevention from *fraud, returns, and chargebacks* — transaction-level, adversarial-actor problems. Candidate B has no adversary; every merchant *wants* to be verified and stay live. The actual problem is a **workforce-capacity and prioritization problem under a fixed deadline** — an operations-research problem wearing a compliance hat, not a fraud-detection problem. A second likely question: "why hasn't RBI or an existing vendor solved this?" — answer: the deadline and the "PA's own employees only" constraint are both brand new (2025 Directions), so no vendor has had a full cycle to build for it. Strongest point in its favor: a judge can be told, truthfully, "Razorpay is almost certainly running this exact exercise internally right now" — that's about as close to "we could actually integrate this" as an Open Track pitch can get.

**On Candidate D:** Weaker than B on track-overlap — "flagging merchants who might be misclassified to game interchange" is uncomfortably close to fraud detection, and a skeptical judge would likely just call it Risk Manager. Kept as a runner-up, not a finalist.

**On Candidate E:** A judge who knows fintech will likely say "isn't this just receivables financing, i.e., Revenue Recovery adjacent?" Hard to fully rebut — the mechanism differs (getting paid early by a third-party financier vs. chasing a debtor) but the surface story ("MSME gets paid faster") sounds identical to what Revenue Recovery teams will pitch. Riskiest of the five on track fit.

**On Candidate C:** Genuinely safe on track-overlap, but a judge will reasonably ask "what stops CorpHedge or an existing FX platform from doing this?" — the honest answer is "not much, they're already moving this direction," which is a weaker uniqueness story than B's "this regulatory cycle is 11 days old."

**On Candidate F:** Compelling as a compliance-ops story alongside B, but harder to demo convincingly (registry-change data is not as intuitively demoable as a field-agent dispatch map), and carries similar Risk-Manager-adjacency risk to D.

---

## Top 5 vs. Candidate A — Head-to-Head

| Axis | A: MSME 45-day payment | B: Merchant re-KYC crisis | D: MCC integrity | E: TReDS fragmentation | C: FX hedging | F: UBO monitoring |
|---|---|---|---|---|---|---|
| Real, evidenced pain | Strong (tax law + Atradius data) | Strong (breaking news, today) | Strong (RBI probe, ₹5,000cr/mo) | Moderate | Moderate-strong | Moderate |
| Urgency / "why now" | High (Sep 30 audit deadline) | **Highest (Sep 15 deadline, 11 days)** | Moderate | Moderate | Moderate | Moderate |
| Saturation | 💎 Highly differentiated | 💎 Highly differentiated | 🟢 Uncommon | 🟢 Uncommon | 🟠 Moderately common | 🟢 Uncommon |
| Track-overlap risk | Finance Controller (moderate, rebuttable) | Risk Manager (moderate, rebuttable) | Risk Manager (high) | Revenue Recovery (high) | Low | Risk Manager (moderate) |
| Razorpay integration story | Feeds RazorpayX Payouts (customer-facing) | **Razorpay's own live regulatory obligation** (internal + partner-facing) | Razorpay's own regulatory exposure | Weak — new adjacency | Weak — no current product | Razorpay's own regulatory exposure |
| Demo feasibility | High | High | Medium | Medium | Medium | Medium-low |
| Multiple genuinely different solution paths | Yes (classification + allocation + form-gen) | Yes (triage/dispatch + document copilot + path-classifier + forecaster) | Somewhat | Yes | Yes | Somewhat |
| "Wow, why doesn't this exist" factor | Strong | **Strongest — because the crisis is 11 days old, "why doesn't it exist" answers itself** | Moderate | Moderate | Weak (it's being built already) | Moderate |

**B edges out A** on two dimensions that matter most for an Open Track pitch aimed at a Razorpay judge: (1) urgency — B's deadline is closer and is literally in the news today, and (2) integration credibility — B is not just "a product Razorpay could sell," it's arguably **a problem Razorpay is personally living through right now**, which is the single strongest version of "we could actually integrate this" a pitch can offer.

---

## Final Selection

### 🏆 Winner of this round: Candidate B — Merchant Re-KYC Completion & Field-Verification Triage for Payment Aggregators

Scored against your 10 criteria:

- **Real pain:** Confirmed by breaking news dated today, naming Paytm, PhonePe, and Google Pay as struggling, under an RBI framework that applies to all authorized PAs [freepressjournal.in](https://www.freepressjournal.in/business/payment-aggregators-seek-rbi-extension-for-merchant-re-kyc-deadline).
- **Uniqueness:** The regulatory cycle itself is under a year old — no existing vendor has had a full cycle to build a dedicated solution. Verified by the absence of any purpose-built tool in search results, only generic Video-KYC and generic route-optimization products.
- **WOW/solution potential:** "You have 11 days, here's the optimized plan that gets you to 95% instead of 80%" is a genuinely dramatic, numbers-driven live demo.
- **Clear solution approach:** Yes — triage-and-dispatch is a well-defined optimization problem with a clean synthetic-data MVP path.
- **Meaningful AI:** Constrained optimization (not a chatbot), document/vision classification, and policy-eligibility reasoning — three distinct, real AI tasks.
- **Multiple solution paths:** Four genuinely different approaches identified (dispatch optimizer, document copilot, compliant-path classifier, backlog forecaster) — a team could pick any combination.
- **Razorpay strategic value:** The strongest of any candidate assessed across both rounds — this is Razorpay's own probable live operational problem, not just an ecosystem-adjacent one.
- **Technical feasibility:** High — buildable and demoable on synthetic data in a hackathon window.
- **Measurable ROI:** Directly quantifiable — completion-rate lift, revisit-rate reduction, merchants (and transaction volume) protected from suspension.
- **Open Track fit:** Confirmed outside Growth, Revenue Recovery, and Finance Controller; the one real risk (Risk Manager adjacency) has a clear, honest rebuttal that should be stated explicitly and early in the pitch, exactly as recommended for Candidate A's Finance Controller risk.

**Recommendation:** Candidate B is the stronger Open Track pitch of the two rounds, primarily because of how current and self-referential the pain is — a Razorpay judge is more likely to have personally heard about this internally than about Section 43B(h). Candidate A remains a strong, well-evidenced second option; if presenting both, note that B's story is more dramatic and time-boxed, while A's is more durable (it recurs every year, whereas B's acute version resolves once this KYC cycle completes, though the underlying periodic-KYC problem — as shown by the years of prior bank-account-freeze episodes — is structurally recurring for regulated entities generally, so the *product*, even if this specific crisis passes, has a lasting home).

---

## Sources & Evidence

- [Payment aggregators seek RBI extension, Sep 15 2026 deadline — BusinessToday (published 2026-09-04)](https://www.businesstoday.in/latest/corporate/story/payment-aggregators-seek-more-time-from-rbi-to-complete-merchant-re-kyc-report-553334-2026-09-04)
- [Payment aggregators seek RBI extension — Free Press Journal](https://www.freepressjournal.in/business/payment-aggregators-seek-rbi-extension-for-merchant-re-kyc-deadline)
- [RBI Rewrites the Payment Aggregator Rulebook — Ikigai Law](https://www.ikigailaw.com/article/639/rbi-rewrites-the-payment-aggregator-rulebook)
- [RBI's Updated Guidelines for Payment Aggregators 2025 — AuthBridge](https://authbridge.com/blog/rbi-payment-aggregator-master-direction-2025/)
- [RBI lens on payment fintechs over misclassified merchants — Business Standard](https://www.business-standard.com/amp/finance/news/rbi-lens-on-payments-fintechs-over-misclassified-merchants-125052901817_1.html)
- [RBI asks banks to enable seamless KYC updation — Moneylife](https://www.moneylife.in/article/rbi-asks-banks-to-enable-seamless-kyc-updation-urgently-bring-down-number-of-inoperative-or-frozen-accounts/75768.html)
- [Yawning gulf in importer-exporter FX hedging — MarketScreener](https://www.marketscreener.com/news/yawning-gulf-in-importer-exporter-hedging-heightens-indian-rupee-s-reliance-on-rbi-ce7d5fdedd8af721)
- [Forex risk management for SMBs — xFlowPay](https://www.xflowpay.com/blog/forex-risk-management)
- [TReDS platforms compared — Karbon Card](https://www.karboncard.com/blog/treds-platforms-in-india-compared-rxil-m1xchange)
- [TReDS RBI directive on easing invoice discounting — M1xchange](https://www.m1xchange.com/treds-platform-operators-welcome-rbis-directive-to-ease-msme-invoice-discounting-boost-liquidity/)
- [UBO compliance guide — AuthBridge](https://authbridge.com/blog/what-is-ultimate-beneficial-ownership-ubo-complete-guide/)
- [Beneficial ownership disclosure compliance challenges — Lexology](https://www.lexology.com/library/detail.aspx?g=7f996a69-f427-46a8-86de-973a2265a114)
- [GST notice automation — Open Money](https://open.money/blog/automating-gst-notice-tracking-and-response-management/)
- [E-invoice threshold reduced to ₹1 crore, April 2025 — Gimbooks](https://www.gimbooks.com/blog/e-invoice-applicability-limit-in-2025-latest-rules-threshold-who-must-comply/)
- [Escrow-as-a-service — SprintEscrow / Paysprint](https://www.paysprint.in/excrow.html)
