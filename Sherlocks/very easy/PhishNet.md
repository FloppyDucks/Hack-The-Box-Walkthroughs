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
|Result| Meaning                                                                 |
-------|:-----------------------------------------------------------------------:|
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









