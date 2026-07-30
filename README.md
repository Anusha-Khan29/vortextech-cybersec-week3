# OWASP Juice Shop Security Audit

**Internship Task – Vortex Tech**
**Author:** Anosha Nadeem

## Overview
A hands-on vulnerability assessment of OWASP Juice Shop (a deliberately vulnerable practice application), combining manual browser-based testing with an automated OWASP ZAP scan.

## What Was Built

- Local instance of OWASP Juice Shop deployed via Docker
- Manual (active) testing of key attack surfaces using browser DevTools
- Automated (passive) scan of the application using OWASP ZAP
- A structured vulnerability report covering 7 findings across multiple OWASP categories, each with evidence, impact, and remediation recommendations

## Findings Summary

- ✅ Reflected XSS (search function)
- ✅ Broken Authentication — SQL Injection login bypass
- ✅ Sensitive Data Exposure — `whoami` API endpoint
- ✅ Missing Content Security Policy header (ZAP)
- ✅ CORS misconfiguration (ZAP)
- ✅ Timestamp disclosure (ZAP)
- ✅ Informational: Modern web application detection (ZAP)

📄 [Read the full audit report](./anosha_Vortex_week3.pdf)

## How to Run This Yourself

### 1. Set up Juice Shop
```bash
docker pull bkimminich/juice-shop
docker run -d -p 3000:3000 bkimminich/juice-shop
```
Then open `http://localhost:3000` in your browser.

### 2. Manual testing
- Open browser DevTools (`F12`) → **Network** tab
- Try payloads like `<img src=x onerror=alert('XSS')>` in the search bar
- Try `' OR 1=1--` in the login email field with any password
- Inspect API responses (e.g. `/rest/user/whoami`) for over-exposed data

### 3. Automated scan with OWASP ZAP
- Install ZAP from [zaproxy.org](https://www.zaproxy.org/download/)
- Open ZAP → **Automated Scan**
- Enter `http://localhost:3000` as the target URL
- Click **Attack** and review results in the **Alerts** tab

## Disclaimer
This audit was performed only against OWASP Juice Shop, an intentionally vulnerable application built for security training. Never test real websites or systems without explicit permission.
