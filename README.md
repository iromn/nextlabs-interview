# NextLabsInterview

### Section C

Write and share a small note about your choice of system to schedule periodic tasks (such as downloading list of ISINs every 24 hours). Why did you choose it? Is it reliable enough; Or will it scale? If not, what are the problems with it? And, what else would you recommend to fix this problem at scale in production?

```
I personally use ClickUp which is a task management and project management platform 
that includes features for scheduling periodic tasks.

Reasons for Choosing ClickUp:
1. User-friendly interface and easy setup.
2. Availability of recurring task functionality.
3. Collaboration features and notifications.

Reliability and Scalability:
1. ClickUp's free version is reliable enough for my current needs.
2. It may have limitations when it comes to scaling up as my requirements grow.
3. Potential issues can arise in handling larger volumes of tasks or involving more team members.

Recommendations for Production-scale Solution:
1. Evaluate ClickUp's paid plans for additional features and scalability options.
2. Integration with automation tools or scripting solutions can optimize task execution and enhance scalability.
```

Suppose you are building a financial planning tool - which requires us to fetch bank statements from the user. Now, we would like to encrypt the data - so that nobody - not even the developer can view it. What would you do to solve this problem?

```
I would follow the below steps:

1. Client-Side Encryption: Implement client-side encryption, where the encryption process occurs on the user's device before the data is sent to your servers. This way, the sensitive information never leaves the user's device in plaintext form.
2. Strong Encryption Algorithm: Utilize a strong encryption algorithm.
3. Key Management: Implement a secure key management system. Generate a unique encryption key for each user and store it securely.
4. Secure Transmission: Ensure secure transmission of encrypted data from the user's device to the servers. This protects against eavesdropping and tampering during data transmission.
5. Secure Storage: Store the encrypted data in a secure and protected environment, such as an encrypted database or encrypted file storage. Regularly update and patch the software and systems to address any vulnerabilities that may arise.
6. Access Control: Implement strict access controls and authentication mechanisms to restrict access to the encrypted data. Only authorized personnel should have access to the decryption keys and systems.
7. Privacy Policy: Clearly communicate your data privacy practices to users through a privacy policy. Assure them that their data will be encrypted and stored securely, and outline the measures you have taken to protect their information.
8. Compliance: Ensure compliance with applicable data protection regulations, such as the General Data Protection Regulation (GDPR) or any other relevant laws specific to your jurisdiction. Follow the necessary guidelines and procedures to protect user data and privacy.
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).



