# Analysis: Discovery sweep — incumbents not covered elsewhere

The closest company nobody had covered is **Lassie**. It is a dental (now also medical) back-office agent company with 700+ practices and $47M raised, led by a16z. It grades itself on cash confirmed in the practice's bank account, which is the answer key Cyclical's realizations name, and its lead investor describes the end goal as "the small business that runs itself." Across every other vertical swept (veterinary, legal, property, home services, insurance brokerage, freight, restaurants, salons, e-commerce), the market splits three ways:
- **System-of-record vendors adding assistants:** Toast, Shopify, Clio, IDEXX, Mindbody.
- **Single-task agent startups:** Avoca, Netic, HappyRobot, Encore.
- **Companies that own or become the business:** Long Lake, Harper.

None of them pairs a whole-business graph with outcome grading pooled across businesses, so the thesis survives this sweep. The strongest pattern evidence is that hospitals in 2026 already talk in Cyclical's stage language: agents "start in a shadow-like mode, then earn autonomy" above benchmark thresholds, with periodic audits (Becker's). Notable sells exactly that to health systems. Progressive autonomy is therefore becoming table stakes in healthcare, and the moat has to come from pooled outcomes and structural experiments, not from the stages.

Caveat on method: these hosts could not be fetched from this session: a16z.com, netic.ai, pulse2.com, onhealthcare.tech and hitconsultant.net. Facts about them come from search extracts. Anything marked "(from memory)" was not re-verified.

## Closest missed candidates (deep)

### 1. Lassie — closeness 7/10
URL: https://a16z.com/announcement/investing-in-lassie/ (company site not verified)

**What it is**
- **Product.** An AI back office for independent dental and medical practices. It covers EFT enrollment (EFT = electronic funds transfer from insurers), EOB retrieval (EOB = the insurer's "explanation of benefits" saying what it paid), payment posting into the practice software, EFT reconciliation, secondary claims, appeals and follow-up [1][2].
- **How it connects.** It installs a local agent next to on-premise Dentrix, Eaglesoft or Open Dental, rather than asking the practice to adopt a new tool [2].
- **Scale.** 700+ practices in 49 states and about 250,000 labor hours a year (company figures) [1][2].
- **Funding.** A $35M Series A led by a16z in June 2026, $47M disclosed in total. One outlet puts the valuation at about $250M, citing an unnamed source [1].
- **Autonomy and outcome check.** The company reports that 98% of posting is handled autonomously, and the agent "logs into payer portals, pulls remits, posts payments, and confirms cash in the bank" (vendor claim) [2].
- **Coverage gap.** One review says insurance verification and claim submission are not offered [2].
- **Stated ambition.** The a16z framing is "starting with dental, but the broader opportunity is much larger: the small business that runs itself" [2]. A trade write-up calls it "the bet that autonomous AI can replace the dental front desk" [2].

**Matches**
- (b) Yes. Its success test is a deposit in the bank, which is a real-world outcome rather than agreement with a human.
- (d) Partial. The 98% autonomous rate implies exception routing to humans. No staged graduation mechanism is published.
- (e) Yes. Small practices, run end to end within the payments subgraph.
- (c) Plausible but unconfirmed. One agent across 700 practices sees payer behavior across all of them; there is no evidence it runs outcome experiments.
- (a) Absent. It is a task agent, not a graph.

**Why it matters more than the dental receptionist agents already covered**
- Payment posting is the last node in the insurance subgraph. The EOB and the deposit are the answer key that grades every upstream node: eligibility check, coding, claim submission, denial handling.
- Whoever posts payments therefore holds the grading tape for the whole claims chain, across 700 practices today.
- If Lassie moves upstream into verification and claims, it gets Cyclical's stage-1 outcome grading (A5) and payer-level pooling (A11) for the most valuable dental subgraph, as a side effect of a product practices already pay for.

**What Cyclical should do**
- **Copy:** the local on-prem agent as the A2 onboarding answer for legacy practice software.
- **Exploit:** Lassie has no view of scheduling, show-ups or recall (patients due for their next cleaning), so the front-office graph is still open.
- **Partner option:** treat Lassie as an occupant of the payments node and buy or join its outcome stream.

**What would signal a rising threat:** Lassie launching eligibility or claim submission, publishing denial rates by insurer across practices, or shipping a front-desk product.

### 2. Notable — closeness 6/10
URL: https://www.notablehealth.com

**What it is**
- **Buyer.** Health systems, not small businesses.
- **Product.** Notable calls its platform a "System of Work" where "people and AI agents coordinate across existing applications to complete work from start to finish." Its flows run across the EHR (the hospital's electronic health record) and payer portals: intake, referrals, prior authorization, scheduling [3].
- **Flow Compass (launched 19 Oct 2026).** A governance layer to "build, test and deploy dependable AI automation" with human control [3].
- **Autonomy path.** Notable says deployments start with a human checking the algorithm's output, and that oversight is usually dropped "after a few weeks or months" (vendor claim) [3].
- **Scale.** A sponsored Fierce piece claims over a million workflows a day (vendor claim) [4].
- **Positioning.** Its 2026 positioning is explicitly outcome-based: "2026 will be the year healthcare stops talking about AI and starts demanding outcomes," with "auditable work completion" as the selling point [3].

**Matches**
- (a) Partial. Flows mix staff and agent steps over existing apps.
- (d) Yes, by its own description.
- (b) Partial. It audits that work was completed, not business results such as collections.
- (c) Partial. It runs the same flow templates across many health systems; no evidence of pooled outcome tests.
- (e) No.

**Why it matters**
- Notable is the closest existing product to Cyclical's A1 + A3 + A5–A7 package, and it ships.
- Its buyer choice shows the trade-off Cyclical faces. Health systems have the volume to graduate tasks on their own data and a single buyer to sell to. Small practices have neither, which is the reason for Cyclical's pooling.
- **Threat to Cyclical:** low in dental, since Notable sells to enterprises. It rises if Notable sells a packaged version to small groups or DSOs.
- **Lesson:** the Becker's quote shows hospital buyers already want "shadow mode → earn autonomy above threshold → periodic audit" [5]. Cyclical's sequence will read as familiar, not novel. Its pitch has to be pooled certification ("your clinic graduates in weeks, not years").

### 3. EliseAI — closeness 5/10
URL: https://www.eliseai.com

**What it is**
- **Product.** AI agents for apartment operators: leasing, maintenance requests, renewals, collections. It also has a healthcare line.
- **Funding and scale.** $350M raised at a $4B valuation (29 Sep 2026); ARR above $200M (June 2026); 600+ owners and operators; roughly 1 in 6 US apartment units [6].
- **Apollo (3 Sep 2026).** Its first "agentic AI teammate", able to perform any task in the Elise platform [6].

**Matches**
- (c) Structurally yes. The same leasing and renewal process runs across a sixth of US rental stock. Whether outcomes are pooled for experiments was not found.
- (b) Partial. Leasing conversion and renewals are measurable outcomes it markets on.
- (e) Partial. Its customers are mid-size and large operators, not small landlords.

**Why it matters**
- It is the scale proof that "one vertical, the same process run across many operators" can reach $200M ARR in agents.
- It shows the route Cyclical would take: wedge into one process, then add a general "teammate" that acts across the vendor's own platform.
- It has a second vertical in healthcare, so medical practices are already being approached by a well-capitalized vendor of this kind.

### 4. Harper — closeness 5/10
URL: https://techcrunch.com/2026/02/25/ai-insurance-brokerage-harper-raises-45m-series-a-and-seed/

**What it is**
- **Model.** An AI-native commercial insurance brokerage: it is the licensed broker itself, not a tool sold to brokers [7].
- **Funding and scale.** $46.8M seed and Series A (Feb 2026, led by Emergence); about 6–7k customers, with a target of 100k [7].
- **Operations.** Submission routing, underwriter follow-ups, document collection and the pipeline, run by agents with human brokers. It claims "cross-network synthesis" across wholesalers, MGAs and carriers (vendor claim) [7].

**Matches**
- (e) Yes. It runs the operation end to end, and its customers are small businesses.
- (b) Yes. A bound policy and the commission on it are the outcome.
- (c) Partial. Every carrier interaction pools into one book.
- (d) Implied.

**Why it matters**
- It is the de-novo version of the General Catalyst roll-up logic: become the business rather than sell to it, and own the outcome data by construction.
- In insurance brokerage, the system-of-record risk disappears because Harper is the system of record.
- Compare Outmarket AI ($17M Series A, May 2026), which sells an intelligence layer to 250+ existing brokerages [8].

### 5. Hyperscience — closeness 4/10 (mechanism match, wrong market)
URL: https://www.hyperscience.ai

**What it is (from memory)**
- Enterprise and government document processing.
- Each field gets a confidence score. The customer sets a target accuracy, and the system picks the confidence threshold per field so that only uncertain fields go to a human "Supervision" queue.
- Sampled QA (quality assurance) keeps measuring machine accuracy on fields it handled alone.
- Human corrections retrain the models, so the automation rate rises over time.

**Matches**
- (a) Partial: human and machine are interchangeable per field.
- (d) Yes: graduation is driven by the threshold.
- (b) No: it grades against human-keyed truth, not outcomes.
- (c) No: models are per customer.

**Why it matters**
- It has run Cyclical's stages 2–3 in production for years, at a finer grain than "case type": per field, set by a target error rate.
- **Copy:** let the customer set a target error rate, have the system compute the autonomy threshold, and keep sampled audits running after graduation. That is A7 with a usable control knob.
- **Avoid:** ground truth defined as "what the human keyed." That is the ceiling problem Cyclical's stage 1 rejects.

## Other candidates

| Candidate | URL | What it is | Matches | Score | Why |
|---|---|---|---|---|---|
| Pilot (bookkeeping) | pilot.com | Startup and SMB bookkeeping, tax and CFO service: human accountants plus software, automation share rising, AI-accountant features (from memory) | c, d, e | 4 | The services-as-software human/machine mix across thousands of sets of books; answer key = books close, bank reconciles. Not a graph, no structural experiments |
| Ramp | ramp.com | Corporate card and AP (accounts payable). Agents for controllers auto-approve or flag expenses against policy; price-intelligence benchmarks from pooled customer spend (from memory, 2025) | c, d (partial), e | 4 | Pools cross-customer data into product (vendor price benchmarks), and policy agents go from suggestion to auto-approval. Finance-only subgraph |
| Avoca | avoca.ai | AI agents for home-service businesses across chat, email, voice and SMS through the customer journey; $125M+ at $1B (Apr 2026); 800+ customers [9] | b (booked jobs), e | 4 | Same SMB-operations bet in home services, front-office subgraph only. ServiceTitan analysis mentions it briefly |
| Netic | netic.ai | "AI growth engine for service enterprises" (plumbing, roofing, HVAC); $23M Series B (Founders Fund, Nov 2025), ~$43M total, 66 staff (Sep 2026) [10] | b (revenue booked), e | 4 | Pitches revenue outcomes, not tasks. Targets larger contractors on ServiceTitan; no graph or pooled-experiment evidence |
| Zentist | zentist.io | Dental RCM (revenue cycle management: getting claims paid) for DSOs: remittance automation, claims, eligibility (from memory) | b, c (across DSO locations) | 4 | Holds the same remittance answer key as Lassie but sells to DSOs. Threat if it moves down-market |
| Infinx | infinx.com | Healthcare and dental RCM mixing an offshore human workforce with automation; automation share grows over time (from memory) | a (partial), d | 4 | Closest "AI BPO" (business process outsourcing) analogue in dental billing. Its humans are a pooled exception desk, the A11 idea, sold as a service |
| Rippling | rippling.com | HR/IT/finance platform built on an "Employee Graph"; policies and app permissions derive from role and attributes (from memory) | a (people graph, not process graph), e | 3 | The best existing answer to Cyclical's unresolved A4: permissions as functions of position in a graph, with the system of record as authority. Worth studying |
| Asana AI Teammates | asana.com | AI teammates assigned tasks like people, built on Asana's Work Graph, with human checkpoints (launched Oct 2025, from memory) | a (assignee interchangeable), d (partial) | 3 | Literally "human or agent can be the assignee." No outcome grading, no pooling, not small-business operations |
| Zapier / n8n / Workato | zapier.com, n8n.io, workato.com | Workflow graphs with AI-agent steps and human-approval steps (Zapier has a human-in-the-loop action, from memory) | a | 3 | The graph-with-human-steps primitive is a commodity. Missing: outcome joins, pooling, autonomy staging |
| Shopify Sidekick | shopify.com | Since Winter '26, Sidekick executes admin tasks, not just suggests them; scoped tasks; 58% of admin merchants aware of it [11] | e, c (latent: millions of merchants) | 3 | Archetype of the system-of-record owner that could pool outcomes across merchants and hasn't shown it |
| Toast (Toast IQ) | toasttab.com | Restaurant POS (point of sale) with an AI assistant and peer benchmarks (from memory); nothing on Toast IQ surfaced in search | c (benchmarks), e | 3 | Same archetype in restaurants: holds sales and labor outcomes for ~150k locations (from memory) |
| HappyRobot / Augment | happyrobot.ai | Voice and email agents for freight brokers: carrier sales, check calls, load booking (from memory) | b (load covered, margin), e (partial) | 3 | Freight is outcome-rich and high-volume, but these are task agents with no graph |
| Taktile | taktile.com | Credit-decision platform with backtesting and experiments of decision policies against real defaults (covered in passing in the Aera analysis) | b | 3 | Shows outcome-graded experiments work where outcomes are logged. Lending, not operations |
| Lupa / Digitail (veterinary) | digitail.com; Lupa via [12] | Vet "AI operating systems": Lupa $20M Series A (Oct 2025) replacing 7 tools; Digitail $23M Series B (Nov 2025) with 15+ AI workflows [12] | e | 3 | Vet practice software rebuilt AI-first, i.e. becoming the system of record. No outcome or pooling claims |
| Fyxer AI | fyxer.com | Email assistant that sorts the inbox and writes reply drafts into Gmail/Outlook drafts, learning from the user's edits (from memory) | d (implicit), e | 3 | Ships Cyclical's A3 UX ("sending = approval, editing = correction") at scale. That UX is not a differentiator |
| Encore AI (ex-Insait) | via [13] | Voice and text agents for banks and insurers trained by patented "Interaction Mining" of top human performers' calls; $30M Series A (Team8, Jul 2026) [13] | b (revenue claims), a (weak) | 3 | Imitates the best human, the ceiling Cyclical's stage 1 rejects, though "learn from top performers" is a useful prior |
| Gemini Enterprise (Google) | cloud.google.com/gemini-enterprise | Agent platform with no-code agent designer and connectors to Workspace and M365; Business edition for small teams (from memory) | e (partial) | 2 | Google holds the Gmail and Calendar event logs Cyclical's A2 reads, so it is a latent system-of-record risk for small-business communications |
| AWS AgentCore Evaluations / Amazon Connect | aws.amazon.com/bedrock/agentcore | GA 31 Mar 2026: 13 built-in evaluators; online evaluation on sampled live traffic, which "can only use evaluators that do not require ground truth"; AWS sample repo adds "progressive trust gates" for irreversible actions [14][15] | d (gates), task evals only | 2 | Shows the gap: hyperscaler eval infrastructure has no way to join real-world outcomes. That join is Cyclical's product |
| Anthropic Claude (Cowork, vertical plugins) | claude.com | Desktop agent for knowledge work plus vertical plugins; the Feb 2026 legal plugin knocked 13–16% off legal-data incumbents (per realizations.md) | e (partial) | 2 | The model lab ships the general skill (Cyclical's level 1) for free. Cyclical's value has to sit above it |
| Clio (Clio Work agents) | clio.com | Legal practice management; Clio Work gained agentic mode (Apr 2026) and became standalone for solo and small firms [16] | e | 2 | Legal system-of-record owner adding agents; no outcome grading |
| Square, Mindbody, Boulevard | squareup.com, mindbodyonline.com, joinblvd.com | POS and booking systems adding AI assistants and front-desk agents. Square's 2026 agent work is buyer-side (ChatGPT/Claude integrations, Jul 2026) [11] | e | 2 | Same system-of-record archetype; salon and fitness rebooking rates are a clean outcome nobody grades agents on |
| IDEXX / Covetrus / Mars (VCA, Banfield) | software.idexx.com | Vet software and payments vendors; IDEXX predicts AI invoicing will reshape front-desk work in 2026 [17]. Mars is the vet "DSO" (thousands of hospitals, from memory) | c (latent), e | 2 | Nothing found on agent graphs or outcome pooling. Mars could run randomized role-removal tests across hospitals and shows no sign of doing so |
| Nooks (Node) | nooks.ai/node | "Revenue Agent Platform where human sellers and AI agents work together"; Node AI assistant for sales reps; $500M non-dilutive from GC's Customer Value Fund (Nov 2026) [18] | a (weak) | 2 | Sales teams, not small-business operations. The interesting part is the financing: capital repaid from customer revenue |
| Accenture / Cognizant agent factories | accenture.com, cognizant.com | Builds agents for each enterprise client (from memory) | — | 1 | Delivered per client, so no pooling; enterprise only |
| Cloverpop | cloverpop.com | Decision-intelligence records for enterprise teams | — | 1 | Logs decisions, not processes; no agents occupying steps |

## Flagged names assessed

- **Hyperscience (4).** See deep section. Copy the target-accuracy → threshold → sampled-QA control loop.
- **Encore AI (3).** Learns from top human performers in bank and insurer contact centers. Opposite grading philosophy from Cyclical; no small-business focus.
- **Nooks Node (2).** A sales-rep assistant. Irrelevant except as proof of "humans + agents on one team" framing in sales.
- **Fyxer AI (3).** Proves drafts-in-the-drafts-folder is a shipped, mass-market UX. Cyclical should assume users already expect it.
- **Netic (4).** Outcome-priced home-services growth agents for larger contractors on ServiceTitan.
- **Zentist / Infinx (4 each).** Dental RCM.
  - Zentist holds remittance outcomes for DSOs.
  - Infinx is the human-plus-automation BPO, i.e. Cyclical's pooled exception desk sold as a service.
  - Either could compete for the insurance subgraph; neither models the front office.
- **Vyne Dental (3).** A clearinghouse (the intermediary that routes claims to insurers) and eligibility network. It holds claim outcomes, which makes it a data partner rather than a competitor (already noted in the dental-agents analysis).
- **Overjet / Pearl (3 / 2).** X-ray AI pooled across many practices.
  - Overjet also sells to insurers for claims review (from memory). That makes it the one player that sees both sides of a dental claim, and a potential grader of a claims node.
  - Neither runs operations.
- **Cloverpop (1).** Not relevant.
- **Taktile (3).** Outcome-graded decision experiments, in lending only.
- **Fin, Sam Lessin's company (historically 4, now 0).** From memory:
  - Founded 2015 as a human-plus-AI assistant: people did the tasks while the system recorded them, with automation meant to follow.
  - It never graduated enough tasks because personal-assistant requests are a long tail with no repeated case types and no shared process to pool across.
  - In 2019–20 it pivoted to Fin Analytics, which measured how operations teams work (process analytics).
  - This is the clearest historical evidence for Cyclical's "one vertical, same process" constraint. Without repeated case types, stage 3 never arrives.
- **Botkeeper / Pilot (3 / 4).** Human-plus-machine bookkeeping where automation rises over time.
  - Botkeeper sold to accounting firms, and its later status is uncertain to me (~50% it was wound down or sold by 2025, from memory).
  - Pilot is covered above.
  - Lesson: bookkeeping has a clean answer key (the bank reconciles), yet these companies stayed service businesses with software margins below SaaS. The pooled human desk is a cost line Cyclical must price for.

## Verticals where nobody is doing this

No company in any vertical swept combines a whole-business graph, outcome grading and pooled structural experiments. The gaps that best fit Cyclical's selection rule (high volume, outcomes the world grades, many near-identical small operators):

- **Veterinary (~30k US clinics, from memory).** The closest analogue to dental.
  - Answer keys: appointment show-ups, reminder compliance, invoice capture (missed charges), payment collection. Pet insurance is mostly reimbursement to the owner, so there is no claims answer key.
  - Players: practice software is being rebuilt AI-first (Lupa, Digitail); receptionist agents cost $49–325/month [19]. Nobody pools outcomes.
  - Corporate groups (Mars, IDEXX's installed base) hold the data and do nothing visible with it.
  - Natural second vertical, and lower regulatory weight than dental.
- **Physical therapy and other visit-based allied health.** Insurer remittances and visit adherence are dense answer keys, the work is front-office-heavy, and practices are fragmented. Found no agent-graph player.
- **Independent pharmacy.** Pharmacy-benefit-manager claim responses come back in real time, so this has the fastest answer key of any vertical. No player found.
- **Auto repair.** Estimate-approval rate, show-ups and comebacks (repeat repairs) are clean outcomes. Practice software (Tekmetric, Shopmonkey) adds AI; no pooling found.
- **Freight brokerage.** Very high volume (loads covered, margin per load, on-time delivery) and many small brokers. Agents (HappyRobot) are task-level only.
- **Salons and fitness.** Rebooking rate is a clean outcome. Booking-software vendors add front-desk AI and grade nothing.

Insurance brokerage (Harper), HOA management (Long Lake) and accounting (Crete, Thrive) are being taken by companies that become the business. A software-only Cyclical would be late there.

## Sources

1. https://sacra.com/c/lassie ; https://www.upstartsmedia.com/p/toothy-ai-lassie-raises-35m ; https://www.orrick.com/fr-FR/News/2026/06/Lassie-Raises-35-Million-in-Series-A-Round-Led-By-a16z
2. https://a16z.com/announcement/investing-in-lassie/ (search extract) ; https://www.amalgamate.tech/blog/lassie-ai-review ; https://www.onhealthcare.tech/p/lassies-47m-a16z-round-and-the-bet (search extract) ; https://tooldirectory.ai/tools/lassie
3. https://hitconsultant.net/2026/10/19/notable-introduces-flow-compass-conversational-ai-agent-workforce-governance-ehr-workflows/ ; https://www.notablehealth.com/blog/why-2026-will-be-the-year-healthcare-stops-talking-about-ai---and-starts-demanding-outcomes ; https://www.notablehealth.com/blog/how-ai-agents-and-human-staff-are-powering-the-future-of-healthcare-together ; https://www.healthcaredive.com/news/notable-artificial-intelligence-agents-healthcare/741592/
4. https://www.fiercehealthcare.com/sponsored/company-leveraging-ai-streamline-over-million-healthcare-workflows-daily
5. https://www.beckershospitalreview.com/healthcare-information-technology/ai/kill-switches-guardrails-the-raging-debate-over-healthcare-ai-agents/
6. https://fortune.com/2026/09/29/elise-ai-4-billion-valuation-funding-round-housing-unicorn-andreessen-bessemer/ ; https://siliconangle.com/2026/09/29/eliseai-raises-350m-to-enhance-its-ai-work-automation-suite/ ; https://builtin.com/articles/eliseai-raises-350m-4b-valuation-20260929
7. https://techcrunch.com/2026/02/25/ai-insurance-brokerage-harper-raises-45m-series-a-and-seed/ ; https://www.emcap.com/thoughts/harper-building-the-ai-native-insurance-brokerage-every-business-deserves
8. https://www.prnewswire.com/news-releases/outmarket-ai-raises-17m-series-a-to-power-the-intelligence-era-of-insurance-302770379.html
9. https://theaiinsider.tech/2026/04/29/avoca-closes-125m-at-1b-valuation-to-power-americas-services-economy-with-ai/
10. https://techfundingnews.com/netic-ai-raises-23m-for-plumbers-roofers-home-services/ ; https://tracxn.com/d/companies/netic/__ZAnO0cCEaMKY3x0EXHl2hTfcd2R3hQIFupcHbTQ7HSU ; https://www.roofingcontractor.com/articles/101559-netic-ai-for-roofing-receives-23m-in-series-b-funding
11. https://tenten.co/shopify/shopify-sidekick-2026-deep-dive/ ; https://www.fudge.ai/blog/state-of-shopify-ai-2026/
12. https://www.vetshow.com/london-vet-show-press-releases/lupa-raises-20m-transform-veterinary-space-ai-powered-os-vet-clinics ; https://ventureburn.com/digitail-funding-23m/
13. https://techcrunch.com/2026/07/29/encore-ai-raises-30m-to-build-ai-agents-that-learn-from-customer-calls/ ; https://www.cmswire.com/customer-experience/encore-ai-lands-30m-series-a-for-revenue-agents/
14. https://aws.amazon.com/about-aws/whats-new/2026/03/agentcore-evaluations-generally-available ; https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/evaluations-types.html
15. https://github.com/aws-samples/sample-bedrock-agentcore-evaluations-framework
16. https://www.clio.com/about/press/clio-work-agentic-mode-small-law-firms/ ; https://www.lawnext.com/2026/04/clio-work-clios-ai-workspace-is-now-available-to-solo-and-smaller-law-firms-as-a-standalone-product.html ; https://www.artificiallawyer.com/2026/04/08/clio-rolls-out-agents-for-work-and-vincent/
17. https://software.idexx.com/resources/blog/veterinary-payment-trends-what-to-expect-in-2026
18. https://www.contentgrip.com/nooks-ai-sales-agents/ ; https://runtimewire.com/article/nooks-500m-general-catalyst-node-ai-sales-assistant
19. https://www.vetsoftwarehub.com/article/veterinary-ai-scribe-pricing-comparison-2026 ; https://enterprisedna.co/resources/insights/medical-ai-receptionist-pricing/
