# Analysis: Notable (notablehealth.com)

Notable sells US health systems a platform where software agents and staff share administrative work (intake, referrals, prior authorization, scheduling, revenue cycle) inside the EHR and payer portals they already use. Its rollout pattern is the closest thing on the market to Cyclical's three eval stages: a human checks every output first, and checking is dropped after "a few weeks or months". **Overlap: 5/10.** It matches Cyclical on the shape of the product (people and agents, existing apps, oversight that phases out), but it is missing the parts Cyclical calls its moat. There is no evidence of grading against real-world outcomes, of a statistical graduation threshold, of graduation per case type, of process mining, or of pooling outcomes across customers. **The most important lesson is about the buyer.** Notable picked enterprise health systems, and an enterprise is already its own pool: hundreds of clinics, tens of thousands of runs a day, one owner who can randomize across its own sites. So enterprise vendors can graduate agents without cross-customer pooling. Cyclical's pooling argument holds only for independent small practices. In dental, that means Cyclical's real rival is the large DSO (dental service organization: a company that runs billing, insurance and phones centrally for hundreds of dental offices), not Notable.

*Method caveat: every primary page (notablehealth.com, hitconsultant.net, healthcaredive.com, beckershospitalreview.com) was unreachable from this session's network. The facts below come from search-engine extracts of those pages, third-party aggregators and the brief's quotes. Items marked "(from memory)" are unverified.*

## What it actually is

**Product.**
- **Agents and staff on the same work.** Notable calls itself a healthcare "System of Work" where "people and AI agents coordinate across existing applications to complete work from start to finish" (brief, vendor). The agents work the EHR (electronic health record: Epic, Oracle Cerner and the like) and payer portals as "digital staff". In practice they log in like a user and read faxes, referrals and forms. That combines robotic process automation (RPA: software that drives other apps' screens like a person would) with LLMs (from memory).
- **Patient-facing side.** Notable also runs patient-facing pieces: digital intake/registration, reminders and outreach (its "Patient AI").
- **Pricing pitch.** The CEO describes agents as an "elastic" workforce: "health systems no longer have to choose between being overstaffed or overwhelmed" ([Greylock / HIT Consultant 2025 via search](https://greylock.com/greymatter/notable-healthcare-ai-pranay-kapadia/)).

**Build and governance layer.**
- **Flow Studio.** Health-system "operators" use Flow Studio to "build out their own workflow automations, monitor performance, view analytics dashboards" ([AVIA marketplace listing](https://marketplace.aviahealth.com/product/25664)).
- **Flow Compass (launched Oct 19 2026).** A conversational layer on top of Flow Studio to "build, test and deploy dependable AI automation".
  - Operators can ask in plain language why a live flow is failing.
  - It works within role-based access and keeps an audit trail.
  - Only the health system's own team can publish changes.
  - Launch anecdote: at NKC Health it caught, before go-live, a configuration error that would have kept questionnaire answers out of the chart ([Notable release](https://www.notablehealth.com/blog/notable-introduces-flow-compass-giving-healthcare-operators-control-of-their-ai-workforce), [HIT Consultant](https://hitconsultant.net/2026/10/19/notable-introduces-flow-compass-conversational-ai-agent-workforce-governance-ehr-workflows/)).
  - Notable frames the launch as an answer to "AI agent sprawl": configuration drift and silent failures.

**Buyer and traction (all vendor claims unless noted).**

| Metric | Figure | Source |
|---|---|---|
| Named customers | Intermountain Health, CommonSpirit Health, Sanford Health, Montage Health, NKC Health | Greylock; Notable customer stories; Healthcare Dive |
| Reach | Live at "more than 10,000 care sites" | [Healthcare Dive](https://www.healthcaredive.com/news/notable-artificial-intelligence-agents-healthcare/741592/), vendor |
| Volume | "1.5 million tasks daily" (Sept 2025); "1M+ workflows/day" (brief) | vendor |
| Impact | 3.2M staff hours "returned" a year; $130M a year in revenue plus cost savings for partners | Oct 2026, vendor |
| Case study | Montage Health: digital intake completion went from <20% to ~50% in six weeks | [Montage story](https://www.notablehealth.com/customer-story/montage-health), vendor |
| Revenue | ~$42.5M (2023, unaudited) | [Latka](https://getlatka.com/companies/notablehealth.com) |
| Funding | ~$116–127M total; Series B Nov 2021 at a ~$600M post-money valuation (one source); no confirmed round since | [PitchBook](https://pitchbook.com/profiles/company/228399-67), [Tracxn](https://tracxn.com/d/companies/notable/__M7aVzsUvlHVolDo8uFqeXB2cKqXuL1JgeEp5bBevQLM), [multiples.vc](https://multiples.vc/private-comps/notable) |
| Headcount | ~240–275 | aggregators |

No customer count is published. I estimate roughly 50–100 health-system and large medical-group customers (from memory, ~50% confidence on that range).

**Pricing: usage-based, not outcome-based.**
- **Partner schedule (~2025).** $25k a year for the platform, Flow Studio and two builder seats, plus $5k per extra seat. Worked examples bill **$10 per run** with volume discounts ([partner terms](https://www.notablehealth.com/builder-commercial-schedule)).
- **2026 summary.** Clunic describes a platform fee plus a credit allowance used up against a per-component rate card, and a $100k joining fee with a 5% revenue share for partner-built skills ([Clunic](https://clunic.com/pricing/notable)).
- **Outcome pricing.** I found no evidence of payment per claim paid or appointment kept (~80% confident none exists as standard).
- **Positioning vs. pricing.** The 2026 positioning ("vendors get held to outcomes instead of demos", "reliability replaces autonomy theater", "auditable work completion") is ahead of the pricing. "Outcome" in Notable's usage means *the work got completed and is auditable*, not that the claim was paid.

## Loop comparison

| Aspect | Notable's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | "System of Work": people and agents coordinate on multi-step flows across apps. Agents and staff fill steps, but there is no explicit graph with interchangeable occupants. | **Same idea, weaker form** |
| A2 Observation / onboarding | Flows built by operators in Flow Studio, with implementation staff and a template library. Flow Compass is a conversational builder/debugger. No evidence of mining event logs to discover the process. | **Different (worse for SMB)** |
| A3 UX | Staff keep working in the EHR; agents write into the EHR and route exceptions to work queues. Patients get a new intake surface. Operators get Flow Studio and Compass. | **Same** for workers; **better tooling** for operators |
| A4 Permissions | Agents hold their own EHR accounts under the health system's role-based access; audit trail; only the customer can publish changes. Static, not just-in-time. | **Different**. It answers Cyclical's unresolved "system node" question by using the system's own access model. |
| A5 Shadow | "Start with a human in the loop" who checks each output. That is closer to Cyclical's stage 2 than true shadow. Some health systems (UCHealth) run agents "in a shadow-like mode" first. | **Partial** |
| A6 Checkoff | Human reviews output. No known seeding of known-bad outputs, and no measurement of reviewer quality. | **Worse / absent** |
| A7 Graduation | Oversight "usually dropped after a few weeks or months". Judgment-based, per flow/deployment. No published n-runs threshold, no case-type split, no stated rule that sends an agent back for re-review after a model change. | **Worse** |
| A8 Replacement levels | Already a mix of deterministic RPA, rules and LLM steps inside one flow, so it starts at level 3 for much work. Shared flow templates across customers are roughly level 1. | **Different**: started deterministic and added LLMs |
| A9 Orchestrator agent | Flow Compass helps humans build, test and diagnose flows. No evidence it proposes removing roles or merging steps. | **Partial** (a builder, not a reorganizer) |
| A10 Shared context | Patient/EHR context shared across flows inside one customer | **Same-ish** |
| A11 Cross-business pooling | No evidence that outcomes pool across health systems. Shared asset = flow templates, connectors, partner skills. | **Absent** (each customer is big enough not to need it) |
| A12 Anti-Goodhart guardrails | Headline metrics are hours saved, task completion and intake completion; no paired business-level guardrail is described. A critic notes hours-saved ignores supervision and rework. | **Absent** |
| A13 Model-agnostic | Platform orchestrates RPA plus multiple models; specifics not public. | **Probably same** |
| A14 Business model & moat | Enterprise platform plus usage credits. Moat = EHR integrations, deployments across 10,000+ sites, operator community. | **Different** |

**A5–A7 in detail: Notable's graduation is trust-based, not statistical.**
- **What the record says.** CMO Aaron Neinstein: "when we deploy, we start with a human in the loop", framed as trust-building, with the human dropped after weeks or months ([Healthcare Dive](https://www.healthcaredive.com/news/notable-artificial-intelligence-agents-healthcare/741592/)). Nothing public says who decides, at what error rate, on how many runs, or per which case type.
- **Unit of graduation.** It appears to be a flow or deployment at one customer.
- **Who actually drives it.** The customer. Becker's quotes UCHealth: agents "start in a shadow-like mode, then earn autonomy" once proven accurate, with audit logs, dashboards and a kill switch ([Becker's](https://www.beckershospitalreview.com/healthcare-information-technology/ai/kill-switches-guardrails-the-raging-debate-over-healthcare-ai-agents/)). Governance writers note these thresholds are "management choices, not universal legal numbers" ([Hygiea](https://hygiea.tech/knowledge/how_should_healthcare_organizations_govern_autonomous_ai_agents_in_2026.php)).
- **Implication.** The market has accepted the *stages* but has no *statistic*. Cyclical's A7 rule (zero errors in n runs, per case type, re-review after a model swap) would be a real step up. Its value is defensibility: a health system's compliance officer can sign off on it.

**A4: a usable answer to Cyclical's "who answers for the system node" problem.**
- **How Notable does it.** It never asks a system for permission. The agent gets a named EHR service account. The customer's IT team grants roles through the EHR's own role-based access control, and every action is logged under that account.
- **What it means for Cyclical.** In dental, the practice software (Dentrix, Eaglesoft, Open Dental) has user roles. A system node's answer could simply be its native access-control list, administered by the office manager. Cyclical would add just-in-time *requests* routed to that admin. This is inelegant but it is what enterprises accept. Copy it.

**A2: the build model is the cost.**
- **How flows are built.** Operators configure flows; FDE-style implementation engineers sit alongside the self-service tools ([Forbes on FDEs](https://www.forbes.com/sites/spencerdorn/2026/09/02/why-forward-deployed-engineers-are-spreading-into-healthcare/)). An FDE, or forward-deployed engineer, is an engineer who works on-site at the customer to set up the product.
- **What it costs.** Building and maintaining flows is the customer's labor (builder seats, certification). That is fine for a 30-hospital system with an automation team. It is impossible for a 9-person dental office. Process mining, which reads the office's existing tool logs instead of having someone model the flow, is what makes Cyclical's version work for small practices.

**A11: why pooling is absent.**
- **Volume math.** Spread Notable's claimed ~1M workflows a day over an assumed ~50–100 customers and each customer averages roughly 10–20k runs a day (*rough*). A common case type, such as Aetna referrals to cardiology at one system, reaches 300 clean runs (<1% error at 95% confidence) in days. 3,000 runs (<0.1% error) takes weeks.
- **Internal experiments.** A system with 300+ clinics can randomize changes across its own sites. That is the role-removal experiment Cyclical says needs "hundreds of businesses".
- **What pooling would still add.** Rare cells, such as a small payer × rare procedure, and faster re-review after a model swap. Those are the leftovers Notable doesn't address.

## Where they're ahead of Cyclical

- **Production scale and integrations.** Agents run inside Epic and Cerner across 10,000+ sites (vendor claim), with payer-portal automation and patient intake already live. Cyclical has no integration with dental practice software yet.
- **Operator tooling for a governed fleet of agents.**
  - Flow Compass covers pre-launch testing (the NKC Health catch) and plain-language diagnosis of live flows.
  - Role-based publishing plus an audit trail.
  - These are what a buyer's compliance team asks for. Cyclical's orchestrator view needs the same: test before deploy, "why did this fail", who changed what.
- **Hybrid execution.** Deterministic RPA where it works and LLMs where it doesn't, in one flow. That is Cyclical's level 3, but reached from the opposite direction: they started with rules and added models.
- **Distribution and trust.** Seven-plus years selling to conservative hospital buyers. The customer-community event ("Noteworthy") gives it a channel.

## Where they're doing it differently (and whether their way is better)

- **Enterprise vs. small business.**
  - *Notable's choice:* sell to buyers who already have the volume (graduation from their own data), an automation team (build cost absorbed) and IT (permissions solved by role-based access).
  - *Cyclical's choice:* small practices, which have none of the three, so it must supply all three: process mining, pooling, and an answer for permissions.
  - Notable's path is easier to sell per dollar of engineering. Cyclical's path is the only one that reaches independents, and it creates a data asset Notable can't build, because its customers' data isn't pooled.
- **Graded on completion, not outcome.** Notable's metrics are hours returned, tasks completed and intake completion rate. For referrals, intake and scheduling it could tie runs to downstream outcomes inside the EHR (patient booked, showed up, claim paid). It has not marketed that as its grading signal. Cyclical's way is better on the merits. It also produces better sales evidence once insurers' payment statements are the answer key.
- **Trust-based graduation.** Notable's version is cheaper to explain and good enough for high-volume clerical flows, where errors surface fast in work queues. It will fail on rare, high-cost errors (wrong-payer prior auths, coding), which is where a statistical bar plus per-case-type graduation matters.
- **Vendor-built flows vs. discovered flows.** Notable's flows are modeled on purpose, so they are clean but never show "missing edges". Cyclical's mined graph shows what really happens, but it will be noisier. Unknown which wins; for small practices only discovery is affordable.

## Feedback & reviews on these parts of the loop

**Graduation and oversight (A5–A7).**
- *Vendor:* "start with a human in the loop" to build trust (Neinstein, [Healthcare Dive](https://www.healthcaredive.com/news/notable-artificial-intelligence-agents-healthcare/741592/)).
- *Independent:* UCHealth (a customer of agentic AI generally, not confirmed as a Notable customer) says agents "earn" autonomy from a shadow-like start, with a kill switch ([Becker's](https://www.beckershospitalreview.com/healthcare-information-technology/ai/kill-switches-guardrails-the-raging-debate-over-healthcare-ai-agents/)). Practitioner writers recommend moving up one autonomy level at a time and say most healthcare work belongs at levels 1–2 today ([LaunchPad Lab](https://launchpadlab.com/blog/ai-agents-in-healthcare/)). None publishes a numeric bar.

**Metrics and Goodhart risk (A12, A14).**
- *Independent (Substack):* "an agent that saves 1,000 hours while creating 400 hours of supervision, rework and exception handling has a much weaker business case". It argues for managing agents as an accountable workforce, measured net of exceptions ([Substack](https://rahmeh1.substack.com/p/32-million-hours-claimed-whos-managing)). This is the same point as Cyclical's: grade against what happens, not against activity.

**Operator tooling (A9).**
- *Vendor plus trade press repeating the release:* the NKC Health pre-launch catch. No independent user review of Flow Compass exists yet; it is five weeks old.

**Third-party ratings.**
- **KLAS (the healthcare-IT customer-ratings firm):** no score found for Notable. In patient access, Waystar won Best in KLAS 2026 at 91.2 ([KLAS](https://klasresearch.com/best-in-klas-ranking/patient-access/2026/210)). In agentic administrative AI, Magical got an A+ "Emerging Company Spotlight", from only 3 interviews.
- **G2:** a page exists; no review content surfaced. No Reddit threads found, and no patient complaints found.
- **Glassdoor (employees):** 3.1/5 on 95 reviews. Cons cite "tons of layoffs" and "lack of direction" ([Glassdoor](https://www.glassdoor.com/Reviews/Employee-Review-Notable-Health-E2311834-RVW103742201.htm)). Together with no confirmed raise since 2021, this weakly suggests capital constraints, while peers raised at multi-billion valuations.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraints.**
- **Where it started.** Notable launched in 2017 with voice/wearable documentation, then pivoted to RPA-style "digital employees" for health-system front and back offices (from memory).
- **Its asset.** Deep integration with Epic and Cerner plus hospital sales relationships.
- **Why enterprise follows from that.** EHR integration is expensive to build and only pays back on big contracts. Health systems have staffing shortages, automation teams and volume. Selling per run with a platform fee fits enterprise procurement.
- **What was never forced on them.** Every customer is large enough to graduate agents on its own data and run internal A/B tests across its own clinics. Notable never *had* to pool outcomes. Its customers would likely refuse to share data with competing systems anyway.

**Answering the key questions.**

*Is Notable "Cyclical for health systems"?* Half. It has Cyclical's product shape: people plus agents in existing tools, oversight that phases out, an operator console. It lacks Cyclical's learning engine: outcome grading, a statistical graduation rule per case type, mined graphs, cross-customer pooling. Health systems don't need the last two, so it's closer to "Cyclical with the pooling removed because the customer *is* the pool."

*What does the enterprise choice tell us?* It largely confirms the founder's own model. Pooling is needed for *graduation* only below a volume threshold.
- A health system, or a 500-office DSO, is above it for common case types.
- An independent dental office (~6,000 visits a year, *rough*) is far below it.
- **Pooling stays valuable at enterprise scale for:**
  - rare insurer × procedure combinations;
  - re-review after model swaps across many variants;
  - deciding which process design is best across *different organizations* (no single system can compare itself to others).
- **Consequences for Cyclical:**
  - Cyclical's moat is specifically the independent and small-group segment. That is ~86% of US dentists in 2023 but shrinking as DSOs grow (ADA HPI).
  - Pitch Cyclical as **a virtual DSO**: pooled back office and pooled learning without the change of ownership.
  - Large DSOs are the segment where a Notable-style enterprise vendor beats Cyclical, because the DSO already pools internally.

*Would Notable move down to DSOs or small groups?*
- **Small dental practices: unlikely**, about 10% within 2 years. Its pricing ($25k platform fee plus builder seats plus usage), its operator-builds-the-flows model, and its EHR integrations don't fit a $5–10k/year dental budget. Dental practice software, dental payers (Delta, MetLife dental) and CDT procedure codes are a separate stack.
- **Large DSOs: more plausible**, about 20–25%. They have enterprise buying, central RCM (revenue cycle management: billing and collections) and IT teams.
- **Ambulatory medical groups: more plausible still.** Notable already serves medical groups through their health systems (Montage Medical Group).

**Copy.**
- Flow Compass-style operator tooling: test before deploy, plain-language "why did this fail", role-based publishing, audit trail.
- The pattern of giving each agent its own account in the practice software, with the system's role-based access as the system node's answer for permissions (A4).
- Hybrid RPA plus LLM execution.
- The language of "auditable work completion", which hospital buyers have already accepted.

**Avoid.**
- Hours-saved as the headline metric; critics already attack it.
- Customer-built flows. Small offices won't staff a builder seat.
- Judgment-based graduation without a number.

**Exploit.**
- Notable's customers have no outcome-graded, statistically certified graduation. Cyclical's A5–A7 could become the standard regulators and auditors ask for. Publishing the rule (zero errors in n runs per case type, plus re-review after a model swap) is cheap marketing in a market that is openly debating "kill switches".

**Threat level: low for dental independents now, medium for large DSOs.** Signals that the threat is rising, any one of which should change David's plan:
1. Notable (or a peer) announces a DSO customer or a dental practice-software integration (Dentrix, Open Dental, Curve).
2. Notable launches benchmarks *across* customers or pooled "network" models, i.e. starts pooling.
3. Notable moves to per-outcome pricing (per claim paid or appointment kept), which would mean it grades against outcomes.
4. An Epic or Oracle partnership that gives Notable-like agents native system-of-record status. In dental the equivalent is Henry Schein One (owner of Dentrix) building this itself.

**Peers, briefly.**

| Company | What it does | Funding / valuation | Relevance to Cyclical |
|---|---|---|---|
| **Infinitus** | Voice agents for payer phone calls (benefits checks, prior-auth status); sells to pharma hubs and providers | $52M Series C Oct 2024; ~$100M total | A single-step agent. Its database of payer-call outcomes across customers is arguably *real cross-customer pooling* on one step (from memory) |
| **AKASA** | Generative AI for health-system revenue cycle (coding, prior auth) with RCM experts in the loop | $60M Series B 2021; ~$80M total | Closer to a permanent stage 2 than to graduation |
| **Hippocratic AI** | Patient-facing, non-diagnostic clinical voice agents, safety-tested by licensed clinicians | $126M Series C Nov 2025 at $3.5B | Strongest pre-deployment safety testing; reported per-hour pricing (from memory) |
| **Commure** (incl. Athelas) | RCM software plus services and ambient documentation, sold to health systems *and* medical groups | $7B valuation May 2026 | Closest to Cyclical's economics: charging a % of collections is outcome-based pricing, and its human RCM services are a pooled exception desk (from memory) |
| **Qventus** | Hospital capacity and perioperative "AI teammates" | $85M Series D Jan 2025 | Mainly scheduling and throughput optimization; orthogonal |

Peer funding figures come from aggregators ([newmarketpitch](https://newmarketpitch.com/blogs/news/healthcare-ai-agents-top-startups-valuation)). Commure is the peer to watch over Notable: it already sells to smaller medical groups, prices on outcomes and pools human labor.

## Sources

1. https://hitconsultant.net/2026/10/19/notable-introduces-flow-compass-conversational-ai-agent-workforce-governance-ehr-workflows/ (search extract only)
2. https://www.notablehealth.com/blog/notable-introduces-flow-compass-giving-healthcare-operators-control-of-their-ai-workforce (search extract)
3. https://app.dealroom.co/news/feed/notable-launches-flow-compass-to-help-health-systems-manage-ai-agents-citing-130m-in-annual-savings
4. https://www.notablehealth.com/blog/why-2026-will-be-the-year-healthcare-stops-talking-about-ai---and-starts-demanding-outcomes (search extract)
5. https://www.healthcaredive.com/news/notable-artificial-intelligence-agents-healthcare/741592/ (search extract and brief)
6. https://www.beckershospitalreview.com/healthcare-information-technology/ai/kill-switches-guardrails-the-raging-debate-over-healthcare-ai-agents/ (search extract)
7. https://rahmeh1.substack.com/p/32-million-hours-claimed-whos-managing
8. https://www.notablehealth.com/builder-commercial-schedule
9. https://clunic.com/pricing/notable
10. https://marketplace.aviahealth.com/product/25664
11. https://www.forbes.com/sites/spencerdorn/2026/09/02/why-forward-deployed-engineers-are-spreading-into-healthcare/
12. https://greylock.com/greymatter/notable-healthcare-ai-pranay-kapadia/
13. https://hitconsultant.net/2025/09/23/the-ai-paradox-in-healthcare-notable-ceo/
14. https://www.notablehealth.com/blog/healthcare-doesnt-need-more-point-solutions
15. https://www.notablehealth.com/customer-story/montage-health
16. https://pitchbook.com/profiles/company/228399-67
17. https://tracxn.com/d/companies/notable/__M7aVzsUvlHVolDo8uFqeXB2cKqXuL1JgeEp5bBevQLM
18. https://multiples.vc/private-comps/notable
19. https://getlatka.com/companies/notablehealth.com
20. https://www.glassdoor.com/Reviews/Employee-Review-Notable-Health-E2311834-RVW103742201.htm
21. https://klasresearch.com/best-in-klas-ranking/patient-access/2026/210
22. https://www.beckershospitalreview.com/healthcare-information-technology/ai/magical-earns-a-in-klas-company-spotlight-report/
23. https://hygiea.tech/knowledge/how_should_healthcare_organizations_govern_autonomous_ai_agents_in_2026.php
24. https://launchpadlab.com/blog/ai-agents-in-healthcare/
25. https://newmarketpitch.com/blogs/news/healthcare-ai-agents-top-startups-valuation
