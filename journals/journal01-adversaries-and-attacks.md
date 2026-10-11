# Learning Journal 1 — Understanding Adversaries and Attacks

##### Part 1: Ethics and law

1. Hacking is legal only when it is performed ethically, with explicit permission. Hacking with maintaining laws and regulations is also called ethical hacking. 

##### **Part 2: The Metasploit Framework**

1. The Metasploit Framework (MSF) is a widely used penetration testing and exploitation framework. It provides tools for protecting platforms from various exploits. It helps penetration testers, security professionals, and hackers to find the vulnerabilities in a network or system. 
2. Msfcli is a command-line interface (CLI) for the Metasploit Framework. It allows to execute metasploit modules directly from command line without using many interfaces. It is a very helpful for quick attacks without any graphical interface. 
3. Msfconsole is the interactive command-line interface of the Metasploit Framework. It allows users to access and configure modules, exploits, payloads, and settings. It also provides a range of functionalities for conducting penetration tests. 
4. Metasploit uses a PostgreSQL database to store data. It helps to store hosts, services, vulnerabilities. It also helps in tracking testing results.
5. Meterpreter is an advanced payload within the Metasploit Framework that provides an interactive shell for remote exploitation. It helps hackers to manipulate systems and gain access and information. It works on a secure communication channel, which gives hackers significant control over the target system. 
6. msfvenom is a tool within Metasploit which is used for generating custom playloads. These playloads can be used in exploits and providing methods for attackers to gain access to target systems. 
7. Vulnerability: A weakness in a system or application that can be exploited by an attacker.

   Exploit: It can be anything that takes advantage of a vulnerability in a system to gain unauthorized access in a system.
   
   Playload: Playload is a piece of code that can be executed after a attack successfully compromises a system. It can perform tasks like opening a backdoor or escalating privileges.
    
   shell: A command-line interface that allows an attacker to interact with a compromised system. 

  8. Five advantages of using the Metasploit Framework:
- Industry accepted tool for testing on vulnerabilities and exploits. 
- Simplifies complex tasks.
- Myriad set of capabilities ordered in a systematic manner.
- Consistent updates. 
- Contains many different types of modules.

9. Seven ranks of exploits in the Metasploit Framework

- Excellent: The exploit works perfectly on most systems and requires little to no customization. This is the case for SQL injection, CMD execution etc.
- Great: The exploit has in-built target or they detect the target automatically. It can also use application-specific return address. 
- Good: It has a solid functionality and it is the common case for software like Windows 7 or 12. 
- Normal: Requires significant modification and may not always work.
- Average: May work intermittently depending on system configuration.
- Low: Unreliable or outdated exploits.
- Manual: Exploits that do not work or are under development.

10. Metasploit should only be used in controlled environments such as test labs, bug bounty programs, or CTFs. Unauthorized use of Metasploit can lead to legal consequences, damage to systems, and unintentional exposure of sensitive data. It is crucial to only run it on systems that you have explicit permission to attack.

11. I can see descriptions, targeted vulnerabilities, required payloads, options, and exploit effectiveness for each exploit. This data helps me understand how and when to use the exploit in a testing scenario.

12. The "show options" command displays all the configurable options for the selected exploit. It includes things like target IP address, port number, payload type, and other settings that need to be configured before running the exploit.

13. Payloads in Metasploit come in various types, such as reverse shells, bind shells, Meterpreter, command shells, and staged or non-staged payloads. Each type has a different way of interacting with the target system.

14. During post-exploitation, attackers typically gather information about the system, escalate privileges, maintain persistence, and exfiltrate data. It's the phase after gaining access, and actions vary depending on the attacker's goal (e.g., information gathering, persistence, data extraction).

15. Auxiliary modules are tools used in Metasploit for tasks like scanning, brute-forcing, and DoS (Denial of Service) attacks. These modules don’t necessarily require exploits and can be used for information gathering, vulnerability scanning, and network reconnaissance.

16. The "show" command in Metasploit is used to display various types of information like available exploits, payloads, or options. For example, show exploits lists all the available exploits in the framework.

17. e. The selected exploit in the video targets a Windows vulnerability. It allows the attacker to gain unauthorized access.
   f. The payload used in the video is typically a reverse shell or Meterpreter. 


##### Part 2 - Understanding Adversaries and Attacks


1. The 4 points typically highlight:

- **The nature of the adversary**: This addresses who the potential attackers are and the different motivations behind their actions.
    
- **The context of security**: Discusses how security should be approached within the scope of adversaries' capabilities.
    
- **Adversary profiling**: Understanding the profiles, motivations, and capabilities of the attackers.
    
- **The importance of context in security design**: Recognizing that the threat landscape is dynamic and requires adaptable security strategies.

2. - **Cyber Criminals**: Individuals or groups motivated by financial gain. Example: A hacker exploiting a vulnerability for credit card fraud.
    
- **Hacktivists**: Attackers with political motives, aiming to promote a cause. Example: Anonymous targeting government websites to protest.
    
- **Nation-State Actors**: Governments or affiliated organizations conducting cyber operations for espionage, military, or intelligence purposes. Example: Russian cyberattacks targeting other countries' political systems.
    
- **Insiders**: Employees or trusted individuals who misuse their access for malicious purposes. Example: A disgruntled employee leaking confidential company data.

3. - **Edward Snowden**: A former NSA contractor who leaked classified information about government surveillance programs, revealing the extent of global surveillance efforts.
    
- **Google's issue**: Google faced pressure from governments and spy agencies to comply with surveillance demands, which led to a conflict between privacy and government authority, especially with respect to user data and encryption.

4. The EU was annoyed by the excessive surveillance by the US government, particularly after revelations from Snowden. The EU was concerned about privacy violations and the lack of control over its citizens' data, prompting the General Data Protection Regulation (GDPR) to safeguard personal information.

5.  The Crypto Wars refer to the ongoing battle over encryption and privacy. Governments, particularly the US, have sought backdoors into encrypted communications for national security purposes, while tech companies resist such attempts, fearing the erosion of user privacy.

6. -  The Five Eyes is an intelligence alliance comprising the US, UK, Canada, Australia, and New Zealand. These countries share intelligence, particularly related to signals intelligence (SIGINT).
    
- 5 points raised may include their surveillance capabilities, global intelligence sharing, privacy concerns, impact on citizens' rights, and the role of tech companies in cooperating with intelligence agencies.

7. Ross Anderson discusses how China is heavily involved in cyber-espionage and intelligence operations. He mentions:

- Dalai Lama: China’s efforts to control or surveil communications around the Dalai Lama, a prominent figure in Tibetan independence movements.
    
- Google: Google’s interactions with the Chinese government, including censorship of search results to comply with China’s laws.
    
- Office of Personnel Management (OPM): Chinese hackers targeted the OPM to steal sensitive information of US federal employees, which led to a massive data breach.
    
- Belt and Road strategy: China’s global infrastructure project, which could also have cybersecurity implications as it extends Chinese influence.
    
- TikTok: Concerns about the data privacy of TikTok, with allegations that it poses a national security threat due to its Chinese ownership.

8. These nations are known for their cyber operations that target other countries for espionage, financial theft, or disruption:
- Russia: Engages in espionage, disinformation campaigns, and cyber-attacks against political and economic targets.
    
- Iran: Known for cyber-attacks against critical infrastructure, especially in the Middle East .
- North Korea: A major actor in cybercrime and financial theft, including the WannaCry ransomware attack.
    
- Cyber warfare: These nations often target their adversaries through digital means.
    
- Political influence: These countries use cyber-attacks to further their political interests.
    
- Impact on global security: Their activities influence global cybersecurity strategies and geopolitics.

9. The SolarWinds hack was a massive supply-chain attack carried out by Russian state-sponsored hackers. They compromised the SolarWinds Orion software, which was used by thousands of organizations worldwide, including US government agencies. This allowed attackers to monitor and manipulate sensitive data undetected for months.

10. - **Access**: How adversaries gain access to systems.
    
- **Control**: Maintaining control of the exploited systems.
    
- **Secrecy**: The degree to which actions remain covert.
    
- **Deception**: Misleading the opponent regarding your actions.
    
- **Damage**: The impact of the attack on the adversary.

11. Bitcoin has become a preferred payment method for cybercriminals, offering anonymity and decentralized transactions. It is commonly used in ransomware attacks, dark web transactions, and to facilitate money laundering activities. 

12. Abuse in cybersecurity includes data breaches, phishing, malware, hacking, privacy violations, and disinformation. These issues lead to unauthorized access to systems, theft of sensitive data, and damage to individuals or organizations. Cybercriminals exploit vulnerabilities to cause harm or gain financial benefit.

13. Mitigation can be achieved through strong authentication like multi-factor authentication (MFA), training users to recognize phishing, and encrypting sensitive data. Access control, continuous monitoring, and having an incident response plan also help prevent and minimize damage. Compliance with cybersecurity laws and regulations further strengthens security defenses.
14. Performative shaming refers to publicly criticizing or condemning individuals or organizations to signal virtue or moral superiority without addressing the underlying issues or providing meaningful solutions.

15. - **Technology**: Improved encryption and security measures.
    
- **Regulation**: Stricter cybersecurity laws and standards.
    
- **Human factors**: Education and awareness to reduce human errors.

16. Stuxnet was a highly sophisticated worm discovered in 2010 that targeted Iran's nuclear enrichment facilities specifically. It crippled the industrial control systems and destroyed the centrifuges, one of the earliest recorded cyberattacks to have physical consequences.

17. Bug discovery is the finding of defects within software. Responsible disclosure is when the vendor is notified and given a time frame in which to fix the bug before publication. Problems with this are timing, trust, and pre-patching exploitation.

18. The Vulnerability Lifecycle is the sequence a vulnerability goes through, beginning with discovery and concluding with patching. This includes discovery, reporting, patch creation, deployment, and public notification.

19. Google Zero policy ensures that the moment a vulnerability is discovered, the vendor is notified and a patch can be expected within **90 days** before going public. This policy is to protect users with enough time allowed for the vendors to fix the issue.

20. CERT window of disclosure is a period which optimally balances giving organizations sufficient time to remediate vulnerabilities before going public. This minimizes the risk of exploitation by giving vendors time to patch vulnerabilities without undue delay.

21. Disclosure is challenging since sellers might be under pressure to silently patch vulnerabilities to prevent public shame. In the Heartbleed example, the OpenSSL vulnerability was serious, and disclosure had to be coordinated closely to prevent large-scale exploitation before a fix could be made.

22. The lesson is to advance responsible disclosure to prevent damage, yet ensure security patches are rolled out in a timely fashion.

23. Meltdown was a hardware vulnerability in Intel and other processors that allowed attackers to read protected memory. It was discovered in 2017 and affected billions of devices worldwide.

24. Coordinated disclosure is when security researchers and vendors work together to responsibly disclose vulnerabilities such that the vulnerability is resolved prior to public disclosure.

25. While zero-day exploits are dangerous, focusing on them in isolation will generate unnecessary hype. Google suggests keeping the big picture in mind with regards to vulnerability context and maintaining well-protected systems, whether zero-day or otherwise.

26. Users have been trained in terrible security practices, poor education, and security convenience by avoiding security features, such as weak passwords or neglecting updates.

27. The hierarchy of tools includes basic tools (e.g., firewalls and antiviruses), advanced tools (e.g., Metasploit and penetration testing suites), and extremely advanced tools (e.g., nation-state level attack tools).

28. Inappropriate storage of sensitive data increases the probability of data breaches. It's extremely important to follow best practices in data encryption, access control, and storage practices.

29. The final summary illustrates the complexity of cybersecurity, the fluidity of threats, and the necessity for ongoing learning and adaptation in order to shield oneself against attack.

30. **Honeypot:**

A honeypot refers to a security term used to define a **decoy network or system** that is designed to lure hackers and become aware of their tactics and methods. It is designed to appear weak and is strategically placed so it would be an easy target for hackers. The purpose of a honeypot is to **capture attackers**, become aware of their behavior, and understand how they exploit vulnerabilities so that defenders can devise better security solutions to protect against similar attacks in the future.

##### Part 3 - Lab 0

1. An inexperienced penetration tester can inadvertently perform unauthorized testing on systems they do not have explicit permission to test, which is illegal. They can also violate privacy laws when they collect or disclose sensitive data, or violate terms of service agreements. One should always have written permission and work within the predefined scope of a penetration test.
2. The Discovery tactic involves techniques used by attackers to gather information about a system, network, or environment to better understand how to exploit vulnerabilities. This may include identifying running services, users, or system configurations. It’s typically done after gaining initial access but before performing the actual attack.
3.  The **Discovery technique** includes techniques that attackers employ to gain more information about a system, network, or environment to determine the best way to exploit vulnerabilities. It may include finding running services, users, or system configurations. It is typically performed after gaining initial access but before attempting the actual attack.

- Detection: Can be detected via IDS/IPS systems or network monitoring tools that alert on unusual or excessive probing activity.
    
- Mitigation: Limit access to ports, use firewalls, and employ rate-limiting or blocking techniques to prevent or reduce scanning.

4. Active scanning can be detected through intrusion detection systems (IDS) or network traffic analysis, which monitor for unusual or unauthorized requests, like port scans or ICMP sweeps.

5. Mitigations include using firewalls to block unnecessary ports, rate-limiting access to sensitive services, and implementing intrusion detection and prevention systems to alert on suspicious scanning activities.

6. The Network Service Discovery technique is used to find active services and their configurations within a network. Attackers use this to identify open ports, running services, and the network topology to find vulnerabilities to exploit.

- Detection: Can be detected by network monitoring tools that log unexpected service discovery or probing attempts.
    
- Mitigation: Limiting exposed services, using network segmentation, and employing firewalls to block unnecessary services.

7. This can be detected using network intrusion detection systems (NIDS), which can flag scans or requests designed to discover open services or ports.

8. Mitigations include disabling unused services, restricting service exposure through firewalls or VPNs, and conducting regular network audits to ensure that only essential services are running and accessible.

9. **Vulnerability Scanning** is the process where attackers scan systems or networks to find known vulnerabilities. This can be done using automated tools that check for common misconfigurations or outdated software that can be exploited.

- **Detection**: Can be detected by monitoring for automated traffic patterns, such as requests to multiple endpoints that match common vulnerability databases.
    
- **Mitigation**: Keep software updated, apply patches regularly, and use vulnerability management tools to identify and fix vulnerabilities before attackers exploit them.

10. It can be detected by monitoring for high-frequency automated scanning patterns, which might resemble activities of vulnerability scanning tools such as Nessus or OpenVAS.

11. Mitigations include regularly applying security patches, running vulnerability management programs, and using IDS/IPS systems to detect and alert on scanning activities.

12. Using **Nmap**, an attacker can retrieve detailed information about your network, including:

- **Open Ports**: Nmap can identify open ports on your devices, exposing available services.
    
- **Service Versions**: It can detect which services are running and their version numbers.
    
- **Operating System**: Nmap can sometimes determine the operating system running on a target machine.
    
- **Firewall/Filtering Information**: Nmap can indicate which ports or services are being blocked by firewalls or other filtering mechanisms.
    
- **Host Discovery**: It can find which hosts are up and responding within a network.