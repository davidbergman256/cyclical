# Analysis: Lassie

Lassie sells AI agents that run the insurance-payment part of the back office for independent dental practices, and now medical practices too: it pulls remittances from insurer portals, posts payments into the practice software, and reconciles them against the bank. It is the closest company found so far, but it occupies one subgraph. It is not a graph system. **Overlap: 6/10.** It already holds Cyclical's best answer key (remittance plus bank deposit) at 700+ practices and rolls out one insurer at a time, which is a crude form of per-case-type graduation. I found no evidence that it models the business as a graph, mines processes, grades upstream steps, pools outcomes across practices, or runs any shared human desk. The discovery sweep's 7/10 measured where Lassie is heading more than what it ships today.

The most important lesson is that Lassie's bet runs the opposite way to Cyclical's. It is going wide on one process (insurance payments) across many kinds of practice, while Cyclical goes deep on the whole graph of one kind of practice. The two collide only if Lassie moves into the front office, and both depend on the practice-software vendors allowing write access.

Caveat on method: these hosts could not be fetched from this session: a16z.com, sacra.com, lassie.ai, amalgamate.tech, upstartsmedia.com, teero.com, onhealthcare.tech and henryscheinone.com. Facts about them come from search-result extracts, and much of the third-party material is competitors' marketing.

## What it actually is

**Founders and history.**
- **Founders.** Steijn Pelle (CEO, previously consumer fintech at Robinhood and Coinbase) and Frédéric Renken (product at Superhuman and Uber) [1][2][3]. One headline calls them "Ex-Robinhood and Superhuman alums" [3].
- **Origin.** The idea came from Pelle's own dentist. Before writing code, the two did the back office by hand at two offices, one in Menlo Park and one in Scranton: opening envelopes, depositing paper checks, posting payments [2][4][5]. One profile says they "manually operated two medical practices for a full year" [5].
- **Early sales.** Pelle reportedly flew to more than 100 dental offices to implement the product himself before hiring a salesperson [4][6].
- **Pattern.** They did the work by hand first and productized it second, the "Wizard of Oz" approach.

**Funding and traction.**
- **Round.** $35M Series A led by a16z, announced June 3, 2026 (one outlet says August). Total raised is about $47M, at a reported valuation of about $250M from an unnamed source [1][7][8].
- **Angels.** Rahul Vohra (Superhuman), Zach Perret (Plaid), Taavet Hinrikus (Wise), Gokul Rajaram and Brian Balfour, plus Night Capital and Homebrew [1][9].
- **Customers.** 700+ practices in 49 states [1][10]. A later article says "800+ small service businesses" [5].
- **Revenue.** About $10M+ annualized (TechFastForward, unverified) [8]. That implies roughly 25× revenue at the reported valuation.
- **Caveat.** A 2026 industry guide notes that every Lassie metric comes from the company or its investors, with no independent audit [11].

**Product.**
- **What ships.** EFT enrollment (EFT = electronic funds transfer, insurers paying by direct deposit instead of paper check); EOB/ERA retrieval from payer portals (EOB = explanation of benefits, the insurer's statement of what it paid and why; ERA = its electronic form, the X12 "835" file); payment posting into the practice-management system (PMS); EFT-to-bank reconciliation; secondary claims; and, in some descriptions, reading denials and filing appeals [1][10][12].
- **Fee-schedule check.** A June 2026 Lassie blog post says the agent "halts EOB posting when the paid allowable doesn't match your contracted fee schedule." It checks each payment against the contracted fee schedule loaded for that payer before posting (vendor claim) [13].
- **Not offered, per competitor comparisons:** claim submission, eligibility verification, active denial management, pre-authorization, and Denticon support [14][15].
- **Headline metric.** "98% of posting handled autonomously" (vendor figure) [10][16].

**Pricing.**
- **Reported model.** Usage-based: 2% of each claim posted, billed annually, plus a $3,000 setup fee per location. Zentist (a competitor) reports this, and View (another competitor) says Lassie's own blog listed it before the post was removed [14][15][17].
- **Officially.** Lassie now quotes after a demo [15].
- **What 2% means.** It is effectively a percentage of insurance collections. A practice collecting about $750k a year from insurers would pay about $15k a year (my arithmetic).
- **Cross-check.** 700 practices × about $15k ≈ $10M, which matches the reported run rate.
- **Comparison.** A $15k-a-year fee costs about a third of one billing coordinator.

**Architecture.**
- **Local agent.** Dentrix, Eaglesoft and Open Dental run on Windows on the practice's own machines. Lassie installs "a local agent that links Windows-based software to Lassie's servers" [16][12].
- **Rollout.** Lassie goes live "one carrier at a time, so an office can check accuracy on one payer before trusting it with the rest" [16].
- **Time to go live.** One to two weeks for offices already paid by EFT; up to about eight weeks for offices still receiving paper checks (vendor) [15].
- **Exceptions.** Underpayments, mismatched EFTs and ambiguous write-offs are "flagged for staff review" at the practice [16].
- **Bank reconciliation.** One reviewer says it lands monthly, not in real time [14].

**Stated ambition.**
- **a16z:** "Most small businesses are run by reluctant operators… starting with dental, but the broader opportunity is the small business that runs itself" [1][18].
- **Gokul Rajaram:** Lassie builds "autonomous systems that complete operational tasks on behalf of businesses," with healthcare as the "initial market" [19].
- **Pelle:** the next step is "other doctor offices" [7].
- **Other verticals.** No launch outside healthcare is confirmed [7].

## Loop comparison

| Aspect | Lassie's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | One fixed pipeline (remit → post → reconcile → exception). The agent replaces a task; staff backstop it. No business graph. | Absent |
| A2 Observation / onboarding | Connects the PMS (local agent), payer-portal logins and the bank. It reads the systems it automates, not people's work. No process mining. | Different (narrower; the local agent is a good A2 primitive) |
| A3 UX | Output lands in the PMS ledger the office already uses. Staff see only exceptions. | Same in spirit (near-zero new UI), but there is no "send = approve" draft loop |
| A4 Permissions | Standing credentials to payer portals, the bank and the PMS. Nothing published on scoping or just-in-time grants. | Absent |
| A5 Shadow eval | Each office checks one payer before expanding. The grade is the remittance matched to the bank deposit, a world outcome, not agreement with staff. | Partial and better-grounded than most; not a formal shadow stage |
| A6 Checkoff | Exceptions go to staff. No sign of seeded known-bad items or checker grading. | Worse / absent |
| A7 Graduation | Per insurer, per office, decided by the customer's trust, not a statistical bar. "98% autonomous" measures the share not escalated, not an error rate. | Partial (per case type, no statistics) |
| A8 Replacement levels | Posting logic per payer, shared across practices (inferred from the payer-by-payer rollout), plus each practice's fee schedules. Mix of rules and models unknown. | Partly the same (level 1 + level 2, organized by payer) |
| A9 Orchestrator | None. | Absent |
| A10 Shared context | Practice fee schedules, payer contracts, the ledger. Scoped to the payments subgraph. | Narrower |
| A11 Pooling | Holds pooled ERAs and deposits across 700+ practices. No published payer benchmarks, denial statistics or cross-practice experiments. Exceptions go to each practice's own staff, not a central desk. | Latent (data yes, mechanism unproven) |
| A12 Anti-Goodhart | The fee-schedule check guards against underpayment, a business-level guardrail on collections. No upstream optimization exists yet to Goodhart. | Partial |
| A13 Model-agnostic | Not disclosed. The value is in integrations and payer logic, so it is likely agnostic in practice. | Unknown |
| A14 Business model & moat | 2% of posted insurance plus $3k per location (reported). Moat = payer integrations, PMS write access, customer trust, remittance history. Horizontal across practice types. | Different: wide on one process, not deep on one vertical |

**A5/A7: the payer-by-payer rollout is Cyclical's "graduate per case type" built by customer instinct.**
- Each insurer's remittance formats, portal quirks and adjustment codes differ, so "posting for Delta Dental" and "posting for MetLife" really are different case types.
- Lassie lets the office decide when each graduates, which builds trust fast but gives no error bound.
- The grade is better than most of the market's, because the bank deposit is the truth, not a human checker.
- What is missing is a number: no published error rate, no audit sampling, no rule that sends a payer back to human review after a model or portal change.

**A8: Lassie's shared skill is almost certainly organized by payer, not by practice.**
- Learning how to pull and post a given insurer's 835 once serves every practice that insurer pays.
- That is Cyclical's level 1 (shared general skill from the pool) in its most obvious form, and it explains why Lassie scales without per-practice setup beyond fee schedules.

**A11: the key question.** Lassie holds the remittance-plus-deposit answer key for the whole claims subgraph across 700+ practices. Does it use it to grade upstream steps or pool payer behavior?
- **Grading upstream steps: no evidence, and structurally it can't yet.** Lassie does not run eligibility checks, coding or claim submission. A denial on a claim it didn't submit cannot be attributed to the step that caused it, because that step lives in the practice's head or in another vendor (clearinghouses like Vyne Trellis, or Toothy AI).
  - Grading upstream steps needs both the outcome and the run log of the upstream step. Lassie has only the outcome.
- **Pooling payer behavior: the data exists, but nothing is shown.**
  - Every ERA carries reason codes per procedure (CARC/RARC = standard insurer codes for why a line was cut or denied) and the allowed amount.
  - Across 700 practices that adds up to a payer × procedure × region map of allowables and denial reasons.
  - The fee-schedule-mismatch feature [13] uses each practice's own contracted rates, not a pooled benchmark.
  - I found no published payer scorecards, denial-rate benchmarks or "your peers get paid X for D2740" product.
- **Estimate.** ~60% that Lassie already uses pooled payer data internally to build per-payer posting logic (they have to). ~25% that it uses it to grade or advise anything upstream today.

## Where they're ahead of Cyclical

- **They have the answer key, at scale, today.** Cyclical's realizations name "insurer payment statements, bank deposits, show-ups" as the world's grading tape. Lassie collects the first two daily for 700+ practices.
- **They solved legacy-PMS onboarding with a local agent.** Dentrix, Eaglesoft and Open Dental are on-premise Windows software. A local agent that reads and writes the PMS database or drives its interface is the practical answer to Cyclical's A2 "read event logs of tools people already use" for dental, and it has been proven across about 50 states' worth of installs.
- **They found a paid wedge whose output is the outcome.**
  - Posting is the last step of the claims chain, so doing the job produces the grading data as a by-product.
  - Customers pay 2% of collections for it, a pricing unit tied to dollars, not seats, that grows with the practice and doesn't fall when models get cheaper.
- **They earned trust by doing the work by hand first.** A year of manual operation and 100 personally attended installs is how they learned the exception taxonomy. Cyclical's plan has no equivalent step yet.
- **Capital and channel.** $47M, a16z's "small business that runs itself" framing, and 700 practices that already let an outside agent write to their ledger. That last fact is the hardest-won permission in dental software.

## Where they're doing it differently (and whether their way is better)

**Exceptions go to the practice's own staff, not a pooled desk.**
- Competitors describe Lassie as "software your team still backstops" and say "exceptions go to your team" [14][17].
- This keeps Lassie's margin at software levels and avoids running a billing service with licensing, staffing and liability exposure.
- The cost is that the practice keeps its billing person, so Lassie removes hours, not a role. That caps what Lassie can claim and leaves Cyclical's "0.1 of a full-time person per clinic" central desk unclaimed.
- **Better for Lassie's stage; worse for the end state.** Whoever runs the pooled desk sees every hard case, which is the training data for the next 2%.

**Wide on one process, not deep on one vertical.**
- Moving into medical reuses the same skill (pull remits, post, reconcile) on different payers and PMSs.
- That pools *process* knowledge across verticals but not *business-graph* knowledge within one.
- It is the right move for a payments-node company and the wrong move if the aim is to test whether a dental front-desk role can be removed. Pooling by process cannot answer structural questions inside one business type.

**Trust gate instead of a statistical bar.** The payer-by-payer rollout decided by the office is better at adoption than Cyclical's stage 3 math, because practices understand "turn on Delta first." Cyclical should keep the payer-sized rollout as the visible unit and put its error statistics behind it.

**Pricing on dollars, not labor replaced.** 2% of posted collections is simpler to sell than "we replaced 0.6 of a full-time person."

## Feedback & reviews on these parts of the loop

**Independent reviews: essentially none.**
- Searches found no Lassie reviews on G2, Capterra, Dentaltown or r/Dentistry.
- Every comparison page found is written by a competitor (Zentist, View, Teero, Layer3) or by Lassie itself [14][15][17][20].
- That is notable for a company claiming 700+ practices, and it means the 98% figure is unverified.

**Accuracy (A5/A7):**
- "roughly 98% autonomously per its own figures"; "escalates ambiguous cases rather than posting incorrectly" (vendor claim, via third-party summaries) [15][16].
- "No independent audit" (nextmd.ai field guide) [11].

**Exceptions (A6/A11):**
- Teero, a competitor: "AI posts electronic payments (EFTs) into your PMS; exceptions go to your team" [17].
- View, a competitor: Lassie is "software your team still backstops" [15].
- Both say the human layer stays inside the practice.

**Reconciliation timing (A12):** one reviewer says bank reconciliation is monthly, not real time, which contradicts Zentist's description [14]. Unresolved.

**Pricing:** Zentist, a competitor, calls Lassie's pricing "the most transparent pricing in this comparison" [14]. View says the figures came from a since-removed Lassie blog post [15].

**PMS access (A2/A4/A14): the legal environment, not Lassie-specific.**
- In HSO v. Vyne (HSO = Henry Schein One, maker of Dentrix; Vyne = a dental claims vendor), the court issued a split preliminary injunction:
  - Vyne must stop marketing or distributing software that writes back to Dentrix databases without authorization.
  - HSO may not disable Vyne's read-only functions.
  - Sources disagree on the date: commentary says May 12, 2026; HSO's FAQ cites a July 31, 2026 order [21][22][23].
- HSO says it is "closing down unauthorized access methods currently used by certain third-party vendors… not using our approved API program" [22].
- HSO's API Exchange lists 140+ authorized vendors, who must meet SOC 2 Type II and OAuth 2.0 requirements [22][24].
- A health-interoperability analyst summed it up as "Right to Read, but Wrong to Write" [25].
- I could not confirm whether Lassie is an authorized API Exchange vendor or how it writes to Dentrix.
- Payment posting is by definition a write to the ledger. If Lassie writes to Dentrix without HSO authorization, the Vyne ruling is a direct threat. Rough probability that Lassie's Dentrix path is unauthorized direct-database or interface automation: ~50%.
- **Eaglesoft.** Patterson's Innovation Connection program reportedly has an integration backlog [24]. Nothing found on Patterson's stance toward Lassie.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraint.**
- The founders came from fintech (Robinhood, Coinbase, Plaid and Wise angels), so they started from money movement and reconciliation, the most deterministic and best-graded part of a practice.
- Posting was chosen because:
  - it is tedious;
  - it is measurable against the bank;
  - it needs no clinical judgment or patient contact;
  - payers have pushed practices onto EFT and ERA, so the inputs are increasingly machine-readable.
- The constraint was trust: a practice lets an outsider write to its ledger only after watching it be right on one insurer.
- Everything else follows from those two facts: the local agent, the payer-by-payer rollout, exceptions left with staff, and pricing on collections.

**Is Lassie on a trajectory to become Cyclical in dental?** Partly, along a different axis.
- **The likely path** is the whole revenue cycle, the full insurance chain from eligibility through collection (also called RCM, revenue cycle management): eligibility, claims, denials and appeals, then patient balances. Then the same chain in medical, optometry and veterinary.
- **"The small business that runs itself" in a16z's framing** most plausibly means an autonomous back office sold across many small businesses, not a model of each business's whole graph.
- **What would make it Cyclical** is moving into the front office: scheduling, recall, phones, show-ups. Today it shows no sign of that, and the front office is crowded with Weave, NexHealth, Arini and PatientDesk.
- **Probability** that Lassie ships an eligibility or claim-submission product within 12 months: ~60%. That it ships a front-desk or scheduling product: ~20%.
- Even with eligibility and claims, it would become the best-graded occupant of the insurance subgraph, which is still a subset of Cyclical's graph.

**Clone, subset, superset or orthogonal?** Lassie is a **subset in scope** (one subgraph of Cyclical's dental graph) and a **superset in reach** (going across practice types). Cyclical is not a clone. Lassie has no graph, orchestrator, structural experiments or pooled human desk, and no observable cross-practice outcome mechanism.

**What Cyclical should do differently:**

- **Copy:**
  - the local Windows agent as the dental onboarding primitive;
  - payer-sized go-live units ("turn on Delta first") as the customer-facing version of per-case-type graduation;
  - pricing on collected dollars rather than seats;
  - the founders' year of doing the work by hand. Cyclical should run one or two clinics' front office by hand before claiming it knows the graph.
- **Avoid:**
  - **Starting at payment posting.** Lassie is about 700 practices ahead, and View, Teero and Zentist are already there. The wedge is commoditizing toward a 2%-of-collections price.
  - **Writing to Dentrix without HSO authorization.** The Vyne injunction makes unauthorized write-back a litigation target. Read-only access has some legal protection under the Cures Act information-blocking rules; write access does not.
- **Exploit:**
  - **The answer key is not Lassie's alone.** Payments posted by anyone land in the PMS ledger, and deposits land in the bank feed. Cyclical can read both at its own clinics regardless of who posts.
    - What Lassie has that Cyclical lacks is cross-practice scale on day one, not exclusive access.
    - Cyclical's edge is the upstream run logs: who verified eligibility, what was coded, what the front desk told the patient. Only these let a denial be attributed to a step.
  - **The front-office subgraph is open to an outcome-graded entrant.** Lassie does not touch scheduling, recall or show-ups.
  - **The pooled exception desk.** Lassie leaves exceptions with each practice's staff, so the "central desk shared across clinics" model is unclaimed.
- **Partner, don't fight.**
  - Treat Lassie as the occupant of the payments node in Cyclical's graph. Its output is already in the PMS.
  - Combine Cyclical's upstream logs with Lassie's remittance outcomes, ideally through a data-sharing agreement on ERA reason codes, to grade eligibility and claim steps.
  - Lassie gains denial-root-cause attribution it cannot produce alone; Cyclical gains pooled payer outcomes without building posting.
  - Risk: Lassie sees Cyclical as its upstream roadmap and declines.

**Threat level: medium, rising.** Watch for these, in order of how much they would hurt Cyclical:
1. Lassie launches eligibility or claim submission. It would then hold both upstream logs and outcomes for the insurance subgraph and could grade its own upstream steps.
2. Lassie publishes payer benchmarks or denial-rate-by-insurer products. That would show pooling is real.
3. Lassie launches a managed "we run your billing" tier with its own staff on exceptions, i.e. the pooled desk.
4. Lassie ships scheduling, recall or phones, or acquires a front-office tool.
5. Lassie announces HSO API Exchange write access or a PMS acquisition. That would secure the channel Cyclical also needs.

## Sources

1. https://a16z.com/announcement/investing-in-lassie/ (search extract)
2. https://yespress.io/steijn-pelle (search extract)
3. https://techfundingnews.com/ex-robinhood-and-superhuman-alums-raise-35m-in-a16z-led-round-to-let-ai-run-small-businesses-end-to-end/ (search extract)
4. https://founderledsalesstories.substack.com/p/lassie-from-flying-to-100-dental (search extract)
5. https://demg.ai/blog/lassie-35m-ai-running-service-businesses-exit/ (search extract)
6. https://a16zjobs.substack.com/p/how-steijn-pelle-built-lassie-to (search extract)
7. https://www.upstartsmedia.com/p/toothy-ai-lassie-raises-35m (search extract)
8. https://techfastforward.com/articles/lassie-raises-35m-to-run-dental-offices-with-ai-2026 (search extract)
9. https://www.homebrew.co/blog-posts/lassie-raises-usd35-million-series-a-to-save-doctors-the-busy-work ; https://www.startuphub.ai/ai-news/investors-news/2026/lassie-secures-35m-series-a
10. https://tooldirectory.ai/tools/lassie ; https://www.fiercehealthcare.com/health-tech/fierce-healthcare-fundraising-tracker-26
11. https://nextmd.ai/blog/the-ai-tools-running-the-back-office-at-independent-doctors-offices-a-2026-field-guide ; https://nextmd.ai/blog/lassie-raised-35m-to-do-the-back-office-paperwork-so-doctors-don-t-have-to
12. https://www.onhealthcare.tech/p/lassies-47m-a16z-round-and-the-bet-1d2 (paywalled; summary only)
13. https://www.lassie.ai/blog/dental-fee-schedules-underpaid (vendor; search extract)
14. https://www.zentist.io/blog/best-dental-rcm-automation-software ; https://www.zentist.io/blog/best-dental-rcm-software-2026 (competitor)
15. https://view-ai.com/blog/best-dental-insurance-payment-posting-software (competitor)
16. https://www.amalgamate.tech/blog/lassie-ai-review ; https://www.layer3labs.io/comparisons/lassie-ai-alternatives (search extracts)
17. https://www.teero.com/dental-office/payment-posting/compare/teero-vs-lassie (competitor; search extract)
18. https://x.com/a16z/status/2062186811414475005
19. https://x.com/gokulr/status/2062263045003342182 ; https://pulse2.com/lassie-raises-35-million-series-a-to-build-autonomous-ai-systems-for-small-businesses/
20. https://www.lassie.ai/blog/best-dental-payment-posting-software ; https://www.lassie.ai/blog/dental-payment-posting-dentrix-automate-eob (vendor)
21. https://www.readers.id/en/henry-schein-vyne-legal-injunction ; https://www.mogazmasr.com/100534
22. https://www.henryscheinone.com/dental-solutions/api-exchange/customer-faqs/ ; https://www.dentrix.com/insights/blogs/dentrix-vyne-dental-dispute-explained/ (search extracts)
23. https://www.drbicuspid.com/dental-practice/legal-issues/article/15769212/henry-schein-one-committed-to-customer-trust-in-light-of-suit ; https://vynedental.com/?p=25613
24. https://www.henryscheinone.com/dental-solutions/api-exchange/api-exchange-vendors/ ; https://au.finance.yahoo.com/news/patterson-companies-pdco-launch-boost-153700167.html (search extracts)
25. https://healthapiguy.substack.com/p/right-to-read-but-wrong-to-write
26. https://newmarketpitch.com/blogs/news/ai-revenue-cycle-management-top-startups-valuation ; https://avized.com/insights/avized-q3-2026-dental-technology-report
