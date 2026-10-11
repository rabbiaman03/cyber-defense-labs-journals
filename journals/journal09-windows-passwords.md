# Learning Journal 9 — Windows Password Security

**Part 0: Windows History and Why Passwords Need to Be Over 14 Characters**
****Passwords should be more than 14 characters because the longer the password, the harder it is for an attacker to crack. The technology behind this is that increasing password length exponentially increases the number of possible combinations, making brute-force attacks more time-consuming and resource-intensive. In addition, modern password policies have moved past simple character combinations to include complexity requirements, further strengthening password security.**

***Part 1: Microsoft Credentials *****

1. **How Passwords are Stored as OWF: In Windows, passwords are stored as an "NT Hash" using the One-Way Function (OWF). This means the password is hashed using a cryptographic algorithm-like MD4-which makes it hard to reverse-engineer. Once hashed, it can't be easily decrypted back into the original password.**

2. **How Passwords are Stored in Active Directory: Passwords in Active Directory are stored in a hashed format, specifically in NTLM hash format, and then mapped to the appropriate user account. These hashes are stored in the AD database and are matched during authentication.**
3. **Password Storage in the Local SAM: The local SAM stores passwords as NTLM hashes. These hashes are stored in the SAM for local accounts, which indirectly requires administrator-level permissions to access it.**
4. **Cached Credentials: These are the credentials cached locally on a computer to enable users to log on even when they cannot connect to the network. The credentials are cached as hashed versions and checked against those on Active Directory once the computer reconnects to the network.**
5. **How Passwords Work in Windows: Passwords in Windows are used for user authentication. When one logs in, the operating system hashes the entered password and compares it against a stored hash. When matched, the user is authenticated for access to the system.**
6. **How Passwords are used by Windows: Windows passwords serve to authenticate users at the operating system level. Once authenticated, the password will grant access to resources and services based on permissions granted to the user in Active Directory or on the local system.**
7. **What Fine-Grained Password Policies Do: Fine-grained password policies applied to Active Directory enable the administrator to apply different kinds of password rules in distinct groups of users, imposing strong password complexities on specific departments or highly privileged users.**

8. **How to Prevent Windows from Storing a LAN Manager Hash: You can prevent Windows from storing the LAN Manager hash of your password in Active Directory or the local SAM database by disabling the storage of LAN Manager hashes via Group Policy or security settings. This secures passwords using stronger encryption methods.**

***Part 2: Kerberos - Kerberoasting***
1. **What is Kerberos? Kerberos is a network authentication protocol designed to provide secure authentication using secret-key cryptography. It allows users and services to securely authenticate each other without transmitting passwords over the network.**
2. **Kerberos Transaction Components: The critical components are the client, the service desired (which could be a file server), the Key Distribution Center, and the Ticket Granting Service. The KDC issues tickets for authentication.**
3. **Who is the Trusted Party? The Kerberos trusted party is the Key Distribution Center, KDC, which provides tickets to validate users and service identities.**
4. **How Does Windows Authenticate If Kerberos is not Available? If it does not find Kerberos, then Windows falls back to NTLM authentication, which is less secure but still functional for local and network logins.**
5. **Three Long Term Keys: The three long-term keys in Kerberos are the user's password hash, the service's password hash, and the KDC's secret key. Using these keys, tickets can be created and users and services can be authenticated in a secure manner.**
6. **Shared Secret in a Windows Domain: This usually refers to the hash form of the password. Both the client and KDC use it for verification purposes when authentication is involved.**
7. **Simplified Authentication Process: The process starts when a client requests a TGT from the KDC. The KDC verifies the identity of the user and responds with the TGT that shall be used to request service tickets from the KDC for any particular service.**
8. **Two Alias Expressions to TGT: Two alias expressions to the server using TGT are "Authentication Server" and "KDC."**
9. **Why Doesn’t the DC Decide Who Has Access? The Domain Controller (DC) does the credentials validation but not the decision on access, which would be based on the service’s permissions.**
10. **AS-REQ, AS-REP, TGS-REQ, TGS-REP, ST: AS-REQ is the initial request for authentication, AS-REP is the response with a TGT. TGS-REQ is the request for a service ticket, TGS-REP is the response, and the ST (Service Ticket) is the final ticket used to access the requested service.**
11. **Service Ticket: The Service Ticket lists the identity of the client, the identity of the service, and a time stamp, all encrypted in a way that ensures the ticket is not reused.**

12. **PAC: The Privilege Attribute Certificate maintains information about user group memberships, rights, and permissions granted, which allow services to determine the level of access.**

13. **SPN: The Service Principal Name enables a service to be uniquely identified within Active Directory and allows the Kerberos system to authenticate the correct service.**
14. **Three Long Term Keys: The password hash of the user, the password hash of the service, and the secret key of the KDC-all vital for the authentication process.**
****Kerberoasting**
15. **How Kerberoasting Works: Kerberoasting is an attack where an attacker requests service tickets for service accounts with weak passwords and tries to crack the tickets offline to reveal the service account password.**

16. **What Must Be True for Successful Kerberoasting: The service account would have to be configured to use the Kerberos authentication and its password must be relatively weak to be cracked.**

17. **Kerberoasting Tools: The tools used to request and crack service tickets are Rubeus, Impacket, Mimikatz, and Hashcat for retrieving interesting information such as the password of service accounts.**

18. **Why User Accounts Are More Crackable: User accounts are more susceptible to being crackable since they usually use weaker passwords compared to the service accounts, which are normally better protected.**

19. **Ease of Kerberoasting Detection: Kerberoasting detection can be effectively done by monitoring applications that request service tickets or request tickets associated with service accounts.**

20. **Kerberoasting OpSec: These include the limitation of service account access, strong passwords, and monitoring of service ticket requests to find anomalies.**

**Silver Ticket Attack**

1. **What is a Silver Ticket Attack? In a Silver Ticket attack, the attacker uses a compromised service account key to create a forged service ticket that provides unauthorized access to a specific service.**

2. **Mechanisms of a Silver Ticket Attack: The attacker creates a service ticket by compromising a service account key, which will enable him to pretend to be a valid user of the service concerned.**

**Golden Ticket Attack**

1. **What is a Golden Ticket Attack? The Golden Ticket attack allows an attacker to create a fake TGT for a user, which in turn grants the attacker access to all services within the domain.**

2. **What Makes a Golden Ticket "Special"? One reason why the Golden Ticket is special is that it gives unlimited access to the domain to all systems and services until such time as the TGT expires or gets revoked.**

3. **Privilege Required to Perform Silver and Golden Ticket Attacks: Attackers would need the service account key for a Silver Ticket attack, while they would need the password hash of the KRBTGT account for a Golden Ticket attack.**

**Skeleton Key Attack**

1. **What is Skeleton Key Attack? During a Skeleton Key attack, an attacker injects a master password into the Active Directory database, which, in turn, can be used by the attacker to authenticate to all systems without requiring individual credentials.**

**2. **Process of a Skeleton Key Attack: The attacker injects the Skeleton Key into the memory of the DC, bypassing all normal authentication.****
******Pass-The-Ticket and Over-Pass-The-Hash Attacks******
*****1. **Pass-The-Ticket: The ticket, which was already earned by a valid Kerberos, is stolen and used in order to authenticate to other services using a Pass-The-Ticket attack. *******

******2. **Over-Pass-The-Hash: This is when the NTLM hash is used in requesting a TGT, hence bypassing any need for a password.******

********Defenses and Detection******

**1. **Why Can't We Prevent These Attacks?**** 
****These attacks are hard to prevent because Kerberos itself is inherently vulnerable to the exploitation of some sort-weak password and poor key management being two of those forms.******

**2. **Primary Defense Against Kerberoasting:**** 

****The main defense is to use strong, complex passwords for service accounts and to monitor abnormal requests for tickets.********

**3. **Honey Tickets: These are decoy tickets, which are capable of detecting an attacker by trapping unauthorized requests within them.****

**4. **Defensive Measures: Some of the defense mechanisms include regular rotation of service account keys, strict authentication policies, and logging and monitoring against suspected activities. ******

******Question Round:******

********1. Why do we have to rotate the KRBTGT hash twice in order to kill a Golden Ticket?****

************ The KRBTGT (Kerberos Ticket Granting Ticket) hash must be rotated twice to invalidate the Golden Tickets. Once the first rotation is performed, this automatically revokes the current TGT and then makes tickets previously issued unable to be used. A second rotation ensures that any potential new Golden Tickets-which may be created after the first rotation-are also invalidated. This double rotation ensures the complete removal of access that was granted to any forged Golden Tickets.****

************ ****2. What should we be careful about when this is done?****

******Here are several things to consider in your planning when rotating the KRBTGT hash.****** 

**- **Disrupting Authentication: It will temporarily disrupt the authentication mechanism across the domain, since all TGTs will now be invalid and users will have to re-authenticate.****
**- ****** ***Service Downtimes: Services dependent on Kerberos authentication may go down temporarily because their tickets become invalidated; therefore, proper timing needs to be taken into consideration and communicated to users. ******* 
**- *****Reauthentication: After the hash rotation, the users have to log on again to get the latest TGT, which can be a problem if not planned and managed properly.******* 
****-****
******3. Is there a better authentication system than Kerberos? Explain ******** 

********While Kerberos is highly secure and in wide use, some feel that other systems may be more secure or more suited for ease of use in a particular context:****
**- **Public Key Infrastructure: PKI, based on certificates, is more scalable and allows better encryption, especially in environments when cross-platform authentication is required. However, it necessitates proper key management and infrastructure.**** 
**- **FIDO2/WebAuthn - A newer standard of authentication that involves hardware-based authentication, such as biometrics and security keys, to replace passwords. It is more resistant than Kerberos against phishing and password theft.**** 
**- **OAuth/OpenID Connect: Modern, widely used authentication systems, especially for web-based applications, offering token-based authentication and better integration with cloud and distributed services. However, they lack the extended auditing and ticketing available in Kerberos.********