# Active Subdomain Enumeration

## Purpose

Discover subdomains that are not publicly exposed or visible through standard DNS queries.

This technique uses a wordlist to brute-force potential subdomains against the target DNS server.

---

## Example Command

```bash id="2jcds7"
dnsenum --dnsserver DNS_SERVER \
--enum \
-p 0 \
-s 0 \
-o subdomains.txt \
-f wordlist.txt \
domain.com
```

---

## Parameters

| Parameter     | Description                     |
| ------------- | ------------------------------- |
| `--dnsserver` | Specify target DNS server       |
| `--enum`      | Perform DNS enumeration         |
| `-p 0`        | Disable reverse lookup scanning |
| `-s 0`        | Disable scraping                |
| `-o`          | Save output to file             |
| `-f`          | Specify wordlist                |

---

## Security Insight

Subdomain brute forcing may reveal:

* internal applications
* development environments
* administrative portals
* hidden services

Examples:

* dev.domain.com
* admin.domain.com
* vpn.domain.com
* internal.domain.com

---

## Attack Surface Expansion

Discovered subdomains should be:

* scanned with Nmap
* checked for web services
* tested for virtual hosts
* further enumerated
