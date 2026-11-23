# Analysis: all incumbents — what exists, what's missing, and what it means for Cyclical

**Verdict.** Cyclical is not a clone of anyone, and nobody among the ~120 companies covered in 33 analyses runs its whole loop. But almost every *piece* of the loop is already shipping somewhere, and several pieces Cyclical treats as core are now commodity. The interchangeable human/agent graph (A1) is sold by UiPath, Camunda, ServiceNow, Palantir and Microsoft. Shadow → approval → autonomy staging is how hospitals and Notable already describe their rollouts. Just-in-time agent permissions are being bought up by Workday (C1) and ServiceNow (Veza). Drafts-in-your-inbox UX ships in Fyxer and Lindy. What nobody does is the combination that actually produces the asset: **grade both humans and agents against what the world reports (payments, show-ups), certify per case type with a statistical bar, and pool those outcomes across many small businesses running the same process so you can run experiments no single business can.** Sorting incumbents by why they don't do it gives the main strategic result. The horizontal platforms *can't* pool, because their enterprise contracts forbid it, and they don't need to, because each customer has enough volume. The vertical systems of record *won't* run role-removal experiments, because they sell seats to the offices whose roles would go. The roll-ups *can* do all of it, by owning the businesses, and in dental the roll-up already exists: it's called a DSO.

Four findings change the thesis rather than confirm it:

1. **Pooled outcome history in payer behavior is real but not a moat on its own.** athenahealth ran exactly this play in medicine for 20 years (denials across the network → rules for everyone, priced on collections). It worked operationally and still lost the market. Payer knowledge saturates, clearinghouses see it at higher volume, and the buyer (independent practices) got absorbed by owners with a different system. The pooled assets that *don't* saturate, and that no clearinghouse sees, are randomized structural experiments (can this role go?), early detection of payer rule changes, and fast re-certification after model swaps. Lead the moat pitch with those.
2. **The first customer is almost certainly a DSO.** Eight independent analyses reached this separately: DSOs, General Catalyst, Thrive, athenahealth, Palantir, Aera, Stripe, Teamshares. A DSO is a ready-made pool of 50–1,700 offices with one decision-maker. It already owns the system-of-record question, can authorize randomized role-removal tests, and buys like a mid-enterprise. The same analyses flag DSOs as the likeliest competitor if one builds this in-house.
3. **The closest dental company found is Lassie (overlap 6/10).** It runs payment-posting agents in 700+ practices, graded on cash confirmed in the bank. It charges a reported 2% of posted insurance collections plus $3k per location (~$10M run rate). It rolls out one insurer at a time, which is per-case-type graduation decided by the customer's trust rather than statistics, and its lead investor (a16z) calls the goal "the small business that runs itself." It is a *subset* in scope: one subgraph, no graph, no orchestrator, exceptions left to each practice's own staff, and no visible cross-practice pooling. It is a *superset* in reach, since it is moving into medical practices on the same process. Two limits on its position. Its answer key is not exclusive: posted payments land in the PMS ledger and deposits in the bank feed, so Cyclical can read both at its own clinics. And it cannot grade upstream steps (eligibility, coding, submission) because it lacks their run logs. That makes it a natural partner: Cyclical's upstream logs plus Lassie's remittance outcomes can attribute denials to the step that caused them. The threat rises sharply if it launches eligibility and claims (~60% within 12 months per the Lassie file) or the front office (~20%). See `analysis-lassie.md`.

A fourth finding reframes the pitch. **Enterprises are their own pool** (`analysis-notable.md`, `analysis-sierra.md`, `analysis-aera-technology.md`). A health system running ~10–20k agent runs a day, or a 500-office DSO, can graduate common case types and randomize across its own sites without anyone else's data. So Cyclical's moat lives specifically with independents and small groups, about 86% of US dentists in 2023 but shrinking as DSOs grow. The cleanest one-line positioning that came out of the research: **Cyclical is a virtual DSO.** It gives independents the pooled back office and pooled learning a DSO gets by buying practices, without the change of ownership.

> **Research caveats, stated once.** Every subagent hit the same limits. The web-search budget ran out after about 6–12 queries per agent, and the session network blocked direct fetches of most vendor sites, SEC filings, Reddit, G2 and Gartner. Most facts therefore come from search-result extracts. Each file marks what is "(from memory)" or "(vendor claim)", and almost every outcome number in the market is a vendor claim with no published denominator. My overall probability that a closer clone exists that we missed is about 25%, concentrated in 2026 YC/seed batches whose directories couldn't be browsed. A rerun with ycombinator.com, sec.gov and reddit.com allowed would tighten this.

---

## 1. The map: every incumbent, scored

Overlap is each analysis's 0–10 score for "how much of Cyclical's loop and business they already are." Threat is to Cyclical's dental wedge specifically.

| Incumbent (file) | Category | Overlap | What they have of Cyclical | Threat to dental Cyclical |
|---|---|---|---|---|
| [Lassie](analysis-lassie.md) | Dental back-office agents | 6 | Payments subgraph graded on bank deposits, payer-by-payer rollout, 2%-of-collections pricing, 700+ practices | **Medium, rising**; also the best partner |
| [Thrive Holdings](analysis-thrive-holdings.md) | Lab-backed roll-up (accounting, IT) | 6 | Pooled corrections across 50+ owned firms improving one agent; self-rewriting harness under regression tests | Medium, rising (~25% it buys a DSO in 24 mo) |
| [ServiceTitan](analysis-servicetitan.md) | Vertical system of record (trades) | 6 | Whole job graph with outcome labels; 30+ agents; "fully automated job" metric; ~2% of revenue pricing | Template for the dental PMS threat |
| [AI-native BPOs](analysis-ai-native-bpo-crescendo-assembled.md) | Services-as-software | 6 | Pooled humans + agents, outcome pricing, per-contact-type AI capacity (Assembled) | Medium; high if a dental RCM outsourcer moves first |
| [Notable](analysis-notable.md) | Health-system "System of Work" | 5 | Staff + agents in shared flows inside the EHR; human oversight dropped after "weeks or months" by judgment; Flow Compass governance; $10/run pricing | Low for independents; medium for large DSOs (~20–25%) |
| [UiPath](analysis-uipath.md) | Agentic orchestration | 5 | Maestro: agent, robot and human as interchangeable BPMN task occupants; process + task mining | Low (moderate via DSOs) |
| [Celonis](analysis-celonis.md) | Process mining | 5 | A2 method, Context Model, Orchestration Engine; SAP fight = system-node problem at scale | Low |
| [Palantir](analysis-palantir.md) | Ontology + AIP | 5 | Business-as-graph, one action layer for people, LLMs and automation; AI FDE builds the graph | Low; medium via DSOs |
| [Intuit](analysis-intuit.md) | SMB finance system of record | 5 | Pooled data on ~100M customers, money events as answer keys, pooled human desk (QuickBooks Live) | Low–moderate (~20% enters dental by 2029) |
| [General Catalyst roll-ups](analysis-general-catalyst-rollups.md) | AI-native holdcos | 5 | Own the businesses, so own the data and the authority to experiment | Medium; high if it enters dental |
| [athenahealth](analysis-athenahealth.md) | Medical PMS + RCM network | 5 | The 20-year precedent: pooled denials → rules, % of collections, human ops desk | Low directly; the template for the risk |
| [AI-native holdcos (AGI, COVU, Numica…)](analysis-teamshares-smb-holdcos.md) | Single-vertical roll-ups | 5 | Agents across owned same-process businesses | Medium if one enters dental |
| [Dental PMS vendors](analysis-dental-pms-archy-planetdds-henryschein.md) | Dental system of record | 4 | Answer keys in their tables; agents inside the PMS; Planet DDS cross-DSO benchmarks | **High**, and they control access |
| [Dental AI agents](analysis-dental-ai-agents-weave-nexhealth-arini.md) | Single-node dental agents | 4 | Same buyer, same nodes; pieces of the loop spread across firms (Weave phones, Dental Intelligence KPIs, NexHealth pipe) | Medium, rising |
| [DSOs](analysis-dsos-heartland-pds-aspen.md) | Human version of Cyclical | 4 | Pooled back office, central call center = exception desk, cross-office benchmarks | Medium-low now, rising; **also the best customer** |
| [Microsoft](analysis-microsoft.md) | Agent identity + context | 4 | Entra Agent ID (agents with managers), Work IQ, owns the drafts folder | Moderate for SMBs on M365 |
| [OpenAI Frontier](analysis-openai-frontier.md) | Lab agent platform | 4 | Context layer, agent identity, human-review loop; *no* outcome grading or pooling | Low (~10%); real threat runs through Thrive |
| [Salesforce Agentforce](analysis-salesforce-agentforce.md) | CRM agents | 4 | "Digital labor" queue; retreat to deterministic Agent Script; 9k→5k support staff | Low-medium |
| [ServiceNow](analysis-servicenow.md) | Workflow system of record | 4 | AI Control Tower, Veza permission graph, agent flows | Low; a template for PMS vendors |
| [Workday](analysis-workday.md) | HR system of record for agents | 4 | Agents as workforce rows, Delegate/Ambient permission modes, buying C1 | Low |
| [BPM: Camunda/Pega/Appian](analysis-bpm-camunda-pega-appian.md) | Process orchestration | 4 | BPMN graph where user tasks and agent tasks are interchangeable | Low |
| [Aera Technology](analysis-aera-technology.md) | Decision intelligence | 4 | Decision Ledger (context → recommendation → accept/override → outcome) | Low (~5%) |
| [Task mining (Skan, Soroco…)](analysis-task-mining-skan-soroco-mimica-kyp.md) | Observation-based work graphs | 4 | Observe → graph → agent; Soroco "work graph" | Low (~2/10) |
| [Invisible Technologies](analysis-invisible-technologies.md) | Human + automation process outsourcer | 4 | The 2015 version of A1+A8, which never automated and pivoted | Low (~10%) |
| [Sierra (+ Decagon, Fin)](analysis-sierra.md) | Outcome-priced CX agents | 4 | Paid per outcome; pass^k reliability; immutable release snapshots | Low (~15%) |
| [Smith.ai, Ruby](analysis-hybrid-receptionists-smithai-ruby.md) | Hybrid receptionist desk | 4 | Person and AI interchangeable in the phone node; pooled human desk across thousands of SMBs | Low-moderate (~20%) |
| [YC "AI OS" startups](analysis-ai-os-startups-yc-rfs.md) | Early-stage | 4 | YC's own RFS uses Cyclical's "closed loop" language; Light Anchor pools across owned brands; Patientdesk in dental | Low today, rising |
| [Eval infra (Braintrust, Arize…)](analysis-eval-infra-braintrust-langsmith-arize.md) | Components | 4 | Plumbing for A5–A7 | Low; buy from them |
| [GoHighLevel, Podium, Vendasta](analysis-smb-ai-employee-gohighlevel-podium-vendasta.md) | SMB "AI employee" | 3 | Same SMB buyer; GHL snapshots copy one process template across thousands of businesses, but pool no outcomes | Low-moderate (watch Podium) |
| [AI-employee startups (11x, Artisan…)](analysis-ai-employee-startups-lindy-relevance-artisan-11x.md) | Horizontal agents | 3 | Vocabulary only | Low |
| [Teamshares](analysis-teamshares-smb-holdcos.md) | Cross-industry SMB holdco | 3 | Shared back office across 92 businesses | Low |
| [Agent permissions (Okta, Entra, C1)](analysis-agent-permissions-okta-entra-c1.md) | Components | 2 | Most of A4's machinery | Low; standards to follow |
| [Stripe](analysis-stripe-pooled-outcomes.md) | Pooled-outcome analog | 2 | The existence proof of the moat logic | <5% |
| [Discovery sweep](analysis-discovery-sweep.md) | — | — | Lassie, Notable, EliseAI, Harper, Hyperscience + 20 others | — |

The scores cluster at 4–6, and the maximum is 6. The pattern is a field where every serious player has two to five of the fourteen aspects, and the specific set each one has is predictable from where it started.

---

## 2. Loop step by step: who does it better, who does it differently, what the feedback says

Each paragraph covers one aspect of the rubric (A1–A14 from `thinking.md`). The detail and citations are in the individual files.

**A1. Business as graph, person and agent interchangeable.** *No longer a differentiator.* UiPath Maestro puts agent tasks, robot tasks and human tasks in one BPMN diagram for ~10,350 enterprises. Camunda 8.8 makes an agent an "ad-hoc sub-process" that can call a human as a tool. Palantir's Ontology exposes one set of "actions" that a person, an LLM function or a schedule can all call. Workday registers agents as rows in the workforce table. Smith.ai switches person and AI per call in the phone node. The difference that remains: in every incumbent a human *designs* which occupant holds a step, while in Cyclical evidence *moves* the occupant. ServiceNow's own community guidance names the "agent-driven vs workflow-driven" patterns, but occupancy is still an admin toggle. *Feedback:* UiPath has never disclosed a Maestro production count, and its net new ARR fell from $70M to $37M across three quarters while AI attach rose. Selling the frame is not the same as delivering the value.

**A2. Observation through existing tools' event logs.** Celonis and UiPath own process mining, but only on thick ERP logs at Fortune-500 volume. Celonis needs a case ID on every event, tens of thousands of cases, and enough dollars per percentage point, and it dropped its free small-business tier (Snap). Task-mining vendors (Skan, Soroco, Mimica) record screens instead, which catches the re-typing between systems that logs miss. In a 9-person clinic, though, aggregation is impossible: "the pattern" is one named biller's performance record. Press coverage of Skan's $63M round already reads "employee work monitoring." *Different and better for Cyclical:* fit each clinic's thin log to a pre-built dental template (object-centric, OCEL 2.0) and pool variant statistics across clinics (Celonis analysis). Close the portal-work gap narrowly with a browser extension scoped to insurer portals, not screen recording. Lassie's local on-prem agent next to Dentrix/Eaglesoft/Open Dental is the shipped answer for legacy practice software.

**A3. Near-zero UI; drafts land where people work.** Already a mass-market UX: Fyxer drafts into Gmail and learns from edits, Lindy moved inbox-native, Microsoft owns the drafts folder. Two incumbents add something Cyclical lacks. First, for the 12 of 14 dental handoffs that end in the practice software, "send = approve" needs a PMS equivalent, a pending change the human commits (dental PMS analysis). Second, synchronous nodes (the phone) cannot wait for approval, so stage 2 there must be live warm transfer, which Smith.ai already prices.

**A4. Permissions.** The machinery is commodity and being consolidated. Entra Agent ID gives every agent an owner and a sponsor, and access packages expire by default. Okta's Cross App Access is now MCP's enterprise authorization extension. Workday is buying C1 (just-in-time requests, logged temporary grants, unused-access revocation), and ServiceNow bought Veza for ~$1.2B. Workday's **Delegate vs Ambient** split should be adopted directly: in Delegate mode the agent uses the invoking person's permissions, in Ambient mode its own. Graduation then becomes a logged permission change. Two pieces are Cyclical's alone. One is turning request frequency into a *missing edge* rather than more access; IGA tools have no work model, so they can only answer repeated access with more access. The other is the answer to the UNRESOLVED system-node question, which the permissions analysis proposes, and I endorse it:

- the vendor's API **contract** sets the outer envelope (Dentrix API Exchange: $5k read + $5k write setup plus royalties, revocable);
- the practice owner (HIPAA's covered entity) authors a small **policy** table once, pre-filled from the pool;
- a central policy decision point (Cedar/OPA) answers most requests with no human;
- unmatched requests escalate to the **steward**, defined as *the node whose edge writes that data class into the system*. That is computed from the same event log A2 reads, so stewardship moves automatically when an edge moves.

*Feedback that changes the design:* both headline agent-permission incidents involved legitimately entitled agents with poisoned context. ServiceNow Now Assist (Nov 2025) let agents recruit other agents through default discovery. Salesforce ForcedLeak (Sept 2025, CVSS 9.4) was a web form's description field exfiltrating CRM data through a lapsed allowlisted domain. A rule on "who asks" passes both. The rule key must become (requester, data class, task type, **taint of the task's context, egress destination**). Nearly every dental front-office node reads untrusted input, touches PHI and sends messages, which is all three legs of Meta's "Rule of Two."

**A5. Shadow mode graded against the world.** *This is the genuinely rare part, and Cyclical's strongest differentiator.* Almost everyone grades against something the vendor or a human controls:

| Incumbent | What it grades against |
|---|---|
| UiPath, Salesforce | Golden answers written by people |
| ServiceNow | Its own LLM judging execution logs; its docs call this "decision support, not a deployment gate" |
| OpenAI Frontier | Human review "the way a review might help an employee" |
| Thrive's tax AI | Reviewer corrections |
| Sierra, Intercom Fin | A resolution observed in-session, billed by the vendor; critics call it "a deflection meter dressed up as a resolution meter" |
| Skan | "What top performers do" |

Those that do grade against the world are the payment-pipe owners: Stripe (chargebacks), athenahealth (remittances), Intuit (deposits), Lassie (cash in the bank). None of them grades the *human* on the same outcome. The eval-infra analysis adds one correction. The tooling to store delayed labels exists (Arize's "delayed actuals" joined by prediction ID), but nobody ships outcome *connectors with business semantics*: ERA/835 remittances, PMS show/no-show, bank deposits, outcome windows and censoring. That is a build item. Two more mechanisms from Stripe:

- *label maturity:* a claim isn't a "clean run" until its remittance arrives;
- *counterfactual exploration:* once a graduated agent decides "don't send," the world never reports what sending would have done, so keep a randomized 1–5% exploration budget per case type.

**A6. Checkoff with seeded known-bad outputs.** Gold or honeypot items are decades old in data labeling (Labelbox Benchmarks, Appen test questions), but no agent product ships them in live approval flows. **The most important evidence against the current design** is an HBS field experiment (2026, 10,088 AI-assisted drug-safety reviews, preregistered, randomized). Low-frequency error injection *reduced* reviewers' odds of catching natural AI errors by 22%, high-frequency injection *raised* them by 47%, and control reviewers caught only ~24% of real errors. Cyclical's "~1 in 50" may sit in the harmful regime (≈50% risk; the paper's exact rates weren't visible). Treat the rate as a parameter to test, not a constant. Seeded items also need a send interlock, because a seeded bad draft in a real drafts folder could actually be sent. A separate 2,784-person experiment found that requiring corrections for flagged errors *increased* acceptance of wrong suggestions. "Editing = correction" fails if edits feel like extra work.

**A7. Statistical graduation per case type.** Nobody publishes a statistical bar, though several have the per-case-type structure. Assembled plans staffing with an AI resolution rate per contact type. ServiceTitan counts "fully automated jobs" per job type. Smith.ai lets owners route new callers to humans and existing callers to AI. Hyperscience lets a customer set a target accuracy and computes a per-field confidence threshold, with sampled QA continuing after automation. That's the best control knob to copy. Three corrections from the research:

- **The audit-catch correction.** "Zero errors in n ⇒ error < 3/n" assumes every error would be seen. If checkers catch only a fraction q, the bound is ~3/(n·q). At HBS-like q ≈ 0.24–0.35, 300 clean runs certify <~9–12%, not <1%. Seeded items are the instrument that *measures* q. Where the world grades the output (remittances, show-ups), q ≈ 1 and the math holds, which is one more reason to prefer world outcomes.
- **Clustering.** Runs within one clinic are correlated, so pooled pass rates need clinic-clustered or hierarchical intervals (Anthropic's "error bars on evals": clustered SEs can be over 3× naive ones), or the pool overstates confidence.
- **pass^k.** Sierra's τ-bench showed agents at 61% pass^1 falling to 25% pass^8 on the *same* task. Replay historical cases k times as a pre-graduation check and as fast re-certification after a model swap. Simulated users are unreliable (40–47% simulator error in τ²), so simulation adds evidence but never replaces outcome grading.

**A8. What "replacement" means.** Level 3 (compile to code) is the most validated and the most transformed:

- **Salesforce:** with every model and all the data it wanted, it retreated in 2025 to hand-written deterministic Agent Script because agents dropped instructions beyond ~8 and drifted. Determinism was needed early, for *reliability*, not only cost.
- **UiPath's RPA history:** hand-maintained deterministic bots rot, which is the case for disposable code regenerated from contract + tests.
- **Thrive:** the most concrete public version of that discipline. Codex rewrites the harness (schemas, mappers) under regression evals built from reviewer corrections, keeping the model in the loop. That is easier than compiling the agent into a rule, and probably the better default.
- **Dental PMS:** fee schedules, claim scrubbers and auto-posting are already deterministic code inside the PMS, so level 3 is worth less in dental than `thinking.md` implies. Levels 1–2 matter more for the unstructured work (phones, denials, portals).
- **Distillation:** at the pooled level-1 skill (millions of runs), CoreWeave-style distillation to a small open model is the lever behind realizations' ~$99M → ~$51M compute line.

**A9. Orchestrator proposing reorganizations.** Nobody has one. Simulation of redesigns exists (Soroco Avali, Celonis + Ikigai), but calibrated on effort, not outcomes. Everyone else's "orchestrator" is a runtime router. Roll-ups reorganize by managerial decree. Keep Cyclical's "propose to a human" default: owners are liable (HIPAA, insurer fraud rules), and accepted or rejected proposals are themselves labels.

**A10. Shared context.** The most crowded category in the whole field. YC funded at least five "company brain" layers in 2026. Microsoft (Work IQ), OpenAI Frontier, Celonis (Context Model), Salesforce (Data 360) and Palantir (Ontology) all lead with it. Treat it as plumbing to buy, not build. The best independent critique (Launch HN on Hyper) says context "right on Monday is quietly wrong by Friday." An event-log graph refreshed by what happened is the answer to that.

**A11. Cross-business pooling.** The table explains the whole market:

| Who | Pools what | Why not outcomes-for-experiments |
|---|---|---|
| Salesforce, OpenAI, Microsoft, UiPath, ServiceNow, Workday, eval vendors | Nothing (or masked prompts for model training: ServiceNow) | Enterprise contracts promise data never crosses tenants; each customer has enough volume |
| Sierra | Know-how, not data | ADT alone sends 1–2M inquiries/month: one customer is its own pool |
| Aera | Nothing | One Merck makes millions of decisions; contracts forbid it |
| Intuit, Stripe, athenahealth | Outcomes, into shared prediction models | They pool to predict, not to experiment on process structure |
| Planet DDS, Dental Intelligence, Weave | Benchmarks across practices/DSOs | Sell seats to the offices whose roles experiments would remove |
| GoHighLevel | Process *templates* (snapshots) | Agencies fork each copy, so no two "dental snapshots" are the same graph by month three |
| DSOs, GC roll-ups, Thrive, Light Anchor, AI holdcos | Everything, by ownership | Could randomize; nobody publicly does |
| Smith.ai, Crescendo, Invisible, Infinx | Humans (the exception desk) | Horizontal or contractually siloed, so outcomes aren't comparable |

So the pooled *outcome-experiment* asset is genuinely unoccupied. The Sierra and Aera analyses explain why that's not an accident: **pooling is a need created by small customers.** That supports the SMB-vertical choice. The Stripe and athenahealth analyses explain why the asset is narrower than "more data." Payer-behavior and show-up prediction pools saturate. The Stripe analysis estimates (~60%) that per-clinic accuracy stops improving materially below ~1,000 clinics, and a clearinghouse already holds a bigger claims pool on day one. What keeps growing is (a) randomized structural experiments, (b) payer-policy drift detection ("the first 20 clinics to see a new Delta Dental frequency edit protect the other 9,980"), (c) re-certification after model swaps, and (d) **cold-start graduation**, which is what to sell: "a new clinic's claims agent starts already graduated on the common insurer × procedure cells, the way Radar protects a merchant on day one." Two practical constraints:

- HIPAA allows cross-covered-entity aggregation only where the BAA permits it, so write pooling into the first contract and pool de-identified outcome schemas.
- The pooled exception desk is real and runs profitably at Smith.ai, Crescendo and Teamshares. Smith.ai's ~30% escalation rate implies ~0.1–0.2 FTE per clinic *for phones alone*, which suggests realizations' ~0.1 FTE/clinic for the whole desk is optimistic.

**A12. Anti-Goodhart guardrails.** The best implementations put the guardrail in the *price* or hand it to a third party:

- athenahealth charges a percentage of collections, so downcoding cuts its own fee.
- Card networks cap Stripe's retries.
- Archy takes a share of payments.

The worst put the incentive the wrong way:

- Sierra and Fin bill resolutions, and escalations are free, so revenue rises with containment.
- Smith.ai bills $3 per AI-to-human transfer. The top customer complaint: it "transfers calls to live agents without my consent which will raise my bill."
- SDR agents optimize meetings booked and burn sending domains.

The dangerous precedent is the DSO record: pooled office metrics plus production quotas led to attorney-general settlements in NY (2015), MA (2023) and CA (2026) and overtreatment bankruptcies (Small Smiles 2012, Benevis 2020). **A pooled optimizer anywhere near treatment decisions will be read through that history.** Keep Cyclical's optimizer on the administrative graph, and say so publicly.

**A13. Model-agnosticism.** Table stakes. Sierra routes across 15+ models with failover, Stripe's labeled history survived three architecture changes, and Microsoft offers OpenAI and Anthropic. Thrive is the counterexample, contractually aligned with OpenAI, and that is an opening with DSOs who want a neutral supplier.

**A14. Business model and moat.** Outcome pricing is proven: Sierra ~$200M+ ARR, Crescendo $100M ARR (vendor), athenahealth 25 years at % of collections. The AI-native BPO analysis makes the most actionable observation in the set: **buyers don't want to operate eval stages; they want to buy a guaranteed outcome and let the vendor carry the graduation risk.** Cyclical's stages may be best sold as an outcome-priced service whose internals the clinic can audit, not as a tool the clinic runs. The system-of-record risk named in realizations §6 is fully confirmed:

- ServiceTitan is the live version in trades.
- Henry Schein One sued Vyne (Oct 2025) over a third party reading Dentrix data.
- A split preliminary injunction in 2026 barred Vyne from distributing software that *writes* back to Dentrix without authorization, while HSO may not disable Vyne's read-only functions. In one analyst's phrase: "right to read, but wrong to write." Since payment posting, drafts committed into the PMS and every other stage-3 action are writes, the authorized-write channel is the real gate.
- Dentrix's API costs $10k setup plus royalties.
- HSO's MCP "Orchestrate/Build" tiers (Apr 2026) are the door it controls.
- Celonis, at a $13B valuation, needed a lawsuit and a regulator to keep one SAP extractor open.

---

## 3. Top level: the six paths incumbents took, why, and what each teaches

Every incumbent's position follows from its starting asset and the constraint that asset imposed. Grouping them this way explains the gaps above better than the aspect table does.

### Path 1. Horizontal enterprise platforms
*UiPath, ServiceNow, Salesforce, Microsoft, OpenAI Frontier, Workday, Palantir, Celonis, Camunda/Pega/Appian, Aera.*

- **Starting asset:** an installed base inside large enterprises (robots, tickets, CRM rows, the directory, the ERP log).
- **Constraint:** customers each have their own processes and demand tenant isolation. "Your data never trains anything shared" is the price of entry to every Fortune-500 deal.
- **Result:** they sell the frame (A1), the context layer (A10), governance (A4) and task-level evals, which buyers pay for first. ServiceNow's AI Control Tower ACV grew >6× year over year; "control sells before improvement." They grade with golden answers or LLM judges because outcomes are scattered across systems they don't own. None can pool, and none needs to, because one customer is its own statistical pool.
- **Lesson:** Cyclical's pooling moat exists *only because its customer is small*. A small business's data is not competitively sensitive (a clinic 50 miles away doesn't care about your no-show rate), and its volume is too low to learn alone. That is the cleanest structural reason none of these companies becomes Cyclical. They also set the vocabulary buyers will use (agent identity, sponsor, autopilot, Delegate/Ambient), so adopt it.

### Path 2. Vertical systems of record
*ServiceTitan, Henry Schein One / Planet DDS / Archy, Intuit, athenahealth.*

- **Starting asset:** the database where outcomes land. They need no process mining and no permission, and get the answer keys free.
- **Constraint:** they're paid per seat, location or percentage, by the very offices whose staff an agent would replace. HSO also earns API royalties and runs adjacent businesses (eClaims, payments, supplies).
- **Result:** agents per module, sold as tier upgrades (Ascend Pro, Max, Intuit Intelligence). Benchmarks yes, randomized role-removal no.
- **Lesson from athenahealth:** this path executed Cyclical's pooling thesis in medicine 15 years early and showed its limit. The pool was real, it was not a moat, and the market was decided by who owned the practices (hospitals on Epic). Applied to dental, DSO consolidation plays the hospitals' role: if DSO affiliation goes from ~14% toward physician-like levels, the independent-clinic buyer shrinks the way athena's did. Sell to DSOs as well as independents from the start.
- **Lesson from ServiceTitan:** the system-of-record owner *can* build the multi-agent graph. Its bottleneck is human onboarding labor, not models: demand for full Max deployments exceeds implementation capacity.

### Path 3. Own the businesses
*DSOs, General Catalyst (Long Lake), Thrive Holdings, Teamshares, AGI/COVU/Numica, Light Anchor, Harper.*

- **Starting asset:** capital, plus a sourcing story (succession crisis, retiring owners).
- **Constraint:** cost of capital. Teamshares has $225M of perpetual preferred and $153M of debt due Dec 2026, its stock is at ~45% of the SPAC price, and organic growth is 3.6%.
- **Result:** ownership removes Cyclical's three hardest problems in one move: consent, the system-of-record question (you replace the software), and the authority to randomize role removal. Light Anchor runs it in e-commerce, Harper becomes the insurance broker rather than selling to one, and Thrive moved a hard task from 25% → 86% in six weeks by pooling corrections across 50+ owned firms.
- **Lesson:** the single-vertical AI holdco is simultaneously Cyclical's most dangerous competitor and its best possible customer. Every one of them chose one vertical, which is market evidence for "pick one vertical," refined by Teamshares into **"pool by process, not by industry."** Pooling across 40 industries gave Teamshares scale on the general ledger and no visible operating lift. In dental the holdco already exists (the DSO), it already has the human version of the exception desk, and it has not built the agent loop. Cyclical can be the eval-and-orchestration layer DSOs and AI holdcos lack: none of them publishes per-case-type graduation evidence, and a holdco needs exactly that to know where it can cut people without hurting collections.

### Path 4. Pooled human desks sold as a service
*Invisible, Crescendo, AI-native BPOs, Smith.ai/Ruby, Infinx, offshore dental VAs, Intuit's QuickBooks Live.*

- **Starting asset:** a trained, scheduled human workforce.
- **Constraint:** they sit *outside* the client's business and take a function away, so they can never see or restructure the rest of it.
- **Result:** the A11 exception desk exists, is profitable (Smith.ai labor margin ~50–70%), and is priced per outcome or per call.
- **Lesson from Invisible:** in 2015 it ran "a step can be a human or a bot; bots take over over time." Seven years later contractor pay was still 60–70% of revenue, because every process belonged to one client and ran at one client's volume. That is the strongest outside evidence for one vertical with pooled outcomes. Fin (Sam Lessin) failed the same way.
- **Lesson from Smith.ai:** an escalation fee turns the exception desk into a profit center that corrupts the graduation signal. Price the desk flat or by outcome, and publish escalation rates per case type.
- **Lesson from Crescendo (it bought PartnerHero's ~3,000 staff):** the fastest way to get a desk is to buy or subcontract one. In the early phase, use a dental billing outsourcer or offshore dental assistants at $5–16/hour rather than hiring.

### Path 5. Single-node agents
*Dental AI receptionists and verifiers, 11x/Artisan, Sierra/Decagon/Fin, Podium/GHL, Lassie.*

- **Starting asset:** a model good enough at one job, and a buyer with a budget line for that job.
- **Constraint:** no proprietary outcome data, and next month's model makes every competitor equally good.
- **Result:** commoditization. Dozens of dental AI receptionists exist, most with under $3M raised. The role-shaped sale works for the first sale and fails on retention. The 11x story (logos it didn't have, trial contracts counted as ARR, customers using break clauses, CEO out) is the failure mode of selling "replace the role" with autonomy as a switch instead of graduation per case type with an error bar.
- **Lesson from the dental-agents analysis:** the scarce inputs are not agent quality. They are **the data pipe into the practice software** (NexHealth, local agents) **and the answer keys** (claims and remittance data, show-ups). Lassie is the exception that proves it: it chose the one node that *holds* an answer key (posting payments, confirming deposits), and that choice is why it scores 7/10 rather than 3/10.

### Path 6. Components and analogs
*Eval infra, permissions vendors, task mining, Stripe.*

- **Starting asset:** a horizontal developer or security buyer.
- **Result:** the plumbing Cyclical should buy. Tracing, scorers, dataset versioning and model-swap regression gates are commodity (Braintrust Pro is $249/mo, Phoenix/Langfuse are free). So are policy engines (Cedar, OPA, SpiceDB), identity standards (XAA/ID-JAG, Entra Agent ID) and credential brokers (Keycard, Arcade).
- **Lesson from consolidation:** Humanloop, W&B, Galileo, Langfuse and Promptfoo were all absorbed within ~11 months, so prefer open-source, self-hostable components.
- **Lesson from Stripe:** its pool is defensible for three reasons. The judged entity recurs across merchants (92% of cards seen before). A third party with money at stake produces the label, through Stripe's own pipe. The domain is adversarial, so frozen datasets decay and only a live pool keeps up. Dental meets the second condition for remittances and the first only at the insurer × plan × procedure level. It fails the third, since payers drift but don't evade, and the label pipe belongs to clearinghouses and PMS vendors. The "Stripe of dental" threat is therefore the **label-pipe owners**: clearinghouses (DentalXChange, Vyne, Optum/Change), PMS vendors, and Lassie.

---

## 4. Where this leaves the thesis

**What survives, with evidence:**

- Grading humans and agents against world outcomes. Nobody does it, it is cheaper per label than LLM judges (Braintrust meters every score), and it fixes the measured weakness of human checking (control reviewers caught ~24% of real errors).
- Per-case-type graduation with a statistical bar, the logic missing from everyone's checkpoints.
- Pooled randomized structural experiments, which nobody can run except owners, and no owner does.
- The small-business, single-vertical choice, which is *why* pooling is needed and *why* platform incumbents can't follow.
- The asset surviving model releases. Stripe's labeled history survived three architectures. Each release cuts Cyclical's costs, while Workday's and ServiceNow's seat-based revenue is threatened by their own agents.

**What should be rewritten in `realizations.md` / `thinking.md`:**

1. The moat sentence. "An outcome history no model release can produce" is true but incomplete. athenahealth shows outcome history about a third party (payers) is a feature, not a moat. Restate it as: the moat is (a) randomized evidence about *how small businesses' own processes should be structured*, which no clearinghouse or vendor sees, (b) live drift detection, and (c) cold-start certification, all within one vertical's process family.
2. Correct realizations §4 on OpenAI Frontier. It is sales-led with limited availability, its evals are manager-style human review, its "self-improvement" is memory, and its data terms forbid pooling. The lab's real vertical move is Thrive (owning the firms).
3. A6: make the seeding rate a tested parameter, and feed measured catch rate q into A7's bound (3/(n·q)).
4. A7: add label maturity, clinic-clustered intervals, pass^k replay for re-certification, and a post-graduation exploration budget.
5. A4: replace node-to-node asking with a central policy decision point. Define the steward as the writer node. Add taint and egress to the rule key. Adopt Delegate/Ambient. Buy the machinery.
6. A8: level 3 in dental is mostly already in the PMS. Copy Thrive's "rewrite the harness under regression evals" instead of compiling agents into rules.
7. A11: write data aggregation into the BAA from contract one. Plan the exception desk at ~0.2 FTE/clinic until proven lower. Subcontract it early.
8. Start where nobody holds the answer key yet. Payment posting is taken (Lassie, View, Teero, Zentist) and commoditizing toward 2% of collections. The front-office subgraph (scheduling, confirmations, recall, show-ups) is crowded with single-node agents, but nobody grades it on outcomes. Copy Lassie's founders and run one or two clinics' front office by hand for months before claiming to know the graph.
9. Go-to-market: DSO first, priced on outcomes (a percentage of collections or of front-office cost saved, which is also the A12 guardrail), sold as a service with auditable internals. Expect investors to file Cyclical as "Agentforce for dentists" or "Thrive for DSOs" unless the first slide shows pooled randomized evidence.

**What would falsify the thesis, and what to watch.** These are listed roughly in order of how much each would change David's plan:

| Signal | Why it matters | Rough probability (from the files) |
|---|---|---|
| Lassie launches eligibility/claims submission, publishes denial rates by insurer, or launches a managed "we run your billing" tier | It would hold both upstream logs and outcomes for the insurance subgraph, and the pooled desk | ~60% it ships eligibility or claims within 12 months; ~20% front office |
| A dental PMS vendor opens an "Orchestrate"/agent-registry tier that grades agents on collections or show rate, or excludes "agents performing staff functions" from its API terms | The system-of-record owner builds A5 or cuts access | HSO/Planet DDS: highest-probability threat |
| Thrive, General Catalyst or another AI holdco buys a mid-size DSO | Pool + authority + lab engineers in one owner | ~25% in 24 months (Thrive file) |
| A top DSO runs randomized cross-office staffing experiments, or sells its support center + AI to non-affiliated practices ("DSO-as-a-service") | The DSO becomes Cyclical with an existing pool | Rising |
| Podium/Weave ships a dental agent with PMS write-back plus "learned across N practices" playbooks | Distribution + pooling in the front office | Moderate |
| Eval vendors ship native outcome connectors plus confidence-interval graduation | A5–A7 tooling becomes commodity too | ~35% in 18 months (eval-infra file) |
| Microsoft bundles Entra Agent ID governance into M365 Business Premium and a PMS accepts Entra/Okta agent identities | A4 lives in Microsoft's tenant; only the work graph is left | Moderate |

**The single sentence to take away:** the market has built every component of Cyclical except the evidence engine. The evidence engine is only valuable where customers are too small to learn alone and the outcomes are graded by a third party. Dental fits, and the people with the strongest structural claim to build it there are DSOs, PMS vendors and Lassie. So Cyclical's first job is to become the evidence engine *for* a DSO, wired into an open PMS (Open Dental, Denticon, or Ascend via MCP) and into the remittance stream, before one of those three decides to build it themselves.

---

## 5. Index of files

**Enterprise platforms:**
- [UiPath](analysis-uipath.md)
- [Celonis](analysis-celonis.md)
- [OpenAI Frontier](analysis-openai-frontier.md)
- [Microsoft](analysis-microsoft.md)
- [Salesforce Agentforce](analysis-salesforce-agentforce.md)
- [ServiceNow](analysis-servicenow.md)
- [Palantir](analysis-palantir.md)
- [Workday](analysis-workday.md)
- [BPM: Camunda/Pega/Appian](analysis-bpm-camunda-pega-appian.md)
- [Aera](analysis-aera-technology.md)
- [Task mining](analysis-task-mining-skan-soroco-mimica-kyp.md)

**Vertical systems of record:**
- [ServiceTitan](analysis-servicetitan.md)
- [Intuit](analysis-intuit.md)
- [athenahealth](analysis-athenahealth.md)
- [Dental PMS](analysis-dental-pms-archy-planetdds-henryschein.md)

**Dental front line:**
- [Dental AI agents](analysis-dental-ai-agents-weave-nexhealth-arini.md)
- [DSOs](analysis-dsos-heartland-pds-aspen.md)
- [Lassie](analysis-lassie.md)

**Owners and roll-ups:**
- [General Catalyst](analysis-general-catalyst-rollups.md)
- [Thrive Holdings](analysis-thrive-holdings.md)
- [Teamshares + AI holdcos](analysis-teamshares-smb-holdcos.md)

**Pooled human desks / services:**
- [Invisible](analysis-invisible-technologies.md)
- [AI-native BPOs](analysis-ai-native-bpo-crescendo-assembled.md)
- [Smith.ai/Ruby](analysis-hybrid-receptionists-smithai-ruby.md)

**Agents and AI-OS startups:**
- [Sierra](analysis-sierra.md)
- [Notable](analysis-notable.md)
- [AI-employee startups](analysis-ai-employee-startups-lindy-relevance-artisan-11x.md)
- [SMB AI-employee platforms](analysis-smb-ai-employee-gohighlevel-podium-vendasta.md)
- [YC "AI OS" startups](analysis-ai-os-startups-yc-rfs.md)

**Components and analogs:**
- [Eval infra](analysis-eval-infra-braintrust-langsmith-arize.md)
- [Agent permissions](analysis-agent-permissions-okta-entra-c1.md)
- [Stripe](analysis-stripe-pooled-outcomes.md)

**Sweep:**
- [Discovery sweep](analysis-discovery-sweep.md)
