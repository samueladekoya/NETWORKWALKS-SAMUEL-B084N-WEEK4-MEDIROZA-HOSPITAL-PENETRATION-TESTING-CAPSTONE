# NETWORKWALKS-SAMUEL-B084N-WEEK4-MEDIROZA-HOSPITAL-PENETRATION-TESTING-CAPSTONE
A hands-on web application penetration testing capstone documenting reconnaissance, SQL injection, authentication bypass, PDF password recovery, database exposure, and security remediation.




# PENETRATION TESTING REPORT
## Mediroza General Hospital

| Project Detail | Information |
|---|---|
| Prepared By | [Samuel Ayomide Adekoya |
| Organization | Networkwalks |
| Batch | B084 |
| Project | Week 4 – Penetration Testing |
| Client | Mediroza General Hospital |
| Target | https://medirozahospital.com |
| Assessment Type | Black-Box Penetration Test |
| Duration | 5 Days |
| Date | 25-11-2026 |

---

# TABLE OF CONTENTS

1. [Executive Summary](#1-executive-summary)
2. [Scope and Methodology](#2-scope-and-methodology)
3. [Tools Used](#3-tools-used)
4. [Milestone 1 – Initial Access](#4-milestone-1--initial-access)
5. [Milestone 2 – Data Extraction](#5-milestone-2--data-extraction)
6. [Milestone 3 – Attack (Cracking)](#6-milestone-3--attack-cracking)
7. [Findings and Risk Ratings](#7-findings-and-risk-ratings)
8. [Recommendations and Remediation](#8-recommendations-and-remediation)
9. [Conclusion](#9-conclusion)
10. [Appendices](#10-appendices)

---

# 1. EXECUTIVE SUMMARY

A black-box penetration test was conducted against Mediroza General Hospital's web infrastructure as part of the Networkwalks Week 4 Penetration Testing Project.

The primary objective was to identify security vulnerabilities, demonstrate their potential impact within the authorized testing scope, and document the findings in a professional penetration testing report.

The assessment involved reconnaissance, identification of exposed entry points, analysis of authentication mechanisms, vulnerability scanning, controlled exploitation, recovery of encrypted PDF documents, and investigation of exposed information.

The following security issues were identified and investigated:

- SQL injection vulnerability affecting the patient portal authentication mechanism.
- Successful authentication bypass and access to a restricted patient portal.
- Retrieval of three encrypted PDF laboratory reports.
- Successful password recovery for all three PDF documents.
- Discovery of a publicly accessible directory containing a database backup.
- Exposure of confidential hospital employee salary and shareholder information.

The findings demonstrate how weaknesses in application security, access controls, and server configuration can expose sensitive organizational information.

**Overall Assessment:** High to Critical risk, subject to final validation of individual findings and their impact.

This report provides the technical findings, supporting evidence, risk assessments, and recommendations for improving the security posture of the hospital's web infrastructure.

---

# 2. SCOPE AND METHODOLOGY

## 2.1 Assessment Scope

The assessment was conducted against the following authorized target:

| Item | Description |
|---|---|
| Client | Mediroza General Hospital |
| Target Domain | medirozahospital.com |
| Target URL | https://medirozahospital.com |
| Assessment Type | Black-Box Penetration Test |
| Testing Approach | Reconnaissance, vulnerability assessment, and controlled exploitation |
| Authorization | Written authorization granted through Networkwalks |

Testing was restricted to the authorized target domain.

## 2.2 Rules of Engagement

The following restrictions were observed:

- Testing was limited to the authorized target domain.
- No social engineering activities were conducted.
- No denial-of-service testing was performed.
- No testing was conducted outside the agreed scope.
- Activities were performed for authorized educational security assessment purposes.

## 2.3 Testing Methodology

The assessment followed a structured penetration testing methodology.

### Phase 1: Reconnaissance

Information about the target domain, DNS configuration, web technologies, and publicly accessible resources was investigated.

### Phase 2: Enumeration and Vulnerability Assessment

Exposed entry points and application behavior were examined. OWASP ZAP was used to identify potential web application vulnerabilities.

### Phase 3: Initial Access

The patient portal authentication mechanism was investigated. A SQL injection vulnerability was identified and successfully demonstrated.

### Phase 4: Data Extraction

Three encrypted PDF laboratory reports were retrieved from the restricted area of the website.

### Phase 5: Password Recovery and Data Analysis

The encryption of the retrieved documents was examined, and appropriate password-recovery techniques were used to access all three documents.

### Phase 6: Further Information Disclosure Investigation

Additional exposed resources were investigated. A publicly accessible directory containing a database backup was discovered, leading to the identification of confidential hospital information.

### Phase 7: Reporting

The findings were documented, assessed for risk, and accompanied by remediation recommendations.

---

# 3. TOOLS USED

The following tools were used during the assessment.

| Tool | Purpose |
|---|---|
| WHOIS | Retrieves domain registration and publicly available ownership information. |
| WhatWeb | Identifies website technologies, frameworks, and server-related information. |
| Nslookup | Performs DNS queries and investigates domain name resolution. |
| cURL | Retrieves HTTP responses, inspects response headers, and accesses publicly available web resources. |
| WAFW00F | Detects and identifies possible Web Application Firewalls. |
| DNSRecon | Performs DNS reconnaissance and enumerates DNS records. |
| OWASP ZAP | Performs web application security testing and identifies potential vulnerabilities, including SQL injection. |

## 3.1 WHOIS

WHOIS was used during reconnaissance to retrieve publicly available domain registration information.

**Objectives:**

- Examine domain registration details.
- Identify available registrar information.
- Gather publicly available information associated with the target domain.



![WHOIS reconnaissance](Screenshot%20().png)

---

## 3.2 WhatWeb

WhatWeb was used to fingerprint the target website and identify technologies used by the web application.

**Objectives:**

- Identify web technologies and frameworks.
- Examine server-related information.
- Gather information that could assist subsequent testing.



![WhatWeb results](Screenshot%20().png)

---

## 3.3 Nslookup

Nslookup was used to investigate DNS resolution for the target domain.

**Objectives:**

- Resolve the target domain.
- Examine available DNS information.
- Identify relevant DNS records.



![Nslookup results](Screenshot%20().png)

---

## 3.4 cURL

cURL was used to retrieve HTTP responses and inspect server behavior.

One of the commands used during reconnaissance was:

```bash
curl -I https://medirozahospital.com/robots.txt
```

This allowed inspection of the HTTP response headers.

The publicly accessible `robots.txt` file was also examined for information about website paths.

The file contained the following entries:

```text
User-agent: *
Disallow: /patient/
Disallow: /staff/
Disallow: /old/

Sitemap: https://medirozahospital.com/sitemap.xml
```

These entries provided useful information about website directories and resources that warranted further investigation.



![cURL HTTP response](Screenshot%20().png)

![Robots.txt contents](Screenshot%20().png)

---

## 3.5 WAFW00F

WAFW00F was used to investigate whether the target website was protected by a Web Application Firewall.

**Objectives:**

- Determine whether a WAF could be identified.
- Identify the WAF product where possible.
- Understand the available web application protection mechanisms.


![WAFW00F results](Screenshot%20().png)

---

## 3.6 DNSRecon

DNSRecon was used to perform additional DNS reconnaissance and investigate available DNS records.

**Objectives:**

- Enumerate available DNS records.
- Gather information about the target's DNS configuration.
- Identify relevant DNS information for the assessment.



![DNSRecon results](Screenshot%20().png)

---

## 3.7 OWASP ZAP

OWASP ZAP was used to perform web application vulnerability scanning.

**Objectives:**

- Examine the security of the target web application.
- Identify potential input-handling vulnerabilities.
- Investigate authentication-related weaknesses.
- Review vulnerability alerts generated during the assessment.

**Results:**

OWASP ZAP identified a SQL injection vulnerability during the assessment. The finding was investigated further, and a successful authentication bypass was demonstrated against the patient portal.



![OWASP ZAP vulnerability scan](Screenshot%20().png)


---

# 4. MILESTONE 1 – INITIAL ACCESS

## 4.1 Objective

The objective of Milestone 1 was to attack the website within the authorized scope, identify weaknesses in its authentication mechanisms, gain access to a restricted area, and retrieve three confidential PDF laboratory reports.

## 4.2 Reconnaissance

Initial reconnaissance was conducted using WHOIS, WhatWeb, Nslookup, cURL, WAFW00F, and DNSRecon.

The information gathered helped identify publicly exposed infrastructure and potential entry points.


![Initial reconnaissance](Screenshot%20().png)


## 4.3 Identification of Exposed Entry Points

The website's publicly accessible resources were examined, including its `robots.txt` file.

The file referenced the following directories:

- `/patient/`
- `/staff/`
- `/old/`

These paths provided useful leads for further investigation.



![Exposed website paths](Screenshot%20().png)


## 4.4 Patient Portal Authentication Analysis

The patient portal was identified as an important application entry point.

Its login functionality was examined to determine how the application handled user-supplied authentication input.

During vulnerability testing, OWASP ZAP identified a SQL injection weakness affecting the authentication mechanism.



![Patient portal login page](Screenshot%20().png)



## 4.5 SQL Injection and Initial Access

The SQL injection vulnerability was investigated further.

A crafted username input was used to demonstrate that the authentication mechanism could be bypassed.

The successful test resulted in access to the restricted patient portal.

This demonstrated that the application did not adequately protect its authentication process against SQL injection.



![SQL injection authentication bypass](Screenshot%20().png)

![Successful patient portal access](Screenshot%20().png)


## 4.6 Retrieval of the Three PDF Reports

After gaining access to the patient portal, three encrypted PDF laboratory reports were identified and retrieved.

These files were preserved for further investigation during Milestone 2.



![Retrieved PDF report](Screenshot%20().png)


**Milestone 1 Deliverable:** Successful access to the restricted portal and retrieval of all three PDF laboratory reports.

---

# 5. MILESTONE 2 – DATA EXTRACTION

## 5.1 Objective

The objective of Milestone 2 was to investigate and recover the encryption passwords protecting all three PDF reports.

The project required each document to be examined independently because the same password-recovery approach was not guaranteed to work for every file.

## 5.2 Encryption Analysis

The three retrieved PDF documents were examined to determine their encryption properties.

The analysis established that the documents were password-protected.

The encryption characteristics were investigated using available PDF inspection utilities.


![PDF encryption analysis](Screenshot%20().png)

## 5.3 Password Recovery

Password-recovery tools and wordlists were used to investigate the encrypted documents.

The first two documents were successfully recovered using the initial password-recovery approach.

The third document required a different approach because its password format differed from the first two and included special characters.

An alternative password-recovery approach was subsequently used, resulting in successful recovery of the third document's password.


![First PDF password recovery](Screenshot%20().png)

![Second PDF password recovery](Screenshot%20().png)

![Third PDF password recovery](Screenshot%20().png)


## 5.4 Verification of Recovered Documents

After recovering the passwords, each document was opened to confirm that its contents were accessible.

All three PDF reports were successfully recovered and opened.


![First recovered PDF](Screenshot%20().png)

![Second recovered PDF](Screenshot%20().png)

![Third recovered PDF](Screenshot%20().png)

**Milestone 2 Deliverable:** Successful recovery and verification of all three encrypted PDF reports.

---

# 6. MILESTONE 3 – ATTACK (CRACKING)

## 6.1 Objective

The objective of Milestone 3 was to investigate information obtained during the previous milestones and identify critical data exposure affecting the hospital.

The project specifically required the discovery of:

1. Salaries of all hospital employees.
2. Shareholder details of the hospital.

## 6.2 Analysis of Retrieved Information

The previously retrieved PDF documents and their associated information were examined for additional clues.

The investigation extended beyond the visible contents of the reports to identify other potentially exposed resources.

The project brief indicated that one of the findings would lead to a further critical exposure on the server.

## 6.3 Discovery of the Exposed `/old/` Directory

Further investigation of the website revealed that the following directory was publicly accessible:

https://medirozahospital.com/old/

The directory exposed a database backup file named:

```text
mediroza_db_backup_2019.sql
```

The discovery indicated that a database backup had been placed in a publicly accessible web directory.


![Exposed database backup filename](Screenshot%20().png)


## 6.4 Discovery of Confidential Hospital Information

The exposed database backup was examined as part of the authorized assessment.

The investigation revealed information that answered the two Milestone 3 tasks:

- Hospital employee salary information.
- Hospital shareholder details.

The exposure demonstrated the potential impact of leaving sensitive database backups accessible through a public web directory.


![Employee salary information exposure](Screenshot%20().png)

![Shareholder information exposure](Screenshot%20().png)

**Milestone 3 Deliverable:** Identification and documentation of the exposed employee salary and shareholder information.

---

# 7. FINDINGS AND RISK RATINGS

The following findings summarize the security weaknesses identified during the assessment.

Risk ratings are preliminary and should be finalized against the demonstrated impact, affected data, and exploitability.

| ID | Finding | Preliminary Severity |
|---|---|---|
| F-01 | SQL Injection in Patient Portal Authentication | High |
| F-02 | Unauthorized Access to Restricted Patient Portal | High |
| F-03 | Exposure of Confidential PDF Laboratory Reports | High |
| F-04 | Publicly Accessible Database Backup | Critical |
| F-05 | Exposure of Employee Salary and Shareholder Information | Critical |

## F-01: SQL Injection in Patient Portal Authentication

**Severity:** High  
**Affected Component:** Patient Portal Login  
**Vulnerability Type:** SQL Injection  
**Evidence:** OWASP ZAP results and successful authentication bypass.

### Description

A SQL injection vulnerability was identified in the patient portal authentication mechanism.

The application did not adequately handle user-supplied input before processing authentication requests.

A crafted username input successfully demonstrated that the authentication mechanism could be bypassed.

### Impact

An attacker could potentially bypass authentication controls and gain unauthorized access to restricted application functionality.

Depending on the database privileges and application architecture, SQL injection may also expose additional database information.

### Recommendation

- Use parameterized SQL queries and prepared statements.
- Avoid constructing SQL queries through direct string concatenation.
- Validate and safely handle all user-supplied input.
- Apply least-privilege permissions to database accounts.
- Conduct regular secure code reviews and penetration tests.

---

## F-02: Unauthorized Access to Restricted Patient Portal

**Severity:** High  
**Affected Component:** Patient Portal  
**Vulnerability Type:** Authentication Bypass  
**Evidence:** Successful access following SQL injection testing.

### Description

The patient portal's authentication mechanism could be bypassed through the identified SQL injection weakness.

This allowed access to functionality intended for authenticated users.

### Impact

Unauthorized individuals could potentially access restricted portal functionality and information.

### Recommendation

- Fix the underlying SQL injection vulnerability.
- Enforce authentication checks on every protected endpoint.
- Implement secure session management.
- Regenerate session identifiers after authentication.
- Monitor authentication failures and suspicious login activity.

---

## F-03: Exposure of Confidential PDF Laboratory Reports

**Severity:** High  
**Affected Component:** Patient Portal / PDF Laboratory Reports  
**Vulnerability Type:** Unauthorized Access to Confidential Documents  
**Evidence:** Retrieval of three encrypted PDF reports.

### Description

Three confidential PDF laboratory reports were retrieved after access to the restricted patient portal was obtained.

Although the documents were password-protected, the successful retrieval demonstrated that the application did not sufficiently protect access to the underlying documents.

### Impact

Unauthorized access to laboratory reports could expose confidential information and potentially compromise patient privacy.

### Recommendation

- Enforce server-side authorization checks before serving documents.
- Store confidential reports outside publicly accessible directories.
- Use secure, short-lived download links where appropriate.
- Apply strong encryption and password-management practices.
- Log and monitor access to confidential documents.

---

## F-04: Publicly Accessible Database Backup

**Severity:** Critical  
**Affected Component:** `/old/` Directory  
**Vulnerability Type:** Sensitive File Exposure / Security Misconfiguration  
**Evidence:** Public directory listing and discovery of `mediroza_db_backup_2019.sql`.

### Description

A publicly accessible directory was discovered at:

https://medirozahospital.com/old/

The directory exposed a database backup file named `mediroza_db_backup_2019.sql`.

The availability of a database backup through a public web directory created an information disclosure risk.

### Impact

An attacker could potentially retrieve the backup and inspect its contents for sensitive information.

Depending on the contents, this could expose employee information, shareholder information, application data, or other confidential records.

### Recommendation

- Remove database backups from publicly accessible directories.
- Store backups outside the web root.
- Disable directory listing on the web server.
- Apply appropriate access controls to backup storage.
- Encrypt backups at rest.
- Review the server for other accidentally exposed files.
- Rotate credentials or secrets if they may have been exposed.

---

## F-05: Exposure of Employee Salary and Shareholder Information

**Severity:** Critical  
**Affected Component:** Exposed Database Backup  
**Vulnerability Type:** Sensitive Information Disclosure  
**Evidence:** Identification of employee salaries and shareholder details during Milestone 3.

### Description

Investigation of the exposed database backup revealed confidential information relating to hospital employees and shareholders.

The information included employee salary details and shareholder information, both of which should have been protected from public access.

### Impact

The exposure could result in:

- Compromise of employee privacy.
- Unauthorized disclosure of financial information.
- Exposure of confidential shareholder information.
- Potential fraud, impersonation, or targeted social engineering.
- Reputational and legal consequences for the organization.

### Recommendation

- Restrict database backup access to authorized personnel.
- Remove sensitive backups from the public web directory.
- Apply encryption to stored database backups.
- Review database access privileges.
- Establish a secure backup retention and disposal policy.
- Investigate whether exposed credentials or other secrets require rotation.
- Conduct an assessment to determine whether other sensitive information was exposed.

---

# 8. RECOMMENDATIONS AND REMEDIATION

Based on the findings, the following security improvements are recommended.

## 8.1 Secure Database Queries

The patient portal should use parameterized queries and prepared statements to prevent SQL injection.

All user-supplied input must be handled securely before being processed by database queries.

## 8.2 Strengthen Authentication

The hospital should implement secure authentication controls, including:

- Strong password policies.
- Secure session management.
- Server-side authentication checks.
- Multi-factor authentication where appropriate.
- Monitoring of suspicious login activity.

## 8.3 Enforce Access Controls

Access to patient records, laboratory reports, and other confidential documents must be restricted to authorized users.

Authorization checks should be performed server-side for every protected resource.

## 8.4 Protect Database Backups

Database backups must never be stored in publicly accessible web directories.

They should be stored in protected locations with appropriate permissions and encryption.

## 8.5 Disable Directory Listing

Directory listing should be disabled on the web server to prevent visitors from browsing directory contents and discovering sensitive files.

## 8.6 Protect Confidential Information

Employee salary details, shareholder information, and patient-related records must be protected through appropriate access controls, encryption, and secure data-handling procedures.

## 8.7 Conduct Regular Security Assessments

The organization should conduct periodic vulnerability assessments and penetration tests to identify weaknesses before they can be exploited.

---

# 9. CONCLUSION

The Networkwalks Week 4 penetration testing assessment of Mediroza General Hospital demonstrated several security weaknesses affecting the target web application and its publicly accessible resources.

The assessment successfully identified a SQL injection vulnerability in the patient portal authentication mechanism and demonstrated the resulting unauthorized access.

Three encrypted PDF laboratory reports were retrieved, and their passwords were successfully recovered.

Further investigation revealed a publicly accessible directory containing a database backup. Examination of the exposed information led to the discovery of confidential employee salary and shareholder details.

These findings demonstrate the importance of secure application development, proper authentication and authorization, safe backup storage, and effective server configuration.

The most significant issue identified was the exposure of a database backup containing sensitive organizational information.

Implementing the recommendations in this report would significantly improve the security posture of the hospital's web infrastructure and reduce the likelihood of similar information disclosure incidents.

**Assessment Status:** All four project milestones completed.

---

# 10. APPENDICES


## Appendix A – Assessment Limitations

- The assessment was restricted to the authorized target domain.
- No denial-of-service testing was performed.
- No social engineering activities were conducted.
- Findings were based on the activities and evidence collected during the five-day assessment.
- Risk ratings are preliminary and should be reviewed against the client's actual environment.
- Sensitive information should be redacted before this report or its supporting screenshots are made publicly available.

## Appendix B – Declaration

This penetration testing report documents activities conducted as part of the Networkwalks Week 4 educational penetration testing project.

The assessment was performed against the authorized target with written permission granted through Networkwalks.

All testing activities were restricted to the agreed scope and conducted for educational and security assessment purposes.

**Prepared By:** [Samuel Ayomide Adekoya]  
**Organization:** Networkwalks  
**Project:** Mediroza General Hospital – Week 4 Penetration Testing  
**Date:** [25-11-2026]
