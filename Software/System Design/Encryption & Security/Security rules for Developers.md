---
date: 2024-10-09
tags: 
link: "[[System Design]]"
---

# Security rules for Developers

> Security is as much as important while developing the Software. Safeguarding user's data is inevitable, we are going to look into some functionalities how we can safeguard the user data.



## 1. Legal Obligation

- **General Data Protection Regulation** :  governs how the personal data of individuals in the European may be processed and transferred. 
	- Lawfulness
	- fairness
	- transparency
	- Purpose limitation
	- Data minimization
	- Accuracy; 
	- Storage limitation
	- Integrity and confidentiality
	- Accountability
	- These principles are found right at the outset of the GDPR, and inform and permeate all other provisions of that legislation.
- **HIPPA** : HIPAA includes the HIPAA Privacy Rule and the HIPAA Security Rule. The Privacy Rule establishes standards for protecting health information, while the Security Rule establishes standards for protecting electronic health information. 
- **California Consumer Privacy Act (CCPA)** : Consumers have the right to know what personal information is being collected, how it's used, and how to delete it. They also have the right to opt out of sharing or selling their personal information

#### 🔑Things to consider

- **PII (Personally identifiable information)** - any information that can be used to identify an individual. It should be stored safely in encryption	
- **Principle of minimalism** - need to get only the needed information from the user
- **Transparency** - Why you are collecting the information should be mentioned in the 'terms and conditions'
- **Anonymous** - Data should be stored in encrypted, so that if the data is hacked means it should be decrypted through only your application(code). Ex: hashing, salting

