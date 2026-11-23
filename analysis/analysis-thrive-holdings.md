# Analysis: Thrive Holdings

Thrive Holdings is the closest real-world version of half of Cyclical's thesis. It owns 70+ same-process service businesses in accounting (Current, formerly Crete Professionals Alliance) and IT services (Shield). OpenAI owns equity in it and has engineers embedded in its businesses. It pools work from dozens of firms to improve one shared agent. It is not yet Cyclical in accounting. Its "self-improving" tax AI is graded against what human reviewers corrected, not against what happened in the world. It improves one task (drafting a return), not the business's graph. It runs no structural experiments such as removing a role. **Overlap: 6/10.** It shares the vertical pooling, the frontier-lab backing and the aim of taking over the work, but it has no graph, no outcome grading, no graduation step and no model-neutrality. The main lesson is that the fastest way to solve "who owns the system of record, who consents, who has the data" is to own the business, or to sell to someone who already owns hundreds of them. In dental, that someone is a DSO (dental service organization: a company that owns or runs the back office of many dental practices). A Thrive-style dental roll-up would beat Cyclical inside the offices it owns. It would not beat a Cyclical that signs DSOs first.

*Method note: openai.com, techcrunch.com, fourweekmba.com and artificialintelligence-news.com could not be reached from this session (network allowlist), and WebFetch failed on every host I tried. All facts below come from search-engine extracts of those pages and of secondary coverage. Treat exact wording as unverified against the primary posts.*

## What it actually is

**Structure and money.** Thrive Holdings was spun out of Thrive Capital, which is itself a major OpenAI investor. Its timeline:

- **Dec 1, 2025.** OpenAI took a stake, terms undisclosed. OpenAI sends engineering, research and product staff to work inside Thrive's companies, and its stake grows if those companies succeed [8][9].
- **Aug 12, 2026.** Thrive raised $2B at a $12B valuation from SoftBank, D1 and Altimeter [1][10].
- **The August raise also funds a third vertical:** "regulatory services for physical infrastructure", meaning permitting, certification and compliance for data centers, healthcare facilities and power projects [11][12].
- **Oct 29, 2026.** Thrive agreed to buy ADT for $15.3B in enterprise value ($10/share), closing in Q1 2027 [13][14]. Thrive no longer buys only small firms; it will also buy an entire platform company.

**Current (accounting).**

- **History.** Founded as Crete in 2023–24. In June 2025 Reuters reported a plan to spend $500M over two years buying US firms, with selling partners keeping a minority stake in their local firm [15]. Rebranded Current in mid-2026 [16][17]. CEO: Steve Stagner [18].
- **Size.** 50+ firms and 2,000+ professionals as of Aug 2026 [8][19]. An industry roundup cites ~30 firms and $500M+ revenue (unverified, likely older) [20].
- **Forbes, June 2026.** Executives said they will commit $1B to buying more local firms [18].

**The Tax AI.** OpenAI's engineering post "Building self-improving tax agents with Codex" (May 27, 2026) describes it [3][4][5]:

- **Scope.** It prepares medium- to high-complexity 1040 (individual) and 1041 (trust/estate) returns from messy source documents, including K-1s (partnership income statements).
- **Volume.** 7,000 returns in the 2025 season. Forbes ties all 7,000 to one firm, Larson Gross [18][21]. OpenAI frames it as a pilot across Crete's 30+ firms [2]. Which is true matters for pooling.
- **Headline metric.** Within about six weeks, the share of returns with at least 75% of fields correct before review rose from ~25% to 86%. Results at the 90% and 100% field thresholds rose faster [3][4].
- **Other figures.** Accuracy "up to 97%" (OpenAI). Prep time down about a third (31% average). Throughput up ~50%.
- **Forbes's version.** "Up to 98% accurate in data entry", against "the 10% to 15% manual error rate typical of human preparers" [18][19][22].

**Shield (IT services: managed service providers, or MSPs, which run IT for small companies).**

- **Funding and scale.** $200M from Thrive in two $100M tranches [23][24]. 20 MSP acquisitions by its Nerds Support deal [25].
- **Tools.** Internal tools Sentinel and Spectre "address over 60% of high-volume ticket categories" and more than halve median resolution time (vendor claim) [26].
- **Forge (Sept 2026).** An "AI operating system for MSP service delivery". Its "AI Engineer" agent takes eligible helpdesk tickets from intake to resolution, "25× faster than technicians", with a 16-minute median (vendor claim) [27].
- **Framing.** The Register called it the "Palantir-ization of IT services" [28], meaning forward-deployed engineers rebuilding a customer's operations.

**Pricing.** Not applicable: Thrive doesn't sell software, it owns the firms and keeps their margin. No revenue, margin or per-firm economics have been published [19].

## Loop comparison

| Aspect | Thrive Holdings | vs Cyclical |
|---|---|---|
| A1 Core frame (graph, interchangeable occupants) | Linear task pipelines (tax prep; ticket intake→resolution). The firm is a private-equity operating unit, not a graph. | Absent |
| A2 Observation / onboarding | Forward-deployed engineers sit beside accountants and map the work by hand ("worked side-by-side… to iterate quickly") [21]. No process mining (reconstructing a workflow from software event logs) reported. | Different (higher fidelity, far more expensive per business) |
| A3 UX | Not public. The agent drafts the return; practitioners correct it inside the prep workflow. Corrections are captured as "product traces". | Similar intent, details unknown |
| A4 Permissions | Not needed in the same way: Thrive owns the firm, so data access is an ownership decision. Nothing public on agent-to-agent access rules. | Absent (avoided by ownership) |
| A5 Shadow eval | Graded against **expert corrections**. The reviewer's final return is the answer key. No public use of IRS acceptance, notices, amended returns or client outcomes. | Worse by Cyclical's standard (ceiling = the reviewer), but pragmatic in tax |
| A6 Checkoff | Two human gates: practitioners review every return, and engineers review every Codex-generated code change [3][4]. No seeding of known-bad drafts reported. | Same gate, no anti-rubber-stamp defense |
| A7 Graduation | None. Paid preparers must sign returns (IRS rules, from memory), so the signer can never be removed. Field-completion bands (75/90/100%) work as a graded, non-binary error metric. | Absent; better error metric |
| A8 What "replacement" means | The "self-improvement" changes the harness (the code around the model), not the model's weights. Codex edits schemas and mappers and must pass targeted and regression evals before opening a pull request [3][4][5]. | Ahead on Cyclical's level 3 (code regenerated from contract + tests) |
| A9 Orchestrator agent | Codex acts as an orchestrator at the **code** level: it diagnoses failures and proposes fixes. Reorganizations (merging firms, centralizing back office) are done by PE managers, not an agent. | Different; narrower |
| A10 Shared context | Not public | Unknown |
| A11 Cross-business pooling | Yes, structurally: one Tax AI across 50+ owned firms, with corrections pooled into shared evals. Nothing reported on outcome A/B tests, rare-segment tracking, re-certification after model swaps, or randomized role-removal tests. | Partial; same bet, much narrower use |
| A12 Anti-Goodhart | Reports time saved and accuracy only; no business-level guardrail (realization rate, client retention, IRS notices) published. | Absent publicly |
| A13 Model-agnosticism | Built with OpenAI engineers on Codex, and OpenAI's stake grows with success. The harness-plus-evals design is in principle portable. | Worse (aligned with one lab by contract) |
| A14 Business model & moat | Owns the businesses and captures operating margin. Moat = capital ($2B), ownership (consent, data, the power to mandate a change), and privileged lab access. Asset = owned cash flows plus a correction history in one task. | Different; solves Cyclical's system-of-record risk by owning the operator |

**A5: what the loop is graded against.** Every account describes the same chain [3][4][5]:

1. A practitioner corrects the AI's draft.
2. A "product trace" records each step the agent took.
3. The pair (draft field, corrected field) becomes a structured eval target.
4. Codex finds the failing step, writes a fix to the harness (extraction schemas, field mappers), and runs targeted evals plus a regression suite.
5. An engineer reviews the pull request before it ships.

No source mentions IRS acceptance, IRS notices, amended returns or audit adjustments as signals. I put ~15% on any of those feeding the loop today. This is the stage-1 design Cyclical explicitly rejects: "minimize difference from the human", where the reviewer's mistakes become ground truth.

In tax that choice is defensible, and the reason is useful for Cyclical. The world grades a 1040 slowly and rarely. E-file acceptance mostly checks format. Math-error and underreporting notices arrive months to years later, and audits cover under 1% of individual returns (from memory). The reviewer's correction is the only fast answer key. Dental has faster world answer keys: show-ups the same day, insurer payment statements (ERAs, electronic remittance advice) in weeks. Cyclical's "grade against the world" principle is easier to apply in dental than in Thrive's vertical.

**A7 and the field-completion metric.** Thrive answers a question thinking.md leaves open: how to measure error on non-binary tasks. A return is scored as the share of fields correct, and progress is tracked as the share of returns above 75%, 90% and 100% of fields correct. That is a usable bar per case type. Cyclical could adopt it for claims, treatment-plan entry and charting.

There is no graduation, for a legal reason: a signing preparer is required. What shrinks is the junior data-entry and preparer labor under the signer, not the signer. Throughput rose ~50% while prep time fell ~31%. That suggests Current used the freed hours for more volume rather than cutting headcount, consistent with the accounting talent shortage. No layoffs are reported.

**A8.** Thrive's loop is the most concrete public version of Cyclical's "generated code is disposable, regenerated from contract + tests". The harness is code. The eval suite, built from corrections, is the contract. A coding agent rewrites the code under regression tests. Cyclical's level 3 imagines compiling an agent's behavior into a deterministic rule. Thrive instead keeps the model in the loop and keeps rewriting the deterministic scaffolding around it. The second is easier to run and probably the better default.

**A11.** Pooling exists, but it pools corrections, not outcomes, and it feeds one task agent rather than tests of the business's structure. Owning the firms means it could run randomized role-removal tests across 50+ firms without asking any owner. Nothing suggests it does. If all 7,000 returns came from Larson Gross, the "pooled across many firms" claim is weaker than the framing implies. I put ~50% on most of the 2025 volume coming from one or two firms.

## Where they're ahead of Cyclical

- **Ownership solves the problems Cyclical leaves open.** Thrive doesn't need clinic-by-clinic consent, permission design (A4), or an answer to "who speaks for the practice software". It can mandate adoption, standardize software across firms, and put engineers on site. Cyclical's UNRESOLVED item on system nodes disappears when you own the system's operator.
- **A working self-improvement loop on real volume.** 25%→86% in six weeks on 7,000 complex returns [3][4], with the mechanism public. Cyclical has a design document.
- **Capital and model access.** $2B fresh, a $15.3B acquisition, and OpenAI forward-deployed engineers. If Thrive enters a vertical, it can buy the pool outright instead of accumulating it.
- **A non-binary error metric** (field-completion bands) and a harness-level regression suite that doubles as a re-certification mechanism when the model changes.

## Where they're doing it differently (and whether their way is better)

**Buy the firms vs. sell to them.** Buying gets data and authority on day one. Its costs are capital, about $1B per vertical per Forbes [18], and integration speed: ~50 firms in ~2 years. Cyclical's realizations say role-removal experiments need hundreds of businesses. At 50 firms Thrive has a pool big enough to improve a task, but not yet big enough to test the business's structure. Buying is better for the first 2–3 years. Selling software scales the pool further per dollar, if adoption happens.

**Grade against reviewers vs. against the world.** Thrive's way is right for tax (slow, rare world signal) and wrong for dental claims or recall, where the world answers quickly. This is a real difference, not a gap Thrive will close soon.

**Embedded engineers vs. process mining.** Forward-deployed engineers give perfect understanding of a workflow and cost roughly an engineer-year per platform. Process mining is cheaper per business but sees only what the logs see. For a 9-person dental clinic, Thrive's method doesn't pay unless you own hundreds of clinics. For a DSO it does.

**One task agent vs. a business graph.** Thrive optimizes the expensive task (return prep, ticket resolution) and leaves reorganization to PE managers. That is the standard roll-up playbook (centralize back office, cut the junior pyramid), done by humans. Cyclical's claim is that an orchestrator plus pooled experiments does this better. Thrive's results neither prove nor refute that.

## Feedback & reviews on these parts of the loop

**Accuracy and verifiability (A5–A7), all independent commentary.**

- **Pebblous:** "the denominator behind 98% was never published". The metric could be per return or per line item, and it is unclear which returns are excluded [22].
- **Caritas Ventures:** the two numbers measure different things. OpenAI's 97% is drafting accuracy, Forbes's 98% is data-entry accuracy, and both are "up to" ceilings, not averages. "Neither is Thrive Holdings' own revenue, profit, or margin lift public" [19].
- **AgentClaw:** 98% on 7,000 returns implies ~140 returns with errors, if the metric is per return [8].
- **Several analysts:** the 86%-at-≥75%-fields figure means about 14% of returns still had more than a quarter of fields wrong before review. The headline 97% describes the best cases [4].

**Circular deal and attribution (A14).**

- **TechCrunch** called OpenAI's investment "its latest circular deal": Thrive Capital invests in OpenAI, and OpenAI invests in Thrive Capital's holding company. Thrive disputed the label [9].
- **Critics** argue that with OpenAI staff embedded, outsiders can't tell whether results reflect a repeatable product or subsidized engineering that won't scale [29].
- **The vendor side** says the goal "is not to replace accountants" but to free them for client work. One partner reported audit tools saving "hundreds of hours every month" (vendor-sourced) [15].

**Staff reaction (A6, roles replaced).**

- No firsthand staff or partner accounts turned up on Reddit or elsewhere.
- Forbes reports a meeting at Larson Gross where junior staff were told new software would automate parts of their jobs [21].
- The targets are seasonal data entry and junior preparers. Reviewers and signers stay.

**Commoditization.** One commentary argues the same tax-automation capability is now sold to every independent firm by Ramp, Basis, Digits and others, so the edge is ownership and capital, not the agent [21; attribution among the aggregated sources uncertain]. This supports Cyclical's view that single-task agents commoditize.

**Shield.** All metrics (60% of ticket categories, 25× faster, 16-minute median) are vendor claims; I found no independent MSP or customer reviews [26][27].

## Top-level: why they chose this path, and what to learn

**Starting assets and constraints.** Thrive Capital had capital, an early OpenAI stake, and a thesis that AI's value lands in labor-heavy services. A software vendor can only capture a slice of a firm's spend. An owner captures the whole margin gain: cut a firm's labor by a third and its value rises accordingly, at roll-up multiples. Accounting was chosen because of a retiring-partner succession crisis, a shortage of CPA candidates, highly standardized work (IRS forms), and annual volume concentrated in one season, which makes improvement measurable. OpenAI's motive is to show "real economy" deployment and to get deployment lessons and traces. Its upside grows with portfolio success, which explains the forward-deployed engineers.

**Is Thrive already Cyclical in accounting?** No. It is the "own many same-process businesses and pool their work to improve the agent" half of Cyclical, run as a PE roll-up. The other half (the graph, grading against the world, graduation by case type, an orchestrator that proposes reorganizations, structural experiments) is absent from everything public. The probability that Thrive has an unpublished version of the structural half today is about 20%.

**Does it threaten or validate Cyclical's thesis?** Both, but mainly validation:

- Investors paid $12B for "pool across same-process businesses in a vertical, with frontier AI".
- Pooled corrections moved a hard task from 25% to 86% in six weeks.
- Thrive picked one vertical per platform, as Cyclical's realizations recommend.

The threat is to Cyclical's go-to-market, not its loop. Thrive shows that the system-of-record and consent problems are solved by ownership, and that a lab-backed holdco can enter a vertical by buying a platform (ADT) rather than accumulating clinics.

**Would a dental Thrive beat Cyclical?** Inside the offices it owns, yes. It would have full data access, mandated adoption, embedded OpenAI engineers, and could randomize role removal across its own offices without persuading anyone. Across the market, no, for three reasons:

1. **Dental roll-ups already exist.** DSOs covered ~14% of dentists in 2023, and the largest run 1,000+ offices (from memory), so an AI holdco pays full DSO multiples with no succession-crisis discount.
2. **Corporate-practice-of-dentistry laws.** Many states bar non-dentists from owning practices, which forces the DSO management-agreement structure and slows integration.
3. **Graded against the wrong thing.** Thrive's loop grades against reviewers. In dental, the answer keys are show-ups and insurer payment statements, which Cyclical's design uses and Thrive's doesn't.

The realistic threat is Thrive or a peer buying a mid-size DSO outright, as it did with ADT, and embedding lab engineers. I put that at ~25% within 24 months, given the new healthcare-adjacent infrastructure vertical and the ADT precedent.

**Copy:**

- Field-completion bands as the error metric for non-binary tasks.
- Reviewer corrections turned into regression evals, with a coding agent rewriting the harness under test. Use this as Cyclical's level-3 mechanism and its re-certification suite after model swaps.
- Minority equity for selling owners, as a template if Cyclical ever takes ownership.
- **Above all, sell to DSOs first.** One contract covers hundreds of offices, the pool exists on day one, and the DSO already owns the operator, so it answers the system-of-record question the way Thrive does, without Cyclical's capital.

**Avoid:** grading against the human approver where the world answers within weeks; tying the stack to one lab by contract; letting "up to X%" headline metrics stand in for published denominators. Cyclical's credibility edge can be outcome metrics that someone outside the company can check.

**Exploit:**

- Thrive's alignment with OpenAI makes it an awkward partner for DSOs that want model-neutrality or a supplier that won't later compete with them by buying a rival DSO.
- Thrive optimizes the task, not the organization. Cyclical's pooled role-removal tests and orchestrator are what it lacks.
- Thrive's loop has no defense against reviewers rubber-stamping drafts.

**Threat level:** moderate now, rising. These observations would tell David it is rising:

- **Most important: Thrive enters dental, healthcare services or a DSO.** It announces such a vertical or buys a DSO (ADT shows it buys platforms).
- **Thrive starts selling its tools.** Shield's Forge or Current's Tax AI is licensed to firms Thrive doesn't own. That would turn the holdco into a software vendor competing for the same pool.
- **OpenAI starts grading against outcomes.** OpenAI publishes a follow-up where the tax loop is graded against IRS notices or collections, or reports a randomized test across firms of removing a role.

## Sources

1. https://techcrunch.com/2026/08/12/openai-backed-thrive-holdings-raises-2b-to-bring-ai-to-the-enterprise/ (via search extract)
2. https://fourweekmba.com/ai-tax-ai-built-with-openai-ran-7000-returns-at-thrives-firms/ (via search extract)
3. https://openai.com/index/building-self-improving-tax-agents-with-codex/ (via search extract)
4. https://www.krasa.ai/news/openai-thrive-self-improving-tax-agents-codex-may-2026
5. https://x.com/OpenAIDevs/status/2059638868983562640
6. https://cryptobriefing.com/openai-thrive-tax-ai-97-accuracy/
7. https://nerova.ai/news/openai-codex-self-improving-tax-agents-crete-may-27-2026
8. https://www.agentclawhq.com/blog/openai-thrive-accounting-rollup
9. https://techcrunch.com/2025/12/01/openais-investment-into-thrive-holdings-is-its-latest-circular-deal/
10. https://mlq.ai/news/thrive-holdings-raises-2-billion-at-a-12-billion-valuation-to-expand-ai-services-roll-up/
11. https://theaiinsider.tech/2026/08/13/thrive-holdings-raises-2b-at-12b-valuation-to-expand-ai-driven-business-acquisition-model/
12. https://insight.tmcnet.com/insight/thrive-holdings-raises-2-billion-and-targets-infrastructure-approvals-msqh0co0
13. https://techcrunch.com/2026/10/29/openai-backed-thrive-holdings-acquires-adt/
14. https://www.thriveholdings.com/thrive-holdings-adt
15. https://finance.yahoo.com/news/thrive-backed-accounting-firm-crete-130200467.html (Reuters, June 2025)
16. https://app.dealroom.co/news/feed/crete-professionals-alliance-rebrands-as-current-cuts-tax-prep-time-by-31-with-ai-across-7-000-returns
17. https://cfotech.news/story/current-rebrands-to-push-ai-led-tax-work-in-accounting
18. https://www.forbes.com/sites/annatong/2026/06/02/thrive-holdings-to-bet-1-billion-on-ai-powered-accounting-roll-up/ (via search extract)
19. https://caritas.ventures/ai-rollup-market-map/thrive-holdings/
20. https://jupid.com/blog/who-is-buying-accounting-firms-2026
21. https://demg.ai/blog/doctrine-says-thrive-holdings-ai-rollup-owners-exit-engine/ and https://footnote.news/p/private-equity-bet-accounting-was-a-fortress-ai-is-lowering-the-walls (secondary reporting of Forbes's Larson Gross details)
22. https://blog.pebblous.ai/blog/ai-rollup-workflow-records-diligence/en/
23. https://www.bloomberg.com/news/articles/2026-02-02/thrive-holdings-makes-a-100-million-bet-on-ai-for-it-help
24. https://businessof.tech/2026/02/02/shield-secures-second-100m-from-openai-backed-thrive-holdings-for-ai-operations-platform/
25. https://www.channeldive.com/news/shield-technology-partners-nerds-support-acquisition-forge-platform/831181/
26. https://www.channelinsider.com/channel-business/shield-technology-partners-funding/
27. https://www.channelinsider.com/ai/shield-forge-ai-msp-service-delivery/
28. https://www.theregister.com/2025/12/16/shield_technology_partners_nabs_palantir/
29. https://www.techbuzz.ai/articles/openai-s-thrive-holdings-deal-sparks-ai-bubble-concerns
