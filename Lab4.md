<img width="728" height="693" alt="Screenshot 2025-10-21 122710" src="https://github.com/user-attachments/assets/d02fbe9d-678d-4747-ab88-6641320dbe12" />

# 🔎 Authorized Scan Report — kwasuportal.com

> **Important:** This report is intended to document an **authorized** security assessment.  
> Confirm written permission from the owner/operator of `kwasuportal.com` before performing any active scanning, port/protocol probing, or vulnerability testing.

## Report Metadata
- **Target:** kwasuportal.com  
- **Scanned by:** `<Your Name / Team>`  
- **Authorization:** `<Attach or reference the written authorization>`  
- **Date (UTC):** `YYYY-MM-DD`  
- **Tools used:** `nmap`, `masscan`, `curl`, `nikto` (list versions)  
- **Command(s) used (examples):**
  - `nmap -sS -sV -O -p- --min-rate=1000 -oA kwasu_nmap_full kwasuportal.com`
  - `nmap -p 80,443 -sV --script=http-enum -oN kwasu_nmap_http kwasuportal.com`
  - `masscan -p1-65535 --rate=1000 -oL kwasu_masscan.txt kwasuportal.com`

---

## Executive Summary
_A brief one-paragraph summary of findings, risk level, and recommended next steps (e.g., "Several public services discovered; no critical exposures found" or "High-severity exposed service found — immediate patch recommended")._

---

## Host(s) and IP(s)
| Hostname | Resolved IP | Notes |
|---|---:|---|
| kwasuportal.com | `X.X.X.X` | Primary web host / CDN / load balancer |

---

## Open Ports & Services (Summary Table)
> Replace sample rows with your actual scan output.

| IP Address | Port | Protocol | Service / Banner | Version (if available) | Notes / Risk |
|------------|-----:|:--------:|------------------|------------------------|--------------|
| `X.X.X.X` | 80 | tcp | http | Apache httpd 2.4.41 | Default server signature visible — medium risk |
| `X.X.X.X` | 443 | tcp | https | nginx 1.18.0, TLS 1.2 | Certificate CN: `kwasuportal.com` |
| `X.X.X.X` | 22 | tcp | ssh | OpenSSH 8.2p1 | Ensure strong auth; no root login |
| `X.X.X.X` | 3306 | tcp | mysql | MySQL 5.7.32 | Database port exposed to internet — high risk |

---

## Detailed Service Notes & Evidence
### `X.X.X.X:80 (HTTP)`
- **Banner / Fingerprint:** `Apache/2.4.41 (Ubuntu)`  
- **Observed endpoints:** `/`, `/admin`, `/login`  
- **Potential issues:** Directory listing on `/uploads/` (if present), missing security headers (HSTS, X-Frame-Options)  
- **Suggested remediation:** Harden HTTP headers, remove directory listing, apply latest patches.

### `X.X.X.X:443 (HTTPS)`
- **TLS:** `TLS 1.2` (recommended: enable TLS 1.3, disable TLS 1.0/1.1)  
- **Cert:** Issuer: `Let’s Encrypt` — expires `YYYY-MM-DD`  
- **Suggested remediation:** Enforce modern TLS config, enable HSTS.

*(Add similar subsections for each discovered service)*

---

## Risk Rating (Suggested)
- **High:** Services that expose sensitive data (databases, unsecured admin panels) to the internet.  
- **Medium:** Public services with outdated versions or missing security headers.  
- **Low:** Standard web ports with hardened configurations.

---

## Action Items & Recommendations
1. Close or firewall database ports (e.g., 3306) from public internet; use VPN or private network access.  
2. Apply OS and application patches for reported versions.  
3. Harden TLS configuration, enable HSTS, check certif
