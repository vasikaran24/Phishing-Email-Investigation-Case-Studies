# SOC Phishing Investigation Workflow

## Objective

This workflow describes the process followed by the analyst when
investigating a suspicious email.

---

## Phase 1 — Triage

Collect:

- Sender
- Recipient
- Subject
- Reply-To
- Return-Path
- Date
- URLs
- Attachments

Determine whether the email requires further investigation.

---

## Phase 2 — Header Investigation

Review:

- Received headers
- Sending IP
- Mail relays
- SPF
- DKIM
- DMARC
- Message-ID
- Originating IP

Document unusual findings.

---

## Phase 3 — Content Investigation

Analyze:

- Subject
- Language
- Urgency
- Requested action
- Brand impersonation
- Credential requests
- Payment requests
- Attachments
- URLs

---

## Phase 4 — IOC Extraction

Extract:

| Type | Example |
|------|---------|
| Domain | suspicious-domain.com |
| IP | 203.0.113.10 |
| Email | attacker@example.com |
| URL | https://example.com/login |
| Hash | SHA256 hash |

Record the source of every observable.

---

## Phase 5 — Correlation

Compare the extracted indicators against available security
telemetry and threat-intelligence sources.

Possible sources include:

- DNS logs
- Proxy logs
- SIEM
- EDR
- Email gateway
- Threat intelligence
- Authentication logs

---

## Phase 6 — Verdict

Assign:

    BENIGN
    SUSPICIOUS
    PHISHING

Then assign a confidence level:

    LOW
    MEDIUM
    HIGH

The verdict must be supported by documented evidence.

---

## Phase 7 — Detection

If recurring indicators are identified:

1. Develop detection logic.
2. Create a Sigma rule.
3. Test the rule.
4. Review false positives.
5. Tune the rule.
6. Document the detection.

---

## Phase 8 — Documentation

Each investigation should contain:

- Raw evidence
- Investigation notes
- Extracted observables
- Detection logic
- Final verdict
- Analyst reasoning

---

## Complete Workflow

```text
Email Received
      |
      v
Initial Triage
      |
      v
Header Analysis
      |
      v
Authentication Analysis
      |
      v
Body & URL Analysis
      |
      v
IOC Extraction
      |
      v
Threat Intelligence / SIEM Correlation
      |
      v
Verdict
      |
      v
Detection Engineering
      |
      v
Documentation
