+++
date = '2026-03-20T15:40:34+07:00'
draft = true
title = 'Unlocking the Mystery of TLS: How Secret Keys are Made'
+++

Have you ever wondered how your computer (the client) and a website (the server) can agree on a secret password over the open internet without hackers stealing it? This article explains the clever math and steps behind this process, known as a secure key exchange.

---

### 1. The Basics of Key Exchange

In modern web security (specifically TLS 1.2 and above), the two sides usually use a method called **ECDHE** to exchange keys. 

Both the client and the server create a pair of keys: a **private key** (kept hidden) and a **public key** (shared openly).

| Role | Private Key (Secret) | Public Key (Sent over network) |
| :--- | :--- | :--- |
| **Client** | $a$ | $A = g^a \bmod p$ |
| **Server** | $b$ | $B = g^b \bmod p$ |

*(Note: $g$ and $p$ are public mathematical parameters that everyone knows.)*

These public keys, $A$ and $B$, are sent over the open network. An eavesdropper (hacker) can easily see them. However, only the client knows $a$, and only the server knows $b$.

---

### 2. Creating the Shared Secret

When they receive each other's public keys, they do a bit more math to create a shared `pre_master_secret`:

* **The Client calculates:** $$pre\_master\_secret = B^a \bmod p = g^{ab} \bmod p$$
* **The Server calculates:** $$pre\_master\_secret = A^b \bmod p = g^{ab} \bmod p$$

Both sides get the exact same result ($g^{ab} \bmod p$), even though they never sent their private keys over the internet! 

The hacker knows $g$, $p$, $A$, and $B$. However, because they do not know $a$ or $b$, they cannot calculate the shared secret. Figuring out the private keys from the public keys is considered nearly impossible to solve.

---

### 3. Making the Final Master Secret

Now, both the client and server have the same `pre_master_secret`. But they need to mix it up to make it even more secure. They combine it with two random numbers created at the start of the connection (`ClientRandom` and `ServerRandom`).

They use a special mixing function called a **PRF**:

`master_secret = PRF(pre_master_secret, "master secret", ClientRandom + ServerRandom)`

This function acts like a blender. Because the hacker does not have the `pre_master_secret` to put into the blender, they cannot possibly guess the final `master_secret`.

---

### 4. Why the Hacker Fails

Imagine a hacker intercepts everything:
* The `ClientRandom` and `ServerRandom`
* The server's public key ($B$)
* The client's public key ($A$)

They still fail because they do not have $a$ and $b$. These private keys only live temporarily in the computer's memory (RAM) and are deleted right after the connection is set up. Without $a$ or $b$, there is no `pre_master_secret`, and without that, there is no `master_secret`.

---

### 5. Locking the Channel

Once the `master_secret` is created, it is used to generate the final session keys. From this moment on, all data sent between the client and server is encrypted using these keys. The secure channel is officially open!

---

### Summary of TLS Components

| Component | Who knows it? | Is it public? | What is it used for? |
| :--- | :--- | :--- | :--- |
| **$a$, $b$** | Kept private by each side | ❌ No | Creating the secret |
| **$A$, $B$** | Both sides + Hacker | ✅ Yes | Exchanging public keys |
| **pre_master_secret** | Both sides | ❌ No | Base for the final key |
| **Client/Server Random** | Everyone | ✅ Yes | Preventing replay attacks |
| **master_secret** | Both sides | ❌ No | Making encryption keys |

---

### How it looks in Action (Sequence Diagrams)

Here is how the communication flows step-by-step.

#### TLS 1.2 Handshake Flow

```mermaid
sequenceDiagram
    participant Client
    participant Server

    Client->>Server: ClientHello (supported versions, cipher suites, random_C)
    Note right of Client: "random_C" = client's random number

    Server->>Client: ServerHello (chosen version, cipher suite, random_S)
    Note right of Server: "random_S" = server's random number

    Server->>Client: Certificate (server's public key)
    Server->>rverKeyExchange (server sends ECDHE params)
    Server->>Client: ServerHelloDone
    Note over Client,Server: 🔓 Everything so far is plain text

    Client->>Server: ClientKeyExchange (client sends its ECDHE public key)
    Note right of Client: Both sides now compute shared pre_master_secret

    Note over Client,Server: Create master_secret = PRF(pre_master, random_C, random_S)
    Note over Client,Server: Use it to make session keys for encryption

    Client->>Server: ChangeCipherSpec (start using encryption)
    Client->>Server: Finished (first encrypted message)
    Server->>Client: ChangeCipherSpec
    Server->>Client: Finished (encrypted)

    Note over Client,Server: 🔒 Secure channel is now active
```

#### TLS 1.3 Handshake Flow (Faster and more secure)

```mermaid
sequenceDiagram
    participant Client
    participant Server

    Client->>Server: ClientHello (supported cipher suites, key_share_C, random_C)
    Note right of Client: "key_share_C" = client’s public key for ECDHE

    Serverent: ServerHello (chosen cipher, key_share_S)
    Note right of Server: "key_share_S" = server’s public key for ECDHE
    Note over Client,Server: Both create shared_secret = ECDHE(key_share_C, key_share_S)
    
    Note over Client,Server: 🔐 From now, handshake messages are encrypted

    Server->>Client: EncryptedExtensions, Certificate, CertificateVerify, Finished
    Client->>Server: Finished (encrypted)

    Note over Client,Server: 🔒 Secure channel ready for app data
```

---

### Vocabulary

* **ECDHE (Elliptic-Curve Diffie–Hellman Ephemeral):** A complex mathematical method that allows two parties to agree on a shared secret over a public network.
* **Ephemeral:** Something that lasts for a very short time. In this case, the private keys are deleted immediately after use, making the system highly secure.
* **PRF (Pseudo-Random Function):** A mathematical algorithm used to mix data securely. It takes inputs and creates a random-looking output that is virtually impossible to reverse.
* **Cipe:** A set of rules and algorithms that the client and server agree to use for a secure connection.

