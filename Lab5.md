| Aspect | Passive Recon | Active Recon |
|---|---:|---:|
| Definition | Gathering information without interacting directly with the target (observational). | Probing the target directly to discover services, hosts, and vulnerabilities. |
| Tool Examples | whois, theHarvester, OSINT (public records, search engines, certificates) | nmap, ping, traceroute, banner grabbing, vulnerability scanners |
| Risk Level | Low — non-intrusive, usually safe | High — can trigger alerts or disrupt services |
| Detection Possibility | Minimal — hard to detect when only using public sources | High — network probes are logged and detectable |
| Data Depth | Broad contextual info (contacts, domains, public IPs, historical data) | Deep technical details (open ports, services, versions, misconfigurations) |
| Typical Use Cases | Recon before engagement, target profiling, footprinting, compliance/OSINT | Scanning for vulnerabilities, penetration testing, network discovery |
| Legal / Ethical Considerations | Usually acceptable when using public sources — respect privacy and TOS | Requires explicit authorization (e.g., written permission) to avoid legal issues |
| Recommended When | Building a list of public assets, mapping organizational footprint, low-risk intel gathering | You have permission to test, need technical findings, or are doing a sanctioned security assessment |

**When to use each method:**  
Use **passive reconnaissance** when you need to map a target’s public footprint safely and quietly — it’s ideal for initial research, asset discovery, and gathering contextual information from public sources (WHOIS, certificates, search engines) without touching the target. Use **active reconnaissance** only when you have explicit authorization (written permission); it’s appropriate for in-depth technical discovery (open ports, services, versions, misconfigurations) during sanctioned penetration tests or vulnerability assessments, since it can be detectable and carry legal/operational risk.
