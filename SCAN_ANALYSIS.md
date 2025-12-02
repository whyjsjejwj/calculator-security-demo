# Security Scan Analysis - [2/12/2025]

## DAST Results (ZAP Baseline)
- Total URLs scanned: 5
- PASS: 0
- WARN-NEW: 7 warnings
- FAIL-NEW: 0 failures

### Warning Summary
| Code  | Issue                                                                        | Risk |
|-------|------------------------------------------------------------------------------|------|
| 10038 | Content Security Policy (CSP) Header Not Set                                 | Medium |
| 10106 | HTTP Only Site                                                               | Medium |
| 10020 | Missing Anti-clickjacking Header                                             | Medium |
| 90004 | Insufficient Site Isolation Against Spectre Vulnerability                    | Low |
| 10063 | Permissions Policy Header Not Set                                            | Low |
| 10036 | Server Leaks Version Information via "Server" HTTP Response Header Field     | Low |
| 10021 | X-Content-Type-Options Header Missing                                        | Low |


## SCA Results (Dependency Check)
- High severity: 0
- Medium severity: 0
- Low severity: 0

### Vulnerable Packages
- **None Detected**

## SAST Results (CodeQL)
- Total issues: 1
- By type: **High Severity** - **"Flask app is run in debug mode"**        

## Recommendations
- Firstly, work on the high severity vulnerability, which is for the Flask app to not run in debug mode. After the high severity vulnerability is resolved, then focus ont he medium severity vulnerabilities before working on the low severity ones.