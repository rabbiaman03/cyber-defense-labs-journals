# Learning Journal 7 — Zero Trust

Part 1

1. Describe, in detail, the concept of Zero Trust.

Zero Trust (ZT) is a paradigm for designing networks, systems and workflows that focuses on resource protection, according to the National Institute of Standards and Technology. _Trust is never granted implicitly_; every access request is continuously evaluated using risk‑based policies. In addition, Zero Trust assumes an attacker is present on the network and that internal and external networks should be treated as hostile.

2. In detail, describe how you would answer the following question in a job interview, "How would you go about implementing zero trust in our company?"

I would approach Zero Trust as a strategic initiative, following a some steps :
a. **Identify the Protect Surface:** Start small by identifying the most critical data, assets, applications, and services. This is more focused and manageable than trying to secure the entire attack surface.
b. **Map the Transaction Flows:** Understand how users and systems interact with the protect surface. This reveals dependencies and helps design policies that don't break workflows.
c. **Architect a Zero Trust Environment:** Build policies around the protect surface using a Zero Trust control plane and data plane.
d. **Create the Zero Trust Policy:** Write the core policy: Who can access What under Which conditions. This is based on user identity, device posture, requested application, and other context.
e. **Monitor and Maintain:** Continuously monitor the network, log traffic, and inspect activity. Use this data to improve policies, detect anomalies, and respond to incidents.

3. Describe the Gartner Hype cycle, and how it applies to Zero trust. Please do a little outside reading for this.
The Gartner Hype represents the maturity, adoption and social application of specific technologies. It has five phases:
Innovation Trigger: A breakthrough that generates significant press and social applications. 
Peak of Innflated Expectations: It refers early success stories crate over unrealistic expectations. 
Trough of Disillusionment: Interest go through experiments and implementations fail to deliver.
Slope of Enlightenment: The benefits and practical application of the technology become better understood. 
Plateau of Productivity: The benefits of technology become demonstated and accepted. 

4. What is cyber hygiene,, and how can it add to zero trust?
Cyber hygiene refers to to the fundamental practices and habits that users and administrators must follow to maintain system health and improve online security. It adds to Zero Trust by  strengthening the verify process. A device which is not updated or has outdated antivirus can be deemed non-compliant by a policy engine and it can deny access. Thus, it enforced a higher security standard before granting trust. 

5. Describe the concept of defense in depth, providing examples,, and how it can add to zero trust.
Defense in depth is a way of increasing security controls by implementing multiple layers of security and diverse controls throughout an IT system to protect valuable assets. If one control fails, another steps in. For example a firewall playing rule on layer 1, Intrusion Detection System on layer 2 and encryption on layer 3.  Zero Trust can adopt defense in depth by making each layer more intelligent and context-aware. Instead of relying only on static firewall, it can have identity-aware proxy. 

6. Describe the concept of perimeter defense, and how it can add to zero trust.

perimeter defense is a security model, where strong defenses such as firewall or IDS/IPS are placed at the network's end boundary to keep the treats out and everything inside to be trusted. Zero Trust, on the other hand, does not add perimeter defense. It replaces its underlying assumption.  Zero Trust takes the _concept_ of strict access control from the perimeter and applies it to every individual resource.

7. What assumption is made by network architects attempting to achieve zero trust?

The core assumption is that a network breach is unstoppable or it has has already occurred. Therefore, trust is never granted based on network location and every request on the system or network must be treated as a potential threat. 

8. Describe the concept, "Zero trust is a philosophy, not a product".

It means zero trust is not a product you can buy from market, rather it means a set of policies and strategies that can set on network ends to protect it. If a organization needs to apply Zero Trust, they have to apply them through applying some policies and parameters. It can be done many ways such as Identity check, Endpoint security and analytics. 

9. What are next generation firewalls? How do they help us implement zero trust? Describe in detail.

Next-Generation Firewalls are advanced firewalls that integrate capabilities beyond the traditional port/blocking protocols. They help us to implement zero trust by identifying and controlling traffic based on the application. It also ties traffic to a specific user, not only IP address. 

10. What is logical segmentation? How can it add to zero trust?

Logical segmentation is the process of dividing a network into separate logical segments. It helps to control traffic flow between them. It creates security boundaries within the network. It adds to Zero Trust by reducing the attack surface. If an attacker compromises a device in the guest Wi-Fi segment, logical segmentation can prevent them from easily pivoting to the sensitive finance segment.

11. What is micro segmentation? How can it add to zero trust?

Micro-segmentation is a more granular form of network segmentation applied at the workload level. It allows for security policies to be defined for each individual workload. It is a core technical implementation of Zero Trust. It enforces least privileges by ensuring that a web server can only communicate with its specific application server and database. So that attackers can not take the advantages on these ports. 

12. Describe the process of vulnerability management.

Vulnerability Management is a continuous and active cycle that can identify, classify and mitigate software vulnerabilities. The process is:
Discover: Catalog all assets in the environment.
Assess: Scan assets to identify vulnerabilities.
Prioritize:  Rank vulnerabilities based on severity, exploit availability, and asset criticality.
Remediate: Apply patches, configuration changes, or other fixes.
Verify: Confirm that the remediation was successful.
Report: Document the process and metrics for improvement.

13. What activities should we think about before we can consider applying patches?

Before applying patches we must:

Test: pply the patch in a non-production environment. It ensures that it does not cause system or break applications. 
Assess Criticality: Determine if the vulnerability is being actively exploited and how severe it is to prioritize the patch. 
plan: We will schedule the deployment during a maintenance window to minimize business disruption.
Have a Rollback Plan: Prepare a procedure to quickly revert the patch if it causes unforeseen issues. 

14. Describe SBOMs? What role does an SBOM play in zero trust.

A Software Bill of Materials is a nested inventory, a formal record of all details and relationships with its supply chain concerning the various components used in building software. It's rather like an ingredient list for an application.
In Zero Trust, which "assumes breach," an SBOM is critical for rapid response. If a new vulnerability is found in one of these common open-source libraries-say, Log4j-the organization that has SBOMs would immediately learn which applications they have that include the vulnerable library and can rapidly patch or isolate the vulnerable systems, thus sustaining a robust security posture.

15. What is meant by the term "supply chain attack?" (outside reading may be required)

In a supply chain attack, an attacker gains entry into a system by exploiting some weak link in the supply chain-for example, through some third-party vendor, software library, or open-source component. The attackers will compromise one of the trusted partners instead of attacking the final target themselves. An attack on SolarWinds is a very good example in which the attackers injected malicious code into a routine software update.

16. How does the use of open source software affect zero trust? How big is this issue?

Open Source Software introduces a supply chain risk in that its components and dependencies often are brought in without full visibility into their security-a possible contradiction with Zero Trust's explicit need for verification of all assets.
This is a huge problem. Modern applications are typically 80-90% open-source components. A vulnerability in a single, highly-used OSS library can affect thousands of organisations across the world, as witnessed with the Log4Shell vulnerability.

17. What is the TPS metaphor? Where does it break down?

The TPS metaphor likens a TPM to a "notary public" for your computer. It provides a hardware-based root of trust to verify the integrity of the system's boot process and software state.It breaks down because, while a TPM can verify that the system started in a known good state, it cannot guarantee what happens after boot. Malware could still run in memory, or a user with valid credentials could be acting maliciously. It's a component of trust, not a guarantee.

18. What is SPDX?

SPDX (Software Package Data Exchange) is an open standard format for communicating SBOM information, including components, licenses, copyrights, and security references. It ensures communication and connection between different tools and organizations.

19. What is SWID?

SWID (Software Identification) tags are XML files that provide a unique identifier for a specific installed software product. They help in accurately identifying software assets, which is eventually a foundational step for creating SBOMs and vulnerability management. 

20. Why are SBOMs now being widely adopted?

SBOMs are now widely adopted for many reason. The US government mandated SBOMs for federal software suppliers. Also the components of security tools and and open-source tools make it a necessity for risk management. 

15. What is CVSS?

The Common Vulnerability Scoring System (CVSS) is an open framework for communicating the characteristics and severity of software vulnerabilities. It provides a numerical score (0-10) representing the severity of a vulnerability. 

15. What is VEX?

VEX (Vulnerability Exploitability Exchange) is a companion document to an SBOM. This prevents vulnerability fatigue by helping consumers focus on the vulnerabilities that are actually exploitable in their specific environment.

23. From the author's point of view, what is the bottom line if we are to reduce the risk of supply chain attacks?

The bottom line is that organizations must have visibility and most importantly control over their software supply chain. This requires taking steps on all vendors, actively managing vulnerabilities and understanding the provenance of every component iin their environment. Not-trusting every network system and protect all the threats are the core concept and viewpoint of the author. 

###### Part 2 - IAM

1. What is identity?
Identify is the unique set of attributes that define a user, system or service within a digital environment. It a new security perimeter in a zero trust model. 

2. What do we mean by the phrase "Access Control"?
Access Control is the process of granting or denying requests to obtain and use information of processing services. It also enforces least privilege principle. 

3. What is IAM?
Identify and Access Management is the security discipline that ensures the right individuals to access the right resources at the right times for the right reasons.  

4. What is LDAP?
The Lightweight Directory Access Protocol (LDAP) is an open, vendor-neutral applicatioln protocol for accessing and maintaining distributed directory information services over an IP network. It is commonly used for user authentication and storing information about users,groups and systems. 

5. Quote:"One of the problems with digital identity and authentication is that our current systems are site-centric". Explain this. How do we solve the problem?
The term "site-centric" describes when every website or service has its own siloed identity system, meaning that users have to create and remember different credentials for each site, creating password fatigue and the bad behavior of password reuse. This is solved with federated identity, where a trusted third party manages authentication, normally an Identity Provider, and the user has to prove their identity once to the IdP, which in turn vouches for them to the different services they need, called Service Providers, using standards such as SAML or OIDC.

6. What is federation, in terms of IAM?
Federation is a process that allows for the portability of identify information across different security domains. It enables users from one domain to access resources in another domain. 

7. What are the seven characteristics a modern identity system should have?
 The seven characteristics a modern identity system should have are:
a. Distributed and Federated.
b. Privacy-Enhancing.
c. Interoperable.
d. Scalable
e. Security and Resilient
f. Usable
g. Consent-Based and Transparent
 
8. According to the author, what is the bottom line here?
The bottom line is that identify is the cornerstone of modern security, especially for zero trust. Without a strong, modern IAM foundation and Zero Trust principles, it is impossible to ensure secure environment. 

9. What information do you need before you can reliably restrict access on a need-to-know basis?
I need various things to reliably restrict access on a need-to-know basis. First, I will look for Data Classification. It will show what data is sensitive and where does it reside. Then I will look for User Roles and Responsibilities which will show what each user's job function. I will also look Business Processes and see what data does a user need to perform their specific tasks.

10. Describe the Cozy Bear supply chain attack on Solar winds.
The Cozy Bear (APT29) attack on SolarWinds was a sophisticated supply chain attack. Threat actors infiltered SolarWinds' network and inserted malicious code and file into the Orion platform's legitimate software updates.

11. How does Gartner describe IAM? How does NIST describe it?
Gartner:  Focuses on IAM as a business enabler that "enables the right individuals to access the right resources at the right times for the right reasons."

NIST: Takes a more technical, standards-based approach, defining IAM in the context of frameworks like Digital Identity Guidelines (SP 800-63) and the Zero Trust Architecture (SP 800-207).

12. Name and describe the 3 parts of IAM.
a. Identification: The act of claiming an identify. (eg. Providing a username).
b. Authentication: The process of verifying that claimed identify. 
c. Authorization: The process of determining what an authentication identify is allowed to do. 

13. Why is it important to secure IAM?
IAM systems are the keys to the kingdom. If compromised, an attacker can grant themselves access to any resources the IAM system controls. A breach can take control the entire security infrastructure. 

14. Describe SSO.
Single Sign-On (SSO) is an authentication scheme that allows a user to log in with a single set of credentials to multiple independent software systems. It works through a central Identity Provider (IdP) that authenticates the user and then provides a token to other applications.

15. Describe the OAuth process. In what environment is OAuth primarily used?
OAuth 2.0 is an authorization framework rather than an authentication protocol, because a user can grant a third-party application limited access to their resources without sharing credentials with it.
Process: The application redirects the user to the resource owner for example, Google. A user authenticates at the resource owner and consents to the access. The resource owner issues a limited-access token to the application.
Primary Use: It is primarily used for API authorization and consumer-facing web/mobile applications, such as "Sign in with Google/Facebook".

16. Describe the SAML process In what environment is SAML primarily used?
SAML, or Security Assertion Markup Language, is an XML-based standard for exchanging authentication and authorization data between the Identity Provider and the Service Provider.
Process: A user attempts to access an SP. The SP redirects the user to the IdP. In turn, the user authenticates at the IdP. The IdP generates a SAML assertion-a signed XML document-and returns it to the SP, which grants access.
Primary Use: It's mainly used for enterprise-level single sign-on to provide seamless access to internal applications like Salesforce, Workday, etc.

17. What is two-factor Authentication? What is MFA?
Two-Factor Authentication: It is a way of authentication that requires two exact different types of factors to authentication. 
Multi-Factor Authentication: A security system that requires more than one distinct authentication factor to login in the system and application. 

18. Describe the types of Two-Factor Authentication.
There are many types of Two-Factor Authentication. The basic one is something that I know. It can be a password or pin. The we can use smart card, security key to authenticate in the system. lastly, we can use Biometric (fingerprint, facial recognition).

19. Rank these types according to their security.. Justify each ranking by explaining why.you gave it that ranking.
We can rank these types according to their security by following:
Something you are (Biometrics) + Something you have (Hardware Key): Most secure. Requires physical possession of a device and a unique biological trait; very difficult to phish or replicate.

Something you have: Hardware Key + Something you know: Password. Highly secure, resists phishing and remote attacks. The physical key has to be stolen.

Something you have Software Token + Something you know Password: Secure. It's better than passwords alone but vulnerable to phishing in cases where the user manually enters the code, or to device cloning.

Password: Something you know only-the least secure. It can be phished, brute-forced, or reused.

20. What is software-defined perimeter?
SDP is a cybersecurity framework that builds dynamic, individual network perimeters around particular resources. Infrastructure should be hidden from the internet, or as some experts put it, kept in a "black cloud," and users and devices should be authenticated and authorized to have access to an application or network segment. It is one of the enabling technologies for Zero Trust Network Access.

21. Explain the use of traditional firewalls and VPNs, why they fail, and compare them.
Traditional Firewalls/VPNs: Firewalls build a static perimeter, and VPNs provide users with complete access to the internal network once they authenticate. They implement a "connect first, authenticate later" model.

Why they fail: They trust anyone inside the network, providing ample opportunities for lateral movement by attackers. VPNs also expose the entire network to compromised devices.

Compared to SDP, it reverses the model to "authenticate first, connect later." It offers granular, one-to-one connections to specific applications, not the whole network, which perfectly meets Zero Trust principles.

22. Explain de-perimeterization. How does it add to zero trust.
De-perimeterization refers to the breaking down of the traditional network perimeter because of the cloud, mobility, and working remotely. For this reason, security can no longer depend on a single well-guarded border.
This is where the very idea of Zero Trust comes from. Zero Trust embraces de-perimeterization, shifting the focus of security from the edge of the network to individual identities and resources by creating many micro-perimeters.

23. What was Operation Aurora, and how did Google respond to it?
Operation Aurora was a sophisticated 2009 cyber attack emanating from China that targeted Google and dozens of other companies. It used a zero-day Internet Explorer vulnerability to access the target's corporate system and intellectual property.
This attack was one of the factors that catalyzed Google to develop and implement BeyondCorp, its landmark Zero Trust architecture. BeyondCorp shifted access controls from the network perimeter to individual devices and users, allowing access based on dynamic assessments of trust, irrespective of network location.

24. Explain why SDPis effective in increasing zero trust.
SDP is effective because it operationalizes core Zero Trust principles:

Verify Explicitly: Before any connection is established, it requires strong authentication and device health checks.

Assume Breach: Hides resources and provides least privilege access 1:1 app access to reduce lateral movement that an attacker could achieve.

Micro-segmentation: It creates an individual, encrypted tunnel for each user-to-application session.

25. Why isn't SDP in common use?
SDP is not commonly used because of it's complexity. It can be very complex to implement in legacy or on-premise environments. Some older applications cannot easily be integrated into a modern SDP framework. It is also represent traditional network security models. 

26. Why do zero trust initiatives fail?
Zero Trust fail due to many reasons. It often fails when it is being used as product, not a strategy. Lack of clear vision and real understanding meaning of Zero Trust are also the reasons to lead failure. Moreover, poor communication and change management can be the reason of initiatives. 

27. What is "technical debt"?
Technical debt is the implied cost and future rework created by deciding to implement an easy, limited, or quick technical solution now instead of using a better approach that would take longer. In security, it's the accumulation of outdated systems, unpatched software, and legacy architectures that make the implementation of modern frameworks like Zero Trust hard and expensive.

28. Where in the business hierarchy of a company should access policies be SET?
Access policies should be defined by the owners of the business and data owners, not just the IT department. IT's role is to implement and enforce these business-driven policies.

29. What does the author typically bring up when new technology is being considered?
The author typically asks, "What problem are we trying to solve?" This ensures that technology is not adopted for its own sake but is aligned with a specific business need or security goal.

30. Describe the teamwork required to implement zero trust solutions in an organization, as described by the author.
Implementing Zero Trust requires a cross-functional team:

- Executive Leadership: To sponsor the initiative and align it with business goals.
- Security Team: To design the architecture and policies.
- IT Team: To implement and manage the technical controls.
- Application Developers: To ensure applications are compatible with ZT principles (e.g., using standard authentication protocols).
- Human Resources: To help manage the identity lifecycle (onboarding, role changes, offboarding).
- End Users: To provide feedback and adopt new processes.



###### Conclusion

1. How should we think of zero trust?
It is best to think of Zero Trust as a guiding philosophy and a strategic framework for securing modern digital enterprises. It's a journey, not a destination. It requires continuous improvement and a mindset shift from "trust but verify" to "never trust, always verify."

2. What are Kindervag's nine rules of zero trust?
Kindervag's nine rules of zero trust are:
 - Focus on business outcomes. 
 - Design from the inside out.  
 - Determine who/what needs access. 
 - Inspect and log all traffic
 - Define the protect surface.
 - Map the transaction flows.
 - Architect a Zero Trust environment.
 - Create Zero Trust policies.
 - Monitor and maintain.

3. List the tactics that will have the most impact.

The tactics that will have the most impact are:

Begin with a robust IAM foundation consisting of MFA and SSO.

Implement micro-segmentation to control East-West traffic and limit lateral movement.

Adopt a ZTNA/SDP solution to replace or complement traditional VPNs.

Visibility is key to asset management, SBOMs, and continuous monitoring.

Focus on the "Protect Surface", rather than the whole "Attack Surface."

Adopt automation for vulnerability management, policy enforcement, and threat response.