# Analysis: Stripe as the canonical pooled-outcome network (Radar, Adaptive Acceptance, Smart Retries, Payments Foundation Model, agentic commerce)

Stripe is not a Cyclical competitor. It is the best real example of the moat Cyclical claims in A11/A14: outcome labels (chargebacks, declines, recoveries) that arrive weeks after a decision, pooled across millions of merchants, train shared models that no single merchant could build. The models have been rebuilt three times while the labeled history carried over. **Overlap score: 2/10.** Stripe shares Cyclical's moat logic but none of the business-graph, workflow or staff-replacement parts. The most important lesson is that Stripe's pool is defensible mainly for two reasons. First, the entity being judged (the card, device or IP) recurs across merchants: 92% of cards are "seen before". Second, the label is produced by a third party with money at stake and flows into Stripe's own pipe automatically. Dental front-office work meets the second condition only for insurer remittances, and the first only through the insurer × plan × procedure combination, not through patients. So Cyclical's pool will likely saturate far sooner than Stripe's, and it has to be defended by other means.

## What it actually is

**Scale.** Businesses on Stripe processed about **$1.9T in 2025, up 34%** (2026 annual letter, via a secondary tracker; I could not reach the primary). Radar, Adaptive Acceptance, Smart Retries and the foundation model all train on that same flow.

**Radar** (fraud scoring, launched 2016; Radar 2.0 in 2018) scores every card payment inside the API call. Stripe's product page says there is a **92% chance a card has been seen before on the network**. Earlier Stripe material said 89% (2018) and 91% (2023). The 2018 post says Radar "trains and evaluates multiple models daily and determines which one achieves the best performance for you." Labels come from disputes, which Stripe receives automatically because it sits in the payment flow. Stripe also gets faster pre-dispute signals through network partnerships: Visa TC40 and Mastercard SAFE fraud reports, plus early dispute notifications. A third-party summary says the false-positive rate is **0.1% of good payments blocked**, which it attributes to Stripe. Architecture according to secondary write-ups: an XGBoost + deep neural network ensemble until mid-2022, then DNN-only, which cut training time by over 85% to under 2 hours (unverified against Stripe's primary post). Pricing (from memory): included in standard 2.9% + 30¢ pricing; about 5¢ per screened transaction on custom pricing; Radar for Fraud Teams (custom rules, review queues, risk insights) about 2¢ more. US dispute fee about $15 (from memory).

**Label delay is explicit in Stripe's own engineering writing.** A stripe.dev post on agent-assisted ML says: "when Stripe receives the fraudulent dispute, we gain a fraud label for a payment we scored weeks earlier." The most recent training weeks "had the most immature labels." Including them means training on fraud mislabeled as legitimate, so Stripe trades freshness against label trust. Card-network dispute windows run to about 120 days (from memory).

**Adaptive Acceptance** (re-tries falsely declined payments with modified parameters in real time). Stripe says it recovered **a record $6B in falsely declined transactions in 2024**, retry success rose **60% year over year**, and the AI upgrade brought **70% higher precision** in spotting false declines with **35% fewer retry attempts** (vendor claims, via secondary summaries). A third-party blog cites about **2.2% average authorization lift**. Make's case study reports a 4.7% revenue uplift over 3 years (vendor case study).

**Smart Retries** (Billing: chooses when to retry a failed subscription charge). Stripe's "How we built it" post claims about **$9 recovered per $1 spent on Billing**. A secondary source attributes to Stripe a 55–57% recovery rate on failed recurring payments, with Smart Retries adding about 9% over a fixed schedule (not confirmed in Stripe's own materials). Case studies give only dollar amounts: VEED $1.8M in one year, Make $1.2M, Deliveroo more than £100M combined with card updater and Adaptive Acceptance.

**Payments Foundation Model (PFM)**, announced at Sessions on 7 May 2025, is a transformer trained by **self-supervised learning on "tens of billions of transactions"**. It produces one general-purpose embedding per charge. Task classifiers then read sequences of these embeddings. Headline result: card-testing detection on large users went from **59% → 97%** (Stripe's "64% increase, practically overnight"). That came after earlier models had cut card testing by 80% over two years. Stripe says the same embeddings are being applied to disputes and authorizations. All numbers are Stripe's own; I found no independent verification.

**Agentic commerce.** Stripe co-developed the Agentic Commerce Protocol with OpenAI (open standard, Sept 2025; powers ChatGPT Instant Checkout). It also offers **Shared Payment Tokens**, scoped credentials limited by seller, amount and time window that let an agent pay without seeing card data, and Radar scoring for agent-led payments using signals like agent behaviour and transaction frequency. A critical review calls the agent-fraud piece "existing Radar applied to a new primitive", US-only and in private preview. Strategically, Stripe is making sure that outcome labels from agent purchases land in its own pipe.

**Data terms.** Stripe's Privacy Center says personal data "is required to train Stripe's fraud and loss prevention models, including those employed by Stripe Radar." Pooling comes by default with the services agreement. A merchant can opt out of the Radar API model only by contacting support, and can turn off device-signal collection, which Stripe warns raises fraud risk. Device data from Stripe.js is limited to fraud and security use: "never used for advertising… won't be rented, sold." Benchmarks shown to merchants use aggregated or de-identified data, so that a recipient "cannot identify another Business User's individual customers."

## Loop comparison

| Aspect | Stripe | vs Cyclical |
|---|---|---|
| A1 Core frame | Models payments and payment-related entities (card, device, merchant), not a business process graph | Absent |
| A2 Observation | No integration needed: Stripe *is* the payment system of record, so events and labels (disputes, declines, recoveries) arrive by construction | Different (stronger position, narrower scope) |
| A3 UX | On by default with zero setup; dashboards and a rules editor only for fraud teams | Same spirit (invisible by default) |
| A4 Permissions | No just-in-time grants. Pooling consent is blanket, through the services agreement; opt-out only via support | Different |
| A5 Shadow eval vs outcomes | Candidate models are graded daily against dispute outcomes, not reviewer opinion. Counterfactual exploration: a small random share of would-be-blocked payments is let through to measure what blocking hides (from memory, Stripe ML talks ~2015) | Ahead |
| A6 Checkoff audits | Radar for Fraud Teams has human review queues; no known seeded-error audit of reviewers | Absent |
| A7 Graduation | Per-merchant model selection and risk thresholds, not per-case-type statistical graduation | Different |
| A8 Replacement levels | Shared network model plus merchant-specific rules and thresholds. PFM embeddings plus small task heads = "general skill + thin local layer." No compiling of models into rules | Same at levels 1–2; absent at levels 3–4 |
| A9 Orchestrator | Absent (Payments Intelligence suggests settings, not reorganizations) | Absent |
| A10 Shared context | One PFM embedding per charge is reused across fraud, authorization and disputes | Different (cross-task within one domain) |
| A11 Cross-business pooling | The canonical case: 92% card recurrence, tens of billions of transactions | Ahead |
| A12 Anti-Goodhart | Fraud caught is traded against false declines. Retries are capped by card-network retry rules, and Adaptive Acceptance cut retry attempts 35%. The guardrails come from outside parties | Ahead (guardrail enforced by a third party) |
| A13 Model-agnosticism | Architecture went XGBoost+DNN → DNN (2022) → transformer foundation model (2025); the labeled history carried through each swap | Same (proof that the principle works) |
| A14 Moat | Outcome history plus position in the flow; $1.9T processed | Ahead |

**A5: counterfactual labels are the lesson Cyclical has not yet written down.** Once Radar blocks a payment, the world never says whether it was fraud. This is the "selective labels" problem: a decision suppresses its own outcome. Stripe's answer (from memory) is to let a small random fraction of payments that would have been blocked go through, and weight their outcomes by the probability of being let through. Cyclical hits the same wall the moment an agent graduates and acts. A recall agent that decides "don't text this patient" never learns whether the text would have worked. A claims agent that holds back a claim it predicts will be denied never sees the denial. Cyclical needs a standing exploration budget per case type, perhaps 1–5% randomized, or stage 3 graduation will slowly stop seeing the outcomes it was certified on. This is the A11 equivalent of the A6 seeded known-bad outputs, applied to the agent instead of the human checker.

**A13: Stripe is the existence proof.** Radar's model family changed three times in about 7 years and the PFM replaced task-specific feature engineering. The asset that carried over was the history of labeled transactions. This supports the "sign of the next model release" test in realizations.md: Stripe gains when architectures improve, because it re-trains on history nobody else holds.

**A10/A8: the foundation-model move.** Before 2025, Radar, Adaptive Acceptance and Smart Retries were separate models, each needing its own scarce labels. PFM learns from *unlabeled* transaction sequences, so label delay and label scarcity do not limit pretraining. Thin task heads then use the sparse labels. The 59%→97% jump came from better representations, not more labels. For Cyclical this connects A2 and A11. Practice-software event logs (appointments, confirmations, claims, remits, payments) are exactly that kind of unlabeled sequence, pooled across clinics. A self-supervised "practice event" embedding needs no outcome labels to train, and it makes each scarce label (a denial, a no-show) go further.

## Where they're ahead of Cyclical

- **Labels by construction.** Stripe never asks anyone for its outcome labels; disputes arrive through the pipe it operates. Cyclical has to read labels out of practice software (Dentrix, Eaglesoft, Open Dental, Denticon) and clearinghouses it does not control.
- **Default-on pooling.** Every merchant contributes on day one under the standard agreement, and opting out takes a support ticket. Cyclical's pooling will run on PHI under HIPAA. A business associate may combine data across covered entities ("data aggregation" for health-care operations) only if the BAA allows it (from memory, 45 CFR 164.504(e)). Training a cross-clinic model on identifiable PHI is legally gray. De-identified claim outcomes (insurer, plan, CDT procedure code, denial code, days to pay) are much easier to pool. The BAA has to be designed for pooling from the first contract.
- **Cold start solved by the network.** A brand-new Stripe merchant gets full Radar protection with zero history, because the card has a history. This is the commercial form of A11 Cyclical should sell: a new clinic's claims agent starts *already graduated* on common insurer × procedure cells, skipping stages 1–2 for the 80% of cases the pool has certified.
- **Handling of immature labels.** Stripe explicitly trades off training on recent weeks with immature labels against training on stale data. Cyclical's stage 3 counts ("zero errors in n runs") need the same rule: a claim is not a "clean run" until its remittance has arrived, and a denial can arrive about 42 days after resubmission (vendor figure). Counting too early inflates graduation.

## Where they're doing it differently (and whether their way is better)

The table below tests whether the conditions behind Stripe's defensibility hold for dental front-office work.

| Condition | Stripe | Dental front office (Cyclical) | Holds? |
|---|---|---|---|
| Entity recurs across nodes | 92% of cards seen before; tens of billions of transactions | Patients rarely span clinics, so patient-level recurrence is ~0. **Insurer × plan × procedure recurs almost totally**: a few dozen large payers × ~30 procedure groups ≈ 1,500 core cells (rough) | Only for payer-facing processes |
| Volume per node | Large merchants alone generate millions of labels | ~3,000–5,000 claims and ~5,000 appointments per clinic per year (rough); 10,000 clinics ≈ 40M claims/yr ≈ 27k per core cell | Enough for stage 3 per cell; 3–4 orders of magnitude below Stripe |
| Label delay | Weeks (Stripe's word), up to ~120-day dispute windows; early fraud warnings shorten it | Insurer payment averages ~17 days (Henry Schein One figure); range 15–60 days; denial rework +42 days (vendor, unsourced). Show-ups: same day. Recall reactivation: months | **Holds as well as or better than Stripe**; delay is not the binding constraint |
| Label clarity | Disputes are money-denominated but noisy (friendly fraud labeled as fraud) | Remits: very clear (paid amount plus standard denial reason codes). Show-ups: clear. Treatment acceptance, call quality: weak or none | Holds for remits and show-ups |
| Who produces the label | Issuer or cardholder, a third party with money at stake; the merchant can't tamper | Insurer remits: third party ✓. Bank deposits ✓. Show-up status and treatment acceptance: typed in by front-desk staff, the people being replaced | Partly; staff-entered labels need cross-checks (check-in timestamp, same-day payment) |
| Adversarial? | Yes. Fraudsters adapt, so a frozen dataset decays and only a *live* pool keeps up. This is the deepest part of Stripe's moat | Mostly not. Payers change rules yearly (frequency limits, downcoding edits), which is drift, not evasion. Patients don't game no-show models | **Does not hold**: a static dataset of a few hundred clinics may match a huge pool |
| Who owns the label pipe | Stripe | Practice-software vendors and clearinghouses (DentalXChange, Vyne, Optum/Change) | **Does not hold**: the label owner is the strategic threat |

**What this implies, quantified.** Stripe's pool keeps compounding because new fraud patterns keep appearing and each card's history keeps growing. Cyclical's no-show and confirmation-text models are non-adversarial and keyed on features rather than identities, so they hit diminishing returns. My rough estimate (~60%) is that per-clinic accuracy on show-up and claims-acceptance prediction stops improving materially somewhere below about 1,000 clinics. A clearinghouse already processing millions of dental claims a year could pass that point on day one. The parts of A11 that do **not** saturate are:

- **randomized structural experiments** (remove a role, merge nodes), which need hundreds of clinics *running Cyclical's graph*, not just claims data;
- **payer-policy drift detection**: the first 20 clinics to see a new Delta Dental frequency edit protect the other 9,980, which is the dental equivalent of Stripe's live fraud signals;
- **fast re-certification after model swaps**.

Cyclical's moat pitch should lead with these three, not with "more claims data".

**On the Goodhart guardrail, Stripe's arrangement is better.** Adaptive Acceptance cannot spam retries because card networks cap and penalize excessive retries (from memory), so the guardrail is enforced by someone else. Cyclical's own example, a claims agent that downcodes to raise acceptance, has the same kind of external check available: the insurer's payment total and the bank deposit. Wherever possible, anchor the A12 guardrail in a number a third party produces, not in a metric Cyclical computes.

**On incentives, Stripe has a weakness worth exploiting.** The merchant bears fraud losses and the $15 dispute fee, while Stripe earns on approved volume. That pushes Stripe to lean toward approving, and merchants complain about the opposite failure (false declines), so the tension shows up on both sides. Cyclical can price so that it earns from collections or show-ups, not per task, which puts its incentive on the business-level outcome. That would be a real sales argument to clinic owners who distrust vendors.

## Feedback & reviews on these parts of the loop

**Pooling and privacy (A11, A4).** The independent evidence is a 2020 Hacker News thread, "Stripe records user movements on its customers' websites" (Stripe.js collecting mouse and device signals for Radar). A Stripe cofounder replied in the thread that the data serves fraud prevention only. Lesson: merchants accepted network-wide pooling *because* it was scoped narrowly to one purpose (fraud) and visibly worked. Cyclical's pooling terms should name the purposes (claims outcomes, scheduling outcomes) as narrowly as possible. Independent.

**False positives (A5/A12).**
- A BlackHatWorld merchant reported "almost all of my transactions are being blocked" after Stripe imposed 3D Secure, and a reply noted Radar can block a payment even after it passes 3DS. Independent, anecdotal, and from a forum that skews high-risk.
- Chargeblast (a vendor selling chargeback tools) advises raising the block threshold to 85–90 to cut false declines. Vendor.
- A review aggregator claims Capterra and G2 users report 5–12% false-positive rates in some verticals, especially international SaaS, without citing reviews. Unverified.
- Against these sits the 0.1% false-block figure attributed to Stripe. Vendor.

The pattern: complaints cluster on opacity (why was this blocked?) and on merchants in unusual segments where the pooled model fits poorly. **That is the cost of pooling for whoever is atypical.** In dental, the atypical clinics are pediatric, ortho-heavy, Medicaid-heavy and rural clinics. Cyclical needs per-segment pools, or at least segment-specific stage-3 bars, so the general model doesn't quietly underperform for them.

**Recovery tools (Smart Retries / Adaptive Acceptance).** FlyCode, a recovery vendor, writes about "what they miss", arguing a 55–57% recovery ceiling leaves revenue on the table. Churnkey claims a further ~20% lift on top of Stripe. Both are competitors selling add-ons, so treat them as vendor claims. They do show that even the canonical pooled model leaves a layer of per-business behaviour (dunning messaging, cancellation flows) to specialists. This matches Cyclical's A8 level 2.

**Foundation model (A10/A13).** A Medium piece asks "does Stripe really need a transformer?" Skeptics note that the 64% headline is a relative gain on one task (card testing at large users), the most adversarial and highest-volume pattern there is. I found no independent replication or evidence that it helps low-volume, slow-label tasks like disputes. Independent, but commentary only.

**Agentic commerce.** One independent review calls agent-fraud scoring a relabel of existing Radar, in private preview and US-only.

## Comparison: other pooled-outcome networks (Gong, Klaviyo, Ramp)

| | Gong | Klaviyo | Ramp |
|---|---|---|---|
| What's pooled | Recorded sales conversations: "2.5 billion customer conversations", 300+ buying signals (vendor) | Email/SMS sends and the orders they drive; benchmarks over "billions of emails and text messages", 167k+ merchants (third-party figure) | Card, bill-pay and contract spend across customers (~50k businesses, from memory) |
| Outcome label | Deal closed won or lost, in Salesforce | Order placed (Shopify or other store event) | Price paid: a benchmark, not an outcome |
| Label delay | Sales cycle, months | Hours to days | None |
| Who owns the label | The CRM, maintained by reps | Partly Klaviyo (it observes the store's order events) | Ramp (it processes the payment) |
| Published lift | Deal score "20% more accurate than CRM data alone, 22% more than reps" (vendor) | Benchmarks use peer-group medians; I know of no published lift for the pooled models | "Price Intelligence" savings claims (vendor, from memory) |
| Defensibility | Medium. Independent reviewers note accuracy "depends entirely on manual CRM data quality" | Medium. Benchmarks pool across merchants, but predictive CLV/churn models are trained per account and need a minimum order history (from memory: ~500 ordering customers, 180 days) | Low to medium. Similar contract-price data exists at Vendr and Tropic; Ramp publishes vendor-adoption stats openly |

Each one teaches Cyclical something different. **Gong** shows a label that lives in someone else's system and is typed in by the people being measured: its forecast quality depends on rep CRM hygiene. That is exactly Cyclical's exposure on show-up and treatment-acceptance labels typed into practice software. **Klaviyo** draws the boundary Cyclical has to cross. It pools *benchmarks* across merchants but trains *predictions* per account, because store-level behaviour varies more than the pool can absorb. Cyclical's claim that a shared skill plus a thin local layer beats per-clinic models needs evidence per process. It probably holds for payer-facing work (insurer behaviour is shared) and is weaker for patient-facing work (local demographics). **Ramp** shows that a pooled *benchmark* with no delay and no adversary is easy to copy. If Cyclical's pooled asset ends up as "median days-to-pay by insurer", it is a Ramp-style benchmark, not a Stripe-style moat.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraint.** Stripe started as a developer-first payment API. Owning the transaction flow gave it three things free: every event, every outcome label, and every merchant's data under one agreement. It faced an adversary (card testers, stolen cards) that punishes any frozen model. Fraud prevention began as a cost to Stripe, because fraud drives chargebacks and merchant loss. Radar turned that cost into a product bundled into the base price, which kept every merchant contributing data. The foundation model is the logical next step: once you hold tens of billions of labeled-and-unlabeled sequences, the asset is the sequence history, and each task becomes a cheap head on a shared representation.

**Copy.**
1. Bundle pooling into the base product, opt-out rather than opt-in, with narrowly named purposes. For Cyclical that means a BAA written for data aggregation and a de-identified claims-outcome schema from day one.
2. Use self-supervised pretraining on pooled event logs (A2 data) so label scarcity limits only the thin task heads.
3. Keep a randomized exploration budget after graduation (counterfactual labels).
4. Gate stage-3 "clean run" counts on label maturity (remit received), as Stripe handles immature labels.
5. Sell cold-start graduation ("day-one autonomous on common insurer × procedure cells") as Radar sells day-one fraud protection.

**Avoid.** Claiming a Stripe-sized compounding moat on non-adversarial, patient-level predictions. The pool for those likely saturates at hundreds of clinics, and a clearinghouse or practice-software vendor already holds a bigger one.

**Exploit.** Stripe's pool covers *one transaction type* and cannot run structural experiments on how a business is organized. Cyclical's defensible pooled asset is the one only a graph operator across hundreds of clinics can produce: randomized role-removal and node-merge results, plus early detection of payer-policy drift. Neither is in any clearinghouse's data.

**Threat level.** Stripe itself: low. Stripe moving into dental front-office orchestration is unlikely (<5% in 3 years). The danger is the **Stripe pattern applied by dental's own pipe owners**. A clearinghouse (DentalXChange, Vyne, Optum/Change) or a practice-software vendor (Henry Schein One, Planet DDS) already receives claim and remit pairs across tens of thousands of practices "by construction", just as Stripe receives disputes. **The signal to watch:** one of them launching a pooled, outcome-trained claims model, such as "predicted denial before submission, trained on N million remits", or a payments-plus-practice-software bundle with default-on data terms. That would mean the label owner has started converting its label stream into models, which is the Radar move.

## Sources

1. https://stripe.com/newsroom/news/sessions-2025 (via search extract; stripe.com was not reachable from this session)
2. https://www.zenml.io/llmops-database/building-economic-infrastructure-for-ai-with-foundation-models-and-agentic-commerce
3. https://finance.yahoo.com/news/stripe-unveils-ai-foundation-model-213120963.html
4. https://analyticsindiamag.com/global-tech/how-stripe-used-ai-to-boost-fraud-detection-from-59-97-overnight
5. https://medium.com/data-science-in-your-pocket/stripes-payment-foundation-model-does-stripe-really-need-transformer-68457b887bd4
6. https://stripe.com/radar and https://stripe.com/blog/radar-2018 (via search extract)
7. https://stripe.com/guides/primer-on-machine-learning-for-fraud-protection (via search extract)
8. https://stripe.dev/blog/scaling-radar-fighting-fraud-with-agent-assisted-machine-learning (via search extract)
9. https://blog.bytebytego.com/p/how-stripe-detects-fraudulent-transactions (via search extract)
10. https://aiengg.dev/blog/how-stripe-detects-payment-fraud
11. https://stripe.com/blog/ai-enhancements-to-adaptive-acceptance (via search extract)
12. https://stripe.com/blog/how-we-built-it-smart-retries (via search extract)
13. https://www.flycode.com/blog/stripe-smart-retries-adaptive-acceptance-explained-2026
14. https://churnkey.co/blog/stripe-smart-retries
15. https://stripe.com/en-sg/customers/veed ; https://stripe.com/au/customers/make
16. https://stripe.com/legal/privacy-center (via search extract)
17. https://docs.stripe.com/radar/risk-evaluation ; https://docs.stripe.com/disputes/prevention/advanced-fraud-detection (via search extract)
18. https://news.ycombinator.com/item?id=22936818 ; https://news.ycombinator.com/item?id=22937303
19. https://www.blackhatworld.com/seo/stripe-radar-blocking-legitimate-payments-how-can-i-adjust-fraud-rules.1713023/
20. https://www.chargeblast.com/blog/stripe-radar-blocking-real-customers
21. https://saasflags.com/products/stripe/is-it-a-scam
22. https://www.mindstudio.ai/blog/stripe-agentic-commerce-suite-5-new-primitives-ai-agents-buy-pay ; https://i10x.ai/news/stripe-extends-agentic-commerce-with-shared-tokens ; https://agentspay.ai/vs/stripe-agentic-commerce
23. https://www.dentrixascend.com/insights/blogs/dental-claims-management-reduce-denials/
24. https://clerri.com/blog/dental-insurance-claim-denial-statistics/ ; https://clerri.com/blog/dental-practice-billing-statistics/
25. https://www.beckersdental.com/dental-insurance/dentists-patients-getting-hit-by-big-insurers/78-of-dental-offices-see-uptick-in-claim-denials-report.html
26. https://help.gong.io/docs/faqs-for-deal-likelihood-scores ; https://venturebeat.com/ai/gong-forecast-gets-ai-upgrade-improving-accuracy-20-over-crm-revenue-forecasting ; https://www.oliv.ai/blog/gong-forecasting
27. https://help.klaviyo.com/hc/en-us/articles/360050180151 (via search extract) ; https://klaviyocms.wpengine.com/wp-content/uploads/2025/02/2025-Benchmark-Report_AMER.pdf
28. https://ramp.com/vendors/klaviyo
