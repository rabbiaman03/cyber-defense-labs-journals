# Learning Journal 2 — Anatomy of Attacks

Question 1: 

The IEEE Computer Society article explains that Lockheed Martin created the cyber kill chain to help security teams understand and interfere with cyber‑attacks. The term kill chain came from the military concept of interfering with an attack's chain, and the cyber counterpart maps out the steps of an intrusion so that defenders could interfere with them. The article lists seven steps:

Reconnaissance: attackers try to learn about the target (harvest email, test defenses)
Weaponization: malware is crafted from exploiting vulnerabilities; attackers tailor malware and try evasion.
Delivery: weapon is transported by phishing emails, websites or removable media; this is a key juncture where defenders can stop the attack.
Exploitation: malicious code executes and the perimeter is broken; attackers install tools or modify certificates.
Installation: backdoors or remote-access Trojans (RATs) are installed to allow sustained access.
Command & Control: attackers communicate with compromised systems, attempt to acquire privileged accounts and conduct brute‑force attacks.
Actions on Objective: attackers steal or encrypt data and achieve their objective.
The article emphasizes that these stages are not a mere descriptive model; they correspond to security controls. All the stages can be countered through detection, denial, disruption, degradation, deception or containment. For example:

During the reconnaissance stage, web and network intrusion-detection tools can detect scanning, and firewall access control lists can restrict access.

During delivery, endpoint malware defense must detect malicious payloads, and application whitelisting and proxy filters may block them; inline anti-virus software can intercept delivery.


During the installation stage, host-based intrusion detection and strong passwords/privilege separation can detect or block backdoor installation.

When attackers attempt command & control, segmentation and firewalls can slow or stop communications.

To address objective/action on exfiltration, data‑loss prevention appliances and egress filtering help detect and prevent data robbery.

Aside from rolling out controls, the article encourages using cyber‑attack simulation platforms to test defenses on a periodic basis. Simulation platforms enable firms to simulate attacks with lifelike behavior across multiple vectors, validate controls' effectiveness, and remediate vulnerabilities—interrupting the kill chain at many points
computer. Continuous validation seals the window of vulnerability and strengthens response to incidents.







Question2:

Dark Reading's article argues that while the kill chain is appealing, it is seriously flawed. The model puts a strong focus on intrusion, i.e., infiltrating the network, and lists seven steps (reconnaissance, weaponization, delivery, exploitation, installation, command & control and actions on objectives).
. The article observes, however, that steps 1–6 are solely focused on intrusion, whereas step 7 ("action on objectives") encompasses months of activity wherein attackers achieve their true goals.
This creates two main pitfalls:
Perimeter‑centric bias: the kill chain reinforces "old‑school, perimeter‑focused, malware‑prevention thinking," leading organizations to over‑invest in preventing initial intrusion and under‑invest in detecting attackers already inside.
The article continues that sophisticated attackers will eventually bypass perimeter defenses, so relying solely on firewalls, sandboxes and antivirus leaves networks vulnerable once those controls are bypassed.
Irrelevant or narrow steps: steps 1–3 occur outside of the defender's network (the attacker's reconnaissance, weaponization and delivery), and thus defenders cannot directly influence them.
The model is also malware‑centric and does not address other threat vectors such as insider threats, social‑engineering or intrusion via remote access (which may not involve malware).
This nearsighted focus on detail makes the model blind to "infinite space between steps 6 and 7," where attackers operate covertly and are undetectable to kill‑chain‑focused defenses.
Dark Reading concludes that over‑focus on the kill chain can be a bad thing because it diverts attention from how to uncover attacks that are already underway. The authors endorse the deployment of breach‑detection systems that track user and computer behavioral drift to detect attackers who have already crossed the perimeter.
That is, step 7—what the attackers do on objectives—is more important than the earlier kill‑chain steps.






Question3:

Black Hills Information Security's "Zero to Hero Attack" webcast demonstrates how an attacker can progress from zero initial access to domain administrator. The slides outline each step, the privileges required, the escalation in each step and the goal.

1. Reconnaissance

Context & Privileges: The attacker has no internal access. Through the use of external recon tools—recon‑ng, theHarvester, InSpy, Burp, DNSDumpster, DNS UltraTools and MXToolbox—the attackers scrape publicly available data such as corporate profile data, user email addresses and domain info blackhillsinfosec.com. They use metadata tools and credential-harvesting to build a list of 212 user accounts and identify externally facing services like Outlook Web Access (OWA) and OpenVPN portals blackhillsinfosec.com. These activities do not require any privilege at all; the attacker simply employs OSINT.

Objective: Discovery of potential usernames and services to attack later. Here no privilege escalation is performed.

2. Scanning & Enumeration

Environment & Privileges: After the attacker has acquired credentials (refer gaining‑access phase), they utilize network scanner tools to scan the internal network. They traverse the VPN and perform live host discovery and service enumeration with nmap. They display Windows and Linux hosts and services such as SSH and SMB, identify a domain controller, SMB services and web server.They also run custom nmap scripts to probe SMB signing and enumerated network topology.

Objective: Establish a topology of hosts and live services to enumerate vulnerable points. This requires a legitimate VPN user (obtained via credential harvesting), hence transitioning from external to internal network compromise.

3. Gaining Access – Password Spraying & OWA Enumeration

Context & Privileges: The SprayingToolkit is used by the attacker to perform a password spray against OWA portal. They run python3 atomizer.py owa mail.r‑1x.com 'Dakota2019!' ~/users.txt to attempt a single password ("Dakota2019!") across all found user accounts blackhillsinfosec.com.
Valid credentials are found, giving them an authenticated OWA session blackhillsinfosec.com.
Using MailSniper's Invoke‑PasswordSprayOWA module, they spray once more and capture more. They then invoke Get‑GlobalAddressList to scan the entire address book, obtaining 214 user accounts.
Privilege: After attackers obtain legitimate credentials, they are normal domain users. They do not possess high privilege yet but gain permission to access corporate email and extract contact details.

Objective: Obtain legitimate credentials and scan all user accounts for further attacks.

4. Lateral Movement – OWA & VPN Access

Context & Privileges: The attacker exploits their credentials to log onto OWA in order to read users' emails and then the same credentials to log onto the OpenVPN web portal blackhillsinfosec.com. After accessing via VPN, they create internal network access and are able to access internal servers. They then perform network discovery using nmap to find live hosts, services and an unused SSH server blackhillsinfosec.com.

Objective: Move from first email access to additional internal network access. This stage elevates the attacker's privilege from an external user to an internal network user (by using VPN). No admin privilege yet.

5. Internal Host Compromise – SSH Brute Force & SMB Weaknesses

Background & Privileges: In scanning, the attacker comes across an internal Kali server that has SSH open. They run nmap's ssh-brute script with user and password lists for brute-forcing SSH credentials.
. A weak password is found, providing access to an internal pivot host (internal Kali server).
. Next, they check SMB security using nmap --script=smb2-security-mode and find that SMB signing is disabled, leaving the system vulnerable to NTLM relay attacks.

Goal: Create a presence in the network and identify weaknesses. By brute-forcing SSH, the attacker moves from VPN user to local admin on a pivot server. Discovering SMB signing off sets the scene for the next attack.

6. Credential Harvesting – LLMNR/Responder & ntlmrelayx

Context & Privileges: When SMB signing is disabled, the attacker uses Responder and ntlmrelayx to exploit Link‑Local Multicast Name Resolution (LLMNR) and NetBIOS Name Service. They run python Responder.py -I eth0 -A and python ntlmrelayx.py -tf targets -smb2support.
. These tools answer LLMNR requests and send captured NTLM hashes to SMB shares. As SMB signing is turned off, the hashes can be sent to gain local administrator rights on most hosts. The attackers steal local admin hashes and gain local administrator rights.

Goal: Local standard user privilege escalation to local administrator on most hosts, harvesting hashes to use later. This provides privilege escalation domain-wide.

7. Lateral Movement & Privilege Escalation – crackmapexec

Context & Privileges: The attacker, using the harvested hashes, runs crackmapexec across the SMB network: crackmapexec smb 10.55.100.0/23 -u LA‑ITAdmin -H <hash> --local and --lsa.
. This allows them to authenticate to hosts with the stolen hash and dump more credentials (LSA secrets). At some point they obtain a domain administrator hash, giving them domain‑wide administrative privileges.
. With this, they can query domain groups, dump hashes and fully own the domain blackhillsinfosec.com.

Goal: Get domain administrator access. This is a serious escalation—from local admin on a few hosts to full domain admin control.

8. Post‑Exploitation & Pillage – GoPhish & Cobalt Strike

Context & Privileges: To gain more control and maintain, the attacker starts a GoPhish attack. They create a phishing message for "free greenhouse coupons" and send it via SendGrid to all 212 users.
. The email also points to a landing page with an HTA file that drops a Cobalt Strike Beacon. When executed, the beacon reports back to the attacker, giving them interactive command‑and‑control sessions. Using Cobalt Strike they run commands like Mimikatz, Hashdump, shell net group "domain admins" /domain and psexec_psh against domain controllers.

Objective: Cred-environmentize more, change to domain controllers, dump all the stuff that is of interest and utterly loot the environment. At this point, the attacker is completely privileged and achieves the "zero‑to‑hero" level.





Question 4: 

The "Group Policies That Kill Kill Chains" slides (used in the following "Quest for the Kill Chain Killer Continues" webcast) recommend hardening Active Directory to disrupt kill‑chain phases. Key methods include:

Enforce prerequisite security practices: principle of least privilege, network partition, centralized logging, strong password policies and multifactor VPN access.

Manage AD groups and organizational units properly: structure well‑defined groups, even nested groups, and precisely know who is in what 
. Use small, targeted group-policy objects (GPOs), prevent inheritance and loopback, and target policies toward either computers or users—not both—to reduce complexity.

Rename or replace local admin accounts and use LAPS: rename the default local admin or make a honey account, and install the Local Administrator Password Solution (LAPS) to centrally manage local admin passwords safely.LAPS updates local admin passwords and stores them in Active Directory, but admins need to restrict access to the clear-text password in the schema.

Control local admin group membership: apply Restricted Groups or Local Users and Groups policy to include only authorized accounts as members of the Administrators group and remove all unauthorized members.

Disable LLMNR and related protocols: apply following GPO under Computer Configuration -> Administrative Templates -> Network -> DNS Client and enable Turn off multicast name resolution. This shuts down the exploitation of LLMNR/NetBIOS name resolution and hash-harvesting attacks.

Enable SMB message signing: Microsoft network server: Digitally sign communications (always) must be set to Enabled. SMB signing shuts down NTLM relay attacks such as those launched in the Zero-to-Hero attack.

Turn on host-based firewalls: turn on the Windows Defender firewall for servers and workstations and activate fine-grained rules blackhillsinfosec.com. Workstations should not be allowed to communicate directly with one another.

Restrict network logons: use User Rights Assignment to limit which accounts can log onto what systems blackhillsinfosec.com. Service accounts should not have unnecessary remote desktop privileges; this inhibits lateral movement.

Set system web proxies and disable WPAD: set enforce proxy settings and disable auto-discovery of proxies to prevent proxy hijacking configuration by attackers.

Enable full auditing and logging: run auditpol.exe /set /Category:* /success:enable /failure:enable to enable comprehensive auditing and force subcategory auditing to override simple settings.
Audit Kerberos ticket actions (credential verification, authentication service and service ticket operations) to detect kerberoasting.

Enable PowerShell and CMD transcription: allow PowerShell transcription, script block logging, module logging and restrict script execution to signed scripts. These controls record attacker commands and assist with detection.

Install Sysmon and Windows Event Forwarding (WEF): Sysmon provides enhanced event logging and can be deployed via GPO. Event logs need to be forwarded to a central collection point for monitoring.

These moves together strengthen Active Directory, limit privilege escalation attack vectors and create logs for early detection, thereby "killing" the kill chain.





Question 5:

CrowdStrike's blog "Skeletons in the IT Closet" refers to seven misconfigurations that attackers often attack. In each misconfiguration, there is an explanation of the vulnerability and solution.

Misconfiguration Vulnerability Exposed & Adversary Abuse\tMitigation (IT Action Items)
1. Administrative Privileges
The Domain Users group sometimes inherits administrative rights on computer objects. All domain users belong to Domain Users, so all users can have admin rights on some systems. Attackers that are able to breach a user account can lateral move to systems where the user (as Domain Users) has admin rights and harvest credentials. Limit administrative rights to a privileged set of users and remove Domain Users from local admin groups. Use BloodHound to check AD relationships and find unauthorized admin privileges
2. Network Shares
Unmapped network shares can allow a standard user to write to an IIS web root and upload a web shell or read confidential information. Attackers can then gain code execution as the service account or obtain confidential information. All network shares need to be discovered with tools like SharpShares; RBAC and ACLs need to be enforced to restrict read/write access. 
3. Weak Passwords on Service Accounts
Service accounts often have administrative privileges on multiple hosts and use weak passwords. Attackers utilize kerberoasting to ask for service tickets on service principal name (SPN) accounts and then crack the tickets to obtain plaintext passwords.
Use strong passwords and implement advanced encryption (e.g., AES) for Kerberos tickets.
Use BloodHound to find privileged service accounts and restrict their privileges.
4. Services Running on Hosts with Multiple Admins:
When services run under the domain user account, the password resides in the LSA secrets registry hive. Any local administrator on such a machine can obtain the plaintext password with tools like secretsdump.py. When there are numerous users with local admin privileges on a "jumpbox," breaching any one of them means an attacker is able to extract the service account password and use that to breach other hosts. Check running services and implement least privilege—service accounts should not have overly permissive privileges. Limit local admin users and don't share "jumpbox" hosts with more than one admin.
5. Aged Accounts:
Accounts that are not expired (stale or aged accounts) provide long-term persistence. Attackers like these types of accounts because the passwords typically don't change. Check AD to find out which accounts violate the password-expiration policy and stale accounts. Transition administrative accounts to a privileged access management (PAM) solution and have passwords expire rapidly (e.g., 90 minutes).
6. Passwords, Passwords, Passwords
    The blog identifies three sub‑issues:
a. Plaintext Passwords: because of password rotation service bugs, the userPassword attribute or description field might hold plaintext or encoded passwords.
    b. Weak Passwords & Inadequate Lockout: hackers do password spraying to guess weak passwords; inadequate lockout limits enable multiple attempts.
c. Password Reuse: if the same RID 500 local admin password is reused in many hosts, the attacker can obtain one NTLM hash and then use it to traverse laterally using tools like CrackMapExec.
    a. Plaintext: block all plaintext passwords from being stored in AD attributes.
 b. Weak/Lockout: implement good password policies and appropriate lockout thresholds; identify multiple logons from a single host (which is characteristic of password spraying).
c. Reuse: deploy LAPS to generate random local admin passwords and rotate them automatically. Detect local authentication attempts to multiple hosts from one host.
7. Legacy Systems
Aged systems (e.g., Windows 2003) still exist in networks because of business dependencies. These systems are vulnerable to EternalBlue (MS17‑010) or BlueKeep exploits, which allow attackers to execute code as SYSTEM.






Question6:

Black Hills Information Security’s blog explains that Link‑Local Multicast Name Resolution (LLMNR) allows hosts to resolve names on a local network without a DNS server. The protocol broadcasts a query to the local subnet and trusts the first response received. Attackers can exploit this by configuring a rogue host to reply authoritatively to any query (“I’mEveryoneNotReally”), causing clients to believe the rogue host is the intended server. When Windows then attempts to connect to the file server, it will send the user's credential hash to the attacker's host, which can steal the hash or pass it along to the real server and remain undetected. Because legitimate DNS is typically available, LLMNR is largely unnecessary in modern times. Disabling it removes a large attack vector.

A few methods for disabling LLMNR are outlined in the blog:

Active Directory Group Policy: edit or create a GPO; go to Computer Configuration → Administrative Templates → Network → DNS Client and enable Turn off multicast name resolution.

Local Group Policy: on an individual workstation (Windows 7/8/10 Pro) execute gpedit.msc and enable the same policy under DNS Client.
Command Line: for Home versions, add registry entries to HKLM\Software\policies\Microsoft\Windows NT\DNSClient and set EnableMulticast to 0.
Linux (Ubuntu): modify /etc/systemd/resolved.conf and change LLMNR=yes to LLMNR=no, then reboot.
The author notes that LLMNR is a legacy protocol and companies should test the impact of disabling it, but in most environments it's a sound security practice.