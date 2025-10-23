Passive (Linux)	Active (Linux)
Purpose: Gather information from public sources (domains, DNS, certificates, web content) without touching the target’s systems.	Purpose: Directly interact with the target to discover hosts, open ports, services and versions.
Common tools: whois, theHarvester, recon-ng, curl/wget (site scraping), PassiveTotal/PassiveDNS clients, shodan (querying), dig/nslookup (DNS lookup).	Common tools: nmap, masscan, netcat (nc), hping3, nikto, enum4linux, smtp-user-enum, sslscan.
Typical commands (examples): whois example.com; theHarvester -d example.com -b google; curl -I https://example.com; dig +short example.com.	Typical commands (examples): nmap -sS -p1-65535 example.com; masscan -p80,443 example.com; nc -v target 22; nikto -h http://example.com.
Data gained: Domain registrant, historical DNS, subdomains, public documents, leaked credentials references, exposed metadata, public-facing services listed in search engines.	Data gained: Open ports, running services, service versions, OS fingerprinting, reachable hosts, misconfigured services, response times.
Interaction level: No direct probes to target hosts — requests go to third-party sources or public endpoints only.	Interaction level: Sends packets/queries directly to target hosts and services (scans, banner grabs, crafted packets).
Risk & detection: Low risk; hard for the target to detect (uses public repositories/search engines).	Risk & detection: Higher risk; likely to appear in logs, IDS/IPS alerts or generate rate-limiting/blocks.
When to use: Initial reconnaissance, stealthy info collection, OSINT research, scoping before tests, compliance checks.	When to use: After consent in pentests, vulnerability discovery, network mapping, exploit development and verification.
Pros: Safe, legal-friendly when only using public data; useful for building attack surface map.	Pros: Accurate, detailed technical insight; reveals actual reachable services and potential attack vectors.
Cons: May miss hidden/filtered services; less technical detail.	Cons: Can alert defenders, may be blocked, and requires authorization in most contexts.

Summary On When To Use Them
Passive reconnaissance is best used in the early stages of information gathering when you want to collect data about a target without directly interacting with its systems, minimizing the risk of detection.
It relies on publicly available sources and open databases to gather intelligence discreetly. In contrast, active reconnaissance involves directly probing or interacting with the target—such as scanning ports or sending network requests—to obtain detailed technical information, making it suitable for later stages of penetration testing when more in-depth analysis is required, despite its higher risk of detection.
