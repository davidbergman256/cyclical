>Cyclical runs a small business as a graph where people and agents are interchangeable steps, graded on what actually happens (show-ups, payments) and improved using outcomes pooled from every business running the same process, so the system does the orchestrating and the asset is an outcome history no model release can produce.


what we have to figure out:

UX
- orchestrator view
- node view (edges accessible to node and their context, missing edge flag that increases graph accuracy to reality)

typical agent best practices (limited context, permission limits)

model-agnostic evals for every edge - so the graph can improve
1. mirrors human task, tries to minimize difference between human output and its own
2. does the human tasks, but they require human checkoff before being passed
3. once it reaches some threshold, human feedback is no longer needed and the node can be replaced. 

stage 1: don't grade against the human. if the agent minimizes its difference from the human, its ceiling is the human, mistakes included. score both human and agent against what actually happened (invoice paid, patient showed up) wherever that exists; use agreement with the human only where nothing in the world grades the output. disagreements between human and agent are the most valuable data: resolve a sample of them by outcome.

stage 2: checkoffs decay into rubber stamps. approval rates drift toward 100% as people stop really looking, and the checker is labeling their own replacement. seed known-bad outputs into the queue at ~1 in 50; a checker who misses them isn't checking, and their approvals stop counting as evidence.

stage 3: needs a number. zero errors in n runs → 95% confident the error rate is below ~3/n (300 clean runs to claim <1%, 3,000 for <0.1%). a node that runs 50×/year never gets there on its own data → pooling. TODO: figure out pooling.

obvious question: what does replacement mean? new skill/plugin? skill/plugin that's adjusted to the general-task skill/plugin by the business' volume of this task? also, how do you measure error? most tasks aren't binary - the whole point of them not being automated yet is that they're not just successful/unsuccessful.  

what replacement means: four levels, each cheaper to run than the last.
1. general skill: instructions + tools shared across every business, learned from the pool.
2. general skill + this business's layer: its examples, rules, context, kept small. stop here for most nodes. at small-business volume (hundreds of examples) fine-tuning isn't worth it; retrieved examples in the prompt do about as well and survive model swaps, which keeps it model-agnostic.
3. code (the "vibe code an app" case). trigger: when a simple rule predicts the agent's outputs from its inputs, the agent is doing deterministic work at model prices. e.g. after 500 runs, "invoices from vendor X go to account Y" reproduces 99.5% of what the expense-categorizing agent does → compile that to code, keep the agent for the remaining 0.5%.
4. removal / merge: the edge disappears because two nodes become one.

generated code goes through the same 3 stages as any agent, and it's disposable: regenerate it from its contract + tests whenever the graph changes, never maintain it by hand.
  
  
graph orchestrator agent that makes suggestions for nod reorg / replacement based on the eval loops and suggestions (that maybe we can merge 3 nodes into 1, or we can make some edges cheaper to run) to human manager of the graph. - also the orchestrator agent should have the ability to just briefly vibe code an app by itself if it deems that it passes evals and does the job (so yes we can not only replace edges but nodes too).  
  
shared context layer (so agents can leverage the general info of the whole business, not only the edges they;re responsible for).