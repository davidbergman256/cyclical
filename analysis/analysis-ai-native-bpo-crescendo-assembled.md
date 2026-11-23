# Analysis: AI-native BPOs / "services-as-software" (Crescendo, Yellow.ai's BPO roll-up, Assembled, Smarter Technologies/Thoughtful AI, AKASA, Infinitus, dental RCM vendors)

This cluster sells Cyclical's back half as a service today. A vendor takes over one function (customer support, or healthcare billing), runs it with AI plus a shared pool of its own human agents, and charges per outcome. That is Cyclical's A11 exception desk and A1 interchangeability, already working commercially: Crescendo reports $100M ARR (vendor claim) about two years after founding, and Smarter Technologies has over $800M of RCM revenue. **Overlap: 6/10.** They match Cyclical on pooled humans plus agents and outcome pricing. They have nothing on the business-as-a-graph frame, process-mining onboarding, statistical graduation per case type, or role-removal experiments, because they sit *outside* the client's business and own one function. **The most important lesson:** buyers don't want to run eval stages themselves. They want to buy a guaranteed outcome and let the vendor carry the risk of handing work to agents. Cyclical's eval machinery may be best sold as a service that is priced on outcomes and runs inside the clinic, not as a tool the clinic operates.

## What it actually is

**Crescendo** (founded 2024) calls itself a "fully-managed AI-native contact center." It runs customer support for enterprises with AI agents plus its own human agents.
- **Humans.** It got them by acquiring the outsourcer PartnerHero in October 2024: about 3,000 support staff and 200+ customers, in the same month as a $50M Series C led by General Catalyst at a $500M post-money valuation [5][6].
- **Traction.** It reported passing $100M ARR in May 2026 (vendor claim; much of that is plausibly PartnerHero's services revenue counted as ARR). Co-founder Andy Lee became CEO on July 14, 2026 [6].
- **Pricing.** Priced per outcome, and the per-outcome pricing covers its human agents too, "from AI Assistants to Superhuman agents, including setup and management charges" [1]. A "Total Outcome Guarantee" promised go-live in 30 days or free implementation, with payment only for positive outcomes (secondary source) [1]. Reported prices conflict: about $2.99 per resolution in most reviews, and $1.25 per resolution plus a $2,900/month service fee in a capture from August 2026. The pricing page was later pulled, and the human tier never had a public price [1][6].
- **Architecture** (vendor and secondary sources). A "Quality agent" scores "100% of conversations against outcomes, performance and policy." When AI confidence falls below preset thresholds, the conversation goes to a human specialist with full context [7][8]. In 2026 it relaunched as an "AI-native Customer Experience Platform: one system that runs and continuously improves the entire customer operation" [9].

**Yellow.ai** is an Indian enterprise conversational-AI vendor with about $34M revenue (secondary) [11].
- **The deal.** On August 3, 2026 it agreed to go public by merging with the SPAC Bluerock Acquisition Corp. (Nasdaq: BLRK), at about $300M pre-money and about $550M pro forma equity value [10][11].
- **The plan.** The deck lists an "active target pipeline" of 10 BPO/CX acquisition targets. Its playbook is to acquire contact centers, deploy Yellow.ai's software, and expand margins by moving "from human agent to outcome-based model" [11]. It cites a $384B category in which about 85% of customer-service calls are still answered by humans [10].
- **Funding.** Committed money is $30M of private placement. The rest is about $175M in the SPAC trust, which public shareholders can redeem [11]. The deal had not closed as of the sources.

**Assembled** is workforce-management (WFM) software for support teams: forecasting contact volume, then scheduling agents to meet it.
- **Customers and pricing.** Customers include Canva, Etsy, Robinhood and Patreon, and it is backed by $70M from NEA, Emergence and Stripe [13]. A third-party listing puts the core WFM tier at $25 per agent per month [13].
- **Humans and AI as one workforce.** Staffing plans count AI agent capacity alongside human FTE. Total capacity is the sum of human and AI throughput, with AI resolution rates set **per contact type**. AI capacity is measured in concurrent sessions and resolution rate, human capacity in FTE and skill coverage [13][14].
- **Recent launches.** Agentic schedule generation became generally available in January 2026, with "human involvement in the design." Assembled's own survey found 45% of respondents doubted AI reliability and 23% feared job loss [12]. Five9 integrated it to plan "across human and AI capacity in real time" [13].
- From memory: Assembled also manages outside BPO vendors' capacity alongside in-house staff, and sells its own AI agent and copilot.

**Healthcare revenue cycle.** RCM is the billing pipeline: eligibility checks, coding, claims, denials, payment posting.
- **Smarter Technologies** was formed in May 2025 when New Mountain Capital combined three companies [15]:
  - Access Healthcare: a large offshore RCM outsourcer with tens of thousands of staff (from memory).
  - SmarterDx: clinical AI that reviews claims before billing.
  - Thoughtful.ai: agents for eligibility checks and claims.
  - The combined company has over $800M revenue, more than 200 clients including 60+ health systems, and about 500,000 providers. It is run by Jeremy Delinsky, former athenahealth CTO, and each unit keeps its own leadership. It describes its AI as "human-in-the-loop" [15].
- **AKASA.** In October 2026 it launched autonomous inpatient coding (coding = turning clinical notes into billing codes), claiming it "matched or exceeded human coders on key accuracy measures for most inpatient cases" (vendor claim) [16]. It starts customers on assistive workflows that keep hospital staff in the loop [16][17]. From memory (about 70% confident): AKASA began around 2019–21 as "Unified Automation," with machine learning plus AKASA's own human operators handling exceptions, i.e. an AI-native outsourcer, and later moved toward software used by hospital staff.
- **Infinitus** builds AI voice agents that make payer phone calls for benefit verification and prior authorization, with humans taking over failed calls (from memory; my searches found no current coverage).

**Dental RCM.**
- **Zentist** is software-first: RPA plus "early-stage agentic AI" for DSOs, priced at 2% per claim posted plus a $3,000 setup fee per location (vendor blog) [18].
- **Infinx** sells AI-plus-human patient-access and RCM services, including dental (from memory; nothing found in search).
- The large human dental-billing outsourcers, such as eAssist (from memory), are the human-only form of the same service.

**Portage report (March 2026).** I could not fetch the PDF: portageinvest.com is outside this session's allowed network, and it has to be allowed to read the full report. From search extracts: "We believe that BPOs are facing an existential threat to their business models. **Industry-specific, business-unit-agnostic orchestration platforms will gain share**." It predicts a move away from per-seat pricing and argues that a smooth implementation justifies switching costs [3].

## Loop comparison

| Aspect | Incumbent cluster's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | The unit is a *queue or function*, not a business graph. Human and AI are interchangeable at the queue level (Assembled: capacity = human FTE + AI throughput, per contact type). | Different (narrower; same interchangeability idea) |
| A2 Observation/onboarding | Takeover through integrations (helpdesk, CRM, EHR/practice software), knowledge-base ingestion and an implementation project ("30-day go-live"). No process mining of the client's whole operation. | Absent |
| A3 UX | Work moves *out* of the client into the vendor's queue, so client staff see no new UI because they no longer do the work. The client gets dashboards. | Different (removes work instead of observing it in place) |
| A4 Permissions | Contract-level data access granted to the vendor (BAA/SOC 2). No just-in-time grants between nodes. | Absent |
| A5 Shadow eval vs outcomes | Crescendo: an LLM "Quality agent" scores every conversation against a rubric (self-graded). AKASA: graded by agreement with human coders. RCM has answer keys from the world (remittances, denials), and outcome pricing ties revenue to them. | Mixed: CX is worse (rubric/agreement), RCM similar in principle |
| A6 Checkoff / anti-rubber-stamp | Traditional QA sampling and calibration. Nothing found on seeded known-bad outputs. | Absent |
| A7 Graduation per case type | Crescendo routes *per conversation* on a confidence threshold. Assembled models AI resolution rates *per contact type*. AKASA moves workflows from assistive to autonomous one at a time (e.g. inpatient coding). No statistical criteria published. | Same direction, less rigorous |
| A8 Levels of replacement | AI first, humans as fallback, RPA still used for deterministic steps (Zentist, Thoughtful). No explicit compile-to-code or regenerate-from-tests discipline. | Partial |
| A9 Orchestrator proposes reorganizations | Vendor operations staff redesign the function inside their own shop. The client gets no reorganization proposals. Yellow.ai's "orchestrator" is a roll-up playbook. | Absent for the client |
| A10 Shared context | Per-client knowledge base and policies. | Same, narrower |
| A11 Pooling across businesses | **The human pool is shared across clients** (Crescendo's ~3,000 staff, Access Healthcare's offshore staff). Pooling of *outcomes* across clients is not documented, and enterprise contracts usually forbid it. | Ahead on the human desk; outcome pooling absent or unproven |
| A12 Anti-Goodhart | Outcome pricing pays for "resolution" as the vendor defines it. No published business-level guardrail beyond CSAT. | Worse: price is a local metric |
| A13 Model-agnosticism | Not disclosed. These are managed services, so the client doesn't care. | Unknown / irrelevant to the buyer |
| A14 Business model & moat | Services revenue, outcome priced; the moat is contracts, a trained workforce and implementation. Yellow.ai: buy cheap BPO cash flows and expand margins. Buyers are enterprises and health systems, not small businesses. | Different buyer, different moat |

**A11 is where they are ahead.** Cyclical's realizations doc proposes "~0.1 of a full-time person per clinic (~1,300 people across 10,000 clinics)" as a central exception desk. Crescendo's 3,000 PartnerHero staff and Access Healthcare's offshore RCM staff are that desk, already staffed, trained, under contract and billable. They also solved how such a desk gets paid: the client pays per outcome and the vendor keeps the gap between price and blended human+AI cost. What none of them shows is pooling of *outcomes* for learning (A/B tests across clients, rare-segment certification, randomized role-removal tests). In enterprise CX each client's policies and knowledge base differ and data-use clauses restrict cross-client training, so the pool is labor, not evidence. Smarter Technologies is the exception to watch. Claims in RCM are standardized (payer × CPT/CDT code), so its 200+ clients do run "the same process," and a remittance is a free answer key. It is the one member of this cluster that could build Cyclical-style pooled outcome history, in medical rather than dental.

**A7: Assembled's per-contact-type model is the closest public match to "graduate per case type."** It treats the AI resolution rate as a parameter that differs by contact type (e.g. password resets versus billing disputes) and plans human staffing for the remainder. That matches Cyclical's bookkeeping example (invoices autonomous, disputes human). The gap is that Assembled takes the resolution rate as an *input to scheduling*, measured after the fact. It has no confidence bound, no "300 clean runs" rule, and no demotion after a model swap. Crescendo's per-conversation confidence threshold is a runtime router, not a graduation decision. It answers "should this case go to a human now?" but never "is this case type certified?"

**A5/A12: outcome pricing is both their best idea and their Goodhart trap.** Pricing per resolution forces the vendor to measure something closer to the real-world outcome than seat-hours do. But the vendor defines "resolved" and grades itself. ZazaChat: "a quality layer built by the same vendor as the agent it audits is not independent oversight, it's a dashboard" [8]. A support agent that deflects, or an RCM agent that downcodes to raise first-pass acceptance, raises vendor revenue under a local metric. That is exactly Cyclical's A12 example. Cyclical's insistence on outside answer keys (bank deposits, insurer payments, show-ups) is a real advantage over CX vendors. In RCM the vendors have the same answer keys available, so the advantage there is smaller.

## Where they're ahead of Cyclical

- **A working delivery and pricing model for "humans + agents as one pooled workforce."** Crescendo went from $0 to $100M ARR in about 2 years (vendor claim) by *buying* a human outsourcer and putting AI in front of it. The client never manages graduation: on day one it gets a price per outcome, and the vendor carries the risk of the AI shift. Cyclical's three-stage eval asks the clinic to trust and watch a process. The services-as-software model asks the clinic to watch only a bill.
- **An exception desk that already exists.** Access Healthcare and PartnerHero already employ, train and quality-check thousands of people doing RCM and support at offshore wages. Cyclical would have to build or buy this.
- **Thinking in contact types.** Assembled plans human and AI staffing with an explicit AI resolution rate per contact type, and the industry is adopting it (Five9 integration). That is the operational version of per-case-type graduation, already in use.
- **Scale in the target pipeline.** Smarter Technologies' $800M revenue and 500,000 providers is a pooled RCM dataset (payer × procedure × denial outcome) of the kind Cyclical's "rare segments" argument needs. It is in medical, not dental.
- **A buyer story that sells.** HFS sizes "services-as-software" at $422B within BPO by 2035 [19]. Yellow.ai is betting its listing on it [10][11].

## Where they're doing it differently (and whether their way is better)

**They pull the work out of the business; Cyclical restructures it in place.** A BPO, AI-native or not, takes a function off the client's hands. That avoids Cyclical's hardest problems (A2 process mining, A3 drafts landing in the user's tools, A4 just-in-time permissions between nodes) because the vendor's own staff and systems do the work. The price is that the vendor can never see or change the rest of the business. Crescendo cannot merge the clinic's front desk with its treatment coordinator, and cannot test whether a role can be removed. That role-removal test is where Cyclical's realizations doc puts the moat. For the jobs Cyclical expects to shrink (billing, insurance checks, phones), outsourcing is the simpler model and probably better for a 9-person clinic. For front-desk work and office management, which are tangled with what happens in the chair, outsourcing can't reach. That's Cyclical's opening (roughly 60% confidence).

**Graduation happens inside the vendor and the client never sees it.** In Cyclical, stages 1–3 and their statistics are shown to the business. In services-as-software they are the vendor's internal cost optimization: the client pays $X per resolution whether a human or an AI did it. The vendor's way is better for adoption, and worse for the client's ability to keep the gains. As AI shares rise, the vendor keeps the margin unless prices are renegotiated. Yellow.ai's deck says this outright: margin expansion comes from "human agent to outcome-based model" [11].

**Enterprise and health-system buyers, not small businesses.** This is the important difference for pooling. Enterprise CX processes are idiosyncratic and contractually siloed, so outcome pooling barely works. Dental clinics run a near-identical process, and DSOs already prove clinics will accept pooled shared services. Cyclical's choice of vertical is the condition for outcome pooling that these vendors mostly lack. The exception is RCM, where processes are standardized because payers standardize them.

**The Yellow.ai roll-up is the strategy General Catalyst also runs (buy the services firm, inject AI, harvest margin), done with a thin balance sheet.** It gives Cyclical a precedent for a "buy a dental billing outsourcer and convert it" path, and a warning. The independent critique is that the targets are Yellow.ai's own customers, which "puts the vendor on both sides," and that only $30M of the $550M headline is committed [11].

## Feedback & reviews on these parts of the loop

**Quality measurement (A5/A6).**
- Vendor: Crescendo's Quality agent scores "100% of conversations against outcomes, performance and policy" [7]. PartnerHero's scoring draws on voice of the customer, ability to solve the problem and NPS [7].
- Independent: ZazaChat on self-grading: "not independent oversight, it's a dashboard". It recommends asking for "the scoring methodology in writing" before treating full coverage as evidence, and asks whether anyone independent has verified the numbers [8].
- A third-party review calls the self-healing QA "a real advance over human sampling" but says Crescendo is priced above pure-software rivals [5].
- Sacra flags "maintaining consistent quality and cultural expertise across diverse markets while managing labor costs" as an operating risk [6].

**Outcome pricing and unit economics (A12/A14).**
- Independent: reviewers could not pin down Crescendo's prices. The pricing page was pulled by September 2026, and "the tier that actually includes Crescendo's human agents never carried a published price" [1].
- An Everest Group finding, cited secondhand on a vendor blog and unverified, says outcome-based models "demand operational transparency and measurement capabilities that some BPO operations lack" [19].
- HFS's own PE survey: only 42% find providers' end-to-end tech + operations + AI claims believable, and 46% are on the fence [19]. HFS also concedes that "true Services-as-Software remains limited, with autonomy lagging platformization" [20].
- Morningstar (March 2026): the total cost of ownership of AI-native systems is "too expensive for widespread adoption at present" [3].
- From memory, rough benchmarks: a fully human outsourced contact costs about $3–6 offshore and more onshore, and pure-AI resolution pricing such as Intercom Fin is about $0.99. Crescendo's $1.25–2.99 sits between the two, consistent with a blended human+AI cost.

**Roll-up strategy (Yellow.ai).**
- Independent: Beri notes that "the BPO assets are genuinely cheap, the automation thesis is genuinely right" but that the plan has a vendor-conflict risk and only $30M committed (via search extract; beri.net was not reachable) [11].
- Tracxn shows no acquisitions since Yellow.ai's 2016 founding, so it has no M&A integration record [11].

**Human/AI split (A7).**
- Assembled's survey: 45% doubt AI reliability and 23% fear job loss, which is why it keeps humans in its schedule generation (vendor survey) [12].
- AKASA: autonomous on "most inpatient cases" (vendor) [16]. A July 2026 interview describes clients whose entire hospital billing is reviewed by AI "with a human still checking the results" [17]. Even the autonomous product keeps a human check, so in practice graduation stops short of full autonomy.

**Employee and customer reviews.** No Glassdoor, Reddit or G2 evidence specific to Crescendo's human pool or to Smarter Technologies' AI/human split turned up in my searches. Zentist has G2 and TrustRadius listings [18], but I did not read their content. This is a real gap.

**Portage (March 2026).** From extracts only: BPOs face "an existential threat," per-seat pricing gives way, and "industry-specific, business-unit-agnostic orchestration platforms will gain share" [3]. That last phrase describes Cyclical's own position: one vertical, many functions, orchestrated together.

## Top-level: why they chose this path, and what to learn

**Starting assets and constraints.**
- Crescendo started from capital and an operator thesis (General Catalyst, which runs the same "buy services, add AI" playbook in rollups) plus a human workforce it acquired.
- Yellow.ai started from software sold *to* BPOs and a stock-market listing whose currency is margin expansion.
- Smarter Technologies started from a private-equity owner holding an RCM outsourcer and two AI startups, and combined them.
- Assembled started from scheduling software, so it frames AI as capacity in a schedule.
- What constrains all of them: enterprises and hospitals already buy BPO by the seat or FTE, so the shortest path to revenue is to replace the seat with an outcome price and keep the procurement relationship. None of them started from the client's whole operation, so none of them can redesign it.

**Copy.**
1. **Price on outcomes and carry the graduation risk.** For dental, Cyclical could charge per verified eligibility check, per paid claim, or per kept appointment, and run stages 1–3 behind the price. This also funds the exception desk.
2. **Treat the exception desk as a business line from day one.** Consider buying or partnering with a dental billing outsourcer (an eAssist-type firm, from memory) instead of hiring 1,300 people. That is Crescendo's PartnerHero move, in dental.
3. **Use Assembled's per-contact-type capacity model** as the orchestrator view's staffing layer.

**Avoid.**
1. **Self-grading.** Publish answer-key-based metrics (insurer remittances, show-ups), since the main critique of this cluster is a vendor grading itself.
2. **Revenue tied to a local metric.** Pair any outcome price with a business-level guardrail, e.g. pay per collected dollar, not per accepted claim.
3. **The enterprise-CX trap, where data can't be pooled.** Write rights to pool outcomes across clinics into the contract at signup.

**Exploit.** Because they sit outside the business, they can't test structural changes. "Can this clinic run without a treatment coordinator?" is a question only a system inside the graph across hundreds of clinics can answer. They also serve enterprises, while small independent dental practices are underserved by both AI-native BPOs and DSOs.

**Relationship.** Cyclical is not a clone. It is a *superset in scope* (whole graph, structural experiments, onboarding by process mining) and *behind in delivery* (no staffed desk, no outcome contract, no revenue). On A11 and the pricing model, the services-as-software cluster is the commercial form of Cyclical's own plan.

**Threat level: medium in dental, high if a dental RCM outsourcer moves first.** These signals would mean the threat is rising:
- Smarter Technologies, Infinx, or a dental billing outsourcer launching an outcome-priced, AI-plus-pooled-human front-office service (eligibility + claims + recall + phones) for *independent* practices.
- A large DSO selling its shared-services center to non-affiliated clinics.
- Crescendo or a Yellow.ai-style roll-up acquiring a dental or healthcare BPO.

Each of these puts a pooled desk and pooled payer-outcome data in dental before Cyclical has either.

## Sources

1. eesel.ai, getmacha.com, makerstack.co: Crescendo pricing reviews (2026). https://www.eesel.ai/blog/crescendo-ai-alternatives ; https://www.getmacha.com/blog/crescendo-ai-complete-guide ; https://makerstack.co/reviews/crescendo-review/
2. aitoolsatlas, ai-cmo.net Crescendo reviews. https://aitoolsatlas.ai/tools/crescendo-ai ; https://ai-cmo.net/tools/crescendo
3. Portage, "AI Disruption in Business Process Outsourcing" (March 2026), search extracts only; host blocked. https://portageinvest.com/wp-content/uploads/2026/03/AI-Disruption-in-Business-Process-Outsourcing_A-Portage-Perspective-March-2026_vF.pdf ; Morningstar: https://www.morningstar.com/markets/how-ai-will-likely-disrupt-it-services-moats ; ISG: https://research.isg-one.com/isg-market-lens/business-process-outsourcing-study-2026
4. Crescendo homepage. https://www.crescendo.ai/
5. SiliconANGLE, Crescendo raises $50M (Oct 2024). https://siliconangle.com/2024/10/02/crescendo-raises-50m-ai-powered-customer-service-platform/
6. Sacra Crescendo profile (search extract; host blocked); Outsource Accelerator on the PartnerHero acquisition. https://sacra.com/c/crescendo/ ; https://news.outsourceaccelerator.com/crescendo-acquires-partnerhero-ai-powered-cx/
7. Crescendo × PartnerHero solution PDF; PartnerHero insights page. https://m.partnerhero.com/hubfs/Crescendo-PartnerHero-Solution-10-02-2024.pdf ; https://www.partnerhero.com/product/insights-reporting
8. ZazaChat, "Can Crescendo's AI Agents Really Run the Whole CX Operation?" https://zazachat.com/news/can-crescendos-ai-agents-really-run-the-whole-cx-b7e177/
9. ZazaChat, Crescendo AI-native CX platform launch. https://zazachat.com/news/crescendo-launches-the-ai-native-customer-experience-platform-one-2c4cce/
10. CMSWire on Yellow.ai's $550M SPAC; Tribune India press release. https://www.cmswire.com/contact-center/inside-yellow-ais-550m-ipo-target-and-vision-to-transform-legacy-call-centers-with-ai/ ; https://www.tribuneindia.com/news/business/yellow-ai-a-global-leader-in-enterprise-agentic-ai-to-go-public-via-550-million-merger-with-bluerock-acquisition-corp/
11. Beri critique (search extract; host blocked); Unite.ai; cacube consulting; StockTitan 8-K. https://www.beri.net/article/yellow-ai-bluerock-spac-550m-bpo-rollup-vendor-risk ; https://www.unite.ai/yellow-ai-goes-public-via-spac-to-roll-up-outsourcing-firms/ ; https://www.cacubeconsulting.com/p/yellow-ai-goes-public-with-a-bold-bpo-transformation-strategy ; https://www.stocktitan.net/sec-filings/BLRK/8-k-bluerock-acquisition-corp-reports-material-event-1e6e276c0ce5.html
12. SiliconANGLE, Assembled schedule generation GA (Jan 28, 2026). https://siliconangle.com/?p=728955
13. Assembled WFM product pages; CX Today on Five9 + Assembled; Assembled job posting (funding, customers); tooliverse pricing. https://www.assembled.com/products/workforce-management ; https://www.assembled.com/page/ai-workforce-management ; https://www.cxtoday.com/workforce-engagement-management/five9-deepens-its-multi-agent-play-with-assembled-workforce-management/ ; https://builtin.com/job/software-engineer-ai-agents/7312223 ; https://tooliverse.ai/tools/assembled
14. WFM Labs wiki, Assembled. https://wiki.wfmlabs.org/wiki/Assembled
15. Fierce Healthcare and HC Innovation Group on the Smarter Technologies formation; BusinessWire launch. https://www.fiercehealthcare.com/health-tech/new-mountain-capital-brings-together-3-companies-form-ai-enabled-rcm-platform ; https://www.hcinnovationgroup.com/finance-revenue-cycle/hospital-and-health-system-operations/news/55291202/three-revenue-cycle-companies-combine-to-form-smarter-technologies ; https://www.businesswire.com/news/home/20250519780986/en/
16. TechTarget, AKASA autonomous mid-cycle coding (Oct 2026). https://www.techtarget.com/revcyclemanagement/news/366651634/AKASA-launches-AI-for-autonomous-mid-cycle-coding
17. Healthcare IT Today, generative AI in RCM (Jul 2026); AKASA GenAI page. https://www.healthcareittoday.com/2026/07/08/unlocking-capabilities-in-revenue-cycle-management-with-generative-ai/ ; https://akasa.com/generative-ai-in-healthcare-revenue-cycle
18. Zentist blog (AI in dental RCM; best RCM software 2026); G2 listing. https://www.zentist.io/blog/how-ai-is-transforming-dental-rcm ; https://www.zentist.io/blog/best-dental-rcm-software-2026 ; https://www.g2.com/products/zentist/reviews
19. HFS Research, "Is this the end of BPO as we know it? SaS creating a $422B market"; HFS "Buying Services-as-Software" webinar; anyreach H1 2026 BPO report (Everest citation). https://www.hfsresearch.com/research/bpo-sas-creating-market/ ; https://www.hfsresearch.com/wp-content/uploads/pdf/HFS-Webinar-Buying-SaS_21-07-2026.pdf ; https://blog.anyreach.ai/h1-2026-report/
20. HFS Horizons: Agentic Services 2026 (hosted by KPMG). https://assets.kpmg.com/content/dam/kpmgsites/xx/pdf/2026/04/hfs-horizons-agentic-services-2026.pdf
21. verifytx.com, Thoughtful AI competitors 2026. https://www.verifytx.com/thoughtful-ai-competitors/

(Note: WebFetch failed on portageinvest.com, sacra.com, sec.gov and beri.net because those hosts are outside the session's allowed network. Claims from them come from search-result extracts only.)
