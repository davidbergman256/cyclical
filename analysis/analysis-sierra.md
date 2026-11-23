# Analysis: Sierra

Sierra is an enterprise customer-service agent platform, founded in 2023 by Bret Taylor and Clay Bavor. It is paid per autonomously resolved conversation, per saved cancellation or per upsell, not per seat. It is valued at $15.8B (May 2026), with reported talks at about $30B. **Overlap: 4/10.** Cyclical shares Sierra's idea that the vendor is paid and graded on outcomes, and its view of evaluation as release engineering. Sierra lacks Cyclical's graph, its process mining, the human/agent interchangeability across a whole business, cross-customer outcome pooling and the small-business target. The most important lesson is that Sierra's "outcome" is a proxy observed inside its own conversation (no escalation, no cancellation in-session), not a downstream fact in the world. That gap is exactly where the critiques of outcome pricing land, and it is the gap Cyclical's design (grade on payments and show-ups) is built to close. A second lesson matters as much: Sierra needs no pooling, because each enterprise customer (e.g. ADT at 1–2M inquiries a month) is large enough to be its own statistical pool. Pooling is a need that small businesses create, which supports Cyclical's vertical small-business choice rather than threatening it.

## What it actually is

**Product.** The product is "Agent OS", a platform for building branded customer-facing agents on chat, voice, email and SMS. Its parts:
- **Agent SDK** (code-level, for Sierra's own engineers and customer developers) and **Agent Studio** (no-code; version 2.0 shipped with Agent OS 2.0), with **Agent Traces** showing every decision, tool call and response [7][8].
- **Agent Data Platform** (Nov 2025): a memory layer that joins conversation data (calls, chats, emails) with structured business data (billing, orders) so the agent carries context across conversations and channels [9][10].
- **Supervisors**: secondary models that audit every action and response for policy violations or harmful language. For high-risk topics they can switch from *observe* to *intercept* [8].
- **Monitors** (alerts), **Insights 2.0 / Pulse** (AI that surfaces issues and improvement opportunities from live conversations) [7][9].
- A **"constellation" of 15+ models** from OpenAI, Anthropic, Meta, Google and others. Each sub-task goes to the model that suits it, and if one provider goes down, work fails over to another [10][11].
- The **"Agent Development Life Cycle"**: every agent release is an immutable snapshot of code, prompts, model-version dependencies and knowledge. Changes are tested by simulated conversations and regression suites before release [6].
- **τ-bench (tau-bench)**: Sierra's research benchmark, released in June 2024. An LLM-simulated customer talks to an agent that holds tools and a policy, and success is checked by comparing the final database state against the target state. The benchmark introduced **pass^k**, the probability that the agent succeeds on *all* k independent trials of the same task. GPT-4o scored about 61% pass^1 on retail and 35% on airline, falling to about 25% at pass^8 on retail [12][13]. Successors are τ²-bench (2025, where user and agent both act on a shared environment) and τ³ / τ-Knowledge (2026) [14][15].

**Buyer.** Large consumer brands' CX and contact-center leaders. Named customers include WeightWatchers, SiriusXM, ADT, Sonos and Madison Reed. Sierra claims more than 40% of the Fortune 50, which is a vendor claim [1][2][16].

**Traction.**
- **Funding:** $950M Series E at $15.8B post-money (May 4, 2026), led by Tiger Global and GV. Prior rounds were $4.5B (Oct 2024) and $10B (Sep 2025). Total funding is about $1.6B [2][3].
- **Revenue:** ARR was $100M in Nov 2025 and $200M in May 2026 (Taylor) [2][17]. Aggregators report more than $400M by Oct–Nov 2026 and talks at $30B. These are unverified and about 60% likely to be roughly right [1][4].

**Pricing.** There is no public rate card. Most customers pay a pre-negotiated rate per autonomous resolution. Taylor: "if we escalate to a person, it's free" [17][18]. Other billable outcomes are saved cancellations and completed upsells (per a co-founder on CNBC, via [19]). Third parties estimate about $1–2.50 per resolution, with ~$1.50 most often cited. Sierra has not confirmed this [19][20]. One secondary summary claims Sierra initially lost money per resolution ($1.21 cost against a 99¢ price) until efficiency improved. This is unverified [18]. What counts as "success" is negotiated contract by contract [20].

**Architecture point that matters for Cyclical.** Sierra writes business logic (refund rules, eligibility checks) as deterministic code in the SDK and uses LLMs for conversation and judgment (from memory, consistent with [6][8]). Cyclical's level 3 compiles deterministic work out of the agent after observing it. Sierra puts it there from the start because an enterprise can write down its policies up front.

## Loop comparison

| Aspect | Sierra's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | One agent per brand, built from "journeys"/skills, with an escalation edge to the human queue. The business itself is not modeled. | **Different** (narrower) |
| A2 Observation | Forward-deployed engineers plus ingestion of knowledge bases, past transcripts and APIs. Insights mines *conversations*, not cross-tool event logs. | **Different / partial** |
| A3 UX | Agent faces the end customer directly. CX ops team uses Agent Studio, Traces and Insights. Human reps receive handoffs. No "draft lands in your outbox" mode in the core product. | **Different** |
| A4 Permissions | Tool-level access fixed in code, end-customer authentication, supervisors that intercept. No just-in-time node-to-node grants. Prompt-injection defense comes from deterministic code paths. | **Different / partial** |
| A5 Shadow grading on outcomes | Pre-launch grading is simulation against τ-style goal states. In production, billable outcomes are judged inside the conversation. No human-vs-agent shadow scored on downstream outcomes. | **Worse / absent** |
| A6 Checkoff with seeded errors | Automated supervisors and human conversation review. No seeded known-bad audits found. | **Absent** |
| A7 Statistical graduation | pass^k reliability, simulation regression suites, immutable release snapshots including model version. Graduation is per release, with no published per-case-type threshold. | **Better on tooling, different unit** |
| A8 Replacement levels | Deterministic code for policy from day one, plus LLM for conversation. Per-customer agent, no shared skill. | **Different** (code first rather than code compiled later) |
| A9 Orchestrator agent | Insights/Pulse suggest fixes to the agent. Nothing proposes reorganizing the business. | **Partial** |
| A10 Shared context | Agent Data Platform: unified per-end-customer memory across channels. | **Same idea, customer-centric** |
| A11 Cross-business pooling | No evidence of outcome pooling across customers. What carries across customers is the platform, τ-bench research and the deployment team's know-how. | **Absent** (and not needed at their scale) |
| A12 Anti-Goodhart | Supervisors for policy and safety, contract-negotiated definitions, customer CSAT. The pricing pays Sierra for *not* escalating. | **Worse** (incentive cuts the wrong way) |
| A13 Model-agnostic | 15+ model constellation with failover. Model version pinned in each release. | **Same / ahead** |
| A14 Business model & moat | Outcome pricing to enterprises. Moat is brand, Taylor's network, deployment capacity and platform. Not an outcome-history asset. | **Different** |

**A5/A14, what "outcome" means.** Cyclical grades on facts the world reports later: the invoice is paid, the patient shows up. Sierra's billable resolution is, on the most widely reported definition, "a successfully closed customer interaction handled by the agent without human escalation" [20]. That is decided at the end of the conversation by data Sierra itself holds. A customer who gives up and closes the chat may count [20][21]. No source describes recontact windows (e.g. the same customer returning within 7 days voids the resolution) or saved cancellations that are clawed back if the customer churns 30 days later. Some negotiated contracts probably have them, but I could not verify any (about 40% likely that large contracts include a recontact clause). A "saved cancellation" is likewise judged in-session. Whether the customer actually stayed is a downstream fact Sierra's meter does not obviously wait for.

**A7, pass^k versus the rule of three.** Cyclical's stage-3 threshold (zero errors in n *production* runs ⇒ error < ~3/n at 95%) asks how often the agent fails across varied cases. pass^k asks a different question: given one case, how reliably does the agent succeed if you rerun it k times? It is estimated as C(c,k)/C(n,k) from c successes in n trials [12]. The τ-bench result that 61% pass^1 falls to 25% pass^8 shows that agents that look competent are often unreliable on the very same case. Neither the rule of three nor approval rates would detect this from single production runs. Cyclical could use it at three points:
1. **Pre-graduation:** replay historical cases of one case type k times and require high pass^k before stage 3.
2. **Model-swap re-certification:** rerun a frozen case set at pass^k without waiting for live volume. Sierra's snapshot-with-model-version is exactly this mechanism.
3. **Low-volume case types:** simulation multiplies evidence without pooling.

The caveat is just as concrete. τ²-bench's own authors measured user-simulator error rates of 40% (retail) and 47% (airline), with 12–13% being errors that block task completion [14]. Amazon's τ²-Bench-Verified fixed ground-truth errors in the task set [22]. An independent 2026 paper found success rates swing by up to 9 points depending on which LLM plays the user, and are worse for speakers of African American Vernacular English [23]. So simulation can *add* evidence to Cyclical's stage 3 but cannot *replace* outcome grading. That confirms the founder's "grade against the world" rule.

**A12, Goodhart.** Sierra is the cleanest live case of the failure Cyclical's A12 warns about. Escalations are free and resolutions are billed, so the vendor's revenue rises with containment. Every escalation the agent avoids is revenue to Sierra, whether or not the customer was helped. Sierra's guards are supervisors (policy compliance), customer-set escalation rules, CSAT and Insights, plus the customer's own scrutiny of bills. None of these is a business-level outcome guardrail of the kind Cyclical requires (e.g. resolution paired with 30-day recontact or churn). The cancellation-save product sharpens the problem. An agent paid per retained subscriber has an incentive that sits close to "dark pattern" territory, and an agent claiming to have cancelled while billing continues is a documented failure mode in the field [24]. No regulator or lawsuit has targeted Sierra on this that I found.

**A11, why Sierra does not pool.** ADT alone sends 1.2–2M inquiries a month to its Sierra agent (secondary sources disagree [16]). At that volume, Cyclical's sample-size arithmetic (3,800 runs per variant to detect a 20% lift on a 10% rate; 300 clean runs for <1% error) is met in hours inside one customer. Enterprise customers would also refuse to have their conversation outcomes feed competitors' agents. Sierra's cross-customer learning therefore lives in people (forward-deployed agent engineers), product (SDK patterns, supervisors) and public research (τ-bench), not in a shared outcome history. That gives Cyclical a non-obvious result: the pooling moat exists only *because* the customer is small. It is a structural gap Sierra has no reason to fill.

## Where they're ahead of Cyclical

- **Evaluation as release engineering.** Sierra already runs immutable release snapshots (code + prompts + model version + knowledge), simulation-based regression suites and pass^k reliability measurement. This is Cyclical's "model swap sends a case type back to stage 2" made operational: a model change is a new release that must pass the suite. Cyclical should adopt the snapshot unit, because without it "audit drift" has no defined baseline.
- **A published reliability metric.** pass^k is well known and cited in model launches. Cyclical's statistical graduation would be more credible if stated as pass^k on replayed cases plus a zero-failure n on live outcomes.
- **Outcome pricing proven at scale.** $200M ARR in May 2026 (Taylor), and reportedly much more by late 2026, mostly billed per outcome [2][17]. That is evidence enterprises will sign outcome contracts. Taylor's framing, "what business outcome is this agent designed to produce and did it produce it?", is the pitch Cyclical needs [25].
- **Multi-model routing in production.** Sierra runs 15+ models with failover [10][11]. That is A13 in practice, at scale.
- **Supervisors.** A second model watching every turn, able to switch from observe to intercept on high-risk topics [8], is a cheap runtime guard Cyclical's design lacks between stage 2 and stage 3.

## Where they're doing it differently (and whether their way is better)

- **Code first versus compile later (A8).** Sierra codes policy up front because enterprises have written SOPs and engineers to encode them. Cyclical's small businesses have neither. Their rules exist only in staff behavior, so learning the rule from observed agent outputs and then compiling it is the right order *for Cyclical's customer*. Sierra's way is better where policy is already written down.
- **Customer-facing agent versus drafts in the worker's outbox (A3).** Sierra replaces the first-line conversation outright and escalates the rest. Cyclical keeps a human in the loop silently through drafts. Sierra's approach yields measurable containment immediately. Cyclical's yields cleaner evaluation data (an edit is a correction) and less staff resistance. For a 9-person dental office, where the front desk *is* the relationship, Cyclical's approach is probably better. For a 10,000-seat contact center, Sierra's is.
- **Outcome measured in-conversation versus downstream (A5).** Sierra's meter is instant and fully in its own hands, which makes billing simple and keeps the timing of its revenue predictable. Cyclical's meter (payments, show-ups) waits weeks and depends on data from the system of record. Cyclical's is harder to game. Sierra's is easier to bill on. A hybrid is the lesson: bill on the instant proxy, then true it up against the downstream outcome after a lag.
- **Humans as an overflow queue at each customer (A11 exception desk).** Sierra's escalations go back to the customer's own human agents. Cyclical's pooled central exception desk is a different and more aggressive structural bet that Sierra cannot make, because enterprises will not share support staff.

## Feedback & reviews on these parts of the loop

**Outcome definitions and billing (A5/A14)**
- *Independent/critical:* "a deflection meter dressed up as a resolution meter is the fastest way to pay for the privilege of losing customers" [21]. A customer who gives up "counts as deflected but not resolved" [21].
- *Independent/critical:* Outcome pricing "replaces a unit buyers could verify themselves with one only the vendor can measure". "Resolution by silence" is where billing disputes concentrate [26][27].
- *Third-party guide:* Sierra's reported definition "is generous to the vendor, since a customer who gives up can still count" [20].
- *Industry press:* the software industry sees "dispute risk" as outcome pricing spreads [28].
- *Vendor (Sierra, via third party):* "if the conversation is unresolved, in most cases, there's no charge" [20]. Sierra admits the model only works where the agent acts on its own and the result can be credited to it [20].
- *SaaStr (analyst-ish):* Salesforce, Zendesk, Intercom and Gorgias all charge or try to charge $1–3 per resolution. The open question is "whether it will stick" [29].
- *Competitor critique:* Siena AI publicly argued that per-resolution billing rewards closing conversations fast rather than well [26].

**Resolution rates and evidence quality (A5)**
- *Vendor:* WeightWatchers' agent contained "nearly 70% of all cases within the first week" at 4.6 CSAT [16][30].
- *Independent analysis:* published case studies range 64–94%, mostly 65–77%. Production evidence "clusters at 40 to 70 percent" [21][31]. No independent outlet confirms Sierra's case-study numbers [30].

**Product and operations (A3/A9)**
- *G2:* 4.4–4.5 stars on about 128–132 reviews [21].
- *Third-party reviews:* many configuration changes require Sierra's team rather than self-service. The agent can lose context in long multi-turn conversations [21]. Customers depending on the vendor to change the agent is the forward-deployed model's cost.

**Evaluation methodology (A7)**
- *Independent research:* LLM-simulated users are "unreliable proxies for human users in agentic evaluations", with up to 9-point swings across simulator LLMs and dialect bias [23]. τ² simulator error was 40–47% in retail/airline [14]. Amazon's τ²-Bench-Verified found policy, database and grading errors in tasks [22].

**Human handoff and jobs.** I found no customer headcount figures for WeightWatchers, SiriusXM or ADT. Sierra positions escalation as free and the human as the fallback. The jobs effect is unreported, not disproven.

## Top-level: why they chose this path, and what to learn

**Starting assets.**
- **People:** Taylor (ex co-CEO of Salesforce, CTO of Facebook, chair of OpenAI) and Bavor (ex-Google). Their asset was trust and access in Fortune 500 boardrooms, not data.
- **The buyer:** contact centers are a large, measurable cost line with a budget owner who already thinks in cost per contact. That makes per-resolution pricing legible.
- **The constraint:** no proprietary outcome data and a crowded market (Decagon, Intercom Fin, Agentforce, Zendesk). Outcome pricing let Sierra take the risk the buyer feared ("pay only if it works"). It also turned the sale from a software line item into a share of the cost saved.
- **Why not pool:** the buyers are each large enough not to need it, and would not allow it.
- **Why simulation:** pre-launch evidence was needed before a brand would expose its customers. τ-bench turned that need into research credibility and recruiting pull.

**Copy.**
1. Immutable release snapshots with model version pinned, as the unit that graduates or reverts.
2. pass^k on replayed historical cases as a stage-3 pre-check and as fast re-certification after model swaps. Keep live-outcome zero-failure counts as the final gate.
3. Runtime supervisors that can switch from observe to intercept on high-risk case types (e.g. clinical, payment).
4. Outcome pricing as the go-to-market, but tied to the downstream fact. For example, per claim paid on first submission, per recall appointment that actually shows, with a true-up lag. This defends against the "resolution by silence" critique Sierra and Fin face.

**Avoid.** Do not bill on an outcome the vendor alone observes and that rises when the agent avoids the human. Every billed local metric needs the paired business guardrail (A12) written into the contract, e.g. a resolution voided if the customer recontacts within 7 days.

**Exploit.**
- Sierra's structure keeps it out of small businesses: no pooling, outcomes measured in-session, high-touch deployment.
- Decagon's median contract is reportedly about $430k a year with a ~$50k platform fee (Vendr via third party, unverified) [32]. That price point and sales motion cannot reach a 9-person clinic.
- Cyclical's claim that it can learn from 10,000 small clinics what no single clinic can is precisely what Sierra's enterprise model never builds.

**Clone, subset, superset or orthogonal?** Mostly orthogonal, with partial overlap. Sierra covers one edge of Cyclical's graph (customer conversation and the escalation edge to a human) much more deeply than Cyclical would. Cyclical is a superset in *scope* (the whole graph, reorganization, pooling) and a subset in *depth* on conversational agents.

**Threat: low for now (about 15% that Sierra competes directly in small-business dental within 3 years).** Signals that the threat is rising:
- Sierra publishes downstream outcome grading (recontact, churn or payment windows) or cross-customer benchmarks.
- Sierra ships a self-serve or packaged vertical agent priced for small businesses (e.g. a healthcare front-desk agent through a practice-software partner).
- Sierra adopts per-case-type graduation that hands back-office tasks, not just conversations, to agents.
- Sierra partners with or acquires a system-of-record vendor (e.g. Dentsply Sirona / Dentrix, Henry Schein One).

**Brief comparison of outcome pricing among competitors.**

| Vendor | Pricing | What counts | Verification |
|---|---|---|---|
| **Sierra** | Negotiated per-resolution rate; escalations free; also bills saves and upsells | Agent-closed conversation without escalation (reported) | Vendor-measured, per contract [17][20] |
| **Intercom Fin** | $0.99 per "outcome". Outcome now includes resolutions, procedure handoffs, disqualifications and self-serve routings at $0.99, and qualifications at $9.99 (third-party reading of Fin's page) [33][34] | Customer confirms, *or* does not ask for more help after Fin's last answer | The "soft resolution" by silence is the most criticized definition in the market [26][27][34] |
| **Decagon** | Annual platform fee (~$50k reported) plus custom per-conversation or per-resolution fees; one reported rate is $0.50 per resolution [32] | Customer can choose per-conversation, which sidesteps resolution disputes | Unverified |
| **Zendesk** (contrast) | Per verified resolution | Only resolutions passing an AI check; assisted escalations and unverified contained conversations made free in 2026 [26] | The closest any vendor gets to separating proxy from outcome, though the verifier is still the vendor's own AI |

## Sources

1. https://gokhshtein.com/news/2026-11-18-sierras-30b-valuation-rests-on-400m-arr-but-growth-math
2. https://www.idlen.io/news/sierra-950-million-series-e-15-8-billion-valuation-bret-taylor-tiger-global-may-2026/
3. https://okara.ai/blog/sierra-ai-revenue-growth
4. https://getlatka.com/companies/sierra
5. https://www.teahose.com/guides/sierra-valuation
6. https://sierra.ai/blog/agent-development-life-cycle
7. https://sierra.ai/product/agent-studio
8. https://sierra.ai/uk/blog/enterprise-grade-agents
9. https://sierra.ai/blog/agent-os-2-0
10. https://atlan.com/know/ai-agent/ai-agent-applications/sierra-ai-vs-agentforce/
11. https://atlan.com/know/ai-agent/ai-agent-applications/what-is-sierra-ai/
12. https://export.arxiv.org/pdf/2406.12045
13. https://sierra.ai/blog/benchmarking-ai-agents
14. https://arxiv.org/pdf/2506.07982
15. https://arxiv.org/pdf/2603.04370
16. https://sierra.ai/customers/weightwatchers
17. https://techcrunch.com/?p=3070105
18. https://tipsheet.ai/news/openai-chairman-outcomes/
19. https://www.buildmvpfast.com/blog/sierra-per-resolution-economics-vertical-ai-agents-2026
20. https://myaskai.com/blog/sierra-ai-pricing-explained
21. https://sitegpt.ai/resources/sierra-review
22. https://github.com/amazon-agi/tau2-bench-verified
23. https://arxiv.org/html/2601.17087v2
24. https://dev.to/chenwengui23/your-ai-told-the-customer-they-were-cancelled-the-subscription-renewed-11-days-later-463m
25. https://cheekypint.substack.com/p/bret-taylor-of-sierra-on-ai-agents
26. https://www.flowverify.co/blog/outcome-based-ai-pricing-salesforce-intercom-2026
27. https://www.flowverify.co/blog/outcome-based-ai-pricing-resolution-definition
28. https://www.digitaltoday.co.kr/en/view/98342/software-industry-outcome-based-pricing-spread-dispute-risk
29. https://www.saastr.com/the-real-question-for-outcome-based-pricing-is-if-it-will-stick
30. https://theinternetninja.com/stories/sierra-weightwatchers-ai-cx/
31. https://www.dragapp.com/blog/ai-support-agent-resolution-rates/
32. https://myaskai.com/blog/intercom-fin-decagon-ai-comparison-2026
33. https://www.usagepricing.com/blueprint/intercom-fin
34. https://selvo.co/blog/intercom-fin-pricing
35. https://sierra.ai/blog/ai-agents-drive-customer-retention
36. https://sequoiacap.com/podcast/training-data-bret-taylor

Method note: WebFetch could not resolve sierra.ai, cheekypint.transistor.fm and other hosts in this session, so Sierra primary pages and interviews were read through search extracts only.
