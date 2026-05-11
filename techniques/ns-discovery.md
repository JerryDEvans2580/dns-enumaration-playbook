# Name Server Discovery

## Purpose

Identify authoritative DNS servers for a domain.

---

## Command

```bash
dig ns domain.com
```

---

## Output

Returns:

* primary DNS servers
* domain authority structure

---

## Security Insight

Knowing the DNS server allows:

* direct interaction
* zone transfer attempts
* deeper enumeration

