>Cyclical runs a small business as a graph where people and agents are interchangeable steps, graded on what actually happens (show-ups, payments) and improved using outcomes pooled from every business running the same process, so the system does the orchestrating and the asset is an outcome history no model release can produce.


what we have to figure out:

UX
- orchestrator view
- node view (edges accessible to node and their context, missing edge flag that increases graph accuracy to reality)

human + agent UX should be extremely minimal. employees know it's happening, but they don't get new tools with 5 buttons and 5 shortcuts. they keep doing the work they're best at; we learn which work an agent does better and make them more productive at what they're uniquely good at.
- observe through the tools they already use (email, calendar, practice/admin software, accounting): read their event logs. that's process mining (celonis's method), not a new box.
- stage 2 is silent too: the agent's draft lands where the person already works (e.g. their email drafts folder). sending it = approval, editing it = correction.

typical agent best practices (limited context, permission limits)

permissions (just-in-time access):
- every node has the default permissions it needs for its edges.
- if it needs more, it asks the node that has the information. that node decides whether to share and whether to extend the permission. the grant is temporary, and every request is logged.
- agent-to-agent approvals follow rules, not persuasion: decided only by who is asking, what class of data, and what kind of task, never by the wording of the request. otherwise a malicious email in some agent's context can talk its way into data (prompt injection).
- the frequency signal runs both ways. node A keeps asking node B for the same thing → the orchestrator proposes a permanent grant to the owner, or better, a missing edge (that info should just flow to A). permissions unused for months → proposed for removal. so permission requests are the automatic version of the missing-edge flag: one mechanism, not two.

UNRESOLVED: where data lives. most data sits in systems (practice software, admin apps), not with people, and a system is itself a node. who answers a permission request sent to a system node? giving every system a "responsible" node is a special case, and it's inelegant. needs an elegant solution.

model-agnostic evals for every edge - so the graph can improve
1. mirrors human task, tries to minimize difference between human output and its own
2. does the human tasks, but they require human checkoff before being passed
3. once it reaches some threshold, human feedback is no longer needed and the node can be replaced. 

stage 1: don't grade against the human. if the agent minimizes its difference from the human, its ceiling is the human, mistakes included. score both human and agent against what actually happened (invoice paid, patient showed up) wherever that exists; use agreement with the human only where nothing in the world grades the output. disagreements between human and agent are the most valuable data: resolve a sample of them by outcome.

stage 2: checkoffs decay into rubber stamps. approval rates drift toward 100% as people stop really looking, and the checker is labeling their own replacement. seed known-bad outputs into the queue at ~1 in 50; a checker who misses them isn't checking, and their approvals stop counting as evidence.

stage 3: needs a number. zero errors in n runs → 95% confident the error rate is below ~3/n (300 clean runs to claim <1%, 3,000 for <0.1%). a node that runs 50×/year never gets there on its own data → pooling. TODO: figure out pooling.

graduate per case type, not per node. one node handles several kinds of cases, and the agent is ready for some long before others. bookkeeping: 95% recurring vendor invoices, 5% refunds/disputes. the agent hits 300 clean invoices in weeks but has seen a dozen disputes. so invoices go autonomous now and disputes stay with the person, which is exactly where the human is still better. a model swap, or drift in sampled audits, sends a case type back to stage 2.

obvious question: what does replacement mean? new skill/plugin? skill/plugin that's adjusted to the general-task skill/plugin by the business' volume of this task? also, how do you measure error? most tasks aren't binary - the whole point of them not being automated yet is that they're not just successful/unsuccessful.  

what replacement means: four levels, each cheaper to run than the last.
1. general skill: instructions + tools shared across every business, learned from the pool.
2. general skill + this business's layer: its examples, rules, context, kept small. stop here for most nodes. at small-business volume (hundreds of examples) fine-tuning isn't worth it; retrieved examples in the prompt do about as well and survive model swaps, which keeps it model-agnostic.
3. code (the "vibe code an app" case). trigger: when a simple rule predicts the agent's outputs from its inputs, the agent is doing deterministic work at model prices. e.g. after 500 runs, "invoices from vendor X go to account Y" reproduces 99.5% of what the expense-categorizing agent does → compile that to code, keep the agent for the remaining 0.5%.
4. removal / merge: the edge disappears because two nodes become one.

generated code goes through the same 3 stages as any agent, and it's disposable: regenerate it from its contract + tests whenever the graph changes, never maintain it by hand.
  
  
graph orchestrator agent that makes suggestions for nod reorg / replacement based on the eval loops and suggestions (that maybe we can merge 3 nodes into 1, or we can make some edges cheaper to run) to human manager of the graph. - also the orchestrator agent should have the ability to just briefly vibe code an app by itself if it deems that it passes evals and does the job (so yes we can not only replace edges but nodes too).  
  
shared context layer (so agents can leverage the general info of the whole business, not only the edges they;re responsible for).