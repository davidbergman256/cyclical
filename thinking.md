# Thinking: how cyclical works, and what we still have to figure out

Written Nov 23, 2026, the day of the first build. Companion to `realizations.md`. Figures marked *rough* are estimates.

**Thesis.** Cyclical runs a small business as a graph where people and agents are interchangeable steps, graded on what actually happens (show-ups, payments) and improved using outcomes pooled from every business running the same process, so the system does the orchestrating and the asset is an outcome history no model release can produce.

**The differentiating idea.** Employees shouldn't become orchestrators of agents. Most people won't be good at it, and the system can do it. They should become a node in the workflow, on the same level as an agent: they do the task they're already good at and get graded on the same answer key. Most of the market assumes the opposite: Microsoft's 2025 Work Trend Index told everyone to become an "agent boss" (*from memory*). Our bet is that orchestration is the first thing to be automated, not the last.

---

## Part 1: the process

These pieces run at the same time, all the time, so the order below isn't a sequence.

### The owner describes the business, and the system compiles a graph
The owner (a clinic owner, an office manager, a roaster) explains in plain words how work gets done. The system turns that into a graph and shows it back as a diagram with one plain-English sentence per step. The owner corrects it by talking, never by editing a spec. The first draft will be wrong in places; flags and experiments fix it over time.

### The graph is data, not code
The engine is general and contains no business-specific code. Each business's graph is a data object, and that object is fully tailored to the business, the way a spreadsheet program is general but each spreadsheet is specific. Every graph is versioned, and every run records which version produced it, because that history is the asset.

### Every node has a contract that doesn't care who fills it
A node declares:
- its inputs
- its required outputs
- its deadline
- its **answer key**: the signal from the world that says whether it went right
- its run volume per year, outcome lag, and the smallest effect worth detecting

The **executor** is either an agent or a named person. Both are graded the same way. This makes swapping a person for an agent an experiment instead of a reorganization.

### Nodes come in shared types and custom ones
**Shared node types** ("send appointment reminder", "chase unpaid invoice", "request insurer approval") pool their outcomes across every business that uses them. Business-specific settings sit on top. Steps that fit no type stay custom and learn only from their own business.

### The engine runs the graph on events
Events come from the world: a booking, a reply, a payment, a missed visit. The engine routes each case through the graph to agents and people. The clock is injectable, so the simulator and live operation run the same code. Otherwise the tests test the simulator, not the product.

### Employees see a task inbox, never the graph
One card per task. Do it, mark it done, or press **doesn't fit** and write one line ("this insurer needed approval before booking the crown and nobody asked for it"). Each card shows the case history, because one person in a small business fills many nodes and carries context between them.

### Grading against the world, at three layers
1. **Task check**: is the output well-formed and sensible?
2. **World answer key**: show-ups, insurer payment statements (EOBs), bank deposits, signed contracts.
3. **Business guardrail**: did the business-level number get worse?

A person approving an agent's output doesn't prove the output was right, and staff approving drafts are labeling their own replacement. So grading uses the world, not approvals.

### Doesn't-fit flags become graph changes
The system groups flags that describe the same gap and proposes a step to fill it. Here, it would propose "request insurer approval before scheduling crowns for insurer X". The owner approves, and the gap's symptom (denials) falls. The world's answer key says *something* is wrong ("claim rejected, code 197"). The flag says *what*. This makes employees sensors without making them orchestrators.

### Experiments
The optimizer reads the logs and proposes variants. Message and settings changes are randomized per case. Structural changes (remove a person from a node, merge two nodes) are randomized per business, because one business can't be its own control. The sample size is fixed before an experiment starts, and stop rules prevent peeking until something looks significant.

### Executor swaps
At a given node, run the person and the agent on comparable cases, grade both on the same answer key, and move the node to whichever wins on the business objective. Each executor's speed, cost and error rate is modeled, so the comparison isn't rigged in either direction.

### Model swaps
When a node's model changes, its eval suite re-runs before the new model can take traffic. Pooling makes this fast. Re-certifying with one business's volume alone would take months.

### Owner approvals
Prompt changes, model changes and settings within bounds go live automatically once they pass their tests. Structural changes always go to the owner as a plain-language card ("Clinics like yours that stopped confirmation calls for patients under 65 saw no change in show-ups. Stop them here?").

### Pooling by process type
The unit of pooling is the process, not the industry. A reminder-timing result transfers across dentists, physios, vets and salons, because the mechanism is the same: a person forgets an appointment. It doesn't transfer to a roaster's wholesale onboarding. Each business's estimate is pulled toward the pool's estimate in proportion to how little data it has of its own. Statisticians call this partial pooling, or a hierarchical model.

### A shared exception desk
Cases nobody at the business can resolve go to a central queue shared across businesses: about 0.1 of a full-time person per clinic (*rough*, from `realizations.md`).

### The simulator as test world
We don't have a real business, so the simulator is the business. It contains:
- simulated customers with hidden traits
- counterparties with hidden rules, such as insurers
- simulated employees with planted skills, speeds, error rates and wages
- a mock system of record

It also contains **planted truths**, effects we put in on purpose so the tests can check whether the product finds them.

---

## Part 2: the challenges

### 1. Feedback is scarce, and how scarce varies hugely by business
For a yes/no outcome, the runs needed per variant are about `16 × p(1−p) / Δ²`, where p is the base rate and Δ the change you want to detect. That gives 80% power at 5% false alarms. Halving the effect quadruples the runs. Time to a decision is runs needed divided by runs per year, plus the outcome lag. *Rough* examples:

| Case | Runs needed | Volume | Time at one business |
|---|---|---|---|
| Dental no-shows, 10% → 9% | ~29,000 | ~8,000 appointments/yr | ~3.6 years |
| Roaster café signups, 20% → 25% | ~2,000 | ~30 pitches/yr | ~70 years |
| Architecture margin, +3 pts (σ ≈ 15) | ~800 | ~15 projects/yr | ~53 years, plus a 2-year lag per outcome |

Pooling multiplies volume and does nothing for lag. Where pooling isn't enough, grade each run on an earlier signal (plan-check comments, RFIs), and check that signal against the real outcome so it can't be gamed. **Open question:** can the system triage each node automatically into "learns from own data / needs the pool / needs an earlier signal" from its volume, lag and effect size?

### 2. Tailoring vs pooling
The more each business's graph diverges, the less one business's result tells you about another's. Shared node types plus partial pooling is the proposed fix. **Open question:** how fine-grained should node types be? Too coarse, and the pool mixes different mechanisms. Too fine, and every pool is tiny.

### 3. Whether the first graph is good enough
If the graph compiled from an owner's description is so wrong that flags can't fix it within a few weeks, onboarding needs a human doing setup on site, and the self-improving loop takes over afterward. Then the honest model is Palantir-style forward-deployed setup plus the loop. Tests 1 and 6 below measure this.

### 4. We don't know how small businesses optimize today
Best guess (*from memory*, unverified): mostly not systematically. Changes happen after something breaks or a customer complains, the owner glances at a few numbers in their software monthly, and almost nothing is measured before and after. The simulator's baseline should be exactly that owner, and the product's value is the gap. **Needs:** conversations with ~5 owners to confirm or replace this.

### 5. The simulator is the answer key
Tests on a simulator prove the machinery works: it finds planted effects at roughly the predicted sample size, it rejects Goodhart traps, and it detects removable roles only with randomized pooled businesses. They don't prove the product creates value at a real business. There's also a risk that the optimizer learns quirks of the simulator rather than anything about real businesses. Only real deployments close this.

### 6. Scale vs fidelity
Pooling across thousands of businesses means hundreds of millions of node runs, which is impossible with real model calls. One A/B test at ~3,800 runs per arm is affordable: ~20k calls, ~$50–150 on a small model (*rough*). So there are two modes on one engine:
- **statistical mode**: nodes are cheap parametric policies, for the pooling and structural experiments
- **real mode**: nodes are real agents, run on tens to hundreds of cases, to show the agents actually work

### 7. Humans as nodes, without breaking the humans
- **Sensors.** People notice the missing steps the graph doesn't contain. Pure nodes with no flag button go blind.
- **Context.** One person fills many nodes and remembers the anxious patient from Tuesday. Task cards have to carry the case history.
- **Not literally equal.** People take hours, agents take seconds. People cost more and are sometimes much better. The model has to reflect all of that.
- **Morale.** Being a node is how Amazon pickers and Uber drivers experience their work, and that kind of algorithmic management is known for turnover. And whoever's node is being tested against an agent knows it.

### 8. Goodhart
Every local metric needs a business-level guardrail. For example, a claims agent that maximizes acceptance by downcoding (billing a cheaper procedure code so the claim passes) lowers collections. Earlier signals used to beat lag are especially gameable: drawings tuned to minimize RFIs can make the building worse to construct.

### 9. The system of record
The vendors whose software already holds a business's records (in dental, the practice-management software) are best placed to build this. We either integrate deeply or become the system of record. Today everything is mocked.

### 10. Why the labs don't just do this
OpenAI Frontier already ships agents with evals and self-improvement, and it's better built than anything we'll ship today. Speed is how you build a moat, not the moat itself. The only defensible asset is pooled outcome history plus a graph that treats people and agents the same, so either can be graded at any step. If a lab builds the same pools first, this fails.

### 11. Trust takes calendar time
Owners need months to trust each automated step, insurers take weeks to pay or deny, and some steps wait on a capable enough model. Pooling doesn't speed up any of these.

---

## Part 3: what today's build has to prove

Acceptance tests. Each runs in the simulator with fixed random seeds.

1. **Plain-language round trip.** A non-technical description compiles to a graph whose plain-English rendering matches the description.
2. **Generality.** The same engine, with no engine changes, runs three businesses: dental clinic, coffee roaster and architecture studio. Adding a business means writing a simulator plus a description.
3. **Planted effect recovery.** A planted reminder-timing effect is proposed and confirmed using at most ~2× the runs the power calculation predicts.
4. **Null control.** With no effect planted, a change is wrongly promoted ≤5% of the time across seeds.
5. **Goodhart trap.** A downcoding variant wins on its task metric and is blocked by the collections guardrail.
6. **Missing step.** A planted gap (the insurer requires approval, and the graph has no approval step) produces flags, which produce a correctly placed new step, after which denials fall.
7. **Executor swap.** A node moves to an agent where the agent is planted to be better, and stays with the person where the person is better, even when the agent is cheaper.
8. **Pooled vs alone.** The same experiment decides in days of simulated time across 500 businesses and takes years at one.
9. **Transfer.** A reminder finding transfers between two appointment-based businesses and is refused where the mechanism differs.
10. **Model swap.** Changing a node's model re-runs its evals before it takes traffic.
11. **Exception path.** A case nobody can handle reaches the shared desk and completes.
12. **Operator walkthrough.** A browser script runs onboarding → approve a change → handle a task. The test fails if the UI shows JSON or words like "node", "prompt" or "eval" to the owner or employees.
13. **Determinism.** The same seed gives identical results.

## Open decisions for today (defaults in brackets)

- Who the primary user is [the owner or office manager of one business; pooling runs underneath]
- Objective [monthly net revenue − staff cost − agent cost, with guardrails on customer complaints, error rates and safety]
- Approval rules [settings and models automatic once tested; structure needs owner approval]
- Spend cap for model calls today [?]
- Model API key [none in the build environment yet; real mode stays stubbed until one is added]
- Hosting [local plus pushing to the branch; deploy at the end if there's time]
- Stack [one TypeScript repo, Next.js, SQLite append-only event log]
