DNS Enumeration Playbook

This repository documents practical DNS enumeration techniques used during penetration testing.

The goal is to identify DNS misconfigurations, discover subdomains, and expand the attack surface for further analysis.

📌 Covered Techniques
Name Server (NS) discovery
DNS Zone Transfer (AXFR) testing
TXT record enumeration
SPF record analysis
Reverse DNS (PTR) enumeration
Subdomain discovery concepts
🎯 Objective

DNS enumeration is a critical reconnaissance step that allows attackers to:

Map internal infrastructure
Identify hidden services
Discover misconfigurations
Expand the attack surface
🧠 Key Insight

DNS is not just about resolving domains —
it is often a source of information leakage.

Misconfigured DNS servers can expose:

internal hostnames
private IP ranges
email infrastructure
third-party integrations
📂 Repository Structure
workflow.md → full enumeration process
techniques/ → individual DNS techniques
cheatsheet/ → quick command reference
⚠️ Disclaimer

All examples are generalized and do not reference any real or lab environments.
This repository is intended for educational purposes only.
