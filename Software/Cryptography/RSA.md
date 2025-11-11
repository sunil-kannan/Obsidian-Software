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


### Advantages

- **Security:** RSA algorithm is considered to be very secure and is widely used for secure data transmission.
- **Public-key cryptography:** RSA algorithm is a public-key cryptography algorithm, which means that it uses two different keys for encryption and decryption. The public key is used to encrypt the data, while the private key is used to decrypt the data.
- **Key exchange:** RSA algorithm can be used for secure key exchange, which means that two parties can exchange a secret key without actually sending the key over the network.
- **Digital signatures:** RSA algorithm can be used for digital signatures, which means that a sender can sign a message using their private key, and the receiver can verify the signature using the sender's public key.
- **Widely used:** Online banking, e-commerce, and secure communications are just a few fields and applications where the RSA algorithm is extensively developed.

### Disadvantages

- **Slow processing speed:** RSA algorithm is slower than other encryption algorithms, especially when dealing with large amounts of data.
- **Large key size:** RSA algorithm requires large key sizes to be secure, which means that it requires more computational resources and storage space.
- **Vulnerability to side-channel attacks:** RSA algorithm is vulnerable to side-channel attacks, which means an attacker can use information leaked through side channels such as power consumption, electromagnetic radiation, and timing analysis to extract the private key.
- **Limited use in some applications:** RSA algorithm is not suitable for some applications, such as those that require constant encryption and decryption of large amounts of data, due to its slow processing speed.
- **Complexity:** The RSA algorithm is a sophisticated mathematical technique that some individuals may find challenging to comprehend and use.
- **Key Management:** The secure administration of the private key is necessary for the RSA algorithm, although in some cases this can be difficult.
- **Vulnerability to Quantum Computing:** Quantum computers have the ability to attack the RSA algorithm, potentially decrypting the data.