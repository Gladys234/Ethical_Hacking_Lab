<img width="762" height="317" alt="Screenshot 2025-10-24 100915" src="https://github.com/user-attachments/assets/818fc4c6-f881-4139-9276-bc5fd21786e4" />
<img width="768" height="667" alt="Screenshot 2025-10-24 100903" src="https://github.com/user-attachments/assets/ef05a99e-6aa3-4954-bd66-8694f1c12ec4" />
<img width="1003" height="633" alt="Screenshot 2025-10-24 100837" src="https://github.com/user-attachments/assets/b27a70be-5b46-4a9b-9094-8045b7bc9176" />

# 🔎 Scan Summary — Hosts, Open Ports & Services

> **Source:** Provided scan output (author: you). Replace or update notes after verification.

| Port | State     | Service   | Version / Banner | Notes / Risk |
|-----:|:---------:|:---------:|:-----------------|:-------------|
| 22/tcp | open    | ssh       | OpenSSH 8.7 (protocol 2.0) | ✅ Common remote admin service. Recommend enforcing key-based auth, disabling root login, & rate-limiting. |
| 25/tcp | filtered| smtp      | — | Filtered — limited visibility. Check MX records and relay policy. |
| 53/tcp | open    | domain    | PowerDNS Authoritative Server 4.9.5 | ⚠️ Authoritative DNS exposed; verify zone transfer (AXFR) restrictions and DNSSEC where applicable. |
| 80/tcp | open    | http      | nginx | ✔️ Web server detected. Verify up-to-date packages and secure headers (HSTS, CSP, X-Frame-Options). |
| 81/tcp | open    | http      | Apache httpd | ⚠️ Additional HTTP endpoint — check purpose (admin UI?) and patch level. |
|110/tcp | open    | pop3      | Dovecot pop3d | ⚠️ Mail retrieval service — ensure TLS (POP3S) or deprecation of plain auth. |
|143/tcp | open    | imap      | Dovecot imapd | ⚠️ Mail access service — enforce STARTTLS / IMAPS, strong auth policies. |
|443/tcp | open    | ssl/http  | nginx | ✔️ HTTPS present — verify TLS config, cert validity, and modern ciphers (TLS 1.2/1.3). |
|444/tcp | open    | ssl/http  | Apache httpd | ⚠️ Alternate HTTPS — confirm its role and TLS settings. |
|465/tcp | open    | ssl/smtp  | Exim smtpd 4.98.2 | ⚠️ SMTPS active — check authentication, open relay status, and Exim security patches. |
|514/tcp | filtered| shell     | — | Filtered — historically insecure (syslog/shell); no firm conclusion without further auth. |
|587/tcp | open    | smtp      | Exim smtpd 4.98.2 | ⚠️ Submission port — ensure authentication required and rate/relay controls in place. |
|631/tcp | filtered| ipp       | — | Filtered — IPP (printer) visibility limited; verify exposure if printers are not intended to be public. |
|993/tcp | open    | imaps?    | — | ⚠️ Likely IMAPS (secure IMAP). Confirm TLS certificate and auth hardening. |
|995/tcp | open    | pop3s?    | — | ⚠️ Likely POP3S (secure POP3). Confirm TLS and disable plain POP3 if unused. |
|3306/tcp| open    | mysql     | MySQL (unauthorized) | 🔥 **High risk** — database port exposed to Internet; if truly accessible, restrict to internal networks or VPN immediately. |

---

## Quick Recommendations
- **Immediate (High priority):**
  - Restrict **3306 (MySQL)** to internal networks / VPN or firewall it off from the public Internet. Exposed DB ports are high-risk.
  - Ensure **SMTP (25/465/587)** requires authentication and is not an open relay.
- **High / Medium priority:**
  - Harden **SSH (22)**: disable password auth, use key-based login, and enable fail2ban or equivalent rate-limiting.
  - Verify TLS configurations on **443 / 444 / 993 / 995 / 465** — prefer TLS 1.3, disable weak ciphers, and check cert expiries.
  - Audit the **PowerDNS (53)** server for AXFR misconfiguration and consider DNSSEC if applicable.
  - Identify why **HTTP on port 81** exists and remove or secure any unnecessary additional web endpoints.
- **General:**
  - Keep services updated (Exim, Dovecot, Apache, nginx, MySQL, PowerDNS).
  - Scan internally and perform authenticated web application testing (with authorization) for admin panels or sensitive endpoints.
  - Log and monitor connections to high-risk services; implement alerting for anomalous access.


