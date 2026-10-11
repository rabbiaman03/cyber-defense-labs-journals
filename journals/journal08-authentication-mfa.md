# Learning Journal 8 — Authentication and MFA

##### **Topic 1: MFA and other technologies
1. What is MFA?

Multi-Factor Authentication (MFA) is a security approach that requires two or more independent pieces of evidence, called factors, to verify the user's identity.

2. What is a factor, in terms of MFA?

A **factor** is a category of authentication evidence.

Each factor should be **independent** in that compromising one (e.g., stealing a password) does not compromise the others.

3. Name and describe each of the four kinds of authentication factors, and then use an example of each.

Four types of authentication factors are:

Knowledge Factor — “Something you know”

Examples include password, PIN, security questions.

Possession factor — “Something you have”.

Examples: one-time code from a phone, hardware security key (YubiKey).

Inherent Factor — “Something you are”

Examples include fingerprint, face scan, iris scan.
Behavioural Factor — “Something you do”

Examples include: typing pattern, mouse movement, walking gait, typical IP/location.

4. Describe Adaptive MFA

Adaptive MFA bases the required authentication factors on **login risk. It takes into account device reputation, location, time of day, user behavior, network/IP risk. In other words: if something looks unusual, it asks for _more_ factors; if everything looks normal.

5. Describe Passwordless MFA
Passwordless MFA removes passwords altogether.
It uses device-bound cryptographic keys, biometrics, hardware security keys, mobile push approvals. This removes password weaknesses such as reuse, phishing, and guessing.

6. Why is MFA important?

MFA protects against:
- Stolen credentials
- Phishing
- Brute-force attacks
- password reuse
It significantly reduces account compromise risk.

7. Differentiate MFA vs. single sign-on by describing the differences and purpose of each.

**MFA focuses on security**, requiring multiple identity proofs.  
**SSO focuses on convenience**, providing access to multiple applications with a single login.

8. What is the difference between 2FA and MFA?
**2FA** demands _precisely two_ factors.
**MFA** necessitates _two or more_ factors.
9. Research Password vaults. Pick your favourite, describe how it works, and why you chose it
All credentials are stored in Bitwarden, within an encrypted vault locked by a master password. It is open-source and cross-platform, with MFA support. I chose Bitwarden for its transparency, strong security, and usability.

10. Describe various types of MFA.

Types of MFA:
- SMS/Email OTPs
- Authenticator apps (TOTP)
- Push notifications
- Hardware keys (FIDO2)
- Biometric
- Passwordless MFA

3. Describe various MFA bypass attacks

Common bypass attacks include:

- MFA Fatigue (Push Bombing)
- SIM swapping
- Phishing proxies: adversary-in-the-middle
- Session hijacking
- Legacy protocol abuse

##### **Topic 2: Understanding Password Entropy - Longer

1. Explain why it is more important to have long passwords instead of complex ones.

Long passwords create exponentially more combinations, making them far harder to crack. 
Complex short passwords can still be based on predictable patterns.

1. **Explain, in your own words, what the comic is trying to say. Create a secure passphrase that reflects your understanding.

This comic demonstrates that complicated passwords are hard to remember for users but very easy to break for computers, while long passphrases are much easier for humans and way harder for attackers.

2. **Refer to the Crambler article and discuss the time taken to crack various length passwords

- 8 characters → seconds/minutes
- 10 characters → hours/days
- 12 characters → decades
- 16+ characters → virtually uncrackable

2. **Describe how they created the Hive table

Brute-force times are calculated in the Hive Systems table using:

- password length

Character set size
- GPU cracking rates
- distributed computing models

3. **Looking at the Hive table, what would your recommendations be for a password policy?

I would suggest the following:

- Minimum **16 characters**
- Use **passphrases
- Avoid verbosity rules
- Be sure to have a password manager

- MFA implementation

##### **Topic 3 - Password Cracking

1. Explain the process of password cracking.

The process of password cracking are:

- Obtain hashes through breaches or system access.

- Attack methods include brute-force, dictionary, or hybrid attacks.

- Test candidates against hashes.

- Recover matching passwords.

2. describe why attackers have the advantage, including techniques they use

Attackers use:

- GPUs

- automated scripts

* Huge leaked password databases

- cloud computing

- password reuse by victims

Attackers use these components and take the advantage.

3. Describe random guess attacks. I described a very common one in class, which is not included in the article. What is it?

One common example is **password spraying**: attackers try one common password on many accounts.

4. Describe brute force attacks

A **brute force attack** is a trial-and-error method of obtaining information, such as a user's password or a decryption key. It involves a systematic check of every possible password or key combination until the correct combination is found. The attacker uses automated software to generate a large number of guesses, submitting them rapidly against a target login page, encryption scheme, or service.

5. Describe dictionary attacks

A **dictionary attack** is one of the more sophisticated brute-force methods that attempts to guess passwords by using a list of common words, phrases, and previously compromised passwords. The attacker uses a dictionary file containing several thousands or millions of most likely passwords, such as names, common words, common number sequences like "123456," or even specific domain-related terms.

6. Credential stuffing

Credential stuffing is an attack where an attacker tries to log into a large number of accounts on a target website using stolen pairs of usernames and passwords that were previously leaked from a different website. It exploits the common bad practice of password reuse.

7. Describe password spraying

Password spraying is a form of brute-force attack that involves a bad actor attempting to gain access to a large number of different user accounts using a small list of common passwords; for example, "Password1" or "Winter2025!". It's used to get around security measures that lock out accounts if there are too many incorrect login attempts.

8. Describe social engineering and human-based attacks including techniques

Social Engineering: A set of manipulative psychological techniques used to trick users into divulging confidential information or giving them access to protected systems. It takes advantage of the human factor in security. The common techniques include Phishing, Pretexting, Baiting, Tailgating.

9. What are hash-based attacks?

Hash-based attacks aim at the hash of a password, not directly at the password. A system usually passes a password through a one-way mathematical function called a hashing algorithm - for example, SHA-256 or bcrypt - when storing it. The system then stores the resulting fixed-length string, which is called the hash, instead of storing the original password.

10. Describe Pass-the-Hash Attacks.

A **Pass-the-Hash (PtH)** attack is a technique whereby an attacker authenticates to a network service using the underlying **password hash** rather than the plaintext password. In practice, this occurs in a Windows environment utilizing protocols like NTLM.

11. Describe Pass-the-Ticket Attacks

A **Pass-the-Ticket (PtT)** attack is similar to PtH but is specific to the **Kerberos** authentication protocol - used in modern Windows/Active Directory environments. Instead of passing a hash, the attacker steals and uses a **Kerberos ticket**.

12. Describe Kerberoasting Attacks.

**Kerberoasting** is an attack that takes advantage of a feature in the Kerberos protocol to collect password hashes for user accounts that have been configured as **service accounts**-accounts used by non-human services such as web servers. Service Principal Names (SPNs) used by the service accounts.

- An attacker, posing as any authenticated domain user, requests a Kerberos service ticket (TGS) for a service account's SPN.

- The Kerberos KDC encrypts the TGS with the **NTLM password hash of the service account** as the key and returns it to the attacker.

- The attacker receives the ticket, takes it offline, and performs a fast, offline brute-force or dictionary attack on the encrypted ticket to recover the service account's plaintext password.

13. Describe Rainbow Table attacks.

A **Rainbow Table** attack is a hash-based attack that is optimized for efficiency to dramatically speed up the process of finding a password from a stolen hash.

- **What is a Rainbow Table?**
It is a huge, pre-computed table that contains chains of hash-password pairs. The attacker does not have to compute the hash for every possible password in real time; he simply looks up the stolen hash in a pre-computed table.

- Process:

-  The attacker obtains a stolen password hash.

-  They look for the stolen hash in the Rainbow Table.

-  If found, the corresponding plaintext password is disclosed straight away.

14. Explain in detail each of the 5 Risky Password Practices.

Such practices significantly increase the risk of the account being compromised.

1. Using the Same Password for Numerous Accounts

- **Detail:** Using the exact same password for two or more unrelated services, such as your bank, your email, and a shopping site.

- **Risk:** This is considered the main enabler of **Credential Stuffing** attacks. Once one account gets compromised-especially a low-security one-the attacker immediately gets access to all other accounts which use the very same password.

2. Using Predictable and Common Passwords

- **Detail:** Selecting passwords that are well-known, short, or easily guessed, such as "123456," "password," "qwerty," or simple dictionary words.

- **Risk:** These passwords are the first targets for **Dictionary Attacks** and standard **Brute Force** attempts. They can often be cracked within seconds or minutes.



- **Detail:** Creating passwords based on easily obtainable personal details, such as a name, pet's name, birthdate, or street address.

- **Risk:** Attackers employ **Social Engineering** and publicly available information, such as social media profiles, to obtain this information and merge it with common substitutions ('s' becoming '$', for example) to formulate very effective, targeted guesses of passwords.

4. Writing Down Passwords in Plain Sight


- **Detail:** Passwords stored on unencrypted digital files, such as a spreadsheet on a desktop, or on physical notes, like a sticky note under a keyboard.

- **Risk:** This forms a huge vulnerability for physical security breaches. Anyone who gets access to either the physical or logical location can immediately compromise the account without necessarily having to carry out a sophisticated cyberattack.

5. Password or credential sharing

- Detail: Sharing your password with your colleague, your friend, or any other person, be it for a temporary purpose.

- **Risk:** Loss of the **non-repudiation** principle. If an account is used maliciously, you cannot prove definitively that _you_ were not the one who performed the action. Moreover, each person who knows the password is a new potential point of compromise.

15. Describe, in detail, each one of the 8 Password Security Best Practices.

These practices serve as the foundation for good password hygiene and security.

1. Use Long and Complex Passwords
- **Detail:** Passwords should be long-12+ characters is a minimum recommended length-and include a mix of uppercase letters, lowercase letters, numbers, and symbols.
- **Benefit:** This exponentially increases the time required for a **Brute Force Attack** to succeed. Longer passwords are the single greatest deterrent against cracking.
2. Make sure to use a different password for each account.
- **Detail:** Each web service, application, or system should have a unique, randomized password.

- **Benefit:** This entirely eliminates the risk of a **Credential Stuffing** attack. A breach on one service will not affect any other account.

3. Using a Password Manager

- **Detail:** Generate, store, and manage all passwords using a secure, encrypted application such as 1Password or LastPass.

- **Benefit:** This enables the use of long, complex, unique passwords (Best Practices 1 & 2) without the user having to memorize them, which is otherwise impossible.

4. Enable Multi-Factor Authentication (MFA/2FA)

- **Detail:** In addition to the password, require a second verification factor-which could be a code from a phone app, a text message, or a physical security key.



5. Change Default Passwords Immediately

- **Detail:** The vendor-provided default password for all new hardware, software, routers, and IoT devices shall be changed upon first use.

- **Benefit:** Prevents attackers from gaining immediate, easy access by simply using a publicly known default password.

6. Do Not Store Passwords in the Browser

- **Detail:** Avoid using the browser's built-in password saving feature, such as Chrome Password Manager.

- **Benefit:** Passwords stored in browsers are less securely encrypted than those in password managers and can easily be extracted by some kinds of malware.

7. Never send passwords via unsecured communication.
- **Detail:** Passwords should never be shared over email, instant messaging applications like Slack or Teams, or over an unencrypted voice call.
- **Benefit:** Prevents the password from being intercepted as plaintext during transmission or stored insecurely in chat/email logs.
8. Employ a Strong Hashing Algorithm with Salting (For Developers/Admins)

- **Benefit:** Slows down **Brute Force** attempts, renders **Rainbow Table Attacks** useless, protects the database of stolen hashes in case of a breach.
##### **Topic 4: You are the weakest Link**

1. Why did the Green Book consider 8 characters long enough to be a secure password?

Because the computing power was very weak at that time. Brute forcing 8 characters was considered unrealistic then.

2. Is storing passwords in browsers secure?

Not completely. Browsers store them locally, and malware is able to extract them. Password managers are much safer.

2. Why should we not use SMS for 2FA?

SMS should not be used for 2FA because SMS can be:

- SIM-swapped
- intercepted
- spoofed
- rerouted
- stolen via malware
- dependant upon telecom networks

4. What is password cracking?

Process of password recovery by guessing, brute-forcing, or exploiting hashes. 

5. What are the two types of Windows hashes? - **LM (LAN Manager) - **NTLM / NT hash** 


6. Why is it important to use more than 14 characters? 

Using more than 14 characters is critical, since LM hashing chops passwords into **two 7-character pieces**; these are much simpler to crack.

7. Why are LM hashes weaker than they appear? (2 reasons) 

Two reasons are: - 
They convert all letters to **uppercase.
They divide the password into **7-character blocks** and crack each separately. 

8. Why is greater length more important than larger character sets? 

For with increasing length, entropy increases **exponentially**, while complexity does so only **linearly**. 

9. What are some recommendations given in this video? 

Recommendations made in this video are: - Use long passphrases - Avoid complex rules; - Do not share passwords - Employ MFA - Prefer hardware keys - Avoid SMS - Check email for breaches - Using password managers.

10. Why does CJ say that there are no right or wrong answers to the password questions?

CJ state that there are no right or wrong answers for the password questions since password security has to balance - usability - memorability - threat model - organizational policy.

11. What are the current NIST recommendations for passwords? (use your favourite search engine for this) 
Current NIST Recommendations are: 
- Minimum 8 characters
- Allow up to 64 characters
- No composition rules 
- No forced periodic resets
- Screen new passwords against breach lists 
- Encourage password managers 
- Use MFA 

11. Describe what this site does: 1. https://haveibeenpwned.com/

It lets you see whether your e-mail, usernames, and passwords have shown up in known data breaches. It provides password leak detection and alerts.