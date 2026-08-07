# Hacker Holidays 2026 Day 4

**Path:** Hacker Holidays 2026

**Room:** Packed Light

**Difficulty:** Easy

**Category:** Forensics

**Tags:** Network Forensics, PCAP Analysis, Cryptography


---

## Objective

Today's objective is to analyze the provided Wireshark capture file in order to find the encrypted data, as well as the encryption key to decode the data. 

---

## Steps I took:
### 1. Download the task file
Upon opening the room, I noticed there was no virtual machine to start, but instead a file to download. The task file downloaded as a ZIP folder, so I next extracted the file. 
Upon evaluation, I noticed that the provided file was a Wireshark capture. After noticing this, I had to download Wireshark to my computer. Once the installation had finished, I opened the file in Wireshark. 

### 2. Filter the Wireshark Capture
On the room card, user **@0xMia** had posted about the request headers. I decided to filter the capture by `http.request`. After doing this, I noticed that one request looked different from the rest. 
Packet 16 downloaded `/temp/updates.py HTTP/1.1 ` whereas the rest of the request only had `HTTP/1.1`. 

After realizing the key difference, I exported packet 16 as an HTTP object. 

### 3. Evaluate `updates.py`
I used VS Code to open the `updates.py` file. Within that file, I found the encryption code. From this, I learned that the data went from original characters > XOR > Base64. 

### 4. Extract the Cookies from Wireshark
Every packet that came through after `updates.py` was downloaded had a similar cookie structure. In order to find the cookies, I expanded the `Hypertext Transfer Protocol` and reviewed the `Cookie` header. 
I copied all the necessary data from the `Cookie` header into my notepad app. 

### 5. Decode using CyberChef
I started by pasting the encoded data I had gotten from the packets into CyberChef. Remembering that the encryption order went from original> XOR > Base64, I went in the reverse order. I added the recipe for Base64.
This still did not give me anything useful, as the data was still encoded with XOR. 

In order to get the key for XOR, I had to go back to the `updates.py` file, where I found the key. After having the key, I added the XOR recipe into CyberChef, choosing `utf-8`. I then pasted the key that I had gotten
from the `updates.py`, but still did not have my final answer. I slowly deleted one letter from the key until I had the expected output. This decrypted data provided the information I needed to complete the room. 

---

## Tools Used
 - Wireshark
 - CyberChef
 - VS Code

 ---

 ## Key Takeaways 
  - Used Wireshark filters to narrow down network traffic to review
  - Gained more experience with CyberChef and decoding data
  - Recognized and reversed a multi-step encryption process
    
