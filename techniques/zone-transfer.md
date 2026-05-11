# DNS Zone Transfer (AXFR)

## Description

Zone transfer is used by DNS servers to synchronize records.

If misconfigured, it allows full disclosure of DNS data.

---

## Command

```bash
dig axfr domain.com @DNS_SERVER
```

---

## Impact

* Exposure of all subdomains
* Discovery of internal hosts
* Increased attack surface
* Information disclosure vulnerability

---

## Key Insight

Zone transfer is one of the most valuable DNS misconfigurations.

Always test it early during reconnaissance.

