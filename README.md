# NETWORKWALKS-B083-WEEK-4 WEB-APPLICATION-PENETRATION-TEST

###  — Batch B083 | Week 04

## 📌 Project Overview

This project involved a practical **web application penetration test** performed against the authorized NetworkWalks training target.

The assessment covered authentication testing, SQL injection, document security, password recovery, metadata analysis, directory exposure, and sensitive information disclosure.

### 🎯 Objective

* Identify security weaknesses in the web application
* Validate vulnerabilities using controlled testing
* Assess the potential impact of discovered issues
* Document evidence and provide remediation recommendations

---

# M1 — Initial Access

## Objective

Identify the exposed areas of the Mediroza Hospital web application and obtain authorized access to the patient portal.

## Activities Performed

- Checked `robots.txt`
- Identified `/patient/`, `/staff/` and `/old/`
- Accessed the patient login page
- Tested username behavior
- Identified username enumeration
- Tested the login input for SQL injection
- Confirmed SQL injection login bypass
- Accessed the patient portal
- Identified the available patient reports

## Key Findings

| Finding | Severity |
|---|---|
| Username Enumeration | Medium |
| SQL Injection Login Bypass | Critical |
| Patient Reports Accessible After Login Bypass | High |

## Evidence
<img width="1920" height="923" alt="M1-04-login-page" src="https://github.com/user-attachments/assets/34575b53-0f02-41c0-be89-91b1dd29fb98" />
<img width="1920" height="923" alt="M1-05-sql-error" src="https://github.com/user-attachments/assets/9b5b50f1-1ea7-4658-abe9-6b9ee2d6c300" />
<img width="1920" height="923" alt="M1-06-restricted-access" src="https://github.com/user-attachments/assets/3ee9e176-050d-4f4c-b63a-95dcfa9912ca" />

# M2 — PDF Password Recovery

## Objective

Recover the passwords protecting the patient PDF reports and decrypt the third report for further analysis.

## Activities Performed

- Downloaded the available patient reports
- Generated password hashes for the protected PDFs
- Tested John the Ripper
- Investigated the hash-format issue encountered with Report 3
- Used PDF password recovery techniques
- Recovered the passwords for the reports
- Used qpdf to decrypt Report 3
- Verified the decrypted PDF

## Recovered Passwords

The recovered passwords were:

- Report 1 — `123456`
  
  <img width="1408" height="933" alt="Screenshot 2026-10-03 194314" src="https://github.com/user-attachments/assets/38b7a9f1-dbd2-4aee-a9f3-0680daf4ff5c" />

- Report 2 — `password`
  
  <img width="1253" height="926" alt="Screenshot 2026-10-03 194500" src="https://github.com/user-attachments/assets/23ee4eae-675d-47d7-8f24-5abdac30276b" />

- Report 3 — `!@#$%^&` (pdfcrack tool)

## Tools Used
- Kali Linux
- John the Ripper
- pdfcrack
- qpdf
- pdfinfo

## Evidence
<img width="1920" height="922" alt="M2-04-report3 -decrypted" src="https://github.com/user-attachments/assets/1f2bf2de-efb4-4ade-b403-9dd31643e4d8" />

# M3 — Attack/Cracking

## Objective

Perform deeper reconnaissance on the compromised application and identify additional information exposed through the application and its supporting files.

## Activities Performed

- Extracted metadata from the decrypted PDF
- Reviewed the application's `robots.txt`
- Investigated the `/old/` directory
- Identified an exposed database backup
- Reviewed staff information contained in the database
- Reviewed shareholder information
- Correlated information discovered during reconnaissance

## Key Discoveries

### PDF Metadata

The decrypted report contained metadata identifying:

- Author: Jameel Malik

### robots.txt

The application's `robots.txt` referenced:

- `/patient/`
- `/staff/`
- `/old/`

### Exposed Old Directory

The `/old/` directory exposed:

`mediroza_db_backup_2019.sql`

### Staff Information

The database backup contained confidential staff information.

The investigation identified:

- Jameel Malik
- Position: IT Systems Administrator
- Department: IT
- Email: j.malik@medirozahospital.com

### Shareholder Information

The database backup also contained shareholder records and ownership information.

## Evidence
<img width="1920" height="922" alt="M3-01-report3-metadata" src="https://github.com/user-attachments/assets/a446026f-6077-49ff-bff2-37fbb91909bd" />
<img width="1920" height="922" alt="M3-02-robots-old" src="https://github.com/user-attachments/assets/20b1800b-9f2c-4a24-8076-f540f10a8b41" />
<img width="1920" height="922" alt="M3-04-staff-data" src="https://github.com/user-attachments/assets/366a910b-b4fe-4e98-9727-c11a3212073e" />

<img width="1472" height="669" alt="Screenshot 2026-10-04 193953" src="https://github.com/user-attachments/assets/595fb061-57cd-43fe-9528-31d206fcb69a" />


## 🧪 Milestones

| Milestone | Focus |
|---|---|
| M1 | Initial Access |
| M2 | PDF Password Recovery |
| M3 | Deep Reconnaissance |
| M4 | Final Security Assessment |


## 🛠️ Tools & Technologies

| Tool                       | Purpose                            |
| -------------------------- | ---------------------------------- |
| Kali Linux                 | Security testing environment       |
| cURL                       | Web reconnaissance                 |
| Browser                    | Application testing                |
| PDF tools                  | PDF analysis and password recovery |
| John the Ripper / pdfcrack | Password recovery                  |
| qpdf                       | PDF decryption                     |
| ExifTool                   | Metadata analysis                  |
| Linux CLI                  | File and evidence analysis         |

---

## 🚨 Findings Summary

| ID   | Finding                                        | Severity    |
| ---- | ---------------------------------------------- | ----------- |
| F-01 | Username Enumeration                           | 🟠 Medium   |
| F-02 | SQL Injection Authentication Bypass            | 🔴 Critical |
| F-03 | Sensitive PDF Reports Accessible               | 🟠 High     |
| F-04 | Weak PDF Passwords                             | 🟠 High     |
| F-05 | Sensitive PDF Metadata                         | 🟠 Medium   |
| F-06 | Exposed `/old/` Directory & Database Backup    | 🔴 Critical |
| F-07 | Confidential Staff & Shareholder Data Exposure | 🔴 Critical |

---

## 📂 Evidence & Documentation

All supporting evidence, screenshots and documentation are organized according to the assessment milestones.

| Section                    | Evidence                             |
| -------------------------- | ------------------------------------ |
| M1 — Initial Access        | `M1-Initial-Access/evidence/`        |
| M2 — PDF Password Recovery | `M2-PDF-Password-Recovery/evidence/` |
| M3 — Deep Reconnaissance   | `M3-Deep-Recon/evidence/`            |
| M4 — Final Report          | `M4-Final-Report/`                   |

> 📸 Screenshots and supporting files are provided as evidence of the testing and findings.

---

## 💡 Key Takeaways

* Authentication responses can reveal valid usernames.
* Improper input handling can lead to SQL injection and authentication bypass.
* Weak document passwords can significantly reduce the protection provided by encryption.
* Metadata can unintentionally reveal useful internal information.
* Forgotten directories and exposed backups can lead to serious information disclosure.
* Security testing is not only about finding vulnerabilities, but also documenting evidence and recommending practical fixes.

---

## 🛠️ Recommendations

* Use parameterized SQL queries and prepared statements.
* Return consistent authentication error messages.
* Implement strong authentication and access controls.
* Use strong, unique passwords for protected documents.
* Remove unnecessary metadata from sensitive documents.
* Remove old backups from web-accessible directories.
* Disable directory listing where it is not required.
* Store database backups outside the public web root.

---

## 🔐 Security & Ethical Use

This project was performed in an **authorized educational cybersecurity environment** provided for NetworkWalks training.

All testing activities were limited to the permitted target and intended for learning and security assessment purposes only.

---

## 📚 Project Information

| Field           | Details                                     |
| --------------- | ------------------------------------------- |
| Program         | NetworkWalks Cybersecurity Internship       |
| Batch           | B083                                        |
| Week            | 04                                          |
| Project         | Web Application Penetration Testing         |
| Environment     | Kali Linux                                  |
| Assessment Type | Authorized Web Application Security Testing |

---

### 👤 Author

**Javeriya Tahreem**

Cybersecurity Learner | NetworkWalks Batch B083

