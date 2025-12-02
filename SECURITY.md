# Security Scanning

## Overview
This repository uses three types of security scanning:

### SAST (Static Analysis with CodeQL)
- Scans source code for vulnerabilities
- Runs on push to main branch
- Checks for:
  - Insecure configurations (e.g., debug mode enabled)
  - Code-level security weaknesses
  - Data flow and logic issues
- Artifacts: See GitHub Security tab

### SCA (Dependency Check)
- Scans Python packages for known CVEs
- Runs on push to main branch
- Checks for:
  - Outdated dependencies
  - Vulnerable library versions
  - Published CVEs
- Artifacts: sca-reports

### DAST (Live Application with ZAP)
- Tests running application for vulnerabilities
- Runs on push to main branch
- Checks for:
  - Missing security headers
  - Runtime misconfigurations
  - Weak content policies
  - Clickjacking and related risks
- Artifacts: zap-baseline-reports, zap-fullscan-reports

## Understanding Results
ZAP, CodeQL, and Dependency-Check each produce different types of findings.  
Here is how to interpret the results from your security scans:

### DAST (ZAP) Result Types
- **PASS** – The security check passed (e.g., directory browsing disabled).
- **WARN-NEW** – A new warning was found in this scan (e.g., missing security headers).
- **WARN-INPROG** – A warning that already existed in previous scans.
- **FAIL-NEW** – A new critical vulnerability was found (e.g., SQL injection).
- **FAIL-INPROG** – A previously known critical issue that still exists.
- **INFO** – Informational items that do not require immediate action.

### Common DAST Findings
ZAP often reports missing or weak security headers:
- **10020 – Missing X-Frame-Options:** Enables clickjacking.
- **10021 – Missing X-Content-Type-Options:** Allows MIME-sniffing attacks.
- **10035 – Missing HSTS:** Increases risk of HTTPS downgrade attacks.
- **10038 – Missing Content-Security-Policy:** Increases XSS risk.
- **10049 – Cacheable content:** Sensitive data could be stored.
- **10063 – Missing Permissions-Policy:** Browser features may be exposed.
- **90004 – Spectre vulnerability:** Possible side-channel information leakage.
- **10036 – Server version leakage:** Reveals server software details.

ZAP may also detect application-level issues:
- **40018 – SQL Injection**  
- **40019 – Cross-Site Scripting (XSS)**  
- **90005 – Broken authentication**  
- **90006 – CORS misconfiguration**

### How to Read Your Scan Output
Your scan results typically include:
- Number of URLs scanned
- PASS / WARN-NEW / FAIL-NEW counts
- Affected URLs (e.g., `/`, `/robots.txt`, `/sitemap.xml`)

Interpretation:
- **PASS** means the check is safe.
- **WARN-NEW** means something needs review.
- **FAIL-NEW** means immediate remediation is required.
- **INFO** means low-priority observations.

### Recommended Follow-Up Actions
For each finding:
1. Identify the risk (clickjacking, XSS, etc.)
2. Check which URL is affected.
3. Assess severity (critical → low).
4. Apply a fix (e.g., add missing headers).
5. Re-run scans to ensure the issue is resolved.

### Notes
- “Permission denied” warnings in ZAP logs are normal and do not stop the scan.
- ZAP may discover more issues over time as it learns more URLs in the application.
- INFO findings are not urgent and usually do not require fixes.


## Reporting Vulnerabilities
Please email security@example.com
