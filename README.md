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
- URL2PNG
  
  
  
## General Knowledge
Before I begin I will give a litle background on Sublime Text, Wannabrowser, DomainTools, URL2PNG and VirusTotal
<br>

Sublime is a text editor which I will be using for identifying and retrieving email artifacts.
<br>

Wannabrowser is a tool that allows you to simulate any browser, similar to using a virtual machine but specifically for browsers. It enables you to inspect where shortened URLs, such as malicious Bitly links, lead without actually clicking on them. Wannabrowser can show you the number of redirects a URL goes through and provide other insights into the behavior and final destination of the URL. This can be particularly useful for cybersecurity professionals who need to analyze suspicious links safely.
<br>

URL2PNG allows you to view an image of the webpage that a URL leads to, so you can see what the site looks like without actually visiting it.

<br>

## Author's Notes
During my studies at New York City College of Technology, my school received a lot of phishing emails, and many students fell victim to them because they looked either too enticing, urgent, or too real. Back when I was a student at City Tech, I always knew when an email felt suspicious or malicious, but I could only tell at a glance and didn't know how to analyze it to see if it was truly malicious or not. After finishing the BTL1 certification, I've learned how to identify, analyze, and remediate phishing emails, and this project will demonstrate my skills in doing so.
<br>
<br>
## Suspicious Email 
![Source1](https://github.com/user-attachments/assets/7f90f8e8-2782-4b9d-8f59-634d95047e0c)
The first red flag I instantly noticed in this email was the subject line, 'URGENT NOTICE: START APPLYING.' at the top of the email. This is a red flag because phishing emails often create a sense of urgency to get the targeted user to act quickly without thinking, which can lead them to click on a link that will inevitably compromise their machine. Another red flag is the very vague "Hey There" can indicate a mass phishing attempt rather than a personalized message from a legitimate source.
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
hxxps://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fforms.gle%2FrFDnUFD3CoX1UxA27&data=05%7C02%7C%7C5161dc9668084c5ec93f08dca4d880f8%7C252ec9a0a12c49f9ba6628624defd571%7C0%7C0%7C638566497025899129%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=Ilh6La%2B%2Fb8v7twK6PyOo4BFPf%2FU3oFC%2F%2FYMTE5UlgRU%3D&reserved=0 <br>

## Wannabrowser Analysis <br>
First, I will utilize the tool "WannaBrowser" to see what happens if a user clicks on both URLs in the email. To do this, I will simply copy and paste the URL into Wannabrowser and select the GET request option. <br>
![ana1](https://github.com/user-attachments/assets/3338a485-529e-4d29-a3ea-627fc495039b)
This screenshot from Wannabrowser tells many stories, and i'll be breaking everything down. <br> 

The URL I copied and pasted from the email is at the top, and I selected a GET request, meaning Wannabrowser is going to send a GET request to download the webpage.<br> 

The User-Agent is the type of browser making the request on my behalf, so in this case, it's Safari. The URL circled in blue indicates the actual URL from the email, unmasked. As you can see, it looks like it's going to a Google Forms page. Wannabrowser states this URL had two redirects, meaning that when you click on the link, it first takes you to one webpage, then redirects you to another webpage. In this case, it seems to bring you to the Google Forms webpage first, then instantly redirects you to a different webpage. <br>

Looking at the Header(s), the HTTP1.1 302 Found status code tells me that the requested resource has temporarily moved to a different URL. The client is redirected to this new URL, but should use the original URL for future requests. We know this because this is where the original URL from the email was unmasked, which revealed the the google forms webpage. <br>

![ana2](https://github.com/user-attachments/assets/44d5d373-fa42-4965-b445-56011b132a2b) <br>
If we scroll down further, we can see that the "Location" field shows the Google Forms webpage that was unmasked. From the Google Forms webpage, it then redirects the client to the same webpage. Judging by the status code 200 OK, this indicates that the client successfully accessed the redirected URL and received a valid response. 
<br> <br>
You may be wondering why there is a redirection to the same URL. There can be several malicious reasons for this. Some of them include: <br> 
Phishing: An attacker could use redirects to obscure the true destination of a page, potentially tricking users into thinking they are on a legitimate site when they are not.<br>

Session Hijacking: Malicious redirects could be used to manipulate session cookies or tokens, potentially leading to session hijacking or unauthorized access.

Cross-Site Scripting (XSS): If the redirect URL contains parameters that can be manipulated, attackers might use them to inject malicious scripts or capture sensitive information. Additionally, malicious actors might use redirects to track user behavior or gather information about users in ways that aren't immediately obvious. There are many potential malicious reasons why a redirection to the same URL might be used.
<br> <br>

I ran the same analysis using WannaBrowser on the second URL from the email, the one under "Apply Now," and it revealed the same unmasked URL as the first one. This is both strange and suspicious.
<br><br>
## URL2PNG Analysis <br>
Second, I will utilize the tool URL2PNG to see what the actual webpage looks like and it's contents. <br>
![ana3](https://github.com/user-attachments/assets/f72dd0c5-bcc7-45af-9f00-3b2936a26782) <br>
As you can see, URL2PNG shows a screenshot of what the landing page looks like for this webpage and it seems like the google forms is asking the user some interesting personal information. To get a better look I will right click on the image and select inspect. <br>
![ana4](https://github.com/user-attachments/assets/3ee6e495-6089-48c1-9336-eb4d44665bd8) <br>
Where it says img id="sample" etc, I'm going to copy the image id sample url next to it and paste it into a new browser tab. <br>
![ana5](https://github.com/user-attachments/assets/32ea8482-63be-4f13-bfd8-5f43c71d3d3b) <br>
Looking at this google forms, my red flag alerts are shooting through the roof. At the top of the forms, I can see who ever the malicious actor was, utilized Citytech's logo and name to make it seem it came from the school, which can fool users think it's legitimate. <br> <br> 

Looking at the text, it states that your job title will be "Feedback Agent" and that you will be paid for shopping at various retail stores and providing feedback on the items purchased. It further specifies, "You will receive your payment and task funds as Certified or Electronic Checks by mail. It is important to cash or deposit the check before beginning your shopping.". The task involves buying items from different retail stores using funds provided by the company in the form of certified or electronic checks sent by mail, and you would get paid $450 for each task completed. The idea of getting paid for shopping and reviewing items sounds like an easy money-making scheme (and I’m being sarcastic). This is obviously a scam. <br><br>

Additionally, why is the form asking, "Do you own a credit card?" If the employee is supposed to be shopping on behalf of the company, wouldn't they provide a prepaid card or a company-owned credit/debit card to ensure that the employee doesn’t accidentally overspend? This adds to the suspicion that this offer is very dubious indeed.<br><br> 

Looking at the other questions on this form, it's safe to assume this is a case of information or data harvesting. Data harvesting involves collecting sensitive or personal information, such as Personally Identifiable Information (PII) including names, addresses, phone numbers, or even Social Security numbers, as well as financial information like credit card numbers, bank account details, or transaction history. The goal is typically to gather data that can be used for further attacks or identity theft.<br><br>

URLPNG doesn't allow me to fully scroll all the way to the bottom of the webpage to see the rest of the questions being asked in this form, but based on the PII it already asked, it's safe to assume it gets more personal at the bottom. <br> <br>

## Malicous Email Report <br>
![original](https://github.com/user-attachments/assets/b2d0c80d-c3cd-4345-bfa3-86ce67dbcdb3) <br>
Email description: <br>
The email uses social engineering techniques such as impersonation, by posing as Citytech, and emotional appeals. It also includes an unsolicited offer, presenting a potential job opportunity with flexible hours and decent pay to attract interest.<br>

Email Artifacts: <br>
Sending Address: Muhammad[.]Jawad@mail[.]citytech[.]cuny[.]edu <br>
Subject line: URGENT NOTICE: START APPLYING <br>
Recipients: none <br>
Reply-to: none <br>
Date/time: Monday, July 15, 2024, at 14:14:56 +0000 <br>
Sending Server IP: 2603:10b6:408:16e::14 <br>
Reverse DNS: BN0PR02MB8031.namprd02.prod.outlook.com <br> 
URLs: <br>
hxxps://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fforms.gle%2FrFDnUFD3CoX1UxA27&data=05%7C02%7C%7C5161dc9668084c5ec93f08dca4d880f8%7C252ec9a0a12c49f9ba6628624defd571%7C0%7C0%7C638566497025889836%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=ZYhxUn%2BxvTNQOkEINp0ttmIAVCuow8i5R%2FCb%2BcpyQAw%3D&reserved=0 <br>AND <br> 
hxxps://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fforms.gle%2FrFDnUFD3CoX1UxA27&data=05%7C02%7C%7C5161dc9668084c5ec93f08dca4d880f8%7C252ec9a0a12c49f9ba6628624defd571%7C0%7C0%7C638566497025899129%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=Ilh6La%2B%2Fb8v7twK6PyOo4BFPf%2FU3oFC%2F%2FYMTE5UlgRU%3D&reserved=0 <br>

Artifact Analysis: <br>
A reverse DNS search on the sending server IP shows that this email originated from an internal server within the school's domain<br>

Wannabrowser and URL2PNG shows the URL redict's the client into a malicous personal/data harvester on google forms. <br>

Defensive Measures: <br>
The sender of the email came from an official CityTech domain and was deemed internal. We are unable to block the server domain or IP because it may interfere with legitimate emails being sent, so I will block the subject line: <br>
Subject Line Block (Email Gateway) "URGENT NOTICE: START APPLYING" on 7/21/2024 at 7:22 PM by Marc P. <br>

The URL within the email is deemed malicious because it is extracting personal data on who ever completes the form. Since docs.google.com is a legitimate domain used by employee's or students, we are unable to block the entire domain. Instead I will block the entire URL because it's extremly specific and will only block the URL that has been provided. <br>
URL Block (Web Proxy) "hxxps://docs.google.com/forms/d/e/1FAIpQLSdtQPCT5O8AwvyRMM6aebsNgMSAogLbpEMGCKFmOMiy7mUe7w/viewform?usp=send_form" on 7/21/2024 at 7:24 PM by Marc P.
<br> <br>

# Project Concluded




























 



















