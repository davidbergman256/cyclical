# Analysis: Celonis

Celonis is the process-mining leader: it reconstructs how a large company's processes actually run from ERP/CRM event logs, and since 2024–26 it has been repositioning that reconstructed model (the Process Intelligence Graph, now the "Celonis Context Model") as the context layer and orchestrator for AI agents built on other vendors' platforms. **Overlap score: 5/10** — it owns Cyclical's A2 (observation by process mining) and is moving fast on A1/A9/A10 (agents and people coordinated as steps in a mined process, a shared context layer), but it has nothing like Cyclical's outcome-graded eval stages (A5–A7), no outcome pooling across companies in the experimental sense (A11), and it is structurally unable to sell to small businesses. The single most important lesson is the SAP fight: Celonis's entire business depends on reading a system of record it does not own, and the owner (SAP) has spent 2025–26 tightening extraction rules while selling a competing product (Signavio). That is a live preview of Cyclical's A4 "system node" problem and A14 strategic risk in dental, where the practice-software vendors play SAP's role.

> **Research limits.** This session's web-search budget ran out after six searches and WebFetch was blocked for most hosts, so primary pages could not be read in full. Facts with a source link come from search-result summaries of those sources. Everything marked *(from memory)* is from training knowledge (cutoff mid-2026) and was not re-verified; treat those with roughly 75% confidence on specifics (numbers, dates) and higher on the broad picture.

## What it actually is

**Process mining, defined once.** Every transactional system writes an event log: rows of *(case id, activity, timestamp)* — e.g. purchase order 4711, "goods received", 2026-03-02 14:11. Process mining stitches those rows into the actual flow of each case, then aggregates thousands of cases into a map showing the real paths, their frequencies, durations and rework loops, and compares that to the intended process. Celonis did not invent the method (Wil van der Aalst's academic work did, and van der Aalst has been Celonis's Chief Scientist since ~2021 *(from memory)*), but it commercialized it on SAP data.

**Product, layer by layer** (names change often; this is the late-2026 stack):

| Layer | What it does | Status / source |
|---|---|---|
| Extraction & Data Core | Connectors pull tables from SAP (via the RFC/ABAP extractor), Oracle, Salesforce, ServiceNow etc.; Data Core (GA Nov 2025) also queries customer data lakes (Databricks, Microsoft Fabric) without copying data | [7], [8] |
| Object-centric process mining (OCPM) | Instead of forcing one case id per process, models many object types (order, delivery, invoice, customer) and the events that touch several at once; OCEL 2.0 is the open log standard Celonis's researchers co-authored *(from memory)*. Celonis introduced object-centric "Process Sphere" ~2022–23 and extended OCPM capabilities at Celosphere 2025 | [7]; *(from memory)* |
| Process Intelligence Graph (PIG) | Announced Celosphere 2023 *(from memory)*: a system-agnostic model of the business built from objects, events and relationships, enriched with Celonis's pre-built "business knowledge" (KPIs, process templates, best-practice libraries for P2P, O2C, AP etc.) | [5]; *(from memory)* |
| Celonis Context Model (CCM) | Launched **12 May 2026** with the acquisition of Ikigai Labs (decision intelligence / forecasting). Pitched as a layer "between raw data systems and AI execution platforms"; Constellation describes it as a context graph plus a "world model" for inference and foresight, and as the new core of the platform that evolves the PIG. Available regardless of which stack the customer builds agents on | [1], [2] |
| Action Flows / Action Engine | Low-code automations triggered from process signals (e.g. invoice about to miss early-payment discount → write-back to SAP, Slack message). Built on technology from Integromat, which Celonis acquired in 2020 and which also became the standalone SMB automation brand **Make** *(from memory)* | *(from memory)* |
| Orchestration Engine | GA at Celosphere 2025: "coordinates AI agents alongside people and systems as they run end-to-end processes" | [7], [8] |
| AgentC + MCP server | Launched Celosphere 2024: tooling and partnerships so agents built on Microsoft Copilot Studio, IBM watsonx Orchestrate (also AWS Bedrock, CrewAI, others *(from memory)*) can read Celonis process data; 2025 added a Process Intelligence MCP server ("USB-C for agents") | [3], [4], [6], [7] |
| Agent Miner | 2025 app that mines the behavior of AI agents themselves, to understand and govern them | [7] |

**Buyer and traction** *(from memory unless noted)*: founded 2011 in Munich by three TU Munich students; dual HQ Munich/New York; ~3,000 employees; last priced round Aug 2022, $1B at a **$13B valuation**; customer count publicly stated in the low thousands (~1,400–1,600 enterprises: Siemens, BMW, Uber, Dell, Pepsico-class names); ARR reported in the high hundreds of millions, never confirmed publicly; layoffs in 2023. Gartner Magic Quadrant for Process Mining: Leader every edition. Buyer is the CFO/COO/CIO of companies with typically $1B+ revenue, often with an SI (Accenture, Deloitte, EY, KPMG) running the implementation.

**Pricing** *(from memory)*: not public. Enterprise subscriptions priced by platform tier, number of processes/use cases, data volume and users; typical contracts six figures per year at entry and seven to eight figures for global rollouts, plus SI services. A free tier, **Celonis Snap** (2019), let small teams upload CSVs or connect a few cloud apps; it was quietly retired a few years later — Celonis's one visible attempt to go downmarket did not stick.

## Loop comparison

| Aspect | Celonis's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | Business as an object-centric graph of objects/events (PIG → CCM). Orchestration Engine coordinates "AI agents alongside people and systems" as steps in a process | **Different / partial** — graph of *objects and activities*, not of *roles*; a person and an agent can perform the same step, but the node isn't an occupant slot with a contract |
| A2 Observation | Mining ERP/CRM event logs via standardized extractors; conformance checking against the intended model | **Better** (on structured systems) — 15 years of connectors, OCPM, conformance checking. **Absent** for email/calendar-heavy work; task mining (desktop capture) is the stopgap *(from memory)* |
| A3 UX | Analyst-built dashboards ("Views", "Studio"), Process Copilots (chat over process data); agents pushed into Teams/Copilot | **Different** — new tool for analysts and managers, not "drafts in your drafts folder"; the agent-in-Teams route is closer to Cyclical |
| A4 Permissions | Service-account extraction with broad read; access governed by the SoR vendor's license/API policy and customer IT; no JIT node-to-node grants | **Absent** for JIT; but Celonis is the live case study of *who answers for the system node*: the SoR vendor, through licensing |
| A5 Shadow eval vs outcomes | Not offered. Celonis measures *process KPIs* (cycle time, touchless rate, on-time payment), which are outcome-like, but does not run agent-vs-human shadow trials | **Absent**, though Celonis has the outcome data (paid/not paid, delivered late) that such grading would need |
| A6 Checkoff with seeded errors | Not offered | **Absent** |
| A7 Graduation per case type | Not offered; Agent Miner observes agent behavior but no statistical graduation threshold is published | **Absent** |
| A8 Replacement levels | Action Flows = deterministic automation (level 3); agents built elsewhere (level 1–2); no "compile agent to code when a rule reproduces it" mechanism | **Different** — Celonis starts at level 3 (rules) and is adding agents, the reverse of Cyclical's agent→code path |
| A9 Orchestrator agent | Opportunity identification ("Value Discovery", Transformation Hub *(from memory)*), simulation via Ikigai/CCM world model (2026), Orchestration Engine | **Same direction, stronger on simulation**; no agent that proposes removing a role and tests it |
| A10 Shared context layer | The CCM is literally sold as this: a shared operational context for every agent on any platform | **Better / same** — this is their core 2026 product |
| A11 Cross-business pooling | Benchmarks and value libraries derived from thousands of implementations (KPI ranges, "best practice" paths); no pooled outcome experiments, no randomized role-removal tests, no shared exception desk | **Different / mostly absent** — pools *knowledge and benchmarks*, not *outcomes for training and certifying agents* |
| A12 Anti-Goodhart | KPI trees link local KPIs to financial outcomes (DSO, working capital); no explicit pairing of agent evals with guardrails | **Partial** — the KPI tree is the raw material for Cyclical's guardrail pairing |
| A13 Model-agnosticism | Explicit: CCM "regardless of the technology stack"; agents on Microsoft, IBM, AWS, etc. | **Same** — and further along in practice |
| A14 Business model & moat | Moat = connectors + data model + process content + SI channel, on enterprise volume. Risk = SoR owner (SAP) restricting access and bundling Signavio | **Different target, same risk** |

### A2 — observation (where Celonis is ahead, and where the method breaks for small businesses)

The founder cites Celonis's method for A2, and it is the right method — but the method has three preconditions that hold in a Fortune 500 SAP shop and mostly fail in a 9-person clinic:

1. **A case id on every event.** SAP tables carry document numbers that link a purchase requisition to an order to a goods receipt to an invoice to a payment. Email, calendar and phone logs carry no shared case id; linking "the email to Mrs. Diaz" to "appointment 8812" to "claim 3391" is an entity-resolution problem Celonis has never had to solve at scale.
2. **Volume.** Process maps and variant statistics are meaningful at tens of thousands of cases per process per year. A clinic sees a few thousand appointments and a few thousand claims a year; most variants appear a handful of times.
3. **Money per percentage point.** Celonis's sales pitch is "1% faster cash collection on $10B of receivables = $X million of working capital." The software and SI cost (six to seven figures) only clears that bar above roughly $1B revenue. A clinic's whole front office costs ~$558k a year (realizations.md); no Celonis deal fits inside that.

That is why Celonis sells only to large enterprises: its value scales with throughput, while its cost (data engineering per ERP instance, data-model building, SI services) is a large fixed cost per customer. Snap, the free downmarket tier, died because small companies had neither the clean logs nor the dollars-per-percentage-point *(from memory)*.

**Implication for Cyclical.** Thin per-business logs are fatal to Celonis's model and only partly fatal to Cyclical's, for one reason: Cyclical's process maps don't need to be *discovered from scratch per business*. In dental, a few practice-management systems (Dentrix, Eaglesoft, Open Dental, Curve, Denticon *(from memory)*) hold appointments, procedures, claims and payments with real ids — a structured log equivalent to SAP's, just small. Cyclical can (a) ship a pre-built object-centric template of "the dental front office" (patient, appointment, treatment plan, claim, payment, recall as object types), as Celonis ships P2P/O2C templates; (b) use each clinic's thin log only to *fit* the template — which variants exist, which edges are missing — rather than to discover it; and (c) pool variant statistics across clinics on the same PMS so the thin per-clinic log is read against a thick prior. That inverts Celonis: Celonis has thick logs and pays a large fixed cost per customer; Cyclical has thin logs and must make the per-customer cost near zero by standardizing on one vertical's few systems. The email/calendar part of A2 is the genuinely new problem, and Celonis offers no help with it (task mining captures screens, which violates Cyclical's "no new box" rule).

Copy the data model: object-centric event logs (OCEL 2.0) are a better fit for a clinic than single-case-id logs, because one phone call touches a patient, an appointment and a claim at once.

### A4 and A14 — the SAP lawsuit is Cyclical's system-node problem, at scale

Facts: Celonis sued SAP in **March 2025** (N.D. Cal., No. 3:25-cv-02519), alleging SAP uses ERP dominance to make third-party access to customers' own SAP data harder and more expensive, to favor its own process-mining product Signavio [9][10]. SAP argued an injunction would force it to abandon its extraction policies and licenses, and that Celonis's refusal-to-deal theory fails [11]. On **5 June 2025** the parties stipulated that SAP will not interfere with Celonis's RFC/ABAP extractor — the method most Celonis customers use — or charge added fees for it while the case is pending; Celonis withdrew its injunction motion (Judge Chhabria) [12][13]. A secondary summary says tying claims were dismissed while monopolization, pricing and false-advertising claims survived, and that in August 2026 the court allowed supplemental discovery on SAP's "New Data Access Policy" (unverified against the docket) [14]. In Germany, the **Bundeskartellamt closed its preliminary investigation on 30 July 2026** without opening abuse proceedings: large-scale extraction is "technically challenging" but "various permissible and viable options" remain; SAP's spring-2026 API Policy had not eliminated previously permitted methods; SAP offers licensing variants without Signavio at a lower price; and SAP's commitment to keep one Celonis extraction route available weighed in the decision. Celonis replied that the decision rests on a premise SAP "has not yet confirmed" — that extraction will remain possible under the new API policy [15][16][17].

What this tells Cyclical:

- **The system node is answered by its vendor, not by anyone in the business.** Cyclical's unresolved question — who answers a permission request sent to the practice software? — has a de facto answer in Celonis's world: the customer owns the data legally, but the SoR vendor's license and API policy decide what can be read, how fast, and at what price. A "responsible human node" inside the clinic cannot grant what the vendor's terms forbid. An elegant A4 design therefore models the system node as having *two* principals: the clinic (owner of the data, grants use) and the vendor (gatekeeper of the channel, sets rate/price/scope). Rules-based grants (who asks, data class, task type) apply on the clinic side; the vendor side is a contract, not a runtime decision.
- **The SoR owner builds the competing product and then tightens access.** SAP bought Signavio (2021, *from memory*) and later moved toward API-only, policy-governed extraction. The dental analogue is a PMS vendor (Henry Schein One/Dentrix, Patterson/Eaglesoft, *from memory*) shipping its own AI front office and restricting third-party read/write. Henry Schein One has historically run a gated partner program for Dentrix integrations *(from memory)*. Celonis — a $13B company with antitrust counsel — needed a lawsuit and a regulator to keep one extractor open; a seed-stage Cyclical has neither. Realizations.md's conclusion ("integrate deeply or become that system") is reinforced: prefer PMSs with open databases (Open Dental is open-source with a documented schema, *from memory*) for the first clinics, and treat write-back access as the critical dependency to secure contractually.
- **Regulators found "technically challenging but viable" sufficient.** Expect no rescue from antitrust if a dental PMS vendor degrades access short of a full block.

### A10, A13 — Celonis is building the "shared context layer" and selling it to every agent platform

The May 2026 Context Model is the clearest statement of Celonis's strategy: become the neutral context layer that any agent (Copilot Studio, watsonx Orchestrate, Bedrock, custom) queries via MCP, so that Celonis gains value whichever model or agent vendor wins [1][2][6][7]. This is exactly realizations.md's "model-neutral layer" argument, applied to enterprise context instead of a vertical workflow. For Cyclical it confirms A10/A13 are table stakes, not differentiators: the shared context layer is being commoditized from the top of the market down.

### A5–A7, A11 — where Cyclical is genuinely different

Celonis grades *processes*, not *agents*. Its KPIs (on-time payment, touchless rate, DSO) are real-world outcomes, which is the hard part of Cyclical's A5 — but Celonis does not run an agent in shadow against a human, does not seed known-bad outputs into approval queues, and publishes no per-case-type graduation threshold. Agent Miner (2025) observes agents' behavior; it does not certify them [7]. The cross-company asset Celonis does have is *process content and benchmarks*: KPI ranges and best-practice paths accumulated from thousands of implementations and sold through value-discovery engagements *(from memory; whether Celonis computes benchmarks from pooled customer data or from consultant-curated studies could not be verified — ~50%)*. That pools *descriptions* of processes across companies, not *outcomes of interventions*. No randomized cross-company experiments, no pooled re-certification after model swaps, no shared exception desk. Enterprise customers would also resist pooling raw outcomes across competitors; small clinics, which already pool via DSOs, are more likely to accept it.

## Where they're ahead of Cyclical

- **Extraction and data modeling on structured systems.** Fifteen years of connectors, the OCPM data model, conformance checking, and pre-built process templates. Cyclical would be rebuilding a small slice of this for one vertical.
- **Context-layer positioning with distribution.** CCM + MCP server + Microsoft/IBM partnerships put Celonis process context inside the agent tools enterprises already buy [1][3][6][7].
- **Simulation.** The Ikigai acquisition adds forecasting/"world model" capability to test operating scenarios before changing them [1][2] — a model-based substitute for the randomized experiments Cyclical wants to run via pooling.
- **Battle-tested on SoR access.** Celonis knows exactly how a system-of-record vendor fights back, and has a legal and regulatory record of it.

## Where they're doing it differently (and whether their way is better)

- **Rules first, agents later (A8).** Celonis's automation path started with Action Flows (deterministic triggers and write-backs) and added agents in 2024–25. Cyclical starts with agents and compiles them to code. For high-volume enterprise processes Celonis's order is cheaper; for small businesses with few examples per rule, Cyclical's order is better because nobody will write the rules by hand.
- **Analyst UX vs ambient UX (A3).** Celonis requires analysts and data engineers to build and maintain the model and dashboards. That is the cost driver that keeps it upmarket; Cyclical's "drafts folder" approach is the only version a clinic will use.
- **Simulation vs experiment (A9/A11).** Celonis's world-model route estimates the effect of a change from historical data; Cyclical's route measures it with randomized trials across businesses. Experiments are more credible for "can this role be removed?"; simulation works with one customer's data. Cyclical should do both: simulate per clinic, confirm across clinics.
- **System-agnostic vs vertical.** Celonis sells horizontal process templates (P2P, O2C, AP) across industries, because each enterprise has enough volume alone. Cyclical must go vertical because each clinic doesn't.

## Feedback & reviews on these parts of the loop

Independent evidence gathered here is thin because of the research limits; the points below are flagged accordingly.

**A2 — implementation time and data effort** *(independent, from memory of G2/Gartner Peer Insights/Reddit patterns)*: Celonis scores well overall on G2 and Gartner Peer Insights (~4.5/5 on several hundred reviews), but the recurring complaints are that building the data model and connecting SAP takes months and requires data engineers fluent in SQL and Celonis's PQL query language, and that value depends on clean source data. Bundeskartellamt's own finding that large-scale extraction from SAP is "technically challenging" [15][16] independently confirms the extraction burden.

**A9 — "insights without action"** *(independent and vendor)*: the classic critique of process mining is that it produces beautiful maps and no change. Celonis's own product history concedes it: it rebranded from process mining to the "Execution Management System" in 2020 and added the Action Engine and Integromat-based automation explicitly to close the gap between insight and action *(from memory)*; the 2025 Orchestration Engine and 2026 Context Model are the latest round of the same move [1][7]. Coverage of Celosphere 2025 framed the pitch as "no enterprise AI without process intelligence" [18] — i.e., Celonis now sells itself as a prerequisite for someone else's action layer.

**A11 — value realization claims** *(vendor)*: Celonis publishes customer value figures (often hundreds of millions of dollars of working-capital or cost impact at large customers) from its value-discovery program; these are self-reported and should be treated as marketing.

**A14 — SoR dependence** *(independent)*: Heise headlined the Bundeskartellamt decision "Setback for Celonis" [17]; Celonis's own statement that SAP had "not yet confirmed" continued extraction under its API policy [15] is the clearest public evidence of how exposed the business is to its data supplier.

**A13 — partner integrations** *(vendor / developer docs)*: Celonis's own Copilot Studio MCP guide notes a limitation — Copilot Studio cannot name the connection created when adding an MCP tool — and offers a workaround [6]; minor, but it shows the integrations are early.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraint.** Celonis began in 2011 with one asset: the ability to read SAP tables and reconstruct processes from them. SAP runs the core of most large enterprises, and its data has stable document-id chains — the perfect process-mining substrate. That fixed the customer (large SAP shops), the channel (SAP-skilled system integrators), the price (justified by working-capital gains on billions of revenue) and the dependency (SAP's goodwill). Each later move — EMS and action automation (2020), the Process Intelligence Graph (2023), AgentC (2024), the Orchestration Engine (2025), the Context Model (2026) — extends the same asset up the stack as the market's buzzword shifted from RPA to GenAI to agents, while trying to reduce dependence on SAP by going "system-agnostic" and adding zero-copy data-lake access.

**Copy.**
- The object-centric event-log model (OCEL 2.0) as Cyclical's internal representation of the clinic graph's *data*, layered under the role/node graph.
- Pre-built process templates per vertical (Celonis's P2P/O2C content), so each clinic's thin log *fits* a known template rather than discovering a process from scratch.
- KPI trees linking local metrics to money — the raw material for A12 guardrails.
- The context-layer-via-MCP interface, so third-party dental agents (Toothy, Newton, PatientDesk) could become node occupants Cyclical grades, rather than competitors.

**Avoid.**
- Analyst-heavy implementation. Celonis's cost structure (data engineers + SI per customer) is what locks it out of small businesses; any per-clinic setup that needs a human analyst kills Cyclical's unit economics.
- Building on a single SoR vendor's goodwill without a contract for read *and* write access.
- Selling "insight". A clinic will not pay for a map of its front office; it pays for a removed task.

**Exploit.**
- Celonis cannot go downmarket: thin logs, low dollars per percentage point, and an enterprise SI channel. Its tried-and-abandoned free tier is evidence. Small, single-vertical businesses are structurally outside its reach.
- Celonis grades processes, not agents. The certification machinery (shadow against outcomes, seeded checks, per-case-type graduation, pooled re-certification) is unoccupied territory even at the enterprise top end — and it could later be sold *to* enterprises if Cyclical's dental record proves it.
- Celonis's horizontal posture means no vertical outcome pool; in dental, a pool across hundreds of clinics would be data Celonis structurally never collects.

**Relationship.** Cyclical is **orthogonal-to-superset** on the loop (it adds eval/graduation/pooling that Celonis lacks) and a **tiny-vertical subset** on observation (it needs a small slice of Celonis's mining capability). It is not a clone.

**Threat level: low for the next 2–3 years** (rough 10% chance Celonis targets small businesses in that window). The observations that would tell David the threat is rising: (1) Celonis bundling CCM or Orchestration Engine into **Make** (its own SMB automation brand) with prebuilt vertical templates; (2) Celonis publishing agent-certification features — pass/fail thresholds or graduation per case type — in the Orchestration Engine or Agent Miner; (3) a dental PMS vendor or DSO-scale group (e.g. Henry Schein One, Heartland, Aspen) licensing Celonis. The higher-probability threat remains the one the SAP case demonstrates: a dental practice-software vendor tightening data access while launching its own AI front office.

## Sources

1. Celonis press release, "Celonis Launches the Context Model to Eliminate Enterprise AI's Operational Blind Spots, Agrees to Acquire AI Decision Intelligence Leader Ikigai Labs" (12 May 2026) — https://www.celonis.com/news/press/celonis-launches-the-context-model-to-eliminate-enterprise-ais-operational-blind-spots-agrees-to-acquire-ai-decision-intelligence-leader-ikigai-labs ; also https://www.businesswire.com/news/home/20260512279732/en/
2. Constellation Research, "Celonis acquires Ikigai Labs, launches Context Model, eyes simulation-based AI models" — https://www.constellationr.com/insights/news/celonis-acquires-ikigai-labs-launches-context-model-eyes-simulation-based-ai-models ; itbrief, https://itbrief.news/story/celonis-launches-context-model-in-ikigai-labs-deal
3. Celonis, "Celonis AgentC: Making AI Agents Work for the Enterprise with Process Intelligence" — https://www.celonis.com/news/press/celonis-agentc-making-ai-agents-work-for-the-enterprise-with-process-intelligence
4. Celonis, "Celonis enables agents in Microsoft Copilot Studio" — https://www.celonis.com/news/article/celonis-enables-agents-in-microsoft-copilot-studio-autonomous-ai-agents-powered-by-process-intelligence
5. Cloud Wars, "How the Launch of AgentC Could Propel Celonis into the Ranks of Critical GenAI Enabler" — https://cloudwars.com/ai/how-the-launch-of-agentc-could-propel-celonis-into-the-ranks-of-critical-genai-enabler/
6. Celonis developer docs, "Custom Celonis MCP Server at Microsoft Copilot Studio" — https://developer.celonis.com/mcp-server-asset/integrations/custom-mcp-server
7. Business Wire, Celosphere 2025 platform announcements (4 Nov 2025) — https://www.businesswire.com/news/home/20251104046489/en ; iTWire, https://itwire.com/business-it-news/data/celonis-unveils-ai-driven-platform-innovations-at-celosphere-2025.html
8. Celonis Community, "Celosphere 2025 Product Highlights: Data Core and Orchestration Engine" — https://community.celonis.com/product-updates/celosphere-2025-product-highlights-data-core-and-orchestration-engine-5901
9. Celonis SE v. SAP SE complaint, N.D. Cal. 3:25-cv-02519 — https://regmedia.co.uk/2025/03/17/3-25-cv-02519.pdf
10. CourtListener docket — https://www.courtlistener.com/docket/69736382/celonis-se-v-sap-se/
11. MLex, "SAP says Celonis's refusal-to-deal claim fails in US antitrust dispute" — https://www.mlex.com/mlex/antitrust/articles/2333918/sap-says-celonis-s-refusal-to-deal-claim-fails-in-us-antitrust-dispute
12. Celonis, "Legal Update: SAP Agrees to Not Interfere with Celonis Extractor in Antitrust Litigation" — https://www.celonis.com/news/press/legal-update-sap-agrees-to-not-interfere-with-celonis-extractor-in-antitrust-litigation
13. Techzine, "SAP and Celonis enter stipulation while litigation continues" — https://www.techzine.eu/news/applications/132059/sap-and-celonis-enter-stipulation-while-litigation-continues/ ; Daily Journal, https://www.dailyjournal.com/article/386016-sap-won-t-impede-celonis-access-to-client-data-pending-trial
14. Licenseware wiki, "Celonis SE v. SAP SE" (secondary, unverified) — https://wiki.licenseware.io/wiki/celonis-v-sap/
15. Bundeskartellamt press release, "Bundeskartellamt concludes preliminary investigation into SAP" (30 July 2026) — https://www.bundeskartellamt.de/SharedDocs/Meldung/EN/Pressemitteilungen/2026/07_30_2026_SAP_Celonis.html
16. Bundeskartellamt case summary B7-1/25/15 — https://www.bundeskartellamt.de/SharedDocs/Entscheidung/EN/Fallberichte/Missbrauchsaufsicht/2026/B7-1-25-15.pdf?__blob=publicationFile&v=6
17. Heise, "Setback for Celonis: Cartel Office opens no abuse proceedings against SAP" — https://www.heise.de/en/news/Setback-for-Celonis-Cartel-Office-opens-no-abuse-proceedings-against-SAP-11389600.html ; CIO, https://www.cio.com/article/4204442/sap-dodges-german-antitrust-investigation-over-data-extraction.html
18. VentureBeat, "Inside Celosphere 2025: Why there's no 'enterprise AI' without process intelligence" — https://venturebeat.com/ai/inside-celosphere-2025-why-theres-no-enterprise-ai-without-process
