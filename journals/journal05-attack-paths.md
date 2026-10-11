# Learning Journal 5 — Attack Paths

## 1. What are Attack Paths?

Attack paths are chains of abusable user actions and privileges which establish direct and indirect dependencies between hosts and computers. They allow attackers to pivot from one compromised host or account to another, escalating privileges and transferring control across a network.

They are sometimes referred to as identity-based attack paths — i.e., attackers utilize valid user identities and access rights rather than relying solely on software vulnerabilities.

## 2. Why the Problem of Attack Paths Is Felt Most Clearly in Active Directory and Azure AD

The problem is most severe in Microsoft Active Directory (AD) and Azure AD because they are:

- Foundational – AD enables identity, authentication, access, endpoint, and business operations for nearly every organization.
- Ubiquitous – Used by governments and Fortune 500 companies, in addition to most other enterprises, rendering it an all-encompassing target.
- Powerful – The same capabilities that enable admins to seize control (Group Policy, delegation, and trusts) can be abused by attackers to seize control.
Taking control of AD means taking control of all users, devices, data, and business processes — the largest prize for attackers.

## 3. Five Reasons Active Directory Is the Adversary's Favorite Target

### 1. Unmatched Payoff

- Gaining control of AD guarantees access to everything: systems, users, data, and processes.
- Even systems not joined to AD may rely on it for identity validation (e.g., SSO, RADIUS).
- Control of AD = control of the enterprise.
### 2. Common Weakness

- Windows and AD make auditing permissions extremely difficult due to nested groups and opaque privilege structures.
- As a result, attackers are able to use the same techniques and tools (e.g., Responder, Mimikatz, BloodHound) against almost any organization.
### 3. Detection is Hard, Evasion is Easy

- Attackers prefer to "live off the land," abusing valid admin commands and activities.
- It is difficult to identify malicious from normal behavior.
- Attackers can evade detection using techniques like code obfuscation or security software disabling.
### 4. Deep Persistence Options

- More privileged environments offer more stealthy, harder-to-detect persistence (e.g., kernel-mode malware).
- AD control allows attackers to manipulate the operating system itself, sending false responses back to defenders.
### 5. Unlimited Retries

- Even the most effective SOCs cannot prevent repeated attempts.
- The attackers retrys infinitely, becoming more and more acquainted with each attempt, finding in the end an effective attack path.


## 4. Compare Attack Path Management and Vulnerability Management

| **Vulnerability Management (VM)**               | **Attack Path Management (APM)**                                                  |
| ----------------------------------------------- | --------------------------------------------------------------------------------- |
| Stresses software bugs and their correction.    | Stresses abusable privileges and identity relationships.                          |
| Uses CVSS scores to rate vulnerabilities.       | Quantifies empirically privilege abuse impact and choke points.                   |
| Exploits have traces and are costly to produce. | Attack paths leave very few traces and are easy to reuse to exploit.              |
| Mitigates one threat class.                     | Mitigates privilege-based lateral movement, usually more prevalent than exploits. |

## 5. The Least Privilege Pipe Dream

Least Privilege" means users have only the permissions they need to get their job done — but actually, this is rarely the case due to complexity and dearth of visibility in AD environments. Three crucial questions administrators need to answer (and wrestle with) are:

1. Is this privilege abusable?
- Hard to tell; new research often makes "safe" privileges vulnerable.
1. Who has this privilege?
- Nested groups make it difficult to trace who truly has access.    
1. Is this privilege required?
- Vendors and admins often overstate the need for broad permissions, and proving a privilege is unnecessary is difficult.
Because of these problems, least privilege is more an ideal than a reality, and attack paths continue to replicate.

## 6. Why Red Team Assessments Are the Incorrect Answer to Counteracting Attack Paths

Red team assessments are meant to assess detection and response capability, not to find and fix attack paths.
- They reveal _how_ the attackers could potentially penetrate the network but not _why_ the routes are there.
- It is a time-wasting exercise to "repair" the specific routes found in a red team exercise — an average environment contains millions or even billions of attack paths.
- Removing a path is like removing one road from a map — attackers will simply take an alternate path.
Thus, red teams are good to practice the defenders but are not good in solving the root cause of attack paths. 

## 7. Three Types of Problems That Threaten Organizations

1. **Known knowns** – Intelligible and measurable (e.g., patch management).
2. **Known unknowns** – Recognizable but hard to measure (e.g., asset management, least privilege).
3. **Unknown unknowns** – Problems the organization is unaware of and can't measure (e.g., attack paths for most orgs).

APM makes it possible to convert **unknown unknowns to known knowns** by constantly mapping and measuring attack paths.
## 8. Why Current Options to Address Attack Paths Fall Short

Existing options are not sufficient because they:

- Don't measure the problem's scale.
- Treat symptoms (e.g., endpoint detection) instead of root causes (abuse of privilege).
- Don't have practical means to actually reduce risk.
Good products like PAM, AV, and EDR are only "speed bumps" for cyber attackers — slowing them down but not stopping them.

## 9. Drivers Preventing Tiered Administration or Least Privilege Deployment

- **Opaque privileges:** Hard to know who has access to what.
- **Complex architecture changes:** Tiering could require redesign of identity, endpoint, and network architectures.
- **Quantifiable outcomes not attainable:** Organizations can't readily prove risk reduction or justify effort.

These barriers allow "best practices" to be nothing more than conceptual notions.

## 10. What Is Attack Path Management (APM)?

Attack Path Management (APM) is a process of constantly discovering, mapping, measuring, and remediating attack paths — namely in Active Directory and Azure AD.

It assists organizations:

- Identify choke points (which are the critical privileges or behaviors an attacker will need to exploit).
- Achieve tiered administration and least privilege in practice.
- Reduce AD's attractiveness as an attack vector.
Significantly, APM does not require dramatic architectural transformations.

## 11. The Three Pillars of APM

### 1. Continuous, Comprehensive Attack Path Mapping

- **Continuous:** As privileges and user activity change every day, mapping must be continuous.
- **Comprehensive:** All relationships and connections are mapped to reveal real privileges and hidden attack paths.
### 2. Empirical Impact Assessment of Attack Path Choke Points

- Identifies privileges or behaviors that **connect attackers to critical assets** (“choke points”).
- Measures the impact of each choke point (e.g., how many users it exposes to Tier Zero assets).
- Helps prioritize remediation.
### 3. Practical, Precise, and Safe Remediation Guidance

- **Practical:** No need for radical changes or migrations.
- **Correct:** Deliberate changing of removing core attack vectors.
- **Secure:** It includes methods to make certain privileges are actually critical before their elimination.
## 12. Attack Path Management advantages

- Elimination of "band-aid" solutions with the correction of root causes, not symptoms.
- Improves security posture with measurable improvement over time.
- Provides differentiated visibility into AD architecture and privilege relationships.
- Makes best practices possible — least privilege, tiering, and credential hygiene.
- Secures AD and causes attackers to seek less profitable or more challenging targets.
## 13. What Is BloodHound? Describe It.

BloodHound is a free, open-source tool initially created for offense security to map attack paths in Active Directory. Privilege relationships are represented and illustrated by the means that attackers could use to escalate access.

Yet defenders soon realized its use in attack path identification and minimization.

FOSS BloodHound limitations:

- Requires high levels of expertise (graph theory, Cypher queries, AD security).
- Does not produce meaningful metrics or offer remediation over time tracking.
- No persistent data collection, so data becomes obsolete quickly.

Beyond these limitations, BloodHound ignited Attack Path Management solutions like BloodHound Enterprise, specifically designed for continuous, defender-focused attack path reduction.