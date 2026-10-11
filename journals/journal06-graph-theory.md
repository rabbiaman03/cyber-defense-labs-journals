# Learning Journal 6 — Lateral Thinking and Graph Theory

Part 1:

1. Describe each type of lateral thinking, along with how each applies to cybersecurity. For each type, think of a real cybersecurity situation in which it applies.

Types of lateral thinking and cybersecurity examples:
• Problem reformulation: The issue is considered from another angle, which uncovers hidden assumptions. Suppose there is an uptick in login failures within an organization. Considering this now as a problem of credential stuffing presents much better defenses.
– Analogical thinking: Transfer ideas from unrelated domains. Since malware authors borrow software‑protection obfuscation tricks, anti‑DRM de‑obfuscation methods can be used against new malware by defenders.
divergent thinking implies the generation of many solutions with subsequent refinement. Red teams generate multiple attack vectors, such as phishing, SQL injection, and misconfiguration, before deciding which ones to test.
- _Challenging assumptions:_ Question conventional wisdom. Assuming all VPN access is MFAprotected can hide a legacy portal without MFA, so challenging that assumption leads to closing the loophole.
– _Pattern recognition_: Identify outliers or trends. It also identifies attempted DNS queries to non‑existent domains to detect DNS‑tunnelling exfiltration.
– Hypothesis testing: Form and systematically test possible vulnerabilities. This could be where a tester suspects that an app doesn’t sanitize input; crafting a payload and verifying whether it executes confirms XSS.
Perspective shifting: Put on the bad guy's glasses. Playing the role of the malicious insider helps identify the lateral movement paths and aids in the design of controls to cut them.
- Mind mapping: Observe the relationships and brainstorm. In incident response, it helps show how the attack happened in IR by designing an attack graph of accounts, servers, and C2 domains.
– _Counterfactual thinking_: Consider "what if" scenarios. Thinking of ransomware encrypting backups creates a desire for off-site backups and tested restore procedures.

- _Curiosity and Continuous Learning_: Keep up to date on new vulnerabilities and techniques. Continuous learning ensures defenders remain adaptable.

2. Why is lateral thinking in cybersecurity so crucial for you to practice?

Attackers view networks as interconnected graphs and creatively chain vulnerabilities. The practice of this set of lateral-thinking skills enables defenders to expect unconventional attack paths, question their assumptions and increase resilience.

3. What are two elements of a graph? Provide examples of each in cybersecurity.

In general, nodes represent entities such as computers, user accounts, or applications, and edges represent relationships such as network connections or admin rights. A directed edge could model an administrative relationship where user A has control over computer B; an undirected edge could indicate that two systems share credentials.

4. What are the three types of graphs? Give an example of each.
- _Directed graphs_ have directional edges, such as login relationships from compromised hosts to lateral-movement targets.

- _Undirected graphs_ show mutual relationships (e.g., trust relationships between domains).

- Weighted graphs assign weights to edges: these weights might be the risk or difficulty of exploiting a certain vulnerability.

5. Graph theory plays a significant role in analyzing network structure, attack pattern identification, and relationship visualization; please provide a detailed description.

Graphs help defenders analyze network structure by showing critical nodes and hidden dependencies, identify attack patterns through path analysis and anomaly detection, and visualize the relationships to understand how attackers might pivot from low-privilege to high-value accounts. Graph construction, shortest-path algorithms, and graph-based machine learning techniques provide methods to build and analyze these models.
6. For each of the three real-world examples of graph theory in cybersecurity from the article, describe them in detail.

- Threat Intelligence: Link analysis shows the relationships among threat actors, malware, and victims, while social-network analysis exposes adversary coordination.

- _Intrusion detection systems_: Graph-based IDS model normal behavior to detect deviations and flag unusual user activity in real time.

- _Malware Detection_: File dependency graphs and dynamic analysis enable detecting malicious interactions within systems and external C2 servers.

7. What are the difficulties in using the graph theory?

Addressing data's complexity and scalability, ensuring its quality, making intricate graphs interpretable to both technical and non-technical stakeholders alike, and keeping algorithms transparent.

8. What are the best practices for implementing graph theory?


Start small, applying graph analysis to high-impact areas and iterating. Invest in training and cross-disciplinary collaboration. Leverage existing network-visualization tools along with graph-based IDS.

9. Describe the two case studies.

- _Targeted attack detection_: A bank that was modeling user interactions in their systems found an unusual spike in data access by an account that had never accessed the data before.

- _Ransomware analysis_ – During a ransomware outbreak, a company constructed a communication graph, located the first set of infected servers, and restricted the propagation of malware.

part2:
1. Explain the following quote: "Defenders think in lists. Attackers think in graphs. s long as this is true, attackers win." - John Lambert, General Manager, Microsoft Threat Intelligence Center
The quote by John Lambert contrasts how defenders versus attackers view an IT environment. Defenders manage lists: assets, user accounts, vulnerabilities or alerts. A list is disconnected; it does not show how items are related. Attackers build graphs of relationships: who logs in where, what rights which accounts have, how servers trust one another. The article then says that lists in themselves such as those of assets and vulnerabilities just don't answer the types of questions like: Which systems are those vulnerabilities on? Who uses those systems? Graphs, on the other hand, show how a lowprivilege account can pivot through connections-for example, group membership, local admin rights, sessions-to reach highvalue targets. As long as defenders use lists and attackers think in graphs, attackers will find attack paths that defenders overlook.

2. Describe how attackers attack corporations, describing the four steps in order as outlined by the speaker.

- Reconnaissance: The attacker gathers publicly available information about the target organisation and its employees. They might mine LinkedIn in order to build a list of employees, job roles, and e-mail formats. Recon also includes finding out what technologies are in use, like public IP ranges, operating systems, Active Directory, etc.
- **Initial Access:** Through spear‑phishing or malicious attachments, an attacker lures a user to execute a payload that opens a connection back to the attacker's command‑and‑control server. Once a user runs the payload, the attacker has gained a foothold inside the LAN.

- **Lateral movement and post-exploitation privilege escalation:** The attacker looks for situational awareness and privilege. He enumerates computers, users, sessions, and file shares. Robbins says PowerView is a PowerShell framework that retrieves such information from Active Directory and is often used in this phase. Attackers also use credential-dumping tools like Mimikatz that can extract passwords from memory. With those credentials, they pivot across systems until they gain the necessary rights to reach the target.

- **Exfiltration:** Once the attacker has acquired the data required or has reached Domain Admin privileges, the data is exported outside over the existing command‑and‑control channe.

3. Describe each of the three key weapons in a red teamer's armory.
- **Situational awareness tool:** PowerView is mentioned as a post‑exploitation framework that enumerates computers, users, sessions and share information directly from Active Directory. It gives attackers a “map” of the network.


Credential‑extraction tool: Mimikatz, by Benjamin Delpy and Vincent Letoux, extracts passwords, NTLM hashes and Kerberos tickets from system memory. In case an attacker has local admin rights on a workstation where an interesting user is logged in, it will be able to recover that user’s credentials.

Command-and-control agent: Tools such as Beacon, Empire or Meterpreter act as implants on compromised machines, allowing remote command execution, data exfiltration, and lateral movement.

4. What were some challenges faced during post exploitation before Bloodhound was developed?
Before graph‑based tools like BloodHound existed, red teamers faced several difficulties:
Manual enumeration: This involved attackers utilizing lists from tools like PowerView and then manually stitching relationships together. This was often time-consuming and prone to error.
- Hidden paths: Complicated nested group memberships and ACLs made it difficult to determine exactly how low‑privilege accounts could indirectly gain high privileges. Attackers might easily overlook “identity snowball” paths where a user’s membership in multiple groups cascades to local admin rights and beyond.

- **Time and risk:** Lateral movement required testing credentials against many systems, which risks detection and can take days or weeks. Without automation, the attacker's situational awareness was limited.

5. What is Sharphound? What data does it collect?

SharpHound is the main data collection utility for BloodHound. It's a C# binary (and a replacement for the PowerShell collector) that has the capability of running via .NET reflection to avoid touching disk. It collects:
- **Local admin group memberships** across the domain.
- **Session information**--which users are logged on to which computers.

- Security‑group memberships and nested relationships.

- **Other edges** like GPO links, OU structures and ACL data when used with newer versions.

SharpHound is capable of gathering data from domain controllers via LDAP/SMB and from domain‑joined workstations via SMB, and it can do that all in memory, making it less detectable.
6. What information provided by BloodHound would an attacker be interested in?

After importing SharpHound data, BloodHound provides nodes (users, computers, groups, etc.) and edges (relationships). Attackers mainly are interested in:

- **Attack paths to high‑value targets:** BloodHound will find the shortest path from a low‑privilege account to Domain Admin or other privileged accounts by traversing relationships like `MemberOf`, `AdminTo` and `HasSession`. The model is simple: a user can be a member of a group, a group can be a member of another group or admin to a computer, and a computer can have a session for a user. A path emerges by chaining `AdminTo` and `HasSession` edges.

- **Who has local admin rights to which computers and who can RDP or execute remotely** via `CanRDP`, `CanPSRemote`, `ExecuteDCOM` edges.

- **ACL‑based object control** (e.g., who has `GenericWrite` or `WriteDACL` rights on a user or group).

- **Where privileged users are currently logged in** so they can steal credentials.

7. What is transitive object control, and in what ways is it useful?

The BloodHound node‑info tab provides metrics including **transitive object control** and **transitive object controllers**: • **Transitive Object Control** measures the number of objects a user, or group/computer, can gain control of by performing only ACL‑based attacks in Active Directory. That is, the maximum number of objects the principal can control without having to pivot to another system. It measures how far your influence can spread by means of chained permissions. - **Transitive Object Controllers** counts the number of objects that could potentially take control of a given object through ACL‑based attack paths. Understanding this allows defenders to identify all accounts that could indirectly compromise a sensitive object. These metrics are helpful for defenders in uncovering hidden privilege‑escalation chains, while helping attackers understand how many takeover paths potentially exist. 

8. What is arbitrary path finding? While BloodHound contains some prebuilt queries (e.g., “Shortest path to Domain Admin”), it also provides **arbitrary path finding**. This functionality enables the analyst to provide two arbitrary nodes—for instance, a help‑desk user and a database server—and task BloodHound with calculating a valid path through the graph. Arbitrary path finding is helpful when examining non‑standard attack scenarios that aren't modeled by one of the prebuilt queries, such as pivoting from a service account to a C‑suite executive's mailbox via delegated rights. 

9. Explain how patterns were used by the Bloodhound team to facilitate the attainment of the attacker's goals. In your explanation, be sure to address nodes and relationships. Robbins explains that after many engagements, red‑teamers noticed common patterns in lateral‑movement paths, such as “identity snowball” attacks. BloodHound codified those patterns by using graph theory. In its schema: - **Nodes** represent AD objects like users, groups, and computers. Connections (edges) represent privileges/activities: `MemberOf` (group membership), `AdminTo` (local administrator rights), `HasSession` (a user logged in on a computer), `GenericAll`/`WriteDACL` (ACL rights) and remote‑execution privileges. By modeling these elements as a graph, BloodHound can perform queries using algorithms like Dijkstra's shortest path to find the most efficient attack paths automatically. This automation turns lateral movement into a data problem and removes all guesswork. The simple schema also allows defenders to run the same queries to discover and remediate dangerous paths before attackers use them.