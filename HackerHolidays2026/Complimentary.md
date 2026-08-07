# Hacker Holidays 2026 Day 3

**Path:** Hacker Holidays 2026

**Room:** Complimentary 

**Difficulty:** Easy

**Category:** Cloud

**Tags:** Cloud, AWS, Cognito, IAM Misconfiguration 


---

## Objective

The objective of this room is to find the AWS credentials that are accidentally made public and use them to dump the database table containing guest information.

---

## Steps I took:
### 1. Open Dev Tools
I started by going to the provided target website and opening up dev tools. After I had dev tools open, I reloaded the page so that I could get the network response information. 
Within the Network tab, I looked specifically for the response provided for the `app.js` file. 

I was able to retrieve the values for : 
- `IDENTITY_POOL_ID`
- `AWS_REGION`
- `TABLE_NAME`
- As well as the configuration for all the values listed above.
  
### 2. Retrieve the IdentityID
Using the information I found in the first step, I ran ```aws cognito-identity get-id \ --region us-east-1 \ identity-pool-id "identity pool id"``` 
(I have replaced the actual identity-pool-id for the sake of this write-up). This command gave me the unique IdentityID for the current session. 

### 3. Get Credentials 
After retrieving the IdentityID for the current session, I ran ```aws cognito get-credentials-for-identity \ --region us-east-1 \ --identity-id "identityID"``` 
(Again, I have replaced the actual identity ID). 

This command provided me with: 
- `AccessKeyId`
- `SecretKey`
- `SessionToken`
- `Expiration`

### 4. Export the temp credentials into the terminal
After receiving the temporary credentials, I exported the AccessKeyId, the SecretKey, the SessionToken, and the default region as environment variables. 

To export, I ran  `export AWS_ACCESS_KEY_ID="AccessKeyId"` (I ensured to copy the actual access key when exporting.) I did this for all four variables. 

### 5. Verify IAM role 
Next, I ran `aws sts get-caller-identity` and ensured that my role was listed as `complimentary-cognito-unauth-role`. 

### 6. Scan the database
Finally, I was able to scan the database and retrieve all the records in the guest information table. In dumping this database, I found the required information to complete the room. 

The command I ran to dump the table was `aws dynamodb scan --table-name complimentary-GuestWellnessProfiles`

---

## Tools Used
 - DevTools 
 - AWS Cognito 

 ---

 ## Key Takeaways 
  - Cognito can be used to retrieve temporary AWS credentials
  - DevTools can be used to expose JavaScript files from the client-side 
  - Gained an understanding of how IAM Misconfiguration can lead to sensitive data being exposed

