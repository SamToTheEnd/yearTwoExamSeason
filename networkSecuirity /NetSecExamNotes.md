# Computer and Network Security Study Guide

## PART 1: TRUE/FALSE QUESTIONS WITH JUSTIFICATIONS

### Key Concepts to Know

#### 1. History and Evolution of Security
- **FALSE:** The Ware report's diagram is no longer applicable to modern IT security.
    - **Justification:** The Ware report (1970s) established foundational concepts like the CIA triad (Confidentiality, Integrity, Availability) that remain fundamental to security frameworks today. Modern security models like Zero Trust still protect these same core attributes.

- **TRUE:** MULTICS inspired fundamental concepts of modern operating system access control.
    - **Justification:** MULTICS introduced critical security concepts including protection rings, access control lists, and privilege separation that heavily influenced UNIX and modern operating systems.

- **FALSE:** Commercial computers in the 1970s came with no security controls.
    - **Justification:** Systems in the 1970s like IBM's System/370 with RACF and MULTICS implemented basic security controls including user authentication, access controls, and privilege separation.
    - **Justification:** You can also argue this is True due to how weak and uncommon the security features were in the 70s on **most** machines.


- **TRUE:** The first computers were programmed in decimal.
    - **Justification:** Early computers like ENIAC (1945) used decimal number systems and were programmed through physical switches and cables before binary programming became standard.

- **TRUE**: The Rand Report (1970) highlighted security challenges in early multi-user systems.
    - **Justification**: The Rand Report emphasized resource sharing risks and laid groundwork for access control models, influencing later systems like MULTICS.

- **TRUE**: The Anderson Report (1972) formalized requirements for secure systems.
    - **Justification**: It introduced concepts like "reference validation mechanisms," directly leading to the development of reference monitors.

- **TRUE**: Saltzer & Schroeder’s principles (1975) remain foundational for secure system design.
    - **Justification:** Principles like "least privilege" and "fail-safe defaults" are still critical in modern security architectures.

#### 2. System Architecture and Memory
- **TRUE/FALSE:** Data and programs are separated in memory.
    - **Justification (TRUE):** Modern architectures implement memory segmentation that separates code (text segment) from data segments through W^X (Write XOR Execute) protection, preventing regions from being both writable and executable.
    - **Justification (FALSE):** Some architectures and systems don't strictly enforce this separation, allowing execution of data sections in certain configurations.

- **FALSE:** Data stored in a process' memory is always accompanied by type information.
    - **Justification:** Many programming languages (C/C++) allow raw memory manipulation without enforcing type metadata. Memory can contain arbitrary binary data without explicit type information.

#### 3. Network Security
- **FALSE:** The TCP handshake prevents man-in-the-middle attacks.
    - **Justification:** The TCP three-way handshake establishes connections but has no authentication mechanisms. An attacker can intercept packets and establish separate connections with both parties, relaying information between them.

- **FALSE:** ARP prevents man-in-the-middle attacks.
    - **Justification:** ARP has no authentication mechanisms and is vulnerable to ARP spoofing/poisoning. These vulnerabilities make ARP a common vector for performing man-in-the-middle attacks.

- **FALSE:** DNS by itself provides strong integrity guarantees.
    - **Justification:** Traditional DNS sends queries and responses unencrypted and unauthenticated, making it vulnerable to cache poisoning and spoofing attacks. DNSSEC was developed specifically to address these integrity issues.

#### 4. Web Security
- **FALSE:** If a script from london.ac.uk makes a request to royalholloway.ac.uk, cookies for london.ac.uk will be included.
    - **Justification:** Browsers only send cookies to the domain they belong to (same-origin policy), unless specifically configured with special attributes for cross-origin sharing.

- **FALSE:** Reflected cross-site scripting attacks are based on a vulnerability of the database system.
    - **Justification:** Reflected XSS attacks exploit web application input validation failures, not database vulnerabilities. They occur when untrusted user input is immediately returned without proper sanitization.

- **TRUE:** Javascript can be embedded in HTML in several tags.
    - **Justification:** JavaScript can be embedded in multiple HTML tags including: `<script>` (primary method), event handler attributes like `onclick`, `onload`, `href` with javascript: protocol, and inline event handlers.

#### 5. System Security
- **FALSE:** Process gates are a technique to prevent reference monitors.
    - **Justification:** Process gates are actually a mechanism to implement reference monitors by controlling how processes can call privileged operations, ensuring security checks when transitioning between privilege levels.

- **FALSE:** Unprivileged processes can modify the UNIX system clock.
    - **Justification:** Modifying the system clock in UNIX/Linux requires root/administrative privileges to prevent time-sensitive security mechanisms like authentication and logging from being tampered with.

- **FALSE:** UNIX user groups always have the same ID number as the user's UID.
    - **Justification:** UNIX user groups have their own identifiers (GIDs) that are separate from user IDs (UIDs), allowing users to belong to multiple groups and for groups to contain multiple users.

- **FALSE:** UNIX user groups never have the same ID number as the user's UID.
    - **Justification:** While typically different, there's no technical restriction preventing a GID from having the same value as a UID. The system treats them as separate entities even if they share the same number.

- **FALSE:** SYN cookies can have the secure flag and are then not sent in plain.
    - **Justification:** SYN cookies are TCP-level sequence numbers to prevent SYN flood attacks, not HTTP cookies. The "secure flag" applies only to HTTP cookies, not to TCP-level mechanisms.

- **FALSE:** Security policies should be written in legal language to be as secure as possible.
    - **Justification:** Security policies should be clear and understandable to all stakeholders. Complex legal language often leads to misinterpretation and non-compliance, reducing their effectiveness.

- **TRUE:** Saltzer & Schroeder’s "least privilege" principle is enforced in UNIX via SUID/SGID bits.
    - **Justification:** SUID allows temporary elevation of privileges, aligning with the principle of minimizing access rights.




    

    Evolution of Security by Decade:

        1970s: Mainframes with basic access controls (MULTICS, RACF). Emergence of foundational reports (Ware, Rand).

        1980s: Rise of PCs with minimal security; viruses like Brain (1986) emerged.

        1990s: Internet expansion led to firewalls and antivirus software. Major exploits (Morris Worm, 1988).

        2000s: Worms (Code Red, SQL Slammer), botnets. Adoption of HTTPS and DNSSEC.

        2010s: APTs (Advanced Persistent Threats), IoT vulnerabilities, cloud security challenges.



## PART 2: NETWORK SECURITY

### Key Acronyms to Know

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| DNS     | Domain Name System | Translates domain names to IP addresses |
| TCP     | Transmission Control Protocol | Connection-oriented, reliable transport protocol |
| UDP     | User Datagram Protocol | Connectionless, unreliable transport protocol |
| ARP     | Address Resolution Protocol | Maps IP addresses to MAC addresses on local networks |
| ICMP    | Internet Control Message Protocol | Used for diagnostics and error reporting in IP networks |
| MAC     | Media Access Control | Physical address of network interface |
| HTTP    | Hypertext Transfer Protocol | Protocol for web communication |
| HTTPS   | HTTP Secure | Encrypted version of HTTP using TLS/SSL |
| IP      | Internet Protocol | Network layer protocol for addressing and routing |
| TTL     | Time To Live | Controls how long data remains valid in cache or network |
| MITM    | Man In The Middle | Attack where attacker secretly relays/alters communication |
| DoS     | Denial of Service | Attack that attempts to make resources unavailable |
| DDoS    | Distributed Denial of Service | DoS attack from multiple sources |
| TLS/SSL | Transport Layer Security/Secure Sockets Layer | Cryptographic protocols for secure communication |
| DHCP    | Dynamic Host Configuration Protocol | Assigns IP addresses to devices on a network |
| NAT     | Network Address Translation | Maps private to public IP addresses |
| VLAN    | Virtual Local Area Network | Logical grouping of network devices |
| OSI     | Open Systems Interconnection | 7-layer reference model for networks |

### DNS Resolution Process

#### How DNS Resolution Works:
1. **DNS Query Initiation**: The client enters a domain name (e.g., example.com) in their browser, which needs to be resolved to an IP address.

2. **Local DNS Cache Check**: The client first checks its local DNS cache to see if this domain has been resolved recently.

3. **Query to Recursive Resolver**: If not in the cache, the client sends a query to its configured DNS resolver (typically provided by the ISP or a third-party like Google's 8.8.8.8).

4. **Root Server Query**: If the recursive resolver doesn't have the answer cached, it queries a root DNS server, which responds with the address of the appropriate Top-Level Domain (TLD) server (e.g., .com TLD server).

5. **TLD Server Query**: The recursive resolver queries the TLD server, which responds with the address of the authoritative name server for the specific domain.

6. **Authoritative Name Server Query**: The recursive resolver queries the authoritative name server, which responds with the IP address for the requested domain.

7. **Response to Client**: The recursive resolver returns the IP address to the client.

8. **Caching**: Both the client and the recursive resolver cache this information for a period specified by the Time-To-Live (TTL) value to speed up future requests.

```
Client                Recursive Resolver           Root Server
  |                          |                         |
  |---DNS query------------->|                         |
  |                          |---Query for TLD-------->|
  |                          |<--TLD server address----|
  |                          |                         |
  |                          |         TLD Server      |
  |                          |            |            |
  |                          |---Query for Auth NS---->|
  |                          |<--Auth NS address-------|
  |                          |                         |
  |                          |     Authoritative NS    |
  |                          |            |            |
  |                          |---Query for IP--------->|
  |                          |<--IP address------------|
  |                          |                         |
  |<--IP address response----|                         |
  |                          |                         |
```

#### DNS Security Weaknesses:
1. **Weak Authentication**: Standard DNS resolvers attempt to authenticate replies by:
    - Matching transaction IDs (only 16 bits - easily guessable)
    - Verifying source address (can be spoofed)
    - Confirming query name/type match
    - No cryptographic authentication in standard DNS

2. **DNS Cache Poisoning**:
    - Attacker sends spoofed responses before legitimate ones arrive
    - Short TTLs help attackers by requiring frequent resolutions, giving more attack opportunities
    - Can include additional "glue records" pointing domains to attacker's IP

3. **Protection Mechanisms**:
    - DNSSEC (adds digital signatures)
    - DNS over HTTPS/TLS (encrypts DNS traffic)
    - Random ports for DNS queries (increases entropy)
    - Source port randomization (harder to guess)

### ARP Protocol

#### How ARP Works:
1. **Need Identification**: Host needs MAC address for IP packet destination on same network
2. **ARP Request**: Broadcast packet to all devices (FF:FF:FF:FF:FF:FF) asking "Who has this IP?"
3. **ARP Reply**: Host with matching IP responds with its MAC address
4. **ARP Cache Update**: Sender updates its ARP table mapping IP to MAC address
5. **Packet Transmission**: Sender encapsulates IP packet with correct destination MAC

#### ARP Security Issues:
- No authentication mechanism for replies
- Enables attacks like:
    - **ARP Spoofing/Poisoning**: Attacker associates their MAC with legitimate IP
    - **MAC Flooding**: Overwhelming switches with fake MAC addresses
    - **Denial of Service**: Disrupting network with conflicting ARP information
    - **Session Hijacking**: Intercepting unencrypted session data

## DNS Security Weaknesses:

### Kaminsky Attack (2008):

#### Exploited DNS cache poisoning by flooding the resolver with fake responses for non-existent subdomains.

#### Impact: Allowed attackers to hijack entire domains by poisoning the resolver’s cache.

#### Mitigation: Increased source port randomization and DNSSEC adoption.

#### DNS Reflection Attacks:

- Abuse public DNS resolvers to amplify traffic towards a victim (e.g., sending large responses to spoofed queries).

- Prevention: Configuring resolvers to reject queries from unauthorized networks.

### Secure DNS Modes:

- DNSSEC: Adds cryptographic signatures to DNS records.

- DNS over HTTPS (DoH) / DNS over TLS (DoT): Encrypt DNS queries to prevent eavesdropping.

### TLS Stripping (SSL Stripping):

- Mechanism: Downgrades HTTPS connections to HTTP via MITM attacks.

- Prevention: HSTS (HTTP Strict Transport Security) headers enforce HTTPS-only connections.

## PART 3: SYSTEM SECURITY

### Key Acronyms to Know

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| UID     | User ID | Numeric user identifier in Unix-like systems |
| GID     | Group ID | Numeric group identifier |
| EUID    | Effective User ID | User ID used for permission checks |
| RGID    | Real Group ID | Original group ID of user |
| SUID    | Set User ID | Permission bit allowing execution with file owner's privileges |
| SGID    | Set Group ID | Permission bit allowing execution with file group's privileges |
| ACL     | Access Control List | Rules specifying which users/processes have access to objects |
| DAC     | Discretionary Access Control | Control based on identity of requestor and access rules |
| MAC     | Mandatory Access Control | System-enforced access control independent of user wishes |
| RBAC    | Role-Based Access Control | Access rights assigned to roles |
| NOP     | No Operation | Assembly instruction that does nothing |
| GDB     | GNU Debugger | Debugging tool for programs |
| TOP     | Trusted Operating Platform | Framework for secure computing environment |
| TOCTOU  | Time Of Check to Time Of Use | Race condition vulnerability |
| DEP     | Data Execution Prevention | Security feature preventing code execution from data pages |
| ASLR    | Address Space Layout Randomization | Randomizes memory addresses to prevent exploitation |
| SELinux | Security-Enhanced Linux | Implementation of MAC for Linux |

### Linux File System Security

#### Key Concepts:
1. **File Permissions** (3 digits):
    - First digit: Owner permissions
    - Second digit: Group permissions
    - Third digit: Others' permissions
    - Each digit: read (4) + write (2) + execute (1)
    - Example: chmod 750 (rwx r-x ---)

2. **Special Permission Bits**:
    - SUID (4000): Execute with owner's privileges
    - SGID (2000): Execute with group's privileges
    - Sticky bit (1000): Only file owner can delete/rename in directory

3. **Access Control Lists (ACLs)**:
    - More granular permissions beyond basic owner/group/others
    - Commands:
        - `getfacl`: View ACL settings
        - `setfacl`: Set ACL permissions
        - `setfacl -m u:user:permissions file`: Set user permissions
        - `setfacl -m g:group:permissions file`: Set group permissions
        - `setfacl -d`: Set default ACLs for new files

4. **User and Group Management**:
    - `/etc/passwd`: User account information
        - Format: `username:password_placeholder:UID:GID:GECOS:home_directory:shell`
    - `/etc/shadow`: Encrypted password storage
    - `/etc/group`: Group definitions

#### Example `/etc/passwd` File Analysis:
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
acooper:x:1299:1320:IT,A-1-24,x867:/home/IT/acooper:/bin/bash
```

- First field: Username
- Second field: `x` means password stored in `/etc/shadow`
- Third field: UID (0 for root)
- Fourth field: GID (primary group)
- Fifth field: GECOS (user info - name, location, phone, etc.)
- Sixth field: Home directory
- Seventh field: Login shell

### Buffer Overflow Vulnerabilities

#### Vulnerable Code Example:
```c
int main(int argc, char **argv){
    char lbuf[64];
    if (argc > 1)
        strcpy(lbuf, argv[1]);
    return(0);
}
```

#### Vulnerability Explanation:
- `strcpy()` performs no bounds checking
- If `argv[1]` exceeds buffer size (64 bytes), it overflows
- Overflow can overwrite return address on stack
- On x86-32, stack is typically executable by default

#### Exploitation Steps:
1. Craft payload: `[SHELLCODE][PADDING][RETURN ADDRESS]`
2. Often uses NOP sled for easier targeting: `[NOP SLED][SHELLCODE][PADDING][RETURN ADDRESS]`
3. Return address points to start of buffer or NOP sled
4. When function returns, execution jumps to shellcode
5. Shellcode executes with program's privileges

#### Protection Mechanisms:
- Stack canaries (stack cookies)
- Address Space Layout Randomization (ASLR)
- Data Execution Prevention (DEP/NX bit)
- Compiler security features

### Reference Monitors

#### Definition:
A reference monitor is a security mechanism that mediates all access attempts between subjects (users/processes) and objects (files/resources) in a computer system, enforcing access control policies.

#### Essential Properties:
1. **Complete Mediation**: Must intercept every access request with no bypass possible
2. **Tamperproof**: Must be protected from unauthorized modification
3. **Verifiable**: Must be simple enough to be thoroughly tested and validated

#### Implementations:
- Kernel-based reference monitors
- Virtual machine monitors (hypervisors)
- Hardware-based security modules
- Security microkernels

#### Security Violations:
- **Time-of-Check to Time-of-Use (TOCTOU)** race conditions
    - Example: Hard links creating alternate access paths to files
    - Checking permissions at one time, accessing file at another
    - Can bypass intended access controls




### Adversarial Model:

    Defines an attacker’s capabilities (e.g., network access, physical access) and goals (data theft, disruption).

### STRIDE Framework:

- Spoofing: Impersonating users/devices.

- Tampering: Unauthorized data modification.

- Repudiation: Inability to trace malicious actions.

- Information Disclosure: Data leaks.

- Denial of Service: Disrupting availability.

- Elevation of Privilege: Gaining unauthorized access.

### Security by Design:

#### Saltzer & Schroeder’s Principles:

- Least Privilege

- Fail-Safe Defaults

- Economy of Mechanism

- Complete Mediation

- open Design

### Virtual Memory Organization:

- Segmentation & Paging: Isolate processes’ memory spaces.

- ASLR: Randomizes memory addresses to hinder buffer overflow exploits.

### Processes & Execution Domains:

#### Protection Rings:

- Ring 0 (Kernel), Ring 3 (User applications). Gates (system calls) mediate transitions between rings.

#### Reference Monitor Location:

- Implemented in the OS kernel (e.g., SELinux), hypervisors, or hardware (e.g., Intel SGX).

## PART 4: WEB SECURITY

### Key Acronyms to Know

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| XSS     | Cross-Site Scripting | Attack injecting client-side scripts into web pages |
| CSRF    | Cross-Site Request Forgery | Tricks user browser into performing unwanted actions |
| SQL     | Structured Query Language | Language for database operations |
| SOP     | Same-Origin Policy | Browser security mechanism restricting how documents/scripts interact |
| DOM     | Document Object Model | Programming interface for HTML/XML documents |
| TLS     | Transport Layer Security | Cryptographic protocol securing communications |
| XML     | eXtensible Markup Language | Markup language defining rules for encoding documents |
| API     | Application Programming Interface | Interface allowing software components to communicate |
| JSON    | JavaScript Object Notation | Data interchange format |
| JWT     | JSON Web Token | Compact method for secure information transmission |
| CORS    | Cross-Origin Resource Sharing | Mechanism allowing restricted resources to be requested |
| CSP     | Content Security Policy | Added layer of security to detect/mitigate attacks |
| OWASP   | Open Web Application Security Project | Online community producing articles about web security |

### Cross-Site Scripting (XSS)

#### Main Vulnerability:
Insufficient validation or sanitization of user-supplied input that is later incorporated into web pages and executed by the browser.

#### General Principle:
XSS attacks involve injecting malicious client-side scripts (typically JavaScript) into web pages viewed by other users. When these users visit the affected page, the malicious script executes within their browser context, allowing attackers to:
- Steal cookies or session tokens
- Redirect users to malicious sites
- Perform actions on behalf of the victim
- Access sensitive information

The Same-Origin Policy (SOP) is both evaded and exploited:
- **Evaded**: Injected code appears to originate from the trusted website
- **Exploited**: Once executing within target origin, SOP grants the script full access to site resources

#### Types of XSS:
1. **Stored XSS (Persistent)**:
    - Malicious script is permanently stored on target servers (databases, forums, comments)
    - Activates whenever a user views the compromised content
    - More dangerous as it affects anyone who visits the page
    - Example: Forum post containing malicious script that steals cookies

2. **Reflected XSS (Non-persistent)**:
    - Malicious script is embedded in URL and reflected back in server response
    - Only activates when victim clicks specially crafted link
    - Requires social engineering to trick users
    - Example: Search query with script that gets reflected in results page

3. **DOM-based XSS**:
    - Vulnerability exists in client-side code
    - Payload never sent to server
    - Manipulation of the DOM environment in victim's browser
    - Example: Script modifying document.location.hash to inject code

#### Prevention:
- Input validation and sanitization
- Output encoding (HTML, JavaScript, URL, CSS encoding)
- Content Security Policy (CSP)
- X-XSS-Protection header
- HttpOnly cookies (inaccessible to JavaScript)

### SQL Injection

#### Description:
SQL injection occurs when unsanitized user input is incorporated into SQL queries, allowing attackers to modify query logic. By inserting SQL commands rather than expected data, attackers can bypass authentication, access sensitive data, or manipulate database contents.

#### Success Factors:
- Direct concatenation of user input into SQL queries
- Lack of input validation or sanitization
- Insufficient parameterization of queries
- Excessive database privileges

#### Example Vulnerability:
```php
$query = "SELECT * FROM members WHERE email='$EMAIL'";
```

#### Attack Payload:
To delete all entries from table foo:
```
' OR 1=1; DROP TABLE foo; --
```

This works because:
1. Single quote (') closes the email string
2. OR 1=1 makes the WHERE clause always true
3. Semicolon (;) terminates the first query
4. DROP TABLE foo executes a destructive command
5. Double dash (--) comments out the rest of the original query

#### Prevention:
1. **Parameterized Queries**:
   ```php
   $stmt = $conn->prepare("SELECT * FROM members WHERE email = ?");
   $stmt->bind_param("s", $email);
   ```

2. **Input Validation**: Whitelist acceptable inputs

3. **Stored Procedures**: Pre-compiled SQL statements

4. **Least Privilege**: Limit database user permissions

5. **Web Application Firewalls (WAF)**: Filter suspicious inputs

6. **Escaping Special Characters**: Use database-specific escaping functions

### Other Web Vulnerabilities

#### CSRF (Cross-Site Request Forgery):
- Tricks authenticated users into executing unwanted actions
- Exploits the trust a website has in a user's browser
- Prevention: Anti-CSRF tokens, SameSite cookies, referer checking

#### Server-Side Request Forgery (SSRF):
- Attacker causes server to make HTTP requests to attacker-chosen destination
- Can access internal services behind firewalls
- Prevention: Whitelist allowed URLs, disable redirects

#### XML External Entity (XXE):
- Attacks poorly configured XML parsers
- Can lead to file disclosure, SSRF, DoS
- Prevention: Disable DTD processing, use less complex data formats

#### Insecure Deserialization:
- Untrusted data processed by deserialization mechanisms
- Can lead to remote code execution
- Prevention: Integrity checks, type checking before deserialization

### Web Security Best Practices

1. **Input Validation**: Validate all user inputs on server-side
2. **Output Encoding**: Context-specific encoding for all user-controlled outputs
3. **Authentication Controls**: Multi-factor, session management, secure password storage
4. **HTTPS Everywhere**: Encrypt all communications with TLS
5. **Security Headers**: CSP, X-Frame-Options, X-Content-Type-Options
6. **Cookie Security**: HttpOnly, Secure, SameSite flags
7. **Principle of Least Privilege**: Minimize permissions for all components
8. **Regular Updates**: Keep all software and dependencies current
9. **Security Testing**: Regular vulnerability scanning and penetration testing
10. **Content Security Policy**: Restrict resource loading to trusted sources

### Clickjacking:

- Mechanism: Tricking users into clicking hidden UI elements (e.g., transparent iframes).

- Prevention: X-Frame-Options header, framebusting scripts.