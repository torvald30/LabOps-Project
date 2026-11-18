# CYBERSECURITY PROJECT REPORT

## COMPROMISE OF A SMALL TEAM

### Project LabOps

**Course:** Cybersecurity Tutorials

**Project Type:** Practical Security Assessment

**Operating System:** Kali Linux

**Testing Environment:** Local LabOps Virtual Environment

**Submission Date:** 20 November 2026

**Student Name:** Alameen Shahul Hameed

**Instructor:** Robi Pritrˇznik

# Project LabOps – Cybersecurity Security Assessment Report

**Project:** Compromise of a Small Team  
**Environment:** Local LabOps virtual environment  
**Operating System:** Kali Linux  

## 1. Introduction

This project examines common cybersecurity weaknesses that could affect a small team called LabOps. The purpose is to understand how security problems can occur and how they can be identified, assessed and prevented.

The project focuses on five areas:

1. Phishing awareness.
2. SSH service security.
3. GPG public-key substitution.
4. Database secret protection.
5. Installation script integrity.

All demonstrations were performed using a controlled local environment and fictional LabOps data. No external systems or real user accounts were targeted.

## 2. Scenario and Important Assets

LabOps is a fictional small team that provides an enrollment helper service. The team uses several digital assets that need protection.

| Asset | Purpose | Security concern |
|---|---|---|
| Helpdesk mailbox | Team communication | Phishing and account compromise |
| SSH account | Remote administration | Unauthorized access |
| GPG release key | Verify release files | Public-key substitution |
| install.sh | Installation script | Unauthorized modification |
| secrets.env | Stores database credentials | Exposure of confidential information |
| Student information | Enrollment-related data | Privacy and unauthorized access |

These assets require confidentiality, integrity and availability.

**Confidentiality** means information should only be accessible to authorized people.

**Integrity** means information and files should not be changed without authorization.

**Availability** means systems and information should remain accessible when needed.

## 3. Methodology and Lab Setup

### 3.1 Lab Environment

The project was completed in Kali Linux using a local LabOps environment.

The environment included:

- Docker and Docker Compose for running the lab services.
- A local SSH service accessible through port 2222.
- Nmap for identifying the local SSH service.
- GPG for public-key and file-encryption demonstrations.
- SHA-256 checksums for checking file integrity.
- A local demonstration directory for project files and evidence.

### 3.2 Testing Method

The project followed a controlled testing approach:

1. Start and check the local LabOps environment.
2. Create a safe phishing-awareness demonstration.
3. Identify the local SSH service.
4. Generate and compare GPG public-key fingerprints.
5. Demonstrate database secret encryption.
6. Check installation script integrity.
7. Save screenshots and text files as evidence.

### 3.3 Testing Limitations

All tests were limited to the local LabOps environment. The phishing page was a static awareness demonstration and did not collect credentials.

The SSH service was identified using Nmap. A weak-password test was not performed, so password weakness was not confirmed.

Only fictional demonstration data was used. No real student information or external systems were involved.

## 4. Security Tests and Results

### 4.1 Test 1 – Phishing Awareness

**Objective:** Understand how a fake login page can be used to deceive users.

**Method:** A static login-page demonstration was created locally to identify common phishing warning signs.

**Result:** The demonstration showed how suspicious website addresses, missing HTTPS, unclear website identity, unusual language and unexpected login requests can indicate phishing.

**What LabOps should notice:** Employees should check website addresses and unexpected login requests before entering account details.

**Security meaning:** Phishing can lead to stolen account credentials and unauthorized access.

**Recommendations:** Provide security awareness training, enable multi-factor authentication and encourage users to report suspicious messages.

**Evidence:** `01-phishing.png`, `01-phishing-analysis.txt`

### 4.2 Test 2 – SSH Service Security

**Objective:** Identify the SSH service running in the local LabOps environment.

**Method:** Nmap was used to scan localhost on port 2222.

**Result:** The scan identified port 2222 as open and running OpenSSH 9.6p1.

**What LabOps should notice:** An accessible SSH service should be limited to authorized administrators.

**Security meaning:** An exposed SSH service can increase the risk of unauthorized access if authentication or access controls are weak. The password strength was not tested in this project.

**Recommendations:** Use strong unique passwords, SSH key authentication, disable unused accounts and monitor login activity.

**Evidence:** `02-nmap.txt`, `02-nmap-analysis.txt`, `02-ssh-port.png`, `03-ssh-analysis.txt`

### 4.3 Test 3 – GPG Public-Key Substitution

**Objective:** Demonstrate why a public-key fingerprint must be verified.

**Method:** Two separate GPG keys were created using the same displayed identity. Their fingerprints were compared. A demonstration public key was imported into an empty keyring, and a test note was encrypted and decrypted using the corresponding local demonstration key.

**Result:** Both keys displayed the same identity but had different fingerprints. The encrypted test note was successfully decrypted using the key that matched the imported public key.

**What LabOps should notice:** A displayed name or email address alone does not prove that a public key belongs to the intended person.

**Security meaning:** Accepting an unverified replacement public key could allow information to be encrypted for the wrong key holder.

**Recommendations:** Verify fingerprints through a separate trusted communication channel before accepting a public key.

**Evidence:** `04-fingerprints.png`, `04-fingerprints.txt`, `04-imported-key.png`, `04-key-substitution.png`, `04-key-substitution.txt`, `04-signature-valid.png`, `04-signature-valid.txt`

### 4.4 Test 4 – Database Secret Protection

**Objective:** Examine how a database secret can be protected.

**Method:** A fictional `secrets.env` file was created with restricted file permissions. GPG was used to encrypt it. Decryption was checked without displaying the secret content.

**Result:** The original file had permission mode 600. The encrypted file was created successfully, and the decryption verification completed without an error.

**What LabOps should notice:** Sensitive credentials should not be stored or shared in an unprotected form.

**Security meaning:** Exposed credentials can allow unauthorized access. Removing a secret from the current file does not necessarily remove it from previous Git history.

**Recommendations:** Use a secrets manager, restrict file permissions, encrypt sensitive data and rotate credentials if exposure is suspected.

**Evidence:** `05-secrets-encryption.png`, `05-secrets-encryption.txt`, `05-secrets-decryption.png`, `05-secrets-decryption.txt`

### 4.5 Test 5 – Installation Script Integrity

**Objective:** Check whether unauthorized changes to an installation script can be detected.

**Method:** The original SHA-256 checksum was checked. A harmless comment was then added to the local demonstration script, and the checksum was checked again. A separate modified checksum file was also tested against its GPG signature.

**Result:** The original checksum matched. After the script was changed, the checksum check failed. The modified checksum file also produced a GPG bad-signature result.

**What LabOps should notice:** Even a small file modification changes its checksum. A valid digital signature helps verify that the signed checksum file has not been altered.

**Security meaning:** Integrity checks can help identify unauthorized changes to software release files.

**Recommendations:** Sign release checksums, verify signatures using a trusted public key and check file hashes before installation.

**Evidence:** `06-checksum-original.png`, `06-checksum-tampered.png`, `06-checksum-tampered.txt`, `06-signature-tampered.png`, `06-signature-tampered.txt`

## 5. Risk Assessment

The following table evaluates the five security weaknesses identified or considered during the project.

| Security issue | Likelihood | Impact | Overall risk |
|---|---|---|---|
| Phishing attacks | Medium | High | High |
| SSH unauthorized access | Medium | High | High |
| GPG public-key substitution | Medium | High | High |
| Database secret exposure | Medium | High | High |
| Installation script tampering | Medium | High | High |

### 5.1 Risk Explanation

**1. Phishing attacks – High risk**

Phishing can trick employees into revealing account information. This may allow unauthorized access to team accounts. The local demonstration showed warning signs but did not test real users.

**2. SSH unauthorized access – High risk**

The local SSH service was accessible on port 2222. Weak password use was not verified, but weak authentication could increase the risk of unauthorized access.

**3. GPG public-key substitution – High risk**

The demonstration showed that two different keys can display the same identity. If fingerprints are not checked, sensitive information could be encrypted for an unintended key holder.

**4. Database secret exposure – High risk**

Database credentials are sensitive information. If they are exposed through files, repositories or backups, unauthorized users may gain access. No external exposure was confirmed during this project.

**5. Installation script tampering – High risk**

An altered installation script could affect the security of a system. The checksum demonstration successfully detected a change to the script.

### 5.2 Risk Assessment Limitation

These ratings are qualitative estimates for the fictional LabOps scenario. They are not based on a full production security audit. Some weaknesses, especially SSH password weakness and actual credential exposure, were not directly verified.

## 6. Security Improvement Plan

LabOps should introduce the following security controls to reduce the risks identified during testing.

### 6.1 Improve Phishing Protection

- Provide regular phishing-awareness training.
- Enable multi-factor authentication for important accounts.
- Teach employees to identify suspicious links and messages.
- Create a process for reporting suspicious emails.

**Related test:** Test 1 – Phishing Awareness.

### 6.2 Secure SSH Access

- Use strong and unique authentication credentials.
- Prefer SSH key authentication where appropriate.
- Disable unused accounts.
- Restrict SSH access to authorized administrators.
- Monitor SSH login activity.

**Related test:** Test 2 – SSH Service Security.

### 6.3 Protect GPG Public Keys

- Verify public-key fingerprints through a separate trusted channel.
- Maintain an approved list of trusted release keys.
- Review key changes before accepting replacement keys.
- Protect private keys with suitable access controls.

**Related test:** Test 3 – GPG Public-Key Substitution.

### 6.4 Protect Database Secrets

- Store sensitive credentials in a secrets manager.
- Avoid committing passwords and secrets to Git repositories.
- Restrict access to sensitive configuration files.
- Encrypt sensitive files when storing or transferring them.
- Rotate credentials if exposure is suspected.

**Related test:** Test 4 – Database Secret Protection.

### 6.5 Protect Installation Files

- Generate SHA-256 checksums for release files.
- Digitally sign checksum files using a trusted release key.
- Verify signatures and checksums before installation.
- Restrict permission to modify release files.
- Review release changes before publishing.

**Related test:** Test 5 – Installation Script Integrity.

### 6.6 Additional Security Controls

LabOps should also:

- Separate vendor-facing systems from internal systems.
- Give employees and vendors only the permissions they need.
- Keep operating systems and applications updated.
- Maintain backups and test recovery procedures.
- Review security alerts and investigate unusual activity.

### 6.7 Implementation Priority

The first priority should be protecting accounts and sensitive credentials. LabOps should then establish trusted key verification and signed software releases. Regular monitoring

## 7. Legal and Ethical Considerations

### 7.1 GDPR and Personal Data

The General Data Protection Regulation (GDPR) protects personal information belonging to individuals in its scope.

If LabOps processes personal information belonging to people protected by GDPR, it should:

- Have a lawful basis for processing personal information.
- Collect only the information needed for its purpose.
- Use personal information only for its intended purpose.
- Restrict access to authorized people.
- Protect information against unauthorized access or disclosure.
- Keep information only for the required period.

If a personal data breach occurs, the organization must assess the incident and follow the applicable notification requirements. Under GDPR, a supervisory authority generally must be notified within 72 hours of becoming aware of a reportable breach. Affected individuals must also be informed when the breach is likely to result in a high risk to their rights and freedoms.

### 7.2 NIS2 Directive

The NIS2 Directive establishes cybersecurity requirements for certain important and essential entities in the European Union.

Whether an organization is covered depends on factors such as its sector, activities, size and applicable national rules.

LabOps is a fictional small team used for this educational project. There is not enough information to conclude that it falls within NIS2 scope. Its actual applicability would need to be checked against the relevant national legislation and organizational circumstances.

### 7.3 Ethical Testing Rules

Cybersecurity testing must be performed responsibly.

The following rules were followed in this project:

- Testing was limited to the authorized local LabOps environment.
- Only fictional demonstration information was used.
- The phishing page was a static awareness demonstration and did not collect passwords.
- No external systems or real user accounts were targeted.
- Evidence was collected for educational reporting

## 8. Conclusion

This project examined five cybersecurity areas that could affect a small team: phishing, SSH security, GPG public-key verification, database secret protection and installation script integrity.

The local demonstrations showed how suspicious login pages can create phishing risks, how an accessible SSH service should be protected, and why public-key fingerprints must be verified. The encryption demonstration showed how sensitive files can be protected, while the checksum and digital-signature tests demonstrated how file modifications can be detected.

The project also highlighted the importance of access control, employee awareness, secure credential storage, trusted software releases and responsible data handling.

Some checks were limited to observations and demonstrations. In particular, SSH password strength and actual external exposure of database credentials were not verified. These limitations have been clearly stated in the report.

Overall, LabOps should apply the recommended security controls and review them regularly to reduce cybersecurity risks and protect its information.

---

**Project:** Compromise of a Small Team – LabOps  
**Environment:** Authorized local educational lab
