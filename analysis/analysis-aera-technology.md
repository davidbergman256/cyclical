# Analysis: Aera Technology

Aera sells a "Decision Cloud" to Fortune-500 supply chains. It reads ERP data, recommends actions such as rebalancing inventory or expediting an order, writes the accepted ones back into the ERP, and logs each decision with its context, the action taken and the outcome in a "Decision Ledger." **Overlap: 4/10.** Aera has built Cyclical's decision record (recommendation → human accept/override → outcome) and a recommend → automate path. It has none of the person/agent node graph, outcome-graded shadow comparison, rubber-stamp defense, statistical graduation or cross-customer pooling. The most important thing to learn is why Aera never needed pooling. One Unilever or Merck generates millions of SKU × location × week decisions, enough to learn inside one customer. Cyclical's pooling plays the same role for small businesses that a single customer's scale plays for Aera, so Aera's buyer choice supports Cyclical's thesis rather than threatening it.

*Research note:* direct page fetches (aeratechnology.com, gartner.com, logisticsviewpoints.com, enterprisetimes.co.uk) were blocked by this session's network, and the shared web-search budget ran out after seven queries. Facts below come from search-result extracts of those pages. Items marked "(from memory)" were not re-verified.

## What it actually is

- **History and team.** Aera began as FusionOps, a supply-chain analytics company, and rebranded as Aera in 2017 with Fred Laluyaux, ex-CEO of Anaplan, as CEO (from memory). It is headquartered in Mountain View. PitchBook lists 438 employees [5].
- **Funding.** Estimates of total funding run from about $134M (ZoomInfo) to $174–178M (PitchBook, CB Insights) [5]. The last widely reported round was an $80M Series C in 2019, led by DFJ Growth with NewView and Georgian [5][6]. Seven years without a public round suggests either profitability or a quiet down-round (probability ~50/50, unverifiable here).
- **Product.**
  - The **Decision Data Model (DDM)** unifies ERP and external data across "100+ subject areas" with "thousands of industry-relevant measures" (vendor claim). It "captures all the decisions made in your organization — along with their context, actions taken, and outcomes" [1][2].
  - **Aera Skills** are packaged decision apps built in Aera's low-code tooling, first announced in 2019 [7]. Examples are demand planning, inventory rebalancing, order expediting, material allocation and waste prevention [8].
  - **Decision Ledger** is "a persistent, traceable record of every decision made in Aera, with its business context, reasoning, policies evaluated, actions, and outcome." Since October 2026 it also takes decisions "sent from another system through Aera's API" [2][3].
  - **Governance and Policy Studio** were among six updates announced at AeraHUB 26 NYC in October 2026. Governance rules can block a decision, require approval or issue a warning, and every rule evaluation is logged in the Ledger. Policy Studio drafts machine-readable rules from an uploaded policy document, which "are not applied without human review" [1][3][4].
  - **Agents** are "grounded in the Decision Data Model: your organization's actual decisions, outcomes, business rules, and certified data" (vendor claim) [1].
- **Buyer.** Heads of supply chain and CIOs at large CPG, pharma and high-tech companies. Named customers include Merck KGaA, whose ~4,000 employees query 1.2B rows daily; its CIO said "Aera is the foundation of our self-driving supply chain" [9]. Unilever's Chief Supply Chain Officer called Aera "instrumental" [7][10]. Mars and Dell expanded their roadmaps (2024) [10]. Merck Animal Health, Hershey and AstraZeneca appear in Aera webinars and press [8][11].
- **Analyst position.** Aera says it was a Leader in Gartner's first Magic Quadrant for Decision Intelligence Platforms (2026, vendor claim, unverified) [1] and a Leader in IDC's MarketScape for decision intelligence twice [2].
- **Pricing.** Not public. Aera sells enterprise subscriptions through AWS and Azure marketplaces [12][13]. Deals are likely six to seven figures a year (from memory, unverified).
- **Architecture.** Aera crawls transactional systems such as SAP, transforms the data into the DDM, runs models and rules, shows recommendations in its own UI, chat or email, and writes accepted actions back to the ERP (from memory, consistent with [1][2]). Each customer has a separate tenant.

## Loop comparison

| Aspect | Aera's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | The unit is a **decision type** (e.g. "rebalance SKU between DCs"), not a node a person or agent occupies. There is no org graph. People appear only as approvers. | Different |
| A2 Observation | Reads ERP and supply-chain transaction data into the DDM through connectors. This is data integration, not process mining of email and calendar logs, and there is no missing-edge detection. Onboarding needs "experienced resources" [GPI]. | Different (heavier, and blind to human work) |
| A3 UX | Aera's own app, plus chat and email delivery of recommendations. Reviewers call it "overwhelming to new users" [GPI]. Accepted actions write back to the ERP. | Worse for Cyclical's goal (adds a new tool); write-back is similar to drafts-as-approval |
| A4 Permissions | Governance rules block, require approval or warn, triggered by policy and criticality tier, not by request wording. Policy Studio turns written policy into rules after human review [3][4]. There is no JIT grant between nodes and no frequency → missing-edge signal. | Partly same (rules over persuasion); no edge-learning |
| A5 Shadow, outcome-graded | Aera logs recommendation, human action and outcome [2]. No source shows it grading the *human's* decisions against outcomes, or resolving human-vs-AI disagreements by outcome. Overrides are "governance" [11]. | Partly. They have the data shape but not the experiment |
| A6 Checkoff, anti-rubber-stamp | Approve, adjust or override with "projected impact" shown [11]. No seeded known-bad outputs and no checker reliability scoring found. | Absent |
| A7 Graduation | Autonomy is set per decision type by confidence scores and "criticality tiers" [11]. Humans choose the level. No published statistical threshold and no automatic demotion on model change. | Different (policy-driven, not evidence-driven) |
| A8 Replacement levels | Skills mix deterministic rules, ML and LLM agents. Policy Studio compiles text into rules. There is no "compile agent behavior to code when a rule reproduces it" trigger. | Different |
| A9 Orchestrator | Policy recommendations are generated from the ledger [2]. These are policy tweaks, not proposals to remove roles or merge nodes. | Narrower |
| A10 Shared context | The DDM is exactly a business-wide context layer, and much deeper than Cyclical's. | **Better** |
| A11 Cross-business pooling | None found. Tenants are separate, and Fortune-500 data contracts make pooling commercially near-impossible. | Absent |
| A12 Anti-Goodhart | Skills are scored on business KPIs (working capital, OTIF, waste), and rule evaluations are logged. There is no explicit pairing of local eval with business guardrail, but the KPIs serve that role. | Same-ish |
| A13 Model-agnosticism | Agents sit on the DDM and the model is swappable (vendor positioning). The asset is the DDM plus the ledger, not a model. | Same |
| A14 Business model & moat | Moat is integration depth into ERP plus per-customer decision history. Target is the largest supply chains. The risk is SAP, Oracle, Kinaxis or o9 adding the same feature. | Different target, same logic (history as asset; risk from the system of record) |

**A5/A7, the aspects that matter most.** Aera's own copy is close to Cyclical's language: "Each decision and result is captured to improve future recommendations, refine thresholds" [2]. The difference is what gets graded. Aera grades its *recommendations* and uses acceptance and outcome to tune thresholds. It does not treat the human planner as a competitor to be graded on the same outcomes, and it does not use outcomes to decide *whether* a decision type may go autonomous. That decision is a human governance setting, gated by "confidence scoring, criticality tiers, and human overrides" [11]. Cyclical's stage 3 is a statistical gate (zero errors in n ⇒ error < 3/n). Aera's is a dial a VP turns once trust exists. For a Fortune-500 buyer the dial may be the right product: the VP wants the control, and the volume per decision type is high enough that a gate would trip within days.

**A10/A2.** The DDM is the most mature version of Cyclical's shared context layer in this comparison set. It was built by crawling every ERP table, not by watching inboxes. It is costly: multi-month deployments and "experienced resources" [GPI]. A dental clinic cannot afford it, and a dental clinic's practice software already *is* a DDM for one clinic.

## Where they're ahead of Cyclical

- **A decision record schema in production at scale.** The Ledger stores context, reasoning, policies evaluated, action and outcome, and now accepts decisions from third-party systems [2][3]. This is the "outcome history" asset Cyclical says it will build. Aera has years of it inside customers like Merck KGaA, where ~4,000 users decide on 1.2B rows [9]. Cyclical should copy the schema, especially "policies evaluated," which makes governance auditable.
- **Write-back.** Accepted recommendations execute in the ERP, which closes the loop. Cyclical's "send the draft = approval" is the same idea and needs equally reliable write-back into dental practice software (Dentrix, Eaglesoft, Open Dental).
- **Policy compilation from documents (Policy Studio).** Uploading a written policy and getting reviewable rules is a clean answer to part of Cyclical's A4. Agent-to-agent approvals become rules derived from the business's own documents and checked by a human before use.
- **Analyst and category legitimacy.** "Decision intelligence" now has a Gartner MQ and an IDC MarketScape. Cyclical could borrow the vocabulary of decision ledgers and decision governance when talking to DSOs, which buy like mid-enterprises.

## Where they're doing it differently (and whether their way is better)

- **Decision type vs node.** Aera never models who does the work, so it can never propose removing a role (A9, A11's randomized role-removal). Its pitch is to "make planners 20–25% more productive" ([8], vendor claim), not to remove nodes. For Aera's buyers, where planners are a small cost next to inventory, this is better. For a 9-person clinic, where labor is the cost, it is worse.
- **Human-set autonomy vs statistical graduation.** Aera's approach is easier to sell and audit. Cyclical's approach is the only one that works when nobody has the expertise or time to set the dial, as in a small clinic. Cyclical should still give owners a manual override on top of the statistical gate.
- **Per-tenant learning vs pooling.** Aera's customers have enough volume per decision type to learn alone. Learning from one tenant's data is better when the tenant is huge and the data is competitively sensitive. Pooling is required when the business is small and its data is not competitive: one clinic's no-show rates are worthless to a rival clinic 50 miles away. This contrast supports realizations §4–5.

## Feedback & reviews on these parts of the loop

**Overall ratings (independent, small n).** Gartner Peer Insights shows Aera Decision Cloud at 4.5–4.6/5 on 39–40 reviews [14][15]. For context, SAS Intelligent Decisioning scores 4.3 (n=37), Quantexa 4.4 (n=21), Cloverpop 4.7 (n=23) and Taktile 4.8 (n=8) [15]. Review pages could not be fetched directly, so the quotes below are search-extract fragments:

- *Automation and integration (A3, A10):* "real time decision automation, seamless integration with multiple enterprise systems" [14].
- *UX burden (A3):* "hard to learn … can be overwhelming to new users" [14]. This is the opposite of Cyclical's near-zero-UI premise.
- *Onboarding (A2):* "onboarding and optimization require experienced resources" [14]. This is independent evidence that DDM-style onboarding is services-heavy.

**Outcome claims (A12, A14), mostly vendor-sourced.**

- Pharma: 20% less demand-planner workload; food and beverage: 25% less planner workload and 5–10% of working capital freed; "$20M saved from decisions previously left unactioned" (vendor claims, unnamed customers) [8].
- Waste prevention: "up to 20%" waste reduction, $50M–$200M working capital released, 75–90% less manual triage time (vendor claims) [8].
- **Independent critique:** Enterprise Times notes that Aera's 20–30% inventory carrying-cost improvement exceeds Deloitte's 7–16% range and calls the claims bold [16]. A customer-reference directory notes Aera's case studies "often focus on deployment scope rather than ROI data" [10].
- *Merck KGaA* (customer-sourced, via CIO.com): inventory reduced and on-time-in-full improved, with no numbers given [9].

No evidence turned up on whether overrides are mined as a learning signal: the search extract says "the results don't say whether overrides are stored … as a separate outcome signal" [2][11]. There is also no evidence of seeded audits or checker scoring. I found no Reddit or Hacker News discussion, which is expected for a product with ~40 Peer Insights reviews and Fortune-500 buyers. Probability Aera does something like A5's outcome-resolved disagreement sampling internally without marketing it: ~30%.

## Peers, only where they illuminate

- **o9 Solutions** (from memory): supply-chain planning built on an "Enterprise Knowledge Graph," valued at ~$3.7B in 2023. Like Aera it serves large enterprises and learns per tenant. Its graph models products, sites and constraints, not people or agents.
- **Peak.ai** (acquired by UiPath in 2025, per brief): a mid-market decision-intelligence company in pricing and inventory. The acquisition shows the category being folded into an automation/RPA vendor, the "system that does the work" layer, which is the layer Cyclical wants to own. This is weak evidence that standalone decision intelligence does not hold up without execution.
- **Quantexa** (from memory): entity resolution for financial crime and KYC, rebranded "decision intelligence." It shares the vocabulary but not the loop.
- **Cloverpop** [15]: a "decision bank" that records *human* business decisions and reviews their outcomes later. It is the closest peer to A5's idea of grading humans on outcomes, but it is manual journaling, not an automation loop.
- **Taktile** [15]: a credit and risk decision platform with backtesting and experimentation of decision policies against real outcomes (defaults). Within lending it is the clearest outcome-graded, experiment-driven decision engine.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraint.** FusionOps had supply-chain analytics connectors into SAP at large manufacturers. Laluyaux came from Anaplan, an enterprise planning company sold top-down to CFOs. Supply chains suit decision automation for four reasons: decisions are high-volume and repetitive (reorder, rebalance, expedite); outcomes are measurable within days or weeks (stockouts, OTIF, write-offs); the dollar effect per decision is large; and the ERP already logs everything. Aera went where the volume of outcome feedback within one customer was enough to learn from. That is the same constraint Cyclical faces, solved by choosing big customers instead of pooling small ones.

**Copy.**
1. The Ledger schema: context, recommendation, policies evaluated, human action, outcome, and decisions ingested from other systems.
2. Rules-based governance with block / require approval / warn tiers, logged on every evaluation.
3. Policy Studio's draft-rules-from-documents step for agent permissions.
4. Write-back as the close of the loop.

**Avoid.** A heavy data model built before any value, a new UI that reviewers call overwhelming, and autonomy as a human-set dial. The dial cannot work in a clinic with no planner to set it.

**Exploit.**
1. Aera cannot pool, for contractual reasons, and does not model people. The products that follow from those two gaps (role-removal experiments, a shared exception desk, rare-segment certification) are Cyclical's.
2. Aera's evidence is weak on outcome numbers. Cyclical can make audited, pooled outcome deltas its sales asset, e.g. "show-up rate +x% across 600 clinics, randomized."
3. DSOs are where the two worlds meet. A 300-office DSO has Aera-like volume and buys like a mid-enterprise. Cyclical's DSO pitch should sound like decision intelligence with pooling built in.

**Is Cyclical a clone?** No. Cyclical overlaps with Aera's *learning-record* layer, A5's data shape and A13, but is orthogonal on A1–A3 and A11 and targets a different buyer. Aera is closer to the "decision record + governance" sub-layer Cyclical would have to build, a strict subset of Cyclical's loop minus the people graph.

**Threat level to dental: low (~5% that Aera competes in dental SMB within 3 years).** The signal that the threat is rising would be Aera launching (a) packaged Skills for multi-site services businesses such as DSOs, vet groups or clinics; (b) any **cross-tenant benchmark or pooled model** offering; or (c) a partnership with a practice-management vendor through the October 2026 API that lets the Ledger take decisions from other systems. Item (c) is the more likely route, because it makes Aera a neutral decision system of record that a system-of-record owner could license instead of building Cyclical's loop.

## Sources

1. https://www.gartner.com/reviews/product/aera-decision-cloud?marketSeoName=analytics-business-intelligence-platforms (plus DDM/agents extracts from https://www.unite.ai/aera-six-updates-building-governing-enterprise-ai-decisions/ and https://pulse2.com/aera-technology-profile-fred-laluyaux-interview/)
2. https://www.aeratechnology.com/technology/ ; https://www.aeratechnology.com/blogs/clinical-trials-reimagined-decision-intelligence-in-action ; https://www.cityam.com/aera-technology-named-a-leader-for-the-second-time-in-the-idc-marketscape-for-worldwide-decision-intelligence-platforms/
3. https://finance.yahoo.com/technology/ai/articles/aera-technology-unveils-six-agentic-130000530.html
4. https://www.enterprisetimes.co.uk/2026/10/30/aera-bets-on-decision-governance-not-just-ai/ ; https://logisticsviewpoints.com/2026/10/07/aera-technology-decision-intelligence-loop/
5. https://pitchbook.com/profiles/company/61119-82 ; https://www.cbinsights.com/company/fusionops/financials ; https://www.zoominfo.com/financial/aera-technology-inc/407259845 ; https://craft.co/aera-technology
6. https://prwire.com.au/pr/84285/aera-raises-80-million-series-c-financing-round-led-by-dfj-growth
7. https://www.enterprisetimes.co.uk/2019/06/27/aera-technology-gets-funding-for-growth/
8. https://www.aeratechnology.com/blogs/optimizing-inventory-in-pharma-supply-chains/ ; https://www.aeratechnology.com/blogs/improving-inventory-performance-in-food-and-beverage-supply-chains-using-decision-intelligence/ ; https://www.aeratechnology.com/news/aera-technology-decision-intelligence-cuts-supply-chain-waste-by-20percent/ ; https://www.aeratechnology.com/blogs/supply-chain-waste-prevention-reimagined-decision-intelligence-in-action/
9. https://www.cio.com/article/215839/merck-prescribes-ai-for-supply-chain-complexity.html
10. https://www.enterprisetimes.co.uk/2024/11/07/a-conversation-with-aera-technology/ ; https://www.featuredcustomers.com/vendor/aera-technology
11. https://www.aeratechnology.com/decision-intelligence-faq/ ; https://www.aeratechnology.com/blogs/agentic-decision-intelligence-orchestrating-ai-agents-that-decide-act-and-deliver/ ; https://meet.aeratechnology.com/summit/aera-technology-customer-success-merck-animal-health
12. https://aws.amazon.com/marketplace/pp/prodview-2eleg2lr5dcuk
13. https://marketplace.microsoft.com/en-us/product/saas/aeratechnologyinc1647381235288.aera_cos_platform?tab=overview
14. https://www.gartner.com/reviews/vendor/aera-technology ; https://www.gartner.com/reviews/product/aera-decision-cloud
15. https://www.gartner.com/reviews/market/decision-intelligence-platforms/compare/product/aera-decision-cloud-vs-quantexa-decision-intelligence-platform ; https://www.gartner.com/reviews/market/decision-intelligence-platforms/compare/product/aera-decision-cloud-vs-cloverpop-decision-intelligence-platform ; https://www.gartner.com/reviews/market/decision-intelligence-platforms/compare/product/aera-decision-cloud-vs-taktile-decision-platform ; https://www.gartner.com/reviews/market/decision-intelligence-platforms/compare/product/sas-intelligent-decisioning-vs-aera-decision-cloud
16. https://www.enterprisetimes.co.uk/2025/04/03/how-to-improve-inventory-metrics-by-20/
