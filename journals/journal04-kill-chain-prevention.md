# Learning Journal 4 — Intrusion Kill Chain Prevention

### 1. Models Before the Kill Chain Paper

**Traditional models:**

- **Castle-and-moat defense (perimeter-focused):** Emphasis on strong firewalls, antivirus, and intrusion detection at network perimeters.

- **Defense-in-depth:** Multiple control layers (network, host, application, user) but sometimes reactive and static.
 - **Patching cycles and vulnerability management:** Emphasis on patching known vulnerabilities, not adversary behavior.
**Why insufficient:**

- They lacked **adversary-centric thinking** and did not take into consideration how attackers attack in stages.

- They were **reactive** rather than proactive.

- They offered no structured method of **segmenting adversary campaigns to dissect and disrupt**.

- They failed to support defenders in **anticipating attacker behavior or building detection/response around attack stages**.
### 2. Most Significant Takeaway from the Kill Chain Paper

The major take-away:

The **Intrusion Kill Chain** frames the attacker's campaign into **seven steps** — Reconnaissance, Weaponization, Delivery, Exploitation, Installation, Command & Control, and Actions on Objectives — giving defenders a way to **detect, deny, disrupt, degrade, deceive, or destroy** at each step.
### 3. Three Research Efforts Contributing to the Kill Chain Thesis

1. **Intelligence-driven defense** – Using adversary behavior patterns to inform defense.

2. **Operational-level analysis** – Campaigns understood over time, not discrete events.
3. **Theory of military kill chain** – Transposing the theory of sequential steps to the target from kinetic conflict into cyber.
### 4. Continuous Low-Level Cyber Conflict

Permanent state of **non-war cyber hostilities** in which nation-states, criminals, and hacktivists continually probe, penetrate, and exploit networks. It is "below the threshold" of public war but enduring and strategic — affecting power relations through espionage, disruption, and data theft.

### 5. Using Kill Chain to Counter Zero-Day Exploits

Even if an exploit is unknown and bypasses defenses at the **Exploitation** stage, defenders can still:

- Detect and block **Delivery** (e.g., phishing emails).
    
- Spot unusual **Installation** activity (e.g., malware persistence).
    
- Intercept **C2 traffic**.
    
- Respond quickly to abnormal **Actions on Objectives**.  
    The kill chain shows defenders they **don’t have to stop every stage** — disrupting any one can neutralize the attack.
### 6. State of Cyber Warfare

- Characterized by **state-sponsored APTs**, criminal syndicates, and hybrid actors.
- Activity is **persistent, stealthy, and strategic** in contrast to short-term.
- Nations utilize cyber means for **espionage, sabotage, and influence**.
- Cyber operations are **deniable and asymmetric**, blurring war and peace lines.
### 7. Where the Kill Chain Model Fails

- Too **linear and attacker-centric**; modern attacks are iterative and adaptive.
    
- Doesn’t cover **post-compromise lateral movement and persistence** in depth.
    
- Struggles with **insider threats** and **supply-chain attacks**.
    
- Lacks integration with broader defensive frameworks and real-world tactics.

### 8. Bottom Line of the MITRE ATT&CK Framework

**A globally accessible, rich knowledge base of adversary tactics, techniques, and procedures (TTPs).**

It supports defenders in attributing adversary behavior to known patterns and improving detection, response, and threat hunting.

### 9. How MITRE ATT&CK Expands the Kill Chain

- Offers **granularity** by explaining each phase of the kill chain in precise **techniques and sub-techniques**.
- Concentrates on **post-compromise behaviors** such as lateral movement, privilege escalation, and data exfiltration.

- Gives a **common language** to defenders and threat hunters.

- Supports **behavior-based detection** and not phase-based defense alone.

### 10. What Still Needs to Be Done with ATT&CK

- Improved **integration with automation and orchestration** tools.
- Enhanced **threat intelligence correlation**.
- Broader adoption for **real-time detection**.
- Expansion to encompass new technologies (IoT, cloud-native, AI-driven attacks).

### 11. The Diamond Model

A framework to analyze intrusions by relating **four fundamental aspects**:

- **Adversary** (who is targeted)

    - **Infrastructure** (what they use)
    - **Capability** /how they strike)
    - **Victim** /who they aim at)
Edges represent connections between these components, allowing analysts to better understand campaigns and attribution.
### Explanation:
- Extension to cover new technologies (IoT, cloud-native, AI-driven attacks).

### 12. Naming and Attribution Problem

- Multiple vendors use **different names for the same threat group** (e.g., APT29 = Cozy Bear = The Dukes).

- Attribution is typically **politically charged, technically vague**, and reliant on classified data.

- This inconsistency undermines cooperation and collective defense.

### 13. Active Adversary Playbooks

At any given time, **dozens of APT campaigns** and **hundreds of active playbooks** are ongoing globally. Because adversaries recycle tools and infrastructure, defenders must anticipate multiple **simultaneous, evolving campaigns** rather than discrete attacks.

### 14. Why the Author Favors the Intrusion Kill Chain Approach

- It shifts defenders from a **reactive to proactive mindset**.

- It provides **multiple opportunities** to disrupt the attacker.
- It aligns defense with **adversary tactics**, rather than vulnerabilities.
- It integrates smarts into business-as-usual work.
### 15. What Is a SOC?

A **Security Operations Center (SOC)** is a centralized entity that identifies, tracks, investigates, and reacts to cybersecurity attacks in real-time.

### 16. SOC Tactics Supporting the Kill Chain (7 total)

1. **Monitoring and detection** (recon/delivery phases)
2. **Threat intelligence integration**
3. **Incident response and containment**
4. **Threat hunting** (proactive detection)
5. **Deception operations**
6. **Automation and orchestration (SOAR)**
7. **Continuous improvement through feedback loops**

### 17. Why SOCs Are Necessary

- Threats are **24/7 and global**, requiring continuous defense.    
- They allow **centralized visibility, coordination, and rapid response**.
- Enable proactive adversarial detection **before goals are achieved**.

### 18. Orchestration in SOCs

Short form for **automating activities and unifying security tools and workflows** — enabling swift, coordinated responses without duplicated human intervention.
### 19. DevOps vs. DevSecOps

- **DevOps:** Combines software development and IT operations for faster delivery.
- **DevSecOps:** Brings **security to all stages** of the DevOps pipeline, so security is integrated in, not bolted on.
### 20. SOAR

**Security Orchestration, Automation, and Response** appliance automates mundane operations, consolidates fragmented security tools, and streamlines incident response — enhancing SOC efficiency and kill chain disruption.

### 21. SASE and SSE

- **SASE (Secure Access Service Edge):** A cloud-born solution that integrates networking (e.g., SD-WAN) with security services (e.g., SWG, CASB, ZTNA) in a single platform.
- **SSE (Security Service Edge):** The security component of SASE — with sole focus on security services and no network components.
### 22. Three Things That Make SSE Different from MSSP _(brief & informative)_

1. **Cloud-native delivery:** SSE is cloud-first; MSSPs work with traditional on-prem tools.
2. **Integrated security stack:** SSE converges SWG, CASB, and ZTNA; MSSPs typically offer point solutions.
3. **Identity-guided, policy-driven control:** SSE follows zero-trust and identity-driven policies, as opposed to MSSPs' reactive perimeter-centric defense.
