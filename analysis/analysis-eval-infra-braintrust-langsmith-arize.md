# Analysis: Agent eval / observability / improvement infrastructure (Braintrust, LangSmith, Arize, Patronus, Galileo, W&B Weave, HoneyHive; Applied Compute, Adaptive ML, OpenPipe/CoreWeave; Scale/Labelbox/Surge QA)

This cluster sells the parts of Cyclical's eval loop (A5–A8): trace storage, scorers, datasets, regression checks when the model changes, annotation queues, and, at the RL end, distillation from production traffic. It sells none of the loop's logic. Nothing in it grades a human and an agent against the same real-world outcome, seeds known-bad items into a live approval flow, graduates work per case type behind a statistical bound, or compiles agent behavior into rules. **Overlap: 4/10.** The tooling for A5–A7 is genuinely commoditized and should be bought or taken from open source, but A1–A4 and A9–A14 are absent, and the vendors' tenant isolation rules out A11 (pooling) by design. The realization needs one correction: *eval infrastructure* is commoditized, *eval ground truth* is not. Hamel Husain and Shreya Shankar's practitioner work and a July 2026 HBS field experiment both show the hard part is the labels and the checkers, not the dashboards. That is the part Cyclical proposes to own.

## What it actually is

**Horizontal LLM eval and observability (sold to AI engineers at software companies).**

| Vendor | Status (Nov 2026) | Traction / price |
|---|---|---|
| Braintrust | $80M Series B led by ICONIQ, Feb 2026, $800M post-money; Series A was $36M at $150M (Oct 2024) [1][2] | Customers include Notion, Cloudflare, Ramp, Replit, Dropbox (vendor claim) [1]. Pro tier $249/mo with 5 GB and 50k scores, then $3/GB and $1.50 per 1k scores. Online scoring rules *and human reviews are both metered as "scores"* [3] |
| LangSmith (LangChain) | Independent. ~$125M at $1.25B, Oct 2025 (from memory) | Plus ~$39/seat/mo plus per-trace pricing (from memory). Annotation queues and pairwise annotation queues [4][5] |
| Arize (AX + open-source Phoenix) | Independent. $70M Series C, Feb 2025 (from memory) | Classical ML monitoring background: **"delayed actuals" joined to predictions by `prediction_id`**, batch-joined daily at 05:00 UTC, labels updatable later, joined regardless of model version [6] |
| Galileo | Acquired by Cisco, completed May 22, 2026; being folded into Splunk Observability [7] | — |
| W&B Weave | W&B acquired by CoreWeave (2025, ~$1.7B, from memory); now part of CoreWeave Forge [8] | — |
| Patronus AI | Active. $50M Series B, June 2026 (single aggregator source) [9] | Judge models (Lynx), agent debugger (from memory) |
| HoneyHive | Active; no acquisition notice as of Oct 2026 [9] | — |
| Humanloop | Team acqui-hired by Anthropic Aug 2025; platform shut down Sept 2025 [9] | — |
| Langfuse / Promptfoo | Langfuse moved to ClickHouse (Jan 2026); Promptfoo to OpenAI (Mar 2026), both per aggregator [9]. Langfuse is deprecating trace-level LLM-judge evaluators on Nov 16, 2026 [10] | — |

All of them run on the same architecture. An OpenTelemetry-style trace is collected for each agent run. Scorers (code or an LLM judge) run offline over datasets or online over a sampled share of production traces. Feedback is attached to a span or run ID at any time. Experiments are compared side by side, with CI gates that fail a build if scores regress. Braintrust adds "Topics", which clusters production logs into intents and failure modes, and "Loop", an agent that proposes new prompts, scorers and datasets [3].

**"Self-improving agent" and RL-for-enterprise companies.**
- **Applied Compute** (founded by ex-OpenAI researchers) raised $80M at $1.3B in Apr 2026 [11]. It reportedly raised $350M at $3.25B in Nov 2026 and claims a **$100M revenue run rate within 18 months** [12]. Its AC2 loop trains open-weight models with RL, "improves them from production traces" and routes between models [13]. One aggregator reports a $4.5B all-stock acquisition by Palo Alto Networks. I could not confirm it, and it conflicts with the November round (~30% it is accurate) [13].
- **Adaptive ML** (Adaptive Engine: tune and run open models from feedback) was acquired by Datadog in June 2026 [14].
- **OpenPipe** began by distilling GPT-4 workflows into small models and then moved to agent RL. Its ART library is open source and uses RULER, where an LLM judge *ranks* rollouts relative to each other and the ranking serves as the GRPO reward. CoreWeave acquired it in 2025. Its product is now **CoreWeave Model Distillation**, which trains a smaller open-weight model on production traffic, compares it with the incumbent, and shifts traffic gradually [8][15].

**Data-labeling QA.** Labelbox "Benchmarks" are gold-labeled items mixed into the labeling queue. The first five items in a queue are guaranteed to be benchmarks, and each labeler gets an average benchmark score. A project must choose benchmarks *or* consensus, not both [16]. CrowdFlower/Appen "hidden test questions", and similar gold tasks at Scale and Surge, are standard practice for catching inattentive paid labelers (from memory). This is the direct ancestor of Cyclical's A6.

## Loop comparison

| Aspect | Cluster's approach | vs Cyclical |
|---|---|---|
| A1 Graph, person ⇄ agent | Traces of agent runs only; humans appear as reviewers, never as graded occupants of a step | Absent |
| A2 Observation via event logs | Instrument the agent's own code (SDK/OTel). Human work is never ingested | Absent (different object: agent traces, not business events) |
| A3 Minimal UX, drafts = approval | Annotation queues are a *new UI* for reviewers. Thumbs, edits and retries can be logged as feedback if the app captures them | Different; Cyclical's way is better for staff, theirs is better for internal QA |
| A4 JIT permissions | — | Absent |
| A5 Shadow, graded on outcomes | Feedback can be attached to a run ID at any time (Braintrust `logFeedback`, LangSmith feedback API, from memory). Arize ML has first-class delayed-actual joins [6]. No outcome connectors (payments, CRM, PMS), no outcome windows or censoring logic, no grading of the human baseline | Partial: the plumbing exists, the semantics are absent |
| A6 Checkoff + seeded known-bad | LLM tools: annotation queues and pairwise queues, with no hidden-gold injection (~80% confident none ships it natively). Labeling tools: benchmarks/gold, per-labeler scores [16] | Labeling vendors: Same mechanism, different setting. LLM tools: Absent |
| A7 Statistical graduation per case type; demote on swap | Pass rates can be filtered by metadata tag. Experiment diffs and CI gates on model swap are mature. No confidence intervals or significance tests in at least Langfuse [17]; none has a graduation or autonomy state machine | Regression on swap: **Better** (mature, cheap). Graduation: Absent |
| A8 Replacement levels | Level 1–2: prompt and dataset management, few-shot from datasets: Same. Distillation to small models (CoreWeave, Applied Compute, Adaptive): Different. Compile to deterministic code: Absent | Mixed |
| A9 Orchestrator proposing reorgs | Braintrust Loop proposes prompt and scorer changes, not org changes [3] | Absent |
| A10 Shared context layer | — | Absent |
| A11 Cross-business pooling | Strict tenant isolation; pooling customer outcomes would breach their contracts | Absent (structurally) |
| A12 Anti-Goodhart guardrails | Multiple scorers per run, nothing pairing them with a business metric. The "guardrail metric" concept belongs to experimentation platforms (Statsig, Eppo; from memory) | Absent here |
| A13 Model-agnostic | Provider-neutral tracing and scoring; model comparison is the core use case | Same (better tooling) |
| A14 Moat: outcome history, one vertical | Horizontal infrastructure. Moat is developer workflow plus data gravity of traces. Consolidating fast (Galileo, Humanloop, W&B, Promptfoo, Langfuse all absorbed in ~11 months [9]) | Different |

**A5 (shadow on outcomes).** The cluster can store a delayed label but does not know what a label *is*. Arize's ML product is the closest to what A5 needs: a prediction ID, a ground truth that arrives days later, an updated label if it changes, and a daily batch join [6]. That covers "claim submitted, paid 23 days later, partially adjusted at day 40". Arize built this for fraud and credit models, where labels arrive late, and its LLM tracing product sits alongside it. What none of them do is the dental part: connectors to ERA/835 remittance files (the insurer's electronic payment explanation), PMS appointment status and bank deposits; deciding *when* a non-event counts as a failure (an unpaid claim at day 10 is censored, not failed); and grading the **human's** output on the same outcome. That last gap is structural. They instrument agent code, so the human baseline A5 relies on is invisible to them. Getting it requires process mining of human work (A2), which is a different data pipeline.

**A6 (seeded known-bad).** The mechanism is decades old in labeling (gold questions, benchmarks), so Cyclical should copy its operational lessons: front-load gold items when a new checker starts (Labelbox's first-five rule), score each checker, and discount their output. Two differences matter. First, labeling honeypots never ship. A seeded bad draft in a dental office's real Gmail drafts folder could be *sent*, so Cyclical needs a send interlock that intercepts seeded items. No vendor offers one because none works inside the user's own tools. Second, the 2026 HBS field experiment ran 10,088 AI-assisted drug-safety reviews in a preregistered, randomized crossover design. **Low-frequency error injection *reduced* reviewers' odds of catching natural AI errors by 22%. High-frequency injection raised them by 47%**, with no rise in false positives, but at the cost of longer reviews and lower trust in the AI. Control reviewers caught only ~24% of real errors. Catch rates on injected errors predicted catch rates on natural ones [18][19]. Cyclical's "~1 in 50" may sit in the harmful low-frequency regime. I could not see the exact rates the paper used, so treat this as roughly a 50% risk. The rate is an empirical parameter to test, not a constant.

**A6 × A7 link.** No vendor makes this connection, and it is the most useful result here. "Zero errors in n runs ⇒ error < 3/n" assumes every error would have been seen. If audits catch only a fraction q of real errors, the bound is ~3/(n·q). With HBS-like q ≈ 0.24–0.35, 300 clean runs certify < ~9–12%, not < 1%. Seeded items are therefore the *instrument that measures q*, and A7 needs q to be valid, beyond their role in discounting lazy checkers. Where world outcomes grade the output (payments, show-ups), q ≈ 1 and the A7 math holds as written. This is one more argument for A5's preference for world outcomes over approvals.

**A7 (graduation).** Model-swap regression testing (run the golden set on the new model, diff scores, block the merge) is the most commoditized feature in the cluster and should simply be bought. Confidence intervals are not standard. Anthropic's "Adding Error Bars to Evals" (Miller, 2024) recommends standard errors, paired per-question comparisons and clustered SEs, which "can be over 3X larger than naive" ones [20][21]. A practitioner review notes Langfuse lacks significance testing [17]. For Cyclical, the clustering point is concrete: runs within one clinic are correlated, so pooled pass rates need clinic-clustered or hierarchical intervals, or the pool will overstate confidence. Per-case-type tagging is available everywhere (metadata filters). The state machine on top (stage 2 → 3 at a bound, back to 2 on a model swap or audit drift) exists nowhere.

**A8 (replacement levels).** Level 2 (a small per-business layer of retrieved examples) is what these tools' "datasets" already support. The interesting nuance concerns distillation. Realizations.md rejects fine-tuning at the single-business level, which is correct at hundreds of examples. But the level-1 pooled skill sees millions of runs across 10,000 clinics. At that scale CoreWeave-style distillation (production traffic → small open model → gradual traffic shift [15]) is exactly the margin lever behind the ~$99M → ~$51M compute line in realizations.md. Level 3, compiling to code (fitting a simple rule that reproduces the agent's outputs and routing the residue to the agent), is offered by none of the cluster. The nearest neighbors are in browser automation (browser-use "workflow-use", Skyvern code generation, Butter-style trajectory caching; all from memory), which replay recorded actions rather than fitting rules on outcomes.

## Where they're ahead of Cyclical

- **Production-grade plumbing that Cyclical should not rebuild.** Trace storage at GB scale, scorer execution, dataset versioning, side-by-side experiment diffs and CI gating on model swap already ship at ~$249/mo (Braintrust Pro) or free in open source (Phoenix, Langfuse) [3].
- **Arize's delayed-actuals discipline** (prediction ID join, label updates, version-independent matching) is a worked design for A5's data model [6].
- **Failure discovery.** Braintrust Topics clusters production failures without predefined categories [3]. This is a cheap way to *discover* case types for A7, which Cyclical currently assumes are known in advance ("recurring invoices vs. disputes").
- **RL and distillation at scale.** Applied Compute's reported $100M run rate [12] says enterprises will pay for "improve from production traces". CoreWeave and Datadog buying the capability (OpenPipe, Adaptive) [8][14] says the training loop is becoming a feature of infrastructure vendors.
- **Labeling QA know-how**: gold-item scheduling, per-worker scoring, and the consensus-vs-gold choice [16].

## Where they're doing it differently (and whether their way is better)

- **They grade with judges and rubrics; Cyclical grades with world outcomes.** Their way is better wherever no outcome exists or it arrives too late to steer (tone of a patient email, an architecture plan). Cyclical's is better wherever an outcome exists, because a judge's ceiling is its rubric, and Shankar shows rubrics drift as people see outputs [22]. Cyclical's A5 already says to fall back to agreement where nothing grades the output. It should also allow a validated LLM judge as a middle tier, checked against human labels as Hamel Husain recommends [22][23].
- **Explicit annotation queues vs. implicit approval.** Queues yield clean, attentive labels from a few motivated experts. Implicit send/edit signals yield huge volume from distracted staff. Cyclical needs both: implicit signals for volume, plus a small explicit expert queue (a pooled central desk) to validate judges and resolve human–agent disagreements. That makes the A11 exception desk double as the annotation team.
- **Tenant isolation vs. pooling.** Their customers are software companies whose traces are proprietary, so pooling is impossible for them. Cyclical's customers run identical processes and benefit from pooling. This is the cleanest structural reason the cluster cannot become Cyclical.
- **Distillation vs. retrieval.** Their cost lever is a smaller model. Cyclical's per-business lever is retrieval plus compile-to-code. Both are right at their own scale, and Cyclical should use distillation for the pooled level-1 skill.

## Feedback & reviews on these parts of the loop

**Who validates the validators / criteria drift (A5, A6). Independent.** Shankar et al. (UIST 2024) found that grading outputs changes what evaluators count as a failure, so criteria cannot be fully fixed in advance [22]. Hamel Husain's guidance is error analysis first, binary pass/fail judgments with written critiques, one domain expert setting the standard, and LLM judges validated against human labels [22][23]. A 2026 Husain/Saha post argues against outsourcing evals to an LLM [22]. **Implication:** task-level eval *tooling* is commoditized, but the *labels* depend on scarce domain experts. In dental, Cyclical's world outcomes replace much of that expert labor.

**Judge reliability (A5). Mixed.** Braintrust's own article calls treating judge scores as ground truth without human validation a common mistake (vendor, cutting against its own default) [24]. A study guide notes a judge can look accurate while missing most failures if its true-negative rate is low [25]. A comparison site notes Braintrust and LangSmith both run sampled, batch judges, so "a regression shows up in the next batch, not on the turn it happened" (vendor-adjacent) [26].

**Gaps practitioners name (A7). Independent but thin.** An Enterprise DNA review says Langfuse eval runs are slow on large datasets, and it lacks native pairwise comparison and significance testing. It also says teams "typically pair Langfuse with Braintrust" for rigorous eval [17]. A competitor (Latitude) claims none of LangSmith, Braintrust or Langfuse auto-generates evals from production (vendor-sourced) [27].

**Rubber-stamping (A6). Independent, strong.** Covered above: in the HBS 10,088-review field experiment, low injection hurt detection (−22% odds) and high injection helped (+47%), while lowering trust and slowing review [18][19]. A 2,784-person randomized experiment (Beck et al., 2025) found people favorable to automation over-rely on it. *Requiring corrections for flagged errors reduced engagement and increased acceptance of wrong suggestions* [28]. That is a warning for "editing = correction" if edits feel like extra work. EU AI Act Art. 14 explicitly names automation bias for high-risk systems [29].

**Pricing friction (A5 online scoring).** Braintrust meters online scores and human reviews as billable "scores" ($1.50–$2.50 per 1k) [3]. Scoring every production run with a judge is a real cost line, which favors world outcomes (free) over judges. Competitor Pydantic Logfire markets the absence of a per-score meter [3].

**Vendor durability.** Four well-known platforms (Humanloop, W&B, Langfuse, Galileo) were acquired or shut down within ~11 months, and Langfuse is removing trace-level evaluators on Nov 16, 2026 [9][10]. Building on a proprietary eval SaaS carries real migration risk.

I could not reach G2 or vendor doc sites (network-blocked), so there are no review scores with sample sizes.

## Top-level: why they chose this path, and what to learn

**Starting assets and constraints.** Braintrust and LangSmith began as developer tools for AI engineers. LangSmith grew out of the most popular agent framework's install base; Braintrust started from the founder's experience building eval tooling at Impira and Figma (from memory). Their buyer ships many different AI features, so the product had to be horizontal, provider-neutral and judge-based: no shared outcome exists across their customers' apps, and tenant data cannot be pooled. Arize came from ML monitoring, which is why it alone treats delayed ground truth as first-class. The RL companies started from frontier-lab training expertise and sell to large enterprises with enough volume to train on their own traces. Applied Compute's customers have millions of runs. A 9-person dental office has hundreds. That volume gap is exactly why Cyclical needs pooling and they don't. The labeling vendors' honeypots exist because their workers are paid per item and anonymous.

**Copy / avoid / exploit.**
- **Buy (or use open source):**
  - tracing and span store
  - scorer runtime
  - dataset and prompt versioning
  - experiment diffs and model-swap regression gates
  - an internal annotation UI for the central desk
  - LLM-judge infrastructure
  - production-trace clustering to discover case types
  - distillation for the pooled level-1 skill (CoreWeave/Fireworks-style)

  Prefer open-source, self-hostable options (Phoenix, Langfuse) given the consolidation churn.
- **Build. These are offered nowhere, and they are the product:**
  1. **Outcome connectors with business semantics**: ERA/835 remittance, PMS show/no-show, bank deposits, joined to the runs of both humans and agents, with outcome windows and censoring. Copy the data model from Arize's delayed actuals.
  2. **Implicit-label capture** from the user's own tools (sent unchanged = approve; edit diff = correction; deleted = reject). GitHub Copilot's acceptance and retention metrics are the precedent (from memory).
  3. **Seeded-error injection into live workflows**, with a send interlock, per-checker credibility scores, an injection rate tuned by experiment (not fixed at 1/50), and the measured catch rate q fed into the A7 bound.
  4. **A graduation state machine** per (process, case type, model): exact or clustered intervals, pooled hierarchical estimates across clinics, automatic demotion on model swap or audit drift.
  5. **Paired guardrails** (task metric + business metric). Borrow the concept from experimentation platforms, not eval tools.
  6. **Compile-to-code** by fitting simple rules to agent input/output and keeping the agent for the residue.
  7. **Cross-tenant pooling**, which these vendors are contractually unable to do.
- **Avoid:** judge-score dashboards as the success metric; per-score metering on every production run; making staff work in a queue UI.

**Is Cyclical a clone, subset, superset or orthogonal?** A superset that should sit *on top of* this cluster. Cyclical's A5–A7 is the cluster's infrastructure plus three things the cluster lacks: an outcome oracle, a model of checker reliability, and pooled statistics. The cluster has nothing of A1–A4 or A9–A14.

**Threat level: low from the observability vendors, medium from the RL/"self-improving" players.** Applied Compute ($100M run rate, "improves from production traces"), OpenAI Frontier (which, per realizations.md, already ships evals plus self-improvement), and Datadog+Adaptive could move down-market into a vertical. **Signals the threat is rising:**
- Braintrust, LangSmith or Arize ship **native outcome connectors** (Stripe, Salesforce, EHR/PMS events as labels) together with **autonomy levels or graduation with confidence intervals**.
- Any of them offers **opt-in cross-customer benchmarks** pooled within a vertical.
- Applied Compute, Datadog or OpenAI announces a **dental or healthcare RCM** design partner (RCM = revenue-cycle management: billing, claims and collections).

The first of these is the most likely, at ~35% within 18 months, because "online evals with business KPIs" is the obvious next pitch once tracing is commoditized.

## Sources
1. https://chatforest.com/reviews/braintrust-ai-eval-observability-platform/ and https://www.icharles.com/articles/braintrust-series-b-ai-observability
2. https://multiples.vc/private-comps/braintrust
3. https://www.truefoundry.com/blog/braintrust-pricing ; https://braintrust.dev/pricing ; https://pydantic.dev/logfire/vs-braintrust (via search extracts)
4. https://docs.langchain.com/langsmith/annotation-queues
5. https://changelog.langchain.com/announcements/pairwise-annotation-queues-for-comparing-agent-outputs
6. https://arize.com/docs/ax/machine-learning/machine-learning/concepts-ml/how-to-send-delayed-actuals ; https://arize.com/docs/ax/machine-learning/machine-learning/how-to-ml/upload-data-to-arize/sending-data-faq
7. https://blogs.cisco.com/news/cisco-announces-the-intent-to-acquire-galileo ; https://www.channelinsider.com/channel-business/mergers-and-acquisitions/cisco-galielo-acquisition-2026/
8. https://coreweave.com/blog/closing-the-loop-between-inference-and-post-training ; https://latent.space/wiki/openpipe-cf55dcb1/
9. https://www.developersdigest.tech/blog/llm-observability-acquisitions-2026 ; https://atlan.com/know/ai-agent/ai-agent-evals/braintrust-alternatives/
10. https://dev.to/shubhampalriwala/langfuse-trace-level-evaluators-stop-on-november-16-2026-what-to-do-54c3
11. https://seedtable.com/companies/applied-compute/funding-rounds/series-a-2026-04
12. https://peepalsglobal.com/tech/article/applied-compute-350-million-3-25-billion-valuation-100-million-run-rate-2026-11-04
13. https://sacra.com/c/applied-compute/ ; https://agentspulse.github.io/tutorials/applied-compute-acquisition/
14. https://en.wikipedia.org/wiki/Adaptive_ML
15. https://coreweave.com/products/coreweave-forge/model-distillation ; https://github.com/OpenPipe/ART
16. https://docs.labelbox.com/docs/benchmarks ; https://community.labelbox.com/t/how-to-benchmark-vs-consensus/1203
17. https://enterprisedna.co/resources/blog/practitioner-langfuse-review/
18. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7108438
19. https://www.researchgate.net/publication/409790747_The_Right_Amount_of_Wrong_Error_Injection_for_AI_Oversight
20. https://arxiv.org/pdf/2411.00640
21. https://github.com/no-magic-ai/no-magic-papers/blob/main/papers/adding-error-bars-to-evals.md
22. https://agentengineering.org/articles/error-analysis-the-first-eval-you-should-run/ ; https://www.designgurus.io/course-play/grokking-llm-evals/doc/why-error-analysis-comes-first
23. https://parlance-labs.com/blog/posts/auto-evals/
24. https://www.braintrust.dev/articles/llm-as-a-judge-vs-human-in-the-loop-evals
25. https://github.com/ombharatiya/ai-system-design-guide/blob/main/ai_evals_complete_guide_langwatch_langfuse.md
26. https://www.morphllm.com/comparisons/braintrust-vs-langsmith
27. https://latitude.so/blog/agent-evaluation-vs-llm-evaluation-traditional-tools-fall-short-2026
28. https://arxiv.org/abs/2509.08514v1
29. https://resources.rework.com/insights/ai-workplace/human-in-the-loop-rubber-stamp
