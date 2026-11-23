# Analysis: Workday (Agent System of Record, Illuminate/Sana agents, Paradox, Flowise, C1.ai)

Workday is extending its HR system of record so that agents become rows in the same table as employees. Each agent gets an identity, a security group, an owner, an on/off state, an audit trail and a cost line. Overlap with Cyclical: **4/10**. Workday shares the "agent as worker" frame (A1) and builds lifecycle and permission governance (A4, part of A7). It measures agents by consumption and vendor-reported productivity, not by real-world outcomes graded against a human doing the same work. It also sells to enterprises with thousands of employees, not to 9-person clinics. The most important lesson: the permission layer Cyclical designed in A4 (just-in-time grants, logged requests, revoking unused access) is the ConductorOne product, which Workday agreed to buy in October 2026. A4 is about to be a commodity governance feature, not a moat. Cyclical's differentiator has to be outcome-graded evaluation plus cross-business pooling, and Workday shows no sign of building either.

*Method note: primary Workday pages (blog.workday.com, doc.workday.com) and several analyst blogs could not be fetched from this session, and the shared search budget ran out mid-research. Facts below come from search-result extracts of those pages, SEC filings and press, or are marked "(from memory)". Roughly 20% of the specific mechanism claims are second-hand.*

## What it actually is

**Workday** sells HR (HCM, human capital management) and finance software to large organisations: 11,000+ customers, and Gartner has rated it a Leader in Cloud HCM for ten consecutive years [9]. It was on track for about $10B revenue in FY2026 [12]. Q3 FY2027 subscription guidance is ~$2.515B per quarter, +12% [5]. Core HCM is priced per employee, which matters for the strategy section below.

**Agent System of Record (ASOR).** Announced February 2025, generally available around February 2026, with broader tier rollout by May 2026 [1][2][3]. Workday describes it as one control centre to "find, register, configure, monitor, manage and audit" agents, both Workday-built and third-party [1][4]. Concretely:
- Each agent gets an **Agent System User (ASU)**, a unique identity for authentication, authorisation and audit, plus an auto-created **Agent Security Group (ASG)** [4][6].
- Agents run in two modes [6][7]. In **Delegate** mode the agent inherits the permissions of the person invoking it. In **Ambient** mode (background jobs, scheduled and autonomous work) it acts under its own ASU and ASG.
- Being allowed to invoke a skill does not grant the underlying data. Data access comes from domain and business-process security policies [6].
- The admin guide (as excerpted) says only **unconstrained** security groups can currently be configured on ASOR policies [6]. In Workday terms, an unconstrained group's access isn't scoped by organisation: an ambient agent sees the whole domain, not "the Boston clinic's data".
- An AI Agent Security report gives an agent-user audit view [6]. Workday-side logs don't cover external orchestrators or model providers [6][7].
- The February 2025 launch bullets were "onboard agents, define roles and responsibilities, track impact, budget and forecast costs, support compliance, foster continuous improvement" (from memory; matches the CIO.com framing "manage AI agents like employees" [8]).
- The GA scope was registration, configuration, activation, ASUs, audit trails and API registration of external agents. Agent owners, role-based security and Microsoft/A2A integration were slated for June 2026 [3, via search extract]. Whether those shipped is unverified.
- Price: no extra SKU; ASOR is included in the core subscription [4].

**Illuminate agents (now orchestrated by Sana).** The launch set (Sept 2024 to June 2025) was Recruiting, Talent Mobility, Payroll, Policy, Contracts, Financial Audit, Self-Service and **Business Process (BP) Optimize** [10][11]. BP Optimize matters most for Cyclical. It reads Workday's own business-process event data, analyses execution times and anomalous patterns over a rolling 18-month window, and recommends configuration changes. It excludes integration loads and web-service transactions and supports English only [13]. That is process mining confined to Workday's own event log.

**Rising, October 2026** [14][15][16]:
- **Sana** becomes the Workday home screen and the agent orchestration engine.
- **Autopilot** versions of the hiring, payroll, accounting and compliance agents; autopilot for Payroll, Accounting and Deployment reaches early adopters in early 2027.
- Agent-Ready Tools, Agent Harness, Custom Agents, Developer Agent and Workday Data Cloud reach GA.
- HR and finance data opened to outside agents through MCP (Model Context Protocol, the open standard for connecting agents to data and tools); Sana available inside Claude (early access).
- Definitive agreement to acquire **C1.ai** (formerly ConductorOne, agentic identity governance), expected to close by January 2027 [17][18]. Bhusri's line: "An agent that's not grounded in business rules might move fast. But it is essentially lawless" [17].

**Acquisitions.**
- **HiredScore** and **Evisort** in 2024 (from memory).
- **Flowise**, an open-source low-code agent builder, August 2025; integration into Sana was described as planned, not shipped [15].
- **Paradox**, a conversational recruiting agent ("Olivia") for high-volume frontline hiring (McDonald's, CVS, Chipotle per third parties), signed August 2025 for $1.0B cash and closed October 1, 2025. The 10-K fair value is $1.1B including a prior $20M stake, and the deal is "not material" to results [19][20]. Olivia is now the "Workday Paradox Candidate Experience Agent".
- **Sana**, an AI-native learning platform plus no-code agent builder, ~$1.1B, closed November 4, 2025 [21].

**Agent Partner Network and Agent Gateway** (June 2025). Launch partners include Accenture, Adobe, AWS, Auditoria, Compa, Deloitte, Glean, Google Cloud, IBM, KPMG, Microsoft, Paradox, PwC and WorkBoardAI. By ASOR GA, 65+ partners were connecting agents via MCP and A2A, with OpenTelemetry alignment [22][1].

**Pricing: Flex Credits** (launched September 2025).
- Credits are charged per completed agent action from a rate card, e.g. Recruiting Agent resume match score = 6 credits; Payroll Q&A = 10 credits.
- Non-production testing is free.
- A Platform Consumption Console shows credit burn by agent and team and alerts at 80%, 90% and 100% of the subscription [23][24].
- The dollar price of a credit is not published [23][25].

**Adoption.**
- Q2 FY2027 (Aug 2026): the CFO said **5,500 customers use the organic agents** but only "a little over 200" had signed Flex Credits. Management: "AI adoption is currently running ahead of monetization" [5].
- A third-party summary puts AI ARR (annual recurring revenue from AI products) near **$600M, up >200% YoY**, and Sana monthly active users +190% [26] (unverified against filings).
- UC Today: **fewer than 900 customers purchased an agent** over the prior year, ~300 on Flex Credits by Q2 [27].
- Q3 FY2027 results land 24 November 2026, after this was written.

## Loop comparison

| Aspect | Workday's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | Agents are workforce entries (identity, role, security group, owner, cost) next to employees. Work is modelled as configurable business processes (steps, approvals, conditions) assigned to roles. Agents act inside those processes, but there's no explicit "this step can be held by a person or an agent, swap freely" abstraction. | **Different (partial overlap).** Same worker metaphor; the unit is the worker record, not the graph node. |
| A2 Observation | BP Optimize mines Workday's own business-process event log (18-month window) for bottlenecks [13]. Nothing reads email, calendar or outside tools to discover the real process. | **Worse / narrower.** Process mining, but only inside the system of record they own. |
| A3 UX | Sana is the new home screen: a conversational front door plus a "Concierge" agent [14][16]. Workers get a new primary UI. Agents surface inside Workday, Slack/Teams and Claude. | **Different.** The opposite of "near-zero new UI"; Workday wants to be where work starts. |
| A4 Permissions | Per-agent identity (ASU/ASG); Delegate vs Ambient modes; least-privilege guidance; unconstrained groups only; audit view [6][7]. C1.ai adds scoped access, human approvals, owners and lifecycle states for agents [17][18]. | **Same direction, more mature plumbing; missing rules-not-wording and frequency → missing-edge.** See below. |
| A5 Shadow eval | None found. Testing in non-production is free of credits [23], but nothing shows a mode where an agent runs alongside a human and both are graded by outcome. | **Absent.** |
| A6 Checkoff | Human-in-the-loop approvals are the default; autopilot is the exception. iTWire: Workday "wants you to stay in the loop" [16]. No seeded-error audits of approvers found. | **Worse.** Has approvals, no defence against rubber-stamping. |
| A7 Graduation | Activate/deactivate per agent in ASOR; assisted → autopilot per agent product, chosen by the vendor and admin [14][16]. No published statistical threshold, no per-case-type graduation, no automatic demotion on model swap. | **Worse.** Lifecycle states exist; the evidence rule for moving between them doesn't. |
| A8 Replacement levels | Pre-built vendor agents; custom agents via Sana/Flowise and the Developer Agent. No "compile to deterministic code when a rule reproduces outputs" loop. | **Different / mostly absent.** |
| A9 Orchestrator | BP Optimize recommends configuration changes to process owners [11][13]; Sana orchestrates agents at run time. Neither proposes merging roles or removing nodes. | **Partial.** Closest Workday piece to A9, but it targets cycle time, not org structure. |
| A10 Shared context | Workday Data Cloud plus the HR/finance system of record as grounding; Sana grounded in organisational data [14][21]. | **Better** for HR/finance context: they own the data. |
| A11 Cross-business pooling | Cross-tenant data is used to train Workday's models (opt-in data contribution, from memory). No pooled outcome experiments, no pooled exception desk. | **Different.** They pool for model training, not for outcome tests or role-removal experiments. |
| A12 Anti-Goodhart | None found beyond responsible-AI reviews. Diginomica criticised Workday for not foregrounding its own risk framework when showcasing higher-risk agents [28]. | **Absent.** |
| A13 Model-agnostic | Partners with several labs (Anthropic, Google, Microsoft); third-party agents from any vendor register via MCP/A2A [1][22]. Workday-built agents use models Workday picks. | **Same (as a registry); Different (for its own agents).** |
| A14 Business model and moat | Moat = system of record for people and money plus distribution to 11,000 large customers. Revenue = per-employee subscription plus Flex Credits per agent action. | **Different.** Their asset is the record; Cyclical's is the outcome history. |

**A1 in detail.** Workday's "agents are workers" is a governance frame, not an operations frame. An agent gets the HR primitives Workday already has: hire (register), role (security group), manager (owner), terminate (deactivate), payroll (Flex Credits). What's missing is the property Cyclical depends on: a slot of work that a person or an agent can occupy, with both scored on the same metric so the system can say which should hold it. Workday's business-process framework comes closest, since steps are assigned to roles and an agent's system user can be placed in a role. But nothing found shows Workday comparing who did that step better. Cyclical's node abstraction is a superset of Workday's worker record.

**A4 in detail.** This is where Workday is ahead in plumbing and where Cyclical should update its design.
- **Workday's Delegate vs Ambient split** answers a question Cyclical's spec doesn't ask: is the agent using the permissions of the human node it's helping, or its own? A stage-2 drafting agent (draft lands in the human's email) is Delegate; a graduated stage-3 agent is Ambient. Cyclical should adopt this split explicitly. Graduation then means a permission change from Delegate to Ambient, which the audit log can track.
- **C1.ai is the rest of A4.** ConductorOne's product (from memory) is just-in-time access requests routed to the resource owner, time-boxed grants, every request logged, periodic access reviews, and automatic revocation of unused access. Cyclical's "temporary, logged grants" and "unused permissions → proposed removal" are that product. Workday is buying it specifically to apply it to agents [17][18].
- **What neither has.** No evidence of the two parts of A4 that are genuinely Cyclical's:
  - approval decided only by (requester, data class, task type) and never by request wording, as a prompt-injection defence. ConductorOne-style approvals route to humans, so the wording does reach a person.
  - turning request frequency into a "missing edge" proposal that changes the process graph rather than the access list.
- **Unresolved A4 question (who answers for data in a system node).** Incumbents answer it bluntly. The system of record's security policy is the answer, and a named human "resource owner" or "agent owner" approves exceptions [6][17]. David finds a responsible human per system node inelegant; the whole identity-governance industry has settled on it. A more elegant Cyclical answer would be a rule table keyed on data class, with a human owner only as the fallback for requests the rules don't decide. It is worth knowing the market has accepted the special case.

**Performance measurement (A5–A7) in detail.** The task asked whether Workday measures agents on outcomes and whether it compares human and agent performance on the same role. On available evidence, **no to both** (≈80% confident; the June 2026 ASOR features and Rising 2026 Agent Harness weren't readable in detail).
- What Workday measures is (a) consumption: credits per agent and team, against budget [23][24]; and (b) vendor-reported productivity, such as "95% of frontline hiring automated" and "70% reduction in time-to-hire" for Paradox customers, which UC Today notes are not attributed to named customers [27].
- "Track impact" in the ASOR launch is a dashboard of usage and attributed impact, not an outcome-graded comparison.
- Workday has a structural reason not to grade hiring agents on downstream outcomes: *Mobley v. Workday*, an age-discrimination collective action over its AI screening, certified in May 2025 (from memory). Any metric that ranks candidates or workers by outcome is litigation-exposed in HR.

## Where they're ahead of Cyclical

- **Identity and lifecycle plumbing for agents, shipped and free.** ASU/ASG per agent, Delegate vs Ambient execution, audit view, activate/deactivate, an MCP/A2A gateway, and 65+ partners registering agents [1][4][6][22]. Cyclical would have to build all of this; Workday includes it in the base subscription.
- **Owning the system node.** For HR and finance data, Workday *is* the system node in Cyclical's unresolved A4 question, so it never has to negotiate access with itself. This is the "system-of-record owner builds it" risk from realizations.md §6, demonstrated in another vertical.
- **Distribution and capital.** 5,500 customers already using agents [5] and $2B+ spent on agent companies (Paradox, Sana, Flowise, C1) in about 14 months.
- **Pricing per action.** Flex Credits put a price on each agent action (6 credits per resume match) [23]. Cyclical will need the same unit to show a clinic its "agent bill vs salaries replaced" comparison.

## Where they're doing it differently (and whether their way is better)

- **Governance-first vs evidence-first.** Workday's gate for autonomy is policy: an admin activates an agent, assigns its security, and opts into autopilot. Cyclical's gate is statistical evidence per case type. Workday's way sells better to CISOs and auditors today; Gartner's First Take on C1 is about centralising identity authority, not agent accuracy [29]. Cyclical's way is the only one that can justify removing a role. For a small clinic with no CISO, evidence beats policy. In an enterprise, Cyclical would need both.
- **New front door vs invisible.** Sana replaces the Workday home screen. Cyclical refuses to add UI. Workday's choice follows from its position: it already owns a screen employees log into. Cyclical has no such screen, so its invisibility is both a constraint and the right call.
- **Process mining inside one system vs across tools.** BP Optimize sees only Workday business-process events and excludes integrations [13]. Clinic work spans the phone, email, the practice software and the payer portal, so a single-system miner would miss most of the graph. Cyclical's cross-tool event-log approach is the better design for small businesses.
- **Pooling for models vs pooling for outcomes.** Workday's multi-tenant data improves its models. Cyclical's pooling is for running experiments (A/B tests, role-removal randomisation), which needs outcome labels Workday doesn't collect for most processes.

## Feedback & reviews on these parts of the loop

**Adoption and monetisation (A14) — independent and earnings call:**
- CFO, Q2 FY2027: 5,500 customers using organic agents vs "a little over 200" on Flex Credits; "AI adoption is currently running ahead of monetization"; consumption pricing can delay revenue "by months or potentially a year" [5].
- UC Today: "fewer than 900 customers purchased an agent over the previous year." The strongest results came from Workday's existing scheduling suite, not the new agents [27].
- BERI on Rising 2026: Workday "sells agents on credits with no published price" [25].

**Governance and permissions (A4) — independent analysts:**
- Gartner First Take on C1.ai: CISOs should keep "independent controls" and not treat Workday as an IAM (identity and access management) replacement; consolidating agent governance inside Workday risks "excessive centralization of identity and access authority" [29].
- Forrester on Rising 2025 called the move to an "open AI orchestration platform" a high-risk bet. Managing mixed-vendor agents through ASOR "remains unproven at scale" [30].
- A third-party implementation guide notes that adding whole populations to interaction policies, or excessive ambient policies, "defeats least privilege" [6]. The unconstrained-groups-only limitation in the admin guide [6] means org-scoped agent access isn't yet possible.

**Measurement and claims (A5–A7, A12) — independent press:**
- UC Today questions the 95% frontline-automation and 70% time-to-hire figures because the customers behind them aren't named [27]. This is the only external probe of Workday's agent performance claims found; it challenges attribution, not method.
- Diginomica (Rising 2026): disappointment that Workday "does not emphasize" its responsible-AI risk framework when showing higher-risk agents [28]. Earlier customer panels said results "require organizational change": data quality, process and skills, not the agent alone [31].
- Gravity Fast (independent blog): ASOR is "the piece that matters most" because Workday is making claims about agents it doesn't sell. It notes Workday's own language drifting from "system of record" to "platform of agents" [32].

**Reviews:** No G2, Gartner Peer Insights or Reddit review specific to ASOR or Flex Credits turned up before search ran out. Workday-platform reviews on Gartner Peer Insights don't isolate agents [9]. Treat the absence as weak evidence of thin hands-on use (consistent with <900 buyers).

## Top-level: why they chose this path, and what to learn

**Starting asset and constraint.** Workday's asset is the employee record: who works here, in what role, with what access, reporting to whom, paid how much. Extending that record to agents is the cheapest move it has: a new worker type in the table, the existing security model, the existing business-process engine. The binding constraint is pricing. HCM is sold per employee, so agents that remove employees shrink Workday's billing base. Counting agents as "digital workers" with their own metered cost (Flex Credits) replaces that revenue (inference, ≈70% this is a major driver).

That same incentive makes Workday unlikely to build Cyclical's sharpest feature, a randomised test of whether a role can be removed. Mobley-style liability makes grading people and agents against each other on outcomes unattractive in HR. Its buyer (CHRO, CFO, CISO) wants control and auditability before accuracy, hence governance-first.

**Is Cyclical a clone, subset, superset or orthogonal?** Cyclical overlaps Workday on the governance half (A1 frame, A4, A7 lifecycle states) and is a superset on the evaluation half (A5–A8, A11, A12), which Workday doesn't do. On market they're orthogonal. Workday sells to large organisations and isn't a dental practice-management system, and a 9-person clinic will never buy Workday. The overlap matters in two ways: Workday is setting the vocabulary buyers will use (agent identity, owner, Delegate/Ambient, autopilot), and it shows how a system-of-record owner moves into this space.

**Copy:**
- Delegate vs Ambient as an explicit permission state, so that graduation becomes a logged permission change.
- A named agent owner per node.
- A per-action price unit visible to the business owner.
- MCP/A2A registration so third-party dental agents (Toothy, Newton, PatientDesk) can occupy Cyclical nodes rather than compete with them.

**Avoid:** building identity governance from scratch; C1-type tools will be bought or bundled. Also avoid unattributed headline stats, which are the first thing an independent reviewer attacked [27].

**Exploit:**
- Workday's measurement gap. It can tell a customer what an agent *cost* but not whether it was *right*, and it's institutionally discouraged from grading agents against humans. Outcome-graded shadow evals and pooled outcome history are the part of the loop nobody in "manage agents like workers" is doing.
- Workday's 18-month, single-system process mining, which shows how far a system-of-record owner gets on A2 without cross-tool logs.

**Threat level: low for dental, moderate as a pattern.** The direct threat is near zero: Workday doesn't serve small clinics and doesn't own dental data. The pattern threat is the one realizations.md names. The practice-software vendor (Dentrix/Henry Schein One, Open Dental, Curve, Dentally) does in dental what Workday is doing in HR: register agents as users, give them security groups, sell autopilot, meter per action.

The observations that would tell David the threat is rising:
- (a) Workday or a peer ships an ASOR metric that grades an agent against an external outcome (offer accepted, payment cleared), or compares a human and an agent on the same business-process step;
- (b) a dental practice-management vendor announces an "agent system of record", agent user types, or a partner gateway for third-party dental agents;
- (c) Workday's Q3/Q4 FY2027 calls report Flex Credit customers moving from ~200–300 toward thousands, which would mean the metered-agent-as-worker model is working commercially.

## Sources

1. Workday blog, "The Workday Agent System of Record Is Now Generally Available" — https://blog.workday.com/en-us/managing-ai-powered-future-of-work.html (via search extract)
2. MeritForge, "Workday's Agent System of Record Hits General Availability" — https://www.meritforgeai.com/news/workday-agent-system-of-record-ga-2026/
3. Incubane, "What Workday's Agent System of Record actually is" — https://www.incubane.com/insights/workday-agent-system-of-record-explained (via search extract)
4. Workday docs, "About Workday Agents / ASOR setup" — https://doc.workday.com/admin-guide/en-us/workday-ai/agents/setup-considerations--agent-system-of-record.html ; product page https://www.workday.com/en-us/ai-platform/agent-system-of-record.html
5. Workday Q2 FY2027 earnings call transcript — https://finance.yahoo.com/markets/stocks/articles/workday-wday-q2-2027-earnings-132153063.html ; https://finance.biggo.com/quote/WDAY/earnings-call/US_WDAY_2026-08-27
6. Workday AI Admin Guide PDF — https://doc.workday.com/content/dam/fmdita-outputs/pdfs/admin-guide/en-us/Admin-Guide-Workday-AI.pdf ; TechBloat guides — https://www.techbloat.com/workday-ai-assistant-governance-delegate-vs-ambient.html , https://www.techbloat.com/securely-connect-an-ai-agent-to-workday-with-least-privilege-controls.html
7. TechBloat, "Workday AI Agent Data Access and Security Explained" — https://www.techbloat.com/how-workday-ai-agents-access-data-and-the-controls-that-protect-it.html
8. CIO.com, "Workday aims to manage AI agents like employees" — https://www.cio.com/article/3821624/workday-aims-to-manage-ai-agents-like-employees.html
9. Gartner Peer Insights, Workday Platform — https://www.gartner.com/reviews/product/workday-platform?marketSeoName=cloud-erp-for-service-centric-enterprises
10. Workday newsroom, "Workday Announces New AI Agents…" (Sept 17, 2024) — https://newsroom.workday.com/2024-09-17-Workday-Announces-New-AI-Agents-to-Transform-HR-and-Finance-Processes
11. Computer Weekly, "Workday Rising: Evolving the 'agentic art of the possible'" — https://www.computerweekly.com/blog/CW-Developer-Network/Workday-Rising-Evolving-the-agentic-art-of-the-possible-for-people-money
12. S&P Global, "Workday poised for $10B in 2026 revenue as it announces Sana acquisition" — https://www.spglobal.com/market-intelligence/en/news-insights/research/2025/10/workday-poised-for-usd10b-in-2026-revenue-as-it-announces-sana-acquisition
13. Workday docs, "Concept: BP Optimize Agent" — https://doc.workday.com/admin-guide/en-us/workday-ai/agents/workday-built-agents/bp-optimize-agent/concept--bp-optimize-agent.html
14. Workday newsroom, "Workday Launches Autopilot Agents…" (Oct 13, 2026) — https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT
15. Josh Bersin, "Workday and Sana Unveil A Bold New Strategy For AI" — https://joshbersin.com/2026/03/workday-and-sana-unveil-a-bold-new-strategy-for-ai/ ; Alacrity, "Rising 2026 Decoded" — https://www.alacrity-solutions.com/post/rising-2026-decoded-what-shipped-what-s-in-early-access-and-what-waits-until-2027
16. iTWire, "Workday Rising 2026 analysis, Part 1: Workday's AI agents are now autopilots, and it wants you to stay in the loop" — https://itwire.com/business-it-news/data/workday-rising-2026-analysis-part-1-of-2-workdays-ai-agents-are-now-autopilots-and-it-wants-you-to-stay-in-the-loop ; Reworked — https://www.reworked.co/talent-management/workday-is-rebuilding-itself-around-sana-and-its-agents/
17. iTWire, "Bhusri buys C1.ai to govern AI agents" — https://itwire.com/business-it-news/data/workday-rising-2026-bhusri-buys-c1-ai-to-govern-ai-agents-as-sana-takes-over-the-home-screen ; Globe and Mail release — https://www.theglobeandmail.com/investing/markets/stocks/WDAY/pressreleases/7603473/workday-to-acquire-agentic-identity-platform-conductorone/
18. NHI Governance, "Workday agrees to acquire C1" — https://nhigovernance.com/news/2026/workday-to-acquire-c1-conductorone.html ; 8-K summary — https://www.stocktitan.net/sec-filings/WDAY/8-k-workday-inc-reports-material-event-d42dc72fabe9.html
19. Workday 8-K (Paradox) — https://www.sec.gov/Archives/edgar/data/1327811/000132781125000182/wday-082125x991.htm
20. Workday 10-K FY2026 — https://www.sec.gov/Archives/edgar/data/1327811/000132781126000014/wday-20260131.htm ; Truffle on Paradox pricing — https://www.hiretruffle.com/blog/paradox-ai-pricing
21. Workday newsroom, "Workday Completes Acquisition of Sana" — https://newsroom.workday.com/2025-11-04-Workday-Completes-Acquisition-of-sana ; 8-K — https://www.sec.gov/Archives/edgar/data/1327811/000132781125000187/wday-09162025x991sunflower.htm
22. Workday newsroom, "Agent Partner Network and Agent Gateway" (June 3, 2025) — https://newsroom.workday.com/2025-06-03-Workday-Announces-New-AI-Agent-Partner-Network-and-Agent-Gateway-to-Power-the-Next-Generation-of-Human-and-Digital-Workforces
23. Workday blog, "Why We Built Flex Credits" — https://blog.workday.com/en-us/introducing-workday-flex-credits-smarter-more-flexible-way-access-ai-innovation.html ; StackOne rate card — https://www.stackone.com/blog/workday-flex-credits-calculator/
24. Workday docs, "About Platform Consumption Console" — https://doc.workday.com/admin-guide/en-us/workday-ai/platform-consumption-console/concept--product-consumption-console.html
25. BERI, "Workday Rising 2026 Sells Agents on Credits With No Published Price" — https://www.beri.net/article/workday-rising-2026-recap-ga-vs-early-adopter-autopilots-sana-agent-harness-flex-credits ; CIO.com, "Unpacking Workday's agentic AI pricing model" — https://www.cio.com/article/4192838/unpacking-workdays-agentic-ai-pricing-model.html
26. TradingKey, "Workday Q2 FY2027 Earnings Call: AI ARR Nears $600 Million" — https://www.tradingkey.com/news/transcripts/262137269-tradingkey
27. UC Today, "Workday Rising Verdict: The Latest Promises Tested" — https://uctoday.com/workday-rising-verdict-the-latest-promises-tested
28. Diginomica, "Workday Rising – pricing, context, and (giving up) UX control" — https://diginomica.com/workday-rising-hot-topics-enterprise-ai-come-head-its-about-pricing-context-and-giving-ux-control
29. Gartner, "First Take: Workday's C1.ai Acquisition Expands Agentic Identity, but Independent Controls Must Be Retained" — https://www.gartner.com/en/documents/8508377
30. Forrester, "Workday Rising 2025: A CIO's Reality Check" — https://www.forrester.com/blogs/workday-rising-2025-a-cios-reality-check-on-the-vendors-heavy-bets-on-ai/
31. Diginomica, "Workday Innovation Summit – agentic AI is not a point solution" — https://diginomica.com/workday-innovation-summit-agentic-ai-not-point-solution-customers-air-out-why-ai-results-require
32. Gravity Fast, "Workday AI Agent: Illuminate, Agent System of Record, the Gap" — https://gravity.fast/blog/workday-ai-agent/
