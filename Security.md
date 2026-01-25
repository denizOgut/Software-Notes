
# SECURITY MINDSET & CORE PRINCIPLES
## 1. THE CIA TRIAD - Your Security North Star

Every security decision you make protects one or more of these:

```
                    ┌─────────────────┐
                    │ CONFIDENTIALITY │
                    │   (Secrecy)     │
                    └────────┬────────┘
                             │
              "Only authorized people 
               can ACCESS the data"
                             │
         ┌───────────────────┴───────────────────┐
         │                                       │
         ▼                                       ▼
┌─────────────────┐                   ┌─────────────────┐
│    INTEGRITY    │◄─────────────────►│  AVAILABILITY   │
│  (Correctness)  │                   │   (Uptime)      │
└─────────────────┘                   └─────────────────┘
         │                                       │
  "Only authorized people                "Authorized people
   can MODIFY the data"                  can access it WHEN NEEDED"
```

### Real Examples for Each:

|Principle|Attack Example|Your Code Impact|
|---|---|---|
|**Confidentiality**|SQL injection leaks user passwords|Encrypt sensitive data, use parameterized queries|
|**Integrity**|Attacker modifies transaction amount|Digital signatures, checksums, audit logs|
|**Availability**|DDoS takes down your API|Rate limiting, redundancy, graceful degradation|

### The Trade-offs (Security is ALWAYS Trade-offs)

```
MORE SECURITY ←─────────────────────────────→ MORE USABILITY

Examples:
- 2FA increases Confidentiality but reduces Availability (user locked out)
- Encryption protects Confidentiality but costs CPU (affects Availability)
- Strict validation improves Integrity but may reject valid input (Availability)

Your job: Find the RIGHT balance for your context.
```

---

## 2. DEFENSE IN DEPTH - Layers Save Lives

**The Castle Analogy:**

```
ATTACKER → [Moat] → [Wall] → [Guards] → [Locked Door] → [Safe] →  DATA

If ONE layer fails, others still protect you.
```

**In Your Spring Boot Application:**

```
                         INTERNET
                             │
                             ▼
┌────────────────────────────────────────────────────────────┐
│ LAYER 1: Network Security                                  │
│ • Firewall rules                                           │
│ • DDoS protection                                          │
│ • TLS/HTTPS only                                           │
└────────────────────────────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────┐
│ LAYER 2: Application Gateway / Load Balancer               │
│ • Rate limiting                                            │
│ • WAF (Web Application Firewall)                           │
│ • Request validation                                       │
└────────────────────────────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────┐
│ LAYER 3: Authentication                                    │
│ • Spring Security filters                                  │
│ • JWT validation                                           │
│ • Session management                                       │
└────────────────────────────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────┐
│ LAYER 4: Authorization                                     │
│ • @PreAuthorize checks                                     │
│ • Role-based access                                        │
│ • Resource ownership validation                            │
└────────────────────────────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────┐
│ LAYER 5: Input Validation                                  │
│ • Bean Validation (@Valid)                                 │
│ • Business rule validation                                 │
│ • Sanitization                                             │
└────────────────────────────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────┐
│ LAYER 6: Data Security                                     │
│ • Parameterized queries (SQL injection prevention)         │
│ • Encryption at rest                                       │
│ • Database access controls                                 │
└────────────────────────────────────────────────────────────┘
                             │
                             ▼
                            DATA
```

**Key Insight:** If your ONLY security is `@PreAuthorize`, one bug exposes everything. Real security has 5-7 layers.

---

## 3. PRINCIPLE OF LEAST PRIVILEGE (PoLP)

**The Golden Rule:** Give the MINIMUM access needed to do the job. Nothing more.

### ❌ VIOLATION - What Most Developers Do:


```java
// Database user with ALL privileges
spring.datasource.username=root
spring.datasource.password=admin123

// Service account with admin role
@Service
public class ReportService {
    // This service only READS data, but runs as ADMIN
    // If compromised, attacker can DELETE everything
}

// API endpoint accessible to all authenticated users
@GetMapping("/admin/users")
@PreAuthorize("isAuthenticated()")  // ANY logged-in user can see ALL users!
public List<User> getAllUsers() { ... }
```

### ✅ CORRECT - Least Privilege Applied:


```java
// Database user with ONLY needed privileges
// Created with: GRANT SELECT, INSERT ON orders TO app_order_service;
spring.datasource.username=app_order_service

// Service with specific, limited role
@Service
public class ReportService {
    // Runs with READ_ONLY role
    // Even if compromised, cannot modify data
}

// API endpoint with specific role requirement
@GetMapping("/admin/users")
@PreAuthorize("hasRole('USER_ADMIN')")  // Only USER_ADMIN can access
public List<User> getAllUsers() { ... }
```

### Least Privilege Checklist:

| Resource | Question to Ask |
|----------|----------------|
| Database user | Does this app need DELETE? DROP? Or just SELECT/INSERT? |
| Service account | Does this service need ADMIN? Or just specific permissions? |
| API endpoints | Should ALL authenticated users access this? Or specific roles? |
| File system | Does the app need write access? Or read-only? |
| Environment variables | Should this service see ALL secrets? Or just its own? |

---

## 4. ZERO TRUST ARCHITECTURE

**Old Model (Castle & Moat):**
```
"If you're inside the network, you're trusted"
     │
     └── This is why breaches spread so fast
         Once inside, attackers move freely
```

**Zero Trust Model:**
```
"Never trust, always verify - even internal traffic"

┌─────────────────────────────────────────────────────────────┐
│                      YOUR NETWORK                           │
│                                                             │
│   ┌─────────┐      VERIFY      ┌─────────┐                  │
│   │Service A│ ───────────────► │Service B│                  │
│   └─────────┘   • Identity     └─────────┘                  │
│                 • Permission                                │
│                 • Context                                   │
│                 • Every time                                │
│                                                             │
│   Even internal services authenticate to each other!        │
└─────────────────────────────────────────────────────────────┘
````

### Zero Trust Principles for Your Code:


```java
// ❌ OLD THINKING: "This is an internal endpoint, no auth needed"
@GetMapping("/internal/user-data")
public UserData getInternalData() {
    // "Only our services call this"... until an attacker gets in
    return userRepository.findAll();
}

// ✅ ZERO TRUST: Internal endpoints ALSO require authentication
@GetMapping("/internal/user-data")
@PreAuthorize("hasRole('INTERNAL_SERVICE') and #oauth2.hasScope('read:users')")
public UserData getInternalData() {
    // Even internal services must prove identity
    return userRepository.findAll();
}
```

### Zero Trust Checklist:

- [ ] Service-to-service communication uses mTLS or tokens
- [ ] No endpoint is "internal only" without authentication
- [ ] Network location doesn't grant trust
- [ ] Every request is authenticated AND authorized
- [ ] Assume breach has already happened

---

## 5. THREAT MODELING WITH STRIDE

Before writing code, think: **"How would an attacker break this?"**

**STRIDE** is a framework to systematically identify threats:
```
┌────────────────┬────────────────────────────────────────────────────────┐
│ Threat         │ What it means                                          │
├────────────────┼────────────────────────────────────────────────────────┤
│ S - Spoofing   │ Pretending to be someone else                          │
│                │ → Fake login, stolen session, forged JWT               │
├────────────────┼────────────────────────────────────────────────────────┤
│ T - Tampering  │ Modifying data without permission                      │
│                │ → SQL injection, man-in-the-middle, parameter tampering│
├────────────────┼────────────────────────────────────────────────────────┤
│ R - Repudiation│ Denying you did something                              │
│                │ → "I never made that transaction" (no audit log)       │
├────────────────┼────────────────────────────────────────────────────────┤
│ I - Info       │ Exposing data to unauthorized parties                  │
│   Disclosure   │ → Error messages with stack traces, data leaks         │
├────────────────┼────────────────────────────────────────────────────────┤
│ D - Denial of  │ Making the system unavailable                          │
│   Service      │ → DDoS, resource exhaustion, infinite loops            │
├────────────────┼────────────────────────────────────────────────────────┤
│ E - Elevation  │ Gaining permissions you shouldn't have                 │
│   of Privilege │ → Regular user becomes admin, IDOR attacks             │
└────────────────┴────────────────────────────────────────────────────────┘
```

### STRIDE Applied to a Simple Feature:

**Feature:** User can update their profile
```
Ask yourself for EACH letter:

S - Spoofing:      Can someone update ANOTHER user's profile?
T - Tampering:     Can they modify fields they shouldn't (e.g., role)?
R - Repudiation:   Do we log WHO made changes and WHEN?
I - Info Disclosure: Does the response leak sensitive fields?
D - Denial of Service: Can they upload a 10GB profile picture?
E - Elevation:     Can they change their role from USER to ADMIN?
````

### Quick STRIDE Example in Code:

java

```java
// Original endpoint - let's STRIDE it
@PutMapping("/users/{id}")
public User updateProfile(@PathVariable Long id, @RequestBody UserUpdateDTO dto) {
    User user = userRepository.findById(id).orElseThrow();
    user.setName(dto.getName());
    user.setEmail(dto.getEmail());
    user.setRole(dto.getRole());  // 😱 E: Elevation of Privilege!
    return userRepository.save(user);
}

// After STRIDE analysis:
@PutMapping("/users/{id}")
@PreAuthorize("#id == authentication.principal.id")  // S: Prevent Spoofing
public User updateProfile(
    @PathVariable Long id,
    @Valid @RequestBody UserUpdateDTO dto  // D: Validation prevents bad input
) {
    User user = userRepository.findById(id).orElseThrow();
    
    // T: Only allow specific fields to be updated
    user.setName(dto.getName());
    user.setEmail(dto.getEmail());
    // Role is NOT updated from DTO - E: Prevent Elevation
    
    // R: Audit logging
    auditLog.log("PROFILE_UPDATE", id, getCurrentUserId());
    
    User saved = userRepository.save(user);
    
    // I: Return limited view, not full entity
    return UserMapper.toPublicView(saved);
}
```

---

## 6. ATTACK SURFACE

**Definition:** Every point where an attacker can try to enter or extract data.

### Your Application's Attack Surface:
```
┌─────────────────────────────────────────────────────────────────────────┐
│                         ATTACK SURFACE MAP                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  EXTERNAL SURFACE (Internet-facing)                                     │
│  ├── REST API endpoints (/api/*)                                        │
│  ├── Authentication endpoints (/login, /oauth)                          │
│  ├── File upload endpoints                                              │
│  ├── Webhooks receiving external data                                   │
│  └── Public static assets                                               │
│                                                                         │
│  INTERNAL SURFACE (Service-to-service)                                  │
│  ├── Internal APIs                                                      │
│  ├── Message queue consumers (RabbitMQ)                                 │
│  ├── Database connections                                               │
│  └── Cache (Redis) connections                                          │
│                                                                         │
│  DATA SURFACE (What you store/process)                                  │
│  ├── User credentials                                                   │
│  ├── Personal data (PII)                                                │
│  ├── Business-sensitive data                                            │
│  └── Logs (might contain sensitive data!)                               │
│                                                                         │
│  DEPENDENCY SURFACE (Third-party code)                                  │
│  ├── Maven/Gradle dependencies                                          │
│  ├── Docker base images                                                 │
│  └── External APIs you call                                             │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Attack Surface Reduction Principles:
```
1. MINIMIZE: Fewer endpoints = fewer attack vectors
   • Do you NEED that /debug endpoint in production?
   • Remove unused dependencies
   
2. HARDEN: Make remaining surface tough to break
   • Input validation on every endpoint
   • Authentication on everything
   
3. MONITOR: Watch for attacks on your surface
   • Log authentication failures
   • Alert on unusual patterns

```
---

## ✅ SECURITY CHECKLIST FOR SESSION 1

□ Every feature decision considers CIA trade-offs
□ Security is layered (Defense in Depth) - not single-point
□ Database users have minimal required privileges
□ Service accounts have minimal required roles
□ API endpoints require specific roles, not just "authenticated"
□ Internal services authenticate to each other (Zero Trust)
□ New features are analyzed with STRIDE before coding
□ Attack surface is documented and minimized
□ Unused endpoints and dependencies are removed


---

## 🚫 COMMON MISTAKES

1. "We have a firewall, so we're secure"
   → Firewall is ONE layer. Equifax had firewalls too.

2. "This is an internal service, no auth needed"
   → Attackers who breach one service will find ALL unprotected internal services.

3. "The database user needs admin access for that one migration"
   → Use a SEPARATE migration user. App user stays limited.

4. "Security slows down development"
   → A breach slows down development for MONTHS. Build security in from day one.

5. "We'll add security later"
   → Technical debt that often never gets paid. Bolt-on security is always weaker.

--- 
## Summary

**Key Takeaways:**
- ==**CIA Triad is your compass for every security decision**==
- ==**Defense in Depth: Never rely on a single security control**==
- ==**Least Privilege: Give minimum access, assume breach**==
- ==**Zero Trust: Verify everything, trust nothing**==
- ==**STRIDE: Systematically find threats before attackers do**==
- ==**Attack Surface: Know it, minimize it, harden it, monitor it==**


# CRYPTOGRAPHY FOR DEVELOPERS (Part 1)

## 1. THE BIG THREE: ENCODING vs ENCRYPTION vs HASHING

This is the **#1 confusion** that causes security disasters. 
```
┌─────────────────────────────────────────────────────────────────────────┐
│                     THE FUNDAMENTAL DIFFERENCES                         │
├─────────────────┬─────────────────┬─────────────────┬───────────────────┤
│                 │    ENCODING     │   ENCRYPTION    │     HASHING       │
├─────────────────┼─────────────────┼─────────────────┼───────────────────┤
│ Purpose         │ Data format     │ Confidentiality │ Integrity/        │
│                 │ transformation  │ (hide data)     │ Verification      │
├─────────────────┼─────────────────┼─────────────────┼───────────────────┤
│ Reversible?     │ YES (always)    │ YES (with key)  │ NO (one-way)      │
├─────────────────┼─────────────────┼─────────────────┼───────────────────┤
│ Key required?   │ NO              │ YES             │ NO                │
├─────────────────┼─────────────────┼─────────────────┼───────────────────┤
│ Security?       │ NONE!           │ YES             │ YES               │
├─────────────────┼─────────────────┼─────────────────┼───────────────────┤
│ Examples        │ Base64, URL     │ AES, RSA        │ SHA-256, bcrypt   │
│                 │ encoding, UTF-8 │ ChaCha20        │ Argon2            │
├─────────────────┼─────────────────┼─────────────────┼───────────────────┤
│ Use for         │ Data transport  │ Secrets, PII,   │ Passwords,        │
│                 │ Binary→Text     │ sensitive data  │ checksums, tokens │
└─────────────────┴─────────────────┴─────────────────┴───────────────────┘
```

### ENCODING - NOT SECURITY! 


Encoding is like changing languages - anyone who knows the language can read it.
```
Original:  "Hello"
Base64:    "SGVsbG8="
URL:       "Hello%20World"
```


**==THERE IS NO SECRET. Anyone can decode it.==**


```java
// ❌ DANGEROUS MISCONCEPTION - This is NOT security!
public class BadSecurity {
    
    public String "encode"Password(String password) {
        // Base64 is NOT encryption! Anyone can decode this!
        return Base64.getEncoder().encodeToString(password.getBytes());
    }
    
    public String encodeApiKey(String apiKey) {
        // Still readable by anyone!
        return Base64.getEncoder().encodeToString(apiKey.getBytes());
    }
}

// Attacker decodes in 1 second:
// echo "SGVsbG8=" | base64 -d
// Output: Hello
```

**When to use Encoding:**
- Transmitting binary data over text protocols (email attachments, JSON)
- URL-safe strings
- ==**NEVER for security!**==

---

### ENCRYPTION - Reversible WITH a Key 

Encryption is like a safe - you need the key to open it.
```

Original:    "Hello"
             + Key: "mysecretkey"
                    ↓
Encrypted:   "U2FsdGVkX1+..." (gibberish without key)
                    ↓
             + Key: "mysecretkey"
                    ↓
Decrypted:   "Hello"
```

**When to use Encryption:**
- Storing sensitive data you need to READ later (credit cards, PII)
- Data in transit (HTTPS/TLS)
- File encryption
- ==**NEVER for passwords!**== (You don't need to read passwords back)

---

### HASHING - One-Way, No Going Back 
Hashing is like a meat grinder - you can't un-grind meat.
```
Original:    "Hello"
                ↓
Hash:        "185f8db32271fe25f561a6fc938b2e26..." (SHA-256)
                ↓
Original:    ??? (IMPOSSIBLE to reverse)
```


Same input **ALWAYS** produces same output. Different input produces COMPLETELY different output.
```
"Hello"  → 185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969
"hello"  → 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
"Hello!" → 33072bed7d6a2991030be4f3be95a0f3fc07c0f71b3c3e73139d8e3e32b22ab0
```


One character change = completely different hash (avalanche effect)

**When to use Hashing:**

- **==Password storage (with salt!)==**
- **==Data integrity verification (checksums)==**
- **==Digital signatures==**
- **==Token generation**==

---

### ❌ CRITICAL MISTAKES IN THE WILD

```java
// MISTAKE 1: Base64 for "hiding" sensitive data
String encoded = Base64.encode(creditCard);  // Anyone can decode!

// MISTAKE 2: Encryption for passwords
String encrypted = AES.encrypt(password, key);  
// If key is stolen, ALL passwords exposed at once!

// MISTAKE 3: Simple hashing for passwords (no salt)
String hashed = SHA256.hash(password);  
// Rainbow table attack: pre-computed hashes defeat this instantly

// MISTAKE 4: MD5/SHA1 for anything security-related
String hash = MD5.hash(data);  // Broken! Collisions found.
```

### ✅ CORRECT USAGE


```java
// Encoding: Only for data format conversion
String base64 = Base64.getEncoder().encodeToString(binaryData);

// Encryption: For data you need to read back
String encrypted = AES_GCM.encrypt(creditCardNumber, secretKey);
String decrypted = AES_GCM.decrypt(encrypted, secretKey);

// Hashing: For passwords (use specialized password hashers)
String passwordHash = BCrypt.hashpw(password, BCrypt.gensalt(12));
boolean matches = BCrypt.checkpw(inputPassword, passwordHash);
```

---

## 2. SYMMETRIC ENCRYPTION - One Key for Both

**Concept:** Same key encrypts AND decrypts.
```
        ┌─────────────┐
        │  SAME KEY   │
        │   🔑        │
        └──────┬──────┘
               │
     ┌─────────┴─────────┐
     │                   │
     ▼                   ▼
┌─────────┐         ┌─────────┐
│ ENCRYPT │         │ DECRYPT │
└─────────┘         └─────────┘
     │                   │
     ▼                   ▼
"Hello" ──────► "x7#kL..." ──────► "Hello"
```

### AES (Advanced Encryption Standard) - The Gold Standard

AES is the most widely used symmetric encryption algorithm.
Used by: Banks, governments, HTTPS, disk encryption, everywhere.

Key sizes:
- AES-128: Good security, faster
- AES-192: Better security
- AES-256: Best security (recommended for sensitive data)


### AES Modes - This Matters!
```
┌─────────────┬────────────────────────────────────────────────────────────┐
│ Mode        │ Description                                                │
├─────────────┼────────────────────────────────────────────────────────────┤
│ ECB         │ ❌ NEVER USE! Same plaintext = same ciphertext            │
│             │    Famous "ECB Penguin" demonstrates the flaw              │
├─────────────┼────────────────────────────────────────────────────────────┤
│ CBC         │ ⚠️ Okay with random IV, but vulnerable to padding oracles │
├─────────────┼────────────────────────────────────────────────────────────┤
│ GCM         │ ✅ RECOMMENDED! Authenticated encryption (integrity check) │
│             │    Detects if ciphertext was tampered with                 │
├─────────────┼────────────────────────────────────────────────────────────┤
│ CTR         │ ✅ Good, but no built-in authentication                    │
└─────────────┴────────────────────────────────────────────────────────────┘
```

**==ALWAYS USE AES-GCM (Galois/Counter Mode)==**

### Why ECB is Dangerous - The Penguin Proof

ECB Mode encrypts each block independently. Same plaintext block = Same ciphertext block.

```
ECB Mode encrypts each block independently.
Same plaintext block = Same ciphertext block.

Original Image:          ECB Encrypted:          Proper Encryption (CBC/GCM):
┌──────────────┐         ┌──────────────┐        ┌──────────────┐
│   🐧🐧🐧     │         │   🐧🐧🐧     │        │   ░░░░░░     │
│  🐧🐧🐧🐧   │  ────►  │  🐧🐧🐧🐧   │        │  ░░░░░░░░   │
│   🐧🐧🐧     │         │   🐧🐧🐧     │        │   ░░░░░░     │
└──────────────┘         └──────────────┘        └──────────────┘
                         Pattern visible!        Random noise!
````

### Java AES-GCM Implementation

```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.GCMParameterSpec;
import java.security.SecureRandom;
import java.util.Base64;

public class AESEncryption {
    
    private static final String ALGORITHM = "AES/GCM/NoPadding";
    private static final int GCM_IV_LENGTH = 12;      // 96 bits recommended for GCM
    private static final int GCM_TAG_LENGTH = 128;    // Authentication tag length
    
    /**
     * Generate a secure AES-256 key
     */
    public static SecretKey generateKey() throws Exception {
        KeyGenerator keyGen = KeyGenerator.getInstance("AES");
        keyGen.init(256);  // AES-256
        return keyGen.generateKey();
    }
    
    /**
     * Encrypt data with AES-GCM
     * Returns: IV + Ciphertext (IV is prepended for decryption)
     */
    public static byte[] encrypt(byte[] plaintext, SecretKey key) throws Exception {
        // Generate random IV (NEVER reuse IV with same key!)
        byte[] iv = new byte[GCM_IV_LENGTH];
        SecureRandom random = new SecureRandom();
        random.nextBytes(iv);
        
        // Initialize cipher
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_LENGTH, iv);
        cipher.init(Cipher.ENCRYPT_MODE, key, spec);
        
        // Encrypt
        byte[] ciphertext = cipher.doFinal(plaintext);
        
        // Prepend IV to ciphertext (needed for decryption)
        byte[] result = new byte[iv.length + ciphertext.length];
        System.arraycopy(iv, 0, result, 0, iv.length);
        System.arraycopy(ciphertext, 0, result, iv.length, ciphertext.length);
        
        return result;
    }
    
    /**
     * Decrypt data with AES-GCM
     * Input format: IV + Ciphertext
     */
    public static byte[] decrypt(byte[] encryptedData, SecretKey key) throws Exception {
        // Extract IV from beginning
        byte[] iv = new byte[GCM_IV_LENGTH];
        System.arraycopy(encryptedData, 0, iv, 0, iv.length);
        
        // Extract ciphertext
        byte[] ciphertext = new byte[encryptedData.length - iv.length];
        System.arraycopy(encryptedData, iv.length, ciphertext, 0, ciphertext.length);
        
        // Initialize cipher
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_LENGTH, iv);
        cipher.init(Cipher.DECRYPT_MODE, key, spec);
        
        // Decrypt (will throw exception if tampered!)
        return cipher.doFinal(ciphertext);
    }
    
    // Convenience methods for String
    public static String encryptString(String plaintext, SecretKey key) throws Exception {
        byte[] encrypted = encrypt(plaintext.getBytes("UTF-8"), key);
        return Base64.getEncoder().encodeToString(encrypted);
    }
    
    public static String decryptString(String ciphertext, SecretKey key) throws Exception {
        byte[] encrypted = Base64.getDecoder().decode(ciphertext);
        byte[] decrypted = decrypt(encrypted, key);
        return new String(decrypted, "UTF-8");
    }
}
```

### Usage Example

java

```java
public class EncryptionDemo {
    public static void main(String[] args) throws Exception {
        // Generate key (store this securely!)
        SecretKey key = AESEncryption.generateKey();
        
        // Encrypt sensitive data
        String creditCard = "4111-1111-1111-1111";
        String encrypted = AESEncryption.encryptString(creditCard, key);
        System.out.println("Encrypted: " + encrypted);
        // Output: "dGhpcyBpcyBub3QgcmVhbCBjaXBoZXJ0ZXh0Li4u..."
        
        // Decrypt when needed
        String decrypted = AESEncryption.decryptString(encrypted, key);
        System.out.println("Decrypted: " + decrypted);
        // Output: "4111-1111-1111-1111"
        
        // Tamper detection (GCM integrity check)
        try {
            byte[] tampered = Base64.getDecoder().decode(encrypted);
            tampered[20] ^= 1;  // Flip one bit
            AESEncryption.decrypt(tampered, key);
        } catch (Exception e) {
            System.out.println("Tampering detected: " + e.getMessage());
            // Output: "Tampering detected: Tag mismatch!"
        }
    }
}
```

---

## 3. ASYMMETRIC ENCRYPTION - Two Keys

**Concept:** Public key encrypts, Private key decrypts (or vice versa for signing).
```
┌──────────────────────────────────────────────────────────────────────┐
│                    ASYMMETRIC ENCRYPTION                             │
│                                                                      │
│     PUBLIC KEY 🔓              PRIVATE KEY 🔐                        │
│     (Share freely)             (Keep secret!)                        │
│                                                                      │
│         │                           │                                │
│         ▼                           ▼                                │
│    ┌─────────┐                 ┌─────────┐                          │
│    │ ENCRYPT │                 │ DECRYPT │                          │
│    └─────────┘                 └─────────┘                          │
│         │                           │                                │
│         └───────────────────────────┘                                │
│                      │                                               │
│                      ▼                                               │
│              "Hello" → "x#7L..." → "Hello"                          │
│                                                                      │
│  Anyone with public key can encrypt.                                 │
│  ONLY private key holder can decrypt.                                │
└──────────────────────────────────────────────────────────────────────┘
```

### RSA vs ECC
```
┌──────────────┬─────────────────────────────────────────────────────────┐
│              │  RSA                        │  ECC (Elliptic Curve)     │
├──────────────┼─────────────────────────────┼───────────────────────────┤
│ Security     │ 2048-bit = 112-bit security │ 256-bit = 128-bit security│
│              │ 3072-bit = 128-bit security │ 384-bit = 192-bit security│
├──────────────┼─────────────────────────────┼───────────────────────────┤
│ Key Size     │ Large (2048-4096 bits)      │ Small (256-384 bits)      │
├──────────────┼─────────────────────────────┼───────────────────────────┤
│ Speed        │ Slower                      │ Faster                    │
├──────────────┼─────────────────────────────┼───────────────────────────┤
│ Use Cases    │ Legacy systems, X.509 certs │ Modern TLS, mobile, JWT   │
├──────────────┼─────────────────────────────┼───────────────────────────┤
│ Recommended  │ RSA-2048 minimum            │ P-256 or P-384            │
│              │ RSA-4096 for long-term      │ Ed25519 for signatures    │
└──────────────┴─────────────────────────────┴───────────────────────────┘
```

**For new systems: Prefer ECC (smaller, faster, same security)** 
**For compatibility: RSA-2048+ still fine**

### Why Asymmetric Encryption Exists

**Problem:** How do you share a symmetric key securely?
```
SYMMETRIC ONLY (The Problem):

Alice                                      Bob
  │                                          │
  │  "I'll encrypt with key K"               │
  │                                          │
  │  But how do I send K to Bob securely?    │
  │  If I send K unencrypted, attacker gets it│
  │                                          │
  │  ──────── Key K (intercepted!) ────────► │
  │                                          │
  │             😈 Attacker has K!            │
  
  
HYBRID APPROACH (The Solution):

Alice                                      Bob
  │                                          │
  │  1. Bob generates RSA key pair           │
  │                                          │
  │  ◄──── Bob's PUBLIC key ────────────     │
  │                                          │
  │  2. Alice generates random AES key       │
  │     Encrypts AES key WITH Bob's          │
  │     public RSA key                       │
  │                                          │
  │  ──── Encrypted AES key ────────────►    │
  │                                          │
  │  3. Bob decrypts AES key with his        │
  │     PRIVATE RSA key                      │
  │                                          │
  │  4. Now both have the AES key!           │
  │     Use fast symmetric encryption        │
  │                                          │
  │  ════ AES encrypted data ═══════════►    │

This is EXACTLY how HTTPS/TLS works!
```

### RSA in Java

java

```java
import java.security.*;
import javax.crypto.Cipher;
import java.util.Base64;

public class RSAEncryption {
    
    private static final String ALGORITHM = "RSA/ECB/OAEPWithSHA-256AndMGF1Padding";
    // OAEP padding is secure, PKCS1 is legacy (avoid for new code)
    
    /**
     * Generate RSA key pair (2048-bit minimum!)
     */
    public static KeyPair generateKeyPair() throws Exception {
        KeyPairGenerator generator = KeyPairGenerator.getInstance("RSA");
        generator.initialize(2048);  // Use 4096 for extra security
        return generator.generateKeyPair();
    }
    
    /**
     * Encrypt with PUBLIC key
     * Anyone can do this - public key is shared
     */
    public static byte[] encrypt(byte[] plaintext, PublicKey publicKey) throws Exception {
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        cipher.init(Cipher.ENCRYPT_MODE, publicKey);
        return cipher.doFinal(plaintext);
    }
    
    /**
     * Decrypt with PRIVATE key
     * Only the key owner can do this
     */
    public static byte[] decrypt(byte[] ciphertext, PrivateKey privateKey) throws Exception {
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        cipher.init(Cipher.DECRYPT_MODE, privateKey);
        return cipher.doFinal(ciphertext);
    }
    
    // String convenience methods
    public static String encryptString(String plaintext, PublicKey publicKey) throws Exception {
        byte[] encrypted = encrypt(plaintext.getBytes("UTF-8"), publicKey);
        return Base64.getEncoder().encodeToString(encrypted);
    }
    
    public static String decryptString(String ciphertext, PrivateKey privateKey) throws Exception {
        byte[] encrypted = Base64.getDecoder().decode(ciphertext);
        byte[] decrypted = decrypt(encrypted, privateKey);
        return new String(decrypted, "UTF-8");
    }
}
```

### RSA Usage Example



```java
public class RSADemo {
    public static void main(String[] args) throws Exception {
        // Generate key pair
        KeyPair keyPair = RSAEncryption.generateKeyPair();
        PublicKey publicKey = keyPair.getPublic();    // Share this
        PrivateKey privateKey = keyPair.getPrivate(); // Keep SECRET!
        
        // Anyone can encrypt with public key
        String secret = "MySecretPassword123";
        String encrypted = RSAEncryption.encryptString(secret, publicKey);
        System.out.println("Encrypted: " + encrypted);
        
        // Only private key holder can decrypt
        String decrypted = RSAEncryption.decryptString(encrypted, privateKey);
        System.out.println("Decrypted: " + decrypted);
    }
}
```

### When to Use Which?
```
┌─────────────────────────────────────────────────────────────────────────┐
│                    ENCRYPTION DECISION TREE                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Need to encrypt data?                                                  │
│         │                                                               │
│         ▼                                                               │
│  Same party encrypts AND decrypts?                                      │
│         │                                                               │
│    YES  │  NO                                                           │
│    │    │                                                               │
│    │    └──► Different parties?                                         │
│    │              │                                                     │
│    │         YES  │                                                     │
│    │              ▼                                                     │
│    │         ASYMMETRIC (RSA/ECC)                                       │
│    │         • Key exchange                                             │
│    │         • Digital signatures                                       │
│    │         • TLS handshake                                            │
│    │                                                                    │
│    ▼                                                                    │
│  SYMMETRIC (AES-GCM)                                                    │
│  • Database field encryption                                            │
│  • File encryption                                                      │
│  • Session data                                                         │
│                                                                         │
│  In practice: HYBRID approach (asymmetric to exchange symmetric key)    │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 4. KEY SIZE MATTERS
```
KEY SIZE = TIME TO BRUTE FORCE

┌───────────────────┬────────────────────────────────────────────────────┐
│ Key Size          │ Brute Force Time (with current technology)         │
├───────────────────┼────────────────────────────────────────────────────┤
│ 56-bit (DES)      │ Hours to days (BROKEN - never use!)               │
│ 64-bit            │ Days to weeks (BROKEN)                            │
│ 128-bit (AES-128) │ Billions of years (secure)                        │
│ 256-bit (AES-256) │ Heat death of universe (very secure)              │
└───────────────────┴────────────────────────────────────────────────────┘
```

**==Each additional bit DOUBLES the brute force time!==**

### Recommended Key Sizes (2024+)

SYMMETRIC:
- AES-128: Acceptable for most use cases
- AES-256: Recommended for sensitive data, future-proof

ASYMMETRIC (RSA):
- RSA-1024: ❌ BROKEN - Never use!
- RSA-2048: ✅ Minimum acceptable (equivalent to ~112-bit symmetric)
- RSA-3072: ✅ Better (equivalent to ~128-bit symmetric)
- RSA-4096: ✅ Best for long-term secrets

ASYMMETRIC (ECC):
- P-256: ✅ Equivalent to AES-128 / RSA-3072
- P-384: ✅ Equivalent to AES-192
- P-521: ✅ Equivalent to AES-256

HASHING:
- MD5:    ❌ BROKEN
- SHA-1:  ❌ BROKEN
- SHA-256: ✅ Recommended
- SHA-384: ✅ High security
- SHA-512: ✅ Maximum security


---

## 5. SECURE RANDOM - The Foundation

**Critical:** Bad randomness = broken encryption.

java

```java
// ❌ NEVER use for security!
Random random = new Random();  // Predictable! Can be reverse-engineered.
int key = random.nextInt();    // Attacker can predict future values!

// ❌ NEVER use for security!
Random seeded = new Random(System.currentTimeMillis());  
// Attacker knows approximate time = can guess seed

// ✅ ALWAYS use for security!
SecureRandom secureRandom = new SecureRandom();
byte[] key = new byte[32];
secureRandom.nextBytes(key);  // Cryptographically secure
```

### Why ``java.util.Random`` is Dangerous

```java
java.util.Random uses a Linear Congruential Generator (LCG):
    next = (seed * 25214903917 + 11) mod 2^48
```

If attacker sees a few outputs, they can:
1. Reverse-engineer the seed
2. Predict ALL future "random" values
3. Break your encryption

``SecureRandom`` uses OS entropy sources (``/dev/urandom`` on Linux) which are truly unpredictable.


---

## ✅ SECURITY CHECKLIST FOR SESSION 2

□ Never confuse encoding (Base64) with encryption
□ Never use encryption for passwords (use hashing - next session)
□ Always use AES-GCM mode (never ECB!)
□ Never reuse IV/nonce with the same key
□ Use AES-256 for sensitive data
□ Use RSA-2048 minimum (RSA-4096 preferred)
□ Always use ``SecureRandom`` for key generation
□ Store keys securely (not in code, not in config files)
□ Use OAEP padding for RSA (not PKCS1v1.5)


---

## 🚫 COMMON MISTAKES

1. "I'll just Base64 encode the password"
   → Base64 is NOT security. Anyone can decode it.

2. "AES is AES, the mode doesn't matter"
   → ECB mode leaks patterns. Always use GCM or CBC with HMAC.

3. "I'll store the encryption key in application.properties"
   → Use a secrets manager (Vault, AWS Secrets Manager)

4. "1024-bit RSA should be enough"
   → It was broken years ago. Use 2048+ minimum.

5. "new Random() is fine for generating tokens"
   → Predictable! Always use ``SecureRandom`` for security.

6. "I'll use the same IV every time for simplicity"
   → Same IV + same key = pattern leakage. IV must be unique per encryption.

--- 
##  SESSION 2 COMPLETE

**Key Takeaways:**
- Encoding ≠ Encryption ≠ Hashing - know when to use each
- AES-GCM is your go-to symmetric encryption
- Never use ECB mode - patterns leak through
- RSA/ECC for key exchange and signatures, not bulk data
- Key size matters: AES-256, RSA-2048+ minimum
- Always use ``SecureRandom`` for cryptographic operations

#  CRYPTOGRAPHY FOR DEVELOPERS (Part 2) Password Hashing - The Art of Storing Secrets You Can't Read

## 1. WHY HASH PASSWORDS? (Not Encrypt!)

**The Core Question:** Why can't we just encrypt passwords?

```
ENCRYPTION PROBLEM:

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  Password: "MySecret123"                                                │
│       │                                                                 │
│       ▼                                                                 │
│  Encrypted: "x7Kj9mNpQ2..."  +  Key: "masterkey123"                     │
│       │                              │                                  │
│       │                              │                                  │
│       ▼                              ▼                                  │
│  Stored in Database            Stored... WHERE?                         │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

**PROBLEM 1: If attacker gets the key, ALL passwords exposed instantly**   
==**PROBLEM 2: You don't NEED to read passwords - just verify them**==         
**PROBLEM 3: Insider threat - anyone with key access sees all passwords**

```
HASHING SOLUTION:

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  Password: "MySecret123"                                                │
│       │                                                                 │
│       ▼                                                                 │
│  Hash: "$2a$12$LQv3c1yqBwe..."  (ONE-WAY, cannot reverse!)              │
│       │                                                                 │
│       ▼                                                                 │
│  Stored in Database                                                     │
│                                                                         │
│  TO VERIFY:                                                             │
│  1. User enters password                                                │
│  2. Hash the input                                                      │
│  3. Compare hashes                                                      │
│  4. If match → password correct                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

Even if database is stolen, ==attacker has **HASHES**, not **PASSWORDS**== They must crack each hash individually (if done right, takes years)

---

## 2. HASHING ALGORITHMS - The Evolution

### The Broken Ones: MD5 and SHA-1

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     ❌ MD5 - COMPLETELY BROKEN                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Created: 1991                                                          │
│  Output: 128-bit (32 hex characters)                                    │
│  Status: BROKEN since 2004                                              │
│                                                                         │
│  Example:                                                               │
│  "password" → "5f4dcc3b5aa765d61d8327deb882cf99"                        │
│                                                                         │
│  WHY IT'S BROKEN:                                                       │
│  • Collision attacks: Two different inputs can produce same hash        │
│  • Speed: Modern GPU can compute 50+ BILLION MD5 hashes per second      │
│  • Rainbow tables: Pre-computed tables exist for all common passwords   │
│                                                                         │
│  NEVER USE MD5 FOR:                                                     │
│  • Passwords                                                            │
│  • Security tokens                                                      │
│  • Digital signatures                                                   │
│  • Anything security-related!                                           │
│                                                                         │
│  MD5 is ONLY acceptable for:                                            │
│  • Non-security checksums (file integrity where attacks aren't a concern)│
│  • Legacy system compatibility (with migration plan)                    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                     ❌ SHA-1 - BROKEN                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Created: 1995                                                          │
│  Output: 160-bit (40 hex characters)                                    │
│  Status: BROKEN since 2017 (SHAttered attack)                           │
│                                                                         │
│  Example:                                                               │
│  "password" → "5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8"                │
│                                                                         │
│  WHY IT'S BROKEN:                                                       │
│  • Google demonstrated practical collision in 2017                      │
│  • Still too fast for password hashing (10+ billion/sec on GPU)         │
│  • Deprecated by browsers, certificate authorities                      │
│                                                                         │
│  NEVER USE SHA-1 FOR NEW SYSTEMS                                        │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### The "Okay for Data" Ones: SHA-256, SHA-512

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     ⚠️ SHA-256/512 - GOOD FOR DATA, BAD FOR PASSWORDS   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  SHA-256 Output: 256-bit (64 hex characters)                            │
│  SHA-512 Output: 512-bit (128 hex characters)                           │
│  Status: SECURE for integrity, NOT for passwords                        │
│                                                                         │
│  Example:                                                               │
│  "password" → "5e884898da28047d9166169...f7306bbf" (SHA-256)            │
│                                                                         │
│  WHY NOT FOR PASSWORDS:                                                 │
│  • Designed to be FAST (that's bad for passwords!)                      │
│  • GPU can compute 5+ billion SHA-256 hashes per second                 │
│  • No built-in salt                                                     │
│  • No work factor / cost parameter                                      │
│                                                                         │
│  GOOD FOR:                                                              │
│  ✅ File integrity verification                                         │
│  ✅ Digital signatures                                                  │
│  ✅ HMAC (keyed hashing)                                                │
│  ✅ Blockchain                                                          │
│  ✅ JWTs signature verification                                         │
│                                                                         │
│  BAD FOR:                                                               │
│  ❌ Password storage (too fast!)                                        │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### The Password Hashing Champions: ``bcrypt``, ``scrypt``, ``Argon2``


THE KEY INSIGHT:
- Regular hash functions are designed to be FAST.
- ==**Password hash functions are designed to be SLOW.==**

Why slow is good:
- User logs in once → 100ms delay is unnoticeable
- Attacker tries 1 billion passwords → 100ms × 1 billion = 3,170 YEARS


---

## 3. ``BCRYPT`` - The Industry Standard

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     ✅ BCRYPT - RECOMMENDED                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Created: 1999 (based on Blowfish cipher)                               │
│  Output: 60 characters                                                  │
│  Status: SECURE and widely supported                                    │
│                                                                         │
│  KEY FEATURES:                                                          │
│  • Built-in salt (automatic, unique per password)                       │
│  • Configurable work factor (cost)                                      │
│  • Deliberately slow                                                    │
│  • GPU-resistant (memory-hard operations)                               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Anatomy of a ``bcrypt`` Hash

```
$2a$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/X4.qHXeVZ5cLKoWWC
│ │  │  │                      │
│ │  │  │                      └── Hash (31 chars)
│ │  │  │
│ │  │  └── Salt (22 chars, Base64)
│ │  │
│ │  └── Cost factor (12 = 2^12 = 4096 iterations)
│ │
│ └── Algorithm version (2a, 2b, 2y)
│
└── bcrypt identifier
```

### Cost Factor Explained

**==How many times the algorithm iterates==**

```
Cost    Iterations    Time (approximate)
────────────────────────────────────────
  4         16           ~1 ms
  8        256          ~10 ms
 10       1024          ~50 ms
 12       4096         ~200 ms    ← RECOMMENDED MINIMUM
 14      16384         ~800 ms
 16      65536        ~3 seconds

Rule: Choose cost so hashing takes 100-500ms on YOUR server
      Increase cost as hardware gets faster
```

### ``bcrypt`` in Java (Spring Security)

```java
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
public class SecurityConfig {
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        // Cost factor of 12 (default is 10)
        return new BCryptPasswordEncoder(12);
    }
}

@Service
public class UserService {
    
    private final PasswordEncoder passwordEncoder;
    private final UserRepository userRepository;
    
    public UserService(PasswordEncoder passwordEncoder, UserRepository userRepository) {
        this.passwordEncoder = passwordEncoder;
        this.userRepository = userRepository;
    }
    
    /**
     * Register new user - hash password before storing
     */
    public User registerUser(String username, String rawPassword) {
        // Hash the password (salt is generated automatically!)
        String hashedPassword = passwordEncoder.encode(rawPassword);
        
        User user = new User();
        user.setUsername(username);
        user.setPassword(hashedPassword);  // Store the hash, NEVER the raw password
        
        return userRepository.save(user);
    }
    
    /**
     * Authenticate user - compare input with stored hash
     */
    public boolean authenticate(String username, String rawPassword) {
        User user = userRepository.findByUsername(username)
            .orElseThrow(() -> new UsernameNotFoundException("User not found"));
        
        // matches() extracts salt from stored hash and compares
        return passwordEncoder.matches(rawPassword, user.getPassword());
    }
}
```

### How ``bcrypt`` Verification Works
```
STORED HASH: $2a$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/X4.qHXeVZ5cLKoWWC

User enters: "password123"

Step 1: Extract salt from stored hash
        Salt = "LQv3c1yqBWVHxkd0LHAkCO"

Step 2: Hash input with SAME salt and cost
        bcrypt("password123", salt, cost=12)
        
Step 3: Compare result with stored hash
        If match → password correct
        If not → password wrong

The salt is NOT secret - it's stored with the hash.
Its purpose is to make each hash unique.
```

---

## 4. ``SCRYPT`` - Memory-Hard Hashing
```
┌─────────────────────────────────────────────────────────────────────────┐
│                     ✅ SCRYPT - MEMORY-HARD                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Created: 2009                                                          │
│  Designed by: Colin Percival (Tarsnap)                                  │
│  Status: SECURE, used by cryptocurrencies (Litecoin, Dogecoin)          │
│                                                                         │
│  KEY FEATURES:                                                          │
│  • Memory-hard: Requires lots of RAM to compute                         │
│  • Makes GPU/ASIC attacks expensive (need memory, not just compute)     │
│  • Configurable CPU cost, memory cost, parallelization                  │
│                                                                         │
│  PARAMETERS:                                                            │
│  • N (CPU/memory cost): Power of 2 (e.g., 16384)                        │
│  • r (block size): Usually 8                                            │
│  • p (parallelization): Usually 1                                       │
│                                                                         │
│  WHEN TO USE:                                                           │
│  • When you want GPU resistance                                         │
│  • When memory availability is controllable                             │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
````

### ``scrypt`` in Java

```java
import org.springframework.security.crypto.scrypt.SCryptPasswordEncoder;

@Configuration
public class SecurityConfig {
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        // Parameters: cpuCost, memoryCost, parallelization, keyLength, saltLength
        // Defaults: 16384, 8, 1, 32, 64
        return new SCryptPasswordEncoder(
            16384,  // N - CPU cost (power of 2)
            8,      // r - memory cost
            1,      // p - parallelization
            32,     // key length
            16      // salt length
        );
    }
}
```

---

## 5. ``ARGON2`` - The Modern Champion
```
┌─────────────────────────────────────────────────────────────────────────┐
│                     ✅ ARGON2ID - RECOMMENDED FOR NEW PROJECTS           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Created: 2015                                                          │
│  Status: Winner of Password Hashing Competition (PHC)                   │
│  Variants:                                                              │
│    • Argon2d: GPU-resistant (side-channel vulnerable)                   │
│    • Argon2i: Side-channel resistant (less GPU-resistant)               │
│    • Argon2id: HYBRID - Best of both! ← USE THIS ONE                    │
│                                                                         │
│  KEY FEATURES:                                                          │
│  • Memory-hard (configurable memory usage)                              │
│  • Time-hard (configurable iterations)                                  │
│  • Parallelism support                                                  │
│  • Resistant to GPU, FPGA, and ASIC attacks                             │
│  • Modern design, learned from bcrypt/scrypt weaknesses                 │
│                                                                         │
│  PARAMETERS:                                                            │
│  • Memory: Amount of RAM (in KB)                                        │
│  • Iterations: Time cost                                                │
│  • Parallelism: Number of threads                                       │
│                                                                         │
│  RECOMMENDED SETTINGS (OWASP):                                          │
│  • Memory: 64 MB (65536 KB)                                             │
│  • Iterations: 3                                                        │
│  • Parallelism: 4                                                       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
````

### ``Argon2`` in Java (Spring Security 5.3+)

```java
import org.springframework.security.crypto.argon2.Argon2PasswordEncoder;

@Configuration
public class SecurityConfig {
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        // Parameters: saltLength, hashLength, parallelism, memory (KB), iterations
        return new Argon2PasswordEncoder(
            16,     // salt length (bytes)
            32,     // hash length (bytes)
            4,      // parallelism (threads)
            65536,  // memory in KB (64 MB)
            3       // iterations
        );
    }
}

// Using default (reasonable) settings:
@Bean
public PasswordEncoder simpleArgon2Encoder() {
    return Argon2PasswordEncoder.defaultsForSpringSecurity_v5_8();
}
```

### Argon2 Hash Anatomy
```
$argon2id$v=19$m=65536,t=3,p=4$c2FsdHNhbHRzYWx0$hash...
│        │    │              │                  │
│        │    │              │                  └── Hash (Base64)
│        │    │              │
│        │    │              └── Salt (Base64)
│        │    │
│        │    └── Parameters: m=memory, t=iterations, p=parallelism
│        │
│        └── Version
│
└── Algorithm (argon2id)
```

---

## 6. COMPARISON: Which One to Choose?
```
┌───────────────┬─────────────┬─────────────┬─────────────┬──────────────┐
│               │   bcrypt    │   scrypt    │  Argon2id   │   SHA-256    │
├───────────────┼─────────────┼─────────────┼─────────────┼──────────────┤
│ Year          │    1999     │    2009     │    2015     │    2001      │
├───────────────┼─────────────┼─────────────┼─────────────┼──────────────┤
│ Memory-Hard   │   Partial   │     Yes     │     Yes     │     No       │
├───────────────┼─────────────┼─────────────┼─────────────┼──────────────┤
│ GPU Resistant │   Partial   │     Yes     │     Yes     │     No       │
├───────────────┼─────────────┼─────────────┼─────────────┼──────────────┤
│ Built-in Salt │     Yes     │     Yes     │     Yes     │     No       │
├───────────────┼─────────────┼─────────────┼─────────────┼──────────────┤
│ Adjustable    │     Yes     │     Yes     │     Yes     │     No       │
│ Work Factor   │             │             │             │              │
├───────────────┼─────────────┼─────────────┼─────────────┼──────────────┤
│ Library       │  Excellent  │    Good     │    Good     │  Excellent   │
│ Support       │             │             │             │              │
├───────────────┼─────────────┼─────────────┼─────────────┼──────────────┤
│ Recommended   │     ✅      │     ✅      │    ✅✅     │     ❌      │
│ for Passwords │             │             │   (best)    │              │
└───────────────┴─────────────┴─────────────┴─────────────┴──────────────┘

```

DECISION GUIDE:
━━━━━━━━━━━━━━━
- ==**New project, modern stack → ``Argon2id``**==
- ==**Need maximum compatibility → ``bcrypt``**==
- ==**Already using ``bcrypt`` → Keep it (it's still secure)==**
- Legacy system with SHA-256 → Migrate to ``bcrypt``/``Argon2id``!

---

## 7. SALTING - Why It's Essential

### The Rainbow Table Attack
```
WITHOUT SALT:

Password      SHA-256 Hash
─────────────────────────────────────────────────────────────────
"password"    5e884898da28047d9166169...
"123456"      8d969eef6ecad3c29a3a629...
"qwerty"      65e84be33532fb784c48129...
```

**==Attacker pre-computes hashes for millions of common passwords. If your hash matches one in their table → instant crack!==**

This is a RAINBOW TABLE attack.

```
WITH SALT:

User 1: password = "password", salt = "x7Kj9m"
        Hash = bcrypt("password" + "x7Kj9m") = "$2a$12$x7Kj9m..."

User 2: password = "password", salt = "Np2Qw8"
        Hash = bcrypt("password" + "Np2Qw8") = "$2a$12$Np2Qw8..."

SAME PASSWORD, DIFFERENT HASHES!

Attacker's rainbow table is now USELESS.
They must crack each user's password individually.
```

### Salt Rules

✅ CORRECT SALT USAGE:
- Unique salt for EVERY password (even if passwords are same)
- Cryptographically random (use SecureRandom)
- At least 16 bytes (128 bits)
- Store salt alongside hash (it's NOT secret)
- Generate NEW salt on password change

❌ WRONG SALT USAGE:
- Same salt for all users (defeats the purpose!)
- Predictable salt (username, email, timestamp)
- Short salt (< 16 bytes)
- Treating salt as secret


### Manual Salting with SHA-256 (Educational Only!)


```java
// ⚠️ EDUCATIONAL EXAMPLE - Use bcrypt/Argon2 in production!
// This shows HOW salting works, not how you should implement passwords

public class ManualSaltExample {
    
    public static String hashWithSalt(String password) {
        // Generate random salt
        byte[] salt = new byte[16];
        new SecureRandom().nextBytes(salt);
        
        // Combine password + salt
        String combined = password + Base64.getEncoder().encodeToString(salt);
        
        // Hash the combination
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        byte[] hash = md.digest(combined.getBytes(StandardCharsets.UTF_8));
        
        // Store: salt + hash (both needed for verification)
        return Base64.getEncoder().encodeToString(salt) + ":" + 
               Base64.getEncoder().encodeToString(hash);
    }
    
    public static boolean verify(String password, String stored) {
        String[] parts = stored.split(":");
        String salt = parts[0];
        String storedHash = parts[1];
        
        // Recreate hash with same salt
        String combined = password + salt;
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        byte[] hash = md.digest(combined.getBytes(StandardCharsets.UTF_8));
        String computedHash = Base64.getEncoder().encodeToString(hash);
        
        // Compare (use constant-time comparison in production!)
        return storedHash.equals(computedHash);
    }
}

// ✅ IN PRODUCTION, JUST USE:
passwordEncoder.encode(password);      // Salt handled automatically
passwordEncoder.matches(input, hash);  // Verification handled automatically
```

---

## 8. PEPPERING - Defense in Depth

**==SALT: Unique per password, stored with hash, NOT secret**== 
==**PEPPER: Same for all passwords, stored SEPARATELY, IS secret==**
```
┌─────────────────────────────────────────────────────────────────────────┐
│                           PEPPERING                                     │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Hash = bcrypt(password + pepper, salt)                                 │
│                                                                         │
│  PEPPER stored in:                                                      │
│  • Environment variable                                                 │
│  • Secrets manager (Vault, AWS Secrets Manager)                         │
│  • Hardware Security Module (HSM)                                       │
│  • NEVER in the database!                                               │
│                                                                         │
│  WHY PEPPER:                                                            │
│  • If database is stolen, attacker has hashes but NOT pepper            │
│  • Adds another layer even if bcrypt is somehow weakened                │
│  • Defense in depth                                                     │
│                                                                         │
│  TRADEOFFS:                                                             │
│  • Pepper rotation is complex                                           │
│  • If pepper is lost, ALL passwords become unverifiable                 │
│  • Adds operational complexity                                          │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Implementing Pepper in Spring

```java
@Service
public class PepperedPasswordService {
    
    private final PasswordEncoder encoder = new BCryptPasswordEncoder(12);
    
    @Value("${security.password.pepper}")  // From environment/secrets
    private String pepper;
    
    public String hashPassword(String rawPassword) {
        // Add pepper before hashing
        String peppered = rawPassword + pepper;
        return encoder.encode(peppered);
    }
    
    public boolean verifyPassword(String rawPassword, String storedHash) {
        // Add same pepper before verification
        String peppered = rawPassword + pepper;
        return encoder.matches(peppered, storedHash);
    }
}
```

### Alternative: HMAC-based Pepper

```java
@Service
public class HmacPepperService {
    
    @Value("${security.password.pepper}")
    private String pepperKey;
    
    private final PasswordEncoder bcrypt = new BCryptPasswordEncoder(12);
    
    /**
     * More secure: Use HMAC instead of concatenation
     */
    public String hashPassword(String rawPassword) throws Exception {
        // HMAC the password with pepper
        Mac mac = Mac.getInstance("HmacSHA256");
        SecretKeySpec keySpec = new SecretKeySpec(
            pepperKey.getBytes(StandardCharsets.UTF_8), "HmacSHA256"
        );
        mac.init(keySpec);
        byte[] hmacResult = mac.doFinal(rawPassword.getBytes(StandardCharsets.UTF_8));
        String pepperedPassword = Base64.getEncoder().encodeToString(hmacResult);
        
        // Then bcrypt the HMAC result
        return bcrypt.encode(pepperedPassword);
    }
    
    public boolean verifyPassword(String rawPassword, String storedHash) throws Exception {
        // Same HMAC process
        Mac mac = Mac.getInstance("HmacSHA256");
        SecretKeySpec keySpec = new SecretKeySpec(
            pepperKey.getBytes(StandardCharsets.UTF_8), "HmacSHA256"
        );
        mac.init(keySpec);
        byte[] hmacResult = mac.doFinal(rawPassword.getBytes(StandardCharsets.UTF_8));
        String pepperedPassword = Base64.getEncoder().encodeToString(hmacResult);
        
        return bcrypt.matches(pepperedPassword, storedHash);
    }
}
```

---

## 9. COMPLETE SECURE PASSWORD IMPLEMENTATION

```java
import org.springframework.security.crypto.argon2.Argon2PasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
public class PasswordConfig {
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        // Argon2id with strong parameters
        return new Argon2PasswordEncoder(
            16,      // salt length
            32,      // hash length  
            4,       // parallelism
            65536,   // 64 MB memory
            3        // iterations
        );
    }
}

@Entity
@Table(name = "users")
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(unique = true, nullable = false)
    private String username;
    
    @Column(nullable = false)
    private String passwordHash;  // NEVER name it just "password"
    
    @Column(nullable = false)
    private Instant passwordChangedAt;
    
    @Column(nullable = false)
    private int failedLoginAttempts;
    
    @Column
    private Instant lockedUntil;
    
    // Getters, setters...
}

@Service
@Transactional
public class AuthenticationService {
    
    private static final int MAX_FAILED_ATTEMPTS = 5;
    private static final Duration LOCKOUT_DURATION = Duration.ofMinutes(15);
    
    private final PasswordEncoder passwordEncoder;
    private final UserRepository userRepository;
    
    public AuthenticationService(PasswordEncoder passwordEncoder, 
                                  UserRepository userRepository) {
        this.passwordEncoder = passwordEncoder;
        this.userRepository = userRepository;
    }
    
    /**
     * Register new user with secure password storage
     */
    public User register(String username, String rawPassword) {
        // Validate password strength (covered in later session)
        validatePasswordStrength(rawPassword);
        
        User user = new User();
        user.setUsername(username.toLowerCase().trim());
        user.setPasswordHash(passwordEncoder.encode(rawPassword));
        user.setPasswordChangedAt(Instant.now());
        user.setFailedLoginAttempts(0);
        
        return userRepository.save(user);
    }
    
    /**
     * Authenticate user with brute-force protection
     */
    public AuthResult authenticate(String username, String rawPassword) {
        // Constant-time lookup to prevent timing attacks
        Optional<User> userOpt = userRepository.findByUsername(
            username.toLowerCase().trim()
        );
        
        // Always perform password check to prevent user enumeration
        // (timing attack: if user doesn't exist, response is faster)
        if (userOpt.isEmpty()) {
            // Hash a dummy password to maintain constant time
            passwordEncoder.matches(rawPassword, 
                "$argon2id$v=19$m=65536,t=3,p=4$dummy$dummyhash");
            return AuthResult.failure("Invalid credentials");
        }
        
        User user = userOpt.get();
        
        // Check if account is locked
        if (user.getLockedUntil() != null && 
            Instant.now().isBefore(user.getLockedUntil())) {
            return AuthResult.failure("Account locked. Try again later.");
        }
        
        // Verify password
        boolean matches = passwordEncoder.matches(rawPassword, user.getPasswordHash());
        
        if (matches) {
            // Reset failed attempts on success
            user.setFailedLoginAttempts(0);
            user.setLockedUntil(null);
            userRepository.save(user);
            return AuthResult.success(user);
        } else {
            // Increment failed attempts
            int attempts = user.getFailedLoginAttempts() + 1;
            user.setFailedLoginAttempts(attempts);
            
            if (attempts >= MAX_FAILED_ATTEMPTS) {
                user.setLockedUntil(Instant.now().plus(LOCKOUT_DURATION));
            }
            
            userRepository.save(user);
            return AuthResult.failure("Invalid credentials");
        }
    }
    
    /**
     * Change password - requires current password verification
     */
    public void changePassword(Long userId, String currentPassword, 
                               String newPassword) {
        User user = userRepository.findById(userId)
            .orElseThrow(() -> new UserNotFoundException(userId));
        
        // Verify current password
        if (!passwordEncoder.matches(currentPassword, user.getPasswordHash())) {
            throw new InvalidCredentialsException("Current password is incorrect");
        }
        
        // Prevent password reuse (compare with current)
        if (passwordEncoder.matches(newPassword, user.getPasswordHash())) {
            throw new PasswordPolicyException("New password cannot be same as current");
        }
        
        // Validate and set new password
        validatePasswordStrength(newPassword);
        user.setPasswordHash(passwordEncoder.encode(newPassword));
        user.setPasswordChangedAt(Instant.now());
        
        userRepository.save(user);
        
        // Invalidate all sessions (covered in Sessions topic)
        sessionService.invalidateAllSessions(userId);
    }
    
    private void validatePasswordStrength(String password) {
        // Minimum requirements (will cover in detail later)
        if (password.length() < 12) {
            throw new PasswordPolicyException("Password must be at least 12 characters");
        }
        // Add more rules: complexity, common password check, etc.
    }
}
```

---

## 10. MIGRATING FROM WEAK HASHES

If you have legacy ``MD5/SHA-1`` passwords:

```java
@Service
public class PasswordMigrationService {
    
    private final PasswordEncoder modernEncoder;  // Argon2
    private final UserRepository userRepository;
    
    /**
     * Strategy: Migrate on next successful login
     */
    public AuthResult authenticateAndMigrate(String username, String password) {
        User user = userRepository.findByUsername(username).orElse(null);
        if (user == null) return AuthResult.failure("Invalid credentials");
        
        String storedHash = user.getPasswordHash();
        
        // Check hash format to determine algorithm
        if (storedHash.startsWith("$argon2") || storedHash.startsWith("$2")) {
            // Already modern - use normal verification
            if (modernEncoder.matches(password, storedHash)) {
                return AuthResult.success(user);
            }
        } else if (isLegacyMd5Hash(storedHash)) {
            // Legacy MD5 - verify with MD5, then upgrade
            if (verifyMd5(password, storedHash)) {
                // Migrate to modern hash
                String newHash = modernEncoder.encode(password);
                user.setPasswordHash(newHash);
                userRepository.save(user);
                
                log.info("Migrated password hash for user: {}", username);
                return AuthResult.success(user);
            }
        }
        
        return AuthResult.failure("Invalid credentials");
    }
    
    private boolean isLegacyMd5Hash(String hash) {
        // MD5 produces 32 hex characters
        return hash.length() == 32 && hash.matches("[a-fA-F0-9]+");
    }
    
    private boolean verifyMd5(String password, String md5Hash) {
        String computed = DigestUtils.md5Hex(password);
        return computed.equalsIgnoreCase(md5Hash);
    }
}
```

---

## ✅ SECURITY CHECKLIST 
```
□ NEVER store passwords in plaintext
□ NEVER use MD5 or SHA-1 for passwords
□ NEVER use fast hashes (SHA-256) for passwords
□ USE bcrypt (cost 12+) or Argon2id for all passwords
□ Salt is automatic with bcrypt/Argon2 - don't manually implement
□ Consider peppering for defense in depth (store pepper in secrets manager)
□ Implement brute-force protection (account lockout)
□ Prevent user enumeration (constant-time responses)
□ Log authentication failures (but NOT passwords!)
□ Invalidate sessions on password change
□ Have a migration plan for legacy hashes
```

---

## 🚫 COMMON MISTAKES
```
1. "MD5 is fine, we add a salt"
   → MD5 is fundamentally broken. Salt doesn't fix collision vulnerabilities.

2. "We use SHA-256, that's secure"
   → SHA-256 is too fast for passwords. GPU cracks billions per second.

3. "Our salt is the username"
   → Predictable salt defeats the purpose. Use cryptographically random salt.

4. "Same salt for all users is fine"
   → This allows pre-computation attacks across your entire user base.

5. "bcrypt cost of 4 is enough, it's still slow"
   → Cost 4 = ~1ms. Attacker can try millions per second. Use 12+.

6. "We store the pepper in the database too"
   → Defeats the purpose! Pepper must be separate from database.

7. "If password is wrong, respond 'user not found'"
   → This leaks which usernames exist. Always say "invalid credentials."
```

---
##  SESSION 3 

**Key Takeaways:**
- Passwords must be HASHED (one-way), never encrypted (reversible)
- MD5 and SHA-1 are BROKEN - never use for security
- ``bcrypt``, ``scrypt``, ``Argon2id`` are designed for passwords (intentionally slow)
- Salt makes each hash unique, defeating rainbow tables
- Pepper adds defense in depth (separate secret)
- Modern algorithms handle salt automatically - don't reinvent the wheel
- Migrate legacy hashes progressively on user login

# CRYPTOGRAPHY FOR DEVELOPERS (Part 3) Digital Signatures, Certificates & TLS - The Trust Infrastructure



## 1. DIGITAL SIGNATURES - Proving "I Wrote This"

### The Problem Signatures Solve

```
SCENARIO: Alice sends Bob a message "Transfer $1000 to Bob"

WITHOUT SIGNATURES:

Alice ─────── "Transfer $1000 to Bob" ──────► Bob
                        │
                        │ Attacker intercepts
                        ▼
              "Transfer $10000 to Attacker"
                        │
                        └──────────────────────► Bob (thinks it's from Alice!)
```

PROBLEMS:
1. **Bob can't verify the message is really FROM Alice (authenticity)**
2. **Bob can't verify the message wasn't MODIFIED (integrity)**
3. **Alice can later deny sending it (non-repudiation)**

### How Digital Signatures Work

```
SIGNING (Alice):
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  Original Message: "Transfer $1000 to Bob"                              │
│         │                                                               │
│         ▼                                                               │
│  ┌─────────────┐                                                        │
│  │   HASH      │  (SHA-256)                                             │
│  └─────────────┘                                                        │
│         │                                                               │
│         ▼                                                               │
│  Hash: "a1b2c3d4..."                                                    │
│         │                                                               │
│         │  + Alice's PRIVATE Key 🔐                                     │
│         ▼                                                               │
│  ┌─────────────┐                                                        │
│  │   ENCRYPT   │  (RSA/ECDSA)                                           │
│  └─────────────┘                                                        │
│         │                                                               │
│         ▼                                                               │
│  Signature: "x7Kj9mNp..."                                               │
│                                                                         │
│  Alice sends: Message + Signature                                       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘


VERIFICATION (Bob):
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  Received: Message + Signature                                          │
│                                                                         │
│  STEP 1: Hash the received message                                      │
│  ┌─────────────┐                                                        │
│  │   HASH      │  "Transfer $1000 to Bob" → "a1b2c3d4..."               │
│  └─────────────┘                                                        │
│                                                                         │
│  STEP 2: Decrypt signature with Alice's PUBLIC key 🔓                   │
│  ┌─────────────┐                                                        │
│  │   DECRYPT   │  "x7Kj9mNp..." → "a1b2c3d4..."                         │
│  └─────────────┘                                                        │
│                                                                         │
│  STEP 3: Compare                                                        │
│                                                                         │
│  Hash from message: "a1b2c3d4..."                                       │
│  Hash from signature: "a1b2c3d4..."                                     │
│                       ════════════                                      │
│                         MATCH! ✅                                        │
│                                                                         │
│  ✓ Message is authentic (only Alice has the private key)                │
│  ✓ Message has integrity (hash matches)                                 │
│  ✓ Alice cannot deny sending it (non-repudiation)                       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Signature Algorithms

```
┌─────────────────┬────────────────────────────────────────────────────────┐
│ Algorithm       │ Description                                            │
├─────────────────┼────────────────────────────────────────────────────────┤
│ RSA-SHA256      │ RSA signature with SHA-256 hash                        │
│                 │ • Widely supported                                     │
│                 │ • Larger signatures (256-512 bytes)                    │
│                 │ • Use RSA-2048 or RSA-4096 keys                        │
├─────────────────┼────────────────────────────────────────────────────────┤
│ ECDSA           │ Elliptic Curve Digital Signature Algorithm             │
│                 │ • Smaller signatures (64-72 bytes)                     │
│                 │ • Faster than RSA                                      │
│                 │ • Use P-256 or P-384 curves                            │
├─────────────────┼────────────────────────────────────────────────────────┤
│ Ed25519         │ Edwards-curve Digital Signature Algorithm              │
│                 │ • Modern, fast, secure                                 │
│                 │ • Fixed 64-byte signatures                             │
│                 │ • Recommended for new systems                          │
├─────────────────┼────────────────────────────────────────────────────────┤
│ RSA-SHA1        │ ❌ DEPRECATED - SHA-1 is broken                        │
│ DSA             │ ❌ DEPRECATED - Use ECDSA instead                      │
└─────────────────┴────────────────────────────────────────────────────────┘
```

### Digital Signatures in Java

java

```java
import java.security.*;
import java.util.Base64;

public class DigitalSignatureExample {
    
    private static final String ALGORITHM = "SHA256withRSA";
    
    /**
     * Generate RSA key pair for signing
     */
    public static KeyPair generateKeyPair() throws Exception {
        KeyPairGenerator generator = KeyPairGenerator.getInstance("RSA");
        generator.initialize(2048);
        return generator.generateKeyPair();
    }
    
    /**
     * Sign data with private key
     */
    public static byte[] sign(byte[] data, PrivateKey privateKey) throws Exception {
        Signature signature = Signature.getInstance(ALGORITHM);
        signature.initSign(privateKey);
        signature.update(data);
        return signature.sign();
    }
    
    /**
     * Verify signature with public key
     */
    public static boolean verify(byte[] data, byte[] signatureBytes, 
                                  PublicKey publicKey) throws Exception {
        Signature signature = Signature.getInstance(ALGORITHM);
        signature.initVerify(publicKey);
        signature.update(data);
        return signature.verify(signatureBytes);
    }
    
    public static void main(String[] args) throws Exception {
        // Generate keys
        KeyPair keyPair = generateKeyPair();
        
        // Message to sign
        String message = "Transfer $1000 to Bob";
        byte[] messageBytes = message.getBytes("UTF-8");
        
        // Sign with private key
        byte[] signatureBytes = sign(messageBytes, keyPair.getPrivate());
        System.out.println("Signature: " + 
            Base64.getEncoder().encodeToString(signatureBytes));
        
        // Verify with public key
        boolean valid = verify(messageBytes, signatureBytes, keyPair.getPublic());
        System.out.println("Signature valid: " + valid);  // true
        
        // Tamper with message
        String tampered = "Transfer $10000 to Attacker";
        boolean tamperedValid = verify(
            tampered.getBytes("UTF-8"), signatureBytes, keyPair.getPublic()
        );
        System.out.println("Tampered valid: " + tamperedValid);  // false!
    }
}
```

### Where Signatures Are Used
```
1. CODE SIGNING
   • JAR files signed by developers
   • Android APKs must be signed
   • Windows executables (.exe) signed
   → Proves code comes from trusted source

2. JWT TOKENS
   • JWT signature proves token wasn't modified
   • Server signs with private key
   • Anyone can verify with public key (RS256)
   → Session 7 covers this in depth

3. TLS CERTIFICATES
   • Certificate Authority signs your certificate
   • Browser verifies signature
   → Coming up in this session!

4. GIT COMMITS
   • Developers sign commits with GPG
   • Proves who made the commit
   → "Verified" badge on GitHub

5. DOCUMENTS
   • PDF digital signatures
   • DocuSign, Adobe Sign
   → Legal validity of electronic signatures
```

---

## 2. CERTIFICATES - Digital Identity Cards

### The Trust Problem

PROBLEM: How does Bob know he has Alice's REAL public key?

Attacker could say: "Here's Alice's public key" (but it's actually attacker's key!)

      Alice's Real Key: 🔓A
      Attacker's Key:   🔓X

Bob thinks he has 🔓A but actually has 🔓X
Now attacker can:
  • Decrypt messages Bob sends to "Alice"
  • Sign messages pretending to be Alice

==This is a **MAN-IN-THE-MIDDLE** attack.==


### Certificates Solve This

A CERTIFICATE is a SIGNED statement saying: "This public key belongs to this identity"

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        X.509 CERTIFICATE                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Subject: CN=www.google.com, O=Google LLC, L=Mountain View, ST=CA, C=US │
│                                                                         │
│  Issuer: CN=GTS CA 1C3, O=Google Trust Services LLC, C=US               │
│                                                                         │
│  Valid From: 2024-01-01                                                 │
│  Valid To:   2024-03-31                                                 │
│                                                                         │
│  Public Key: (RSA 2048-bit)                                             │
│  30 82 01 0a 02 82 01 01 00 bb 21 e9 b5 c6 3b 5c ...                   │
│                                                                         │
│  Signature Algorithm: SHA256withRSA                                     │
│  Signature: (signed by Issuer's private key)                            │
│  4a 7c 9d 2f 8b 5e 1a 3c ...                                           │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

Translation:
"Google Trust Services vouches that this public key belongs to www.google.com"
"If you trust Google Trust Services, you can trust this certificate"

### Certificate Fields Explained
```
┌──────────────────┬───────────────────────────────────────────────────────┐
│ Field            │ Meaning                                               │
├──────────────────┼───────────────────────────────────────────────────────┤
│ Subject          │ WHO this certificate is for                           │
│   CN             │ Common Name (domain name or entity name)              │
│   O              │ Organization                                          │
│   OU             │ Organizational Unit                                   │
│   L              │ Locality (city)                                       │
│   ST             │ State/Province                                        │
│   C              │ Country                                               │
├──────────────────┼───────────────────────────────────────────────────────┤
│ Issuer           │ WHO signed this certificate (the CA)                  │
├──────────────────┼───────────────────────────────────────────────────────┤
│ Serial Number    │ Unique ID from the issuer                             │
├──────────────────┼───────────────────────────────────────────────────────┤
│ Validity Period  │ Not Before / Not After dates                          │
├──────────────────┼───────────────────────────────────────────────────────┤
│ Public Key       │ The actual public key being certified                 │
├──────────────────┼───────────────────────────────────────────────────────┤
│ Extensions       │ Additional info (key usage, SAN, etc.)                │
│   SAN            │ Subject Alternative Names (additional domains)        │
│   Key Usage      │ What the key can be used for                          │
├──────────────────┼───────────────────────────────────────────────────────┤
│ Signature        │ CA's signature over all the above                     │
└──────────────────┴───────────────────────────────────────────────────────┘
```

---

## 3. PKI - Public Key Infrastructure

### The Chain of Trust

THE QUESTION: Why should I trust Google Trust Services?

ANSWER: Because MY BROWSER trusts them!

Browsers/OS come with PRE-INSTALLED "Root Certificates" These are Certificate Authorities (CAs) that browsers trust BY DEFAULT.


```
┌─────────────────────────────────────────────────────────────────────────┐
│                      CERTIFICATE CHAIN                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────────────────────────────┐                           │
│  │         ROOT CA CERTIFICATE             │  ← Pre-installed in       │
│  │   Subject: DigiCert Global Root CA      │     browser/OS            │
│  │   Issuer:  DigiCert Global Root CA      │     (SELF-SIGNED)         │
│  │   (Self-signed - trusts itself)         │                           │
│  └────────────────┬────────────────────────┘                           │
│                   │ Signs ↓                                             │
│  ┌────────────────▼────────────────────────┐                           │
│  │      INTERMEDIATE CA CERTIFICATE        │  ← Signed by Root         │
│  │   Subject: DigiCert TLS RSA SHA256 CA   │                           │
│  │   Issuer:  DigiCert Global Root CA      │                           │
│  └────────────────┬────────────────────────┘                           │
│                   │ Signs ↓                                             │
│  ┌────────────────▼────────────────────────┐                           │
│  │        END-ENTITY CERTIFICATE           │  ← Your website's cert    │
│  │   Subject: www.example.com              │     Signed by Intermediate│
│  │   Issuer:  DigiCert TLS RSA SHA256 CA   │                           │
│  └─────────────────────────────────────────┘                           │
│                                                                         │
│  VERIFICATION (bottom-up):                                              │
│  1. Is www.example.com signed by DigiCert TLS RSA SHA256 CA? ✓         │
│  2. Is DigiCert TLS RSA SHA256 CA signed by DigiCert Global Root? ✓    │
│  3. Is DigiCert Global Root in my trusted store? ✓                     │
│  4. CHAIN VERIFIED! ✅                                                  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Why Intermediate CAs?

ROOT CA private key is EXTREMELY valuable.
If compromised, attacker can impersonate ANY website.

PROTECTION STRATEGY:
- Root CA kept OFFLINE in vault (air-gapped)
- Root only signs Intermediate CA certificates (rarely)
- Intermediate CAs do daily signing operations
- If Intermediate is compromised, revoke it (Root is safe)

This is DEFENSE IN DEPTH applied to PKI!


### Types of Certificates
```
┌─────────────────┬────────────────────────────────────────────────────────┐
│ Type            │ What CA Verifies                                       │
├─────────────────┼────────────────────────────────────────────────────────┤
│ DV              │ Domain Validation                                      │
│ (Domain)        │ • You control the domain (DNS or email check)          │
│                 │ • Cheapest, fastest (minutes)                          │
│                 │ • Let's Encrypt provides FREE DV certs                 │
│                 │ • Good for: blogs, personal sites, APIs                │
├─────────────────┼────────────────────────────────────────────────────────┤
│ OV              │ Organization Validation                                │
│ (Organization)  │ • Domain ownership + organization exists               │
│                 │ • CA verifies business registration                    │
│                 │ • Days to issue                                        │
│                 │ • Good for: business websites                          │
├─────────────────┼────────────────────────────────────────────────────────┤
│ EV              │ Extended Validation                                    │
│ (Extended)      │ • Strictest verification (legal, operational, physical)│
│                 │ • Weeks to issue, most expensive                       │
│                 │ • Used to show green bar (browsers removed this)       │
│                 │ • Good for: banks, e-commerce (regulatory requirement) │
└─────────────────┴────────────────────────────────────────────────────────┘

FOR MOST APPLICATIONS: DV certificates (Let's Encrypt) are sufficient!
```

---

## 4. TLS/SSL HANDSHAKE - How HTTPS Works

### The Big Picture

HTTPS = HTTP + TLS

Before any HTTP data is sent, TLS handshake establishes:
1. AUTHENTICATION: Server proves its identity (certificate)
2. KEY EXCHANGE: Client and server agree on encryption keys
3. ENCRYPTION: All subsequent data is encrypted

```
┌──────────┐                                        ┌──────────┐
│  CLIENT  │                                        │  SERVER  │
│ (Browser)│                                        │ (Website)│
└────┬─────┘                                        └────┬─────┘
     │                                                   │
     │  ══════════ TLS HANDSHAKE (unencrypted) ═══════  │
     │                                                   │
     │──────────────── ClientHello ─────────────────────►│
     │                                                   │
     │◄─────────────── ServerHello ──────────────────────│
     │◄─────────────── Certificate ──────────────────────│
     │◄─────────────── ServerHelloDone ──────────────────│
     │                                                   │
     │──────────────── ClientKeyExchange ───────────────►│
     │──────────────── ChangeCipherSpec ────────────────►│
     │──────────────── Finished ────────────────────────►│
     │                                                   │
     │◄─────────────── ChangeCipherSpec ─────────────────│
     │◄─────────────── Finished ─────────────────────────│
     │                                                   │
     │  ═══════════ APPLICATION DATA (encrypted) ══════  │
     │                                                   │
     │◄════════════════ GET /index.html ════════════════►│
     │◄════════════════ HTTP Response ══════════════════►│
     │                                                   │
```

### TLS 1.2 Handshake Step-by-Step
```
STEP 1: CLIENT HELLO
┌─────────────────────────────────────────────────────────────────────────┐
│ Client → Server                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│ "Hi! I want to connect securely. Here's what I support:"                │
│                                                                         │
│ • TLS Version: 1.2, 1.3                                                 │
│ • Cipher Suites: TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,                 │
│                  TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256, ...             │
│ • Compression Methods: null                                             │
│ • Random: 32 bytes of random data (for key derivation)                  │
│ • Extensions: SNI (server name), supported_groups, etc.                 │
└─────────────────────────────────────────────────────────────────────────┘

STEP 2: SERVER HELLO
┌─────────────────────────────────────────────────────────────────────────┐
│ Server → Client                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│ "Got it! Let's use these:"                                              │
│                                                                         │
│ • TLS Version: 1.2                                                      │
│ • Cipher Suite: TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384                   │
│ • Random: 32 bytes of random data (server's contribution)               │
│ • Session ID: (for session resumption)                                  │
└─────────────────────────────────────────────────────────────────────────┘

STEP 3: CERTIFICATE
┌─────────────────────────────────────────────────────────────────────────┐
│ Server → Client                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│ "Here's my certificate chain. Verify my identity!"                      │
│                                                                         │
│ • Server Certificate (www.example.com)                                  │
│ • Intermediate CA Certificate                                           │
│ • (Root CA is already in client's trust store)                          │
└─────────────────────────────────────────────────────────────────────────┘

Client verifies:
✓ Certificate chain signatures valid
✓ Certificate not expired
✓ Certificate not revoked (OCSP/CRL)
✓ Domain name matches (www.example.com)
✓ Root CA is trusted

STEP 4: KEY EXCHANGE (ECDHE)
┌─────────────────────────────────────────────────────────────────────────┐
│ Both parties perform Elliptic Curve Diffie-Hellman                      │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│ Server: Generates ECDH key pair, sends public part                      │
│ Client: Generates ECDH key pair, sends public part                      │
│                                                                         │
│ MAGIC: Both can now compute the SAME shared secret!                     │
│        But anyone watching the exchange CANNOT compute it.              │
│                                                                         │
│ Shared Secret + Client Random + Server Random                           │
│                      ↓                                                  │
│              Master Secret                                              │
│                      ↓                                                  │
│         Session Keys (encryption + MAC)                                 │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

STEP 5: FINISHED
┌─────────────────────────────────────────────────────────────────────────┐
│ Both sides send "Finished" message encrypted with new keys              │
├─────────────────────────────────────────────────────────────────────────┤
│ • Proves both sides derived the same keys                               │
│ • Contains hash of entire handshake (prevents tampering)                │
│ • If either side's Finished is wrong → handshake fails                  │
└─────────────────────────────────────────────────────────────────────────┘

🎉 HANDSHAKE COMPLETE - All subsequent data is encrypted!
```

### TLS 1.3 - Faster and More Secure
```
TLS 1.3 (2018) improvements:

1. FASTER: 1-RTT handshake (vs 2-RTT in TLS 1.2)
   • Client sends key share in first message
   • Connection established in ONE round trip

2. MORE SECURE:
   • Removed insecure algorithms (RSA key exchange, CBC, SHA-1)
   • Only AEAD ciphers (AES-GCM, ChaCha20-Poly1305)
   • Forward secrecy REQUIRED (ECDHE always)

3. 0-RTT RESUMPTION:
   • Returning clients can send data immediately
   • (With replay attack considerations)

┌──────────┐                                        ┌──────────┐
│  CLIENT  │                                        │  SERVER  │
└────┬─────┘                                        └────┬─────┘
     │                                                   │
     │─── ClientHello + KeyShare ───────────────────────►│
     │                                                   │
     │◄── ServerHello + KeyShare + Cert + Finished ──────│
     │                                                   │
     │─── Finished ─────────────────────────────────────►│
     │                                                   │
     │◄═══════════ Encrypted Data ═════════════════════►│
     │                                                   │

Only 1 round trip! (TLS 1.2 needs 2)
```

---

## 5. CIPHER SUITES - What Gets Negotiated

### Anatomy of a Cipher Suite
```
TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
│    │     │        │   │   │    │
│    │     │        │   │   │    └── PRF Hash (key derivation)
│    │     │        │   │   │
│    │     │        │   │   └── AEAD Mode (authenticated encryption)
│    │     │        │   │
│    │     │        │   └── Key Size (256-bit)
│    │     │        │
│    │     │        └── Bulk Encryption Algorithm
│    │     │
│    │     └── Authentication (certificate signature verification)
│    │
│    └── Key Exchange Algorithm
│
└── Protocol


COMPONENTS:
- Key Exchange: ECDHE (Elliptic Curve Diffie-Hellman Ephemeral)
  - Creates shared secret
  - "Ephemeral" = new keys each session (forward secrecy)

- Authentication: RSA
  - How server proves identity (certificate signature type)

- Bulk Encryption: AES_256_GCM
  - Encrypts actual data
  - GCM = Galois/Counter Mode (authenticated encryption)

- PRF Hash: SHA384
  - Used for key derivation and handshake integrity
```

### Recommended Cipher Suites (2024)
```
✅ STRONG - USE THESE:

TLS 1.3 (only uses strong ciphers):
- TLS_AES_256_GCM_SHA384
- TLS_AES_128_GCM_SHA256
- TLS_CHACHA20_POLY1305_SHA256

TLS 1.2 (if needed for compatibility):
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384


❌ WEAK - DISABLE THESE:

- Anything with RSA key exchange (no forward secrecy):
  TLS_RSA_WITH_AES_256_CBC_SHA

- Anything with CBC mode (padding oracle attacks):
  TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA

- Anything with 3DES, RC4, DES:
  TLS_RSA_WITH_3DES_EDE_CBC_SHA

- Anything with MD5 or SHA-1:
  TLS_RSA_WITH_AES_128_CBC_SHA (uses SHA-1)
  
- NULL ciphers (no encryption!):
  TLS_RSA_WITH_NULL_SHA
```

---

## 6. FORWARD SECRECY - Protecting Past Sessions
```
THE PROBLEM (without forward secrecy):

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  2024: Attacker records encrypted TLS traffic                           │
│        (can't decrypt yet, but stores it)                               │
│                                                                         │
│  2030: Attacker steals server's private key                             │
│        (through hack, insider, quantum computer)                        │
│                                                                         │
│  RESULT: Attacker can decrypt ALL recorded traffic from 2024!           │
│          Passwords, credit cards, messages - everything!                │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘


THE SOLUTION (with forward secrecy - ECDHE):

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  Each session uses EPHEMERAL (temporary) keys for encryption.           │
│  Server's long-term private key only used for AUTHENTICATION.           │
│                                                                         │
│  Session 1: Ephemeral key K1 (discarded after session)                  │
│  Session 2: Ephemeral key K2 (discarded after session)                  │
│  Session 3: Ephemeral key K3 (discarded after session)                  │
│                                                                         │
│  Even if server's private key is stolen:                                │
│  • Attacker can impersonate server for FUTURE connections               │
│  • Attacker CANNOT decrypt PAST sessions (keys are gone!)               │
│                                                                         │
│  This is FORWARD SECRECY (also called Perfect Forward Secrecy / PFS)    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

ECDHE = Elliptic Curve Diffie-Hellman EPHEMERAL
        ────────────────────────────────────────
        The "E" is the important part!
```

---

## 7. COMMON TLS MISCONFIGURATIONS
```
┌─────────────────────────────────────────────────────────────────────────┐
│ ❌ MISCONFIGURATION 1: Supporting Old TLS Versions                      │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│ WRONG:                                                                  │
│ server.ssl.enabled-protocols=TLSv1,TLSv1.1,TLSv1.2                     │
│                                                                         │
│ WHY BAD:                                                                │
│ • TLS 1.0 has BEAST, POODLE vulnerabilities                            │
│ • TLS 1.1 has no modern cipher support                                  │
│ • Attacker can force downgrade to weak version                          │
│                                                                         │
│ CORRECT:                                                                │
│ server.ssl.enabled-protocols=TLSv1.2,TLSv1.3                           │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│ ❌ MISCONFIGURATION 2: Weak Cipher Suites                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│ WRONG:                                                                  │
│ server.ssl.ciphers=TLS_RSA_WITH_AES_128_CBC_SHA,... (RSA key exchange) │
│                                                                         │
│ WHY BAD:                                                                │
│ • No forward secrecy                                                    │
│ • CBC mode vulnerable to padding oracles                                │
│                                                                         │
│ CORRECT:                                                                │
│ server.ssl.ciphers=TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,...           │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│ ❌ MISCONFIGURATION 3: Missing Intermediate Certificates                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│ WRONG:                                                                  │
│ Only installing end-entity certificate, not the chain                   │
│                                                                         │
│ WHY BAD:                                                                │
│ • Some clients can't build the chain                                    │
│ • Results in "certificate not trusted" errors                           │
│                                                                         │
│ CORRECT:                                                                │
│ Install full chain: End-entity + Intermediate(s)                        │
│ (Root CA is NOT included - client has it)                               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│ ❌ MISCONFIGURATION 4: Expired Certificates                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│ WHY IT HAPPENS:                                                         │
│ • Certificates expire (90 days for Let's Encrypt, 1 year for others)   │
│ • No monitoring/alerting in place                                       │
│ • Manual renewal forgotten                                              │
│                                                                         │
│ SOLUTION:                                                               │
│ • Automate renewal (certbot, ACME protocol)                            │
│ • Monitor certificate expiration                                        │
│ • Alert 30 days before expiry                                          │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│ ❌ MISCONFIGURATION 5: Missing HSTS Header                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│ WRONG: No HSTS header, relying only on redirect HTTP → HTTPS           │
│                                                                         │
│ WHY BAD:                                                                │
│ • First request might be HTTP (interceptable)                           │
│ • SSL stripping attacks possible                                        │
│                                                                         │
│ CORRECT:                                                                │
│ Strict-Transport-Security: max-age=31536000; includeSubDomains         │
│                                                                         │
│ This tells browser: "Always use HTTPS, never try HTTP"                  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
````

---
## ✅ SECURITY CHECKLIST FOR SESSION 4
```
□ Understand difference between signing (private key) and verification (public key)
□ Know the certificate chain: Root CA → Intermediate CA → End-entity
□ Use TLS 1.2 minimum, prefer TLS 1.3
□ Only enable strong cipher suites (ECDHE + AES-GCM)
□ Ensure forward secrecy (ephemeral key exchange)
□ Install complete certificate chain (not just end-entity)
□ Monitor certificate expiration
□ Implement HSTS header
□ Use automated certificate renewal (Let's Encrypt + certbot)
□ Test TLS configuration with SSL Labs
```

---

## 🚫 COMMON MISTAKES
```
1. "Self-signed certificates are fine for production"
   → Browsers will show scary warnings. Users will ignore ALL warnings.
   → Get a real certificate (Let's Encrypt is FREE).

2. "We support TLS 1.0 for compatibility"
   → TLS 1.0 has known vulnerabilities. Drop it.
   → Any system still requiring TLS 1.0 has bigger problems.

3. "RSA key exchange is fine"
   → No forward secrecy. Use ECDHE.

4. "We'll renew certificates manually"
   → You'll forget. It's 2 AM on Saturday. Site goes down.
   → AUTOMATE certificate renewal.

5. "Certificate pinning will make us more secure"
   → Only if you have operational maturity to manage it.
   → Most apps should NOT pin (too risky operationally).

6. "Our internal APIs don't need TLS"
   → Zero Trust: encrypt everything, even internal traffic.
```

---


##  SESSION 4 COMPLETE

**Key Takeaways:**
- Digital signatures prove authenticity, integrity, and non-repudiation
- Certificates bind public keys to identities, signed by trusted CAs
- Certificate chains establish trust: Root → Intermediate → End-entity
- TLS handshake authenticates server and establishes encrypted channel
- Forward secrecy (ECDHE) protects past sessions if keys are later compromised
- TLS 1.3 is faster and more secure than TLS 1.2
- Automate certificate management to prevent outages

# AUTHENTICATION FUNDAMENTALS Who Are You? Proving Identity in the Digital World


