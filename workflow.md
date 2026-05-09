# DNS Enumeration Workflow

A structured approach to DNS enumeration:

---

## 1. Identify Name Servers

Determine authoritative DNS servers.

```bash
dig soa domain.com
response:
; <<>> DiG 9.18.33-1~deb12u2-Debian <<>> soa domain.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45522
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;www.inlanefreight.com.		IN	SOA

;; AUTHORITY SECTION:
inlanefreight.com.	900	IN	SOA	ns-161.awsdns-20.com. awsdns-hostmaster.amazon.com. 1 7200 900 1209600 86400

;; Query time: 16 msec
;; SERVER: 1.1.1.1#53(1.1.1.1) (UDP)
;; WHEN: Sat May 09 07:52:55 CDT 2026
;; MSG SIZE  rcvd: 128
___________________________________
dig ns domain.com

resoponse:

```

---

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

```bash
dig txt domain.com
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
