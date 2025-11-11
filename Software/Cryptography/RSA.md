---
date: "2025-11-11"
tags: 
link:
---

# RSA

> RSA(**R**ivest-**S**hamir-**A**dleman) Algorithm is an **asymmetric** or public-key cryptography algorithm which means it works on two different keys: **Public Key and Private Key. The Public Key is used for encryption and is known to everyone, while the Private Key is used for **decryption** and must be kept secret by the receiver. RSA Algorithm is named after Ron Rivest, Adi Shamir and Leonard Adleman, who published the algorithm in 1977.

Example of Asymmetric Cryptography:

If Person A wants to send a message securely to Person B:

- Person A encrypts the message using Person B's Public Key.
- Person B decrypts the message using their Private Key.

### RSA Algorithm

> RSA Algorithm is based on factorization of large number and modular arithmetic for encrypting and decrypting data. It consists of three main stages:
> 
> 1. Key Generation: Creating Public and Private Keys
> 2. Encryption: Sender encrypts the data using Public Key to get cipher text.
> 3. Decryption: Decrypting the cipher text using Private Key to get the original data.