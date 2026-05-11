# TXT and SPF Record Analysis

## TXT Records

TXT records may contain:

* verification tokens
* service integrations
* security policies

---

## SPF Records

SPF defines which servers can send email for a domain.

Example:

```
v=spf1 ip4:10.x.x.x include:service.com ~all
```

---

## What to Look For

* internal IP addresses
* cloud services
* third-party providers

---

## Security Insight

SPF records often leak infrastructure details:

* internal mail servers
* hidden IP ranges
* external dependencies

These can be used to identify new attack targets.

