# **PhishNet**

**1)** We want to download the PhishNet.zip file from the HTB website & extract the file (password is "hacktheblue")...obviously 😄
<img width="1205" height="222" alt="image" src="https://github.com/user-attachments/assets/eafd8881-5aee-4039-a7ac-2ea4c509ced4" />


**2)** Once we have downloaded and extracted the file we should see an email file (.eml)
<img width="652" height="86" alt="image" src="https://github.com/user-attachments/assets/5139532c-90d5-43a7-aeb6-0d6e3cfbecd1" />

**3)** I recommend opening the file with both a text editor like notepad/notepad++ (if on windows) OR nano/vi/pluma/etc. (if on linux) 
<img width="970" height="686" alt="image" src="https://github.com/user-attachments/assets/4a9dee3b-1115-4a9b-b844-5cd31d9086c1" />

**4)** Now that we have the email opened in a text editor we can complete the first task: "*What is the originating IP address of the sender?*" 
Look for the line that says: X-Originating-IP: 
**_answer: [45.67.89.10]_**
