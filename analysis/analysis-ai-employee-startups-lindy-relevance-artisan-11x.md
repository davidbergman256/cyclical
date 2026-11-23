# Analysis: Horizontal "AI employee" startups (Lindy, Relevance AI, Artisan, 11x, Beam AI, Sema4.ai, Tasklet, Manus, Genspark)

These companies sell a business one anthropomorphized agent ("Alice the AI SDR", "Ava the AI BDR", "your AI workforce") that slots into a single role, priced against that role's salary and judged by whether it matches a human's output. **Overlap with Cyclical: 3/10.** They share the vocabulary (agents taking over human roles, human-in-the-loop) but not the loop: none models the business as a graph that people and agents occupy interchangeably, none grades against real-world outcomes per case type, and none pools outcomes across businesses. Relevance AI's multi-agent "Workforce" canvas is the closest thing to A1 and still has only agents as nodes. **The most important lesson is 11x:** if you sell "replace the role" without a staged way to prove the replacement works, customers run a 90-day trial, see the agent fail at the role, and leave. One reported version of 11x's numbers had ~$14M of "ARR" resting on ~$3M of contracts that survived the trial period. Cyclical's per-case-type graduation is that missing mechanism.

> **Research caveat.** The shared web-search budget ran out after six searches, and the fetch tool could not reach techcrunch.com or most other hosts in this session. The 11x and Artisan facts below come from search results that summarize primary reporting (TechCrunch, Bloomberg, Tech.eu) and are cited. Most facts about Lindy, Relevance AI, Beam, Sema4.ai, Tasklet, Manus and Genspark are **(from memory)**, last known as of early-to-mid 2026, and should be re-checked before anyone relies on a number. I'd put roughly a 25% chance that at least one product description below is out of date by Nov 2026, given how often these companies relaunch.

## What it actually is

The cluster splits into two kinds of product that share a marketing frame.

**Role-replacement agents (vertical-in-function, horizontal-in-customer).** 11x and Artisan sell a named digital worker for one sales function: outbound prospecting and email or LinkedIn sequencing.

- **11x.** London-founded, later San Francisco-based. Products: *Alice* (outbound AI SDR, a sales development rep who books meetings for account executives) and an inbound/phone agent, which sources variously call Julian or Jordan [5][8]. Funding: $2M pre-seed (2023), $24M Series A led by Benchmark (2024), $50M Series B led by a16z (late 2024) at a reported ~$320–350M valuation; $70–76M raised in total depending on the source [8]. In Sept 2024 founder Hasan Sukkar said 11x was "approaching $10 million in annual recurring revenue" [8]. In March 2025 TechCrunch reported that 11x showed ZoomInfo and Airtable logos although neither was a customer, and that it counted trial-period contracts as full-year revenue [2][3]. Sukkar stepped down as CEO on 5 May 2025; CTO Prabhav Jain, formerly head of engineering at Brex, replaced him [6][7]. I found no new equity round or revenue figure for 2026. One aggregator attributed a Nov 2026 $500M General Catalyst deal to 11x, but that deal went to **Nooks** [9].
- **Artisan.** YC-backed, San Francisco. Product: *Ava*, an "AI BDR" (business development rep, which here means the same job as an SDR) that finds leads, writes emails and runs sequences. It is known for its "Stop Hiring Humans" billboard campaign (from memory, Dec 2024) and raised a ~$25M Series A in 2025 (from memory). Reported pricing runs from ~$250/month to $2,000+/month; it is not published [10]. Trustpilot showed 4.1/5 from 42 reviews on 31 Oct 2026 [10].

**Horizontal agent builders that call their output "AI employees" or an "AI workforce".**

- **Lindy** (Flo Crivello). A no-code builder for agents ("Lindies") with triggers, actions, LLM steps and knowledge bases. Multiple Lindies can hand work to one another (marketed as "societies"/agent swarms), and an action can require human confirmation. Pricing is credit-based, from a free tier up to roughly $50–300/month (all from memory). By 2025 Lindy was shifting toward a single packaged "AI assistant" for email, calendar and meetings that works in the user's existing inbox and messaging, a sign that the open builder was too hard for small-business buyers (from memory, ~60% confident about the framing).
- **Relevance AI** (Sydney/San Francisco). A builder whose pitch is literally "build your AI workforce". Agents have tools; a *Workforce* canvas wires several agents into a multi-agent system with explicit handoff edges; each tool can be set to auto-run or require approval, and agents can escalate. It raised a ~$24M Series B led by Bessemer in 2025 and uses credit-based pricing (from memory).
- **Beam AI** (Berlin). "Agentic process automation": it turns standard operating procedures (SOPs) into agent flows, with human-in-the-loop checkpoints and "self-learning" from corrections. It sells to mid-market operations teams in claims, order processing and HR (from memory).
- **Sema4.ai** (the 2024 merger of Robocorp's RPA business with Sema4). Enterprise agents defined by natural-language "runbooks", with a Snowflake partnership; it sells to enterprise automation teams, not small businesses (from memory).
- **Tasklet** (Andrew Lee, of Firebase and Shortwave). A cloud agent you instruct in plain English that connects to apps or APIs and runs on triggers. It is closer to "Zapier where the zap is a prompt" than to an employee (from memory).
- **Manus and Genspark.** General-purpose "do the task end to end" agents that later added business and team plans. Manus reportedly passed ~$100M ARR in 2025, and Meta announced it would acquire Manus at the end of 2025. Genspark reported very fast ARR growth and a large 2025 round (all from memory, not verified here). Their buyers are mostly individuals doing research and producing documents, not businesses delegating a process step, so they are peripheral to Cyclical and get little space below.

**Architecture where public.** 11x rebuilt Alice on LangGraph in 2025 as a supervisor agent with sub-agents for research, positioning and writing; LangChain published it as a case study (from memory). Every product in the cluster is a set of prompts, tools and integrations around frontier models. None publishes an evaluation methodology that grades against downstream business outcomes.

## Loop comparison

| # | Aspect | Cluster's approach | vs Cyclical |
|---|---|---|---|
| A1 | Graph frame, person ≡ agent | 11x/Artisan: one agent replaces one role, and no graph exists. Lindy/Relevance: agent-to-agent handoffs on a canvas (Relevance "Workforce", Lindy "societies"); humans appear only as approvers or escalation targets, never as occupants of the same node | **Different** (role, not graph); Relevance is partial |
| A2 | Onboarding by process mining | Users configure the agent: they write instructions, upload the ICP (ideal customer profile) and SOPs, and connect apps. Beam converts SOP documents into flows. Nobody reads event logs to discover the actual process | **Absent** |
| A3 | Minimal UX, drafts where people work | 11x/Artisan: a new dashboard and campaign console; emails go out from the vendor's sending domains or the customer's warmed mailboxes. Lindy can draft into Gmail and works in the inbox (from memory) | **Worse** for SDR tools; Lindy is **Same**-ish on drafts |
| A4 | JIT permissions, rule-based A2A approvals | Static OAuth grants per integration; per-tool "require approval" toggles (Relevance, Lindy). No temporary grants, no request-frequency signal, no rule engine for agent-to-agent data access | **Absent** (static) |
| A5 | Shadow mode graded on outcomes | No shadow mode. The agent goes live and is judged by the buyer on meetings booked or reply rate, at campaign level, not per decision | **Absent** |
| A6 | Checkoff with seeded known-bad outputs | Optional approve-before-send in all of them; nothing guards against rubber-stamping | **Worse** (checkoff without audit) |
| A7 | Statistical graduation per case type | None; autonomy is a toggle the customer flips | **Absent** |
| A8 | Replacement ladder: skill → per-business layer → code → merge | Shared templates plus per-customer prompts and knowledge base ≈ levels 1–2. No compile-to-code step, though Tasklet/Lindy workflows are partly deterministic by construction | **Partial** (levels 1–2) |
| A9 | Orchestrator proposes reorganizations | Lindy/Relevance have a "build an agent for me" copilot that drafts agents from a prompt. Nothing watches performance and proposes merging or removing roles | **Absent** |
| A10 | Shared context layer | Per-agent knowledge bases; Relevance/Lindy let several agents share one KB; 11x keeps per-customer company and product context | **Same** (common practice) |
| A11 | Cross-business outcome pooling | 11x/Artisan see reply and meeting rates across all customers' campaigns and could in principle pool them; there is no public evidence they do it as controlled experiments. Builders have no common process to pool on | **Absent** (latent at 11x/Artisan) |
| A12 | Anti-Goodhart guardrails | The reverse: SDR agents optimize volume or meetings booked, which burns sending domains and brand. No paired business-level metric such as pipeline quality or closed-won | **Worse** (the failure A12 exists to prevent) |
| A13 | Model-agnosticism | Most route across OpenAI/Anthropic models; Lindy/Relevance let users choose the model | **Same** |
| A14 | Business model & moat | Seat-like subscription priced against salary (an SDR costs ~$60–90k/yr loaded; an AI SDR costs ~$3–60k/yr) or usage credits. Moat claimed = brand plus integrations. No outcome-history asset | **Different** (and weaker) |

**A1 is where the frames really diverge.** An "AI SDR" is one anthropomorphized node with no edges modeled. 11x never knows that the account executive who receives Alice's meetings rejects 40% of them as unqualified, because that edge sits outside its product. The role frame sells well because the buyer already has a budget line, a mental model and a comparison price: the salary on the job req. But it bundles every case type in that role into one hire/fire decision. Cyclical's graph frame breaks the role into case types and edges, so an agent can take over the 95% of easy cases while a human keeps the 5% that are hard. The role-as-a-unit choice is why these products churn wholesale instead of shrinking gradually to the part that works.

**A1, partial exception: Relevance AI's Workforce canvas.** It is a real graph, with agents as nodes and handoff conditions as edges, and it is the cluster's closest match to Cyclical's data structure. It differs in three ways: the user draws the graph by hand instead of discovering it (A2); people are not nodes, only approval gates; and edges carry no outcome grades. Relevance has built the editor, not the loop.

**A3: the cluster is split, and Lindy is right.** 11x and Artisan add a new console, new sending infrastructure and new campaign logic, while Lindy's later inbox-native assistant puts drafts in Gmail where sending means approval. The "AI employee" framing pushes vendors toward the console because an employee needs a desk. Cyclical's choice (no new tool; the draft folder is the queue) matches the more defensible half of the cluster. Fyxer AI is a pure version of this UX: it drafts into the user's own inbox and learns from edits (from memory).

**A5–A7: none of them have it, and that is the commercial gap.** The cluster's evaluation is the buyer's gut check after 60–90 days. That gives exactly the outcome the 11x reporting describes: customers used break clauses to leave [2][3]. Cyclical's three stages are a product answer to the trial-churn problem these companies sell into.

## Where they're ahead of Cyclical

- **Go-to-market and distribution.** Lindy, Relevance and Artisan have thousands of paying small-business and mid-market accounts and tested self-serve funnels; Cyclical has none. The "hire an AI employee" message measurably gets attention: Artisan's billboards and 11x's growth to a claimed ~$10M contracted ARR within about 18 months [8].
- **Integration breadth.** Builders like Lindy, Relevance and Tasklet ship hundreds of connectors (Gmail, Outlook, calendar, Slack, HubSpot, Salesforce), plus computer-use or browser agents for apps with no API. Cyclical's A2 observation layer needs the same connectors, so these are the integration surfaces Cyclical will be compared against.
- **Agent-to-agent handoff editors.** Relevance's Workforce canvas is a working UI for showing and editing a multi-agent graph. Cyclical's orchestrator view (A9) can learn from it: a canvas where edges carry conditions is a known, sellable pattern.
- **Speed of shipping on new model capabilities.** Computer use, voice and browser agents land in these products within weeks of a model release. That is a strength for occupying nodes, not for owning the graph.

## Where they're doing it differently (and whether their way is better)

**Unit of sale: a role (theirs) versus a graph (Cyclical).** Their way is better for the first sale: one budget owner (the VP of Sales), one comparison (an SDR's salary) and one KPI (meetings booked). It is worse for retention, because a single KPI on a whole role exposes the agent's worst case types. Cyclical should keep its graph internally but probably sell in role-sized increments ("we'll take your insurance verification") and then expand along edges. In dental, that maps cleanly onto the front-office roles that shrink [realizations §5].

**Grading: human-equivalence or vendor-chosen proxies (theirs) versus world outcomes (Cyclical).** SDR agents grade themselves on emails sent, open rate and meetings booked, all proxies the vendor controls. Those proxies are exactly what Goodhart's law breaks: mass sending raises meetings for a quarter and destroys domain reputation and brand. Cyclical's choice to grade on show-ups and payments, with a paired business guardrail, is strictly better. It is also only possible in a domain where the world produces a grade on its own (insurer remittances, appointment show-ups), and outbound sales mostly lacks one.

**Breadth: horizontal (builders) versus one vertical (Cyclical).** Lindy and Relevance chose horizontal because their starting asset was a general builder. The cost is that no two customers run the same process, so they cannot pool outcomes or certify an agent statistically. The vertical SDR tools (11x, Artisan) do run the same process across hundreds of customers and could pool, but their outcome (a closed deal) arrives months later, is noisy, and is confounded by the customer's own product. Dental is a better pooling domain than outbound sales: claims either pay or don't, patients either show or don't, and the process is nearly identical across ~200,000 US dentists' offices (from memory).

**Human role: approver or escalation target (theirs) versus interchangeable occupant (Cyclical).** In these products the human always sits outside the node, approving or catching exceptions. Cyclical's symmetry, where a person and an agent fill the same node and are graded on the same outcome, is what lets it ask "who is better at disputes?" and get a data-backed answer. The cluster can't ask that question because it never measures the human.

## Feedback & reviews on these parts of the loop

**A5–A7 / A14 (does it work, does revenue stick): 11x, independent.** TechCrunch's March 2025 investigation reported that 11x showed ZoomInfo and Airtable logos without being their customer. A ZoomInfo spokesperson: "We did not give them permission to use our logo in any manner, and we are not a customer"; ZoomInfo's lawyer threatened legal action [2][3]. Airtable "conducted a 'very short' trial... late last year" and decided against it [3]. "Three current and former 11x workers told TechCrunch that most of its early customers took advantage of 'break clauses' in their sales contracts to discontinue using the product" [3]. The reporter's summary: 11x "counted trial users as full-year ones, making its ARR look 4x bigger," and its products "barely work," according to a former engineer [1]. 11x's response: it reports "contracted ARR (CARR)" to its board, investors knew, it removed inaccurate logos, and its retention was 79% [3][4]. **Verification status:** the logo claims are corroborated by statements from ZoomInfo and Airtable. The "~$14M stated vs ~$3M that survived the break clause" figure appears only in a low-authority aggregator [3] and should be treated as unverified. Another blog's "70–80% churn" figure [4] I could not trace to TechCrunch. Both the CEO change [6][7] and Bloomberg's note that Sukkar "strongly denied" the allegations [7] are independently reported.

**A5 / A12 (quality versus volume): Artisan, independent but secondhand.** Several review roundups cite Reddit users who sent 1,000–1,400+ Ava emails and got zero replies, and describe the copy as "extremely bland and obviously AI" [10]. Churn evidence is weak: one blog says users churn after 30–60 days, and 11x's own comparison page claims ~80% churn in Artisan's early cohorts. That comes from a direct competitor and is **not credible as evidence** [10]. Trustpilot is more positive (4.1/5, n=42), with company replies to reviews [10]. That pattern fits review curation as much as it fits product quality.

**A5–A7 (category-level reliability): independent, from memory, not re-verified this session.**
- Carnegie Mellon's *TheAgentCompany* benchmark (Dec 2024) put LLM agents in a simulated software company. The best agent fully completed ~24% of tasks (later model updates ~30%). This is the most direct test of "an AI employee doing a job" and shows a role-level success rate far below what a role-replacement pitch implies.
- Salesforce's *CRMArena-Pro* (2025): leading agents succeeded ~58% of the time on single-turn CRM tasks and ~35% on multi-turn ones.
- Gartner (June 2025) predicted that over 40% of agentic-AI projects would be cancelled by end-2027, and estimated that only ~130 of the thousands of vendors claiming "agentic" capability were real ("agent washing").
- MIT NANDA, *The GenAI Divide* (Aug 2025): ~95% of enterprise generative-AI pilots showed no measurable P&L impact. Its stated cause was tools that don't learn from feedback or adapt to workflows, which is precisely the missing A5–A7 loop.
- Klarna (2024–25) said AI replaced ~700 customer-service agents, then in 2025 said it would bring humans back because quality had fallen. This is the best-known role-replacement reversal.

**A3 (UX), mixed.** Industry roundups say the failures of AI SDRs mostly happen downstream of the product: deliverability (sending domains blacklisted), bounced or wrong contact data, and account executives rejecting meetings that don't fit [4][11]. That supports Cyclical's claim that the unit to grade is the edge (SDR→AE handoff accepted? meeting held?), not the node's output.

**Vendor-sourced (low weight).** 11x's self-reported 79% retention [3]; Artisan's and 11x's case studies and comparison pages [10].

## Top-level: why they chose this path, and what to learn

**Starting asset and constraint.** The SDR tools (11x, Artisan) began in 2023–24 with no proprietary data, frontier models that could write a passable cold email, and a buyer, the VP of Sales, used to paying per seat for outbound tools. Outbound sales was the obvious first role. Its output (an email) is low-stakes per unit, high-volume, and easy to demo, and the buyer's KPI (meetings) is visible within weeks. The "AI employee" framing was a pricing strategy as much as a branding one: anchoring against a $70k salary instead of a $100/seat SaaS tool let them charge $30–60k a year (from memory) for software. Venture investors rewarded fast contracted ARR, and a three-month break clause made contracted ARR easy to book and hard to keep. The builders (Lindy, Relevance) began as general automation platforms and borrowed the "employee/workforce" language because buyers understand hiring better than workflows.

**What that path produced.**
1. Customers judged the whole role on whatever the agent did worst, then churned wholesale.
2. Vendors were incentivized to optimize the visible proxy (volume, meetings) over the business outcome (pipeline, revenue, brand), which is A12's Goodhart failure at company scale.
3. The anthropomorphic frame created a trust problem when results lagged: an "employee" that misbehaves is a PR story, as the logo and ARR controversy showed.
4. There was no accumulating asset: each customer's agent is configured from scratch, and the next model release makes the competitor's agent equally good.

**Copy.**
- The role-shaped sale: enter as "we take your insurance verification and recall calls," priced against the cost of that front-office role, then expand along edges.
- Inbox-native drafts (Lindy's later direction, Fyxer).
- Relevance's canvas as a starting point for the orchestrator view.
- Their connector breadth as table stakes.

**Avoid.**
- Selling autonomy as a switch the customer flips. Sell graduation per case type with a stated error bar ("verification for Delta Dental PPO cleanings: 0 errors in 412 runs, error rate <0.8% at 95%").
- Contracted-ARR-style metrics and break-clause trials. They hide the very churn that Cyclical's staged evals are designed to prevent, and they invite the 11x story.
- Grading on vendor-controlled proxies. Graduation should be tied to remittances, deposits and show-ups.
- Anthropomorphized naming ("Ava the AI receptionist") in a clinical setting, where an error by a named "employee" damages trust more than an error by a "step".

**Exploit.** These vendors cannot easily add A5–A7 or A11, because their customers run different processes (builders) or produce slow, noisy outcomes (SDR). Small businesses burned by an AI-employee trial are a ready audience for "we prove it on your cases before it acts alone." The AI SDR churn wave is a sales argument for Cyclical.

**Is Cyclical a clone, subset, superset, or orthogonal?** A superset in mechanism and orthogonal in market. Cyclical contains their core capability (an agent occupying a role) as one node type, and adds the graph, the outcome grading, the graduation statistics and the pooling. They sell horizontally to sales teams and generalists; Cyclical sells vertically to dental front offices. Evidence: none of them targets dental operations, and none grades on payer or show-up outcomes.

**Threat level: low-to-moderate (≈3/10).** The live threat is not 11x or Artisan. It is a horizontal builder (Lindy, Relevance) or Microsoft/OpenAI-style agent platforms that give agents org-chart identities: Microsoft's Agent 365 / Entra Agent ID (from memory, Nov 2025) and OpenAI Frontier [realizations §4]. Those could productize a vertical template with outcome hooks. **The observation that would tell David the threat is rising:** any of these companies launching a vertical edition (dental, medical front office, home services) that connects to practice-management software (Dentrix, Eaglesoft, Open Dental) and reports outcome metrics such as claim-acceptance or no-show rates per agent instead of tasks completed. A second signal would be a builder publishing cross-customer benchmarks ("agents using template X book 18% more recalls than the median"), which would mean they had started pooling.

**Other incumbents found that may be close to Cyclical and might be missing from the list:**
- **Nooks *Node*** (launched 4 Nov 2026 with a $500M General Catalyst CVF commitment): one agent per deal-team member, and reps approve every outgoing message. That is a per-person node with draft-approval UX, in sales [9].
- **Fyxer AI**: drafts land in your own inbox and the product learns from your edits. It is the purest A3 precedent (from memory).
- **Ema** ("universal AI employee", enterprise horizontal; from memory).
- **Microsoft Agent 365 / Entra Agent ID**: agents as directory identities with permissions and org-chart placement. This is the platform version of the anthropomorphized node and relevant to A4 (from memory).

## Sources

1. Charles Rollet (TechCrunch) on X, summary of the 11x investigation — https://x.com/CharlesRollet1/status/1904313559896797402
2. TechCrunch, "a16z- and Benchmark-backed 11x has been claiming customers it doesn't have" (24 Mar 2025) — https://techcrunch.com/2025/03/24/a16z-and-benchmark-backed-11x-has-been-claiming-customers-it-doesnt-have (reprint: https://finance.yahoo.com/news/a16z-benchmark-backed-11x-claiming-230302762.html; https://philadelphiatechmagazine.com/2025/03/25/a16z-and-benchmark-backed-11x-has-been-claiming-customers-it-doesnt-have/)
3. Secondary summaries of the TechCrunch reporting, including the unverified ~$14M vs ~$3M figure — https://www.usagepricing.com/blueprint/activity/11x-2025-03-24-inflated-arr-claims ; https://ai-founder-atlas.pages.dev/cases/11x/ ; https://siela.in/blog-11x-ai-sdr-techcrunch-report
4. Secondary coverage of 11x churn and the AI SDR cancellation wave — https://coldcalls.ai/blog/what-happened-to-11x-ai ; https://www.leadgen-economy.com/blog/ai-sdr-cancellation-wave-failure-forensics/ ; https://salesmotion.io/blog/ai-sdr-claims-scrutiny-what-buyers-should-verify
5. 11x competitive analysis (Q2 2026) — https://toarn.com/insights/11x-ai
6. TechCrunch, "11x CEO Hasan Sukkar steps down" (5 May 2025) — https://techcrunch.com/2025/05/05/11x-ceo-hasan-sukkar-steps-down/ ; Tech.eu — https://tech.eu/2025/05/06/founder-of-a16z-backed-11x-steps-down-as-ceo/
7. Bloomberg, "Andreessen-Backed AI Bot Startup 11x Replaces CEO Sukkar" — https://www.bloomberg.com/news/articles/2025-05-05/ceo-of-andreessen-horowitz-backed-ai-startup-11x-steps-down
8. 11x funding and revenue aggregators — https://seedtable.com/companies/11x ; https://www.tooljunction.io/ai-tools/11x-ai/company ; https://getleadwave.io/dossier/11x
9. Nooks press release, "Nooks Secures $500 Million from General Catalyst and Launches Node" (4 Nov 2026) — https://www.morningstar.com/news/pr-newswire/20261104sf88531/nooks-secures-500-million-from-general-catalyst-and-launches-node-the-first-ai-personal-assistant-for-sales ; https://www.nooks.ai/blog-posts/introducing-node-revenue-agent-platform
10. Artisan reviews and complaints — https://coldreach.ai/blog/artisan-ai-review ; https://trysolostack.com/blog/is-artisan-legit/ ; https://marketbetter.ai/blog/artisan-ai-review-2026/ ; https://www.11x.ai/guides/artisan-review (competitor-authored) ; https://ca.trustpilot.com/review/artisan.co
11. AI SDR buyer's guide 2026 — https://www.digitalapplied.com/blog/ai-sdr-agents-2026-buyers-guide-landscape-pricing
