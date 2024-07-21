# Phishing-Analysis-Project

## Objective

The primary objective of this project is to identify and analyze phishing emails, determine their intent and maliciousness, and identify appropriate defensive measures once they are identified.


### Skills Learned

- Understanding email headers, content, and attachments to spot suspicious elements.
- Recognizing common phishing tactics and indicators of compromise.
- Knowing the steps to take when a phishing email is identified, including reporting and mitigating the threat.
 
  
### Tools Used

- Sublime Text
- Wannabrowser
- DomainTools
- URL2PNG
- VirusTotal
  
  
  
## General Knowledge
Before I begin I will give a litle background on Sublime Text, Wannabrowser, DomainTools, URL2PNG and VirusTotal
<br>

Sublime is a text editor which I will be using for identifying and retrieving email artifacts.
<br>

Wannabrowser is a tool that allows you to simulate any browser, similar to using a virtual machine but specifically for browsers. It enables you to inspect where shortened URLs, such as malicious Bitly links, lead without actually clicking on them. Wannabrowser can show you the number of redirects a URL goes through and provide other insights into the behavior and final destination of the URL. This can be particularly useful for cybersecurity professionals who need to analyze suspicious links safely.
<br>

DomainTools allows me to perform reverse DNS lookups to see who owns a specific domain.
<br>

URL2PNG allows you to view an image of the webpage that a URL leads to, so you can see what the site looks like without actually visiting it.
<br>

VirusTotal is a free online service that analyzes files and URLs to identify malware and other security threats. It aggregates multiple antivirus engines and various scanning tools to provide users with comprehensive insights into the safety of files and websites.
<br>
<br>

## Author's Notes
During my studies at New York City College of Technology, my school received a lot of phishing emails, and many students fell victim to them because they looked either too enticing, urgent, or too real. Back when I was a student at City Tech, I always knew when an email felt suspicious or malicious, but I could only tell at a glance and didn't know how to analyze it to see if it was truly malicious or not. After finishing the BTL1 certification, I've learned how to identify, analyze, and remediate phishing emails, and this project will demonstrate my skills in doing so.
<br>
<br>
## Email 1
![Source1](https://github.com/user-attachments/assets/7f90f8e8-2782-4b9d-8f59-634d95047e0c)
The first red flag I instantly noticed in this email was the subject line, 'URGENT NOTICE: START APPLYING.' at the top of the email. This is a red flag because phishing emails often create a sense of urgency to get the targeted user to act quickly without thinking, which can lead them to click on a link that will inevitably compromise their machine. 
<br>
<br>
![Source1](https://github.com/user-attachments/assets/c77a3a6f-f8e0-4159-a16a-0c84e3bfe630)
Other red flags include the poor html styling that's suppost to represent the school's logo, as well as telling you to "click the link".
<br>
<br>
To begin this analysis, I will start by retrieving artifacts from this potential phishing email. I will do so by using a tool called Sublime Text.
<br>
![Art1](https://github.com/user-attachments/assets/37fd94b9-f5be-4285-aeb4-773209c75c2a)
<br>
Looking at the first three artifacts, I see that the email was sent from 'Muhammad Jawad' with the email address Muhammad[.]Jawad@mail[.]citytech[.]cuny[.]edu. The subject of the email was 'URGENT NOTICE: START APPLYING,' which we already knew. The email was sent on Monday, July 15, 2024, at 14:14:56 +0000.
<br>
<br>
![Art2](https://github.com/user-attachments/assets/da1f95b2-f2ed-40af-b77a-65613b6261d8)
Looking at the fourth artifact, this represents the URL's the sender wants us to click on. We can futher analyze where this url takes us with tools such as URL2PNG and Wannabrowser.
<br>
<br>
![Art 3](https://github.com/user-attachments/assets/ef4c6c4d-c9bf-409b-a315-663c7f90e0ab)
Looking at these artifacts from sublime, it can tell me many things. The hostnames "BN0PR02MB8031.namprd02.prod.outlook.com" and "CYYPR02MB9885.namprd02.prod.outlook.com" indicate that these servers are part of the Outlook.com (Microsoft) infrastructure. <br> 

The "Received" headers show that the email was relayed between servers within the same domain (namprd02.prod.outlook.com), suggesting internal routing. <br>

Based on the headers, the specific path the email took was: the email was sent from "BN0PR02MB8031.namprd02.prod.outlook.com (2603:10b6:408:16e::14) and was sent to CYYPR02MB9885.namprd02.prod.outlook.com (2603:10b6:930:c5::11).

The private IPv6 address "fe80::9825:8d42:959f:1a17" circled in green indicates that this email originated from an internal network, meaning it didn't come from the internet. This IPv6 address is a link-local address, which is used within a single network segment and is not routable on the broader internet. <br><br>

If a potential phishing email came from an internal network, it can tell me many things such as: <br>
1: Compromised Internal Accounts: An attacker who has compromised an internal account (e.g., through phishing, malware, or credential theft) used that account to send phishing emails from within the organization. These emails might target other employees or external contacts.

2: Insider Threats: An insider with malicious intent might deliberately send phishing emails from within the organization's network. This could be done to steal sensitive information, cause disruption, or for other malicious purposes.

3: Spoofing: The Phishing email can be crafted to appear as though they come from internal sources, even if they are not. For example, attackers might spoof internal email addresses or domains to make their emails seem legitimate and bypass external security filters.

4: Internal Phishing Campaigns: In some cases, the organization might launch phishing campaigns against their own organization to test internal security measures or train employees to recognize phishing attempts.
<br>
<br>
I'm not really sure which is the case as of now, so I will dig deeper and analyze these artifacts futher to discover the truth behind this email.
<br>
<br>
![Art4](https://github.com/user-attachments/assets/675c4b6e-3e06-4c25-ab3c-48c4db7bdd90)
<br>
Looking at more information provided by Sublime Text, I can see that this email wasn't signed by DKIM (DomainKeys Identified Mail). This means that the email's authenticity and integrity cannot be verified through DKIM. In other words, unsigned emails are more likely to be phishing attempts, as DKIM helps to prevent email spoofing. At the same time, there can be possible legitimate reasons, such as the sender's domain not being configured to use DKIM or a misconfiguration in the email sending system. In essence, while the absence of a DKIM signature does not automatically mean an email is malicious, it does reduce the level of trust and verification that can be applied to the email. <br>

Additionally, this email didn't have an SPF (Sender Policy Framework) record either, which is a red flag. I've analyzed a legitimate email the school sent, and it had an SPF. If a potential phishing email doesn't have an SPF record, this suggests the email might not have been sent through the organization's legitimate and authorized email servers.

## Email 1 Artifact Overview <br>
Sending Address: Muhammad[.]Jawad@mail[.]citytech[.]cuny[.]edu <br>
Subject line: URGENT NOTICE: START APPLYING <br>
Recipients: none <br>
Reply-to: none <br>
Date/time: Monday, July 15, 2024, at 14:14:56 +0000 <br>
Sending Server IP: 2603:10b6:408:16e::14 <br>
Reverse DNS: BN0PR02MB8031.namprd02.prod.outlook.com <br> 
URLs: <br>
hxxps://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fforms.gle%2FrFDnUFD3CoX1UxA27&data=05%7C02%7C%7C5161dc9668084c5ec93f08dca4d880f8%7C252ec9a0a12c49f9ba6628624defd571%7C0%7C0%7C638566497025889836%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=ZYhxUn%2BxvTNQOkEINp0ttmIAVCuow8i5R%2FCb%2BcpyQAw%3D&reserved=0 <br>AND <br> 
hxxps://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fforms.gle%2FrFDnUFD3CoX1UxA27&data=05%7C02%7C%7C5161dc9668084c5ec93f08dca4d880f8%7C252ec9a0a12c49f9ba6628624defd571%7C0%7C0%7C638566497025899129%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=Ilh6La%2B%2Fb8v7twK6PyOo4BFPf%2FU3oFC%2F%2FYMTE5UlgRU%3D&reserved=0 <br><br>







 



















