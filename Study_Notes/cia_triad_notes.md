# Cybersecurity Fundamentals

Cybersecurity is the ongoing effort to protect individuals, organizations and governments from digital attacks by protecting networked systems and data from unauthorized use or harm.

---

## The CIA Triad

The McCumber Cube is a model framework created by John McCumber in 1991 to help organizations establish and evaluate information security initiatives. It defines three foundational principles for protecting information systems:

### Confidentiality

Confidentiality is a set of rules that prevents sensitive information from being disclosed to unauthorized people, resources and processes.

**Methods to ensure confidentiality include:**
- Data encryption
- Identity proofing
- Two factor authentication

**What it protects:**
- Personal data (name, social security number, driver license number, date and place of birth)
- Medical records and electronic health records (EHRs)
- Financial records, tax records, credit card statements
- Educational records and academic qualifications
- Employment data and performance reviews

---

### Integrity

Integrity ensures that system information or processes are protected from intentional or accidental modification.

**Methods to ensure integrity include:**
- Hash functions
- Checksums

**Protection scope:**
- System information protected from modification
- Processes protected from unauthorized changes
- Data accuracy maintained throughout storage and transmission
- Prevents accidental data corruption

---

### Availability

Availability means that authorized users are able to access systems and data when and where needed and those that do not meet established conditions, are not.

**Methods to achieve availability include:**
- Maintaining equipment
- Performing hardware repairs
- Keeping operating systems and software up to date
- Creating backups

**Key aspects:**
- Systems must be operational and accessible to legitimate users
- Critical services remain available during emergencies
- Data redundancy through backups
- Disaster recovery planning

---

## Threat Types

### Phishing

Phishing is very common and often works. Cybercriminals use phishing emails to trick users into divulging confidential information or performing unintended actions.

**Example incident:** In August 2020, elite gaming brand Razer experienced a data breach which exposed the personal information of approximately 100,000 customers. A security consultant discovered that a cloud cluster was misconfigured and exposed a segment of Razer's infrastructure to the public Internet. It took Razer more than three weeks to secure the cloud instance, during which time cybercriminals had access to customer information that could have been used in social engineering and fraud attacks.

**Prevention:**
- Be cautious of unexpected requests
- Verify sender identities
- Do not click suspicious links
- Use email filtering
- Enable two-factor authentication

---

### Malware

Malware is malicious software designed to gain unauthorized access to systems and data.

#### Viruses

A virus is a type of computer program that, when executed, replicates and attaches itself to other executable files by inserting its own code.

**Characteristics:**
- Require end-user interaction to initiate activation
- Can be written to act on a specific date or time
- Can be programmed to mutate in order to avoid detection
- Spread by USB drives, optical disks, network shares or email
- Can range from harmless (display funny image) to destructive (modify or delete data)

#### Worms

This is a type of malware that replicates itself in order to spread from one computer to another. Unlike a virus, which requires a host program to run, worms can run by themselves.

**Characteristics:**
- Do not require user participation after initial infection
- Spread very quickly over the network
- Exploit system vulnerabilities
- Have a way to propagate themselves
- Contain malicious code (payload) to cause damage
- Responsible for some of the most devastating attacks on the Internet

**Example:** In 2001, the Code Red worm had infected over 300,000 servers in just 19 hours.

#### Trojans

This malware carries out malicious operations by masking its true intent. It might appear legitimate but is, in fact, very dangerous.

**Characteristics:**
- Exploit your user privileges
- Most often found in image files, audio files or games
- Do not self-replicate
- Act as a decoy to sneak malicious software past unsuspecting users

#### Ransomware

This malware is designed to hold a computer system or the data it contains captive until a payment is made.

**How it works:**
- Usually works by encrypting your data so that you can't access it
- Some versions can take advantage of specific system vulnerabilities to lock down the system
- Often spread through phishing emails that encourage you to download a malicious attachment
- Also spread through software vulnerabilities

#### Spyware

Designed to track and spy on you, spyware monitors your online activity and can log every key you press on your keyboard, as well as capture almost any of your data.

**Capabilities:**
- Monitors online activity
- Logs keystrokes
- Captures sensitive personal information such as online banking details
- Often bundles itself with legitimate software or Trojan horses
- Modifies security settings on your devices

#### Adware

Adware is often installed with some versions of software and is designed to automatically deliver advertisements to a user, most often on a web browser.

**Characteristics:**
- Creates constant pop-up ads
- Hard to ignore
- Common for adware to come with spyware

#### Rootkits

This malware is designed to modify the operating system to create a backdoor, which attackers can then use to access your computer remotely.

**Characteristics:**
- Most rootkits take advantage of software vulnerabilities
- Gain access to resources that normally shouldn't be accessible (privilege escalation)
- Modify system files
- Can modify system forensics and monitoring tools, making them very hard to detect
- Computer infected by a rootkit usually has to be wiped and any required software reinstalled

#### Backdoors

This type of malware is used to gain unauthorized access by bypassing the normal authentication procedures to access a system.

**Impact:**
- Hackers can gain remote access to resources within an application
- Issue remote system commands
- Works in the background and is difficult to detect

#### Scareware

This is a type of malware that uses 'scare' tactics to trick you into taking a specific action.

**How it works:**
- Mainly consists of operating system style windows that pop up
- Warns that your system is at risk and needs to run a specific program
- If you agree to execute the specific program, your system will become infected with malware

---

### Botnets

A botnet is a network of infected devices, like computers and IoT devices, that are remotely controlled by a single attacker or "bot herder". These devices, known as "bots" or "zombies," are used to perform large-scale, malicious activities.

**How botnets work:**

1. **Infection:** Malware, which is often designed to spread automatically by scanning for vulnerabilities, infects devices and turns them into bots.

2. **Control:** The bot herder uses a command and control (C2) server to send instructions to the infected devices.

3. **Execution:** The bots carry out tasks simultaneously, such as overwhelming a server with traffic during a DDoS attack or sending out massive amounts of spam emails.

4. **Concealment:** The botnet remains hidden by using a small portion of each device's resources, which is often too insignificant for the owner to notice.

**Common uses of botnets:**
- Distributed Denial-of-Service (DDoS) attacks - flooding a target server with traffic
- Spam and phishing - sending out large volumes of spam emails or phishing attempts
- Data theft - stealing sensitive information like login credentials or personal data
- Cryptocurrency mining - using the compromised devices' processing power to mine cryptocurrency
- Click fraud - generating fraudulent clicks on online advertisements

**Protection:**
- Keep operating system and software up to date with latest patches
- Use a reputable antivirus or anti-malware program
- Be cautious about clicking links or downloading attachments from unknown sources
- Use strong, unique passwords for all online accounts
- Many organizations like Cisco force network activities through botnet traffic filters

---

### Distributed Denial-of-Service (DDoS) Attacks

A Distributed DoS (DDoS) attack is similar to a DoS attack but originates from multiple, coordinated sources.

**How it works:**
- An attacker builds a network (botnet) of infected hosts called zombies
- These are controlled by handler systems
- Zombie computers constantly scan and infect more hosts, creating more and more zombies
- When ready, the hacker instructs the handler systems to make the botnet of zombies carry out a DDoS attack

**Impact:**
- Results in interruption of network service to users, devices or applications
- Makes services inaccessible to legitimate users
- Can prevent organizations from conducting business online

---

### Brute Force Attacks

Entering a username and password is one of the most popular forms of authenticating to a website. Therefore, uncovering your password is an easy way for cybercriminals to gain access to your most valuable information.

#### Password Spraying

This technique attempts to gain access to a system by 'spraying' a few commonly used passwords across a large number of accounts.

**Example:** A cybercriminal uses 'Password123' with many usernames before trying again with a second commonly-used password, such as 'qwerty.'

**Advantage:** This technique allows the perpetrator to remain undetected as they avoid frequent account lockouts.

#### Dictionary Attacks

A hacker systematically tries every word in a dictionary or a list of commonly used words as a password in an attempt to break into a password-protected account.

#### Brute Force Attacks

The simplest and most commonly used way of gaining access to a password-protected site. Brute-force attacks see an attacker using all possible combinations of letters, numbers and symbols in the password space until they get it right.

**Note:** Because brute-force attacks take time, complex passwords take much longer to guess.

#### Rainbow Table Attacks

Passwords in a computer system are not stored as plain text, but as hashed values (numerical values that uniquely identify data).

**How it works:**
- Rainbow table is a large dictionary of precomputed hashes and the passwords from which they were calculated
- Unlike a brute-force attack that has to calculate each hash, a rainbow attack compares the hash of a password with those stored in the rainbow table
- When an attacker finds a match, they identify the password used to create the hash

#### Plain Text Passwords

Plain text or unencrypted passwords can be easily read by other humans and machines by intercepting communications. If you store a password in clear, readable text, anyone who has access to your account or device, whether authorized or unauthorized, can read it.

---

### SQL Injection

A vulnerability where an attacker crafts malicious SQL code that is injected into input fields.

**How it works:**
- Programs often require data input
- This incoming data could have malicious content designed to force the program to behave in an unintended way
- Example: A malicious user could craft an image file with invalid image dimensions
- The maliciously crafted dimensions could force the program to allocate buffers of incorrect and unexpected sizes

---

### Zero-Day Exploits

A zero-day (0day) exploit is a cyber attack targeting a software vulnerability which is unknown to the software vendor or to antivirus vendors.

**Characteristics:**
- The attacker spots the software vulnerability before any parties interested in mitigating it
- Quickly creates an exploit and uses it for an attack
- Such attacks are highly likely to succeed because defenses are not in place
- Makes zero-day attacks a severe security threat

**Typical attack vectors:**
- Web browsers, which are common targets due to their ubiquity
- Email attachments that exploit vulnerabilities in the application opening the attachment
- Vulnerabilities in specific file types such as Word, Excel, PDF or Flash

**Typical targets:**
1. Government departments
2. Large enterprises
3. Individuals with access to valuable business data, such as intellectual property
4. Large numbers of home users who use a vulnerable system
5. Hardware devices, firmware and Internet of Things (IoT)
6. In some cases governments use zero-day exploits to attack other nations

**Market for zero-day exploits:**
Because zero-day vulnerabilities are valuable, a market exists in which organizations pay researchers. There are white, gray and black markets in which zero-day vulnerabilities are traded for up to hundreds of thousands of dollars.

**Example incidents:**

**Stuxnet:**
- Malicious computer worm targeted computers used for manufacturing in Iran, India, and Indonesia
- Primary target was Iran's uranium enrichment plants
- Zero-day vulnerabilities existed in software running on programmable logic controllers (PLCs) running Microsoft Windows
- Worm infected PLCs through vulnerabilities in Siemens Step7 software
- Caused PLCs to carry out unexpected commands on assembly line machinery
- Sabotaged the centrifuges used to separate nuclear material

**Sony zero-day attack (2014):**
- Sony Pictures was victim of a zero-day exploit in late 2014
- Attack crippled Sony's network
- Led to release of sensitive corporate data
- Compromised data included details of forthcoming movies, business plans, and personal email addresses of senior executives
- Details of exact vulnerability remain unknown

**RSA (2011):**
- Hackers used unpatched vulnerability in Adobe Flash Player
- Gained access to RSA network through Excel spreadsheet attachments
- Spreadsheets contained embedded Flash file exploiting zero-day vulnerability
- Installed Poison Ivy remote administration tool
- Stole sensitive information related to SecurID two-factor authentication products

**Operation Aurora (2009):**
- Targeted intellectual property of major enterprises
- Targeted: Google, Adobe Systems, Yahoo, and Dow Chemical
- Vulnerabilities existed in Internet Explorer and Perforce

---

## Attack Vectors

### Social Engineering

Social engineering is the manipulation of people into performing actions or divulging confidential information. Social engineers often rely on people's willingness to be helpful, but they also prey on their weaknesses.

**Tactics:**
- An attacker will call an authorized employee with an urgent problem that requires immediate network access
- Appeal to the employee's vanity or greed
- Invoke authority by using name-dropping techniques in order to gain access

#### Pretexting

This is when an attacker calls an individual and lies to them in an attempt to gain access to privileged data.

**Example:** Pretending to need a person's personal or financial data in order to confirm their identity.

#### Tailgating

This is when an attacker quickly follows an authorized person into a secure, physical location.

#### Quid Pro Quo (Something for Something)

This is when an attacker requests personal information from a person in exchange for something, like a free gift.

**Real-world example:**
A cybercriminal can take advantage of your relationships by accessing your online accounts and appealing to your good nature to try and trick you into wiring money to your friends or family in a time of need. There have been many reported cases of hackers impersonating family members and sending messages stating that they need money wired in order to get home from abroad after losing their wallets.

---

### Insider Threats

An insider threat comes from within an organization. This could be:
- Current or former employees
- Contractors or business partners
- Anyone with authorized access to systems or data

**Examples:**
- Past employees should not have access to customer information when leaving a company
- Employees with access to sensitive systems may intentionally or unintentionally leak information
- Disgruntled employees may sabotage systems or data

**Prevention:**
- Implement proper access control
- Remove access immediately when employees leave
- Monitor user activities on sensitive systems
- Conduct background checks
- Implement the principle of least privilege

---

### Wireless Attacks

With the increasing use of wireless networks, new attack vectors have emerged.

**Bluetooth Vulnerabilities:**
The Bluetooth wireless protocol, found on many smartphones and tablets, can be exploited by hackers to:
- Eavesdrop on communications
- Establish remote access controls
- Distribute malware
- Drain batteries

**Prevention:**
- Keep Bluetooth turned off when you aren't using it
- Use strong authentication for paired devices
- Keep devices updated with latest patches

**Public Wi-Fi Risks:**
When you are away from home, you can access your online information via public wireless networks or Wi-Fi hotspots. However, there are some risks involved, which mean that it is best not to access or send any personal information when using public Wi-Fi.

**Protection measures:**
- Verify that your device isn't configured with file and media sharing
- Require user authentication with encryption
- Use an encrypted VPN service to prevent others from intercepting your information (known as 'eavesdropping')
- VPN gives secure access to the Internet by encrypting the connection between your device and the VPN server
- Even if hackers intercept a data transmission in an encrypted VPN tunnel, they will not be able to decipher it

---

### Advanced Persistent Threats (APTs)

Attackers also achieve infiltration through advanced persistent threats (APTs) — a multi-phase, long term, stealthy and advanced operation against a specific target.

**Characteristics:**
- Individual attackers often lack the skill set, resources or persistence to perform APTs
- Due to complexity and skill level required, APT is usually well-funded
- Typically targets organizations or nations for business or political reasons
- Main purpose is to deploy customized malware on one or more of the target's systems
- Malware remains undetected for long periods

---

## Protection Strategies

### Understanding Vulnerabilities

**Security vulnerabilities** are any kind of software or hardware defect. A program written to take advantage of a known vulnerability is referred to as an **exploit**. A cybercriminal can use an exploit against a vulnerability to carry out an **attack**.

### Online Security Best Practices

To make your device safe and secure, you should:

#### 1. Use a Firewall

- Turn the firewall on
- Keep it constantly updated
- Use at least one type of firewall (software firewall or hardware firewall on router)
- Protects device from unauthorized access

**Types of firewalls:**
- Network layer firewall: filters communications based on source and destination IP addresses
- Transport layer firewall: filters based on source and destination data ports and connection states
- Application layer firewall: filters based on application, program or service
- Context aware layer firewall: filters based on user, device, role, application type and threat profile
- Proxy server: filters web content requests like URLs, domain names and media types
- Reverse proxy server: placed in front of web servers, protects and distributes access
- NAT firewall: hides or masquerades the private addresses of network hosts
- Host-based firewall: filters ports and system service calls on a single computer operating system

#### 2. Install Antivirus and Antispyware

Malicious software, such as viruses and spyware, are designed to gain unauthorized access to your computer and your data.

**Impact of malware:**
- Viruses can destroy your data and slow down your computer
- Can take over your computer and broadcast spam emails using your account
- Spyware can monitor your online activities and collect your personal information
- Can produce unwanted pop-up ads on your web browser

**Protection:**
- Only download software from trusted websites
- Always use antivirus software to provide another layer of protection
- Software often includes antispyware and is designed to scan your computer and incoming email
- Keep your software up to date to protect against new malicious software

#### 3. Manage Your Operating System and Browser

Hackers are always trying to take advantage of vulnerabilities that may exist in your operating system (such as Microsoft Windows or macOS) or web browser (such as Google Chrome or Apple Safari).

**Protection:**
- Set security settings on your computer and browser to medium level or higher
- Regularly update your computer's operating system, including your web browser
- Download and install the latest software patches and security updates from the vendors

#### 4. Set Up Password Protection

All of your computing devices, including PCs, laptops, tablets and smartphones, should be password protected to prevent unauthorized access.

**Best practices:**
- Any stored information, especially sensitive or confidential data, should be encrypted
- Only store necessary information on your mobile device, in case it is stolen or lost
- If any one of your devices is compromised, criminals may be able to access all of your data through your cloud storage service provider

#### 5. Protect IoT Devices

IoT devices pose an even greater risk than your other computing devices.

**Why:**
- While desktop, laptop and mobile platforms receive frequent software updates, most IoT devices have their original software
- If vulnerabilities are found in the software, the IoT device is likely to be vulnerable
- IoT devices require Internet access, most often relying on your local network
- When IoT devices are compromised, they allow hackers access to your local network and data

**Protection:**
- Set up any IoT devices on an isolated network
- Check Shodan (a web-based IoT device scanner) to identify any vulnerable devices on the Internet
- Keep IoT device firmware updated

### Data Protection Strategies

#### Encryption

Encryption is the process of converting information into a form in which unauthorized parties cannot read it. Only a trusted, authorized person with the secret key or password can decrypt the data and access it in its original form.

**Important note:** The encryption itself does not prevent someone from intercepting the data. It can only prevent an unauthorized person from viewing or accessing the content.

**Tools:**
- Encrypting File System (EFS) is a Windows feature that can encrypt data
- EFS is directly linked to a specific user account
- Only the user that encrypts the data will be able to access it after encryption

#### Data Backup

Having a backup may prevent the loss of irreplaceable data. To back up data properly, you will need an additional storage location for the data and you must copy the data to that location regularly.

**Backup options:**

**Home Network:**
- Store data locally means you have total control of it

**Secondary Location:**
- Copy all of your data to a network attached storage device (NAS)
- Use a simple external hard drive
- Back up important folders on thumb drives, CDs, DVDs or tapes
- You are the owner of the data and totally responsible for cost and maintenance

**Cloud Storage:**
- Subscribe to a cloud storage service like Amazon Web Services (AWS)
- Cost depends on amount of storage space needed
- Access to backup data as long as you have account access
- Data is safe in event of storage device failure or extreme situations like fire or theft

#### Deleted File Recovery

When you move a file to the recycle bin and delete it permanently, the file is only inaccessible from the operating system. Anyone with the right forensic tools could still recover the file due to a magnetic trace left on the hard drive.

### Two-Factor Authentication

Popular online services, such as Google, Facebook, Twitter, LinkedIn, Apple and Microsoft, use two factor authentication to add an extra layer of security for account logins.

**How it works:**
Besides your username and password or personal identification number (PIN), two factor authentication requires a second token to verify your identity. This may be a:
- Physical object such as a credit card, mobile phone or fob
- Biometric scan such as a fingerprint or facial and voice recognition
- Verification code sent via SMS or email

### Open Authorization (OAuth)

Open authorization (OAuth) is an open standard protocol that allows you to use your credentials to access third-party applications without exposing your password.

**Benefit:** Instead of having to reset your login details, you can log into applications using your existing social media accounts.

---

## Key Takeaways

1. **CIA Triad is fundamental:** Every security measure should aim to protect Confidentiality, Integrity, or Availability

2. **Threats are diverse:** From malware to social engineering, threats take many forms and require different defense strategies

3. **Multiple layers matter:** No single solution protects against all threats; use defense in depth approach

4. **User awareness is critical:** Many attacks succeed because of human error or social engineering

5. **Stay updated:** Regularly update operating systems, software, and firmware to patch vulnerabilities

6. **Use multi-factor authentication:** Adds significant protection beyond just passwords

7. **Backup your data:** Regular backups can prevent catastrophic data loss

8. **Encrypt sensitive data:** Encryption protects data even if it's intercepted

9. **Monitor and restrict access:** Implement principle of least privilege and monitor for insider threats

10. **Be cautious online:** Don't click suspicious links, verify sender identities, and be wary of unsolicited requests

---

**Remember:** Cybersecurity is not a one-time effort but an ongoing process of learning, updating, and adapting to new threats.