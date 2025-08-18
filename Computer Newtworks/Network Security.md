
# 🔐 Detailed & Easy Security Notes

---

## 1. Properties of Secure Communication (CIA + AA 🔑)

When two parties communicate (say you sending a WhatsApp message to your friend), the message needs to be **secure**. Security has some important properties:

### (a) **Confidentiality** (🔒 Privacy)

* Only the **intended person** should read the message.
* If someone else sees it → confidentiality is broken.
* **Example:** When you send a WhatsApp message, it is encrypted so hackers cannot read it.

👉 *Think of it like sealing a letter inside an envelope.*

---

### (b) **Integrity** (✍️ No Tampering)

* Ensures data is **not modified** during transmission.
* Even a small change should be detected.
* **Example:** If you send “Pay 500 Taka” and it arrives as “Pay 5000 Taka”, integrity is broken.
* Hash functions (MD5, SHA) help verify integrity.

👉 *Like sealing a parcel – if the seal is broken, you know it’s tampered.*

---

### (c) **Availability** (🟢 Always Accessible)

* Data and systems should be available **whenever needed**.
* **Example:** Online banking should work 24/7 – if hackers launch a DoS attack, service becomes unavailable.

👉 *Like electricity: if it’s cut off, the service is useless.*

---

### (d) **Authenticity** (✔️ Genuine)

* Verifies the sender/receiver is **who they claim to be**.
* **Example:** Logging in with username + password, or OTP in mobile banking.

👉 *Like showing your ID card at an exam hall.*

---

### (e) **Accountability** (📜 Responsibility)

* Every action should be traceable to the person who did it.
* **Example:** A company keeps activity logs (who logged in, what was changed). If data is stolen, they can trace the culprit.

👉 *Like CCTV cameras in a shop – you can see who did what.*

---

## 2. Cryptographic Components (Building Blocks 🧱)

When we talk about **cryptography** (secret writing), these are the basic parts:

1. **Plaintext** → The original readable message.

   * Example: `"Hello, meet me at 5 pm."`

2. **Encryption Algorithm** → A set of rules that scrambles the plaintext.

   * Example: AES, DES.

3. **Secret Key** → A special value that decides *how* the scrambling happens.

   * Different key = different output.
   * Example: Key = `"mySecret123"`.

4. **Ciphertext** → The scrambled (unreadable) output.

   * Example: `"FJ9#*a91@Z"`.

5. **Decryption Algorithm** → The reverse process that converts ciphertext back to plaintext using the key.

👉 *Think of it like a locked box: Plaintext = item, Key = the lock code, Ciphertext = locked box, Decryption = opening it with the key.*

---

## 3. Symmetric vs Asymmetric Cryptography

| Feature            | Symmetric (Shared Key) 🔑                        | Asymmetric (Public + Private Keys) 🔑🔓                     |
| ------------------ | ------------------------------------------------ | ----------------------------------------------------------- |
| Keys               | **One single key** for both encrypt & decrypt    | **Two keys**: Public (to encrypt) + Private (to decrypt)    |
| Speed              | Very **fast**                                    | **Slow** (because of complex math)                          |
| Use                | Best for **large data** (files, videos)          | Best for **small data**, authentication, signatures         |
| Security           | Lower (if key is stolen → everything is exposed) | Higher (even if public key is known, private key is secret) |
| Ciphertext Size    | Same or smaller than plaintext                   | Larger than plaintext                                       |
| Example Algorithms | AES, DES, RC4                                    | RSA, ECC, Diffie-Hellman                                    |
| Real-life Example  | File compression password, WiFi WPA2             | Digital signature, SSL certificates                         |

👉 **Analogy:**

* Symmetric = 🔐 One lock + one key shared by both sender & receiver.
* Asymmetric = 📦 Public box (anyone can put letters inside) + Only you have the private key to open.

---

## 4. Types of Attacks (👨‍💻 Hacker Tricks)

### (a) **Passive Attacks** (Silent listening 👂)

* Attacker only **observes** without changing anything.
* Goal: Steal info secretly.
* **Examples:**

  * Eavesdropping on WiFi.
  * Reading unencrypted emails.

👉 *Like someone secretly listening to your phone call.*

---

### (b) **Active Attacks** (Disrupt & Modify 💣)

* Attacker **changes** or **disrupts** communication.
* **Examples:**

  * Man-in-the-Middle (altering messages).
  * DoS/DDoS attack (blocking access).
  * Message modification (changing "500" to "5000").

👉 *Like a thief not only reading your letter but also replacing the words inside.*

---

## 5. Digital Signature (✍️ Online Signature)

A **digital signature** is like an electronic fingerprint → it proves:

1. The sender is genuine (authentication).
2. The message hasn’t been changed (integrity).
3. The sender cannot deny sending it (non-repudiation).

---

### 🔎 How it Works (Step by Step)

1. Sender writes a **message**.
2. A **hash (digest)** of the message is created (fixed small size).
3. Sender encrypts the digest using their **private key** → this becomes the **digital signature**.
4. Signature is attached to the message.
5. Both message + signature are sent.
6. Receiver uses sender’s **public key** to verify the signature.
7. If digest matches → ✅ message is authentic & unchanged.

---

### ✅ Example in Real Life:

* When you download software (e.g., Windows update), the publisher signs it with a digital signature.
* Your system checks the signature to make sure the file isn’t from a hacker.

👉 *Think of it like signing a contract with your own unique signature that no one else can fake.*

---

## 6. Message Authentication Code (MAC) (🔑 Like a Signature but with Shared Key)

* Ensures data integrity + authenticity.
* Both sender & receiver share a **secret key**.
* Message + key → passed through an algorithm → produces MAC.
* Receiver recalculates MAC and compares.

👉 *Like using a secret handshake between two friends to confirm it’s really them.*

---

# 🎯 Final Quick Recap for Exams

* **CIA Triad**: Confidentiality (privacy), Integrity (no change), Availability (accessible).
* **Extra**: Authenticity (genuine) & Accountability (traceable).
* **Crypto Basics**: Plaintext, Ciphertext, Key, Encryption/Decryption.
* **Symmetric vs Asymmetric**: One key (fast, less secure) vs Two keys (slow, more secure).
* **Attacks**: Passive (just listening) vs Active (modifying/disrupting).
* **Digital Signature**: Private key → encrypt digest → attach → verify with public key.
* **MAC**: Shared key used to prove authenticity + integrity.

---

