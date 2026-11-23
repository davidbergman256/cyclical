# Analysis: OpenAI Frontier (+ AgentKit/Evals, RFT, Thrive Holdings as strategy)

Frontier is a sales-led platform for Fortune-500 companies. It gives agents (OpenAI's, in-house or third-party) a shared business context, an execution runtime, an identity with permissions, and a human-review feedback loop. **Overlap with Cyclical: 4/10.** It shares the "agents are coworkers inside a business" frame and the identity/context plumbing. Its evals grade against human review inside one company. It publishes no outcome grading, no statistical graduation and no per-case-type autonomy. Its enterprise data terms rule out cross-customer pooling. realizations.md §4 overstates what Frontier does (correction below). The most important lesson does not come from Frontier. It comes from OpenAI's other move: **Thrive Holdings, where OpenAI embeds engineers in roll-ups of accounting and IT-services firms it part-owns.** That is the lab's own admission that outcome data in a vertical has to be owned, not bundled. It is also the shape the real threat to Cyclical would take.

**Research limits (read first).** This session could not fetch pages: openai.com, techcrunch.com and the review blogs all failed DNS under the network allowlist. The shared web-search budget ran out after about 8 queries. Everything below comes from search-result excerpts, which are cited, or from my training knowledge (cutoff mid-2026), which is marked *(from memory)*. Facts from after about June 2026 are thin. I found no G2/Capterra reviews of Frontier, and with no public pricing and sales-only access, few would exist.

## Correction to realizations.md

The claim is: *"OpenAI Frontier (Feb 2026) already ships an agent platform with evals and self-improvement that manages other vendors' agents."*

- **"Ships."** Only partly. At launch (Feb 5, 2026) it was "available today to a limited set of customers, with broader availability coming over the next few months" [1][3]. A third-party page reports that as of Oct 10, 2026, OpenAI's Frontier page still lists no availability tiers or dates and sends buyers to sales [8]. Pricing has never been published, and the CRO declined to discuss it at launch [8][9].
- **"Evals."** Yes, but they grade against human judgment. OpenAI's wording is "built-in ways to evaluate and optimize performance" so that "people and agents" can see "what's working," and "good behaviors strengthen over time" [1][5]. TechCrunch describes "a feedback loop that is meant to help them improve over time the same way a review might help an employee" [2]. The model is a performance review: a human manager grades the agent. OpenAI has published nothing showing Frontier evals graded against world outcomes (paid, showed up, claim accepted). An integrator could wire an outcome signal in as a custom metric, but the product has no notion of it.
- **"Self-improvement."** It means memory and behavior tuning, not learning. "AI coworkers build memories, turning past interactions into useful context" [5]. A third-party explainer gives the example of a user's edit to an agent draft being kept as a signal of "what good looks like," and says it is "not training the base model; it's tuning the agent's behavior" [5] (third-party, unverified). That roughly matches Cyclical's level 2 (per-business retrieved examples). It is supervised by edits and has no gate on outcomes.
- **"Manages other vendors' agents."** Yes (vendor claim). TechCrunch: users "can manage agents built outside of OpenAI too" [2]. Launch partners listed as "Frontier Partners" included AI-native app vendors such as Harvey, Sierra, Decagon, Abridge, Ambience and Clay *(from memory)*.
- **Per-case-type autonomy, statistical graduation thresholds, rubber-stamp detection, anti-Goodhart guardrails, cross-customer learning:** none found in any source. Cross-customer learning is ruled out by design. OpenAI's enterprise commitment is that business data is not used for training by default *(from memory; long-standing ChatGPT Enterprise/API policy)*, so Frontier cannot pool one customer's outcomes to improve another's agents.

A corrected line for realizations.md: *"OpenAI Frontier (Feb 2026, sales-led, limited availability) gives enterprises a shared context layer, agent identity/permissions, memory and a human-review feedback loop that also manages third-party agents. It grades agents the way a manager reviews an employee, not against outcomes, and its data terms forbid pooling across customers."* The "first version fails" argument in §4 still holds, because the agent-wrapping layer is being bundled. It now holds for a narrower reason.

## What it actually is

**Frontier (launched Feb 5, 2026).** OpenAI's pitch is that it "gives agents the same skills people need to succeed at work: shared context, onboarding, hands-on learning with feedback, and clear permissions and boundaries" [1][4]. Coverage describes four parts [3][6]:

| Part | What it does (as described) |
|---|---|
| Business context | Connects "siloed internal applications, ticketing tools and data warehouses" into a "shared business context" [4]. Elsewhere it is described as a semantic layer every agent can reference and "durable institutional memory over time" [3]. |
| Agent execution | Runtime where agents reason over data, use files, run code and call tools, on local, cloud or OpenAI-hosted environments *(from memory)*. |
| Evaluation & optimization | Human-visible quality tracking, a feedback loop and memories [1][2][5]. |
| Security & governance | "Each agent gets its own identity with explicit permissions and guardrails" [3]. |

**Buyers and traction.** Early adopters named by Bloomberg include Intuit, State Farm and Thermo Fisher Scientific [3]. Launch coverage also named HP, Oracle and Uber *(from memory)*. BBVA, Cisco and T-Mobile were described as pilots [6]. **No outcome numbers are published for any named customer.** The results OpenAI cited all come from unnamed customers [6]:
- a manufacturer cut production-optimization work from six weeks to one day;
- an investment firm's agents freed "over 90% more" sales time;
- a hardware firm cut root-cause analysis from about 4 hours to minutes.

One guide maps BBVA to financial-services automation, Cisco to network management and T-Mobile to customer service, but other sources do not confirm it [6]. Delivery runs through OpenAI forward-deployed engineers (FDEs: OpenAI engineers placed on site to build with the customer) [3]. Within weeks OpenAI signed "Frontier Alliances" with four large consultancies [7], which I recall as McKinsey, BCG, Accenture and Capgemini *(from memory)*. Commercially, Frontier is OpenAI's lever for raising enterprise share of revenue. Executives talked of enterprise growing from about 40% of revenue toward 50% in 2026 *(from memory, rough)*.

**AgentKit (DevDay, Oct 2025)** *(from memory)* is the developer-side kit:
- Agent Builder, a visual canvas for multi-agent workflows;
- Connector Registry;
- ChatKit, an embeddable chat UI;
- expanded Evals: datasets, *trace grading* (scoring each step of an agent run against a rubric), *automated prompt optimization* (rewriting prompts from graded results and human annotations), and grading of third-party models.

Graders come in four kinds: string match, Python functions, LLM-as-judge rubrics and human annotation. Any of them can grade against ground-truth labels the developer supplies. Outcome grading is therefore *possible*, but only if the developer brings the outcome labels.

**Reinforcement fine-tuning (RFT)** *(from memory)* trains OpenAI reasoning models (o4-mini at GA, May 2025) against a developer-written grader. Agentic RFT with tool calls was announced at DevDay 2025. Showcased users included Ambience (medical coding), Harvey (legal) and Accordance (tax/accounting). RFT produces OpenAI-hosted weights, so it is the opposite of model-agnostic.

**OpenAI SMB-facing products** *(from memory)*:
- ChatGPT Business (renamed from Team in 2025), with connectors to email, calendar and drive;
- ChatGPT agent (July 2025), a general browser and computer agent;
- apps inside ChatGPT.

None of these is a vertical process product, and none grades against outcomes. I found no evidence of a dental-specific OpenAI product.

**Thrive Holdings (Dec 2025)** *(from memory; a separate agent covers Thrive itself)*. OpenAI took an ownership stake in Thrive Capital's operating holding company, which buys and runs services firms. The two named roll-ups are Crete Professionals Alliance (accounting) and Shield Technology Partners (IT services). OpenAI embeds its own researchers and engineers to rebuild the firms' work around AI, and is paid in equity that grows with Thrive Holdings. The relevance here: it is the one OpenAI move where the lab gets **operating data and outcomes inside one vertical, across many firms, with the rights to use them**. That is exactly what Frontier's enterprise terms forbid.

## Loop comparison

| # | Aspect | Frontier / OpenAI approach | vs Cyclical |
|---|---|---|---|
| A1 | Core frame | "AI coworkers" onboarded like employees. Agents and people coexist, but there is no explicit process graph and no notion of a node that a person or an agent can occupy interchangeably. Agent Builder graphs are agent workflows, not business graphs. | Different (narrower) |
| A2 | Observation / onboarding | Connectors to warehouses, CRMs and ticketing feed *context*. Nothing discovers the process from event logs and nothing flags missing edges. FDEs and consultancies map the process by hand. | Absent (replaced by FDE labor) |
| A3 | UX | Agents live in ChatGPT/Frontier surfaces and in customer apps (ChatKit). Draft-edit capture exists as a feedback signal [5]. There is no "your drafts folder is the approval queue" design, and no orchestrator/node views. | Different |
| A4 | Permissions | Per-agent identity with explicit permissions and guardrails [3]: a static, admin-set IAM model. No just-in-time grants between nodes, no frequency signal, no removal of unused grants. Nothing published on rules-not-wording approvals beyond generic prompt-injection guardrails. | Same on identity; worse on dynamics |
| A5 | Shadow eval vs outcomes | Human review loop. AgentKit Evals *can* grade against labels the developer supplies, but nothing pulls world outcomes into a grader, and no human-vs-agent disagreement is resolved by outcome. | Worse / different |
| A6 | Checkoff & rubber-stamping | Human approval and edits feed memory. No seeding of known-bad outputs and no checker-reliability discounting found. | Absent |
| A7 | Graduation | No published statistical threshold, no autonomy per case type, no automatic demotion on model swap. | Absent |
| A8 | Replacement levels | Level 1–2 via instructions, memory and prompt optimization (AgentKit). A "level 2.5" Cyclical lacks: RFT on OpenAI weights. No automatic compile-to-code (level 3), though Codex can write code on request. No node removal (level 4). | Partial; RFT is a different path |
| A9 | Orchestrator agent | None that proposes reorganizations. That job is done by FDEs and the four consultancies, i.e. people. | Absent (humans instead) |
| A10 | Shared context layer | The flagship feature: a semantic layer across enterprise systems, plus memory [3][4]. | Better (more mature, enterprise-scale connectors) |
| A11 | Cross-business pooling | Ruled out by enterprise no-training terms. The only OpenAI route to pooled vertical outcomes is Thrive Holdings (owning the firms). | Absent in Frontier; Thrive is the analog |
| A12 | Anti-Goodhart guardrails | None published. | Absent |
| A13 | Model-agnosticism | Manages third-party *agents* [2]; AgentKit Evals can grade non-OpenAI models. Frontier's own agents, memory and RFT run on OpenAI models, and the platform's purpose is to sell OpenAI tokens. | Different (agnostic at the agent boundary, locked in at the model) |
| A14 | Business model & moat | Moat = model quality + enterprise distribution (FDEs, consultancies, ChatGPT seat footprint). Buyer = Fortune 500. Revenue = platform deals and tokens. | Opposite |

**A10 (context layer).** This is where Frontier is ahead. It treats "business context" as a product: a semantic layer over warehouses, CRMs and ticketing that every agent shares, with memory accumulating on top. Cyclical's A10 is one line in thinking.md. For a dental clinic the context layer is small: the practice software, the insurer portals, email and the calendar. Frontier still shows that the context layer is what buyers pay for first.

**A4 (identity).** Frontier gives each agent its own identity, so an agent is a principal in IAM terms rather than a borrowed human login. Cyclical needs the same: a node's occupant needs its own identity whether it is a person or an agent. Frontier stops at static grants. Cyclical's just-in-time grants, frequency signal and missing-edge proposal go further, and nothing in Frontier answers the open "who answers for a system node" question either.

**A5–A7 (the eval stages).** This is where Cyclical differs most, and where the difference is defensible. Frontier's loop is "the way a review might help an employee" [2]. The grader is a manager, so the ceiling is the manager, which is the failure mode thinking.md names for stage 1. OpenAI's own wider eval culture points the same way. GDPval (Sept 2025) grades model work on 44 occupations by expert pairwise preference, not by downstream outcomes *(from memory)*. The lab grades by expert judgment because, across thousands of enterprise tasks, it has no access to outcomes. An outcome-graded loop needs vertical-specific outcome plumbing: insurer remittances (ERA/EOB files), show-up records, bank deposits. A horizontal platform will not build that plumbing.

**A8 (replacement).** RFT is a real alternative to Cyclical's "retrieved examples, no fine-tuning" choice. At enterprise volume (tens of thousands of graded runs) RFT can beat prompting. At clinic volume (hundreds of runs) it cannot, and it ties the asset to one vendor's weights. Cyclical's choice holds for SMBs. With a pooled set of 10,000 clinics, though, a pooled RFT run on an open-weight model becomes feasible, and that option should stay open.

## Where they're ahead of Cyclical

- **Distribution and delivery capacity.** FDEs plus four global consultancies [7], and a ChatGPT seat footprint already inside most enterprises. Cyclical has none of this.
- **Context-layer engineering** (A10) and **agent identity** (A4) are built and in pilot at banks and telcos [3][6]. Cyclical has these on paper.
- **Grader tooling.** AgentKit trace grading, prompt optimization and RFT graders are mature. Cyclical should *use* them, or their open equivalents, rather than build them. Task-level evals are commoditized, as realizations.md already says.
- **Third-party agent management.** Frontier already treats outside agents as managed occupants, which is half of A1. Cyclical's graph should accept Frontier-, Claude- or vendor-built agents as node occupants instead of competing with them.

## Where they're doing it differently (and whether their way is better)

- **Humans map the process; software does not observe it.** OpenAI chose FDEs and consultancies over process mining. At Fortune-500 scale, with bespoke systems, that is rational. Process mining across SAP variants is a Celonis-sized project, and a $1M+ deal pays for engineers. At dental scale it is not: a clinic cannot pay for an FDE. **Cyclical's way is better for its market and worse for theirs.**
- **The grader is a human reviewer, not the world.** This is cheaper to set up and works where no outcome signal exists, which is much of white-collar enterprise work. It is worse wherever outcomes exist: in dental billing and recall, outcomes exist for most nodes. **Cyclical's way is better where outcomes exist.**
- **Fine-tuning (RFT) instead of retrieval.** Better at high volume with a single vendor, worse for model-agnosticism and small volume. Cyclical's way is better for SMBs.
- **Pooling by owning the firm (Thrive) instead of by software across customers.** This is the most interesting difference. OpenAI cannot pool across Frontier customers, so where it wants pooled vertical learning it buys into the operators. That is the DSO logic from realizations.md §5, run by a lab. Whether it is better depends on capital: owning firms gives full data rights and the ability to randomize (remove a role at half the firms), at roll-up capital costs. Cyclical's software-pooling route needs data-sharing consent from independent clinics. A DSO partnership or ownership route gets around that, and Thrive shows it is a live option.

## Feedback & reviews on these parts of the loop

The independent evidence is thin. Frontier is sales-only with no public pricing [8]. I found no G2, Capterra, Gartner Peer Insights or TrustRadius listings. Searches for customer outcomes at BBVA, Cisco and T-Mobile returned none [6].

- **Evals and self-improvement.** Independent coverage only restates the launch post. No reviewer has described what the evaluation layer measures in practice. The specific metrics ("accuracy, politeness, efficiency") appear only in SEO blogs and are unverified [5]. *(Independent; finding nothing is itself the evidence.)*
- **Deployment gap.** CX Today framed Frontier as OpenAI's answer to the "AI agent deployment gap" in enterprise CX [6]: enterprises build pilots, but few reach production. This fits the FDE-heavy design. *(Independent trade press.)*
- **Context and memory.** MemU's blog asks "where does institutional knowledge live?" and argues Frontier's memory sits inside OpenAI's platform [3]. *(Vendor-sourced: MemU sells a competing memory layer.)* eesel.ai published an "honest review" and a pricing guide [8] *(competitor content; I could not fetch it)*.
- **Pricing opacity.** Multiple sources say pricing is undisclosed and the CRO declined to discuss it [8][9]. *(Independent.)*
- **Agent Builder (AgentKit) developer critique** *(from memory)*. At DevDay 2025, Hacker News and developer reaction called Agent Builder an n8n/Zapier-style canvas that adds lock-in. LangChain's Harrison Chase wrote that visual workflow builders get squeezed between no-code agents and code. The critique applies to deterministic orchestration, not to evals.
- **Market reaction** *(from memory)*. Frontier, alongside Anthropic's Cowork plugins, was cited in the Feb 2026 sell-off of SaaS stocks. Investors priced it as a threat to horizontal workflow software. This is consistent with realizations.md's point that hand-built structure gets repriced while channels do not.

## Top-level: why they chose this path, and what to learn

**Starting assets and constraints.** OpenAI's assets are the best or near-best models, about a billion ChatGPT users, and enterprise seat penetration. Its revenue scales with tokens. Its binding constraint is that **enterprises will not let it train on or pool their data**, which is the price of entry to every Fortune-500 deal. So Frontier is built from what is allowed: per-customer context, per-customer memory, per-customer human-review loops, and a runtime that maximizes OpenAI token use. Managing third-party agents is the "control plane" play. If OpenAI becomes the place enterprises govern all their agents, OpenAI decides which model runs. The Fortune-500 focus follows from FDE economics: a forward-deployed engineer costs too much for any customer paying under roughly $1M a year *(rough)*.

**Implications for the "model lab bundles it for free" threat.**
- **For the agent/eval/permissions layer: real, and already happening.** Anything Cyclical builds that is a generic agent runtime, eval harness, identity system or context connector will be matched by Frontier/AgentKit, or by Anthropic and Google equivalents, at zero marginal price to the buyer.
- **For Cyclical's specific asset (pooled outcome history in dental): low in the near term, roughly 10% that OpenAI ships a pooled, outcome-graded dental process product within 3 years *(rough)*.** Four reasons:
  1. Frontier's data terms forbid pooling across customers.
  2. Its buyer is the Fortune 500, not 9-person clinics.
  3. Outcome plumbing (practice-software event logs, insurer remittances) is vertical-specific integration work that a horizontal platform will not do for a $5–10k/yr account.
  4. Outcome history takes years to accumulate, and intelligence does not speed that up.
- **The threat that matters runs through Thrive, not Frontier.** OpenAI has already shown it will put engineers inside roll-ups to get owned, vertical, outcome-rich operations. The rough probability that OpenAI or Thrive Holdings, or a lab-backed equivalent, moves into dental or DSOs within 3 years is about 15%. If it happens, it gets data rights and randomization power that Cyclical's consent-based pooling must earn clinic by clinic.

**Copy:**
- per-agent identity as a first-class principal;
- the "onboard an AI coworker like an employee" framing, which buyers understand;
- treating outside agents as managed node occupants;
- using their grader and RFT tooling, or open equivalents, instead of building it.

**Avoid:**
- competing on runtime, generic evals, context connectors or agent builders, which are bundled for free;
- an FDE-dependent delivery model, which SMB economics cannot carry. Process mining from event logs (A2) is the SMB substitute for the FDE, and it is load-bearing.

**Exploit:**
- **Frontier's graders are managers; Cyclical's grader is the insurer's remittance and the patient's show-up.** That is a capability Frontier lacks by design.
- **Frontier cannot pool; Cyclical's whole asset is pooling.** Make clinic data-sharing consent part of the product contract from day one, because it is exactly what enterprise-grade platforms promise *not* to do.
- The SMB vertical is uneconomic for OpenAI's delivery model.

**Is Cyclical a clone, subset, superset or orthogonal?** On the platform layer (A1, A4, A10, A13) it is a *subset* of Frontier's plumbing. On the learning loop (A5–A7, A11, A12) it is *orthogonal*, and arguably a superset, because Frontier publishes nothing for those aspects. In business model it is the *opposite*: Frontier sells per-enterprise capability; Cyclical accumulates cross-enterprise outcome history.

**Observations that would tell David the threat is rising, in order of severity:**
1. OpenAI or Thrive Holdings announces a dental, DSO or healthcare-front-office roll-up or partnership.
2. OpenAI enterprise terms add an opt-in "industry benchmark" or pooled-learning program, so customers trade data for better agents.
3. Frontier or ChatGPT Business adds outcome-linked grading (e.g. "connect your billing system to grade agents on collections") or per-case-type autonomy gates.
4. OpenAI ships a certified connector for Open Dental, Dentrix or Eaglesoft, or a practice-software vendor (Henry Schein One, Patterson) announces Frontier as its agent layer. That would combine the system-of-record risk in realizations.md §6 with the lab's distribution.

## Sources

1. OpenAI, "Introducing OpenAI Frontier," Feb 5 2026: https://openai.com/index/introducing-openai-frontier/ (seen via search excerpts only; fetch blocked)
2. TechCrunch, "OpenAI launches a way for enterprises to build and manage AI agents," Feb 5 2026: https://techcrunch.com/2026/02/05/openai-launches-a-way-for-enterprises-to-build-and-manage-ai-agents/
3. Bloomberg, "OpenAI Unveils Platform to Help Companies Deploy 'AI Coworkers'": https://www.bloomberg.com/news/articles/2026-02-05/openai-unveils-platform-to-help-companies-deploy-ai-coworkers ; MemU blog (vendor): https://memu.pro/blog/openai-frontier-agent-platform-memory ; TechInformed: https://techinformed.com/openai-launches-frontier-to-manage-enterprise-ai-agents/
4. CNBC, "OpenAI launches Frontier in bid to win more business customers": https://www.cnbc.com/2026/02/05/open-ai-frontier-enterprise-customers.html ; TechRadar: https://techradar.com/pro/openai-introduces-frontier-an-easier-way-to-manage-all-your-ai-agents-in-one-place
5. Third-party explainers on evals and memory (unverified detail): https://growwstacks.com/blog/openai-frontier-ai-agent-coworkers ; https://www.gend.co/blog/introducing-openai-frontier-enterprise-ai-agents ; https://www.datacamp.com/blog/openai-frontier
6. CX Today, "OpenAI Frontier Tackles AI Agent Deployment Gap in Enterprise CX": https://www.cxtoday.com/contact-center/openai-frontier-ai-agent-deployment-enterprise/ ; Digital Applied guide: https://www.digitalapplied.com/blog/openai-frontier-enterprise-ai-agent-platform-guide ; AI Business: https://aibusiness.com/agentic-ai/openai-s-latest-platform-targets-enterprise-customers
7. TechInformed, "OpenAI signs Frontier Alliances with four major consultancies": https://techinformed.com/openai-signs-frontier-alliances-with-four-major-consultancies/
8. eesel.ai pricing guide and review (competitor content): https://www.eesel.ai/blog/openai-frontier-pricing ; https://www.eesel.ai/blog/openai-frontier-review ; HappyRobot: https://www.happyrobot.ai/hub/what-is-openai-frontier ; nxcode guide: https://www.nxcode.io/resources/news/openai-frontier-enterprise-ai-agent-platform-guide-2026
9. SiliconANGLE, "OpenAI introduces Frontier agent management platform and new GPT-5.3-Codex model": https://siliconangle.com/2026/02/05/openai-introduces-frontier-agent-management-platform-gpt-5-3-codex/

Items marked *(from memory)* (AgentKit/Evals features, RFT details, GDPval, Thrive Holdings structure, Frontier Partners/consultancy names, enterprise revenue share, Feb 2026 SaaS sell-off) were not re-verified in this session.
