# Phishing Email Investigation Case Studies

A hands-on SOC analyst portfolio project focused on investigating
suspicious emails and documenting the reasoning behind each security
verdict.

This repository contains four phishing/email investigation scenarios
based on cybersecurity training exercises.

The goal of this project is not simply to identify whether an email
is malicious. Each case documents how I examined the available
evidence, identified suspicious indicators, extracted IOCs, assessed
the risk, and decided what I would investigate next as a SOC analyst.

---

## What I Practice

- Email header analysis
- Sender and domain analysis
- SPF analysis
- DKIM analysis
- DMARC analysis
- URL analysis
- Social engineering identification
- IOC extraction
- Email authentication analysis
- MITRE ATT&CK mapping
- SOC investigation methodology
- Detection engineering
- Incident response recommendations

---

## Investigation Approach

For each email, I follow a consistent process:

1. Read the email and understand the context
2. Examine the sender and Return-Path
3. Trace the Received headers
4. Check SPF, DKIM, and DMARC
5. Inspect URLs and domains
6. Identify social engineering techniques
7. Extract useful IOCs
8. Compare the evidence
9. Assign a preliminary verdict
10. Identify what I would investigate next
11. Map confirmed malicious behavior to MITRE ATT&CK
12. Develop detection opportunities where applicable

---

## Case Studies

| Case | Scenario | Verdict |
|---|---|---|
| Scenario 01 | Microsoft 365 Password Expiration | Phishing |
| Scenario 02 | Q4 OKR Review | Suspicious / Investigate |

---

## Tools & Technologies

- Email header analysis
- Linux
- Python
- VirusTotal
- URL/domain reputation analysis
- DNS analysis
- Splunk
- Sigma
- MITRE ATT&CK

---

## Source

The scenarios in this repository are based on cybersecurity training
exercises from InfoSecLabs.

The original training material belongs to its respective owner.

This repository focuses on my own analysis, investigation reasoning,
IOC extraction, detection ideas, and security conclusions.

---

## Disclaimer

This repository is intended for educational and defensive security
research.

Any suspicious domains, IP addresses, URLs, or email addresses are
included for analysis purposes only.

Do not interact with suspicious infrastructure outside an authorized
and isolated environment.
