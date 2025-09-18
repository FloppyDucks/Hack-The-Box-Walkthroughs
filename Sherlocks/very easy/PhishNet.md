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




