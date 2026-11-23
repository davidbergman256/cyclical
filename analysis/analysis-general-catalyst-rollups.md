# Analysis: General Catalyst's AI-enabled roll-ups (Creation strategy: Long Lake, Titan MSP, Eudia, and peers)

General Catalyst (GC) funds AI-native holding companies that buy fragmented, labor-heavy services firms, move them onto one in-house AI platform, and keep the margin gain themselves. They aren't selling software. The biggest of them, Long Lake, had made roughly 30–40 acquisitions by autumn 2026 and in September 2026 closed a $6.3B take-private of American Express Global Business Travel. **Overlap: 5/10.** The goal matches Cyclical's (agents doing services work, with value captured from cut labor across many units of the same process), but the vehicle is the opposite, and nothing public shows they grade agents on outcomes or pool outcomes in any structured way. They answer Cyclical's hardest problem, pooling (A11), by owning the businesses, and three things come with ownership: the data rights, the system of record, and the authority to run randomized "can this role be removed?" experiments. A software vendor can never order those experiments. The main lesson: **in dental, the roll-up already exists and is called a DSO.** That makes DSOs Cyclical's best first customer and also its most likely competitor, whether one builds this in-house or a GC-style company buys into dental.

> Research limits (read before trusting details): every primary host I tried (substack.com, pitchbook.com, sec.gov, amexglobalbusinesstravel.com) was blocked from this session's network. The shared web-search budget also ran out after six queries. **I could not read either of the two essays named in the task.** For both I had search-result excerpts only. Facts below are tagged **(search excerpt)** when they came from those excerpts and **(from memory)** when they came from my training data. Claims the companies made about themselves are tagged **(vendor claim)**.

## What it actually is

**The strategy.** GC's "Creation" team, led by Marc Bhargava, sets aside about $1.5B of its fund to start or back AI-native companies that buy traditional services businesses. The Capital & Clarity headline, "The General Catalyst Behind $1.5 Billion of AI Roll-Ups", gives that figure (search excerpt; the allocation size is also from memory). GC describes it this way: *"Layering AI onto legacy systems doesn't work. It's clunky, slow, and difficult to scale. … back AI-native companies, acquire traditional businesses, embed the AI from day one, scale through their…"* ([GC on X](https://x.com/generalcatalyst/status/1981016108984627539)). The bet behind it: services firms trade at roughly 4–10× EBITDA (earnings before interest, tax, depreciation and amortization, a stand-in for operating cash profit). If AI raises their margins and the combined company gets rated as a tech platform, the owner gains twice, once from higher earnings and once from a higher multiple on them.

| Company | Vertical | What's known | Evidence quality |
|---|---|---|---|
| **Long Lake** (CEO Alexander Taubman) | Started in HOA (homeowners' association) management, then other services, then corporate travel | About $670M raised and 18 acquisitions per one newsletter; "more than 30" per CNBC (June 2026); 31 at the time of the Amex GBT deal; **40 in two and a half years** per GC (Sept 2026). All acquired firms run on one in-house platform, **Nexus**. Bought **Amex GBT for $6.3B in cash** ($9.50/share), announced 4 May 2026 and closed 29 Sept 2026. Equity came from existing investors plus Koch Equity Development; JPMorgan, BofA, Citi and MUFG committed debt; holders of 69% of shares signed support agreements. Amex sold its ~30% stake for $1.5B. Long Lake calls itself "the world's first AI holding company" and plans to own businesses long term with permanent capital. | Deal terms come from public press releases and an SEC 8-K (search excerpt). Acquisition counts conflict between sources. |
| Long Lake: **"$100M EBITDA in under two years"** | — | Traced to GC leadership. Commentators call the figure "mostly self-reported". **No audited figure or filing found.** | Vendor claim, unverified. I put ~50% on it being true as a run-rate figure including acquired EBITDA, and below 15% on it being mostly organic AI-driven margin. |
| Long Lake: HOA operating claims | HOA | "25–30% productivity gains in HOA management, 10x pipeline growth across 18+ acquired businesses" (GC). Nexus "generates full board packets and financial reports in seconds", and top managers save "65+ hours a month". The CEO says Nexus scores **5× better than general-purpose models like Claude or ChatGPT on internal evaluations** (No Priors interview). | Vendor claims |
| **Titan MSP** | IT managed services (MSPs: outsourced IT departments for small firms) | Raised about $74M led by GC in 2025. Says its AI tooling can automate about 38% of typical MSP tasks. Buys MSPs and moves them onto its tooling. | From memory (~70% confident on the numbers) |
| **Eudia** | Legal | Raised a ~$105M Series A led by GC in 2025. Bought Johnson Hana, an Irish alternative legal services provider, to become an "augmented legal services" firm. Reportedly licensed as an Arizona ABS (alternative business structure, the one US route for non-lawyers to own a law firm). | From memory (~70%) |
| Others in the GC orbit | Healthcare, UK lettings | HATCo, GC's health-system vehicle, bought Summa Health, an Ohio hospital system: the same "own the operator" logic in healthcare. Dwelly is a UK lettings-agency roll-up. | From memory (~60%) |
| Failure case | Home remodeling | A commentator notes that **Renovo Home Partners**, described as "another General Catalyst roll-up", **collapsed**, and warns that "you don't get to reference-check a category on its two best names". | Search excerpt. I could not confirm the GC link independently. |

**Who the "buyer" is.** No external buyer exists. Long Lake sells HOA management to associations, travel management to corporations, and so on. The AI is an internal cost lever and is never sold. The customer pays the same price for the service while the owner's labor cost per unit falls. Value capture is therefore close to 100% of the labor saved. A SaaS vendor gets only the share it can price for.

**Architecture.** Almost nothing is public beyond "one platform (Nexus) across all acquired firms", "internal evals", and the productivity claims. I found nothing on agent grading, case-type graduation, outcome labels, or experiments across firms. The task asks whether they build a process graph, grade agents on outcomes, or pool learning across acquired firms. On the public record the answer to all three is **unknown**, and their public metrics (hours saved, productivity %, pipeline) measure input and throughput, not outcomes.

## Loop comparison

| Aspect | Roll-up approach | vs Cyclical |
|---|---|---|
| A1 Core frame (graph; person/agent interchangeable) | No graph formalism is public. They think in roles and labor hours ("zero additional headcount" as they add revenue). | Different (implicit) |
| A2 Observation / onboarding | No process mining. **Post-merger integration**: the acquired firm migrates onto Nexus and the holdco playbook. Processes are imposed, not discovered. | Different. Better for data uniformity, worse for keeping local know-how. |
| A3 UX | Workers use the owner's tool because ownership lets the owner require it (board packets generated in Nexus). | Different. Ownership removes the adoption problem Cyclical's no-new-UI design exists to solve. |
| A4 Permissions | One owner holds all the data and all the systems. Access is internal IT policy. | Different. The **unresolved system-node question disappears**: the owner *is* the system node. Agent-level rules for prompt-injection defense aren't public. |
| A5 Shadow eval vs outcomes | Not public. Public metrics are hours saved and productivity. | Absent / unknown |
| A6 Checkoff with seeded errors | Not public | Absent / unknown |
| A7 Statistical graduation per case type | Not public. "5× better than Claude on internal evals" implies an eval suite but says nothing on thresholds. | Absent / unknown |
| A8 Replacement levels | "Automate 38% of tasks" (Titan, from memory) means task-level automation. Nothing about compiling agent behavior to code. | Unknown |
| A9 Orchestrator | Holdco operators do the reorganizing (merge offices, centralize back office, cut roles), with full authority to act. | Different. Humans with owner authority rather than an agent proposing to a manager. **More power to act**, no automated proposals. |
| A10 Shared context | One platform across all firms means shared context by construction | Same / better |
| A11 Cross-business pooling | Pooling *within the owner's portfolio* is structurally easy (one data model, full rights, can randomize staffing). No evidence they run outcome experiments. N equals the number of firms owned (~40), though process runs (tickets, associations, trips) number far more. | **Better positioned, execution unknown.** Siloed: no pooling across owners. |
| A12 Anti-Goodhart guardrails | The owner sees the consolidated P&L and churn. EBITDA and customer retention are the business-level guardrail by default. | Better (comes free with ownership) |
| A13 Model-agnosticism | Built a proprietary platform claimed to beat frontier models. Whether it is model-swappable isn't public. | Unknown; leans toward "own the stack" |
| A14 Business model & moat | Asset = owned cash-flowing businesses, customer relationships, and the multiple gap. Funded by venture equity plus bank debt. | Different. The moat is ownership and capital, not outcome history as such. |

**A11, pooling, is the aspect that matters most.** Realizations §5 lists five things pooling buys. A roll-up can get each one more cheaply than Cyclical can.

- **Outcome A/B tests** (one change tested against another on real outcomes) need only a shared data model and volume. A holdco gets the shared data model by migrating every firm onto Nexus. Cyclical has to get it by integrating with and normalizing many independent systems.
- **Rare segments and rare-error safety bars** depend on volume within the segment. A roll-up's volume is capped by how many firms it owns. Cyclical's isn't capped that way.
- **Fast re-certification after a model swap** is the same for both.
- **Randomized role-removal experiments** take hundreds of units split at random, and someone has to be *allowed to remove the role* in the treatment group. That is a staffing decision. A SaaS vendor can only suggest it to hundreds of independent owners, and owners who opt in aren't a random sample. A holdco can order it. **This is the one item on Cyclical's list that ownership makes trivial and software makes nearly impossible.**
- **The pooled exception desk** of leftover humans shared across clinics is a roll-up's shared-services center by another name. DSOs already run one for billing.

So the brief's worry is correct: for whoever owns hundreds of firms in one vertical, A11 is mostly an internal analytics project. What saves Cyclical is that no roll-up owns *every* firm, and each roll-up's data stays inside that roll-up.

## Where they're ahead of Cyclical

1. **Value capture.** Realizations §5 estimates a clinic saves ~$180k a year in salaries against ~$5–10k of agent bill. A SaaS vendor might price 20–30% of the saving, about $36–54k per clinic per year (rough). An owner keeps all $180k. At a 6× EBITDA multiple that adds about $1.1M of enterprise value per clinic, or about $320M across 300 clinics (rough). Capital chases that arithmetic, which explains why GC, Thrive and others fund roll-ups rather than vertical SaaS for small businesses.
2. **Adoption, permissions, and the system of record are settled by ownership.** Cyclical spends A2, A3 and A4 on getting into a business that doesn't belong to it. Long Lake's integration playbook simply moves every acquired firm onto Nexus. The strategic risk Cyclical names (the system-of-record owner builds it) is removed because the roll-up *becomes* the system of record.
3. **A business-level guardrail comes for free (A12).** The consolidated P&L shows at once whether the claims agent's acceptance-rate gains are costing collections.
4. **Buying history instead of waiting for it.** Realizations §1 says buying beats rebuilding when an asset has to build up over time, and Cyclical names outcome history as exactly that kind of asset. Each acquisition brings years of past event logs: claims, payments, show-ups, churn. Over 40 acquisitions a roll-up gets decades of history at once. Cyclical's version has to accumulate after each clinic signs up, unless the history can be backfilled from the practice software's logs. **Cyclical should backfill.**
5. **Access to capital at scale.** Long Lake financed a $6.3B take-private with bank debt from four large lenders. A data-flywheel thesis has never raised that kind of money. A thesis about buying cash flows can.

## Where they're doing it differently (and whether their way is better)

- **Impose vs observe (A2).** Roll-ups standardize first and measure afterward. Cyclical observes the existing process and lets the graph show where it differs from the intended one. For pooled learning, imposing is *better*: pooling needs comparable units, and a holdco makes them comparable by decree, while Cyclical must normalize forty versions of "recall". The cost is that imposing destroys the local variation that A/B tests need. A holdco running one playbook everywhere has no natural experiments left unless it creates them deliberately. Nothing public says Long Lake does.
- **Labor-hours metrics vs outcome grading (A5–A7).** Long Lake reports hours saved and productivity. Those measure inputs, and they Goodhart the way Cyclical's design warns: a board packet generated in seconds that a board finds wrong still counts as hours saved. Cyclical's insistence on outcome labels (paid, showed, renewed) is the more rigorous approach. On the public record, the roll-ups haven't gone there. If they had, it would be their best marketing material.
- **Proprietary platform vs model-agnostic layer (A13).** "Nexus beats Claude 5×" is the claim of a firm that treats its in-house stack as core IP. By realizations §2, that's the side whose value shrinks with each model release: the hand-built structure a better model replaces. The roll-up's real moat is ownership, so it can afford a disposable stack. Cyclical can't, because Cyclical's moat has to be the outcome history.
- **Drifting toward big targets.** Long Lake started in HOA small-business firms and then bought a $6.3B public company with tens of thousands of employees (from memory). The economics push roll-ups toward bigger targets, where one deal moves EBITDA more than forty small ones. That is the opposite of the "hundreds of small businesses running the same process" structure Cyclical's pooling needs. A roll-up maximizing EBITDA per deal dollar eventually stops being a pooled small-business learner.

## Feedback & reviews on these parts of the loop

**The data flywheel (A11/A14): the central critique.** The brief describes Evan Lyseng's "AI rollups revisited" (published under the title "The Largest Arbitrage in Technology") as arguing that the data-flywheel pitch is a fallacy. **I couldn't read the full text and can't confirm that wording.** From search excerpts (independent analyst; he was earlier a roll-up proponent):

- He describes the pitch: data each firm collects "feeds agents that automate later work, so margins rise with each client".
- He proposes a test: **"strip away the AI-effect, and ask whether or not top tier consolidation platforms can generate venture-scale returns."**
- He doubts the technology lift in many verticals: "there are many more [categories] where I'm not convinced technology adds enough value."
- He says roll-ups "require a centralized, opinionated playbook", and he has suggested a PropCo/OpCo split elsewhere, meaning one entity owns the assets and a separate entity runs the operations.
- His overall framing is that AI capability far outruns distribution, so owning distribution is the trade.

Yoni Rechtman called it "very thoughtful and rigorous" ([99d](https://99d.substack.com/p/insecurity-is-the-enemy-of-improvement)).

My reconstruction of why the flywheel argument is weak *as roll-ups use it*, labeled as my reasoning: (a) most "data" in an acquired HOA or MSP firm is documents and tickets that a frontier model already handles without proprietary training, so extra volume brings diminishing returns; (b) the scarce input is **outcome labels joined to decisions**, which roll-ups don't appear to collect any more systematically than anyone else; (c) one roll-up's 40 firms is a small N for rare segments. This *agrees* with Cyclical's thesis: data volume isn't the moat, outcome-graded history is. It also means the critique of roll-ups hits the flywheel pitch, not the ownership-plus-labor-arbitrage economics.

**Economics and margin claims (A14).** These sources are independent commentary:

- Long Lake's $100M EBITDA is called "notable, though mostly self-reported" and "genuinely unusual" in pace (search excerpts).
- The Renovo collapse is cited as evidence of survivorship bias in the category.
- CNBC framed the June 2026 wave as "Silicon Valley's new buyout playbook hitting Wall Street", which places it as a private-equity variant.
- Skift describes Long Lake as a private equity firm; Long Lake calls itself an AI holding company.

That label dispute is the Lyseng test in miniature.

**Operational AI claims (A5–A8).** All vendor-sourced:

- 25–30% HOA productivity (GC)
- 65+ hours a month saved per top manager
- 5× better than general models on internal evals (CEO)
- about 38% of MSP tasks automatable (Titan, from memory)

I found no customer reviews (G2, Reddit, HOA boards) about service quality after acquisition. **(The search budget ran out before I could look on Reddit, e.g. r/HOA or r/msp.)** That matters because the guardrail for a roll-up's agents is customer churn, and nobody independent has reported on it.

## Top-level: why they chose this path, and what to learn

**Their starting asset and constraint.** GC's starting asset is capital: an ~$8B fund (from memory), banking relationships, and a brand that recruits AI engineers. Its constraint is that vertical SaaS for small businesses has poor value capture and slow adoption, since small firms are hard to sell to and won't change workflows. Buying the firm removes the adoption problem and captures all the savings. The cost is capital intensity, integration risk, and leverage. The path fits a firm with $1.5B to deploy. It does not fit a seed-stage founder.

**Key question 1: is a roll-up a better vehicle for Cyclical's thesis than SaaS?**

Ownership is better for **depth** of pooling: data rights, one data model, randomized role-removal, the system of record, a free EBITDA guardrail, purchased history. SaaS is better for **breadth**: N across owners, rare segments, and capital efficiency. Roughly 300 dental practices at ~$1–2M each would cost ~$0.3–0.6B before integration (rough). Corporate-practice-of-dentistry laws in many states also force a non-dentist owner into an MSO structure (management services organization: the non-clinical company that runs a practice owned by dentists), as DSOs already use.

The thesis's two scarce inputs split cleanly between the two vehicles. The *authority to experiment* belongs to owners. The *pool across many owners* belongs to whoever sits under all of them. **Neither pure vehicle gets both.** The best structure is probably a SaaS layer that pools across many DSOs and independent practices, combined with a few DSO design partners who grant experiment authority over their own offices.

**Key question 2: would a roll-up be Cyclical's best customer?**

**In dental, yes. Generic AI roll-ups like Long Lake, no.**

- **GC-style holdcos won't buy.** GC's thesis says the AI must be built in-house ("embed the AI from day one"), and Long Lake treats Nexus as its core IP. They are competitors for the idea, not buyers.
- **DSOs are the right buyer.** In 2023 about 14% of US dentists were DSO-affiliated, and more than 1 in 4 of those within 10 years of graduating (ADA HPI, per realizations.md). The largest DSOs, such as Heartland (~1,700 offices), Aspen (~1,100) and Pacific Dental (~1,000), are each the size of the pool Cyclical needs inside one owner (from memory). Mid-size DSOs with 20–150 offices have the same incentives and ownership rights but lack an in-house AI team. They are the sweet spot.
- **The pitch to a DSO** follows from the roll-up logic: "Your offices already share billing. We give you outcome-graded agents, case-type graduation, and randomized role-removal trials across your offices. Our cross-DSO pool gives you rare-segment and safety-bar volume you can't reach alone."
- **The risk** is that a top-5 DSO builds its own Nexus. The defense is the cross-owner pool, which no single DSO can replicate.

**Copy:**

- Backfill outcome history from practice-software logs at onboarding, the way a roll-up inherits it on acquisition.
- Use the consolidated P&L (collections, retention) as the default A12 guardrail.
- Sell to owners of many sites first (DSOs), because they can authorize randomized experiments.

**Avoid:**

- Becoming a capital-heavy acquirer before the eval loop is proven.
- Reporting hours saved instead of outcomes. Hours saved is the roll-ups' weakest public evidence and Cyclical's chance to stand out.

**Exploit:**

- Roll-up data is siloed per owner, so only an independent layer can pool across DSOs and independents.
- Roll-ups that impose one playbook destroy their own natural experiments. Cyclical's graph-plus-randomization design can sell experiment design back to them.

**Threat level: medium now, high if one specific thing happens.** GC-style capital enters dental as an AI-native acquirer, or a top-5 DSO announces an in-house agent platform rolled out with outcome grading across its offices. In either case the largest single pool of comparable dental units forms behind one owner's wall. **The observation that would tell David the threat is rising** is any of these:

1. A GC, Thrive, or Bessemer-backed company announces dental-practice or DSO acquisitions.
2. A large DSO's earnings or press materials report AI-driven front-office headcount cuts measured by collections or show-rate outcomes rather than hours.
3. A practice-software vendor partners exclusively with a roll-up.

Probability that an AI-native roll-up (not a legacy DSO) has announced a dental platform by end of 2027: about 40% (rough).

**Other incumbents found, possibly not on the orchestrator's list:**

- **Thrive Holdings** (Thrive Capital): owns Crete Professionals Alliance (accounting) and Shield Technology Partners (IT MSPs). OpenAI reportedly took a stake (from memory).
- **Metropolis**: AI parking operator that bought SP+ for ~$1.5B (from memory).
- **Large DSOs** (Heartland, Aspen, Pacific Dental) as in-house builders.
- PYMNTS reported AI investors buying "ADT, accountants and call centers" (headline only).

## Sources

1. General Catalyst on X, AI-enabled roll-up post — https://x.com/generalcatalyst/status/1981016108984627539
2. Capital & Clarity, "The General Catalyst Behind $1.5 Billion of AI Roll-Ups" (search excerpt only) — https://capitalandclarity.substack.com/p/the-general-catalyst-behind-15-billion
3. Evan Lyseng, "The Largest Arbitrage in Technology" / AI rollups revisited (search excerpt only) — https://evanlyseng.substack.com/p/ai-rollups-revisited
4. Yoni Rechtman, 99d (reaction to Lyseng) — https://99d.substack.com/p/insecurity-is-the-enemy-of-improvement
5. PitchBook, "General Catalyst's $6.3B AMEX deal puts its AI roll-up strategy on display" (search excerpt) — https://pitchbook.com/news/articles/general-catalysts-6-3b-amex-deal-puts-its-ai-roll-up-strategy-on-display
6. Amex GBT press release, deal announcement — https://www.amexglobalbusinesstravel.com/press-releases/long-lake-agrees-to-acquire-amex-gbt-with-support-from-general-catalyst-and-alpha-wave/
7. Amex GBT press release, completion — https://www.amexglobalbusinesstravel.com/press-releases/long-lake-worlds-first-ai-holding-company-completes-acquisition-amex-gbt/
8. Skift, Amex GBT acquired by GC-backed Long Lake — https://skift.com/2026/05/04/amex-gbt-acquired-general-catalyst-long-lake-6-3-billion/
9. SEC 8-K exhibit, Global Business Travel Group — https://www.sec.gov/Archives/edgar/data/0001820872/000114036126018699/ef20072315_ex99-1.htm
10. CNBC, "Silicon Valley's new buyout playbook is hitting Wall Street" (June 2026) — https://www.cnbc.com/2026/06/08/silicon-valleys-new-buyout-playbook-is-hitting-wall-street.html
11. No Priors interview with Long Lake CEO Alexander Taubman (summary) — https://murmurcast.com/summaries/no-priors-artificial-intelligence-technology-startups/amex-global-business-travel-the-worlds-first-ai-take-private-with-long-lake-ceo-alexander-taubman
12. Manthan, "31 Acquisitions in 17 Months. $6.3B Take-Private. Zero Additional Headcount." — https://getmanthan.com/insights/longlake-ai-rollup-services/
13. Buy Build Exit, Long Lake / Amex GBT — https://buybuildexitwithroyredd.substack.com/p/ai-rollup-long-lake-amex-gbt
14. Capital Founders, AI roll-up investors playbook — https://www.capitalfounders.io/playbooks/ai-enabled-roll-ups/chapters/capital-and-players/
15. Luke Sophinos, Linear #186 "AI Roll Ups: Two Years Later" — https://www.newsletter.lukesophinos.com/p/linear-186-ai-roll-ups-two-years
16. PYMNTS, "Why AI Investors Are Buying ADT, Accountants and Call Centers" (headline only) — https://www.pymnts.com/news/artificial-intelligence/2026/why-ai-investors-are-buying-adt-accountants-and-call-centers/
