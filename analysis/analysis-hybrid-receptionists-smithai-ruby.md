# Analysis: Hybrid human + AI virtual receptionists (Smith.ai, Ruby, AnswerConnect, offshore dental front-desk services)

These are outsourced phone desks for small businesses. Smith.ai has gone furthest: an AI answers first and hands off to a shared pool of about 500 North American receptionists (vendor claim), billed per call. Ruby and AnswerConnect remain human-only, using AI as back-office tooling, and offshore dental assistants sell remote human labor by the hour. **Overlap: 4/10.** They already run, commercially and at small-business prices, the two pieces of Cyclical that are hardest to imagine: a person and an agent occupying the same node (the phone) under a routing rule, and one human desk pooled across thousands of businesses. But they model one node, never the graph, and they grade calls on how they sounded, not on what happened after. **The lesson that matters most is incentives.** Smith.ai bills extra when its AI hands a call to a human, so the vendor earns more when its AI is less confident, and the loudest customer complaint is about exactly that. Cyclical's central exception desk has to be priced so that escalations are not a profit center, or the desk corrupts the graduation signal it is supposed to feed.

Caveat on evidence: smith.ai, ruby.com and thunderphone.com could not be fetched from this session (network allowlist), so primary pricing and product pages come through search extracts and third-party pages. Figures from those sources conflict and are marked.

## What it actually is

**Smith.ai** (co-founders Aaron Lee, CEO, and Justin Maxwell) began as a US-based human virtual receptionist service and added an AI receptionist. It now sells three tiers, by its own description [1][2]:

| Tier | What answers | Price per call (sources conflict) |
|---|---|---|
| AI-first | AI 24/7, escalates "only when needed" | from about $1.60 |
| Hybrid | AI plus human, routed by customer rule | from about $2.50 |
| Human-first | live receptionist on every call | from about $7 |

- **AI bundles:** Pro at $150/month for 75 calls and Enterprise at $500/month for 300 calls [3]. Overage is $2.17–$3.00 per AI call [3][10].
- **Human plans:** $300 for 30 calls, $810 for 90 and $2,100 for 300, i.e. $7–$10 per call. Overage is $8.50–$11.50 per call [4][10].
- **Hybrid routing:** set by the customer. One example rule sends new clients to a live agent (about $4.80 per call) and existing clients and all other calls to AI (about $1.80). The hybrid pricing page estimates that **about 30% of calls escalate to live agents** [2].
- **Escalation fees:** the AI-receptionist page says an AI-initiated escalation is free, but the homepage and reviewers cite **$3 per transfer** [2][7].

Smith.ai says it serves 500+ North American live receptionists' worth of capacity and that **"10+ years of live-receptionist operational data"** trained the AI to learn which calls humans handle well. It also says every call is recorded and transcribed, an LLM judge scores every call alongside human reviewers, and an "AI Quality Index" (AQI) drives improvement recommendations. All of this is vendor-stated [8].

Size and funding come only from aggregator estimates:

- funding of about $7M (2019), with one later figure of $13M [5]
- revenue estimated at $26.7M (GetLatka) to $42M (ZoomInfo) [5]
- 282–345 staff [5]
- about 3,000 customers (GetLatka) [5]

Buyers are mainly law firms, then home services, IT services and marketing agencies [5][6]. It is lightly funded and close to profitable on human labor, not a venture-scale AI company.

**Ruby** (Portland, founded 2003; PE-backed, from memory) is human-first. AI runs "behind the scenes": transcripts, sentiment analysis and AI-assisted call flows. The person on the line is always a human receptionist [11]. Its main technology launch was an internal "Receptionist Operating System" for its own agents [11]. Pricing runs $250/month for 50 minutes up to $1,725 for 500, with overage of $3.65–$5.40 per minute [11][12].

**AnswerConnect** is 24/7 human answering that, per several sources, does not use AI to answer calls as a matter of policy [13]. It bills per minute with full-minute rounding plus after-call work: about $350/month for 200 minutes, then $1.85–$2.50 per minute [12][13]. Third-party sources report ratings of about 4.8 on Trustpilot and 4.7 on G2 (unverified) [13].

**Dental remote front desks** are the human version for dentistry:

- **Direct Philippine hires** doing insurance verification and scheduling post at **$5–8/hour** and often require Open Dental, Dentrix or Eaglesoft experience [14].
- **Agency-placed HIPAA-trained assistants** cost **$9–16/hour**, e.g. 3F Solutions at $9/hour full-time [14].
- **"Verification-as-a-service"** sells per verification at **$3–8** [14].
- **Dental AI receptionists with human backup** are emerging. Viva AI is quoted at $399/month AI-only and **$599–899/month for AI plus live agent**. Arini lists human handoff, priced at about $249–550/month (third-party figures) [15].

## Loop comparison

| Aspect | Incumbent's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | One node (inbound phone, sometimes chat). AI and human are explicitly interchangeable occupants, switched per call. No graph beyond "call → message/CRM/calendar/transfer to owner". | **Same in the one node, Absent beyond it** |
| A2 Observation | Onboarding is a script/FAQ form plus integrations (calendar, CRM). No mining of the business's existing logs. | Absent |
| A3 UX | Output lands where the owner works: call summaries in email/text, intake pushed into CRM (Clio, HubSpot; from memory). The owner never touches a new tool. No draft-approval loop. | Similar spirit, no correction signal |
| A4 Permissions | Static: the receptionist gets calendar and CRM write access plus a script. Nothing just-in-time and no rule engine. | Absent |
| A5 Shadow eval | Every call recorded and transcribed. An LLM judge plus human reviewers score "quality, tone, accuracy, adherence"; AQI index [8]. Grades how the call was handled, not whether the lead converted or the patient showed. | **Different (process grading, not outcome grading); Worse on Cyclical's criterion** |
| A6 Checkoff | None. The AI acts live, so there is no pre-send human approval and no seeded bad outputs. The owner can audit transcripts after the fact. | Absent |
| A7 Graduation | **Customer-set routing by caller type** (new client → human, existing → AI) plus AI-initiated escalation on "uncertainty or high-value opportunity" [1][2]. No statistical threshold and no re-certification on model swap (not disclosed). | **Different: manual per-case-type graduation** |
| A8 Replacement levels | Level 1: a shared general receptionist skill trained on pooled call history (vendor claim). Level 2: per-business script and FAQ. No compile-to-code; a phone tree is the deterministic tier, and they sell above it. | Same at L1–L2, Absent at L3–L4 |
| A9 Orchestrator | None. No reorganization proposals. | Absent |
| A10 Shared context | Per-client knowledge base (FAQ, staff list, routing). Narrow. | Worse |
| A11 Pooling | **The human desk is pooled across thousands of SMBs, and the AI skill is pooled across clients.** Outcomes are not pooled, and the business is horizontal (law, home services, IT, agencies), so there are no vertical segments or cross-client experiments. | **Ahead on the pooled desk; Absent on pooled outcomes** |
| A12 Anti-Goodhart | None visible. Per-call and per-escalation billing creates a vendor-side Goodhart: more escalations mean more revenue. | Absent (and the incentive runs the wrong way) |
| A13 Model-agnostic | Not disclosed. Smith.ai presumably runs third-party LLM and voice stacks. The human pool is the model-independent fallback. | Unknown |
| A14 Business model/moat | Per call or per minute. The moat is channel (bar associations, Clio ecosystem, Lawyerist reviews), brand trust and an operated labor pool. No outcome history is sold or used. | Different |

**A1/A7, how routing actually works.** Smith.ai uses two mechanisms at once.

1. **A rule the customer sets per case type, at call start.** "New clients go to a live agent; existing clients and everything else go to AI" [2]. This is Cyclical's "graduate per case type, not per node", done by hand by the owner: existing-client calls have "graduated" and new-client intake has not. Owners choose it for a revenue reason (a new law-firm client is worth thousands), not a statistical one.
2. **AI-initiated escalation mid-call** "when it detects uncertainty or a high-value opportunity" [2]. This is a confidence threshold that nobody outside can audit.

Cyclical should note that SMB owners already accept and understand the first mechanism. The second is where the trust complaints concentrate.

**A5, how quality is measured.** It is call-level process quality: tone, accuracy, script adherence, transcription accuracy, scored by an LLM judge plus humans [8]. No source shows Smith.ai, Ruby or AnswerConnect measuring whether a booked consult showed up, a lead retained the firm, or a caller came back. For a horizontal vendor whose output goes into the client's CRM, that outcome data sits in the client's system. This is the gap Cyclical's thesis predicts. A receptionist vendor cannot grade against the world because the world's answer lands in a system it does not own.

**A11, the pooled desk economics.** Inputs (rough):

| Item | Value |
|---|---|
| Human call price, Smith.ai | $7–10 per call, roughly $2–3/min for a 3–4 minute call |
| Human minute, Ruby | $3.65–5.40 |
| US receptionist wage | about $18–22/hour fully loaded (from memory) |
| Agent occupancy | about 50% |
| AI call price | about $1.60–2.40 |
| AI voice cost | likely $0.20–0.60 per call at current rates (from memory) |

What follows:

- **Human desk:** labor cost is about $0.60–0.75 per handled minute, a gross margin of about 50–70% (*rough*). Pooling is what makes this work. One receptionist covers dozens of firms whose peaks don't coincide, which a single SMB cannot do.
- **AI calls:** priced at about 3–10× their marginal cost.
- **Mixed price:** hybrid's "about 30% escalate" is what sets the blended price.

Revenue per employee of about $95k (GetLatka's $26.7M / 282) is a labor-business number, not a software number [5].

**Implication for Cyclical's numbers.** At Smith.ai's market prices, a dental clinic taking about 40 calls/day (*rough*) would pay roughly $1,800/month (about $21k/year) for AI-first answering. That is double or more Cyclical's own *rough* estimate of $5–10k/year for the clinic's whole agent bill. Either Cyclical is underpricing, or the receptionist market's AI-call margin is a pricing umbrella Cyclical can undercut.

The same 30% escalation rate puts a phone-only exception desk at roughly 0.1–0.2 FTE per clinic: 12 escalated calls × 4 minutes, at 50–100% occupancy. That is in line with realizations.md's ~0.1 FTE per clinic for the whole exception desk, which suggests that figure is optimistic once billing and insurance exceptions are added.

## Where they're ahead of Cyclical

- **An operating pooled human desk with SMB pricing.** Smith.ai's 500 receptionists across about 3,000 customers, and Ruby and AnswerConnect at similar or larger scale, prove that small businesses will accept a shared, remote, rotating human pool at $2–5 per minute. Cyclical's "central desk of leftover humans" is not hypothetical. It is a 20-year-old industry, and Cyclical could subcontract to it rather than build it.
- **Live AI-human switching inside one call.** Warm transfer mid-conversation is shipped and priced. Cyclical's stage-2 "draft in your drafts folder" does not work for synchronous voice. Phone calls cannot wait for approval, so the phone node needs live escalation, not checkoff. Smith.ai has already solved that UX.
- **Ten years of labeled call transcripts** (vendor claim) across verticals, usable to train the shared general receptionist skill.
- **Channel and trust** with law firms (Clio and bar-association ecosystems) and with home services.

## Where they're doing it differently (and whether their way is better)

- **Owner-set routing versus statistical graduation.** Smith.ai lets the owner decide which caller types go to a human. That is legible and matches how owners think about revenue risk. Cyclical's statistical per-case-type graduation is more rigorous, but it should *surface* as a rule of exactly this form ("existing-patient rescheduling now runs on the agent; new-patient calls stay with a person") and let the owner override it. Their way is better on adoption, Cyclical's on evidence. Combining the two is the right design.
- **Process grading versus outcome grading.** An LLM judge on tone and adherence is cheap and immediate, but its ceiling is a well-mannered call that books nobody. Cyclical's approach is better wherever an outcome exists. Show-ups exist in dental; a "retained client" is slower and sparser in law.
- **Horizontal versus vertical.** Smith.ai spreads across law, home services, IT and agencies. That maximizes the desk's load-balancing and the addressable market, but it rules out vertical outcome pooling and deep system-of-record integration. For a receptionist business their choice is right. For Cyclical's thesis it is the reason they can't follow.
- **Per-call pricing versus outcome pricing.** Volume billing is simple, but it puts vendor and client at odds on escalation and on spam calls. Pricing on outcomes (shows, collected revenue) would align incentives but needs the outcome data that only system-of-record access provides.

## Feedback & reviews on these parts of the loop

**Ratings** (all independent platforms, figures via aggregators):

| Platform | Score | n |
|---|---|---|
| G2, human service | 4.9 | 73–115 |
| G2, AI receptionist | 4.7–4.8 | about 33 |
| Capterra | 4.8 | not shown |
| Trustpilot | 4.2–4.4 | about 332–334 |

[7][10]. The gap is typical: G2 and Capterra reviewers are owners invited by the vendor, while Trustpilot draws more billing complaints.

**A7/A12, escalation and incentives (independent):**

- A Trustpilot reviewer says the AI receptionist "transfers calls to live agents without my consent which will raise my bill" [7].
- Aggregated reviews cite $3 per AI-to-human transfer as the most common complaint, alongside $8.50–11.50 human-call overage [10].

This is the clearest evidence on the incentive problem: an escalation threshold that the vendor sets and the vendor profits from destroys trust.

**A1, AI versus human quality as callers experience it (independent):**

- "The AI isn't the favorite of our clients. However, it does an adequate job of capturing data from callers and forwarding them to the correct person" (Trustpilot) [7]. Callers tolerate AI for structured data capture but not for rapport, which matches owners routing new clients to humans.
- Vendor-side, a dental AI vendor concedes that a calm human operator "still has an edge in the highest-stress moments" (urgent pediatric dental calls) [16].

**A11, the cost of pooling for continuity (independent):**

- "Each time there's a call it's a different person handling it" [10].
- Human receptionist quality is "hit or miss" (G2) [10].
- "An outside receptionist will never know your business quite as well as someone sitting in your office" (Capterra) [10].

A pooled desk loses the per-business context that the in-house person carries. For Cyclical, this is the failure mode the per-business layer and shared context (A8 level 2, A10) must prevent for its central desk.

**Reliability (independent, one review):** On Lawyerist, a reviewer writes that "lately more and more calls are going to Smith.ai's voicemail or not being picked up at all" [6].

**Reddit (secondhand):** a review site summarizes the r/LawFirm thread as "mixed, with complaints about scripted calls, value and CMS integration" and a newer r/Lawyertalk thread as leaning positive. I could not verify the threads directly [9]. No r/Dentistry threads on these services surfaced in search.

**A5 (vendor-sourced only):** the LLM-judge review of every call and the AQI index [8]. There is no independent audit of accuracy or of whether these scores predict conversions.

## Top-level: why they chose this path, and what to learn

**Starting asset and constraint.**

- **Smith.ai, Ruby and AnswerConnect** began as labor businesses: trained receptionists, a scheduling and routing operation, and an SMB sales channel. Their revenue is billed minutes or calls. AI entered as cost reduction on that operation. Smith.ai made it caller-facing; Ruby and AnswerConnect kept it backstage and brand themselves as "real humans", which is a defensible position against cheap AI receptionists.
- **Their constraint is position.** They sit at the edge of the client's business: they take the call, hand off a message or booking, and never see what happened next. That is why grading stops at call quality and why pooling stops at a general call-handling skill.
- **Horizontal targeting** keeps the labor pool busy across time zones and industries, which is what makes the desk economics work. It also rules out vertical outcome data.

**Copy:**

1. **Live warm-transfer escalation for synchronous nodes.** Stage 2 of Cyclical's eval cannot be a drafts folder on the phone.
2. **Owner-legible case-type routing rules** as the user-facing form of graduation.
3. **The pooled-desk operating model.** Consider contracting the exception desk to an existing receptionist or offshore dental operator at $5–16/hour in the early phase, rather than hiring.
4. **Record and transcribe everything.** Transcripts paired with outcomes are Cyclical's stage-1 data.

**Avoid:**

1. **Billing that rewards escalation.** Fold the exception desk into a flat or outcome-based fee, and publish escalation rates per case type.
2. **Process-only grading.** In dental, tie phone-node evals to show rate and to production booked, with a guardrail. Example: an agent that books more new patients by over-promising insurance coverage hurts collections and reviews.
3. **Rotating-stranger continuity.** The central desk must work from the shared context, not a script.

**Exploit:**

- They do not own and do not see the dental system of record (Dentrix, Open Dental, Eaglesoft). A Cyclical phone node that writes directly into the practice software and grades itself on attended appointments beats them on the metric owners actually pay for.
- Their AI call prices of $1.60–2.40 sit far above marginal cost, which leaves room to undercut.
- Dental offices already buy offshore human front-desk labor. Those buyers have shown they will outsource the role, and they are a natural wedge for "agents first, pooled humans for exceptions".

**Relationship and threat.** Cyclical is a **superset** of one Smith.ai node. They are a horizontal, single-node, process-graded implementation of A1 plus the A11 human desk, and orthogonal on outcome pooling. Threat level is **low-to-moderate (about 20%** that a receptionist vendor becomes a direct Cyclical competitor in dental within 3 years). The likelier threat to the phone node comes from phone-plus-PMS-connected dental vendors (e.g. Weave) and dental AI receptionists (Arini, Viva).

The threat would be rising if Smith.ai or Ruby did any of the following:

- launched a dental-specific product with write access to Dentrix or Open Dental
- began reporting or billing on booked-and-attended appointments rather than calls
- published cross-client benchmarks such as "show rate by script", meaning they had started pooling outcomes

## Sources

1. https://smith.ai/hybrid-ai-human-receptionists (via search extract)
2. https://smith.ai/pricing/hybrid-ai-human-receptionists and https://smith.ai/pricing/ai-receptionist (via search extract)
3. https://www.hellocounsel.ai/blog/smith-ai-pricing ; https://deployaiworkers.com/blog/smith-ai-receptionist-pricing
4. https://rezora.io/blog/smith-ai-pricing
5. https://tracxn.com/d/companies/smith-ai/__8BnjU62R72adpP4ddWdxuCnBISXebwREkNCLrRrBe6w ; https://www.owler.com/company/smithai ; https://www.zoominfo.com/c/smithai/452682645 ; https://getlatka.com/companies/conversica/vs/smithai ; https://bouncewatch.com/company/smithai
6. https://lawyerist.com/reviews/virtual-receptionists-outsourced-staffing/smith-ai/
7. https://ie.trustpilot.com/review/smith.ai ; https://contractortoolstack.com/software/smith-ai/
8. https://smith.ai/blog/quality-assurance-for-call-systems ; https://smith.ai/ ; https://smith.ai/ai-receptionist (via search extract)
9. https://readbeyondthebar.com/compare/smith-ai-alternatives
10. https://www.ever-help.com/blog/smith-ai-reviews-pros-cons ; https://www.futurocorp.com/blogs/best-smith-ai-alternatives ; https://www.capterra.co.uk/software/181278/smith-ai-live-website-chat ; https://www.cloudtalk.io/blog/smith-ai-review/
11. https://www.ruby.com/ruby-launches-new-receptionist-operating-system/ ; https://www.abby.com/blog/ruby-receptionists/ ; https://www.authencio.com/blog/ruby-review-virtual-receptionists-pricing-alternatives-for-smbs
12. https://upfirst.ai/blog/how-much-does-an-answering-service-cost ; https://www.ringly.io/blog/ruby-receptionist-alternatives
13. https://www.ever-help.com/blog/answerconnect-alternatives-compared ; https://clutch.co/profile/answerconnect ; https://www.getnextphone.com/blog/answering-service-comparison
14. https://3fsolutionsph.com/what-does-a-dental-virtual-assistant-do/ ; https://www.5cvas.com/single-post/virtual-assistant-for-insurance-verification-how-medical-practices-save-15-hours-a-week ; https://himalayas.app/companies/winning-assistants/jobs/dental-virtual-assistant-insurance-verification-scheduling ; https://www.onlinejobs.ph/jobseekers/search/c/insurance--dental-insurance
15. https://avized.com/insights/dental-ai-receptionist-arini-truelark-dentina-viva-compared ; https://www.buildberg.co/blog/dental-ai-receptionist-cost ; https://www.keragon.com/blog/ai-receptionist-dental
16. https://www.patientxpress.us/blog/ai-dental-receptionist-vs-answering-service.html ; https://www.dentalbase.ai/blogs/practice-management/dental-answering-service-vs-virtual-receptionist
