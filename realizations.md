# Realizations: neolabs, wrappers, and turning businesses into agent harnesses

Distilled from one long conversation (Nov 2026). Figures marked *rough* are estimates or invented; figures with a source were checked at the time.

## 1. The right test is not "does it survive AGI?"

"Does it survive unlimited intelligence?" rules out almost every business, so it can't tell one from another. The useful test is the **sign of the next model release**: does the company gain or lose value the day a better model ships?

The bitter lesson is about *substitutes*: compute plus data beats hand-built structure (features, heuristics, workflow code). It says nothing about *complements*, the inputs intelligence can't create:

- measurements nobody has taken yet (wet-lab data, clinical outcomes)
- physical throughput
- licenses, patents, regulatory approvals
- a party that can be sued
- a channel to the customer

When one input gets cheap, the profit moves to whatever scarce input it depends on.

Corollary: **intelligence shortens the time it takes to work something out, not the time it takes to build something up.** Buying a company beats rebuilding it exactly when its assets have to be built up over time.

## 2. Three kinds of AI company, three different bets

- **Frontier on one subtask (e.g. Leash Bio).** It runs on the bitter lesson, not against it. Biology has no cheap simulator to generate training data, so the wet lab *is* the simulator and its throughput is the bottleneck. If Anthropic spent $20B to replicate Leash, it would be buying lab robots, not GPUs. Buying Leash is cheaper, and that's the exit. Caveat: a data moat lasts only where the data can't be derived from existing data plus physics. AlphaFold made the next experimentally solved protein structure worth much less for many uses.
- **Pure-research neolabs (SSI, Thinking Machines, Reflection).** The critique lands hardest here. The bull case is a cheap option on finding the next general method; the floor is that a big lab may license or hire the team. But using a discovery takes compute, and the incumbents have roughly 10× more.
- **Workflow wrappers on a model (e.g. Legora).** The workflow code is disposable. What investors buy is a channel into a conservative buyer, plus being model-neutral while no lab holds the lead for long (open-weight models trail the frontier by about 4 months). The model-neutral layer gets whichever model leads that month, and each release cuts its costs while its price stays tied to lawyer time. The wrapper thesis fails if one lab's lead becomes durable, because then the wrapper is reselling a monopolist that can bundle the product for free. Evidence: Anthropic's legal plugin knocked 13–16% off Thomson Reuters, RELX and Wolters Kluwer in one day (Feb 2026), yet Legora later raised at $8.8B. The market punished incumbents whose margin came from hand-built structure and rewarded the model-neutral channel.

VC math rarely depends on what happens after AGI: a fund needs a few 50× exits within ~10 years. In fast-takeoff worlds everything gets repriced at once, so those worlds don't distinguish one bet from another.

## 3. Biosecurity screening idea

Demand passes the test: more AI-designed DNA means more designs that slip past similarity-based screens. Supply fails as first framed, because a hazard classifier is an intelligence product that the DNA-design labs will build into their own stack. It becomes a complement only if it rests on something they can't produce themselves:

- wet-lab-validated hazard data, which is legally restricted to generate, or
- independence: a producer can't credibly certify its own outputs.

Independence earns money only once a mandate or liability rule forces someone to pay for it. **The question that decides this company is regulatory.**

## 4. The workflow-harness idea, and where it went

**First version ("make every business's workflow model-agnostic").** Fails, because its value is the gap the next model closes. OpenAI Frontier (Feb 2026) already ships an agent platform with evals and self-improvement that manages other vendors' agents. Being model-agnostic protects you from a supplier raising prices, not from a competitor shipping your product.

**Second version ("re-architect the workflow itself into an evaluated harness that improves toward the business's goal").** Better, because the asset moves from the agent, which every model rebuilds, to the history of how the process performed, which only builds up over time. Old idea, new engine: 1990s business-process reengineering, Palantir, Celonis.

**The crux is feedback.** Task-level evals are cheap and already commoditized. Process-level changes are judged by business outcomes, which are scarce. Detecting a 20% lift on a 10% conversion rate takes about 3,800 runs per variant; a small business runs most workflows a few hundred times a year. More intelligence doesn't fix this, because outcome data has to be generated. **The fix is pooling across many businesses running the same process**, which means picking one vertical rather than "every business".

## 5. What the dental clinic models showed

Built: three flow maps (dental clinic, coffee roaster, architecture studio), a live dental flow simulator, and a 48-month agent rollout comparing data pooled across 10,000 clinics with one clinic alone.

- **How much a business can learn from its own outcomes varies hugely by business.** A dental clinic has volume; a coffee roaster can test email in weeks but would need about 110 years to optimize café signups; an architecture studio would need 70–100 years for outcome tests and must instead learn from records that grade each run (plan-check comments, RFIs, change orders).
- **In the 9-person clinic, 12 of the 14 handoffs typed by hand end in the practice software.** About a fifth of all handoffs are a person re-typing something.
- **The DSO already proves the economics.** Dental service organizations pool billing, insurance checks, phones and recall for hundreds of offices. That's the human version of the idea. About 14% of US dentists were affiliated with one in 2023, and more than 1 in 4 dentists within 10 years of graduating (ADA HPI).
- **The assistant isn't the job that goes.** Dental assistants are chairside: paperwork is roughly a sixth of their day, and every chair still needs a person. The jobs that shrink are the front-office ones: front desk, treatment coordinator, billing, office manager. 9 people → ~6; staff cost ~$558k → ~$375k a year (*rough*).
- **Model swaps save the platform money, not the clinic.** The clinic's whole agent bill is ~$5–10k a year against ~$180k of salaries replaced (*rough*). Across 10,000 clinics that's ~$99M → ~$51M a year of compute, which is your gross margin. After the swaps, ~73% of the remaining bill is phone minutes and hold time, which no model change touches.
- **What pooling buys, specifically:**
  - outcome tests (confirmation texts: ~3.3 years at one clinic vs. hours pooled)
  - rare segments (claims must pass for each insurer × procedure group: ~4.5 years alone)
  - rare-error safety bars (30,000 clean clinical notes: ~5+ years alone)
  - fast re-certification when a new model ships
  - **testing whether a role can be removed at all**: this needs hundreds of clinics split at random into two groups, which one clinic can never do
- **What pooling can't buy:** waiting for insurers to pay or deny (weeks), waiting for a model capable enough (some skills had to wait for one), and the months practices need to trust each step.
- **Pool the leftover humans too.** Exceptions go to a central desk shared across clinics: ~0.1 of a full-time person per clinic (~1,300 people across 10,000 clinics) instead of ~20,000 billing people and office managers.
- **Grade agents against the world, not against the human approving them.** Approval isn't proof of correctness, and staff approving drafts are labeling their own replacement. Use answer keys the world provides: insurer payment statements, bank deposits, show-ups.
- **Local evals Goodhart.** Every task-level eval needs a business-level guardrail, e.g. a claims agent that maximizes acceptance by downcoding hurts collections.

## 6. Where the moat actually is

The market for agents that do one task is already crowded (YC alone has Toothy AI for insurance and claims, Newton for calls and verification, PatientDesk for the front desk). None of them can test structural changes, such as removing a role or merging nodes, across hundreds of businesses from inside one task. **That needs both the whole graph and the scale.** Strategic risk: whoever owns the system of record (in dental, the practice-software vendors) is best placed to build it, so you either integrate deeply or become that system.

## 7. Personal

An MIT degree increasingly certifies fast learning of hard things more than it gives skills you can stay ahead of the exponential with. The redirect is to work where intelligence is the complement, not the substitute.
