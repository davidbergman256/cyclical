# Analysis: athenahealth

athenahealth sells a cloud EHR (electronic health record), practice-management software and outsourced billing to about 160,000–170,000 ambulatory clinicians, mostly in independent medical practices. For two decades its pitch has been the closest real-world precedent for Cyclical's A11 + A14 thesis: every payer denial across the network is turned into a billing rule that protects every other practice, delivered by software plus a human operations team and priced as a percentage of collections. **Overlap score: 5/10.** It matches Cyclical on outcome-graded work, cross-customer pooling, outcome-aligned pricing and "compile to rules" (A5, A8 level 3, A11, A12, A14). It has nothing like Cyclical's graph, eval stages or role-removal experiments, and it serves medicine, not dental.

**The most important lesson: the pool worked but was not a moat.** It made athena's billing measurably good, and athena still wins Best in KLAS (a widely used provider-survey ranking) 25 years on. It did not stop the stall. Growth slowed to ~10% by 2017, an activist forced a take-private, and Epic now has about 3× athena's ambulatory install base (19.5% vs 6.9%). Three things combined:
- payer-behavior knowledge saturates;
- payer-behavior knowledge is visible to anyone sitting at a higher-volume chokepoint (clearinghouses);
- athena's buyer, the independent practice, was being bought by hospitals that standardize on Epic.

Cyclical's moat claim survives only if its pool holds data that (a) clearinghouses and practice-software vendors can't see, (b) keeps producing new value rather than saturating, and (c) is attached to a buyer that isn't disappearing.

Research note: the session's network blocked direct fetches of revcycleai.com, techtarget.com and sec.gov, and Reddit was blocked from search. Facts below come from search-result extracts. Items marked "(from memory)" could not be re-checked here. I found no r/medicine or r/medicalbilling threads, so practitioner sentiment comes from review sites and KLAS.

## What it actually is

**Product.** athenaOne bundles three things:
- **athenaClinicals** (EHR);
- **athenaCollector** (practice management and billing: scheduling, claims, payment posting);
- **athenaCommunicator** (patient engagement).

All three run on one multi-tenant cloud platform, historically called athenaNet and now marketed as the "athenaOne Network." Because every client runs on the same instance, a change made once reaches every practice the same day. That single shared instance is what makes the pooling possible. Epic, by contrast, historically ran separate installs per customer. athenaIDX is the enterprise billing product inherited from the 2019 Virence merger (GE's old Centricity/IDX business) [5][15].

**The rules engine.** Third-party descriptions put the athenaOne billing engine at about 29,000–30,000+ rules that check claims before submission and catch payer policy changes [1][2]. The network's real-time rejections and denials feed "regular updates" to the rules engine [1].

The historical mechanism (from memory, consistent with [1][6]) ran in five steps:
1. A claim is denied.
2. athena's operations staff, largely offshore by the 2010s, work the denial.
3. Where the cause generalizes (a payer × procedure × modifier × state combination), they write a rule.
4. The rule then holds or fixes matching claims for every client before submission.
5. Claims stuck past a threshold are escalated by staff who also handle payer enrollment and appeals.

In 2011–12 SEC filings the company described clients as benefiting from "the work athenahealth performs in processing medical claims across more than 900 payers in 45 states." It reported an average client collection rate of 96.1% for FY2011 [6].

**Claimed metrics (all vendor-sourced, none audited):**

| Metric | Claim | Source |
|---|---|---|
| First-pass resolution (share of claims paid on first submission) | 94% (older landing page); 93% (reseller); 98.4% "company-cited" | [1][2][3] |
| First-pass payment success, athenaIDX | 87–94% within the first three months on the product | [4] |
| Days in A/R (average days between service and payment) | 27 days (older page); top-quartile athenaIDX ambulatory clients 27–37 days (Nov 2025 data) | [3][4] |
| Client collection rate | 96.1% average, FY2011 | [6] |

The industry comparison athena used to make was a first-pass rate around 70–80% and A/R of 40–50+ days for a typical practice (from memory). Even on its own numbers the advantage has shrunk. "Top quartile 27–37 days" is a selected subgroup, not the average client.

**Pricing.** athena charges a percentage of net collections, typically estimated at 3–8% depending on bundle and practice size (third-party estimates [7]). It is not a per-seat license. The fee rises with what the practice actually collects, so athena is paid on the same outcome it optimizes. A third-party blog argues athena is more expensive than alternatives for practices collecting under ~$800k a year (opinion, [12]).

**Corporate history.**
- **2007:** IPO.
- **2016:** revenue grew 17% [9].
- **Q3 2017:** revenue of $304.6M, up only 10%, with net income of $13M. R&D was up ~45% year over year. Management cut guidance, citing "weaker utilization trends and a more challenging demand environment," and said products outside the athenaOne core were selling slowly [9][10].
- **2017 activism:** Elliott Management disclosed a 9.2% stake in May 2017. athena rejected an Elliott buyout offer in November 2017 (offer ~$160/share, from memory). About 500 people (9%) were laid off in October 2017 [8][9][10].
- **2018:** founder-CEO Jonathan Bush left in June 2018 amid harassment allegations. Jeff Immelt became executive chairman [8].
- **2018–19 take-private:** Veritas Capital and Elliott's Evergreen Coast agreed to buy the company for ~$5.7B ($135/share). The deal closed in February 2019 and the company merged with Virence. More layoffs followed two months later [8][11].
- **2021–22 resale:** Hellman & Friedman and Bain Capital bought it for ~$17B, announced November 2021 [8][13].

There is still no confirmed second IPO [13]. **Scale:** 160,000–170,000 clinicians, and the company says its network serves "one in five Americans" [1][14][16].

**2025–26 AI (vendor claims):**
- **Feb 2026:** agentic patient communication. Text and voice assistants handle scheduling and FAQs, and an AI waitlist texts patients to fill canceled slots [14].
- **June 3, 2026:** a revenue-cycle roadmap with "80+ AI-native features":
  - Voice AI places over 23,000 prior-authorization calls a month, with status updates typically in under an hour.
  - Express coding, in beta with ~500 clinicians, automates coding on >51% of charges and fully automates nearly one-third of claims.
  - "Payer surveillance and anomaly detection" surfaces payer rule changes "the day they happen."
  - Early results claimed: 30% more recovered payments on coding-related denials and 16% fewer insurance-related denials.
  - Crucially, AI now "monitors every rejection and denial to make same-day updates" to the rules library [15]. This is the old human rule-writing loop, automated.
- **Aug 2026:** athenaAmbient (ambient note-writing) and an "AI-native encounter" available to all ~170,000 clinicians [16].
- **Sept 2026:** "Agentic Care Gap Outreach," which drafts patient outreach "for customer review and approval before they are sent" [17].
- **Nov 2026:** an expansion of Sage, the AI assistant, and a patient-record connection to Anthropic's Claude [14].

## Loop comparison

| Aspect | athenahealth | vs Cyclical |
|---|---|---|
| A1 Core frame (graph, person/agent interchangeable) | Workflow is modeled as claim states and work queues ("holds"). A step is done by the client's staff, athena's ops staff, a rule, or now a voice/coding agent. The interchangeability is real in practice but never formalized as a graph. | Different (implicit, claim-centric) |
| A2 Observation / onboarding | athena *is* the system of record, so it doesn't need to discover anything: every event happens inside its own software. Onboarding is a full migration off the old EHR/PM. | Different (owns the box rather than reading logs; the opposite of "no new box") |
| A3 UX | Work queues inside athenaOne; humans work "claim holds." The 2026 care-gap agent drafts outreach for approval before sending. | Different (new UI, heavy training); same draft-and-approve idea in 2026 |
| A4 Permissions | Standard role-based access in a single SaaS product. No just-in-time grants between nodes. | Absent; but athena *is* the "system node" that answers data requests, which is one answer to Cyclical's UNRESOLVED question |
| A5 Shadow eval graded on outcomes | Claims are graded by the world: a payer's paid/denied response (the remittance) is the label. No human-vs-agent shadow comparison, but the whole engine is outcome-labeled. | Same on outcome grading; Absent on shadowing |
| A6 Checkoff with seeded errors | Human ops review holds; no seeded-error audit of checkers found. | Absent |
| A7 Graduation per case type | Rules are effectively per case type (payer × procedure × modifier). There is no statistical threshold; a rule ships when an analyst judges the pattern real. | Different (judgment, not statistics) |
| A8 Replacement levels | The rules engine is **level 3 run by hand for 20 years**: people compile outcome patterns into deterministic code. 2026 AI automates rule writing ("same-day updates") and fully automates ~1/3 of claims in coding beta. | Same idea at level 3, executed earlier; levels 1–2 and 4 absent |
| A9 Orchestrator proposing reorganizations | None. athena changes its own service model, not the client's org chart. | Absent |
| A10 Shared context layer | One database per practice across clinical, billing and patient data; athena's own staff see across clients. | Better (it owns all the data natively) |
| A11 Cross-business pooling | The core thesis: denials across ~160k clinicians and 900+ payers become rules for everyone. Pooled human operations team = a central exception desk. No randomized experiments on whether a role can be removed. | Same on pooled payer rules and desk; Absent on structural experiments |
| A12 Anti-Goodhart guardrail | Percent-of-collections pricing *is* the business-level guardrail: downcoding to raise acceptance cuts athena's own fee. Coding automation is still graded on denials and recovered payments [15]. | Better (the guardrail is built into the price) |
| A13 Model-agnosticism | Rules are model-free; 2026 AI is an internal stack. Not marketed as model-agnostic. | Different (the asset happens to survive model changes because it is rules plus outcome data) |
| A14 Business model & moat | Asset is claimed to be pooled payer outcome history plus the system of record; percent-of-collections pricing; buyer is independent ambulatory practices. | Same thesis, earlier, in medicine; its history is the test case |

**A8 + A11 are the core of the comparison.** athena built Cyclical's level 3 ("compile to deterministic code when a rule reproduces outcomes") with humans as the compiler and the network as the data source. Its 2026 roadmap swaps the human compiler for AI. What an LLM changes is the latency and labor cost of turning a denial into a rule. It does not change who sees the denial. When rule-writing labor gets cheap, the advantage of athena's large ops team erodes, and the moat shrinks to raw denial volume. Clearinghouses beat athena on raw denial volume (see the competitor-pooling paragraph below).

**A12 is where athena is ahead.** Cyclical treats anti-Goodhart as a separate guardrail eval. athena makes it the revenue line: a percentage of *collections*, not of claims accepted or tasks completed. That single choice rules out the downcoding failure the realizations doc worries about, because downcoding lowers the fee.

**A2/A4: athena resolves Cyclical's open question by being the system node.** It never asks permission to read practice-software data because it is the practice software. That is the "become the system of record" branch of realizations §6, and athena shows its cost: replacing the EHR/PM is the heaviest possible onboarding, which capped how fast the network grew.

## Where they're ahead of Cyclical

- **Proof that pooled denial outcomes can be operated at scale.** For ~20 years one company turned network-wide payer responses into per-case-type rules, across 900+ payers in 45 states by 2011 and ~160k clinicians today [1][6]. Cyclical's "rare segments (insurer × procedure)" pooling benefit is exactly what athena's rule library encodes.
- **Outcome-aligned pricing that works as the guardrail** (A12/A14). Percent-of-collections has survived 25 years and two private-equity owners. It is the commercial form Cyclical should test first.
- **System-of-record ownership.** athena sees the claim, the remittance, the schedule and the note natively, so outcomes are joined automatically. Cyclical has to reconstruct this from event logs and depends on practice-software vendors' APIs.
- **An agent roadmap already in production at scale:**
  - 23,000 prior-auth calls a month by voice AI;
  - ~1/3 of claims fully auto-coded in beta;
  - same-day AI rule updates [15];
  - ambient notes for 170k clinicians [16].

  Any "the incumbent can't do AI" assumption is wrong for athena.
- **Distribution and reputation.** 2026 Best in KLAS Overall Independent Physician Practice Suite (third straight year), plus #1 in the 11–75-physician EHR and PM categories [11a][12a].

## Where they're doing it differently (and whether their way is better)

**Rules vs. evals.** athena ships rules on analyst judgment. Cyclical wants statistical graduation (zero errors in n runs). For payer rules, athena's way is probably right. A denial pattern that recurs across a payer is near-deterministic: once a payer starts rejecting modifier X with code Y, the 3rd example is about as informative as the 300th. Statistical thresholds matter for judgment tasks (coding, outreach copy, clinical notes), and athena has no visible framework there beyond vendor before/after numbers.

**Owning the box vs. reading logs.** athena's full replacement gave it perfect data and slow growth. Cyclical's log-reading approach is faster to install but depends on the practice-software vendor. The DSO analysis in this folder notes dental practice-software vendors restricting API access. athena's history suggests neither is decisive alone: the buyer's ownership structure decided the market.

**Human service as the pooled desk.** athena's "software + service" model scaled headcount: ~5,200 employees by 2016 [9]. That cost is what Elliott attacked: thin margins ($13M net income on $304.6M quarterly revenue) while R&D rose 45% [10]. After 2019 the response was layoffs and consolidation, not smarter routing. Cyclical's pooled exception desk is the same structure, and it only beats athena's economics if graduation actually drains the desk over time.

**Pooling about a third party vs. pooling about the business itself.** Everything in athena's pool describes *payers*: their edits, policies and denial habits. That information is (a) partly published (CMS edits, payer policy bulletins), (b) visible to every intermediary that touches the claim, and (c) saturating. Cyclical's distinctive pool is different in kind. It is about *how a business's own process configuration performs*: which confirmation sequence raises show-ups, whether a front-desk role can be removed. No clearinghouse sees that. This is the main reason athena's failure does not automatically sink Cyclical's moat claim.

## Feedback & reviews on these parts of the loop

**A11/A14, independent verdict on the pool: KLAS.** athena keeps winning the *suite* award, and KLAS's 2026 suites-vs-point-solutions report credits its bundling of software and revenue-cycle services as a strength [12b] (independent). But its KLAS RCM-services score shows as 75.0 (n=19, Oct 2025–Oct 2026, provisional) [11a]. That is solid but not dominant: top revenue-cycle services firms typically score in the high 80s–90s (from memory). The 1–10-physician small-practice award, the segment closest to Cyclical's dental clinics, went to Elation Health, not athena [12a] (independent).

**A3/service, practitioner complaints.** TechRadar's athenaCollector review cites "a multitude of user complaints," centered on support. These include opaque pricing and a report of being charged for technical support, and concerns that the billing component "could be more aggressive, and robust" [18] (independent, secondhand). A third-party 2026 deep-dive argues the tension between private-equity return targets and the R&D needed to "maintain network economy advantages against AI-native competitors" is athena's key vulnerability [13] (independent opinion, not reporting). Reddit was not reachable in this session.

**A8/A11 2026 AI results** (vendor claims only): 30% more recovered payments on coding-related denials, 16% fewer insurance-related denials, prior-auth status 96% faster than humans [15][14]. Coverage disagrees on whether the 30% is recovery or prevention [15]. No independent validation found.

**Metrics drift.** First-pass figures range from 87% to 98.4% across sources and dates. Days in A/R has moved from an all-client "27 days" to a "top-quartile 27–37 days" [1][3][4]. These shifts suggest that either the advantage narrowed or the marketing became more careful. I can't tell which (~50/50).

**Competitor pooling (independent of athena, vendor-sourced):**
- **Waystar** (clearinghouse plus revenue-cycle software, sold to hospitals and practices regardless of EHR) claims 7.5B+ transactions covering ~60% of US patients. It describes its AltitudeAI as "learning from downstream payment outcomes" to create "a self-learning revenue cycle," with agents that resubmit eligible claims [19][20].
- **R1 RCM** (outsourced hospital revenue-cycle operations, taken private 2024 by TowerBrook/CD&R, from memory) claims 600M+ payer transactions a year and $76B+ of net patient revenue on its Phare OS platform [19].
- **Ensemble Health** (outsourced hospital revenue cycle) offers EIQ on Azure, with no outcome data found [19].
- **AKASA** tunes language models on *each customer's own* records, the opposite of pooling [19].

The takeaway is that pooled denial intelligence is now standard across the revenue-cycle industry and is held at larger scale by the clearinghouse layer than by any one EHR vendor.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraints.** athena began in 1997 as a birthing-center operator that couldn't get paid. Its first asset was billing know-how, not software. It bundled human billing service with web software and priced on collections because small practices had no IT staff and wouldn't buy software on faith (from memory). The single cloud instance followed from that: one codebase let one ops team fix a payer problem once for everyone. Activism and the EHR push were later responses to running out of independent practices to sell to.

**Did pooled outcome history prove a durable moat? Four tests:**

| Test | Result | Evidence |
|---|---|---|
| Did the pool produce better outcomes? | Probably yes in 2005–2015 | Vendor metrics well above then-typical practices; years of KLAS wins. Never independently audited. |
| Did the asset persist? | Yes | Still the centerpiece of 2026 messaging, now as AI training data ("AI monitors every rejection") [15] |
| Did it stop competitors or churn? | No | Growth fell to ~10% by 2017 [10]; athena has 6.9% of ambulatory installs vs Epic's 19.5% and eClinicalWorks' 11.9% [21]; KLAS finds Epic has more than twice any rival's mindshare among large practices [21] |
| Did it earn excess returns? | Not as a public company | Thin margins invited activism; value tripled 2019→2021 [8][13], mostly through cost cuts, the Virence merger and market multiples rather than the network |

**Verdict: the pool was real but not durable as a moat.** Five mechanisms explain it, roughly in order of weight:

1. **The buyer disappeared to someone with a different moat.** Physicians in private practice fell from 60.1% (2012) to 42.2% (2024), and hospital-owned practice rose from 23.4% to 34.5% [22]. Hospitals bring acquired practices onto their own Epic install (via Community Connect, Epic's program for extending a hospital's instance to affiliated practices, from memory). In that purchase, collections performance is irrelevant: integration with the hospital decides it. Epic won ambulatory share without any pooled billing rules, only with the system of record and the owner's purchase decision. I put ~60–70% of athena's stall on this market-structure shift rather than on the pool failing.
2. **The content saturates.** Payer behavior is a finite, slowly changing rule set. Once ~30,000 rules exist, the next 10,000 clinicians add little, and first-pass rates top out in the 90s for everyone. Data network effects that plateau protect an early lead but stop widening it.
3. **The content is visible at a bigger chokepoint.** Every denial athena sees also passes through a clearinghouse. Waystar sees ~60% of US patients [19] and sells the scrubbing intelligence to Epic shops too. Edit libraries (sets of pre-submission claim checks) became a commodity feature of clearinghouses and practice-management systems (from memory).
4. **Payers adapt, so the asset is a stream, not a stockpile.** Rules decay as payers change policy. The value lies in current volume plus fast response, which today's AI makes cheap for everyone, not in accumulated history. athena's 2026 pitch says this itself: "surface payer rule changes the day they happen" [15].
5. **Delivering the pool cost a lot of human labor.** The software-plus-service model needed thousands of staff. Margins were thin enough for an activist to argue the network wasn't paying [10].

**What this means for Cyclical's moat claim.** realizations.md says the asset is "an outcome history no model release can produce." athena shows that history alone, if it describes an external party seen by others, is a *feature* that keeps customers loyal, not a moat. Cyclical's claim holds only for pooled data that meets the three tests in the verdict: invisible to clearinghouses and practice-software vendors, non-saturating, and attached to a buyer that is not shrinking. On that standard, Cyclical's insurer × procedure claims pooling is the weakest part of its pitch and repeats athena's ground. Dental claims flow through dental clearinghouses (e.g. Vyne/Tesia, DentalXChange, from memory) that can replicate it. Three parts are genuinely new:
- process-configuration A/B tests on show-ups and collections;
- randomized role-removal trials;
- re-certification of evals after model swaps.

**Copy:**
- Percent-of-collections pricing (or percent of front-office cost saved) as both the price and the anti-Goodhart guardrail.
- One shared instance or rule base so a fix ships to every clinic the same day.
- Remittances as the grading key: athena proves payer responses are a usable, high-volume outcome label.

**Avoid:**
- Putting the moat claim on payer-rule pooling.
- A pooled human desk that grows with customer count. Make "desk headcount per clinic falls each quarter" an explicit metric, because that is the number an activist would have asked athena for.
- Full system-of-record replacement as the entry wedge, which capped athena's growth.

**Exploit:**
- athena never ran structural experiments on its clients' organizations. Its pool optimized one function (billing), never the practice's org chart.
- athena's weakest KLAS segment is 1–10-physician practices [12a]. Dental practices are mostly that size and are outside athena's market entirely.

**The dental analog of athena's failure mode is DSO consolidation.** DSOs play the role hospitals played for athena: they buy practices and standardize their software. If 14% DSO affiliation trends toward the 40–50% physicians reached, Cyclical's independent-clinic buyer shrinks the way athena's did. Cyclical should plan to sell to DSOs as well as to independents. A DSO is a ready-made pool with one decision-maker.

**Threat level: low directly, medium as a template.** athena does not serve dental. Two observations would mean the threat is rising:
- athena (or Epic, which has a dental module for hospitals and community health centers, from memory) announces a dental product or acquires a dental practice-software vendor;
- a dental practice-software vendor (Henry Schein One, Planet DDS) launches a "network-learned" claims engine priced on collections.

The second is the more likely path: realizations §6 already names the system-of-record owner as the strategic risk, and athena is the proof that a system-of-record owner can run this loop.

## Sources

1. business.com, BDC Review of athenahealth's athenaOne — https://www.business.com/reviews/athenahealth/
2. Transcure, athenaOne features / Medical billing guide — https://transcure.net/medical-billing/software/emr/athenahealth-features/ ; https://transcure.net/medical-billing/software/emr/athenahealth/
3. athenahealth medical billing landing page (older) — http://landing.athenahealth.com/g/medicalbilling ; MDS reseller page — https://mdsmedicalsoftware.com/athenahealth/revenue-cycle-management/
4. athenahealth, Enterprise RCM Solutions (athenaIDX) — https://www.athenahealth.com/solutions/revenue-cycle-management
5. Wikipedia, Athenahealth — https://en.wikipedia.org/wiki/Athenahealth
6. athenahealth Form 8-K exhibits, FY2011–2012 (via search extract) — https://www.sec.gov/Archives/edgar/data/0001131096/000095012311040981/b86222exv99w2.htm ; https://www.sec.gov/Archives/edgar/data/0001131096/000119312512063345/d302119dex992.htm
7. athenahealth pricing explainer (third-party) — http://www.athenahealthpricing.com/ ; https://www.ehrsource.com/vendors/athenahealth/
8. Becker's timeline of the acquisition — https://www.beckershospitalreview.com/healthcare-information-technology/a-complete-timeline-of-athenahealth-s-acquisition-may-2017-to-today/ ; Fierce Healthcare — https://www.fiercehealthcare.com/tech/athenahealth-ehr-elliott-management-veritas-capital-5-5b-acquisition-private ; Axios — https://www.axios.com/2021/11/23/athenahealth-elliott-sale-jonathan-bush ; Veritas — https://www.veritascapital.com/pe-deal-of-the-year-athenahealth/
9. athenahealth Q4 2016 prepared remarks (search extract) — https://www.sec.gov/Archives/edgar/data/0001131096/000113109617000010/athnq42016preparedremarks.htm
10. Healthcare IT News, layoffs 2017 — https://www.healthcareitnews.com/news/athenahealth-lays-hundreds-reorganizes-be-leaner ; Boston Globe — https://www.bostonglobe.com/business/2017/10/19/watertown-based-athenahealth-inc-begins-layoffs/Myo8aTnnDXCVKyIUjsYjCP/story.html ; Motley Fool — https://www.fool.com/investing/2017/10/19/premium-athenahealth-inc-cuts-financial-outlook-an.aspx
11. Fierce Healthcare, post-take-private layoffs — https://www.fiercehealthcare.com/tech/two-months-after-going-private-athenahealth-confirms-layoffs
11a. KLAS vendor ratings, athenahealth — https://klasresearch.com/vendor-ratings/athenahealth/61379
12. Health AI Daily, athenahealth for small practices (opinion) — https://healthaidaily.com/blog/athenahealth-worth-it-small-practices-2026/
12a. HIT Consultant, 2026 Best in KLAS full list — https://hitconsultant.net/2026/02/04/2026-best-in-klas-winners-full-list-software-services/ ; athenahealth Best in KLAS page — https://www.athenahealth.com/about/awards/best-in-klas-recognitions
12b. HIT Consultant, KLAS ambulatory suites report 2026 — https://hitconsultant.net/2026/02/09/klas-report-ambulatory-ehr-pm-suites-vs-third-party-2026/
13. revcycleai.com vendor deep dive (search extract) — https://revcycleai.com/blog/athenahealth-vendor-deep-dive/ ; Healthcare IT News, CEO teases IPO — https://www.healthcareitnews.com/news/athenahealth-ceo-teases-second-ipo-new-customer-board-announced ; ipos.fyi — https://ipos.fyi/tracker/athenahealth-ipo
14. Business Wire, agentic patient communication (Feb 2026) — https://businesswire.com/news/home/20260219608674/en/ ; athenahealth press releases — https://www.athenahealth.com/about/press-releases
15. Fierce Healthcare, 80+ AI RCM features — https://www.fiercehealthcare.com/ai-and-machine-learning/athenahealth-rolls-out-over-80-new-expanded-ai-rcm-features-roadmap ; Becker's — https://www.beckershospitalreview.com/finance/revenue-cycle-management/athenahealth-unveils-80-ai-native-revenue-cycle-tools/ ; TechTarget — https://www.techtarget.com/revcyclemanagement/news/366643899/Athenahealth-unveils-over-80-revenue-cycle-AI-features
16. Business Wire, AI-native athenaOne to 170,000 clinicians (Aug 2026) — https://www.businesswire.com/news/home/20260813068205/en/
17. Business Wire, value-based care AI (Sept 2026) — https://www.businesswire.com/news/home/20260924342438/en/
18. TechRadar, athenaCollector review — https://www.techradar.com/reviews/athenacollector
19. TechTarget, Waystar agentic AI — https://www.techtarget.com/revcyclemanagement/news/366649778/Waystar-expands-AI-powered-agentic-revenue-cycle-tools ; RCM rankings (R1, Ensemble, AKASA extracts) — https://theexpertranking.com/healthcare/best-ai-revenue-cycle-management/ ; https://nirmitee.io/blog/best-revenue-cycle-management-software-2026-comparison/
20. Google Cloud press, Waystar — https://www.googlecloudpresscorner.com/2026-03-05-Waystar-Advances-AI-Innovation-with-Google-Cloud-to-Accelerate-the-Autonomous-Revenue-Cycle ; Waystar investor release — https://investors.waystar.com/news-releases/news-release-details/waystar-launches-new-agentic-solutions-transforming-ai-action
21. Definitive Healthcare, top ambulatory EHR systems — https://www.definitivehc.com/blog/top-ambulatory-ehr-systems ; TechTarget, KLAS Epic mindshare — https://www.techtarget.com/searchhealthit/news/366577952/KLAS-Epic-leads-EHR-mindshare-for-independent-ambulatory-care-orgs
22. AMA, Physician Practice Benchmark (2024 data) — https://www.ama-assn.org/press-center/ama-press-releases/more-physicians-move-practices-owned-hospitals-private-equity
