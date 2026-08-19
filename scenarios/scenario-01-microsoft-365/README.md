
# Scenario 01 — Microsoft 365 Password Expiration

## What happened?

The email claims to come from the Microsoft 365 security team and
warns that the user's password will expire within 24 hours.

The recipient is told to verify their credentials through a link.

My initial reaction was that this looked suspicious, so I started by
checking the sender, authentication results, domain, and URL.

---

## Initial Verdict

**Phishing**

**Confidence: High**

---

## What made me suspicious?

The main things that stood out were:

- The sender domain looks like a Microsoft domain but is not
  `microsoft.com`
- SPF failed
- DKIM was absent
- DMARC failed
- The Reply-To address uses another domain
- The email asks for immediate credential verification
- The message threatens account suspension
- The verification URL uses the same suspicious look-alike domain

---

## Investigation Files

- [Email Sample](email-sample.txt)
- [My Investigation](investigation.md)
- [IOC List](iocs.csv)
- [Phishing Checklist](checklist.md)
- [Final Verdict](verdict.md)

---

## Training Source

InfoSecLabs training scenario.

The analysis and investigation notes in this repository are my own.
