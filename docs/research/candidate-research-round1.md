# Razorpay AI Buildathon 2026 — Open Track Problem Research

**Method note:** This document follows your 9-step process exactly. Where a claim is backed by a source, it's cited inline. Where I reasoned from general knowledge without independent verification, it's flagged **(assumption)**. To keep 18 problems readable, Step 2 validation is compressed into 6 fields per problem instead of 10 restated questions — the 10 questions are still answered, just merged where they overlap (e.g. "how does it happen / how often" collapse into one line).

---

## STEP 1 & 2 — The Problem Landscape (18 candidates, with validation)

### 1. Statutory 45-day MSME payment deadline compliance (Section 43B(h) / new Section 37(2)(g))
- **Who:** Any company (not just large ones) that buys goods/services on credit from Udyam-registered micro or small suppliers — manufacturers, retailers, IT/ITES buyers, e-commerce platforms sourcing from small vendors.
- **What happens today / pain:** Since FY2024-25, if a company pays a micro/small vendor later than 15 days (or 45 days under a written contract), that entire expense becomes non-deductible for that year under Section 43B(h) — recently renumbered to **Section 37(2)(g) of the Income-tax Act, 2025**, with the rule carried over unchanged [taxupdate.in](https://taxupdate.in/income-tax/771/cbdt-faq-deep-dive-7-section-43b-43bh-msme-section-37-income-tax-act-2025-actual-payment-tax-audit/). Unlike other Section 37 timing rules, there is **no relief** even if you pay before the tax return is filed — miss the 45-day window and the deduction is gone for that year, permanently increasing that year's tax liability. On top of that, MSMED Act Section 16 imposes compound interest at **3x the RBI bank rate** on the late amount, and companies must separately disclose overdue MSME dues in Form 3CD / MSME Form-1 (para 22 disclosures).
- **Frequency / impact:** Every invoice cycle, for every micro/small vendor — not a one-off event. [Atradius's 2025 India B2B report](https://atradius.in/knowledge-and-research/reports/b2b-payment-practices-trends-india-2026) finds **63% of credit-based B2B sales are currently overdue** in India, and retail/textile industry bodies have publicly said the 90–120 day credit cycles they run on make the 45-day rule "highly unrealistic" [business-standard.com](https://www.business-standard.com/finance/personal-finance/45-day-msme-payment-rule-impact-and-details-of-section-43b-h-explained-124032600333_1.html).
- **Current workaround / why inadequate:** Companies use ERPs (Tally, SAP, Zoho) or manual trackers/interest calculators [thegstcalculator.in tracker](https://thegstcalculator.in/tools/msme-payment-tracker) to flag overdue invoices *after the fact*. Even open-source ERP tooling doesn't fully handle it — a live GitHub issue on the popular `india-compliance` app for Frappe/ERPNext explicitly lists **"no automated flagging of MSME payment timelines" and "no MSME Form-1 export"** as missing features [github.com/resilient-tech/india-compliance#3086](https://github.com/resilient-tech/india-compliance/issues/3086). None of these tools decide *which* vendor to pay *when* the company doesn't have cash to pay everyone on time, or *initiate* the payment.
- **Why it's growing / why now / unsolved:** It's not growing so much as it is acutely *timed* — the transition to the Income-tax Act 2025 keeps the rule unchanged, and the **first tax audit deadline under the harshest reading of the rule is 30 September 2026** [taxupdate.in], which is roughly three weeks from today. It hasn't been solved because it's a niche intersection of tax law, vendor master data (who counts as "MSME"), and treasury execution — accounting vendors treat it as a reporting checkbox, not a cash-allocation decision problem.

### 2. Vendor/business identity verification for B2B onboarding (fake or shell suppliers)
- **Who:** Procurement teams at mid-large enterprises, B2B marketplaces (IndiaMART-style), platforms onboarding new sellers/vendors.
- **What happens / pain:** Fraudulent or shell vendors get onboarded using forged GST/incorporation documents, leading to duplicate-payment fraud, ghost vendors, or export scams. A documented case: fraudsters used **fake ISO certification and buyer credentials to swindle IndiaMART exporters** [the420.in](https://the420.in/delhi-dwarka-cyber-fraud-call-centre-b2b-export-scam/).
- **Current solutions:** Vendor background-verification vendors already exist and are fairly mature — AuthBridge [authbridge.com](https://authbridge.com/solutions/vendor-background-verification/), Veridion [veridion.com](https://veridion.com/insights/articles/how-to-identify-vendor-fraud), OnGrid [ongrid.in](https://ongrid.in/blogs/vendor-fraud-the-silent-risk-that-can-cripple-your-business/). This makes it a real problem but a **crowded one** — not underserved.
- **Verdict:** Real, but not underserved — deprioritized.

### 3. Marketplace seller GST/compliance-status churn silently blocking payouts and buyer ITC
- **Who:** Marketplace operators (Amazon/Flipkart/Meesho-style) and the buyers who purchase from third-party sellers.
- **What happens:** A seller's GST registration can be cancelled or suspended mid-relationship; marketplaces must handle TCS/GST obligations correctly per seller status, and buyers risk losing Input Tax Credit if a seller's compliance status changes after the sale [cleartax.in](https://cleartax.in/s/impact-of-gst-on-e-commerce-marketplace-sellers), [taxbuddy.com](https://www.taxbuddy.com/blog/gst-filing-ecommerce-sellers-taxbuddy).
- **Current solutions:** GST-filing/compliance SaaS (ClearTax, TaxBuddy, LegalWiz) monitor filing status, but as periodic reporting tools, not real-time payout gating.
- **Verdict:** Real and touches Open Track territory, but heavily overlaps "reconciliation" and "tax-line matching," both explicitly excluded by you.

### 4. RBI Payment Aggregator (PA-PG) 2025 nodal/escrow account compliance for platforms
- **Who:** Marketplaces, platforms, and payment aggregators running nodal/escrow accounts for split settlements.
- **What happens:** RBI's 2025 Master Directions for Payment Aggregators tightened rules on nodal account fund flows, settlement timelines, and prohibited commingling [mondaq.com](https://www.mondaq.com/india/financial-services/1706010/rbi-master-direction-2025-compliance-mandate-for-payment-aggregators-and-pa-p-deadline), [authbridge.com](https://authbridge.com/blog/rbi-payment-aggregator-master-direction-2025/). Non-compliant fund flows can trigger RBI action against the platform itself.
- **Current solutions:** Nodal/escrow reconciliation vendors already exist (Terra Insight, Castler) [terra-insight.com](https://www.terra-insight.com/insights/nodal-escrow-reconciliation-india/).
- **Verdict:** Real, but this is deep payments-infrastructure plumbing — hard to demo convincingly in a hackathon MVP, and adjacent to "reconciliation" (excluded).

### 5. Cross-border contractor/vendor payment compliance for remote-first Indian & global companies
- **Who:** Indian companies hiring international contractors, and global companies paying Indian freelancers/vendors — a fast-growing category given remote hiring.
- **What happens:** Every outward/inward remittance needs FEMA purpose-code classification, TCS-on-LRS calculation (for outward personal remittances), and Form 15CA/CB filing for larger payments; errors cause payment holds at the bank or tax notices later [tallysolutions.com](https://tallysolutions.com/business-guides/fema-compliance-for-businesses-foreign-exchange-regulations-how-to-stay-compliant-in-india/), [skydo.com](https://www.skydo.com/blog/pay-remote-workers-india).
- **Current solutions:** Cross-border payout platforms (Skydo, Wise, Deel-style) already build compliance into checkout flows — this space is maturing fast.
- **Verdict:** Real and growing, but increasingly well-served by dedicated cross-border payout startups — moderately saturated.

### 6. Buyer credit-risk transparency for MSME suppliers extending trade credit
- **Who:** Small suppliers deciding whether to extend credit terms to a large buyer.
- **What happens:** Suppliers have no visibility into a buyer's payment behavior before extending credit, leading to bad debt (Atradius: **7% of B2B invoices become bad debt on average**, worse in textiles at ~10% [atradius.in]).
- **Current solutions:** **Recordent's "KnowYourBusinessScore"** already does exactly this — a buyer credit-risk score combining GST compliance, legal checks, and B2B transaction history [smestreet.in](https://smestreet.in/finance-banking/knowyourbusinessscore-to-help-msmes-assess-buyer-credit-risk-12493875).
- **Verdict:** Real problem, but an existing funded player already owns this exact framing. Deprioritized.

### 7. Payment orchestration / PSP failover during outages
- **Who:** Any merchant relying on a single or few payment gateways.
- **What happens:** UPI and PSP outages are a documented recurring issue through 2025 [orfonline.org](https://www.orfonline.org/expert-speak/upi-at-scale-outages-and-the-push-for-resilient-systems), [insightsonindia.com](https://www.insightsonindia.com/2025/04/18/upsc-editorial-analysis-indias-upi-outages-and-the-future-of-digital-payment-infrastructure/).
- **Current solutions:** This is heavily served already — by orchestration vendors (GR4VY [gr4vy.com], Orchestra Solutions [orchestrasolutions.com], Spark [spark.money]) and **Razorpay itself publishes guidance on this** [razorpay.com/blog/payment-gateway-downtime-and-failover-in-2026-india-guide]. 
- **Verdict:** Real but saturated and already a Razorpay-owned narrative. Deprioritized.

### 8. Duplicate/fraudulent invoice detection in enterprise accounts payable
- **Who:** Enterprise finance/procurement teams.
- **What happens:** Duplicate vendor invoices, altered bank details, and P2P fraud cause real losses [open.money](https://open.money/blog/prevent-duplicate-invoice-fraud-ap/), [lseg.com](https://www.lseg.com/en/risk-intelligence/glossary/payment-fraud/accounts-payable-fraud).
- **Current solutions:** Globally saturated (Ramp, Precoro, IntelliChief, Tipalti all sell this) [ramp.com](https://ramp.com/blog/accounts-payable/how-to-prevent-duplicate-payments), [precoro.com](https://precoro.com/blog/what-are-duplicate-invoices/).
- **Verdict:** Deprioritized — crowded and also arguably "AI Finance Controller" territory.

### 9. UPI/payment-infra resilience observability for merchants
- **Who:** Merchants and payment platforms.
- **Verdict:** Real (per above sources) but this is an SRE/infra-reliability problem more than a product a student team can meaningfully demo with "measurable value" in 5 minutes. Deprioritized.

### 10. Multi-entity treasury cash pooling / inter-company settlement for group companies
- **Who:** Corporate groups with multiple legal entities.
- **Verdict:** Real **(assumption based on general treasury-management knowledge, not independently verified with current sources)**, but structurally overlaps "Run the books and the cash position" — literally Razorpay's own description of AI Finance Controller. Rejected on overlap grounds regardless of novelty.

### 11. Working-capital allocation across marketplace sub-merchant accounts (embedded finance)
- **Verdict:** Interesting but drifts into "AI Growth & Agentic Commerce" (merchant monetization) territory. Rejected on overlap grounds.

### 12. Employee/vendor T&E and corporate-card policy compliance
- **Verdict:** Real **(assumption — not independently verified for this research)** but this category (Ramp, Zaggle, Enkash, Happay) is one of the most heavily funded and saturated fintech categories in India. Rejected.

### 13. Warranty/AMC/service-contract payment lifecycle tracking
- **Verdict:** Plausible niche pain **(assumption)**, but I could not find independent evidence this is a widespread, acute problem — doesn't meet your "not theoretical" bar strongly enough. Rejected for weak evidence.

### 14. E-invoicing (GST IRN) mandate compliance and downstream ITC risk from vendor non-compliance
- **Verdict:** Real, but structurally is a reconciliation/tax-matching problem — directly excluded by you.

### 15. Digital lending co-lending settlement between banks and NBFCs
- **Verdict:** Real **(assumption — general fintech knowledge)** but this is deep bank-NBFC infrastructure requiring institutional data access no student team can obtain for an MVP. Rejected as unbuildable.

### 16. Marketplace COD/reverse-logistics-triggered payment holds and return fraud
- **Verdict:** Real, well documented in e-commerce operations, but squarely reads as "AI Risk Manager" territory (fraud/returns — explicitly named in Razorpay's own Track 2 description: *"fraud, returns and chargebacks"*). Rejected — direct overlap.

### 17. Beneficiary/payee name-mismatch failures in high-value B2B bank transfers (misdirected payouts)
- **Verdict:** Real operational pain **(assumption — not independently verified this cycle)**, but reads as "payment failure recovery," explicitly excluded by you.

### 18. Procurement contract payment-terms drift (PO/contract terms vs. what AP actually pays)
- **Verdict:** This is really a sub-mechanism of #1 (MSME 45-day compliance) rather than a separate problem — folded into #1's solution design rather than treated standalone.

---

## STEP 3 — Elimination Table vs. Razorpay's Four Tracks

| # | Problem | Classification | Why |
|---|---|---|---|
| 1 | MSME 45-day payment deadline compliance & treasury prioritization | 🟢 Clearly Open Track | It's a statutory-deadline compliance + cash-allocation *decision and execution* problem on the **payables** side, triggered by tax law, not by internal bookkeeping accuracy or forecasting. |
| 2 | Vendor identity verification | 🟡 Borderline | Reads close to Risk Manager (verification-as-fraud-prevention) |
| 3 | Seller GST-status payout gating | 🔴 Too similar | Overlaps excluded "reconciliation" / "tax-line matching" |
| 4 | PA-PG nodal/escrow compliance | 🔴 Too similar | Overlaps excluded "reconciliation"; also payments-infra plumbing, not a demoable AI product |
| 5 | Cross-border contractor payment compliance | 🟡 Borderline | Could be read as Finance Controller ("run the books") for the compliance-filing part |
| 6 | Buyer credit-risk score for suppliers | 🔴 Too similar | Directly overlaps AI Risk Manager (credit/counterparty risk scoring) |
| 7 | PSP failover orchestration | 🔴 Too similar | Overlaps payment-failure recovery (explicitly excluded) and is a Razorpay-owned narrative already |
| 8 | Duplicate invoice fraud detection | 🔴 Too similar | Explicitly fraud detection (excluded) and Finance Controller |
| 9 | UPI infra resilience | 🔴 Too similar | Infra reliability, not a product; also close to Risk Manager |
| 10 | Multi-entity treasury pooling | 🔴 Too similar | Literally "run cash position" — Razorpay's own Finance Controller wording |
| 11 | Sub-merchant working capital allocation | 🔴 Too similar | Overlaps Growth & Agentic Commerce |
| 12 | T&E/corporate card compliance | 🔴 Too similar | Finance Controller territory, also saturated market |
| 13 | Warranty/AMC payment lifecycle | 🟡 Borderline | Weak evidence, unclear track overlap |
| 14 | E-invoicing/ITC compliance | 🔴 Too similar | Reconciliation/tax-matching (excluded) |
| 15 | Co-lending settlement | 🔴 Too similar | Reconciliation + unbuildable MVP |
| 16 | COD/return-fraud holds | 🔴 Too similar | Explicitly "fraud, returns and chargebacks" — Razorpay's own Risk Manager wording |
| 17 | Beneficiary mismatch/misdirected payouts | 🔴 Too similar | Payment-failure recovery (excluded) |
| 18 | Contract-terms drift | — | Folded into #1 |

**Survivors for Step 4:** #1 (MSME 45-day compliance), #2 (vendor identity verification), #5 (cross-border contractor compliance).

---

## STEP 4 — Competition Saturation Test

| Problem | Saturation | Reasoning |
|---|---|---|
| #1 MSME 45-day payment compliance & prioritization | 💎 Highly differentiated | Requires knowing a fairly obscure intersection of Income-tax Act mechanics, MSMED Act interest rules, and Udyam vendor classification. Search turned up **zero** hackathon projects on this exact angle, and even purpose-built ERP add-ons (the `india-compliance` GitHub issue) haven't shipped the automated-flagging feature yet. Most students default to consumer-facing or generic "AI agent" ideas — very few will spontaneously think "statutory tax-disallowance deadline as a treasury-scheduling problem." |
| #2 Vendor identity verification | 🟠 Moderately common | "Verify this business is real" is an intuitive, well-known KYB pattern; several teams will likely propose some version of it, and real vendors (AuthBridge, Veridion) already own the space. |
| #5 Cross-border contractor payment compliance | 🟠 Moderately common | FEMA/TCS compliance is a known pain point discussed openly in startup circles (Skydo, Wise are visible players), so it's a more "findable" idea via a quick search, and several fintech-savvy teams may converge on it. |

**#1 is the clear winner on the "would 1,000 technically capable students independently think of this" test** — it requires reading tax/compliance material most engineering students never touch, not just a Google search of "fintech pain points."

---

## STEP 5 — Razorpay Strategic Fit

**Why Razorpay should care about #1:** Razorpay already operates **RazorpayX**, its business-banking suite, with a dedicated **Payouts API** for instant bulk vendor payments [razorpay.com/x/payouts/] and general RazorpayX business banking [razorpay.com/x/]. A tool that tells a business *which vendors must be paid, by when, to avoid a tax hit* is a natural feeder into "so pay them now" — i.e., it's a demand-generation layer sitting directly on top of a product Razorpay already sells. This is not a hypothetical integration; Payouts is a live, documented API surface.

- **Which Razorpay capability fits:** RazorpayX Payouts API (bulk/instant vendor disbursal), potentially RazorpayX bank account statements/balance APIs (to know available cash for prioritization), and optionally a lightweight ledger tag for MSME-flagged vendors.
- **How it strengthens Razorpay's business:** Every payment this tool schedules to "beat the deadline" is a payout that can be routed through RazorpayX — a natural top-of-funnel for a banking product Razorpay is actively growing, aimed at exactly the SME/mid-market segment RazorpayX targets.
- **Customer type:** Finance/AP teams at mid-size and large enterprises (anyone buying from small vendors on credit) — precisely the segment that would also be a RazorpayX prospect.
- **Could it become a real product:** Plausibly — a "Compliant Payables" or "MSME Payment Shield" feature bolted onto RazorpayX is a coherent product extension, not a stretch.
- **Strategic advantage:** Positions Razorpay as solving a *statutory, dated, unavoidable* pain (a September 30 tax-audit cliff every year) rather than a "nice to have" — this kind of forced-urgency compliance hook is a strong, recurring acquisition motion for a payments/banking platform.

---

## STEP 6 — Top 5 Strongest Problems (A–N)

### 🥇 #1 — MSME 45-Day Statutory Payment Compliance & Cash-Constrained Payment Prioritization

**A. Problem statement:** Companies that buy from Udyam-registered micro/small vendors on credit must pay them within 15–45 days or permanently lose the tax deduction on that expense (Section 37(2)(g), formerly 43B(h)) — but finance teams currently have no system that knows, across hundreds of open vendor invoices and a constrained cash position, *which specific payments must be prioritized this week* to avoid disallowance, and no way to *act* on that knowledge by initiating the payment itself.

**B. Who suffers:** AP/finance controllers and CFOs at any company sourcing from small vendors — manufacturing, retail, textiles, IT services, e-commerce.

**C. Why it matters now:** The FY2025-26 tax audit deadline (30 September 2026) is the first cycle under the renamed Income-tax Act 2025 provision, with **no relief window** — this is the single biggest Form 3CD exposure item this audit season per tax practitioners [taxupdate.in].

**D. Current workaround:** Spreadsheets, ERP due-date reports, or standalone interest calculators that tell you *after the fact* that you're late [thegstcalculator.in]; none decide *whom to pay first* when cash is short, or execute the payment.

**E. Why current solutions fail:** They are retrospective reporting tools, not forward-looking, cash-aware, decision-and-execution systems. The `india-compliance` GitHub issue shows this gap is acknowledged but unbuilt even in dedicated compliance tooling [github.com].

**F. Why it's underserved:** It sits at the unglamorous intersection of tax law + treasury ops + vendor master data — not a space AI hackathon teams naturally wander into, and not a space consumer-fintech-focused startups have prioritized.

**G. Razorpay relevance:** Directly feeds RazorpayX Payouts [razorpay.com/x/payouts/] — this tool's output (a prioritized payment run) is literally an API call away from being executed on Razorpay's own rails.

**H. AI opportunity:** (1) Classify vendors as MSME/non-MSME and extract the correct payment-window (15 vs. 45 days) from contract text using an LLM reading the vendor agreement; (2) given a cash-position snapshot, solve a prioritization/allocation problem (which subset of due invoices to pay now, ranked by tax-and-interest exposure per rupee of cash used) — a real optimization problem, not just a chatbot; (3) auto-draft the MSME Form-1/Form 3CD disclosure schedule.

**I. Potential product:** An AP compliance co-pilot that ingests vendor master + invoice data, tags MSME exposure, models the cost of delay (lost deduction + Section 16 interest) per invoice, recommends a ranked payment run under a cash constraint, and can trigger the payout via RazorpayX API.

**J. MVP difficulty:** Medium — needs synthetic/sample vendor and invoice data, a classification step, a constrained-optimization or ranking model, and a payout-API demo call (can use RazorpayX sandbox). Buildable in a hackathon timeframe by a competent team.

**K. Business value:** Directly quantifiable in ₹ saved — tax deduction preserved (effective corporate tax rate) plus MSMED Act interest avoided, per invoice, per company, per audit cycle — a genuinely measurable number for the demo.

**L. Saturation:** 💎 Highly differentiated (see Step 4).

**M. Hard to copy because:** It requires correctly modeling two overlapping legal regimes (Income-tax Act disallowance mechanics + MSMED Act interest mechanics) *and* pairing that with a cash-constrained execution decision — most teams that stumble onto "MSME late payment" will build a simple deadline tracker, not a prioritization-and-execution engine.

**N. Why judges remember it:** It's the rare idea grounded in a real regulatory deadline that is *literally happening this month* — an easy, credible story to tell in 5 minutes ("your tax audit is in 26 days, here's ₹X you're about to lose"), backed by citable law rather than a hypothetical trend.

---

### 🥈 #2 — Vendor/Business Identity Verification for B2B Onboarding
A. Real fraud losses from fake suppliers/shell vendors during onboarding. B. Procurement & marketplace onboarding teams. C. Growing with digital B2B trade volume. D. Manual document checks or paid KYB vendors. E. Existing KYB vendors are point-in-time checks, not continuous monitoring. F. Somewhat served already (AuthBridge, Veridion). G. Could tie into Razorpay's own merchant KYC stack. H. Continuous risk-scoring using public registry signals. I. A vendor "trust monitoring" layer. J. Medium MVP difficulty. K. Moderate, hard to quantify uniquely. L. 🟠 Moderately common — several existing well-funded players. M. Hard to differentiate technically from incumbents. N. Judges likely to say "isn't this AuthBridge?" — **weaker than #1**.

### 🥉 #5 — Cross-Border Contractor/Vendor Payment Compliance
A. FEMA/TCS/Form 15CA-CB complexity for every cross-border payment. B. Remote-first companies, freelancer-hiring platforms. C. Growing with remote hiring. D. Manual CA-assisted filing or dedicated cross-border payout platforms. E. Existing platforms (Skydo, Wise) already automate much of this. F. Moderately served, not fully underserved. G. Ties to Razorpay's payments infra if it ever expands cross-border payout rails. H. Auto-classification of purpose codes + auto-drafting 15CA/CB. I. A compliance layer on cross-border payouts. J. Medium-high MVP difficulty (regulatory nuance is easy to get subtly wrong). K. Meaningful but hard to demo safely without real regulatory review. L. 🟠 Moderately common — a "findable" idea for fintech-savvy teams. M. Not very defensible technically. N. Solid but not standout.

*(Given the strength of the elimination and saturation results, #1 is materially stronger than #2 and #5 on every axis that matters to you — buildability, differentiation, and Razorpay fit — so the remaining two "top 5" slots are not filled with weaker forced ideas; #2 and #5 are documented above as the honest runners-up rather than padded out to make five.)*

---

## STEP 7 — Precise Problem Statement (Before Any Feature List)

> **Finance teams that buy goods or services on credit from micro and small enterprises cannot currently tell, on any given day, which of their outstanding vendor invoices are approaching the statutory payment deadline that determines whether that expense remains tax-deductible — and even when they can see the deadline, they have no system that turns limited available cash into a defensible, prioritized payment run before the window closes.**

That's the problem. Nothing about dashboards, agents, or chat interfaces yet — just the gap between "the deadline exists" and "the right payment gets made in time."

---

## STEP 8 — Challenging the Winner

- **Is this actually unique?** No single element is unique — MSME payment tracking and treasury tools both exist separately. The combination (statutory-deadline-aware + cash-constrained prioritization + direct payout execution) is what's unclaimed.
- **Could it secretly be AI Risk Manager?** No — Risk Manager is about *loss from fraud, returns, chargebacks*. This is about *loss from a tax-law technicality on legitimate, real payments*. Different loss mechanism entirely.
- **Could it be AI Revenue Recovery?** No — Revenue Recovery is about money coming *in* (receivables, failed payments, abandoned checkout). This is entirely about money going *out* to vendors.
- **Could it be AI Finance Controller?** This is the honest risk. Finance Controller is "run the books and cash position... reporting match rates and unresolved exceptions" — i.e., **reconciliation-flavored bookkeeping**. This idea doesn't reconcile records against each other or produce match-rate metrics; it makes a forward-looking, legally-constrained *payment decision* under a cash constraint and *executes* it. The distinction should be stated explicitly and early in the pitch, not left for judges to untangle themselves.
- **Could it be Agentic Commerce?** No — that track is about growing merchant revenue and AI-buyer transactability, unrelated to vendor payables.
- **Is it just a chatbot?** No — the core is a classification + constrained-ranking/allocation engine over invoice and cash data, with an LLM used narrowly (reading contract text to extract payment terms), not as the whole product.
- **Is it just an LLM wrapper?** No, for the same reason — the prioritization logic is a genuine algorithmic problem (rank invoices by "tax-and-interest cost of delay per rupee of cash"), not a prompt.
- **Would a typical hackathon team build this?** Unlikely without first reading tax-compliance material most engineering students never encounter — validated by the saturation search finding zero existing hackathon projects on this exact framing.
- **Is there already a major startup solving exactly this?** No dedicated startup was found solving "MSME deadline-aware, cash-constrained AP prioritization + execution" — adjacent point tools exist (trackers, ERPs) but not this combination.
- **Does Razorpay genuinely have a reason to build it?** Yes — it sits directly on top of RazorpayX Payouts, a live product.
- **Can a student team build a convincing MVP?** Yes — synthetic vendor/invoice data, a rules+LLM classification step, a ranking/allocation model, and a RazorpayX sandbox payout call are all realistic in a hackathon window.
- **Can measurable value be shown in 5 minutes?** Yes — "₹X in tax deduction and interest penalty avoided this run" is a concrete, believable number to show live.
- **Would a Razorpay product person think it's worth investigating?** Plausibly yes, precisely because it's an unglamorous, real, dated compliance pain next to a product they already sell.

**Verdict: survives the stress test, with one required mitigation** — the pitch must open by explicitly distinguishing itself from Finance Controller ("we don't reconcile books, we make and execute a legally-constrained payment decision"), rather than letting a judge draw the wrong parallel first.

---

## STEP 9 — Final Output

# 🏆 Winning Open Track Problem

### 1. Problem title
**The MSME Payment Clock** — statutory payment-deadline compliance and cash-constrained vendor payment prioritization.

### 2. One-line problem statement
Companies buying from small vendors on credit have no system that turns a hard tax-law payment deadline and a limited cash position into the right prioritized, executed payment run before the deduction is lost.

### 3. Detailed real-world problem
Under Section 37(2)(g) of the Income-tax Act, 2025 (formerly 43B(h)), any payment to a Udyam-registered micro or small enterprise made later than 15 days (or 45 under written contract) becomes non-deductible for that financial year, with no relief even if paid before the return is filed. MSMED Act Section 16 separately imposes compound interest at 3x the RBI bank rate on the overdue amount. Finance teams must therefore, continuously and correctly: (a) know which vendors are MSME-registered, (b) know the exact contractual payment window per invoice, (c) know how much cash is available right now, and (d) decide which subset of due invoices to pay immediately when cash is tight — then actually execute those payments. No tool currently connects all four steps; existing tools stop at "here's a report of what's overdue."

### 4. Who experiences it
AP/finance controllers, CFOs, and treasury teams at any company — manufacturer, retailer, IT services firm, or e-commerce platform — that sources goods or services on credit from small vendors. Atradius data shows 63% of Indian B2B credit sales are currently overdue, meaning the underlying vendor-payment-delay behavior this rule targets is already widespread [atradius.in].

### 5. Why current solutions are insufficient
ERP due-date reports and standalone interest calculators are backward-looking and passive — they tell you after the fact that you breached the window. None model the *forward* decision ("given ₹X available today and 40 overdue invoices, which do I pay to minimize tax-and-interest exposure?") or connect to a payment rail to act on it. Even purpose-built compliance tooling for this exact rule has open, unbuilt feature requests for basic deadline flagging [github.com/resilient-tech/india-compliance/issues/3086].

### 6. Why this problem is emerging/growing NOW
The rule's substance is unchanged but its legal home just moved to the new Income-tax Act 2025, and the first tax audit deadline under this framing — 30 September 2026 — is weeks away from today, making this the "single biggest Form 3CD exposure" item practitioners are actively flagging right now [taxupdate.in].

### 7. Why existing Razorpay tracks do NOT cover it
Not Growth/Agentic Commerce (no merchant revenue or AI-buyer angle). Not Risk Manager (loss source is a tax-law technicality, not fraud/returns/chargebacks). Not Revenue Recovery (concerns payables, not receivables or checkout). Not Finance Controller in the sense Razorpay defines it — "run the books... reporting match rates and unresolved exceptions" describes reconciliation/bookkeeping; this problem is a forward-looking, legally-constrained payment decision and execution problem, not a books-matching one.

### 8. Why Razorpay should care
It sits directly on RazorpayX's existing Payouts API — a live product for instant bulk vendor disbursal [razorpay.com/x/payouts/] — making this a natural, statutory-urgency-driven demand generator for a product Razorpay already sells, aimed exactly at RazorpayX's target segment (SME/mid-market businesses with vendor payment operations).

### 9. AI's exact role
An LLM reads vendor agreements/POs to extract payment-term text and classify MSME exposure (a genuine unstructured-data extraction task); a ranking/allocation model scores each overdue or soon-due invoice by "tax-plus-interest cost of delay per rupee of cash consumed" and proposes a payment run under a cash constraint — a real constrained-decision problem, not a chat interface bolted onto a database.

### 10. High-level solution direction
Ingest vendor master + invoice/PO data → classify MSME status and extract payment windows → ingest a live cash-position figure → rank and select a payment run that clears the highest-risk invoices first within the available cash → optionally trigger payouts through the RazorpayX Payouts API → generate the MSME Form-1/Form 3CD disclosure draft as a byproduct.

### 11. What the MVP would demonstrate
A sample company with dozens of vendor invoices, a limited cash figure, and a live run showing: which invoices are flagged MSME-critical, the ranked payment order, the ₹ amount of tax deduction and interest penalty avoided by following the recommendation versus a naive "pay oldest first" approach, and a simulated payout call.

### 12. Measurable success metric
₹ of tax deduction preserved + MSMED Act interest avoided per payment run, compared against a baseline (FIFO or ad hoc payment ordering) — directly quantifiable and demoable live.

### 13. Why it could become a real Razorpay product
It's a coherent, narrow extension of RazorpayX ("Compliant Payables" / "MSME Payment Shield") rather than a new business line — the payout execution mechanism already exists; this adds the decision layer on top.

### 14. Why it is difficult for other hackathon teams to copy
It requires correctly modeling two interacting legal regimes (Income-tax Act disallowance + MSMED Act interest) simultaneously with a cash-constrained decision engine — a combination not found in existing tooling and unlikely to be independently discovered by teams defaulting to more visible, Google-able fintech pain points.

### 15. Biggest technical risk
Correctly and robustly extracting payment-term clauses from varied, messy vendor contract/PO text (some may be informal or missing entirely) — misclassification here directly undermines the tool's core value proposition.

### 16. Biggest business risk
The regulatory landscape could shift again (further amendments, deferrals, or industry-lobbied relief for sectors like textiles/retail) — a well-known live tension given industry bodies are already pushing back on the rule [business-standard.com].

### 17. Biggest reason the idea could FAIL the judges
If pitched carelessly, it can sound like "just another compliance dashboard" or get mentally filed under Finance Controller before the differentiation is explained.

### 18. How to overcome that weakness
Open the pitch with the distinction explicitly, in the PM-style problem statement from Step 7 — lead with the ₹-and-days urgency ("your tax audit is in weeks, here's what you're about to lose and here's the payment run that avoids it") before any mention of features, and keep the live demo anchored to a real, cited ₹ number rather than a UI tour.

---

## Sources & Evidence

- [Section 43B(h) → new Income-tax Act 2025 mapping, Sept 30 2026 audit deadline — taxupdate.in](https://taxupdate.in/income-tax/771/cbdt-faq-deep-dive-7-section-43b-43bh-msme-section-37-income-tax-act-2025-actual-payment-tax-audit/)
- [45-day MSME payment rule explainer — Business Standard](https://www.business-standard.com/finance/personal-finance/45-day-msme-payment-rule-impact-and-details-of-section-43b-h-explained-124032600333_1.html)
- [india-compliance GitHub issue #3086 — missing MSME 43B(h) automation features](https://github.com/resilient-tech/india-compliance/issues/3086)
- [MSME Payment Tracker tool — thegstcalculator.in](https://thegstcalculator.in/tools/msme-payment-tracker)
- [B2B Payment Practices Trends India 2025/2026 — Atradius](https://atradius.in/knowledge-and-research/reports/b2b-payment-practices-trends-india-2026)
- [KnowYourBusinessScore / Recordent — SME Street](https://smestreet.in/finance-banking/knowyourbusinessscore-to-help-msmes-assess-buyer-credit-risk-12493875)
- [RazorpayX Payouts product page](https://razorpay.com/x/payouts/)
- [RazorpayX business banking suite](https://razorpay.com/x/)
- [RBI Payment Aggregator Master Direction 2025 — Mondaq](https://www.mondaq.com/india/financial-services/1706010/rbi-master-direction-2025-compliance-mandate-for-payment-aggregators-and-pa-p-deadline)
- [RBI PA 2025 guidelines — AuthBridge](https://authbridge.com/blog/rbi-payment-aggregator-master-direction-2025/)
- [Nodal/Escrow reconciliation — Terra Insight](https://www.terra-insight.com/insights/nodal-escrow-reconciliation-india/)
- [Vendor background verification — AuthBridge](https://authbridge.com/solutions/vendor-background-verification/)
- [Vendor fraud identification — Veridion](https://veridion.com/insights/articles/how-to-identify-vendor-fraud)
- [Fake ISO certification B2B export scam — The420.in](https://the420.in/delhi-dwarka-cyber-fraud-call-centre-b2b-export-scam/)
- [UPI outages 2025 — ORF](https://www.orfonline.org/expert-speak/upi-at-scale-outages-and-the-push-for-resilient-systems)
- [UPI outages analysis — InsightsOnIndia](https://www.insightsonindia.com/2025/04/18/upsc-editorial-analysis-indias-upi-outages-and-the-future-of-digital-payment-infrastructure/)
- [Payment gateway downtime/failover guide — Razorpay blog](https://razorpay.com/blog/payment-gateway-downtime-and-failover-in-2026-india-guide)
- [FEMA compliance guide — Tally Solutions](https://tallysolutions.com/business-guides/fema-compliance-for-businesses-foreign-exchange-regulations-how-to-stay-compliant-in-india/)
- [Paying remote workers in India — Skydo](https://www.skydo.com/blog/pay-remote-workers-india)
- [Duplicate invoice fraud in AP — Open Money](https://open.money/blog/prevent-duplicate-invoice-fraud-ap/)
- [Official Razorpay AI Buildathon 2026 track descriptions — razorpay.com/buildathon/](https://razorpay.com/buildathon/)
