# DNS Enumeration Workflow

A structured approach to DNS enumeration:

---

## 1. Identify Name Servers

Determine authoritative DNS servers.

```bash
# DNS Authority Enumeration

A structured approach to identifying authoritative DNS infrastructure.

---

## SOA Enumeration

The SOA (Start of Authority) record provides information about:

* the primary DNS server
* zone administration
* DNS timing configuration

### Command

```bash
dig soa domain.com
```

### Example Response

```text
; <<>> DiG 9.x <<>> soa domain.com
;; ->>HEADER<<- opcode: QUERY, status: NOERROR

;; QUESTION SECTION:
;domain.com.          IN SOA

;; AUTHORITY SECTION:
domain.com. 900 IN SOA ns-161.awsdns-20.com. awsdns-hostmaster.amazon.com.
```

### Security Insight

SOA records may reveal:

* primary DNS infrastructure
* DNS provider information
* administrative naming conventions

---

## NS Enumeration

Identify authoritative name servers.

### Command

```bash
dig ns domain.com @DNS_SERVER
```

### Example Response

```text
; <<>> DiG 9.x <<>> ns domain.com @192.168.x.x

;; ->>HEADER<<- opcode: QUERY, status: NOERROR
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;domain.com.          IN NS

;; ANSWER SECTION:
domain.com. 604800 IN NS ns.domain.com.

;; ADDITIONAL SECTION:
ns.domain.com. 604800 IN A 127.0.0.1
```
```text
dig CH TXT version.bind @targetIP
<<>> DiG 9.18.33-1~deb12u2-Debian <<>> CH TXT version.bind @targetIP
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41447
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 6f0fdc07326b35210100000069ff4444f19e2c679cfa1c3b (good)
;; QUESTION SECTION:
;version.bind.			CH	TXT

;; ANSWER SECTION:
version.bind.		0	CH	TXT	"9.16.1-Ubuntu"

;; Query time: 9 msec
;; SERVER: targetIP
;; WHEN: Sat May 09 09:27:16 CDT 2026
;; MSG SIZE  rcvd: 95
```
### We can use the option ANY to view all available records. This will cause the server to show us all available entries that it is willing to disclose. It is important to note that not all entries from the zones will be shown.



### Security Insight

NS enumeration helps identify:

* authoritative DNS servers
* DNS authority structure
* potential targets for deeper DNS enumeration


## 2. Test Zone Transfer (AXFR)

Attempt to retrieve the full DNS zone.

```bash
dig axfr domain.com @DNS_SERVER
```

If successful:

* All DNS records are exposed
* Internal infrastructure becomes visible

---

## 3. Enumerate TXT Records
```text
dig CH TXT version.bind @targetIP
<<>> DiG 9.18.33-1~deb12u2-Debian <<>> CH TXT version.bind @targetIP
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41447
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 6f0fdc07326b35210100000069ff4444f19e2c679cfa1c3b (good)
;; QUESTION SECTION:
;version.bind.			CH	TXT

;; ANSWER SECTION:
version.bind.		0	CH	TXT	"9.16.1-Ubuntu"

;; Query time: 9 msec
;; SERVER: targetIP
;; WHEN: Sat May 09 09:27:16 CDT 2026
;; MSG SIZE  rcvd: 95
```
Look for:

* SPF records
* verification tokens
* infrastructure hints

---

## 4. Analyze SPF Records

SPF may reveal:

* internal IP addresses
* third-party services
* hidden infrastructure

---

## 5. Subdomain Discovery

If AXFR fails:

* brute-force subdomains
* use wordlists

---

## 6. Reverse DNS Enumeration

Identify hostnames from IP ranges.

```bash
dig -x IP_ADDRESS
```

---

## 7. Expand Attack Surface

Use discovered data for:

* service scanning
* web enumeration
* further exploitation
