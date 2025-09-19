# **PhishNet**

**1)** We want to download the PhishNet.zip file from the HTB website & extract the file (password is "hacktheblue")...obviously 😄
<img width="1205" height="222" alt="image" src="https://github.com/user-attachments/assets/eafd8881-5aee-4039-a7ac-2ea4c509ced4" />


**2)** Once we have downloaded and extracted the file we should see an email file (.eml)
<img width="652" height="86" alt="image" src="https://github.com/user-attachments/assets/5139532c-90d5-43a7-aeb6-0d6e3cfbecd1" />

**3)** I recommend opening the file with both a text editor like notepad/notepad++ (if on windows) OR nano/vi/pluma/etc. (if on linux) 
<img width="610" height="185" alt="image" src="https://github.com/user-attachments/assets/f224adbd-c48c-4409-8b75-98e4891c8098" />

**4)** Now that we have the email opened in a text editor we can complete the first task: "**_"What is the originating IP address of the sender?"_**
Look for the line that says: X-Originating-IP: 

<img width="257" height="25" alt="image" src="https://github.com/user-attachments/assets/94b58749-d5c2-4bd4-a7a2-1d9e973877f4" />

**_answer: 45.67.89.10_**

**5)** Next **_"Which mail server relayed this email before reaching the victim?"_** If we look in the file we will see 3 lines with 3 IP's 
<img width="485" height="158" alt="image" src="https://github.com/user-attachments/assets/af59a7ca-8758-41f9-a106-9eca2bf88714" />
....So how do we know which one is the right one? well we can guess and check because HTB is forgiving with wrong answers. BUT if this were a test, OR if its an interview question/ real life Incident Response how would we know? the best way to determine is look at the last hop...aka the last IP in the chain. aka 10:15:10 was the last one sent, and the IP associated to that is 203.0.113.25 so...

**_answer: 203.0.113.25_**

**6)** **_What is the sender's email address?_** This one is nice and easy, we look at the very first line, and there is your answer
<img width="360" height="25" alt="image" src="https://github.com/user-attachments/assets/b7c82327-247c-4b3f-be59-8c4ce4a8bb7c" />
...but why not the Reply-To? that is because it is only used when you hit reply in an email. the Return-Path is the true sender of the email. If it cannot find where the email should go, that is where it will be bounced to. Hence we use the Return-Path email

**_answer: finance@business-finance.com_**

**7)** **_What is the 'Reply-To' email address specified in the email?_** This is another easy one, its the second line...it pretty much gives you the answer.

**_answer: support@business-finance.com_**

**8)** **_What is the SPF (Sender Policy Framework) result for this email?_** 

 How SPF results are reported?

Common SPF results:
|Result|                           Meaning                                          |
|:-------:|:-----------------------------------------------------------------------:|
| Pass	| The email came from an IP allowed by the domain’s SPF record Legitimate |
| Fail	| The email came from an IP not listed in the domain’s SPF record Likely spoofed |
| SoftFail | IP not listed but not outright rejected |
| Neutral | No specific policy cannot verify |
| None | Domain has no SPF record |

so for our case we need to look for SPF in the file, and we can see it says Pass

<img width="949" height="22" alt="image" src="https://github.com/user-attachments/assets/805bc95b-6ed4-4e91-ac3e-e002df51a42b" />

**_answer: Pass_**

**9)** **_What is the domain used in the phishing URL inside the email?_** For this we need to look for a link, not an email address, but an https://.... and if we do a search for https. Low and Behold we get 1 instance

<img width="939" height="22" alt="image" src="https://github.com/user-attachments/assets/22eee76d-80a8-4752-88c0-97c1ec144b26" />

so the answer is secure.business-finance.com...why not the parent domain business-finance.com...because its asking what is the domain of the phishing email, and as we see above we are getting the link from secure.business-finance.com NOT just business-finance.com....Hence the phishing domain is secure.business-finance.com

**_answer: secure.business-finance.com_**

**10)** **_What is the fake company name used in the email?_** There are a few ways to do this, I found it easier to find the answer if you open the email in an email viewer instead of notepad...I will be using **_Mozilla thunderbird_** because I dont need to sign into outlook...and fuck outlook...BUT you can use any preferred email viewer
<img width="1358" height="678" alt="image" src="https://github.com/user-attachments/assets/22e39e46-e778-4c51-a293-ec39ce4692f5" />

At the bottom we will see Buisness Finance Ltd. AND that is our answer...nice and easy

**_answer: Business Finance Ltd._**

**11)** **_What is the name of the attachment included in the email?_** We can complete this either way, if you are already looking at the email viewer look for the attachment name and there is your answer...IF you are doing text file only then scroll to the bottom of the file and look for filename. We will see the name of "Invoice_2025_Payment.zip" 

**_answer: Invoice_2025_Payment.zip_**

**12)** **_What is the SHA-256 hash of the attachment?_** To get the sha-256 Download the file Invoice_2025_Payment.zip by downloading the zip file by viewing the email via some email viewer/ email client. Again im using **_Mozilla thunderbird_**, but you can use whatever. Once you have the file downloaded open up the command line interface either powershell if you are on windows, OR terminal on linux. If you are on windows go to the directory where you downloaded the .zip file and run **_Get-FileHash Invoice_2025_Payment.zip_**
IF you are on linux, similar deal, go to the directory where you downloaded it. and run **_sha256sum Invoice_2025_Payment.zip_**...Either way you should get the same answer

<img width="740" height="66" alt="image" src="https://github.com/user-attachments/assets/e476359d-5382-4079-a467-bd87b71a5f36" />

<img width="827" height="47" alt="image" src="https://github.com/user-attachments/assets/3b9150d7-15f2-4892-a453-3716ec8589a8" />

**_answer: 8379C41239E9AF845B2AB6C27A7509AE8804D7D73E455C800A551B22BA25BB4A_**

**13)** **_What is the filename of the malicious file contained within the ZIP attachment?_** This was the hardest one...for me. If you try and unzip the file on windows you will get this error:

<img width="612" height="450" alt="image" src="https://github.com/user-attachments/assets/288dc2c3-89a9-4086-8d32-1111ada81d08" />

If you try doing it via CLI it will tell you the .zip file isnt actually a zip archive which is a hint! and odd. 
<img width="844" height="179" alt="image" src="https://github.com/user-attachments/assets/65846c19-5248-4636-b6bd-5bbc9ed33ff9" />

Because if you check the file type it says zip archive

<img width="875" height="48" alt="image" src="https://github.com/user-attachments/assets/4d63a83a-56ea-4336-99f1-ccf1d8cf625a" />

So lets run a hexdump (on linux) **_hexdump -C Invoice_2025_Payment.zip_** OR of you are on windows **_Format-Hex .\Invoice_2025_Payment.zip | Select-Object -First 16_**

<img width="699" height="149" alt="image" src="https://github.com/user-attachments/assets/728853ab-55ce-4fd7-b951-c094ea1bf160" />

<img width="716" height="133" alt="image" src="https://github.com/user-attachments/assets/88cd3e53-3c0d-4de6-8a01-1cd9a941ca19" />

As we can see there is a file in the hexdump... 

**_answer: invoice_document.pdf.bat_**

**14)** **_Which MITRE ATT&CK techniques are associated with this attack?_** For this we can use google or ChatGPT....same with the rest, but this is easy to find online Phishing: Spearphishing Attachment

**_answer: T1566.001_**
