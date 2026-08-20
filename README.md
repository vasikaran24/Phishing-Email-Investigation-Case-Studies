# Phishing Email Investigation & Detection Case Studies

A practical SOC analyst portfolio project focused on phishing email
triage, header analysis, IOC extraction, investigation, verdict
development, and Sigma detection engineering.

> **Important:** The scenarios in this repository are based on
> sanitized training material from InfoSecLabs. They are provided for
> educational and defensive security analysis only.

---

## Project Overview

Phishing emails are one of the most common initial-access techniques
used by attackers.

This project demonstrates how a SOC analyst can investigate suspicious
emails using multiple sources of evidence instead of relying on a
single indicator.

The project currently contains two investigation scenarios covering
different levels of phishing sophistication.

The investigations follow this workflow:

```text
Raw Email
    |
    v
Initial Triage
    |
    v
Email Header Analysis
    |
    v
SPF / DKIM / DMARC Analysis
    |
    v
Sender & Domain Analysis
    |
    v
URL Analysis
    |
    v
Social Engineering Analysis
    |
    v
IOC Extraction
    |
    v
Evidence Correlation
    |
    v
Verdict
    |
    v
Sigma Detection
