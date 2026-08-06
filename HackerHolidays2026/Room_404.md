# Hacker Holidays 2026 Day 2

**Path:** Hacker Holidays 

**Room:** Room 404

**Difficulty:** Very Easy

**Category:** Web 

**Tags:** Web, Directory Enumeration 


---

## Objective

The objective of this room was to search the website and find the exposed source code. 

---

## Steps I took:
### 1. Find the Open Door 
I started by taking the IP address of the lab machine and ran namp. Before running nmap I created a file that I stored the nmap output into. By doing this I learned that there was something running on port 8080, as well as that on port 8080 there was an exposed git repository.

I ran nmap using the following tags:
 - sC, which runs a set of default scripts
 - sV, which probes the open ports to find what is running
 - oN, which saves the scan to a normal text file that is specified
   
### 2. Install git-dumper
After determmining that there was an exposed git repository, I ran ```pip install git-dumper``` so that git-dumper would be installed. 
### 3. Run git-dumper
After installing git-dumper, I dumped the repository into a file called loot. I was then able to run ```ls -la loot``` to expose all the files from the git repository, including the README.md file. Finally I ran ```cat README.md``` to get the necessary information to complete the room. 
 

---

## Tools Used
 - nmap
 - git-dumper

 ---

 ## Key Takeaways 
  - nmap is used to test all open ports 
  - 
  - 
  -
