# Analysis: Palantir (Foundry + AIP)

Palantir is closer to Cyclical than "ancestor" suggests. For one large organization, Foundry + AIP in November 2026 already ships most of the parts of Cyclical's single-business loop: a graph model of the business (the Ontology), a single set of write operations ("actions") that a person, an LLM function or a scheduled automation can all call, process mining from event logs (Machinery), an eval harness (AIP Evals), model-agnostic LLM slots, and since March 2026 an agent that builds the graph itself (AI FDE). **Overlap: 5/10.** The architecture overlaps on A1, A2 (partly), A4, A10 and A13. Palantir has nothing for outcome-graded staged graduation (A5–A7), cross-customer pooling (A11), passive discovery from email and calendar, or a price a 9-person clinic could pay; its US commercial customers pay about $5.7M a year each. The most important lesson: Palantir proves the "business as graph with interchangeable human/agent steps" frame sells, but only after paying engineers to build each customer's graph by hand, one customer at a time. Cyclical's bet is that observation plus pooling across one vertical replaces both the engineers and the per-customer silo. The real threat in dental is Palantir selling to a large DSO, not to a clinic.

*Research caveat:* this session's web-search quota ran out partway through, and Palantir's docs, SEC filings and most press sites were blocked for direct fetching. Figures marked with a source come from search-result extracts of those pages. Items marked "(from memory)" are my prior knowledge and were not re-checked.

## What it actually is

**Products.**
- **Foundry** is the data-integration and application platform: pipelines from source systems, plus Workshop (a low-code app builder), Quiver, Code Repositories, and more.
- **The Ontology** is the layer on top of Foundry that turns tables into a typed graph:
  - *object types* such as Patient, Claim, Invoice, with their properties;
  - *link types*, the edges between objects;
  - *action types*, the permitted transactions that change objects, properties and links.

  An action "is a single transaction that changes the properties of one or more objects, based on a user-defined logic" [3]. Edits are kept in a writeback dataset per object type [3]. Actions can also call external systems; Palantir's term for this is writeback to systems of record such as SAP (from memory).
- **AIP** (Artificial Intelligence Platform, launched 2023) puts LLMs on top of the Ontology:
  - *AIP Logic*: no-code LLM functions built from blocks that can query objects and apply actions.
  - *AIP Agent Studio*: agents with Ontology retrieval and tools.
  - *AIP Automate*: runs functions on triggers, with an option to stage the resulting edits for human review (from memory).
  - *AIP Evals*: the test harness, described under A5–A7 below.
  - *Machinery*: process mining [6][7].
  - *AI FDE*: a conversational agent that does data integration and Ontology editing; beta from the week of 17 Nov 2025, generally available by March 2026 [8][9].

**Delivery model.** Two parts carry most of the go-to-market.
- *Forward-deployed engineers (FDEs)*: Palantir engineers embedded with the customer, who build that customer's pipelines and Ontology.
- *AIP Bootcamps*: 1–5 day hands-on sessions, "from zero to use case in 5 days" [12]. The CEO said Palantir ran more than 500 in one year [13]; the year is unclear in the coverage. No conversion rate has been published. The evidence is anecdotal, e.g. a utility signing a seven-figure deal days after a bootcamp [12].

**Buyers and traction, Q3 2026** (quarter ended 30 Sep 2026; SEC 8-K extracts via [1], Futurum [2]):

| Metric | Value |
|---|---|
| Total revenue | $2.313B, +96% y/y |
| US commercial revenue | $984M, +148% y/y, +29% q/q (first quarter above US government's $953M) |
| US commercial customers | 686, +29% y/y; +5% q/q, slowing from +6% in Q2 (Futurum; not confirmed in the filing) |
| Implied revenue per US commercial customer | ~$5.7M/yr ($984M × 4 / 686; my arithmetic) |
| TTM revenue per US commercial customer | +88% y/y (Futurum) |
| Deals closed | 212 ≥ $1M; 107 ≥ $5M; 64 ≥ $10M |
| Net dollar retention | 165%, +800 bp q/q (Futurum; company-defined metric) |
| US commercial TCV (total contract value booked) | $1.463B, **+11% y/y** |
| Adjusted operating margin | 62% (GAAP 47%); "Rule of 40" score 158% |
| FY2026 guidance | Revenue $8.530–8.534B (+91%); US commercial > $3.56B (+143%) |

Growth comes mainly from existing giant accounts expanding: revenue per customer is up 88% while the customer count is up 29%. US commercial bookings (TCV +11%) are growing far more slowly than recognized revenue (+148%). That gap is the number to watch for a slowdown.

Management credits the Q3 acceleration to "Sovereign AI": post-training open-weight models on a customer's own data inside AIP [1]. Constellation Research framed the quarter as an "enterprise inflection point due to sovereign AI, LLM disillusionment" [5]. Palantir's pitch is that raw LLMs fail in production without the Ontology.

**Pricing.** Not public. Contracts are enterprise-negotiated and multi-year, with compute-based consumption on top (from memory). The deal-size distribution above shows the floor in practice. A free AIP developer tier exists for builders (from memory), but it is not a route to small-business customers.

## Loop comparison

| Aspect | Palantir's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | Ontology = graph of *entities* (objects, links) plus *verbs* (action types). Any principal — user, AIP Logic function, Automate rule, agent — applies the same action type under the same submission criteria. Process flow is modeled separately in Machinery as states and transitions. | **Same idea, different decomposition** (entities + verbs, not roles + handoffs); more mature |
| A2 Observation / onboarding | FDEs and bootcamps integrate source systems by hand. Machinery mines processes from event logs *once the data is in Foundry*. AI FDE builds pipelines and Ontology from natural-language instructions. Nothing reads email or calendar passively to discover the org. | **Different / worse for small business**: discovery is labor (now partly agent-assisted), not passive observation |
| A3 UX | New apps (Workshop, Quiver, AIP Threads, agent chat) plus writeback to systems of record. Workers are trained on a new tool. | **Worse** for Cyclical's goal; fine for enterprises with operations teams |
| A4 Permissions | Markings (mandatory data-class controls), project and role permissions, row- and column-level security, action *submission criteria* (rules over parameters, user/group, object state), Approvals, and Checkpoints that log a stated purpose before sensitive actions [3][4]. Agents act under user or service-account permissions. No node-asks-node just-in-time grants, and no frequency signal proposing new edges. | **Different, partly better**: rule-based, never wording-based, and it answers the "system node" question (see below); lacks the just-in-time and frequency mechanics |
| A5 Shadow eval | AIP Evals runs suites offline. Test cases can be backed by an object set, where each historical object is a test case and ground truth is a property on it; Palantir's example compares output to the "Should Recall" property of a Defect Report [10]. That ground truth is usually a *past human decision*. There is no running shadow mode that scores human and agent against outcomes. | **Worse**: it grades against the human by default, which is exactly what Cyclical rejects |
| A6 Checkoff | Staged edits and Approvals let a person review agent-proposed changes (from memory for Automate). No seeded known-bad items and no scoring of the checkers. | **Absent** (the anti-rubber-stamp part) |
| A7 Graduation | A test case passes only if all its iterations pass [11]. Comparisons run against previous function versions, and experiments grid-search prompt × model [10]. There is no statistical threshold, no per-case-type promotion to autonomy, and no automatic demotion when the model changes. | **Absent** |
| A8 Replacement levels | General LLM function → plus Ontology retrieval → deterministic Functions and rules → full automation. New in 2026: post-training open models per customer ("Sovereign AI"). | **Different**: Palantir fine-tunes per tenant, while Cyclical deliberately uses retrieval to stay model-agnostic |
| A9 Orchestrator agent | AI FDE builds pipelines, Ontology and apps on request [8][9]. Machinery has an "optimize a process" view [7]. Nothing autonomously proposes merging roles or removing nodes; FDEs and the customer's managers do that. | **Partial**: has the "vibe-code an app" half, not the "propose a reorganization" half |
| A10 Shared context | The Ontology *is* a business-wide context layer that every agent queries within its permissions. | **Better / more mature** |
| A11 Pooling | None. Each customer's enrollment is siloed. Cross-customer reuse covers only *structure* (packaged Ontology/app templates via Marketplace, FDE know-how), never *outcomes* (from memory). | **Absent, by design** |
| A12 Anti-Goodhart | Business KPIs live in the same Ontology, so a guardrail metric *can* be built. Nothing pairs each task eval with a business-level guardrail. | **Absent as a mechanism** |
| A13 Model-agnosticism | Multiple vendors' models (OpenAI, Anthropic, Google, open-weight) can be selected per function (from memory). Experiments compare models [10]. Palantir's message is that LLMs are commodities and the Ontology is the value. | **Same** (and Palantir says it louder) |
| A14 Business model & moat | The moat is a per-customer Ontology plus switching costs from operational dependency. Target is the largest governments and enterprises (~$5.7M/yr per US commercial customer). | **Opposite target; different asset** (per-tenant integration vs. pooled outcome history) |

### A1: the frame is implemented, but the graph is of data, not of work

Palantir's strongest idea for Cyclical is that the **action type is the contract**. A "Submit claim" action has typed parameters, validation (submission criteria) and side effects. Whether a biller clicks a button in a Workshop app, an AIP Logic function calls it, or an Automate rule fires it, the same rule checks run and the same writeback happens [3]. That makes human and agent interchangeable at the point that matters: where a step changes state. Cyclical's spec says "a person and an agent are interchangeable occupants of a node" but does not say what the node's interface is. Palantir's answer is that the interface is a typed, validated, permissioned write.

The difference is in what the nodes are. Palantir's nodes are business *objects* (Claim, Patient, Appointment); the edges are relationships; the verbs are attached to objects. Cyclical's nodes are *roles or steps* and its edges are *handoffs*. Palantir keeps "who does what in what order" in a separate tool (Machinery's state-transition graph [6]). Cyclical's eval and graduation logic is defined per node and per case type. In Palantir's model that maps more cleanly onto (action type × object subtype) than onto a role. I'd guess at 60% that Cyclical would gain by making its nodes "verbs on objects" and treating roles as bundles of verbs. The A7 rule "graduate per case type" then falls out for free: it becomes graduation per (verb, object subtype).

### A2: Palantir has process mining, but uses it only after a human has built the graph

Machinery mines "an ongoing process from external event logs" and draws states and transitions as a graph [6]. The Palantir Learn course loads claims data, mines the process logs, and inspects them for bottlenecks [6]. So the method Cyclical names (Celonis-style process mining) already sits inside Palantir. But it runs on object sets in Foundry: an FDE or customer engineer has to connect the systems, build pipelines and define the objects first. Discovery is labor. That labor is the FDE model, and its cost explains why Palantir only sells to customers paying millions a year.

Palantir is now automating that labor. AI FDE "translates natural language requests into Foundry operations", including "creating or updating the objects, links, and actions that make up your ontology" [8][9]. It still needs someone to say what to build. Cyclical's A2 is the next step: infer the graph from logs of email, calendar and practice software, with no one specifying it. In a 9-person dental clinic the systems are few and standard (one practice-management system, one email, one accounting package), so passive discovery is far more tractable than in a Fortune 500 with 400 source systems. **The FDE model tells you what graph discovery costs when the business is heterogeneous: roughly one engineer-team per customer.** Cyclical can automate it because a single vertical is homogeneous: every clinic runs some version of the same graph, so discovery reduces to matching the clinic against a pooled template plus "missing edge" flags.

### A4: Palantir's answer to Cyclical's UNRESOLVED question

The spec asks who answers a permission request sent to a *system* node, such as the practice software. Palantir's answer is that nobody answers ad hoc. Access is a property of the **data class**, not a decision by a responsible person:
- *Markings*, mandatory labels like "PHI", propagate from source datasets to every object and derived dataset;
- *submission criteria* gate each verb by who is asking and by object state [3][4];
- *Checkpoints* make the requester log a purpose before a sensitive action proceeds [4].

That matches Cyclical's rule that approvals are decided "by who is asking, what class of data, and what kind of task, never by the wording". Palantir has run it at scale on classified data. The elegant fix for Cyclical: system nodes hold no discretion. Their data carries markings, and a grant is a policy evaluation logged like a Checkpoint. Only a request that falls *outside* policy is routed to a person, namely the owner of the policy for that data class, which is one human role per data class rather than one per system. Palantir lacks the two dynamic parts Cyclical wants: temporary just-in-time grants between nodes, and "frequent requests ⇒ propose a permanent edge, unused ⇒ propose removal". Those are Cyclical's additions, and they suit a business where nobody has the time to write policy up front.

### A5–A7: Palantir's evals are a pre-deployment test bench, not a graduation process

AIP Evals lets you:
- write manual test cases, or back them with an object set so that each historical object becomes a test case [10];
- pick built-in evaluators (exact match, LLM-as-judge with its reasoning shown, etc.) or custom ones [10][11];
- run each case several times to absorb LLM randomness, and grid-search prompt × model combinations [10];
- compare a function to its previous versions [11].

The pass rule is strict: a case passes only if all iterations pass [11]. Palantir's own example grades against the "Should Recall" property, which is a past human decision [10]. Cyclical's thinking.md says to avoid exactly that, because the human's mistakes become the ceiling. In Palantir, outcome-graded evals are *possible*: because Foundry has integrated the systems of record, "claim paid" or "patient showed" can be a property on the object, so a suite could grade against it. But nothing in the product pushes you there. Nothing scores the human and the agent side by side, samples their disagreements, seeds bad items to catch rubber-stamping, or converts "zero errors in n runs" into autonomy for one case type and demotion on model swap. Third-party exam guidance from the Palantir ecosystem tells builders to "reserve LLM-as-a-judge for what a deterministic check cannot verify" [14]. That is sound engineering, but it is still about test design, not graduation.

That gap is Cyclical's clearest technical difference from Palantir. It also explains why the gap exists: at Palantir's scale, each customer has enough volume to collect test cases from its own history, and a human (often an FDE) decides when to go live. No statistical graduation machinery is needed when an engineer is in the room.

### A8 and A13: same thesis on models, opposite choice on fine-tuning

Palantir and Cyclical agree that the model is a commodity and the structure around it holds the value. Constellation's Q3 headline [5] and management's framing of "Sovereign AI" both say this. But Palantir's 2026 growth story is *post-training open-weight models per customer* [1]. That makes sense when a customer has millions of records per process and pays $5M+ a year. Cyclical's level 2 (retrieved examples, no fine-tuning) is the right call for a clinic with hundreds of examples. Palantir's move does carry a warning: if per-tenant post-training becomes cheap and automatic, "retrieval survives model swaps" weakens as a differentiator. Pooled fine-tuning across 10,000 clinics then becomes possible for Cyclical and impossible for Palantir.

### A11: Palantir doesn't pool because its customers would leave if it did

Palantir started in 2003–04, funded partly by In-Q-Tel, building Gotham for intelligence agencies, where mixing one customer's data with another's is illegal (from memory). Its commercial pitch kept that promise: your data, your Ontology, your enrollment, and Palantir doesn't own or resell it. For a bank or the Army that promise is a precondition of the sale. The cost:
- Every customer pays again for graph discovery, which is where the FDEs come in.
- Every customer's evals start from zero.
- No customer benefits from another's outcomes. Palantir cannot run Cyclical's "randomize role removal across hundreds of businesses" experiment, because no two Palantir customers share an outcome table.

Palantir reuses *structure*: packaged Ontology and app templates, and the FDE corps' pattern library (from memory). That is weaker than pooling outcomes, because structure is exactly what a stronger model or AI FDE can regenerate.

**The important exception for dental:** a large DSO (dental service organization, a company that owns or runs the business side of many practices) *is* a pool under one owner. Heartland Dental, the largest US DSO, has on the order of 1,700+ affiliated offices (from memory). A DSO on Foundry could pool outcomes across its own offices legally, run randomized role-removal tests across its own sites, and staff its own central exception desk; DSOs already run shared billing centers. Palantir plus one DSO would reproduce A11 inside a single tenant. Cyclical's pooling advantage holds only for the ~75–85% of dentists *not* in a DSO (ADA HPI figures in realizations.md). It is strongest if Cyclical's pool ends up larger than the largest DSO.

## Where they're ahead of Cyclical

- **Action types as the interface where humans and agents are interchangeable** [3]: typed, validated, permissioned and transactional, with writeback to systems of record. Cyclical has nothing this concrete yet.
- **A permission model that answers the system-node question**: data-class markings, rule-based submission criteria, and purpose-logged Checkpoints [3][4]. It has been proven in classified settings.
- **A shared context layer (A10) that exists and is queried by agents in production**, at 686 US commercial customers.
- **Process mining built into the same platform as the agents** (Machinery [6][7]). The graph that is mined and the graph that is acted on are the same object model.
- **AI FDE** [8][9]: Palantir is already using agents to cut the cost of graph construction, the exact cost Cyclical wants to remove.
- **Distribution and trust**: bootcamps that take a customer from zero to a working use case in 1–5 days [12], NDR of 165% [2], and a brand that buyers cite when they pick a vendor for operational AI.

## Where they're doing it differently (and whether their way is better)

| Difference | Palantir | Cyclical | Which is better, for whom |
|---|---|---|---|
| Graph discovery | Human engineers, now agent-assisted (AI FDE) | Passive mining of existing tool logs | Palantir's works for heterogeneous giants. Cyclical's only works in a homogeneous vertical, which is why "pick one vertical" is load-bearing. |
| Graph unit | Objects + verbs (actions) | Roles/steps + handoffs | Palantir's is cleaner for permissions and per-case-type evals; Cyclical should consider adopting it |
| Eval ground truth | Historical properties, often past human decisions | Real-world outcomes; agreement with the human only as a fallback | Cyclical's is better in principle. Palantir's is easier and good enough when an FDE decides go-live. |
| Adaptation | Per-tenant post-training ("Sovereign AI") | Retrieved examples; pooled general skill | Palantir's fits huge single-tenant volume; Cyclical's fits small tenants |
| Data scope | Strict per-tenant silo | Pooled across a vertical | The silo buys trust and big contracts; the pool buys statistical power. They are incompatible. |
| UX | New apps; workers trained | Drafts appear in tools people already use | Cyclical's is necessary for clinics with no ops team; Palantir's is acceptable where a COO mandates the new tool |
| Delivery | FDEs and bootcamps | Software-only (intended) | Palantir's produces $5.7M/yr customers; Cyclical needs ~$5–10k/yr of agent spend per clinic to work with zero human delivery |

## Feedback & reviews on these parts of the loop

My search budget ran out before I could pull G2, Gartner Peer Insights or Reddit threads on AIP specifically. The evidence below is what I gathered; review-site scores are missing.

**Delivery model / graph discovery (A2, A14). Independent commentary, mostly secondary:**
- Gartner reportedly warns that FDE engagements can create "vendor dependency, security risks, technical debt, and talent atrophy", and Forrester that bespoke builds "deepen vendor dependence, making future changes costly". I saw both only in secondary coverage, not the original reports [15][16].
- Palantir's former CFO Colin Anderson is quoted in secondary coverage warning that companies copying the FDE model on small contracts are "lighting equity on fire" [16][17]. This is the most direct evidence that FDE-style graph discovery only pays at Palantir's contract sizes.
- A critic describes Palantir's version as "deliberately expensive per engagement, deliberately slow to onboard, deliberately low-ratio of engineers to accounts" [17].
- The defense: FDEs are "product-formation" investment, creating "extremely high switching costs, not through contractual lock-in, but through operational dependency" [18]. The Motley Fool (Oct 2026) argues Palantir "looks like a consulting company" but its margins say otherwise [19]. The Q3 2026 adjusted operating margin of 62% supports that [1].
- Vendor-sourced: Palantir's own filings note customers depend on its operations-and-maintenance services after deployment, framed as an operational risk [20].
- The Register (Oct 2026) traces how the FDE model became an industry fad, with model labs and vendors copying it [15][21].

**Evals (A5–A7):**
- The Palantir community's guide to writing evals opens by saying the team is "working on better docs for AIP Evals", and advises starting with "a handful of carefully chosen test cases with pass/fail checks" [11]. This is vendor-adjacent. The point is that the eval practice is still hand-built test design, not outcome-driven graduation.
- A third-party case study (Morph Systems Substack) shows object-set-backed tests with ground truth taken from a past decision property, and notes the prompt × model experiment feature [10]. This is independent, but from a Palantir partner.

**Commercial adoption (A14). Vendor and analyst:**
- Futurum flags that NDR is "company-defined", that growth is concentrated in existing accounts (+88% revenue per customer), and that sequential customer adds slowed to 5% [2].
- Constellation reads Q3 as an enterprise inflection driven by "LLM disillusionment" [5], an independent analyst's account of why buyers want an Ontology layer rather than raw models.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraints.** Palantir began with intelligence customers. They had enormous, messy, heterogeneous data that could not legally be pooled, and they paid for engineers in the building. Three constraints followed. First, each tenant is a silo, so there is no pooling. Second, each graph is discovered by hand, which means FDEs, and that only pays at seven- to eight-figure contracts. Third, governance is built from rules over data classes, because the customers demanded it. AIP added LLMs to an asset Palantir already had, the per-customer Ontology, which is why Palantir benefits from each model release: better models make the Ontology more usable, and AI FDE makes it cheaper to build. Palantir passes the "sign of the next model release" test from realizations.md. Its asset is integration-built-over-time plus switching costs. That is per-tenant, not a pooled outcome history.

**Is Cyclical a clone, subset, superset or orthogonal?** For a single business, Cyclical is largely a **subset** of what Palantir's components can do (graph, shared context, interchangeable executors, process mining, evals, model choice), **plus** a more rigorous eval discipline (A5–A7) and an orchestrator that proposes reorganizations (A9). Across businesses, Cyclical is **orthogonal**: A11 pooling is something Palantir has structurally refused to do. On market, Cyclical is **disjoint**: 9-person clinics versus customers paying ~$5.7M a year. In short, Cyclical is Palantir's single-tenant loop made cheap by passive discovery and made statistically powerful by pooling, which only works in a homogeneous vertical.

**Copy.**
- Action types as the single typed, validated, logged interface that humans and agents both use.
- Data-class markings plus rule-based submission criteria plus purpose-logged access as the answer to the system-node permission question.
- One object model shared by process mining, agents and evals.
- The bootcamp idea, turned into a product feature: show a clinic its own mined graph and one working agent within a week.

**Avoid.**
- Grading against historical human decisions (Palantir's default test-bench pattern).
- Any delivery step that needs a human engineer per customer. Palantir's former CFO's "lighting equity on fire" warning applies exactly at Cyclical's contract size.
- New UI for workers.

**Exploit.**
- Palantir cannot pool across customers without breaking its core promise, so pooled outcome history is a moat against Palantir specifically.
- Palantir will not sell to independent clinics. At ~$5.7M per US commercial customer and with FDE economics, the long tail of ~150k US dental practices (from memory) is invisible to it.
- Palantir's own "LLMs are commodities, the structure is the value" message helps Cyclical's pitch to investors.

**Threat level: low for independent clinics; medium through DSOs.** The observation that would tell David the threat is rising: **a top-10 DSO (Heartland, Aspen, Pacific Dental, Smile Brands) or a dental practice-software vendor (Henry Schein One / Dentrix, Patterson / Eaglesoft, Planet DDS) announcing a Foundry/AIP deployment for revenue-cycle management (RCM: the billing, claims and collections chain) or front office.** A DSO on Foundry gets single-tenant pooling across 500–1,700 offices. A practice-software vendor on Foundry gets the system of record plus a graph. A secondary signal: Palantir packaging an industry Ontology plus AI FDE into a self-serve, low-price product for mid-market healthcare providers. That would show it is willing to lower its price floor. I put roughly a 15% probability on either happening by end-2027 (a guess).

## Sources

1. Palantir Q3 2026 press release (SEC 8-K Ex. 99.1), via search extracts: https://www.sec.gov/Archives/edgar/data/0001321655/000132165526000045/a2026q3ex991pressrelease.htm
2. Futurum, "Palantir Q3 FY 2026 Earnings: US Commercial Revenue Overtakes US Government": https://futurumgroup.com/?p=97554
3. Palantir docs, Action types overview and Submission criteria: https://www.palantir.com/docs/foundry/action-types/overview/ ; https://www.palantir.com/docs/foundry/action-types/submission-criteria/index.html ; https://palantir.com/docs/foundry/action-types/permissions/
4. Palantir docs, "What is an operational application?" (Approvals, Checkpoints): https://palantir.com/docs/foundry/app-building/operational-apps/
5. Constellation Research, "Palantir's Q3 highlights enterprise inflection point due to sovereign AI, LLM disillusionment": https://www.constellationr.com/insights/news/palantirs-q3-highlights-enterprise-inflection-point-due-sovereign-ai-llm
6. Palantir docs, Process mining (Machinery) overview; Palantir Learn speedrun: https://www.palantir.com/docs/foundry/process-mining/overview/ ; https://learn.palantir.com/speedrun-mining-your-first-business-process
7. Palantir docs, Machinery overview and "Optimize a process": https://www.palantir.com/docs/foundry/machinery/overview ; https://www.palantir.com/docs/foundry/machinery/optimize-process
8. Palantir docs, AI FDE overview and modes: https://www.palantir.com/docs/foundry/ai-fde/overview ; https://www.palantir.com/docs/foundry/ai-fde/modes-and-capabilities
9. Palantir announcements, Nov 2025 and Mar 2026: https://www.palantir.com/docs/foundry/announcements/2025-11 ; https://www.palantir.com/docs/foundry/announcements/2026-03
10. Morph Systems, "Introduction to AIP Evals and Real-World Use Cases"; Palantir blog, "From prototype to production"; AIP Evals docs: https://open.substack.com/pub/morphsys/p/introduction-to-aip-evals-and-real ; https://blog.palantir.com/from-prototype-to-production-engineering-responsible-ai-3-ea18818cd222 ; https://www.palantir.com/docs/foundry/aip-evals/analyze-run-results
11. Palantir AIP Evals docs and community guide: https://www.palantir.com/docs/foundry/aip-evals/overview ; https://palantir.com/docs/foundry/aip-evals/create-suite/ ; https://palantir.com/docs/foundry/aip-evals/run-suite/ ; https://community.palantir.com/t/guide-writing-effective-evals/2856
12. Palantir AIP Bootcamp brochure (Hannover Messe 2024): https://www.hannovermesse.de/apollo/hannover_messe_2024/obs/Binary/A1354173/Palantir%20AIP%20Bootcamp.pdf ; Constellation on bootcamps: https://www.constellationr.com/index%2Ephp/insights/news/palantirs-commercial-business-scales-help-ai-boot-camps
13. Yahoo/Fortune, "Palantir CEO says its unconventional boot camps are drawing crowds": https://news.yahoo.com/tech/palantir-ceo-says-unconventional-boot-185417794.html
14. Ontologize, Palantir Applied AI Engineer Specialist exam guide (Sep 2026): https://www.ontologize.com/exam-guides/palantir-applied-ai-engineer-specialist-exam-guide.pdf
15. The Register, "Palantir's fondness for French food cooked up tech's latest fad: forward-deployed engineers" (Oct 2026): https://www.theregister.com/channel/2026/10/03/palantirs-fondness-for-french-food-cooked-up-techs-latest-fad-forward-deployed-engineers/5300360
16. "Forward Deployed Engineering Is Real. Most of What Companies Are Building Is Not." (Medium): https://medium.com/@jision/forward-deployed-engineering-is-real-most-of-what-companies-are-building-is-not-d6a87e852a7c
17. Perspective AI, "Palantir's Forward-Deployed Engineering Playbook": https://getperspective.ai/blog/palantir-forward-deployed-engineering-playbook-anthropic-openai-copying ; Productics, "Forward Deployed Engineer NO, Product Manager YES": https://productics.substack.com/p/forward-deployed-engineer-no-product
18. "Understanding Palantir: Forward-Deployed Engineers and the Making of an Unusual Platform Company" (Medium): https://medium.com/@balajibal/understanding-palantir-forward-deployed-engineers-and-the-making-of-an-unusual-platform-company-494dc7812f24
19. Motley Fool, "Palantir Looks Like a Consulting Company. Its Numbers Tell a Different Story." (Oct 2026): https://www.fool.com/investing/2026/10/08/palantir-looks-like-a-consulting-company-its-numbe/
20. Palantir Form ARS FY2025: https://www.sec.gov/Archives/edgar/data/0001321655/000132165526000021/fy2025palantirars.pdf
21. "Palantir's forward-deployed engineers spark AI services trend as vendors copy model": https://news.lavx.hu/article/palantir-s-forward-deployed-engineers-spark-ai-services-trend-as-vendors-copy-model
