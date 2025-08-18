

# 🔐 Security Notes

## 1. Properties of Secure Communication

(Also known as the **CIA Triad + Extensions**)

1. **Confidentiality**

   * Protects information from unauthorized access/disclosure.
   * Example: Encrypting emails so only the intended recipient can read them.
   * Loss = Unauthorized disclosure of data.

2. **Integrity**

   * Ensures information is accurate, unmodified, and reliable.
   * Example: Hash checksums (MD5, SHA) to confirm files weren’t tampered with.
   * Loss = Unauthorized modification/destruction of data.

3. **Availability**

   * Ensures timely and reliable access to data/systems.
   * Example: Servers being online 24/7 for banking systems.
   * Loss = System downtime (e.g., DoS attack).

👉 Additional Concepts:

* **Authenticity** – Verifying that users/data sources are genuine (e.g., login with password).
* **Accountability** – Actions are traceable to individuals (e.g., system logs, audit trails).

---

## 2. Cryptographic Components

* **Plaintext** → Original readable message.
* **Encryption Algorithm** → Scrambles plaintext using transformations/substitutions.
* **Secret Key** → Independent value that controls encryption/decryption.
* **Ciphertext** → Output scrambled data (unintelligible).
* **Decryption Algorithm** → Reverse process, converts ciphertext back to plaintext using a key.

🔑 Example:
Message = “HELLO”
Key = Secret passphrase
Ciphertext = “X9@#F1”

---

## 3. Symmetric vs Asymmetric Cryptography

| Feature         | Symmetric (Secret Key)                   | Asymmetric (Public + Private Keys)                 |
| --------------- | ---------------------------------------- | -------------------------------------------------- |
| Keys            | One key for both encryption & decryption | Two keys (public for encrypt, private for decrypt) |
| Speed           | Fast                                     | Slow                                               |
| Data Size       | Large data                               | Small data                                         |
| Security        | Lower (only one key)                     | Higher (two-key system)                            |
| Confidentiality | ✅ Yes                                    | ✅ Yes + authenticity + non-repudiation             |
| Key Length      | 128/256 bits                             | 2048+ bits                                         |
| Efficiency      | High (for bulk data)                     | Low (used for key exchange & digital signatures)   |
| Examples        | AES, DES, RC4                            | RSA, ECC, Diffie-Hellman                           |

💡 Real Use:

* Symmetric → Encrypting files, streaming.
* Asymmetric → Digital signatures, SSL certificates.

---

## 4. Types of Attacks

* **Passive Attacks**

  * Goal: Learn/gather information, no modifications.
  * Examples: Eavesdropping, traffic analysis.

* **Active Attacks**

  * Goal: Alter system resources or disrupt operations.
  * Examples: Man-in-the-Middle (MITM), DoS, data modification.

---

## 5. Digital Signature

* A **digital code** that uniquely identifies the sender & ensures integrity.
* Introduced by **Whitfield Diffie (1976)**.

🔎 **How it works:**

1. Sender creates a **message**.
2. A **hash (message digest)** of the message is generated.
3. Sender encrypts the digest with their **private key** → this is the **digital signature**.
4. Signature is attached to the message.
5. Message + signature encrypted with recipient’s **public key**.
6. Recipient decrypts with their **private key**.
7. Recipient verifies the digest to confirm integrity & authenticity.

✅ Guarantees:

* **Source authentication** (proves sender identity).
* **Message integrity** (detects tampering).
* **Non-repudiation** (sender cannot deny sending).

---

## 6. Message Authentication Code (MAC) *(brief mention in PDF)*

* Like a digital signature but **uses a shared secret key**.
* Verifies both data integrity & authenticity.
* Common in symmetric encryption.

---

# 🎯 Quick Exam-Ready Recap

* **CIA Triad**: Confidentiality, Integrity, Availability + (Authenticity, Accountability).
* **Crypto Components**: Plaintext, Ciphertext, Key, Encryption/Decryption Algorithm.
* **Symmetric vs Asymmetric**: One key vs Two keys, fast vs slow, less secure vs more secure.
* **Attacks**: Passive (listen) vs Active (modify).
* **Digital Signature**: Hash + private key → verify with public key (ensures authenticity, integrity, non-repudiation).

---

