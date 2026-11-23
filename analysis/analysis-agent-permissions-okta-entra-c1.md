# Analysis: Just-in-time authorization for AI agents (Okta XAA, Entra Agent ID, C1/ConductorOne, Veza, Aembit, Keycard, Arcade, policy-as-code, IGA and PAM)

This cluster already ships most of thinking.md's A4 as products and standards: temporary, logged, policy-decided access for agents; human sponsors; access requests answered in Slack; removal of unused rights; role mining. It touches almost nothing else in the loop. **Overlap score: 2/10.** A4 alone is about 6/10, and every other aspect is near zero, because these products govern *who may touch what*, never *what work flows where* or *whether the work was good*. Two things matter most. First, Cyclical should buy or adopt A4's machinery rather than invent it. Second, the field's 40-year-old answer to the UNRESOLVED question is to separate the **custodian** that holds data from the **owner** who writes the policy. A system node never "answers" a request: a policy decision point answers, under rules authored by the data's owner, inside an envelope the vendor's contract sets. My proposal below adds one Cyclical-native step: **the node whose edge writes a data class into the system is its default steward**. That is computed from the same event log A2 already reads, so ownership comes out of process mining and needs no hand-appointed "responsible node".

## What it actually is

The cluster has four layers. They are often confused.

**1. Identity providers (IdPs) extending to agents.** An IdP is the system that logs people in and issues tokens: Okta, Microsoft Entra.
- **Okta Cross App Access (XAA)** is an OAuth extension built on the Identity Assertion Authorization Grant (ID-JAG). The agent's client gets a signed assertion from the company's IdP and trades it for an access token at the target app's authorization server. The IdP's admin policy decides whether app A's agent may reach app B, so the user sees no consent prompt at runtime [1][3]. XAA has been folded into the MCP spec as the "Enterprise-Managed Authorization" extension, with SDK support in TypeScript and Java and Python planned [2][3]. (MCP, the Model Context Protocol, is the standard way agents call tools.) Okta's "Agent SSO" reached GA (general availability) in August 2026 for an installed base of 20,000+ customers (trade press [4]), and the partner ecosystem grew in June 2026 [5]. Okta's own docs advise *against* XAA for agents that run without an active user session or human initiation [3]. That describes a Cyclical node occupant exactly.
- **Okta's other agent products** (from memory): Auth0 "Auth for GenAI" / "Auth0 for AI Agents" offers a Token Vault (Auth0 holds third-party OAuth tokens for the agent), asynchronous human approval via CIBA (Client-Initiated Backchannel Authentication: a push "approve this action?" to a phone), and Okta FGA (fine-grained authorization), a hosted version of the Zanzibar-style OpenFGA. "Okta for AI Agents" discovers shadow agents by reading OAuth grants.
- **Microsoft Entra Agent ID** (announced May 2025; governance features through 2026) gives each agent a directory identity alongside employees. Every agent has an **owner** (technical) and a **sponsor**, the human accountable for it. An agent can request an *access package* (a bundle of group, app and SharePoint rights with an approval policy and an expiry) for itself, or its owner or sponsor can request one for it. The sponsor can be the required approver, with a mandatory business justification. Before expiry the sponsor is notified and can request an extension, which triggers a new approval cycle. If nobody acts, access lapses [6][7][8]. Microsoft's framing: "govern AI agent identities and access the same way you govern your employees" [7]. I found no official page confirming *per-request* just-in-time approval for agents. What ships is time-boxed packages [search extract, 6].

**2. Identity governance (IGA) and access-request products.** IGA is the category that decides who should have which entitlement, runs approvals, and runs periodic "access reviews".
- **C1.ai (formerly ConductorOne)** connects people and agents to email, CRM, code repositories, finance and cloud, with JIT requests and approvals (Slack-native, from memory) and policy-based auto-approval. Workday announced on Oct 13 2026 that it will acquire C1, price undisclosed, expected to close by Jan 31 2027 (8-K [9]). The plan is to extend Workday's "Agent System of Record" (which already registers agents) so that hires, role changes and departures in Workday grant and revoke access for employees *and* agents [9][10]. The announcement is silent on C1 customers whose HR system is not Workday [11].
- **Veza** builds an "Access Graph": a graph of identity → permission → resource across hundreds of systems, used to find over-privilege and dormant rights. ServiceNow announced the acquisition Dec 2 2025 and closed Mar 2 2026 for about $1.2B (secondary source citing the 10-Q [12][13]). Veza had raised a $108M Series D at an $808M valuation in 2025 [13].
- **SailPoint** pioneered role mining: clustering co-occurring entitlements into proposed roles. Its data-access product runs "data owner election", which nominates owners for unowned file shares and data stores from who actually uses them (secondary [22]; product details from memory).

**3. Agent and workload credential brokers.** These hold secrets so the agent never does, and mint short-lived scoped tokens per task.
- **Aembit**: workload IAM (identity and access management) extended to agents. $25M Series A, Sept 2024 [14].
- **Keycard**: task-scoped agent tokens. About $38M total, a $30M Series A led by Acrew (Oct 2025; some trackers date it 2026) [14][16].
- **Arcade.dev**: the authorization layer for agent tool calls, proving "which agent took which action for which user". $60M Series A, June 2026 [15].
- **Astrix**: discovery of non-human identities. $45M Series B, Dec 2024. One tracker reports an acquisition by Cisco (~$400M); I could not verify this [14].
- **Descope** (agentic identity hub) and **Permit.io** (access requests with human approval as embeddable UI) are smaller, from memory.

**4. Policy-as-code and ReBAC engines.**
- **OPA** (Open Policy Agent, Rego language; a CNCF graduated project).
- **Cedar** (AWS's analyzable policy language, behind Amazon Verified Permissions).
- **Zanzibar-style ReBAC** (relationship-based access control): Google's 2019 Zanzibar paper; implemented in AuthZed/SpiceDB, OpenFGA and Oso (from memory).

These engines are the "decide by rules, not wording" part. A request is evaluated as `(principal, action, resource, context)` against policies, with no natural-language input at all.

**Plus PAM JIT.** PAM (privileged access management) covers admin and production access. CyberArk's zero standing privilege model (agreed sale to Palo Alto Networks in 2025, from memory) and Teleport Access Requests (requests auto-approved by rule, e.g. when PagerDuty shows the requester is on call; from memory) are the human-JIT ancestors. **Protocols:** the MCP authorization spec treats MCP servers as OAuth resource servers (2025 revisions, from memory). Google's A2A protocol (Apr 2025, now at the Linux Foundation) has agents advertise their auth schemes in "Agent Cards" but defines no authorization model of its own (from memory).

**Who buys:** CISOs and IAM teams at mid-to-large enterprises. None of these vendors sells to a 9-person dental office. Such an office usually has Microsoft 365, which means it has a basic Entra tenant, but no IGA, no PAM and no policy engine.

## Loop comparison

| Aspect | Cluster's approach | vs Cyclical |
|---|---|---|
| A1 Core frame | Entra and Workday put people and agents in one directory with the same governance (access packages, lifecycle, sponsor/manager). Veza's graph is identity→permission→resource, not a graph of work handoffs. | Same at the identity layer; absent at the work layer |
| A2 Observation | Veza and C1 read entitlements and usage from 300+ connected systems (from memory). Okta discovers agents from OAuth grants. They observe *who can reach what* and *who used it*, not the sequence of work. | Different: permission and usage logs, not process logs; a partial edge detector |
| A3 UX | Access requests answered in Slack/Teams (C1, Teleport); CIBA push approval (Auth0); My Access portal (Entra). Approval happens where people already are. | Same principle |
| **A4 Permissions** | Time-boxed grants (Entra packages, C1, Teleport); full audit logs; policy auto-approval keyed on attributes; human sponsor per agent; XAA replaces runtime consent with admin policy; removal of dormant access (Veza, C1, IGA reviews); role mining turns frequent co-grants into roles. | **Better on mechanics and ahead on standards. Absent: frequency → *missing edge*.** |
| A5 Shadow eval | None | Absent |
| A6 Checkoff / seeded errors | Access reviews are a famous rubber-stamp problem. Nobody seeds known-bad grants to test reviewers (from memory). | Absent; same failure mode documented |
| A7 Graduation | None. The closest analog is the auto-approval policy that replaces a human approver once a pattern is trusted, with no statistical bar. | Absent |
| A8 Replacement levels | Role mining equals "compile repeated decisions into a rule" (level 3) for permissions only. | Analogous, narrow |
| A9 Orchestrator | IGA "AI assistants" recommend approve/revoke (from memory); nothing proposes reorganizing work. | Absent |
| A10 Shared context | Absent. These products *restrict* context. | Absent |
| A11 Pooling | Peer-group analysis within one company (SailPoint, from memory); no cross-customer outcome pooling. | Absent |
| A12 Anti-Goodhart | Separation-of-duties (SoD) rules are a business-level guardrail on access ("no one both creates and approves a vendor payment"). | Analogous, worth copying |
| A13 Model-agnostic | Fully. Identity and policy layers do not care which model runs. | Same |
| A14 Moat | Install base as identity system of record; Workday adds HR system of record. | Different: their moat is the directory, Cyclical's is outcome history |

**A4 element by element.**

*Node-to-node JIT requests.* Products ship the request-and-approve loop, but the requester asks a **central policy point or a named human**, never "the node holding the data". Entra routes to the agent's sponsor or a package approver [6]. XAA routes to the IdP's policy [3]. The central design is better for Cyclical too. Peer-to-peer asking among agents is exactly the channel ServiceNow's agent-to-agent discovery exposed (see Feedback). Cyclical's "ask the node that has the information" should become "ask the policy decision point about the resource that node holds".

*Temporary, logged grants.* Shipped everywhere: Entra expiry and renewal with re-approval [6], Teleport, C1. Practitioners add an important caveat: OAuth tokens do not shrink when a task completes, and MCP scopes are coarse ("read-only access to one folder for an hour" cannot be expressed as a scope) [25][26]. Real task-scoping needs a broker that mints per-task tokens (Keycard, Arcade, Aembit) or a proxy that holds the credential. That is the HN consensus: "your proxy should check if the action is allowed and set the secrets on the fly" [30].

*Rule-based, not persuasion-based approval.* Policy engines do this by construction: Cedar and OPA never see request text. XAA's "no consent at runtime" is the same idea at the protocol level [1]. Cyclical's rule key is (who asks, data class, task type). The incidents below show that key is **necessary but not sufficient**. In both ServiceNow and ForcedLeak, the requester was a legitimately entitled agent whose context had been poisoned. A rule on "who asks" passes it. The missing input is **provenance**: has untrusted content entered this task? CaMeL (Google DeepMind, 2025) tags every value with its source and checks policies at tool-call time, with no model change, at 77% task completion vs 84% undefended on AgentDojo [32][33]. Meta's "Rule of Two" (Oct 2025, from memory) says an agent should have at most two of: untrusted input, sensitive data, external communication or state change. **Almost every dental front-office node has all three by default**: it reads patient email, reads the PMS and sends messages. So A4's rule key should become (requester, data class, task type, *taint of the task's context*, egress destination).

*Frequency → permanent grant.* IGA's role mining does this: repeated co-occurring grants become a proposed role. Teleport and C1 auto-approval policies are the "promote a recurring request to a rule" step (from memory).

*Frequency → missing edge.* **Absent everywhere, and this is Cyclical's genuinely new idea in A4.** IGA has no model of workflow, so it can only answer repeated access with more access. Cyclical can answer "billing agent queries appointment data 40×/week" with "make appointment completion flow to billing as an edge". That changes the process instead of widening the permission.

*Unused-permission removal.* Shipped and mature: Veza dormant-access findings, IGA certification campaigns, Entra expiry-by-default. Expiry-by-default (Entra's model [6]) beats "detect unused for months and propose removal". The right default is that nothing is permanent unless renewed.

## Where they're ahead of Cyclical

1. **Standards Cyclical will have to speak.** XAA is now MCP's enterprise authorization extension [2]. If Henry Schein One's MCP layer (Ask/Orchestrate/Build, announced Apr 2026 [37]) adopts it, practice-level policy for PMS access would sit in an IdP. Cyclical should be an XAA/ID-JAG client and keep its own policy store compatible with that model.
2. **A human sponsor for every agent, with lifecycle.** Entra's owner/sponsor split, plus Workday's plan to revoke an agent's access when its sponsor changes role [9][10], solves "who is accountable for this node occupant" more cleanly than thinking.md does. Cyclical has nodes but no named accountable human per agent occupant.
3. **Expiry as the default, re-approval at renewal** [6].
4. **Credential brokering.** Agents never hold secrets; per-task tokens are minted at call time (Keycard, Arcade, Aembit [14][15][16]).
5. **SoD rules** as access-level guardrails: a direct, proven template for A12.
6. **An 8-year record of IGA failure modes**: rubber-stamp access reviews, orphaned owners, approval fatigue. Cyclical's A6 rediscovers these.

## Where they're doing it differently (and whether their way is better)

**Central policy decision vs node-to-node asking.** The standard architecture (XACML's vocabulary, from memory) splits authorization into four parts:
- PAP (policy administration point): where an owner writes rules.
- PDP (policy decision point): evaluates a request against those rules.
- PEP (policy enforcement point): blocks or allows at the resource.
- PIP (policy information point): supplies attributes such as data class or taint.

Their way is better. It removes the agent-to-agent negotiation channel (the ServiceNow failure) and makes "who decides" a property of the policy rather than of the node. It also dissolves most of the UNRESOLVED question (below).

**Permission-centric vs work-centric graph.** Veza's Access Graph is the closest structural cousin of Cyclical's graph, but its edges are "can access", not "hands work to". Cyclical's way is better for its purpose: only a work graph can convert repeated access into a missing edge. Veza's is better for audit. Cyclical needs both, and could derive the access graph from its work graph.

**Human approval as the normal path vs as the exception.** IGA routes most requests to people. Cyclical (and the better PAM products, e.g. Teleport's on-call auto-approval) routes most to rules and escalates only unmatched cases. Cyclical's way is better for agents: practitioner evidence on approval fatigue is unanimous [26][38][29].

## The UNRESOLVED question: who answers for data in a system node?

Five existing answers, from products and literature, each solve part of it:

| Model | Who answers | Where it ships | Fit for a dental office |
|---|---|---|---|
| IGA resource/data owner | A named business owner per app or data set; requests stall without one (One Identity blocks approval; Ping requires an owner before a resource is requestable) [24] | Every IGA | Correct idea, but a hand-appointed owner per system is the "inelegant special case" thinking.md rejects |
| Owner election from usage | Owner nominated from who actually reads and writes the data, then confirmed [22] | SailPoint data access (secondary) | Good: derived from logs |
| DAMA data owner / steward / custodian | Owner (accountable executive) sets policy; steward defines rules for a data domain; custodian (IT/system) only enforces (DAMA-DMBOK, from memory) | Data governance practice | Exactly the needed split: the PMS is a custodian |
| ReBAC ownership relations (Zanzibar) | Nobody "owns" by being the container. Ownership is a relation tuple (`record#owner@...`) and permissions inherit through relations (`parent` folder → document) (Zanzibar paper, from memory) | SpiceDB, OpenFGA, Okta FGA | Lets authority flow from the business relation (practice ↔ patient) rather than the storage location |
| Contract-defined external authority | The vendor's API program sets what is grantable at all: Dentrix API Exchange charges $5,000 read + $5,000 write setup plus monthly royalties and can revoke [34][37]. HSO v. Vyne (Oct 2025) is a live fight over whether HSO can block practice-authorized data flows; Vyne's countersuit invokes the Cures Act information-blocking rules [35] | Dental PMS | The outer envelope. Not a decider of individual requests |

The law points the same way. Under HIPAA the practice (covered entity) is responsible for the data, and the PMS vendor is a business associate, i.e. a custodian under contract. HIPAA's "minimum necessary" standard requires the practice to define, per workforce class, which categories of patient data each role needs (from memory). That is literally "every node has default permissions for its edges, by data class".

**Proposed answer: the system node is never a decider.** Authority has four layers, and none needs a per-system responsible node:

1. **Envelope: contract.** The vendor API contract (or open API) defines which scopes Cyclical can technically and legally obtain. This is the "external authority" node class from the dental PMS analysis [37]. It changes rarely and is answered commercially.
2. **Policy: owner.** The practice owner (HIPAA's covered entity) authors the policy once at onboarding, as a small rule table keyed on (requester role, data class, task type, context taint, egress). Cyclical's PDP evaluates every request against it. The system node is a PEP. In practice Cyclical's broker is the PEP, because Cyclical holds the single practice-level PMS credential and mints per-task scoped access to agents, which never see the credential [30]. Most requests end here, with no human.
3. **Steward: writer by default.** When no rule matches, the request escalates to the steward of that data class. **The steward is the node whose edge writes that data class into the system**, computed from the PMS audit and event log Cyclical already reads for A2:
   - the front desk writes appointments;
   - billing writes claims and payments;
   - the hygienist writes perio charts;
   - for data arriving from outside (insurer ERAs, patient intake forms), the steward is the node that receives that inbound edge.

   This is SailPoint-style owner election with the vote taken from process mining, and ReBAC's "ownership is a relation" with the relation being *produced-by-edge*. It also makes the steward a property of the graph. When an edge moves (billing goes to the pooled desk), stewardship moves with it automatically.
4. **Fallback: owner.** Data classes with many writers (patient demographics), or a steward node that is itself an agent below graduation, fall back to the practice owner. An agent can occupy a steward node, but its stewardship decisions should be rule-only until the node graduates. A sub-graduation agent never approves an unmatched request.

This is one mechanism, not a special case. The same event log yields edges (A2), steward relations (A4) and request frequencies (A4 → missing edge). The case that stays genuinely unresolved is data written by the vendor itself (fee schedules, insurer plan tables shipped by HSO). Its steward is the contract layer, so it is read-only to the practice by construction. My confidence that this model survives contact with real practices: about 70%. The likeliest failure is that a 9-person office's owner-dentist wants to approve nothing, so the rule table must ship pre-filled from the pool (A11) and need only confirmation.

## Feedback & reviews on these parts of the loop

**Prompt-injection-driven authorization failures (independent research; vendor responses noted).**
- *ServiceNow Now Assist, second-order injection (AppOmni, Nov 2025).* A low-privilege agent reading a poisoned record used default **agent-to-agent discovery** (agents grouped into the same "team" by default) to recruit a more-privileged agent. The chain copied and exfiltrated data, modified records and escalated privileges, and it worked with ServiceNow's prompt-injection protection on. ServiceNow said the system "works as intended" and changed only documentation. AppOmni's Aaron Costello: "it's expected behavior as defined by certain default configuration options." Recommended fixes: supervised mode for privileged agents, disable autonomous override, segment agents by team [17][18]. **Lesson for A4:** peer-to-peer agent requests are the attack surface. Route everything through a PDP and partition which agents can even discover each other.
- *Salesforce Agentforce "ForcedLeak" (Noma Labs, Sept 2025, CVSS 9.4).* Instructions were planted in a public Web-to-Lead form's 42,000-character description field. When an employee later queried the lead, the agent gathered other leads' data and sent it out in an image URL to a domain still on Salesforce's CSP allowlist (the browser's list of permitted destinations). The domain had lapsed, and the researchers bought it for about $5. Salesforce began enforcing Trusted URLs on Sept 8 2025 [19][20]. **Lesson:** the agent had legitimate read access. The failure was untrusted input plus egress. A dental intake form or patient email is the same shape as Web-to-Lead.
- *ServiceNow CVE-2025-12420 (CVSS 9.3, Jan 2026)*: unauthenticated user impersonation in the AI platform. Not prompt injection, but an identity-layer failure in an agent platform [21].

**Practitioner feedback on agent permissions (independent, mostly HN; Reddit was blocked from this session).**
- Agents inherit human credentials: "In most setups I've seen, the AI agent inherits whatever credentials the developer has" [28].
- The working pattern is a broker that holds the credential and asks the human. One commenter: the command goes "to a segregated process which asks the user for permission, then runs it" [30][29].
- Approval prompts decay. A commenter notes the "always approve" option sits next to "approve", and one published attack ran with "Always Allow" set [29][38].
- Approval fatigue is the most-cited complaint even in vendor and integrator write-ups: "If your approval gate fires on every minor action, users click through without reading" (FusionAuth, via [26]). WSO2 notes that confirming every read "creates approval fatigue" [26]. This is the access-request version of A6's rubber-stamp problem, and it argues for rule-first approval with humans only for unmatched cases.
- MCP scopes are too coarse and static. Delegation at connect time does not cover what the agent does afterward, so per-action review is needed for exports and admin changes [25][27] (vendor/analyst-sourced).

**IGA ownership (secondary).** Requests stall without a named owner. One Identity blocks approval, and SAP Access Control stops routing when a risk owner is missing [24]. Owner election "doesn't replace the owner's accountability", and nomination should use "the nominee's actual interaction with the asset" [22]. That supports the writer-is-steward rule. Central IT approvers "often lack business context" [23].

**Adoption signals (vendor/trade press).** Okta Agent SSO GA Aug 2026 [4]; XAA ecosystem expansion Jun 2026 [5]; Workday's C1 rationale is that the HR system of record should drive agent access [9]. I found no independent outcome data (e.g. reduction in over-privilege for agents) for any product in the cluster.

## Top-level: why they chose this path, and what to learn

**Starting assets and constraints.** Okta and Microsoft own the directory and the login. An agent is one more principal to them, so they extend OAuth (XAA) and the directory (Agent ID), and they sell to the CISO. Workday owns the HR record of who works where, so buying C1 makes "joiner/mover/leaver" drive agent access [9]. ServiceNow already runs approvals and workflows, so buying Veza's permission graph completes its "AI control tower" story [12]. The startups (Keycard, Arcade, Aembit) start from developers building agents, where the pain is secrets in prompts and coarse OAuth. Every one of them is constrained to be **workflow-agnostic**. They sell to companies whose workflows they do not see, so they can govern access but cannot propose a different process. That constraint is why frequency → missing edge does not exist in the market.

**Copy.**
- Use a central PDP with policies in Cedar or OPA (Cedar is analyzable, so "can any front-desk agent ever reach payment data?" can be proven).
- Use Zanzibar-style relations for the steward relation.
- Give every agent occupant a human sponsor.
- Expire grants by default.
- Keep credentials in a broker that mints per-task tokens.
- Speak XAA/ID-JAG toward any PMS MCP endpoint.
- Write SoD rules as A12 guardrails.
- Add taint and egress to the rule key (CaMeL / Rule of Two).

**Avoid.**
- Peer-to-peer agent negotiation (ServiceNow).
- Human approval on the hot path (fatigue).
- Hand-appointed per-system owners (stalls).
- Building a general identity product. It is a commodity, and Microsoft gives a basic version away inside Microsoft 365.

**Exploit.** These vendors cannot see the work graph, so they cannot do the two things Cyclical's A4 uniquely enables. One is converting repeated requests into missing edges. The other is deriving stewardship from who writes the data. They also do not sell to 9-person practices. A dental office will not buy Okta or SailPoint, so for Cyclical's customer, A4 must arrive pre-configured, with pooled default policies per role and data class.

**Clone, subset, superset or orthogonal?** Cyclical is a **superset that should treat this cluster as a component**. Cyclical's A4 should run on these mechanisms, as an embedded library (Cedar/SpiceDB) or through standards (XAA), and add the workflow-aware layer on top.

**Threat level: low as competitor (2/10), high as a set of standards Cyclical must follow.** The observation that would tell David the threat is rising: **Microsoft folds Entra Agent ID governance (sponsors, access packages, usage-based recommendations) into Microsoft 365 Business Premium for small businesses, and a dental PMS vendor accepts Entra- or Okta-issued agent identities on its MCP endpoint.** Then the practice's agent registry and permission policy would live in Microsoft's tenant, and the work graph would be the only thing left for Cyclical to own. A second signal: Workday or ServiceNow shipping "access pattern → workflow change" recommendations. That would mean an identity vendor has started modeling the work graph.

## Sources

1. Okta, "Introducing xaa.dev: A Playground for Cross App Access" (Jan 2026): https://developer.okta.com/blog/2026/01/20/xaa-dev-playground
2. Okta newsroom, "Cross App Access extends MCP…": https://www.okta.com/newsroom/articles/cross-app-access-extends-mcp-to-bring-enterprise-grade-security-to-ai-agents/
3. Okta developer docs, Cross App Access concepts and agent-to-app guide (search extracts; host blocked from direct fetch): https://developer.okta.com/docs/concepts/xaa/ ; https://developer.okta.com/docs/guides/xaa-agent-to-app/main/
4. AI Stack Current, "Okta Agent SSO reaches GA with Cross App Access": https://aistackcurrent.com/news/okta-agent-sso-cross-app-access-ga/
5. SiliconANGLE, "Okta expands Cross App Access ecosystem" (Jun 23 2026): https://siliconangle.com/2026/06/23/okta-expands-cross-app-access-ecosystem-secure-ai-agent-connections/
6. Microsoft Learn, "Access packages for agent identities" (search extract; host blocked from direct fetch): https://learn.microsoft.com/en-us/entra/agent-id/agent-access-packages
7. Microsoft Entra blog, "Govern AI agent identities and access the same way you govern your employees": https://techcommunity.microsoft.com/blog/microsoft-entra-blog/govern-ai-agent-identities-and-access-the-same-way-you-govern-your-employees/4529302
8. Microsoft Mechanics, "Microsoft Entra Agent ID explained": https://techcommunity.microsoft.com/blog/microsoftmechanicsblog/microsoft-entra-agent-id-explained/4494408
9. Workday Form 8-K, Exhibit 99.1 (Oct 2026): https://www.sec.gov/Archives/edgar/data/0001327811/000132781126000051/wday-10122026x991.htm
10. Start With Identity, "Workday to acquire C1.ai": https://startwithidentity.com/blog/2026-10-13-workday-to-acquire-c1-ai-formerly-conductorone/
11. BERI, "Workday to Acquire C1.ai to Automate Access for AI Agents": https://www.beri.net/article/workday-c1-ai-conductorone-acquisition-agentic-identity-governance-agent-system-of-record-non-workday-customers-continuity
12. SiliconANGLE, "ServiceNow to acquire Veza" (Dec 2 2025): https://siliconangle.com/2025/12/02/servicenow-acquire-veza-move-expand-identity-security-portfolio/
13. Start With Identity, "ServiceNow completes Veza acquisition": https://startwithidentity.com/blog/2026-03-02-servicenow-completes-veza-acquisition/
14. NHI Governance funding tracker: https://nhigovernance.com/market/nhi-funding-tracker.html
15. PYMNTS, "Arcade raises $60 million": https://www.pymnts.com/news/investment-tracker/2026/arcade-raises-60-million-to-control-ai-agents/
16. Cyber Company Profiles, Keycard: https://cybercompanyprofiles.com/companies/keycard
17. The Hacker News, "ServiceNow AI agents can be tricked into acting against each other": https://thehackernews.com/2025/11/servicenow-ai-agents-can-be-tricked.html
18. AppOmni AO Labs, agent-to-agent discovery prompt injection: https://appomni.com/ao-labs/ai-agent-to-agent-discovery-prompt-injection/
19. SecurityWeek, "Salesforce AI hack enabled CRM data theft": https://www.securityweek.com/salesforce-ai-hack-enabled-crm-data-theft/
20. Security Affairs, ForcedLeak: https://securityaffairs.com/182676/hacking/forcedleak-flaw-in-salesforce-agentforce-exposes-crm-data-via-prompt-injection.html
21. The Hacker News, ServiceNow CVE-2025-12420: https://thehackernews.com/2026/01/servicenow-patches-critical-ai-platform.html
22. NHI Mgmt Group, "Automated data ownership election closes a data governance gap" (citing SailPoint): https://nhimg.org/articles/automated-data-ownership-election-closes-a-data-governance-gap/
23. NHI Mgmt Group FAQ, "Who should own approval authority for app access requests": https://nhimg.org/faq/who-should-own-approval-authority-for-app-access-requests/
24. Ping Identity, access request configuration (owner required); One Identity / SAP ownership behavior via search extracts: https://docs.pingidentity.com/pingoneaic/identity-governance/administration/access-request-configure.html ; https://support.oneidentity.com/technical-documents/doc2096544
25. Curity, "MCP Authorization Isn't Enough for AI Agents": https://curity.io/blog/mcp-authorization-isnt-enough-for-ai-agents/
26. WSO2, "MCP Authorization: The Complete Developer Guide": https://wso2.com/identity-platform/learn/mcp-authorization-guide/
27. NHI Mgmt Group, "Identity assertion grants are changing MCP authorization": https://nhimg.org/articles/identity-assertion-grants-are-changing-mcp-authorization-for-ai-agents/
28. HN, "AI agent has more production access than your senior engineers": https://news.ycombinator.com/item?id=46966307
29. HN, "The Webpage Has Instructions. The Agent Has Your Credentials": https://news.ycombinator.com/item?id=47387870
30. HN, "Running coding agents without handing them my credentials": https://news.ycombinator.com/item?id=50526152
31. HN, "Is anyone else bothered that AI agents can basically do what they want?": https://news.ycombinator.com/item?id=47833278
32. Debenedetti et al., "Defeating Prompt Injections by Design" (CaMeL): https://arxiv.org/abs/2503.18813
33. Simon Willison on CaMeL: https://simonwillison.net/2025/Apr/11/camel/
34. Dentrix API Exchange FAQ (fees), via the dental PMS analysis: https://ddp.dentrix.com/pages/faq
35. HSO v. Vyne: https://www.drbicuspid.com/dental-practice/legal-issues/article/15768710/henry-schein-one-vyne-dental-sue-each-other ; https://www.dentistryiq.com/practice-management/industry/article/55321885/vyne-dental-and-henry-schein-one-file-dueling-lawsuits
36. Zanzibar: Google's Consistent, Global Authorization System (USENIX ATC 2019), referenced from memory, not fetched: https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/
37. Internal: /home/user/cyclical/analysis/analysis-dental-pms-archy-planetdds-henryschein.md (A4 system-node section, HSO MCP tiers, API fees)
38. eSEOspace, "MCP Approval Fatigue": https://eseospace.com/blog/mcp-approval-fatigue/

Research note: learn.microsoft.com and developer.okta.com were blocked from direct fetch in this session (they would need to be allowed in the session's network settings), and Reddit was blocked from search. Facts from those pages come from search extracts. Meta's "Rule of Two", the XACML PDP/PEP split, DAMA-DMBOK roles, HIPAA minimum-necessary and the A2A details are from memory.
