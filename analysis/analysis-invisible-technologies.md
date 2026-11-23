# Analysis: Invisible Technologies

Invisible's original 2015–2021 model ("Worksharing") is the closest historical version of Cyclical's core frame. It split a client's process into steps and ran each step with either a human "agent" or a bot. Its stated plan was "every process is a product we automate over time, driving costs down." It never became an automation business. Its growth came after 2022, when OpenAI hired it as a managed workforce for RLHF (reinforcement learning from human feedback: humans rate and rewrite model outputs so the model can be trained on them). That took revenue from about $60M (2023) to about $134M (2024). It now sells a large-enterprise "AI platform" (Neuron, Atomic, Axon, Synapse, Meridial) on top of the same workforce. **Overlap: 4/10.** The 2018 frame matches A1 and A8 closely (about 7/10 on those aspects alone). Invisible had no outcome-graded evals and no pooling, never picked a vertical, and today targets enterprises and AI labs. **Lesson:** a horizontal "run any business's process with humans + bots" company ends up with every step running at one client's volume. Automation then never earns its keep, and the real asset turns out to be the workforce-management machine, not the processes. That is outside evidence for realizations.md §4: one vertical and pooling are not optional.

> Research note: every agent in this run shares one web-search budget, and it ran out partway through this research. WebFetch could not reach contrary.com, sacra.com, medium.com or wikipedia.org from this session. Facts below come from search-engine summaries of those pages. Anything from my own background knowledge is marked "(from memory)". Reddit threads were not reached.

## What it actually is

**Founding and original product (2015–2021).** Francis Pedraza founded Invisible in 2015 to "combine automation with on-demand human expertise." It started as an executive-support service for CEOs [1]. In Pedraza's own posts (2017–2020), a client delegated work over email or Slack (from memory). Invisible then:

- **Watched the work:** "someone silently watches you while you work and writes down sets of instructions" (2017) [2].
- **Ran it as a "digital assembly line":** "Agents build, execute and upgrade 600+ processes 24/7. Every process is a product we automate over time, driving costs down" (2018) [3].
- **Priced to fall with automation:** "Invisible delivers immediate relief with coordinated labor, and then drives down costs over time with automation." Annual-plan clients got a results-based price whose unit cost "goes down steadily as the company automates" [2][4].

Forbes (2020) called the model "Worksharing": outsourcing combined with automation [5]. Sacra's example: to schedule a meeting, one agent finds calendar openings while another compiles a briefing document [6]. Bots took the repetitive sub-steps [7]. The posts show no public mechanism for deciding when a step was ready to automate: no threshold and no grading against outcomes. Automation was an engineering judgment about which steps were repetitive and high-volume (inferred from the absence of any such mechanism in the public material, about 75% confident there was nothing more formal).

**Pricing then.** A dated review site lists consumer and SMB plans at $15/hour pay-as-you-go, $10–12/hour on subscription and $9–12.50/hour in bulk, with a $40 upfront payment [8]. That puts it in the virtual-assistant (VA) price band, the same as Athena or Wing.

**The pivot (2022 onward).** OpenAI brought Invisible in for model fine-tuning in 2022. That led to contracts with Amazon, Microsoft, Cohere and other labs [9]. A typical task: trainers reviewed model conversations, flagged incorrect or offensive messages, rated responses 1–7, and wrote an ideal response. Internal quality reviewers checked that rewrite before it went to OpenAI. The network was then about 5,000 contract trainers in 100+ countries [1][22]. Business Insider reported in 2023 that Invisible cut 31 contractors when OpenAI reduced its contractor ranks [10]. That cut shows how concentrated its customers were.

**Traction and financials:**

| Metric | Figure | Source quality |
|---|---|---|
| Revenue 2023 | ~$60M | Sacra estimate [9] |
| Revenue 2024 | ~$134M (+123%) | Sacra estimate [9] |
| EBITDA 2024 | ~$15M (~11% margin) | Sacra [9] |
| Contractor pay as % of revenue | 60–70%, implying roughly 30–40% gross margin | secondary summary of Sacra [9]; the margin is my inference |
| Peer gross margins (for comparison) | Scale AI 50%+; Handshake's AI-data unit ~30% | Sacra [9] |
| Sept 2025 round | $100M led by Vanara Capital, valuation >$2B (Bloomberg) | press release + press [11][12] |
| ARR, Dec 2025 | ">$100M" (TechCrunch, per aggregator) | conflicts with the 2024 estimate [13] |
| Run rate, Sept 2026 | ">$350M" (company figure); Latka shows $336M | unverified [13][14] |
| Claimed 2025 revenue | $1.2B | one aggregator; almost certainly wrong [13] |
| Ownership | Pedraza borrowed against the company to buy out early VCs; ~300 current and former employees held 55% (Feb 2025) | Forbes / Contrary [1][15] |
| Headcount | 250 (Contrary) vs 3,906 (aggregator) | conflicting; the gap is employees vs contractors [1][16] |

**Leadership.** Benjamin Plummer was CEO before 2025. Matt Fitzpatrick, formerly head of McKinsey's QuantumBlack Labs, became CEO in January 2025. Pedraza became chairman [17][18]. Kit Colbert, VMware's former CTO, joined as Platform CTO with the 2025 round [12].

**Current platform (2025–2026).** Invisible now runs two linked businesses. One sells training data, evaluations and RL environments to model builders. The other deploys agents plus human experts into enterprise operations [12][19]. The five platform modules:

- **Neuron:** data layer that integrates and cleans structured and unstructured data. Vendor claim: it cleaned and structured 750 scattered tables in one week [19][20].
- **Atomic:** workflow and process mapping/building.
- **Axon:** agent execution, with tool calling and multi-step reasoning.
- **Synapse:** model evaluation.
- **Meridial:** marketplace of human experts (law, finance, coding, STEM) that takes "the remainder" agents can't do. It is also the contractor payment platform.

Pricing is quote-based. One directory lists roughly $10/hour for basic tasks, $30–60+/hour for professional tasks and a ~$2,000/month minimum [7][21]. Sacra frames the CEO change as a move from AI-lab data, which labs are replacing with synthetic data, toward large enterprises such as financial institutions. Other sources show the labs business is still large [9][13].

## Loop comparison

| Aspect | Invisible's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | 2015–21: process = sequence of steps; each step run by a human agent or a bot, swapped over time ("digital assembly line"). Now: Atomic maps the workflow, Axon agents run steps, Meridial experts take the remainder. | **Same frame**, earliest real implementation. Unit is a linear process per client, not a whole-business graph. |
| A2 Observation | A human ops person "silently watches you while you work and writes down instructions"; clients delegate by email or Slack. Now Atomic does workflow mapping (vendor). | **Different / worse for SMB**: manual ethnography, not event-log mining. No missing-edge mechanism. |
| A3 UX | Client delegates through channels it already uses (email, Slack); Invisible's agents work inside Invisible's own tooling. | **Different**: no-new-box for the *client*, but the work moves out of the business to Invisible's workers. Cyclical keeps the business's own staff in their own tools. |
| A4 Permissions | Not public; clients hand over credentials and access to the outsourcer (from memory: common VA practice). | **Absent** |
| A5 Shadow eval | None public. Human output was checked by internal QA reviewers, not against outcomes. | **Absent** |
| A6 Checkoff / anti-rubber-stamp | Layered human QA: trainer output → internal quality reviewers → client (RLHF). Contractors are rated and moved between projects. | **Different**: strong on grading *humans*; no seeded-bad-output method found. |
| A7 Graduation | No statistical threshold found; automation decided by engineering judgment. | **Absent** |
| A8 Replacement levels | Explicit "automate steps over time; unit price falls." Bots replace repetitive sub-steps (≈ Cyclical level 3, deterministic code). Now Axon agents (≈ level 1–2). | **Same idea, cruder**: no per-case-type graduation; code was maintained by hand, not regenerated from a contract + tests. |
| A9 Orchestrator agent | Human ops managers redesigned processes; the 2018 post says agents "build, execute and upgrade" processes. | **Different**: humans did it. No agent proposes reorganizations. |
| A10 Shared context | Neuron (business-wide data layer) for enterprises. | **Similar**, enterprise-scale data work. |
| A11 Cross-business pooling | Pooled *workforce* (the human exception desk, in effect), shared across clients. No pooling of *outcomes*: each client process was bespoke. | **Half**: has the pooled human desk, lacks pooled outcome learning. No vertical. |
| A12 Anti-Goodhart | None public. | **Absent** |
| A13 Model-agnostic | Sells to all labs; Axon is model-neutral (vendor framing). | **Same** |
| A14 Business model / moat | Margin on labor (30–40% GM, inferred) with automation as the margin lever. Moat = recruiting, vetting and QA of a 5,000+ person expert pool and lab relationships. Targets enterprises and AI labs. | **Different**: moat is the workforce, not outcome history. Opposite end of the market. |

**A1/A8: same frame, opposite result.** Invisible had Cyclical's idea (a step can be done by a human or a machine, and machines take over step by step) eight years early, at real scale (600+ processes in 2018) [3]. After seven years most of the revenue was still human labor. The 2024 data says contractor pay was still 60–70% of revenue [9]. The automation lever did not move margins enough to change the business. Three reasons follow from the record:

- **Bespoke processes.** Each process belonged to one client and ran at that client's volume. The realizations.md arithmetic applies: no single process ever accumulated enough runs to justify building and maintaining automation for it.
- **Pre-2022 bots were brittle code.** Every automated step was a hand-maintained integration. Cyclical's "regenerate from contract + tests" (A8) answers exactly this problem, and it only became possible with code-writing models.
- **A better use for the humans appeared.** Labs paid more per human hour for judgment than SMB clients paid for VA work. Labor was the product the market wanted.

**A6: Invisible is ahead on grading humans.** Its RLHF business is a QA pipeline for human judgment work: rating scales, ideal rewrites, a second-layer quality reviewer, per-contractor quality scores used to route projects [1][10]. Cyclical's stage 2 assumes checkers can be graded with seeded bad outputs, and Invisible's operating knowledge (how quickly reviewers drift, what share of output needs re-review) is the closest real data on that. Labelling vendors commonly seed tasks with known answers (often called "honeypots" or "gold tasks") to catch inattentive workers. Invisible very likely uses them (from memory; industry practice, not a confirmed Invisible feature). Cyclical's ~1-in-50 seeding is the same technique pointed at staff checking agent output.

**A11: they pooled the people, not the outcomes.** Invisible's shared workforce is exactly realizations.md's "central exception desk of leftover humans shared across businesses." It shows the desk can run profitably at an 11% EBITDA margin across 100+ countries [1][9]. It also shows what the desk alone does not give you: compounding learning. Without a common process definition across clients, there was nothing to pool except labor.

## Where they're ahead of Cyclical

- **A working human pool at scale.** About 5,000 vetted contractors in 100+ countries, with routing, payment (Meridial) and per-person quality scores [1]. Cyclical's pooled exception desk (~1,300 people for 10,000 clinics, *rough*) is a smaller version of what Invisible already runs.
- **A business that already earns from humans checking AI.** RLHF is paid stage-2/stage-1 labor. Invisible gets paid while the automation isn't ready yet, a bridge Cyclical's plan does not yet have.
- **Revenue and capital.** ~$134M in 2024, profitable, >$2B valuation, a McKinsey-trained CEO selling to financial institutions [9][11][17].
- **Neuron data-cleaning work.** Enterprise data is messier than anything in a 9-person dental clinic. The "750 tables in a week" claim is vendor-sourced [20], but it is the kind of step Cyclical skips by staying inside a single practice-software vendor's schema.

## Where they're doing it differently (and whether their way is better)

- **Outsource versus augment.** Invisible takes work *out* of the client to its own workers. Cyclical keeps the clinic's staff and changes which of their steps agents take over. For a small business that wants to cut headcount, outsourcing is simpler to buy ("$X/hour, someone else does it"). Invisible's 2018 SMB pricing ($9–15/hour) shows that price band works [8]. For a dental clinic, where front-desk staff are also the patient-facing people, Cyclical's approach is likely better. Outsourced front desks (offshore dental VAs) already exist, and Cyclical has to beat them on cost.
- **Human ethnography versus log mining (A2).** Invisible's "silently watches you" onboarding captures steps that never touch a log (phone calls, judgment calls). Log mining misses those. Cyclical's missing-edge flags are meant to cover the gap, and Invisible's history suggests a human onboarding pass is still needed early on.
- **Enterprise versus SMB.** Invisible moved upmarket after the pivot, because enterprise contracts pay for bespoke process work. For Cyclical's dental focus, being upmarket is a reason Invisible won't compete, not a better strategy.

## Feedback & reviews on these parts of the loop

**Workforce and QA side (A6, A11). Independent, worker reviews:**
- Glassdoor, AI Data Trainer: pay and benefits 3.1/5 (n=53), 49% would recommend. Pros: fast payment, flexible hours. Cons: no job security [10].
- Indeed, Trainer: pay 2.5–2.6/5 (n=8–31 depending on filter). "Agents can be moved between different projects with little or no notice and pay scale can vary accordingly" [10]. Quality-based routing looks like arbitrary reassignment from the worker's side.
- Trustpilot: Meridial 1.5/5 (n=35), Invisible 2.3/5 (n=10) [10].
- A posted pay range of "$6-to-$65 per hour" based on experience and *geography*. Workers report offers of $6–20 [10]. The margin depends on paying different rates by geography.

**Pivot and concentration risk. Independent press:**
- Business Insider (2023, via secondary source): 31 contractors cut when OpenAI reduced contractor ranks [10]. A pooled human desk tied to one buyer swings with that buyer.
- Sacra: the move to enterprise is partly a hedge against labs moving to synthetic data [9].

**Customer side (A1, A8).** Weak evidence. A review aggregator listed the consumer-era plans [8], but I found no customer reviews on whether unit prices actually fell as automation increased. That claim is unverified, and its absence from the record is itself evidence. **Vendor-sourced:** the "600+ processes" and "costs fall over time" claims [3][4], and the Neuron "750 tables" example [20].

Not reached: Reddit (r/WFHJobs, r/remotework threads on Invisible trainers exist, from memory), and HN threads on Pedraza's 2017–2019 posts.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraints.** Pedraza started with a VA service and a theory: start with coordinated human labor, automate the steps behind it. The constraints that shaped the company:

- **Horizontal by design.** "Delegate any process" meant each client's process was a one-off.
- **Pre-LLM automation.** Each automated step was hand-written code that broke when the client's tools changed. The cost of automation scaled with the number of processes, while the payoff came from volume per process. With no shared processes, the payoff never arrived.
- **VCs pushed back on "services."** Pedraza bought them out, so Invisible had to stay profitable on labor margins [1][15].

When OpenAI needed thousands of vetted people doing quality-checked judgment work in 2022, Invisible's actual asset (recruiting, QA and routing of remote humans) fit exactly. Revenue roughly doubled in a year [9]. The pivot was market pull meeting the asset the company really had, not the asset it had pitched.

**What this says about "run other businesses' processes with a human + machine mix":**

1. Without a shared process definition across customers, automation is a cost centre and the business stays a labor-arbitrage services firm (30–40% gross margin). This is the strongest outside evidence I've seen for Cyclical's "one vertical, pool outcomes" decision.
2. The pooled human desk is a real, profitable business on its own, but it is a services business. Cyclical should treat its exception desk as a cost of operating the system, not as its moat.
3. Grading humans comes before grading agents. Invisible built the human QA machinery first because it was paid for. Cyclical's stage 1–2 evals need the same machinery (gold tasks, per-checker accuracy, routing by quality).

**Copy:**
- The pricing promise "unit price falls as we automate." Tie Cyclical's price per clinic to steps graduated, so clinics see the automation.
- Per-worker quality scoring and routing for the exception desk.
- The human onboarding pass for steps that leave no log.

**Avoid:**
- Bespoke processes per client.
- Hand-maintained automation.
- Dependence on one buyer (the OpenAI contractor cuts).
- Letting the human desk become the product.

**Exploit:** Invisible has moved upmarket (financial institutions, government, AI labs) and has no vertical SMB product. Dental is far from its customer base.

**Threat level: low (about 10% that Invisible competes in SMB dental within 3 years).** Signals that the threat is rising:

- Invisible launches a packaged vertical offering for SMBs (healthcare front office, dental or medical billing).
- Atomic/Synapse start publishing cross-client benchmarks from outcome data. That would mean it has found pooling.
- It acquires an offshore dental VA or RCM (revenue-cycle management: insurance claims and collections) provider.

**Other close analogues (brief; mostly from memory, unverified this session):**

- **Fin (Sam Lessin, 2015–2020):** human operators plus automation behind an assistant. It pivoted to "Fin Analytics," workforce analytics measuring operator work, then wound down. It is the purest case of the A1+A8 thesis failing pre-LLM, and of the instrumentation outliving the service.
- **x.ai ("Amy") and Facebook M (shut 2018):** human trainers behind "AI" assistants. Automation never caught up with the long tail of cases. x.ai was sold to Bizzabo in 2021.
- **CloudFactory:** managed workforce in Nepal and Kenya that moved from business-process outsourcing to AI data labelling, the same pivot as Invisible.
- **Athena (EAs at ~$3k/month) and Wing Assistant (~$500–1k/month VAs):** pure human pooling, now adding AI. They show what SMBs will pay for a pooled human, which caps what Cyclical can charge before staff are actually cut.
- **Hyperscience (document processing):** routes each field to a machine or a human by confidence threshold, against an accuracy target the customer sets. It is the closest commercial analogue to A7's per-case-type graduation. **Hyperscience is probably worth its own analysis if it isn't on the orchestrator's list.**

## Sources

1. https://research.contrary.com/company/invisible (via search summary)
2. https://medium.com/invisible/executive-summary-47d7d8d3d1bf and https://medium.com/invisible/we-can-automate-your-work-7e9ffa06b77c (via search summary)
3. https://medium.com/invisible/invisible-technologies-a05f8005621d (via search summary)
4. https://medium.com/invisible/the-strategy-for-2019-2020-and-beyond-8de4253d2e2e (via search summary)
5. https://www.forbes.com/sites/frederickdaso/2020/11/02/invisible-technologies-ceo-francis-pedraza-believes-the-future-of-business-is-worksharing/
6. https://sacra.com/c/invisible/
7. https://tooldirectory.ai/tools/invisible-technologies
8. https://www.virtualassistantassistant.com/invisible-technologies/
9. https://sacra.com/research/invisible-at-134m-in-revenue/ and https://sacra-pdfs.s3.us-east-2.amazonaws.com/invisible.pdf (via search summaries)
10. https://www.glassdoor.com/Reviews/Invisible-Technologies-AI-Data-Trainer-Reviews-EI_IE2342977.0,22_KO23,38.htm ; https://www.indeed.com/cmp/Invisible-Technologies/reviews?fcountry=ALL&fjobtitle=Trainer ; https://origindatapartners.com/guides/invisible-technologies-review ; https://aitraining.jobs/platforms/invisible-technologies
11. https://aibusiness.com/data-management/invisible-technologies-secures-100m-ai-training-platform
12. https://www.businesswire.com/news/home/20250916425748/en/Invisible-Technologies-Raises-$100-Million-to-Power-the-Next-Generation-of-AI-Infrastructure-for-the-Enterprise
13. https://enterprisedna.co/resources/ai-map/company/invisible-technologies/ ; https://aitraining.jobs/expert-data/vendors/invisible-technologies
14. https://getlatka.com/companies/invisible-technologies
15. https://www.forbes.com/sites/iainmartin/2025/02/04/this-ai-founders-audacious-plan-to-buy-out-his-own-vcs/
16. https://growthengineer.ai/startups/invisible-technologies
17. https://invisibletech.ai/blog/invisible-technologies-appoints-matt-fitzpatrick-chief-executive-officer
18. https://www.executivebiz.com/articles/matthew-fitzpatrick-invisible-technologies-chief-executive-officer
19. https://www.nextfor.ai/products/invisible-technologies-inc
20. https://techtalksnetwork.com/podcast/tech-talks-daily/episode/invisible-technologies-ceo-on-building-ai-around-real-workflows-not-hype
21. https://www.saasworthy.com/product/invisible-technologies/pricing
22. https://en.wikipedia.org/wiki/Invisible_Technologies (via search summary; source of the 5,000-trainer and 1–7 rating details)
