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
; <<>> DiG 9.x <<>> ns domain.com @ip-address

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

```bash
dig any domain.com @ip-address

; <<>> DiG 9.18.33-1~deb12u2-Debian <<>> any domainame.com @ip-address
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 19568
;; flags: qr aa rd; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 2
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 62e214bfc5366e83010000006a017bba8fb557247976a1ed (good)
;; QUESTION SECTION:
;inlanefreight.htb.		IN	ANY

;; ANSWER SECTION:
"Important info"

;; ADDITIONAL SECTION:
"Important info"

;; Query time: 9 msec
;; SERVER: 10.129.47.154#53(10.129.47.154) (TCP)
;; WHEN: Mon May 11 01:48:25 CDT 2026
;; MSG SIZE  rcvd: 437
```


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

If the administrator used a subnet for the allow-transfer option for testing purposes or as a workaround solution or set it to any, everyone would query the entire zone file at the DNS server. In addition, other zones can be queried, which may even show internal IP addresses and hostnames.
```bash
dig axfr domain.com @ip-address
```
* brute-force subdomains
* use wordlists

---

## 6. Reverse DNS Enumeration

Identify hostnames from IP ranges.

```bash
dig -x IP_ADDRESS
```

And also we can use dnsenum for brutoforcing:

```bash
dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb
```

## 7. Expand Attack Surface

Use discovered data for:

* service scanning
* web enumeration
* further exploitation
