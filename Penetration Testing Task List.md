### **PHASE 1: PRE-ENGAGEMENT & PLANNING**

### 1.1 Documentation Review

- [ ] Define testing scope (all devices vs specific devices only)
- [ ] Review existing cybersecurity policies and procedures
- [ ] Review network architecture diagrams and topology maps
- [ ] Review asset inventory (hardware/software)
- [ ] Review employee organizational chart and access matrix
- [ ] Review M365 configuration documentation
- [ ] Review internet-facing applications list
- [ ] Review third-party integrations and vendor access
- [ ] Review backup and recovery procedures
- [ ] Review incident response procedures
- [ ] Review BCP (Business Continuity Plan)/DRP (Disaster Recovery Plan) documentation

### 1.2 Scope Definition

- [ ] Identify all IP ranges and subnets (on-prem)
- [ ] Identify all M365 tenants and domains
- [ ] Identify all internet-facing assets (websites, portals, email)
- [ ] Identify all critical applications processing client data
- [ ] Identify all network devices (routers, switches, firewalls)
- [ ] Identify all server infrastructure (physical/virtual)
- [ ] Identify all workstations and laptops
- [ ] Identify all mobile devices
- [ ] Identify all wireless networks (guest and corporate)
- [ ] Identify all VPN access points
- [ ] Identify all data storage locations (on-prem and cloud)
- [ ] Identify all file servers and NAS devices
- [ ] Identify all printers and multifunction devices (MFDs)
- [ ] Identify all IoT devices (smart TVs, cameras, etc.)
- [ ] Identify all domain names owned by organization
- [ ] Identify excluded systems (if any)
- [ ] Identify all applications in use with versions (M365, Office apps, web browsers)
- [ ] Identify on-premise vs cloud assets (M365 migration status)
- [ ] Identify OS versions across all systems
- [ ] Identify end-of-life/obsolete technology
- [ ] Define network topology and architecture
- [ ] Define testing windows (business hours constraint)
- [ ] Define communication protocols and escalation paths
- [ ] Document government websites frequently accessed
- [ ] Document internet service providers and connections

### 1.3 Legal & Compliance

- [ ] Execute penetration testing agreement/contract
- [ ] Obtain written authorization from management
- [ ] Define rules of engagement (RoE)
- [ ] Establish emergency contact procedures
- [ ] Define data handling and confidentiality protocols
- [ ] Confirm insurance coverage for testing activities
- [ ] Review compliance with RBI Master Direction on Cyber Security Framework
- [ ] Review compliance with CERT-In directions
- [ ] Review compliance with IT Act 2000 and amendments
- [ ] Review compliance with DPDPA 2023 (Digital Personal Data Protection Act)
- [ ] Review data localization requirements compliance

---

### **PHASE 2: INFORMATION GATHERING & RECONNAISSANCE**

#### 2.1 Passive Reconnaissance

- [ ] OSINT gathering on company domain names
- [ ] DNS enumeration (subdomains, MX records, TXT records)
- [ ] WHOIS information gathering
- [ ] Search for exposed documents (PDFs, Excel files with metadata)
- [ ] Social media enumeration (LinkedIn employee profiles for sensitive data exposure)
- [ ] Search for data leaks in public breaches (Have I Been Pwned)
- [ ] Google dorking for exposed sensitive information
- [ ] Search Shodan/Censys for exposed services
- [ ] Check SSL certificate transparency logs
- [ ] Identify third-party integrations and vendors
- [ ] DNS enumeration and zone transfer attempts
- [ ] Check archive.org for historical website data

#### 2.2 Active Reconnaissance

- [ ] Subdomain enumeration
- [ ] Network range discovery and mapping
- [ ] Live host discovery (ping sweeps)
- [ ] Port scanning (all TCP/UDP ports on critical systems)
- [ ] Service version detection
- [ ] Operating system fingerprinting
- [ ] Banner grabbing from services
- [ ] Identify web technologies (CMS, frameworks, libraries)
- [ ] WAF/IPS/IDS detection
- [ ] Load balancer detection
- [ ] CDN identification
- [ ] Map network topology
- [ ] Identify trust relationships between systems
- [ ] Email server enumeration (VRFY, EXPN, RCPT TO)
- [ ] SNMP enumeration (community strings)
- [ ] SMB/NetBIOS enumeration
- [ ] NFS share enumeration
- [ ] LDAP enumeration
- [ ] VoIP/SIP service discovery
- [ ] Printer discovery and enumeration
- [ ] IPv6 service discovery

---

### **PHASE 3: VULNERABILITY ASSESSMENT**

### 3.1 Automated Vulnerability Scanning

- [ ] Run authenticated vulnerability scans on Windows systems
- [ ] Run authenticated vulnerability scans on network devices
- [ ] Run unauthenticated vulnerability scans (external perspective)
- [ ] Scan web applications with OWASP ZAP/Burp Suite
- [ ] Scan for missing security patches (OS level)
- [ ] Scan for missing security patches (application level)
- [ ] Scan for missing firmware updates (network devices)
- [ ] Scan M365 environment with security assessment tools
- [ ] Scan for SSL/TLS vulnerabilities and weak ciphers
- [ ] Scan for SMB vulnerabilities (EternalBlue, etc.)
- [ ] Scan for RDP vulnerabilities
- [ ] Check for default credentials on services
- [ ] Check for anonymous access to file shares
- [ ] Check for open database ports
- [ ] Identify outdated software versions
- [ ] Identify end-of-life/unsupported software

### 3.2 Configuration Review

- [ ] Review Windows domain controller configurations
- [ ] Review Active Directory security settings
- [ ] Review Group Policy Objects (GPOs)
- [ ] Review firewall rule configurations
- [ ] Review router/switch configurations
- [ ] Review wireless network security (WPA2/WPA3)
- [ ] Review VPN configurations and encryption
- [ ] Review M365 security center configurations
- [ ] Review Azure AD/Entra ID configurations
- [ ] Review Exchange Online security settings
- [ ] Review SharePoint/OneDrive permissions
- [ ] Review Teams security settings
- [ ] Review antivirus/EDR configurations
- [ ] Review browser security policies
- [ ] Review email security (SPF, DKIM, DMARC records)
- [ ] Review backup encryption settings
- [ ] Review printer/MFD security configurations
- [ ] Review NTP server configurations
- [ ] Review SNMP configurations and community strings
- [ ] Review remote access solutions (TeamViewer, AnyDesk, etc.)
- [ ] Review PowerShell execution policies
- [ ] Review Windows Defender/Security Center settings
- [ ] Review Windows Update settings and WSUS configuration
- [ ] Review local Windows Firewall rules on endpoints
- [ ] Review BitLocker configuration and key escrow
- [ ] Review AutoPlay/AutoRun settings

### 3.3 Compliance Gap Assessment

- [ ] Verify password policy compliance (complexity, length, expiry)
- [ ] Verify account lockout policies
- [ ] Verify session timeout configurations
- [ ] Verify vendor default password changes
- [ ] Verify baseline security configurations (CIS Benchmarks)
- [ ] Verify network segmentation implementation
- [ ] Verify logging and monitoring coverage
- [ ] Verify encryption for data-at-rest
- [ ] Verify encryption for data-in-transit
- [ ] Verify patch management process implementation
- [ ] Verify access control lists and permissions
- [ ] Verify privileged access management controls
- [ ] Verify MFA implementation for privileged accounts
- [ ] Verify MFA implementation for M365 access

#### 3.4 Network Infrastructure Scanning

- [ ] Internal network vulnerability scan
- [ ] External perimeter vulnerability scan
- [ ] Wireless network vulnerability assessment
- [ ] Firewall configuration review vs CIS standards
- [ ] Router security assessment
- [ ] Switch configuration review
- [ ] Network segmentation testing
- [ ] VLAN hopping attempts
- [ ] Network device default credential checks

#### 3.5 Operating System Vulnerabilities

- [ ] Windows OS vulnerability assessment
- [ ] Linux/Unix vulnerability assessment (if applicable)
- [ ] Missing security patches identification
- [ ] Kernel vulnerability checks
- [ ] Service misconfigurations
- [ ] Unnecessary services running
- [ ] Local privilege escalation vulnerabilities

#### 3.6 Access Control Testing

- [ ] Password policy compliance testing
  - [ ] Password complexity requirements (8+ chars, 3/4 char types)
  - [ ] Session timeout configuration
  - [ ] Account lockout after 5 attempts
  - [ ] 90-day password expiry
  - [ ] 90-day inactivity lockout
  - [ ] Vendor default password checks
  - [ ] Simultaneous session prevention
- [ ] Logical access rights review
- [ ] Physical access rights review
- [ ] Privileged access management testing
- [ ] Least privilege principle verification
- [ ] Separation of duties validation
- [ ] Multi-factor authentication (MFA) implementation check

#### 3.7 M365 Specific Configuration

- [ ] Azure AD security configuration
- [ ] Conditional access policies review
- [ ] SharePoint/OneDrive permissions audit
- [ ] Exchange Online security settings
- [ ] Microsoft Teams security configuration
- [ ] Data Loss Prevention (DLP) policy review
- [ ] Microsoft Defender configuration
- [ ] Mobile Device Management (MDM) policy review
- [ ] M365 audit logging configuration

---

## **PHASE 4: EXPLOITATION & ATTACK SIMULATION**

### 4.1 Network-Based Attacks

- [ ] Exploit known vulnerabilities in network devices
- [ ] Attempt network sniffing (ARP spoofing, packet capture)
- [ ] Test for man-in-the-middle opportunities
- [ ] Attempt VLAN hopping attacks
- [ ] Test wireless network cracking (if applicable)
- [ ] Attempt rogue DHCP server attacks
- [ ] Test DNS spoofing/poisoning
- [ ] Attempt IPv6 attacks (if IPv6 enabled)
- [ ] Test for broadcast storm vulnerabilities
- [ ] Attempt MAC flooding attacks
- [ ] Test network device authentication bypass
- [ ] Test for unmanaged/rogue devices on network
- [ ] Wireless network attacks (if applicable)
  - [ ] WPA/WPA2 cracking
  - [ ] Rogue access point detection
  - [ ] Evil twin attacks

### 4.2 System-Level Attacks

- [ ] Exploit unpatched Windows vulnerabilities
- [ ] Exploit SMB vulnerabilities (if found)
- [ ] Exploit RDP vulnerabilities (if found)
- [ ] Attempt Windows privilege escalation
- [ ] Test for kernel exploits
- [ ] Attempt pass-the-hash attacks
- [ ] Attempt pass-the-ticket attacks (Kerberos)
- [ ] Test for DLL hijacking vulnerabilities
- [ ] Test for unquoted service path vulnerabilities
- [ ] Attempt registry manipulation attacks
- [ ] Test for weak service permissions
- [ ] Attempt scheduled task abuse
- [ ] Local administrator abuse
- [ ] Credential harvesting
- [ ] Memory dumping (LSASS)
- [ ] Test for insecure file permissions

### 4.3 Active Directory Attacks

- [ ] Enumerate domain users and groups
- [ ] Enumerate domain computers and servers
- [ ] Attempt Kerberoasting attacks
- [ ] Attempt AS-REP roasting attacks
- [ ] Test for unconstrained delegation vulnerabilities
- [ ] Test for constrained delegation abuse
- [ ] Attempt DCSync attacks (if domain admin obtained)
- [ ] Test for NTLM relay opportunities
- [ ] Attempt LDAP enumeration and exploitation
- [ ] Test for GPO abuse opportunities
- [ ] Attempt Golden Ticket attacks (post-compromise)
- [ ] Attempt Silver Ticket attacks
- [ ] Test for certificate services vulnerabilities (AD CS)
- [ ] Enumerate privileged groups (Domain Admins, etc.)

### 4.4 Web Application Attacks

- [ ] Test for SQL injection vulnerabilities
- [ ] Test for Cross-Site Scripting (XSS)
- [ ] Test for Cross-Site Request Forgery (CSRF)
- [ ] Test for authentication bypass
- [ ] Test for authorization flaws (IDOR, privilege escalation)
- [ ] Test for session management vulnerabilities
- [ ] Test for insecure direct object references
- [ ] Test for file upload vulnerabilities
- [ ] Test for path traversal/directory traversal
- [ ] Test for remote code execution (RCE)
- [ ] Test for command injection
- [ ] Test for XML external entity (XXE) injection
- [ ] Test for server-side request forgery (SSRF)
- [ ] Test for insecure deserialization
- [ ] Test for business logic flaws
- [ ] Test API security (if REST/SOAP APIs exist)

### 4.5 Email & M365 Attacks

- [ ] Test email spoofing capabilities
- [ ] Test for email header injection
- [ ] Attempt OAuth token theft/abuse
- [ ] Test for Azure AD password spray attacks
- [ ] Attempt M365 account enumeration
- [ ] Test for conditional access policy bypass
- [ ] Test for MFA fatigue/bypass techniques
- [ ] Attempt SharePoint permission escalation
- [ ] Test for OneDrive external sharing vulnerabilities
- [ ] Test Teams external access controls
- [ ] Attempt mailbox delegation abuse
- [ ] Test for calendar injection attacks
- [ ] Test for Azure AD Connect vulnerabilities

### 4.6 Physical Security Testing (if in scope)

- [ ] Test physical access controls to server rooms
- [ ] Test access badge cloning vulnerabilities
- [ ] Attempt tailgating to restricted areas
- [ ] Test CCTV coverage and monitoring
- [ ] Check for unattended workstations (unlocked)
- [ ] Test USB port restrictions
- [ ] Attempt booting from external media
- [ ] Check for sensitive documents in trash/recycling
- [ ] Test visitor access procedures

### 4.7 Social Engineering Attacks

- [ ] Conduct phishing email campaign (test awareness)
- [ ] Test phone-based social engineering (vishing)
- [ ] Test SMS-based social engineering (smishing)
- [ ] Test response to suspicious attachment/link
- [ ] Test impersonation attacks (IT support, management)
- [ ] Test physical social engineering (tailgating, pretexting)
- [ ] Test information disclosure via phone/email
- [ ] Test employee reporting mechanisms

### 4.8 Credential Attacks

- [ ] Attempt password spraying attacks
- [ ] Attempt brute force attacks (where rate limiting absent)
- [ ] Test for weak/common passwords
- [ ] Crack captured password hashes
- [ ] Test for credential stuffing opportunities
- [ ] Attempt credential harvesting via phishing
- [ ] Test for stored credentials in applications
- [ ] Check for hardcoded credentials in scripts/configs
- [ ] Test for credentials in memory (Mimikatz)
- [ ] Check browser saved passwords
- [ ] Test for credentials in registry
- [ ] Check for credentials in configuration files

### 4.9 Data Exfiltration Testing

- [ ] Test USB device blocking controls
- [ ] Test email attachment size/type restrictions
- [ ] Test cloud storage access (Dropbox, Google Drive)
- [ ] Test FTP/SFTP data transfer capabilities
- [ ] Test HTTP/HTTPS data exfiltration
- [ ] Test DNS tunneling capabilities
- [ ] Test ICMP tunneling capabilities
- [ ] Test Bluetooth data transfer
- [ ] Test mobile hotspot usage restrictions
- [ ] Test printer/scanner usage for data theft
- [ ] Test screenshot/screen capture restrictions

---

## **PHASE 5: POST-EXPLOITATION**

### 5.1 Privilege Escalation

- [ ] Escalate from standard user to local admin
- [ ] Escalate from local admin to domain admin
- [ ] Test for service account privilege escalation
- [ ] Exploit misconfigured scheduled tasks
- [ ] Exploit misconfigured services
- [ ] Exploit AlwaysInstallElevated policy
- [ ] Test for token manipulation opportunities
- [ ] Test for UAC bypass techniques

### 5.2 Lateral Movement

- [ ] Move between workstations using compromised credentials
- [ ] Access file servers from compromised system
- [ ] Access database servers from compromised system
- [ ] Pivot through compromised systems to reach isolated networks
- [ ] Test remote desktop access to other systems
- [ ] Test PSExec/WMI/WinRM for lateral movement
- [ ] Test SSH lateral movement (if applicable)
- [ ] Map trust relationships for movement paths

### 5.3 Persistence Mechanisms

- [ ] Test for registry run key persistence
- [ ] Test for scheduled task persistence
- [ ] Test for service creation persistence
- [ ] Test for WMI event subscription persistence
- [ ] Test for startup folder persistence
- [ ] Test for DLL hijacking persistence
- [ ] Test for Golden Ticket persistence
- [ ] Test for backdoor account creation

### 5.4 Data Discovery & Collection

- [ ] Search for client-related data on systems
- [ ] Search for sensitive financial documents
- [ ] Search for employee personal information
- [ ] Search for password files/databases
- [ ] Search for configuration files with credentials
- [ ] Search for backup files
- [ ] Enumerate accessible file shares
- [ ] Enumerate SharePoint/OneDrive documents
- [ ] Search email for sensitive information
- [ ] Document data classification failures

### 5.5 Detection Evasion

- [ ] Test antivirus/EDR evasion techniques
- [ ] Test log tampering capabilities
- [ ] Test timestomping capabilities
- [ ] Test for IDS/IPS evasion
- [ ] Test obfuscation techniques (PowerShell, etc.)
- [ ] Test living-off-the-land binaries (LOLBins)
- [ ] Test process injection techniques
- [ ] Test DLL sideloading

---

### **PHASE 6: DATA PROTECTION & ENCRYPTION TESTING**

#### 6.1 Data-at-Rest Encryption

- [ ] Verify encryption on file servers
- [ ] Database encryption verification
- [ ] Workstation hard drive encryption (BitLocker)
- [ ] USB/removable media encryption
- [ ] Backup encryption verification
- [ ] Client data storage encryption check

#### 6.2 Data-in-Motion Encryption

- [ ] SSL/TLS implementation testing
- [ ] Certificate validity verification
- [ ] Weak cipher suite identification
- [ ] Email encryption (in transit) testing
- [ ] VPN encryption strength assessment
- [ ] File transfer security testing
- [ ] Internal traffic encryption verification

#### 6.3 Cryptographic Standards Review

- [ ] Encryption algorithm assessment
- [ ] Key management practices review
- [ ] Certificate management review
- [ ] Cryptographic key lifecycle verification
- [ ] Identify weak/deprecated algorithms (MD5, SHA1, DES)

#### 6.4 Encryption Key Management

- [ ] Review BitLocker key escrow to AD/Azure AD
- [ ] Review certificate expiration monitoring
- [ ] Review SSL/TLS certificate management process
- [ ] Test for hardcoded encryption keys
- [ ] Review key rotation procedures
- [ ] Test for encryption key backup procedures
- [ ] Verify secure key storage (not in plain text)

---

### **PHASE 7: LOGGING, MONITORING & DETECTION**

#### 7.1 Log Management Assessment

- [ ] Verify logging on operating systems
- [ ] Application logging verification
- [ ] Database logging check
- [ ] Network device logging
- [ ] Firewall logging review
- [ ] Wireless network logging
- [ ] M365 audit log configuration
- [ ] Privileged access logging
- [ ] Log retention period verification
- [ ] Log integrity protection check
- [ ] Verify PowerShell script block logging
- [ ] Verify PowerShell transcription logging
- [ ] Verify Windows Event Forwarding (WEF) configuration
- [ ] Verify Sysmon deployment (if applicable)
- [ ] Test log tampering detection
- [ ] Verify log compression and archival
- [ ] Test log accessibility for incident response

#### 7.2 Security Monitoring Capabilities

- [ ] SIEM/log aggregation solution review
- [ ] Event correlation capabilities
- [ ] Antivirus alert monitoring
- [ ] IDS/IPS deployment and effectiveness
- [ ] Security alert response time testing
- [ ] Anomaly detection capabilities
- [ ] Centralized log storage verification
- [ ] Log backup and archival process
- [ ] Time synchronization testing

#### 7.3 Threat Detection Testing

- [ ] Malware detection testing
- [ ] Ransomware simulation (in safe environment)
- [ ] Data exfiltration detection
- [ ] Lateral movement detection
- [ ] Privilege escalation detection
- [ ] Test antivirus/EDR bypass techniques
- [ ] Verify antivirus cannot be disabled by users

---

### **PHASE 8: DATA LEAKAGE PREVENTION**

#### 8.1 DLP Controls Testing

- [ ] USB storage device blocking test
- [ ] External drive mapping prevention
- [ ] Cloud storage upload blocking (Dropbox, Google Drive)
- [ ] Email DLP policy testing
- [ ] Web proxy DLP rules verification
- [ ] Printer/fax DLP controls
- [ ] Screen capture/screenshot controls
- [ ] M365 DLP policy effectiveness

#### 8.2 Data Exfiltration Attempts

- [ ] Email-based data exfiltration
- [ ] Web upload attempts
- [ ] DNS tunneling
- [ ] ICMP tunneling
- [ ] Steganography testing
- [ ] Bluetooth/wireless data transfer
- [ ] Mobile device data sync testing

#### 8.3 Insider Threat Indicators

- [ ] Test for monitoring of large data transfers
- [ ] Test for monitoring of after-hours access
- [ ] Test for monitoring of privileged access anomalies
- [ ] Test for monitoring of failed access attempts
- [ ] Test for user behavior analytics (UBA) capabilities

---

### **PHASE 9: MALWARE & ANTIVIRUS TESTING**

#### 9.1 Antivirus/EDR Assessment

- [ ] Verify antivirus deployment on all systems
- [ ] Signature update frequency check
- [ ] Central management console review
- [ ] Real-time protection verification
- [ ] Scheduled scan configuration
- [ ] Quarantine procedures testing
- [ ] User ability to disable AV (should be blocked)
- [ ] Endpoint Detection and Response (EDR) capabilities

#### 9.2 Malware Simulation

- [ ] EICAR test file detection
- [ ] Malicious payload delivery attempts
- [ ] Exploit kit testing (in controlled manner)
- [ ] Ransomware simulation (safe)
- [ ] Fileless malware techniques
- [ ] Living-off-the-land binaries (LOLBins)

#### 9.3 Specific Tests

- [ ] Test macro-enabled document blocking (Office)
- [ ] Test script execution blocking (PowerShell, VBScript)
- [ ] Test potentially unwanted application (PUA) blocking
- [ ] Test antivirus exclusion policies
- [ ] Test behavioral detection capabilities
- [ ] Test sandbox/detonation capabilities
- [ ] Test for antivirus evasion via encryption

---

### **PHASE 10: PATCH MANAGEMENT ASSESSMENT**

#### 10.1 Patch Status Verification

- [ ] Operating system patch status
- [ ] Middleware patch verification (web/app/DB servers)
- [ ] Firmware updates on network devices
- [ ] Application/software patch status
- [ ] Microsoft Office updates
- [ ] Web browser updates
- [ ] Third-party application updates
- [ ] M365 update policies

#### 10.2 Patch Management Process Review

- [ ] Patch deployment tools/process
- [ ] Patch testing procedures
- [ ] Patch deployment timeline based on severity
- [ ] Missing patch identification process
- [ ] Vulnerability intelligence sources
- [ ] Patch compliance monitoring
- [ ] Emergency patching procedures

---

### **PHASE 11: MOBILE DEVICE & ENDPOINT SECURITY**

#### 11.1 Mobile Device Management (MDM)

- [ ] MDM policy enforcement verification
- [ ] Device encryption requirements
- [ ] Remote wipe capability testing
- [ ] Application whitelisting/blacklisting
- [ ] Mobile device access controls
- [ ] BYOD policy compliance
- [ ] M365 mobile app security
- [ ] Mobile device compliance policies

#### 11.2 Endpoint Security

- [ ] Host-based firewall configuration
- [ ] Application whitelisting verification
- [ ] USB device control
- [ ] Local admin rights assessment
- [ ] Workstation hardening review
- [ ] Screen lock enforcement
- [ ] Unattended session timeout

#### 11.3 Endpoint Hardening

- [ ] Test SMBv1 is disabled
- [ ] Test LLMNR/NBT-NS is disabled
- [ ] Test WPAD is disabled
- [ ] Verify unnecessary services are disabled
- [ ] Verify unnecessary protocols are disabled
- [ ] Test for clear-text protocols (Telnet, FTP, HTTP)
- [ ] Verify secure boot configuration
- [ ] Test for firmware/BIOS passwords
- [ ] Test for boot from USB prevention

---

### **PHASE 12: BACKUP & DISASTER RECOVERY TESTING**

#### 12.1 Backup Security Assessment

- [ ] Backup system security review
- [ ] Backup encryption verification
- [ ] Backup storage location security
- [ ] Offsite backup procedures
- [ ] Backup inventory maintenance
- [ ] Backup access controls
- [ ] Backup retention policy
- [ ] Client data backup verification

#### 12.2 Disaster Recovery Testing

- [ ] BCP/DRP documentation review
- [ ] RTO/RPO verification
- [ ] Recovery site assessment (Hot/Warm/Cold)
- [ ] Call tree testing
- [ ] Backup restoration testing
- [ ] Failover procedures validation
- [ ] Data integrity post-recovery

---

### **PHASE 13: INCIDENT RESPONSE TESTING**

#### 13.1 Incident Response Capability

- [ ] Incident response plan review
- [ ] Incident detection capabilities
- [ ] Incident notification procedures
- [ ] Incident response team roles verification
- [ ] Incident containment procedures
- [ ] Incident documentation process
- [ ] Forensic capability assessment
- [ ] Lessons learned process
- [ ] Client notification procedures

#### 13.2 Simulated Incident Testing

- [ ] Ransomware incident simulation
- [ ] Data breach scenario
- [ ] DDoS attack simulation
- [ ] Insider threat scenario
- [ ] Supply chain compromise scenario
- [ ] Response time measurement
- [ ] Communication effectiveness

#### 13.3 Cyber Attack Simulation

- [ ] Conduct phishing simulation exercise
- [ ] Measure employee click rates
- [ ] Measure employee reporting rates
- [ ] Test credential harvesting page detection
- [ ] Test malicious attachment detection
- [ ] Test suspicious link reporting process
- [ ] Verify control gaps in employee behavior
- [ ] Document policy/procedure gaps identified

---

### **PHASE 14: PHYSICAL SECURITY TESTING**

#### 14.1 Physical Access Controls

- [ ] Entrance security assessment
- [ ] Badge/access card system testing
- [ ] Visitor management procedures
- [ ] Tailgating/piggybacking attempts
- [ ] Server room/data center access controls
- [ ] CCTV coverage and monitoring
- [ ] Physical access log review
- [ ] After-hours security measures

#### 14.2 Physical Media Security

- [ ] Data destruction procedures
- [ ] Secure disposal verification
- [ ] Paper document destruction
- [ ] Hard drive wiping/destruction
- [ ] Removable media handling
- [ ] Equipment decommissioning process

---

### **PHASE 15: THIRD-PARTY & SUPPLY CHAIN SECURITY**

- [ ] Vendor security assessment process
- [ ] Third-party access controls
- [ ] Vendor patch management responsibility
- [ ] Supply chain risk assessment
- [ ] Third-party data handling verification
- [ ] Vendor security agreements review
- [ ] Cloud service provider security (M365)

---

### **PHASE 16: COMPLIANCE & GOVERNANCE**

#### 16.1 Policy & Procedure Review

- [ ] Information security policy completeness
- [ ] Acceptable use policy
- [ ] Data classification policy
- [ ] Data retention policy
- [ ] Remote work policy
- [ ] BYOD policy
- [ ] Cryptographic policy
- [ ] Incident response policy

#### 16.2 Security Awareness

- [ ] Training program documentation review
- [ ] Training frequency verification
- [ ] Training content assessment
- [ ] Training attendance records
- [ ] Training effectiveness measurement
- [ ] Role-based training verification
- [ ] Contractor/temporary staff training

#### 16.3 Audit & Compliance

- [ ] Internal audit function review
- [ ] Security control compliance testing
- [ ] Audit log review procedures
- [ ] Compliance reporting mechanisms
- [ ] Independent security assessment history
- [ ] Regulatory compliance verification

---

### **PHASE 17: CLOUD SECURITY (M365 Specific)**

#### 17.1 M365 Security Assessment

- [ ] Azure AD security score review
- [ ] Microsoft Secure Score assessment
- [ ] Identity protection policies
- [ ] Privileged Identity Management (PIM)
- [ ] Application permission review
- [ ] OAuth application audit
- [ ] Guest user access review
- [ ] External sharing settings
- [ ] Information protection labels
- [ ] Sensitivity labels configuration

#### 17.2 M365 Threat Protection

- [ ] Microsoft Defender for Office 365
- [ ] Safe Links configuration
- [ ] Safe Attachments configuration
- [ ] Anti-phishing policies
- [ ] Anti-spam policies
- [ ] Anti-malware policies
- [ ] Threat intelligence integration
- [ ] Attack simulation training

#### 17.3 M365 Compliance & Governance

- [ ] Review Microsoft Compliance Manager score
- [ ] Review retention policies
- [ ] Review eDiscovery configurations
- [ ] Review legal hold configurations
- [ ] Review audit log retention
- [ ] Review information barriers
- [ ] Review communication compliance policies
- [ ] Review insider risk management settings

#### 17.4 M365 Data Protection

- [ ] Test Azure Information Protection (AIP) labels
- [ ] Test rights management (RMS) effectiveness
- [ ] Test encryption for emails in transit
- [ ] Test customer key configuration (if applicable)
- [ ] Test double key encryption (if applicable)
- [ ] Review M365 data residency compliance

---

### **PHASE 18: REPORTING & DOCUMENTATION**

#### 18.1 Finding Documentation

- [ ] Document all vulnerabilities discovered
- [ ] Assign CVSS scores to technical vulnerabilities
- [ ] Classify findings by severity (Critical/High/Medium/Low)
- [ ] Map findings to client control gaps
- [ ] Provide proof-of-concept for critical findings
- [ ] Include screenshots and evidence
- [ ] Document exploitation paths and impact
- [ ] Identify affected systems/applications

#### 18.2 Report Deliverables

- [ ] Executive summary with business risk context
- [ ] Technical findings report with detailed descriptions
- [ ] Risk assessment and business impact
- [ ] Remediation recommendations (prioritized)
- [ ] Compliance gap mapping (client controls)
- [ ] Industry standard alignment (CIS, NIST, OWASP)
- [ ] Remediation timeline suggestions
- [ ] Attack chain visualization
- [ ] Risk heat map
- [ ] Retest requirements
- [ ] Security posture improvement roadmap

---

### **PHASE 19: POST-TESTING ACTIVITIES**

### 19.1 Cleanup & Restoration

- [ ] Secure deletion of all test data
- [ ] Return/destroy any obtained credentials
- [ ] Remove any testing artifacts/backdoors
- [ ] Remove all testing tools from systems
- [ ] Remove test accounts created
- [ ] Remove persistence mechanisms
- [ ] Restore any modified configurations
- [ ] Verify system stability post-testing
- [ ] Document cleanup activities

### 19.2 Retesting & Validation

- [ ] Schedule retest for critical findings
- [ ] Validate remediation effectiveness
- [ ] Issue updated report with retest results
- [ ] Close validated findings
- [ ] Document remaining risks

### 19.3 Continuous Improvement

- [ ] Recommend security program improvements
- [ ] Suggest security tool implementations
- [ ] Recommend security awareness initiatives
- [ ] Provide threat intelligence briefings
- [ ] Suggest next assessment scope and timing

#### 19.4 Testing Standards Methodology Documentation

- [ ] Document alignment with OWASP Testing Guide
- [ ] Document alignment with PTES (Penetration Testing Execution Standard)
- [ ] Document alignment with OSSTMM
- [ ] Document alignment with NIST SP 800-115
- [ ] Document tools and versions used
- [ ] Document testing limitations and constraints
- [ ] Document false positive verification process
