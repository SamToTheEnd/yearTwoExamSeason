# Information Security Exam Notes

## 1. Security Concepts and Elements of Cryptography

### Core Security Principles
- **CIA Triad**:
    - **Confidentiality**: Ensuring information is accessible only to those authorized to have access; preventing unauthorized disclosure
    - **Integrity**: Ensuring information remains unaltered by unauthorized entities; data is accurate and trustworthy
    - **Availability**: Ensuring authorized users have reliable and timely access to resources when needed

- **Kerckhoffs' Principle**: The security of a cryptosystem should depend solely on the secrecy of the key, not the algorithm. The cryptosystem should be secure even if everything about the system, except the key, is public knowledge.

### Cryptographic Concepts
- **Computationally Secure**: A system is computationally secure if breaking it requires an impractical amount of computational resources (time/processing power).

- **One-Time Pad**:
    - **Plain English**: Think of a one-time pad like having a secret decoder sheet that you use exactly once and then destroy. You and your friend both have identical copies of this random sheet. To encrypt, you combine your message with the random characters on your sheet. Since the sheet is completely random and used only once, it's mathematically impossible for someone to crack your code without having a copy of the sheet. It's the only perfectly secure encryption method, but it's impractical because you need a new random key as long as your message every time you communicate.
    - Perfectly secure encryption scheme
    - Requires a truly random key as long as the plaintext
    - Can only be used once (hence "one-time")
    - Impractical for frequent bulk communication due to key management challenges
    - **Example**:
      ```
      Plaintext:  HELLO
      Key:        XMCKL     (randomly generated)
      Encryption: H⊕X=C, E⊕M=Q, L⊕C=N, L⊕K=V, O⊕L=Z
      Ciphertext: CQNVZ
      ```

- **Substitution Ciphers**:
    - **Simple Substitution Cipher**: Each character in plaintext is replaced with another character consistently.
        - Not computationally secure against ciphertext-only attacks when enough ciphertext is available, as statistical analysis can reveal patterns.
        - **Example**: A→D, B→E, C→F, etc. (shift by 3)
          ```
          Plaintext:  HELLO
          Ciphertext: KHOOR
          ```

    - **Caesar Cipher**: A specific type of simple substitution cipher where each letter is shifted by a fixed number of positions.
        - Is it simple? Yes - it's one of the simplest encryption techniques, easily broken by brute force (only 25 possible shifts in English alphabet) or frequency analysis.
        - **Example**: With shift of 3
          ```
          Plain alphabet:  ABCDEFGHIJKLMNOPQRSTUVWXYZ
          Cipher alphabet: DEFGHIJKLMNOPQRSTUVWXYZABC
          
          Plaintext:  ATTACK AT DAWN
          Ciphertext: DWWDFN DW GDZQ
          ```

    - **Vigenère Cipher**:
        - **Plain English**: The Vigenère cipher is like using multiple Caesar ciphers based on a keyword. Imagine having different shifts for each letter in your message, and these shifts repeat based on your keyword. For example, if your keyword is "KEY", the first letter shifts by K (10 places), the second by E (4 places), the third by Y (24 places), then you start over with K for the fourth letter. This makes it much harder to break than a regular Caesar cipher because frequency analysis becomes more difficult – the same letter in your message might be encrypted differently each time it appears.
        - **Example**:
          ```
          Keyword: LEMON
          
          Plaintext:  ATTACKATDAWN
          Key:        LEMONLEMONLE (repeat keyword)
          
          For first letter: A (0) + L (11) = L (11)
          For second letter: T (19) + E (4) = X (23)
          And so on...
          
          Ciphertext: LXFOPVEFRNHR
          ```
        - Historical improvement over simple substitution, but still breakable with modern techniques

- **Block Cipher**: Encrypts fixed-length blocks of plaintext into ciphertext blocks of the same length.

    - **AES (Advanced Encryption Standard)**:
        - **Plain English**: AES is like a high-security safe with multiple locks. It takes your data in fixed chunks (128 bits - about 16 characters), and scrambles each chunk through a series of complex mixing operations. Think of it as putting your text through a very complex blender with 10-14 mixing cycles, where each cycle thoroughly mixes your data in a different way. The key (password) determines exactly how this mixing happens. AES is the current global standard for secure encryption, used by governments and businesses worldwide.
        - Block sizes: 128 bits
        - Key sizes: 128, 192, or 256 bits
        - Process: Multiple rounds of substitution and permutation
        - Operations in each round:
            1. SubBytes: Non-linear substitution using S-box
            2. ShiftRows: Transposition step where rows are shifted
            3. MixColumns: Mixing operation (omitted in final round)
            4. AddRoundKey: XOR with round key
        - **Simplified AES Structure**:
          ```
          Plaintext Block (128 bits)
                  ↓
          AddRoundKey (initial round)
                  ↓
          ┌─────────────────────┐
          │ SubBytes            │
          │ ShiftRows           │ × (N-1) rounds
          │ MixColumns          │ (N=10,12,14 depending on key size)
          │ AddRoundKey         │
          └─────────────────────┘
                  ↓
          SubBytes
          ShiftRows
          AddRoundKey (final round)
                  ↓
          Ciphertext Block (128 bits)
          ```

    - **DES (Data Encryption Standard)**:
        - **Plain English**: DES is like an older model safe with a simpler locking mechanism. It processes data in 64-bit chunks (about 8 characters at a time) using a 56-bit key. Imagine a machine that divides your message into blocks, then runs each block through 16 rounds of scrambling operations. It was the encryption standard from 1977 but is now considered too weak because modern computers can try all possible keys in a reasonable time (brute force attack).
        - 64-bit block size, 56-bit key

    - **2TDES (2-key Triple DES)**:
        - **Plain English**: Think of 2TDES as using the older DES safe three times but with only two different keys. It's like locking your data with the first key, unlocking with a second key (which doesn't fully unlock it but transforms it differently), then locking again with the first key. This makes it much harder to break than regular DES, with a total key length of 112 bits.
        - 64-bit block size, 112-bit key
        - Operation: Encrypt with key 1, decrypt with key 2, encrypt again with key 1

    - **3DES (Triple DES)**:
        - **Plain English**: Triple DES is like putting your data through the DES safe three times with three different keys. It's an attempt to strengthen the aging DES algorithm by applying it multiple times. Imagine locking your data box with one key, then putting that locked box inside another box and locking it with a different key, then repeating once more. It's more secure than DES but much slower than modern algorithms like AES.
        - 64-bit block size, 168-bit key (three 56-bit keys)
        - Operation: Encrypt with key 1, decrypt with key 2, encrypt with key 3

- **Attack Types**:
    - **Passive Attack**: Attempt to learn information without affecting system resources (e.g., eavesdropping)
    - **Active Attack**: Attempt to alter system resources or affect operation (e.g., modification of data, denial of service)
    - **Ciphertext-only Attack**: Attacker has access only to encrypted messages
    - **Known-plaintext Attack**: Attacker has access to plaintext-ciphertext pairs
    - **Chosen-plaintext Attack**: Attacker can choose plaintext and observe resulting ciphertext
    - **Meet-in-the-middle Attack**: Time-memory trade-off technique used against multiple encryption schemes

## 2. Symmetric Key Cryptography and Integrity Mechanisms

### Symmetric Encryption Simplified
Symmetric encryption is like having a single key that both locks and unlocks a box. Both the sender and receiver must have identical copies of this key. While simple in concept, the challenge is securely sharing this key initially.

- **Stream Cipher**:
    - **Plain English**: A stream cipher is like having a scrambling machine that works one character at a time. Imagine you and your friend both have identical randomizing devices synchronized with the same secret setting (the key). As you feed in each character of your message, the device produces a random character that you combine with your message character. Your friend's identical device will generate the same random sequence, allowing them to unscramble your message. The main advantage is that if one character gets corrupted during transmission, only that specific character is affected, not the entire message.
    - Encrypts individual bits/bytes of plaintext one at a time
    - Fast encryption with low error propagation (one bit error affects only corresponding bit)
    - Example structure:
      ```
      Secret key → Keystream Generator → Keystream
                                  |
      Plaintext -----------------XOR------→ Ciphertext
      ```

- **Block Cipher Modes**:
    - **CBC (Cipher Block Chaining)**:
        - **Plain English**: CBC is like linking paper shredders together. Imagine you're shredding a document page by page. In normal shredding, each page is shredded independently. But in CBC mode, before shredding a page, you mix in some shredded bits from the previous page. This creates a dependency chain - if you change even one bit on page 2, all subsequent pages will be shredded differently. This prevents patterns from emerging even when encrypting similar blocks of data. To start the process, you need an "Initialization Vector" (IV), which is like a fake "previous page" to mix with your first real page.
        - Uses an Initialization Vector (IV)
        - Each block's encryption depends on previous ciphertext block
        - One corrupted ciphertext block affects two plaintext blocks during decryption
        - Formula: c₀ = IV, cᵢ = eₖ(cᵢ₋₁ ⊕ mᵢ)
        - **Visual representation**:
          ```
          IV    ┌───┐    C₁    ┌───┐    C₂    ┌───┐    C₃
          ┌─────►XOR│    ┌─────►XOR│    ┌─────►XOR│
          │     └─┬─┘    │     └─┬─┘    │     └─┬─┘
          │       │      │       │      │       │
          │       ▼      │       ▼      │       ▼
          │    ┌──┴──┐   │    ┌──┴──┐   │    ┌──┴──┐
          │    │Encrypt│   │    │Encrypt│   │    │Encrypt│
          │    └──┬──┘   │    └──┬──┘   │    └──┬──┘
          │       │      │       │      │       │
          │       ▼      │       ▼      │       ▼
          └───C₁──┘   └───C₂──┘   └───C₃──┘

          P₁           P₂           P₃           (Plaintext blocks)
          ```
        - **How to solve problems with CBC mode**:
            1. Given plaintext blocks P₁, P₂, P₃, IV, and key K, to find ciphertext:
                - C₁ = E_K(P₁ ⊕ IV)
                - C₂ = E_K(P₂ ⊕ C₁)
                - C₃ = E_K(P₃ ⊕ C₂)
            2. Given ciphertext blocks C₁, C₂, C₃, IV, and key K, to find plaintext:
                - P₁ = D_K(C₁) ⊕ IV
                - P₂ = D_K(C₂) ⊕ C₁
                - P₃ = D_K(C₃) ⊕ C₂

### Integrity Mechanisms
- **Hash Function**: Maps data of arbitrary size to fixed-size values
    - **Plain English**: A hash function is like a fingerprint machine for data. No matter how big or small your data is (a single word or an entire book), a hash function creates a fixed-size "fingerprint" (typically a string of letters and numbers) that uniquely represents your data. It's a one-way process - you can easily create the fingerprint from the data, but you can't recreate the original data from just the fingerprint. Hash functions are used to verify file integrity (checking if a file has been tampered with), store passwords securely (websites don't store your actual password, just its hash), and create digital signatures.
    - **Properties**:
        - **Preimage Resistance**: Given hash h, computationally infeasible to find any message m such that h = hash(m)
        - **Second Preimage Resistance**: Given m₁, computationally infeasible to find m₂ ≠ m₁ such that hash(m₁) = hash(m₂)
        - **Collision Resistance**: Computationally infeasible to find any two distinct inputs that hash to same output
    - **Example**:
      ```
      Hash of "hello" using SHA-256:
      2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
      
      Hash of "Hello" (just capitalized the first letter):
      185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969
      
      Notice how even a tiny change produces a completely different hash value.
      ```

- **Message Authentication Code (MAC)**: Provides data origin authentication and data integrity
    - **Plain English**: A MAC is like a wax seal on a letter that only you and the recipient know how to create. It proves two things: 1) the message really came from you (authentication), and 2) nobody has tampered with the message (integrity). You create this "seal" by applying a special function to your message using a secret key that only you and the recipient know. The recipient can verify the seal using the same key. Unlike a digital signature (which uses public/private keys), a MAC uses the same secret key for creating and verifying the seal.
    - **CBC-MAC**: Based on block cipher in CBC mode
    - **HMAC**: Hash-based MAC algorithm
    - **Process**:
        1. Sender computes MAC of message using shared key
        2. Sends message with MAC
        3. Receiver recomputes MAC and compares with received MAC
        4. Match confirms authenticity and integrity
    - **How to compute a MAC** (simplified example):
        ```
        Message: "Transfer $500 to Bob"
        Shared secret key: K
        
        MAC = HMAC(K, message)
        
        Send both message and MAC to recipient
        
        Recipient computes HMAC(K, received_message) and verifies it matches the received MAC
        ```

## 3. Public Key Cryptography, Authentication, Digital Signatures, and Key Establishment

### Public Key Cryptography Fundamentals
Public key cryptography is like having two keys for a mailbox: a public key that anyone can use to drop mail in (encryption), and a private key that only you possess to retrieve the mail (decryption). Unlike symmetric encryption where the same key is used for both operations, public key cryptography uses mathematically related but different keys.

- **Characteristics**:
    - Uses mathematically related key pairs (public and private keys)
    - No need for pre-shared secrets
    - Based on hard mathematical problems (e.g., integer factorization for RSA)
    - **Key difference from symmetric cryptography**: Different keys for encryption and decryption
    - **Advantages**: Solves the key distribution problem, enables digital signatures
    - **Disadvantages**: Much slower than symmetric encryption

- **RSA**: Based on the integer factorization problem
    - **Plain English**: RSA is like a special lock where anyone can lock a message (using the public key), but only the owner with the private key can unlock it. It's based on a simple mathematical principle: it's easy to multiply two large prime numbers together, but extremely difficult to figure out which two prime numbers were multiplied to get a large number. Imagine writing a secret message, putting it in a box with a special lock that anyone can close (by clicking it shut), but only you have the unique key that can open it. RSA is widely used for secure online communications, including web browsing and email encryption.
    - **Computational Issues**:
        - RSA security relies on the difficulty of factoring large numbers. If efficient factoring algorithms are discovered, RSA would be broken.
        - Key sizes have increased over time as computing power grows (from 512 bits to 2048+ bits today).
        - RSA operations are computationally expensive, so they're often used only to encrypt small pieces of data or to exchange symmetric keys.
        - Quantum computers, if developed sufficiently, could break RSA using Shor's algorithm.
    - **Setup**:
        1. Choose two large prime numbers p and q
        2. Compute n = p × q
        3. Calculate φ(n) = (p-1) × (q-1)
        4. Choose e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1
        5. Compute d such that (d × e) mod φ(n) = 1
    - Public parameters: modulus n (product of two large primes), encryption exponent e
    - Private key: decryption exponent d
    - Security depends on difficulty of factoring large numbers
    - **Encryption/Decryption**:
        - Encryption: c = m^e mod n
        - Decryption: m = c^d mod n
    - **Example** (with small numbers for illustration):
      ```
      Key generation:
      p = 61, q = 53
      n = p × q = 3233
      φ(n) = (p-1)(q-1) = 60 × 52 = 3120
      e = 17 (chosen such that gcd(e, φ(n)) = 1)
      d = 2753 (such that (d × e) mod φ(n) = 1)
      
      Public key: (n=3233, e=17)
      Private key: (n=3233, d=2753)
      
      Encryption of m = 123:
      c = 123^17 mod 3233 = 855
      
      Decryption of c = 855:
      m = 855^2753 mod 3233 = 123
      ```
    - **How to solve RSA mathematical problems**:
        1. Finding d from e and φ(n): Use the Extended Euclidean Algorithm
           Example: Find d where e=17, φ(n)=3120
           We need d such that (d×17) mod 3120 = 1
           Using Extended Euclidean Algorithm: d = 2753

        2. Encryption calculation (avoid actual exponentiation by using repeated squaring):
           To calculate c = 123^17 mod 3233:
            - Convert 17 to binary: 10001
            - Start with result = 1
            - For each bit, from left to right:
                - Square the result, take mod n
                - If bit is 1, multiply by m, take mod n
                  This requires only 5 multiplications instead of 17

- **ElGamal**: A randomized public key cryptosystem

### Authentication and Key Establishment
Authentication is like verifying someone's ID before letting them into a secure building. Key establishment is the process of securely creating and sharing encryption keys between parties.

- **Entity Authentication**: Verifying claimed identity of an entity
    - **Plain English**: Entity authentication is like checking someone's ID at a club entrance. It verifies "you are who you say you are" at a specific point in time. This is different from message authentication, which verifies a message came from a specific sender. Entity authentication typically involves a challenge-response process: imagine a security guard asking a visitor a question that only the real person could answer correctly.
    - Often uses challenge-response mechanisms with:
        - Shared secret key
        - Timestamps
        - Random numbers (nonces)
    - **Example of challenge-response**:
      ```
      Alice wants to authenticate Bob:
      1. Alice generates random number (challenge) R
      2. Alice sends R to Bob
      3. Bob computes f(R, K) using shared key K
      4. Bob sends result back to Alice
      5. Alice verifies the result matches her calculation of f(R, K)
      ```

- **Implicit Key Authentication**: Assurance that only the specified party can access the established key
    - **Plain English**: This means you're sure only the intended recipient can access the key you've established, even if you haven't confirmed they've actually received it yet. It's like sending a locked box that only a specific person can open, but not yet confirming they've actually opened it.

- **Freshness Checking Methods**:
    - **Timestamps**:
        - **Plain English**: Using timestamps is like adding a "valid until" date on a document. It ensures messages aren't outdated or replayed by attackers. The receiver checks if the timestamp is recent enough (within an acceptable window), rejecting any message that's too old.
        - Advantages: Automatic rejection of expired messages, fewer messages needed
        - Disadvantages: Requires synchronized clocks
    - **Nonces** (numbers used once):
        - **Plain English**: A nonce is like a unique ticket number that can only be used once. When you send a message, you include a fresh random number (nonce). The recipient must include this same number in their reply, proving they're responding to your specific message, not replaying an old one.
        - Used to prevent replay attacks
        - Ensures message is fresh/recent

- **Diffie-Hellman Key Exchange**:
    - **Plain English**: Diffie-Hellman is like two people mixing paints in a special way to create the same color without ever sharing their secret initial colors. Alice and Bob both start with a common yellow paint (public values). Alice adds her secret red color, Bob adds his secret blue. They exchange these mixtures but keep their secret colors private. Then, each adds their secret color to the mixture received from the other person. Magically, they both end up with the same final green color (the shared key), yet an eavesdropper who only saw the intermediate mixtures can't figure out the final color.
    - Allows two parties to establish a shared secret over an insecure channel
    - Vulnerable to man-in-the-middle attacks without authentication
    - **Station-to-Station (STS) Protocol**: Enhanced DH with authentication using digital signatures
    - **Process**:
      ```
      Public parameters: Large prime p and generator g
      
      Alice                         Bob
      -----                         ---
      Choose private a              Choose private b
      Calculate A = g^a mod p       Calculate B = g^b mod p
                A →
                ← B
      Compute K = B^a mod p         Compute K = A^b mod p
      
      Result: Both have shared secret K = g^(ab) mod p
      ```
    - **How to solve Diffie-Hellman problems**:
      Given p=23, g=5, a=6, b=15:
        1. Calculate A = g^a mod p = 5^6 mod 23 = 8
        2. Calculate B = g^b mod p = 5^15 mod 23 = 19
        3. Alice computes shared secret: K = B^a mod p = 19^6 mod 23 = 2
        4. Bob computes shared secret: K = A^b mod p = 8^15 mod 23 = 2
           Both arrive at the same shared secret K = 2

### Digital Signatures
Digital signatures are the electronic equivalent of handwritten signatures, but they're much more secure and tied to the specific document being signed.

- **Services Provided**:
    - **Non-repudiation**: Prevents sender from denying having sent a message
        - **Plain English**: Non-repudiation is like having undeniable proof that you sent a message. It means you can't later claim "I didn't send that" because the digital signature is mathematically tied to both your private key (which only you control) and the specific content of the message. It's like having a video recording of you physically signing a document - you can't credibly deny it was you.
    - **Data integrity**: Ensures message hasn't been altered
    - **Does not provide confidentiality**

- **RSA Digital Signature Scheme**:
    - **Plain English**: An RSA digital signature is like a personalized stamp that only you can create but anyone can verify is yours. To create this stamp for a document, you first create a fingerprint (hash) of the document, then use your private key to encrypt this fingerprint. Anyone can verify your signature by decrypting it with your public key and checking if the result matches the fingerprint of the document they received.
    - **Process flow**:
      ```
      Signer (with private key d)              Verifier (with public key e)
      ------------------------                 --------------------------
      Message M                                Receives M and signature S
      Compute hash: h = H(M)                  
      Sign: S = h^d mod n                     Compute hash: h' = H(M)
                                              Verify: h' = S^e mod n
      Send M and S                            If equal, signature is valid
      ```
    - Sign: Encrypt hash of message with private key
    - Verify: Decrypt signature with public key and compare with hash of received message
    - Public: Modulus and encryption exponent
    - Secret: Decryption exponent
    - **Example** (using simplified hashing and small numbers):
      ```
      Message: "Pay Bob $100"
      Hash value: 42 (simplified for example)
      
      Alice's private key d = 2753, public key (n=3233, e=17)
      
      Signature creation:
      S = 42^2753 mod 3233 = 2557
      
      Alice sends message "Pay Bob $100" and signature 2557
      
      Verification by recipient:
      Hash of received message = 42
      S^e mod n = 2557^17 mod 3233 = 42
      
      42 (computed) = 42 (from message hash), so signature is valid
      ```

- **Digital Signature vs. Handwritten Signature**:
    - Digital signatures are:
        - Different for each message (based on message content)
        - Verifiable by anyone with the public key
        - Computationally infeasible to forge
    - Handwritten signatures are:
        - Same for all documents
        - Verified by visual comparison
        - Potentially forgeable with practice

- **Session Keys**:
    - **Plain English**: Session keys are like temporary visitor badges that expire after a short visit. Instead of using your main secure key (which would be like using your house key everywhere), you create temporary keys for each communication session. If one session key is compromised, other sessions remain secure. It's like changing the locks after each guest leaves.
    - Temporary keys used for a single communication session
    - Benefits:
        - Limits exposure of long-term keys
        - Limits damage if compromised
        - Reduces amount of ciphertext under one key
    - **Example Use Case**:
      ```
      1. Alice and Bob use RSA to authenticate and establish a temporary session key
      2. They use this session key with AES for faster encryption of their actual conversation
      3. When conversation ends, they discard the session key
      4. Next conversation will use a completely different session key
      ``` entity
    - Often uses challenge-response mechanisms with:
        - Shared secret key
        - Timestamps
        - Random numbers (nonces)

- **Implicit Key Authentication**: Assurance that only the specified party can access the established key

- **Freshness Checking Methods**:
    - **Timestamps**:
        - Advantages: Automatic rejection of expired messages, fewer messages needed
        - Disadvantages: Requires synchronized clocks
    - **Nonces** (numbers used once):
        - Used to prevent replay attacks
        - Ensures message is fresh/recent

- **Diffie-Hellman Key Exchange**:
    - Allows two parties to establish a shared secret over an insecure channel
    - Vulnerable to man-in-the-middle attacks without authentication
    - **Station-to-Station (STS) Protocol**: Enhanced DH with authentication using digital signatures
    - **Process**:
      ```
      Public parameters: Large prime p and generator g
      
      Alice                         Bob
      -----                         ---
      Choose private a              Choose private b
      Calculate A = g^a mod p       Calculate B = g^b mod p
                A →
                ← B
      Compute K = B^a mod p         Compute K = A^b mod p
      
      Result: Both have shared secret K = g^(ab) mod p
      ```

### Digital Signatures
- **Services Provided**:
    - **Non-repudiation**: Prevents sender from denying having sent a message
    - **Data integrity**: Ensures message hasn't been altered
    - **Does not provide confidentiality**

- **RSA Digital Signature Scheme**:
    - **Process flow**:
      ```
      Signer (with private key d)              Verifier (with public key e)
      ------------------------                 --------------------------
      Message M                                Receives M and signature S
      Compute hash: h = H(M)                  
      Sign: S = h^d mod n                     Compute hash: h' = H(M)
                                              Verify: h' = S^e mod n
      Send M and S                            If equal, signature is valid
      ```
    - Sign: Encrypt hash of message with private key
    - Verify: Decrypt signature with public key and compare with hash of received message
    - Public: Modulus and encryption exponent
    - Secret: Decryption exponent
    - **Example** (using simplified hashing and small numbers):
      ```
      Message: "Pay Bob $100"
      Hash value: 42 (simplified for example)
      
      Alice's private key d = 2753, public key (n=3233, e=17)
      
      Signature creation:
      S = 42^2753 mod 3233 = 2557
      
      Alice sends message "Pay Bob $100" and signature 2557
      
      Verification by recipient:
      Hash of received message = 42
      S^e mod n = 2557^17 mod 3233 = 42
      
      42 (computed) = 42 (from message hash), so signature is valid
      ```

- **Digital Signature vs. Handwritten Signature**:
    - Digital signatures are:
        - Different for each message (based on message content)
        - Verifiable by anyone with the public key
        - Computationally infeasible to forge
    - Handwritten signatures are:
        - Same for all documents
        - Verified by visual comparison
        - Potentially forgeable with practice

- **Session Keys**:
    - Temporary keys used for a single communication session
    - Benefits:
        - Limits exposure of long-term keys
        - Limits damage if compromised
        - Reduces amount of ciphertext under one key

## 4. Computer and Network Security

### Access Control
- **Purpose**: Ensures only authorized users can access specific resources, enforcing principle of least privilege

- **Access Control Matrix**:
    - Rows represent subjects (users)
    - Columns represent objects (resources)
    - Entries contain access rights
    - Reference monitor checks if requested access right exists in matrix
    - **Example**:
      ```
        File1     File2     Program1
      +----------+----------+----------+
      | Read     | Read     | Execute  | Alice
      | Write    |          |          |
      +----------+----------+----------+
      | Read     | Read     | Execute  | Bob
      |          | Write    |          |
      +----------+----------+----------+
      |          | Read     | Execute  | Charlie
      |          |          |          |
      +----------+----------+----------+
      ```

- **Access Control List (ACL)**:
    - Column-wise implementation of access control matrix
    - Lists subjects and their access rights for each object
    - Disadvantage: Inefficient for revoking user access (requires checking every object)

### Network Security
- **Firewalls**:
    - Isolate organization's network from internet
    - Filter traffic based on security rules
    - Prevent unauthorized access and known attacks

- **Intrusion Detection Systems (IDS)**:
    - **Signature-based**: Compares activity against database of known attack patterns
        - Good for detecting known threats
        - Cannot detect novel/unknown attacks
    - **Anomaly-based**: Establishes baseline of normal behavior and flags deviations
        - Can detect previously unknown attacks
        - May generate false positives

### Malware Types
- **Trojan Horse**: Appears as legitimate software but contains hidden malicious functions

- **Spyware**: Collects user information by monitoring web browsing habits and other activities

- **Virus**: Replicates by inserting itself into other code/programs

- **Worm**: Self-replicating malware that spreads across networks without requiring host files

### Software Security
- **Principles of Secure Software Design**:
    - **Defense in Depth**: Multiple layers of security controls
    - **Principle of Least Privilege**: Grant minimal access rights necessary
    - **Input Validation**: Verify all inputs meet expected parameters

- **Factors Contributing to Software Vulnerabilities**:
    - Increased networking exposure
    - System complexity
    - Market pressures leading to rushed development
    - Poor development processes
    - Insufficient testing
    - Lack of security awareness