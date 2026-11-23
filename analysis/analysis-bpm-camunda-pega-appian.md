# Analysis: BPM / agentic process orchestration (Camunda, Pega, Appian; Temporal and Orkes briefly)

These vendors already ship Cyclical's core frame: a business process is a graph in which a "user task" (a person) and a "service task" (code, now an AI agent) occupy steps interchangeably, and in 2025–26 all three turned that into "agentic orchestration". **Overlap: 4/10.** They match A1 almost exactly and partly match A2 (process mining), but none grades steps against real-world outcomes, graduates automation on a statistical threshold, or pools outcomes across customers. All three promise enterprise buyers the opposite of pooling: "your data never trains our models". The most important lesson from 25 years of BPM is that **a hand-authored graph drifts away from reality as soon as it is drawn, and in a small business, where one process runs a few hundred times a year, it never paid back the cost of drawing it.** Cyclical survives where BPM failed only if the graph is derived continuously from logs, never authored, and the payback comes from the pool, not from the single business.

*Research caveat:* the shared web-search budget ran out partway through, and direct page fetches to pega.com, docs.camunda.io, fool.com and holisticon.de were blocked by this session's network policy. The 2026 figures below come from search-result extracts of earnings coverage and docs. Points marked "(from memory)" come from my prior knowledge and were not re-verified. I put roughly a 15% chance on any single "(from memory)" detail being wrong in its specifics, such as a date or an acquisition name, though the overall picture should hold.

## What it actually is

**Camunda** (Berlin; started in 2008 as a BPM consultancy, open-sourced the Camunda BPM engine in 2013, and rewrote it as the cloud-native Zeebe engine for Camunda 8 in 2022, from memory). It sells to developers inside large enterprises such as banks and insurers. Its last large round was roughly a $100M Series B led by Insight Partners in 2021 (from memory). It moved from open source toward a commercial license: Camunda 8.6 (late 2024) required a paid license to run the self-managed engine in production, and Camunda 7 Community Edition reached end of life in 2025 (from memory). Both changes drew community backlash.

Its agentic product shipped in **8.8 (Oct 2025)**. An AI agent is modeled as a BPMN **ad-hoc sub-process**: a container whose inner activities have no fixed order. "Each BPMN element inside an ad-hoc sub-process is a tool exposed to the LLM. The element's ID is used as the tool name, and its Documentation field is used as the tool description" [1][2]. The LLM picks which activities to run, "Camunda activates the corresponding BPMN activity", and the results loop back until the model returns a final answer. Camunda calls this a "governed toolbox": the LLM chooses a path, but only from the options the model allows [1][3]. Because a user task can sit inside the toolbox, **an agent can call a human as one of its tools**, which inverts A1. A January 2026 post shows local LLMs plugged in through Camunda Run [4]. Two documented limits: "you can't use Test mode" with ad-hoc sub-processes, and they support only non-interrupting event sub-processes [1]. Camunda's analytics product, Optimize, reports heatmaps and KPIs, but only on process instances that Camunda's own engine executed (from memory). It does not mine email or calendars.

**Pegasystems** (Cambridge, MA; founded 1983; public). It sells case management and real-time decisioning to banks, insurers, telcos and governments. **Total ACV (annual contract value: the yearly value of active contracts) was $1.66B in Q3 2026, up 7% in constant currency; Pega Cloud ACV grew 20% and is 59% of the total** [5]. The 2026 products are:
- **GenAI Blueprint** (launched 2024): turns a text description, or uploaded documents and screens from a legacy app, into a Pega application with case types, stages, steps, data model and personas. It draws on Pega's library of industry templates (from memory for the mechanism). A "vibe coding" upgrade on 5 Mar 2026 lets a completed blueprint be pushed straight into a Pega Platform environment [6].
- **Agentic Process Fabric** (announced mid-2025, generally available in Q3 2025): a registry and coordination layer for agents, workflows and systems, including non-Pega ones, with MCP/A2A support and audit trails [7].
- **Customer Decision Hub and adaptive models** (long-standing): Bayesian models that learn online from whether an offer or action was accepted (from memory).
- **Pega Process Mining** (from memory: added in 2023 through an acquisition).

Trefler's thesis is "workflows first, prompts second": workflows "define what AI agents can access and do, rather than allowing agents to independently reason through each step" [8][9].

**Appian** (McLean, VA; founded 1999; IPO 2017; revenue roughly $600–700M, from memory). It sells low-code process automation to the US federal government, financial services and insurance. **Process HQ** (2024) combines process mining, built on the Lana Labs acquisition of 2021, with Appian's data fabric. Process mining is available only on the Advanced and Premium tiers, not Standard, and process analysis is not available on Appian Government Cloud [10][11]. The standalone Process Mining 5.0 module was deprecated with 24.2 [12]. **Agent Studio** is Appian's agent builder; one third-party source dates its GA to November 2025, and the 26.3 release groups Composer, Agent Studio, DocCenter and AI Copilot with Process HQ as the "intelligence layer" [11]. A vendor-adjacent write-up says 26.3 "attributes business outcomes to specific AI agents and skills" [11]. That is the closest any of the three comes to A5, and I could not verify the mechanism. Appian names itself a Leader and Star Performer in Everest's 2026 Process Mining PEAK Matrix (vendor claim) [13]. Appian's long-running trade-secret suit against Pega is still producing costs at Pega: legal fees rose 180% year over year to $17.9M in Q2 2026 [14].

**Temporal and Orkes** (brief). These are code-first "durable execution" engines: a workflow is ordinary code whose state survives crashes. They are now marketed as the runtime underneath AI agents. Temporal raised a large Series C in 2025, and OpenAI-style agent stacks use it (from memory). Orkes commercializes Netflix Conductor. A human is a "signal" or "wait" in code, not a node in a business graph. Neither attempts observation, grading or pooling. **They are infrastructure Cyclical could run on, not competitors.**

## Loop comparison

| Aspect | Incumbent approach | vs Cyclical |
|---|---|---|
| A1 Core frame | BPMN graph; user task (human) and service task (automation or agent) are interchangeable step types. Camunda's ad-hoc sub-process lets an agent call humans as tools. Pega's case types (stages → steps) assign each step to a person, an automation or an agent. | **Same** (more mature, and they have 20 years of execution semantics: timers, escalations, compensation) |
| A2 Observation | Two halves. The graph is **authored** (by an analyst, or generated by Blueprint or Camunda Copilot from text and documents). Process mining (Appian Process HQ / Lana; Pega Process Mining; Camunda Optimize on its own engine only) reads ERP/CRM event logs, mainly to analyze and only secondarily to re-derive the graph. Nobody mines email or calendars. | **Different / Worse.** Discovery is an analysis project, not continuous onboarding. Conformance checking (model vs log) is the closest analogue to "missing edge" flags. |
| A3 UX | A modeler (orchestrator view) plus a **task inbox / worklist portal** for workers (Camunda Tasklist, Pega worklists, Appian Tempo/sites). Workers must move into the vendor's UI. | **Worse.** This is exactly the "new tool with 5 buttons" Cyclical avoids. |
| A4 Permissions | Role/group-based task assignment (swimlanes), Pega access groups and attribute-based access, Fabric governance and audit. The agent can only call tools placed inside its sub-process, a structural boundary rather than a persuasive one. | **Same on "rules not wording"** (they state it as their core pitch). **Absent** on just-in-time node-to-node grants, frequency → edge proposals, and pruning unused permissions. |
| A5 Shadow eval vs outcomes | None found for agents. Pega's adaptive models learn from response outcomes, but for marketing and next-best-action decisions, not for grading a human against an agent. Appian 26.3 "outcome attribution to agents" (unverified). | **Absent** (Pega partial, in an adjacent domain) |
| A6 Checkoff + seeded errors | A human-approval user task is a standard pattern. No seeded known-bad items and no checker-quality scoring found. | **Absent** |
| A7 Statistical graduation per case type | None. Autonomy is a design-time choice: the modeler decides whether a step is a user task or an agent. Process versioning exists, but nothing triggers recertification on a model swap. | **Absent** |
| A8 Replacement levels | Pega inverts it: **compile to deterministic workflow first, at design time** ("design-time AI"), and use run-time AI only at the edges. Blueprint templates act as a vendor-curated "general skill". | **Different** (deterministic before evidence, not after) |
| A9 Orchestrator agent | Blueprint and Camunda Copilot generate or modify process models on request. Process HQ and Pega mining surface bottlenecks and recommend changes to an analyst. No agent proposes "merge these 3 nodes" from eval data. | **Partial / Worse** |
| A10 Shared context | Case data model (Pega) / process variables (Camunda) / data fabric (Appian) shared across the steps of a case. | **Same** within a case. Appian's data fabric is broader. |
| A11 Cross-business pooling | **Explicitly refused.** Enterprise buyers demand "private AI". Cross-customer knowledge comes only through vendor templates and consultants, never outcomes. | **Absent (structurally)** |
| A12 Anti-Goodhart | SLA goals and deadlines per stage. Pega Decision Hub's arbitration combines propensity, value and business levers. | **Partial** |
| A13 Model-agnostic | Yes. Camunda connectors take any LLM, including local ones [4]. Pega and Appian are multi-provider. | **Same** |
| A14 Business & moat | Moat = installed enterprise base + systems-integrator ecosystem + certified developers + switching cost. Price floors in the tens to hundreds of thousands of dollars a year (from memory). No SMB motion. | **Different.** They never reached Cyclical's buyer. |

**A1 — they got the frame right two decades ago, and it was not enough.** BPMN 2.0 (2011) already treats "who does this step" as an attribute of the node. Swapping a person for a service was always meant to be a configuration change. The 2025–26 "agentic" releases add a third occupant type (an LLM loop) and let it choose among sibling steps. So the interchangeability Cyclical treats as its core frame is a solved modeling problem. **The frame alone is not differentiating. What differentiates is what decides the occupant: a modeler's guess (BPM) or outcome evidence (Cyclical).**

**A2 — the drift problem is the field's oldest bug.** BPM models drifted from reality in two places. First, the analyst's model diverged from the executable model; the "round-trip" between the business-analyst diagram and the engine model never worked well (from memory: Bruce Silver and others wrote about this for years). Second, the executable model diverged from what people actually did, because the work that mattered happened in email and spreadsheets outside the engine. The academic BPMN-Assistant paper states the mechanism: "the expertise required to modify process models often create[s] a bottleneck in implementing these changes, leading to a gap between actual business operations and their formal documentation" [15]. Another paper reports that business users find enterprise repositories "too complex and continue to use less disciplined tools" like Outlook and SharePoint [15][16]. Process mining (van der Aalst's field, commercialized by Celonis and later by Lana Labs → Appian) exists precisely because the drawn models were wrong. Its "conformance checking" measures how far the log departs from the model, as fitness and precision. This is what Cyclical's missing-edge flag should be built on, and the vocabulary and algorithms are mature. Note what process mining in these products reads: **ERP and CRM event tables in enterprises with data engineers**, not a 9-person clinic's inbox, calendar and practice software.

**A8 — Pega's "deterministic first" is the strongest counter-thesis to Cyclical's ordering.** Cyclical lets an agent do the work, then compiles to code once a simple rule reproduces its outputs (evidence → determinism). Pega has an LLM write the deterministic workflow at design time and keeps LLMs out of run-time steps unless necessary (determinism → evidence never collected) [8][9]. Pega's way is better for auditability and for regulated buyers who want predictability on day one. Cyclical's way is better when nobody knows the rules in advance, which is the small-business case: the process lives in the office manager's head. The two can combine. **Blueprint-style generation is a good way to seed the initial graph, which observation then corrects.**

## Where they're ahead of Cyclical

- **Execution semantics.** Durable state, timers, SLAs, escalations, compensation (undoing earlier steps), process versioning with in-flight migration, and audit trails good enough for banks. Cyclical will need all of this the day an agent occupies a node. Building it is wasteful; Camunda/Zeebe or Temporal can be embedded as the runtime.
- **Agent-boundary design.** Camunda's "governed toolbox" is a working, documented implementation of "an agent can only do what the graph allows" [1][3], which is half of Cyclical's A4 prompt-injection defense. The ad-hoc sub-process also handles cases with no fixed order, which is how a front desk actually works.
- **Process mining tooling.** Appian (Lana) and Pega have shipping discovery and conformance algorithms, and Everest rates Appian a Leader (vendor claim) [13].
- **Outcome-learning machinery in one domain.** Pega's adaptive models are production-grade online learners on real outcomes at bank scale (from memory). They are not applied to grading process steps, but they show the statistics are not the hard part.
- **Graph generation from documents.** Blueprint turns legacy screens and policy documents into a case model in minutes; one Q1 2026 client took two applications live in 92 and 70 days [17].

## Where they're doing it differently (and whether their way is better)

- **Authored vs observed graph.** Their way is better when a regulator wants a signed-off model *before* execution. It is worse for small businesses, which have no analyst to author the graph and no process stable enough to author one for.
- **Design-time vs evidence-time autonomy** (A7/A8). They decide up front which steps are automated. That is safer for a bank with one process run millions of times, where you can test before launch. It is wrong when volume per business is too low to test before launch, which is the case pooling is meant to fix.
- **Worklist UX** (A3). Their way is worse for adoption, and the field knows it. The recurring SMB complaint is that BPM requires "BPMN expertise, custom coding, and specialized consultants" [18].
- **Private AI vs pooling** (A11). Their way is necessary for their buyer, since banks will not pool. That is precisely why the pooled-outcome asset is open for a vertical-SMB player whose buyers already accept pooled back offices through DSOs.

## Feedback & reviews on these parts of the loop

*Limited by the search cap: I found fewer independent reviews than I wanted, and no G2 or Reddit pages could be fetched.*

**Adoption pain / why BPM never reached small businesses (independent and academic):**
- An empirical SME study: traditional BPM software is "complex, costly, and designed primarily for large organizations"; SMEs cite "complexity of BPM tools" and "lack of BPM education and motivation" [16].
- BPMN-Assistant (arXiv 2025): BPMN's "over-engineered nature and the prevalent lack of formal training among its users create substantial barriers to effective adoption" [15].
- An ARIS community critique: BPMN has redundant ways to express the same decision, making it "too complex for no reason" [19]. Netcall (a vendor) warns of "interpretational differences if someone is not a BPMN expert" [20].
- A 2013 paper quotes Olbrich that BPM "has failed to deliver" and argues that "a process model is not BPM" [21].
- Vendor-sourced (Kissflow, Tallyfy, both SMB workflow sellers with an axe to grind): BPM is "complete overkill for 90% of business processes" [18][22]. Analyst history (from memory): Gartner stopped publishing its iBPMS Magic Quadrant around 2019–2020 and folded the category into low-code application platforms. That was the analyst world conceding BPM was a feature, not a market.

**New agentic features (adoption evidence from earnings, the best independent signal available):**
- Pega ACV growth fell from 17% to 12% (Q1) to 7% (Q2 2026), and management blamed "unprecedented changes in the AI market" for clients delaying purchases. A bearish analyst summary calls it "AI Hype Hits Reality" [14][23].
- Q3 2026: "some clients slow to adopt the latest AI capabilities, necessitating a new forward-deployed engineering team" (Lighthouse) [24][25]. Management conceded ACV growth "did not reflect the opportunity we see in the market" [25]. Investing.com headlined Q3 as a miss [26]. Counterpoint (vendor): Infinity '26 adoption was twice the previous release's pace [5][27].
- **Read-through for Cyclical:** even buyers who already think in workflow graphs and already pay for the platform needed vendor engineers on site to put agents into production. Generating the graph (Blueprint) was not the bottleneck; trusting agents in the steps was. That is exactly the gap A5–A7 (graded shadow → checkoff → statistical graduation) are designed to close, and nobody in this cluster sells it.
- Camunda: a practitioner assessment (Holisticon, "what works today and what's coming tomorrow") and the docs' own limits (no Test mode for ad-hoc sub-processes; only non-interrupting event sub-processes) suggest the agent features are early [1][28]. I could not fetch the full text.

**Grading, graduation, pooling:** I found no review, doc or announcement in which any of the three grades agent steps against business outcomes, uses a statistical autonomy threshold, or pools across customers. Appian's "outcome attribution to agents" in 26.3 is the one claim to watch (vendor-adjacent, unverified) [11].

## Top-level: why they chose this path, and what to learn

**Starting asset and constraints.** Each started as software for large regulated enterprises, sold through systems integrators. A process ran thousands to millions of times *inside one customer*, so the vendor never needed data from other customers to reach statistical confidence: a bank's own claims volume suffices. That made "private AI" free for them to promise and impossible to walk back. Their unit of sale (six-figure platform licenses plus certified developers) also priced out any business without an IT department. BPM's graph was authored because enterprises had process-excellence teams paid to author it, and it drifted because no one was paid to keep it current once the consultants left. The 2025–26 agentic pivot follows from that asset base. If your installed base is governed, deterministic workflows, the natural thesis is "agents inside governed workflows" (Camunda's governed toolbox, Pega's workflows-first), not "agents that earn autonomy from evidence".

**What Cyclical is relative to them:** an **orthogonal superset on the learning loop and a subset on execution.** It shares A1 and A13, does A2 and A3 differently and more cheaply, and adds A5–A7, A11 and A12, which they lack. It lacks their execution engine, compliance tooling and enterprise channel. It is not a clone, because the asset differs: their asset is the model library and installed base; Cyclical's is cross-business outcome history.

**Copy:**
1. BPMN's node semantics for the internal representation: user/service/agent task, ad-hoc sub-process for unordered work, timers and escalations. Don't invent a new graph language.
2. Process mining's conformance-checking metrics (fitness, precision) as the formal definition of "missing edge".
3. Camunda's "governed toolbox" as the A4 baseline: an agent's tool list is exactly its node's edges.
4. Blueprint-style generation to seed a draft graph for a dental office from the practice-software schema and a 10-minute interview, which observation then corrects.
5. Embed an existing durable-execution engine (Zeebe, Temporal) rather than building one.

**Avoid:**
1. Authored graphs as the source of truth.
2. Worklist portals.
3. Design-time automation decisions.
4. The SI-led sales model.
5. Any promise of "no cross-customer learning" to dental buyers. Make pooling the explicit, contracted product, the way a DSO's shared billing office is.

**Exploit:** the agentic-BPM vendors cannot pool, cannot price below roughly $50k a year (from memory), and cannot see email or calendar. The small-business segment is structurally closed to them, as it was for BPM. Their 2026 trouble getting agents into production, even with willing enterprise buyers [24][25], suggests that the graduation machinery, not the graph, is the scarce part.

**Threat level: low in dental, moderate as an idea-space competitor.** The real threat in Cyclical's vertical remains the practice-software owner, who could license Camunda or Temporal as an engine for a weekend's work. Signals that the threat is rising:
- (a) Pega, Appian or Camunda launch a multi-tenant vertical SMB edition with **cross-tenant benchmarks**. The first benchmark dashboard ("your claim-denial rate vs peers") is the tell that they accept pooling.
- (b) Appian's agent outcome attribution grows into an autonomy threshold, i.e. auto-promoting an agent once its error rate is below X.
- (c) A dental or healthcare practice-software vendor (Henry Schein One, Patterson, Planet DDS) announces an OEM deal with Camunda, Temporal or Orkes.

## Sources
1. Camunda docs, AI Agent Sub-process connector / Build your first AI agent (search extracts): https://docs.camunda.io/docs/8.8/components/connectors/out-of-the-box-connectors/agentic-ai-aiagent-subprocess/ ; https://docs.camunda.io/docs/guides/getting-started-agentic-orchestration/
2. Camunda docs, AI agents: https://docs.camunda.io/docs/components/agentic-orchestration/ai-agents/
3. Camunda docs, Agentic orchestration design and architecture: https://docs.camunda.io/docs/8.8/components/agentic-orchestration/ao-design/
4. Camunda blog, Bringing Local LLMs to Camunda 8 (Jan 2026): https://camunda.com/blog/2026/01/use-local-llms-with-c8-run/
5. Futurum / Yahoo Finance coverage of Pega Q3 2026: https://finance.yahoo.com/markets/stocks/articles/pegasystems-inc-pega-q3-2026-090047364.html
6. Pega press release, Blueprint vibe coding (5 Mar 2026): https://www.pega.com/about/news/press-releases/pega-blueprint-updates-make-vibe-coding-enterprise-ready
7. Pega press release, Agentic Process Fabric: https://www.pega.com/about/news/press-releases/pega-agentic-process-fabric-reliably-orchestrates-end-end-ai-automation
8. Diginomica, "Pega's agentic approach puts workflows first, prompts second": https://diginomica.com/pegas-agentic-approach-puts-workflows-first-prompts-second-heres-why-matters-enterprise-ai-adoption
9. TechTarget, Pegasystems refines Blueprint agent builder (PegaWorld 2026): https://www.techtarget.com/enterprise-software/news/366643870/Pegasystems-refines-Blueprint-agent-builder-expands-marketing-tools
10. ERP Research, Appian Process Mining Review (2026): https://www.erpresearch.com/erp-add-ons/process-mining/appian-process-mining
11. Appianverse, Appian AI: Composer, Agent Studio, DocCenter & AI Copilot (search extract only): https://appianverse.com/blog/appian-ai-data-academy
12. Appian docs, Process Mining 5.0 (deprecation notice): https://docs.appian.com/suite/help/23.3/pm-5.0/process-mining.html
13. Appian, Everest Group Process Mining PEAK Matrix 2026 (vendor page): https://appian.com/resources/analyst-reports/everest-group-process-mining-products-peak-matrix
14. Finsee, Pega Q2 2026 earnings review: https://finsee.ai/earnings/pega/2026/q2/en/ ; https://x.com/Finsee_main/status/2079673499686223893
15. BPMN Assistant: An LLM-Based Approach to Business Process Modeling (arXiv 2509.24592): https://arxiv.org/pdf/2509.24592
16. From Theory to Practice: Empirical Insights on BPM Lifecycle Adoption and Low-Code Utilization in SMEs: https://www.researchgate.net/publication/393345159_From_Theory_to_Practice_Empirical_Insights_on_BPM_Lifecycle_Adoption_and_Low-Code_Utilization_in_SMEs
17. Pega Q1 2026 results (Business Wire via Morningstar): https://www.morningstar.com/news/business-wire/20260421891107/blueprint-ai-drives-pega-cloud-momentum-in-q1-2026 ; SEC exhibit: https://www.sec.gov/Archives/edgar/data/1013857/000101385726000025/q12026_ex-991.htm
18. Kissflow, What's Wrong with Traditional BPM Software (vendor): https://kissflow.com/workflow/bpm/whats-wrong-with-traditional-bpm-software/
19. ARIS Community, Criticizing BPMN: https://ariscommunity.com/users/sstein/2010-03-19-criticizing-bpmn
20. Netcall, Why BPMN May Not Work For Your Process Mapping Needs (vendor): https://www.netcall.com/blog/why-bpmn-may-not-work-for-your-process-mapping-needs/
21. Distributed Business Processes — A Framework for Modeling and Execution (arXiv 1309.3126): https://arxiv.org/pdf/1309.3126
22. Tallyfy, Best BPM software 2026 (vendor): https://tallyfy.com/best-bpm-software/
23. Futurum, Pegasystems Q1 FY2026: https://futurumgroup.com/insights/pegasystems-q1-fy-2026-cloud-acv-nears-1-billion-mark/
24. StockStory, PEGA Q3 deep dive: https://stockstory.org/us/stocks/nasdaq/pega/news/earnings-call/pega-q3-deep-dive-execution-challenges-persist-amid-ai-adoption-and-go-to-market-changes
25. Yahoo Finance, Pegasystems Q3 2026 Earnings Call Summary / Highlights: https://finance.yahoo.com/markets/stocks/articles/pegasystems-inc-q3-2026-earnings-123000295.html ; https://finance.yahoo.com/technology/ai/articles/pegasystems-q3-earnings-call-highlights-150421152.html
26. Investing.com, Pegasystems misses Q3 2026 estimates: https://uk.investing.com/news/stock-market-news/earnings-call-transcript-pegasystems-misses-q3-2026-estimates-as-stock-falls-premarket-93CH-4922849
27. Benzinga, Pegasystems Q3 2026 Earnings Call Transcript: https://www.benzinga.com/news/26/10/62494449/pegasystems-q3-2026-earnings-call-transcript
28. Holisticon, Agentic AI in Camunda 8: what works today and what's coming tomorrow (title and search extract only): https://www.holisticon.de/en/knowledge-hub/agentic-ai-in-camunda-8-what-works-today-and-what-s-coming-tomorrow
