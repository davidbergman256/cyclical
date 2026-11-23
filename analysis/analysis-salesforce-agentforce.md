# Analysis: Salesforce Agentforce

Agentforce is Salesforce's platform for building, testing and monitoring LLM agents that run inside its CRM, sold to mid-size and large enterprises as "digital labor" next to human staff. Overlap with Cyclical is **4/10**. It shares the frame of a mixed human-and-agent workforce, has a supervisor view over both, and has shipped the testing and observability plumbing. It does not grade agents against real-world outcomes, graduate them statistically, or pool outcomes across customers, and its trust promise to customers rules that pooling out. The lesson that matters most is that Salesforce, with every model and all the data it wants, retreated in 2025 from "let the LLM reason" to hand-written deterministic scripts (Agent Script) because its agents drifted and dropped instructions. That is Cyclical's level 3 ("compile to code") arrived at by pain rather than by measurement. Cyclical's edge is detecting *automatically* which steps can be compiled and proving it with outcomes. Salesforce does neither.

*Research note:* the shared web-search budget ran out partway through this analysis, and primary pages (salesforce.com, sec.gov, fool.com, reddit.com) were unreachable from this session's network. Figures from search results carry a source. Everything else is marked "(from memory)": it is my training knowledge up to mid-2026, which is probably right on the facts (~80%) but unverified here.

## What it actually is

**Product history.** Agentforce launched at Dreamforce in September 2024 and went GA in October 2024, priced at $2 per conversation, with the **Atlas Reasoning Engine** as the planner. Atlas classifies a user's request into a "topic", picks "actions" (Flows, Apex code, prompt templates, API calls) and loops until done (from memory). Releases since:

- **Agentforce 2.0** (Dec 2024): Slack deployment and more prebuilt skills (from memory).
- **Agentforce 3.0** (June 2025): **Command Center** for observability, native MCP support, and AgentExchange, a marketplace (from memory).
- **Agentforce 360** (Dreamforce, Oct 2025): renamed the whole stack. It added **Agent Script**, a deterministic scripting layer mixed with LLM reasoning ("hybrid reasoning"), the Agentforce Builder, Agentforce Voice, and Slack as the "front door". It also renamed Data Cloud to **Data 360** [9][11] (partly from memory).

Command Center has since been renamed **Agentforce Observability**, and Testing Center has been folded into **Agentforce Studio** [3].

**Testing Center / Studio testing** (vendor-described [3]):
- It generates synthetic test utterances.
- Conversation-level tests simulate a persona, such as a "frustrated customer", over several turns and score metrics such as task resolution.
- Custom evaluations are natural-language criteria with a pass/fail threshold, graded by an LLM judge whose reasoning and the agent's full execution trace are shown.
- Run history can be compared over time.
- A CLI integrates with DevOps Testing Center so a failed suite blocks deployment.

Everything here is graded on test scenarios before deployment. None of it is graded on what happened in the world afterwards.

**Observability** (formerly Command Center) tracks error rates, escalation frequency, latency and session traces covering inputs, reasoning steps, LLM calls and guardrail checks. It also sends real-time alerts and is pitched as managing "collaboration between humans and agents" [3]. It sits next to Service Cloud's Omni-Channel supervisor, which routes work and shows human and AI agents in one queue (from memory).

**Data 360 (ex-Data Cloud)** is the shared context. It harmonizes customer records from Salesforce and outside systems, uses "zero-copy" federation with Snowflake and Databricks, and since Nov 2025 includes Informatica, bought for about $8B [1][from memory]. Salesforce's "Agentforce + Data 360" ARR line includes roughly $1.1B from Informatica Cloud [1].

**Einstein Trust Layer** sits between agents and the LLMs (from memory):
- dynamic grounding in CRM data
- masking of personal data before prompts leave
- zero data retention agreements with OpenAI, Anthropic and other model providers
- toxicity scoring
- an audit trail

Agents run as a dedicated "agent user" with standard Salesforce profiles and permission sets, so access is role-based and standing (from memory).

**Pricing** has changed several times [4][5]:

| Model | Price | Notes |
|---|---|---|
| Per conversation (original) | $2 per conversation (£1.60 UK) | Can't be mixed with Flex Credits in the same org [4] |
| Flex Credits (May 2025) | $500 per 100k credits; 20 credits per action = $0.10 per action | Unused credits don't roll over [4] |
| Agentforce user license | $5/user/month | Requires Flex Credits [4] |
| Unmetered add-on | $125/user/month | [4] |
| Agentforce 1 / Max editions | from $550/user/month | Industries add-on $150 [4] |
| Agentic Enterprise License Agreement (AELA) | All-you-can-eat enterprise deal | Introduced late 2025 (from memory) |

Third-party reviewers say real cost is dominated by Data Cloud at $25–50 per user per month plus implementation. One competitor estimates year-one TCO at $270k–540k for a mid-size rollout (competitor claim) [5].

**Traction (vendor-reported, from earnings):**

| Quarter (fiscal) | Agentforce ARR | Other |
|---|---|---|
| Q3 FY26 (Oct 2025) | ~$540M, +330% Y/Y | 9,500+ paid deals, +50% Q/Q [1][2] |
| Q4 FY26 (Jan 2026) | ~$800M | 29,000 deals closed (paid and free) [1] |
| Q1 FY27 (Apr 2026) | $1.2B, +205% Y/Y | [2] |
| Q2 FY27 (Jul 2026, reported Aug 26, 2026) | >$1.5B, +240% Y/Y | **Definition changed**: now includes Slackbot and "Headless 360" [1][2] |

Q2 FY27 also reported:
- combined Agentforce + Data 360 ARR of ~$3.9B
- 3.2B "Agentic Work Units" in the quarter (+97% Q/Q), 7.0B to date
- more than 450 customers for Agentforce IT Service
- total revenue of $11.3B (+11% Y/Y) and FY27 guidance of $46.1–46.4B [2]

Q3 FY27 results were not out as of Nov 23, 2026 [2]. Salesforce says it will move to "milestone-based" reporting [2]. Combined with the definition change, that means the clean Agentforce-only growth rate is no longer published. On the Q2 run-rate, Agentforce is roughly 3% of revenue.

**Customer zero (Salesforce's own support).** Benioff said on the Logan Bartlett podcast in September 2025 that support headcount went "from 9,000 heads to about 5,000 because I need less heads". Salesforce's spokesperson said case volume fell and roles were simply not backfilled. Other claims from the same coverage [6]:
- agents handle about half of customer conversations
- CSAT is "about the same" for AI and human channels
- support costs are down 17% since early 2025

Salesforce has also cited 77% resolution across its first 50,000+ help-site conversations (vendor claim) [5]. **Verified:** the 9,000→5,000 figure is Benioff's own statement, widely reported. How the cut was attributed (fewer cases versus agent resolution) and whether CSAT held were not audited independently.

**Small business.** Salesforce sells Starter and Pro Suites to SMBs, and Agentforce features have been bundled into them with small credit allotments (from memory; ~60% confident on current packaging). Nothing found suggests a vertical or SMB-specific outcome loop. The SMB story is "the same agents, packaged smaller".

## Loop comparison

| Aspect | Agentforce's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | "Digital labor" workforce: agents and humans in one Omni-Channel queue and supervisor view. No explicit process graph. An agent is a set of topics and actions, not the occupant of a node in a business graph. | **Different** (closest in rhetoric, not in model) |
| A2 Observation / onboarding | Agents are configured by hand in Builder from topics, instructions and actions. Data 360 ingests systems but does not mine processes. Salesforce has no Celonis-style discovery; it partners with process-mining vendors (from memory). | **Absent** |
| A3 UX | Builder, Studio and Observability consoles for admins. Workers see agent output in Salesforce screens and Slack. Service Replies drafts for human reps are in-CRM (from memory). Workers must live in Salesforce. | **Different**: a new box, unless you already work in Salesforce |
| A4 Permissions | Standing role-based permission sets on an "agent user", plus Trust Layer masking and audit. No just-in-time grants, no rule-based agent-to-agent approvals, no frequency → grant or removal signal. ForcedLeak (2025) showed prompt injection via Web-to-Lead text (from memory). | **Worse** on JIT and injection; **better** on maturity of audit and compliance |
| A5 Shadow eval vs outcomes | Pre-deployment tests graded by an LLM judge on scenarios. Production metrics are deflection, escalation and CSAT. There is no shadow mode, no grading against outcomes (paid, showed up), and no outcome resolution of human–agent disagreements. | **Absent / worse** |
| A6 Checkoff | Human-in-the-loop via escalation topics and approval steps in Flows. No seeded known-bad outputs and no checker-quality discount. | **Worse** |
| A7 Graduation | Deployment gated by a test suite passing (CI). No statistical threshold on live outcomes, no per-case-type graduation. Model swaps are handled by re-running the test suite. | **Worse / different** |
| A8 Replacement levels | Prebuilt industry agents (≈ level 1) plus customer topics, instructions and RAG over knowledge (≈ level 2). **Agent Script** and deterministic Flows (≈ level 3), but written by people, not compiled from observed outputs. No level 4 merge logic. | **Same idea, worse mechanism** |
| A9 Orchestrator agent | Observability and "Agent Optimization" cluster sessions and flag failing intents for admins (from memory). There is no agent that proposes org redesign (merge roles, remove nodes). Builder can generate agents from natural language. | **Partial / worse** |
| A10 Shared context | Data 360: unified customer profile, zero-copy, Informatica. A mature, expensive, CRM-centric layer. | **Better** (deeper, but customer-centric rather than process-centric) |
| A11 Cross-business pooling | None of outcomes. The Trust Layer's zero-retention promise and "your data is not used to train" posture rule it out. Cross-customer learning is limited to Salesforce-built templates and research benchmarks (CRMArena-Pro). | **Absent**, and structurally blocked |
| A12 Anti-Goodhart | Custom evals plus guardrail checks on safety and topic scope. No pairing of task evals with business-level guardrails. Escalation-rate and deflection KPIs are exactly the ones that Goodhart. | **Absent** |
| A13 Model-agnosticism | Multi-model via the Trust Layer (OpenAI, Anthropic, Gemini, own xGen), "bring your own LLM" (from memory). Lock-in is to the Salesforce platform, not to a model. | **Same** at model level; **worse** at platform level |
| A14 Business model and moat | Moat is the system of record (CRM) plus distribution to ~150k customers. Priced per action, conversation, seat or AELA. Asset is customer data and workflow config, not outcome history. Target is enterprise, horizontal. | **Different** (Salesforce *is* the "system-of-record owner" risk, but in CRM, not dental) |

### A1: the frame is rhetoric, not a graph

Salesforce's "digital labor" language ("humans and agents working together") sounds like Cyclical's interchangeable-occupant frame. The implementation is a contact-center queue: Omni-Channel routes a case either to an AI agent or to a human. Observability shows both in one supervisor console, and escalation is a defined topic that passes the transcript to a human (from memory). There is no representation of the business as a graph of handoffs. The agent is defined by what the customer *says*, as Atlas classifies intent into topics, not by its position in a process. So Agentforce can tell you "this agent resolved 77% of help-site chats". It cannot tell you that the billing node and the scheduling node should merge.

### A5/A12: Agentforce grades on task evals and channel KPIs, not business outcomes

This is the central finding for the brief. Every eval surface Salesforce ships grades *the agent's behaviour*:

- Testing Center: synthetic scenarios, LLM-judge pass/fail, topic and action match, "task resolution" in a simulated conversation [3].
- Observability: error rate, escalation frequency, latency, guardrail trips [3].
- Business KPIs in public claims: deflection, resolution rate, CSAT, cost per case [5][6].

"Resolution" in Salesforce's usage means the chat ended without escalation, not that the customer's problem was fixed downstream. Nothing joins an agent's decision to a later real-world event, such as whether the renewal closed, the invoice got paid or the patient showed up, and uses it to grade or graduate the agent. Data 360 holds those outcomes, so the join is technically within reach. Salesforce simply hasn't built the loop. Deflection is the classic Goodhart metric: an agent that refuses to escalate scores better on it. The Salesforce help-site episode shows the failure mode. Salesforce removed search in favour of the agent, users called the agent "slow, inaccurate, and producing repetitive answers or even incorrect information", and search was restored [5].

### A6: handoff is escalation, not checkoff

Agentforce's human–agent handoff runs one way: agent first, human on escalation. Human approval exists as a Flow step for sensitive actions and through drafted replies for reps (from memory). Nothing addresses rubber-stamping, so there is no seeded-error audit and no weighting of approvers. Customers also complain that escalation is billed twice: "if every query gets escalated, now you're paying twice: once for Agentforce and again for a human" (competitor-quoted) [5]. Cyclical's "send = approve, edit = correct" in the user's own drafts folder is a cleaner design that Salesforce partly has inside its own UI.

### A8: Agent Script is the strongest validation of Cyclical's level 3

In late 2025, The Information reported, and several outlets repeated, that Salesforce executives had lost confidence in pure LLM reasoning [7]:

- SVP Sanjna Parulekar: "We all had more confidence in LLMs a year ago."
- Agentforce CTO Muralidhar Krishnaprasad: with more than eight instructions, models start omitting some.
- Salesforce's own studies found "drift", where agents lose the thread when users ask distracting questions.

The response was Agent Script, which pins the deterministic parts of a flow and leaves the LLM to handle intent and language. A spokesperson denied backtracking and said Salesforce is "more intentional" about where LLMs are used [7]. This is Cyclical's level 3 (compile to code when a rule reproduces outputs), with two differences:

1. **Salesforce asks a human admin to decide which parts are deterministic and write the script.** Cyclical proposes to *detect* it, for example "a simple rule reproduces 99.5% of outputs after 500 runs", and generate disposable code from contract and tests.
2. **Salesforce did it to stop failures. Cyclical does it to cut cost after success.** Salesforce's experience implies Cyclical should expect level 3 to be needed *earlier and more often* than its cost argument suggests: for reliability, not only price.

### A11: cross-customer learning is blocked by the trust posture

Salesforce's Trust Layer promises that customer data is not retained by model providers and not used to train shared models (from memory). That promise is a selling point to enterprise buyers and the reason Agentforce cannot pool outcomes across customers the way Cyclical proposes. The cross-customer learning Salesforce does have runs through people and research:

- prebuilt industry agents and templates
- Salesforce AI Research benchmarks such as CRMArena-Pro, which found leading LLM agents succeed on roughly 58% of single-turn CRM tasks and ~35% of multi-turn tasks (from memory)
- consulting partners carrying patterns between clients

Nothing found shows a pooled outcome dataset or cross-customer A/B testing. For Cyclical, the trap is that the buyer's default expectation, set by Salesforce, is "my data stays mine". Pooling has to be an explicit, contracted, de-identified opt-in (in dental, HIPAA de-identification plus a business associate agreement) with a visible payoff to the clinic.

## Where they're ahead of Cyclical

- **Shipped eval and observability tooling.** Simulated multi-turn persona tests, LLM-judge custom evals, execution traces, CI gating and production alerts all exist and are used by thousands of customers [3]. Cyclical should not rebuild these. They are commodity, and Cyclical's eval layer should sit on outcome data instead.
- **Shared context (A10).** Data 360 plus Informatica is a far deeper, better-governed context layer than a startup can build. For CRM-shaped businesses it is the default.
- **Trust and audit (A4, partially).** The Trust Layer's masking, zero-retention contracts, audit trails and FedRAMP or HIPAA-ready offerings (from memory) are what enterprise buyers check first.
- **A real role-removal case study.** Salesforce's own support org cut from ~9,000 to ~5,000 without backfill, with claimed CSAT parity and 17% lower support cost [6]. It is the largest public instance of "remove a role" in the wild. It was done by attrition and executive judgement, not a randomized test, which is precisely the gap Cyclical's pooled experiments target.
- **Distribution and revenue.** More than $1.5B ARR (redefined) and tens of thousands of deals in two years [1][2].

## Where they're doing it differently (and whether their way is better)

- **Agent-first with human escalation, vs Cyclical's human-first with agent graduation.** Salesforce puts the agent in front of customers on day one and measures deflection. Cyclical shadows the human and graduates case types on evidence. Salesforce's way gets revenue and volume faster. The help-site revolt [5] and the Valoir finding that over three-quarters of B2B pilots stalled before go-live (secondary-reported) [5] suggest it also burns trust. For small businesses, where one bad patient interaction is visible, Cyclical's slower path is the better fit.
- **Hand-authored determinism vs measured determinism.** Discussed under A8. Salesforce's way is better *today*, because admins know their rules. Cyclical's way is only better if its rule-extraction actually works at small-business volume, which is an open risk.
- **Pricing per action vs a share of salary.** Salesforce charges $0.10 per action or $2 per conversation, and customers complain about unpredictability [5]. Cyclical's realizations imply pricing against roughly $180k of replaced salary, with ~$5–10k compute. The lesson is to price on a predictable unit tied to the outcome, such as per clinic per month or per graduated role, never per action.
- **Horizontal platform vs one vertical.** Salesforce's breadth prevents it from knowing what "a good outcome" is per process. Cyclical's single vertical is what makes outcome grading possible.

## Feedback & reviews on these parts of the loop

**Reliability (A5, A7, A8)**
- Salesforce's own executives on LLM unreliability: instruction dropping above eight instructions, drift, and "we all had more confidence in LLMs a year ago" [7]. *Independent reporting of vendor-internal views.*
- The help.salesforce.com agent drew a community backlash ("slow, inaccurate… repetitive answers or even incorrect information"), and search was restored [5]. *Independent, via review aggregator.*
- G2 reviewer: Agentforce "depends heavily on clean data to perform well" [5]. *Independent user.*
- A Valoir study found more than three-quarters of B2B Agentforce pilots stalled before go-live, mostly on data quality [5]. *Analyst, secondary report; not checked against the primary.*
- The Register's coverage of the 4,000 job cuts noted that "doubts over reliability linger" [6]. *Independent press.*

**Cost and pricing (A14)**
- The dominant complaint is unpredictability rather than the headline rate. Data Cloud adds $25–50 per user per month, and escalations are "paying twice" [5]. *Mixed: review aggregators, several of them competitors (11x, YourGPT, Berrydesk), so discount.*
- Gartner Peer Insights reviewers call the per-license cost high [5]. *Independent.*

**Ratings**
- G2: 4.3/5 from 1,694 reviews [5]. *Independent-ish (G2 reviews are often vendor-solicited).*

**Adoption skepticism (A14)**
- The ARR definition changed in Q2 FY27 to include Slackbot and Headless 360, and reporting is moving to "milestone-based" [2]. Analysts flag that the combined Agentforce + Data 360 number includes about $1.1B of acquired Informatica revenue [1][2]. *Independent analysts (Futurum, Yahoo Finance coverage).*
- Gartner forecast (June 2025) that over 40% of agentic AI projects will be cancelled by end-2027 on cost and unclear value (from memory). *Independent, not Agentforce-specific.*

**Permissions (A4)**
- "ForcedLeak" (Noma Security, Sept 2025) was an indirect prompt injection planted in a Web-to-Lead form field. When an employee later asked Agentforce about the lead, the agent followed the hidden instructions and exfiltrated CRM data to an expired, still-whitelisted domain. It was rated CVSS 9.4, and Salesforce patched it with Trusted URL enforcement (from memory). This is the exact attack Cyclical's "rules, not wording" approval principle is designed against. *Independent security research.*
- The Salesloft-Drift OAuth token theft (Aug 2025) exposed data in hundreds of Salesforce orgs through a connected app's standing credentials (from memory). It argues for Cyclical's temporary, logged grants over standing ones. *Independent.*

**Human–agent handoff and role removal (A1, A6)**
- Benioff: "I've reduced it from 9,000 heads to about 5,000 because I need less heads" [6]. *Vendor CEO.* CX Today and NBC coverage pressed on whether quality held, and the only answer was Benioff's CSAT-parity claim [6]. *Independent press, vendor data.*

Reddit (r/salesforce) threads could not be retrieved in this session. Reddit was blocked and search returned none, so practitioner sentiment there is unrepresented here.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraints.** Salesforce owns the system of record for customer data at ~150k companies, a huge partner and consulting channel, and a seat-based revenue model under pressure from the "SaaSpocalypse" fear that agents shrink seat counts [1]. Each choice follows from that:

- **Agents inside the CRM, with the CRM as the context layer.** This keeps Data 360 sticky and monetizes it.
- **Horizontal and configurable rather than outcome-specific.** One platform has to serve every industry, so it ships tools (Builder, Testing Center) and lets customers and partners define "good".
- **Trust Layer, no cross-customer data use.** Enterprise buyers demand it, and Salesforce's brand is "Trust is our #1 value". This forecloses outcome pooling.
- **Consumption pricing, then AELA.** These replace the seat revenue agents eat. Deflection and "agentic work units" are the metrics that justify the bill, so those are what Observability measures.
- **Agent Script.** Enterprise buyers needed reliability more than autonomy, and a hand-scripted path is something a partner can sell and support.

**Copy.**
- Use the shipped eval mechanics (persona simulation, LLM-judge custom evals, traces, CI gating) as commodity infrastructure. Cyclical's differentiation is what those evals are graded *against*, not the eval harness.
- Treat a deterministic layer as necessary early: Salesforce's own CTO found instruction-following breaks at around eight instructions [7].
- Present the human and agent supervisor view as one queue. Salesforce validated that managers want this.

**Avoid.**
- Grading on deflection or resolution. They are Goodhart-prone and produced the help-site backlash.
- Per-action pricing that customers can't forecast.
- Putting agents customer-facing before graduation.
- Standing agent permissions: ForcedLeak is the cautionary tale.

**Exploit.**
1. Salesforce cannot pool outcomes across customers without breaking its trust promise. Cyclical can make pooling the product, with consent and de-identification, in one vertical.
2. Salesforce has no process-mining onboarding. Agents are built by hand, which is why pilots stall [5]. Cyclical reads event logs.
3. Salesforce is not in dental practice management, and its SMB offer is a shrunk enterprise product. The dental system-of-record owners (Dentrix/Henry Schein One, Open Dental, Curve, Denticon) are the relevant "Salesforce" in Cyclical's world. Watch them for an Agentforce-style move.

**Is Cyclical a clone, subset, superset or orthogonal?** Cyclical is a **superset on the eval loop (A5–A9, A11–A12) and a subset on infrastructure (A10, A13, eval tooling)**. It is orthogonal in market: one SMB vertical versus horizontal enterprise. Shared rhetoric ("digital labor", "humans and agents together") will make buyers and investors file Cyclical as "Agentforce for dentists". The pitch has to lead with outcome grading and pooled evidence, which Agentforce visibly lacks.

**Threat level: low-medium** (~15% that Salesforce competes directly in dental within 3 years). The threat rises if any of these appears:

- Agentforce Observability starts grading agents on **downstream business outcomes joined from Data 360**, such as "agent decisions correlated with renewal or payment".
- Salesforce ships **opt-in cross-customer benchmarking** ("how your agent compares to peers in your industry").
- Salesforce launches a **healthcare-SMB or dental** Agentforce package via Health Cloud.

The first is the single observation that would tell David the threat is rising: Salesforce owns the outcome data and the join is easy.

## Sources

1. Yahoo Finance / SalesforceBen / Constellation coverage of Agentforce ARR and Q3 FY26–Q2 FY27 results: https://finance.yahoo.com/technology/ai/articles/agentforce-arr-hits-1-5b-142700697.html ; https://www.salesforceben.com/huge-agentforce-growth-in-salesforce-q4-as-benioff-mocks-saaspocalypse-narratives/ ; https://www.constellationr.com/insights/news/salesforce-delivers-strong-q3-agentforce-data-360-surge ; https://finance.yahoo.com/technology/ai/articles/salesforce-crm-grew-agentforce-data-163207657.html
2. Salesforce Q2 FY27 results (Aug 26, 2026) and analysis: https://investor.salesforce.com/news/news-details/2026/Salesforce-Delivers-Record-Second-Quarter-Fiscal-2027-Results/default.aspx ; https://futurumgroup.com/insights/salesforce-q2-fy-2027-can-agentforce-drive-revenue-reacceleration/ ; https://www.fool.com/earnings/call-transcripts/2026/08/31/salesforce-crm-q2-2027-earnings-call-transcript/ ; https://www.sec.gov/Archives/edgar/data/0001108524/000110852426000187/crm-q2fy27xexhibit991.htm
3. Salesforce blog, Agentforce Testing Center and Command Center / Observability (vendor): https://www.salesforce.com/blog/agentforce-testing-center/ ; https://www.salesforce.com/blog/command-center/
4. Agentforce pricing pages and Flex Credits blog (vendor): https://www.salesforce.com/agentforce/pricing/ ; https://www.salesforce.com/au/blog/flex-credits/ ; https://www.salesforce.com/uk/agentforce/pricing/
5. Reviews and complaints aggregation: https://www.oliv.ai/blog/salesforce-agentforce-reviews-analyzed ; https://www.gartner.com/reviews/product/agentforce-service ; https://www.getmacha.com/blog/agentforce-pricing-explained ; https://www.11x.ai/guides/agentforce-review ; https://www.getclientell.com/salesforce-blogs/what-salesforce-admins-are-saying-about-agentforce-2026
6. Support headcount 9,000→5,000: https://fortune.com/2025/09/02/salesforce-ceo-billionaire-marc-benioff-ai-agents-jobs-layoffs-customer-service-sales/ ; https://www.theregister.com/2025/09/02/salesforce_4000_jobs_ai ; https://www.nbcnews.com/business/business-news/salesforce-ceo-confirms-4000-layoffs-need-less-heads-ai-rcna228703 ; https://cxtoday.com/salesforce-ceo-pressed-on-cutting-4000-customer-support-reps
7. Declining LLM trust and the Agent Script pivot: https://the-decoder.com/salesforce-executives-signal-declining-trust-in-large-language-models/ ; https://windowsreport.com/salesforce-moves-away-from-llm-use-over-enterprise-ai-reliability-concerns/ ; https://paddo.dev/blog/when-ai-isnt-fit-for-purpose/
8. TechCrunch on Agentforce as "digital labor" and hallucination claims: https://techcrunch.com/2024/12/04/llms-may-have-a-killer-enterprise-app-digital-labor-at-least-if-salesforce-agentforce-is-any-indicator
9. Agentforce 360 launch release (Oct 13, 2025): https://markets.financialcontent.com/clarkebroadcasting.mymotherlode/article/bizwire-2025-10-13-welcome-to-the-agentic-enterprise-with-agentforce-360-salesforce-elevates-human-potential-in-the-age-of-ai
10. Agentforce launch (Sept 12, 2024): https://www.businesswire.com/news/home/20240912708121/en/Salesforce-Unveils-AgentforceWhat-AI-Was-Meant-to-Be
11. Items marked "(from memory)" — ForcedLeak/Noma Security, Salesloft-Drift breach, CRMArena-Pro, Gartner 40% cancellation forecast, Agentforce 2.0/3.0 contents, Informatica close, Trust Layer details, AELA — were not re-verified in this session because the search budget ran out and primary hosts were blocked.
