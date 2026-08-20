# Phishing Email Analysis Methodology

## Overview

This document describes the methodology used to investigate suspicious
emails in this project.

The objective is to determine whether an email should be classified as:

- Benign
- Suspicious
- Phishing

The investigation is based on multiple pieces of evidence rather than
a single indicator.

---

## 1. Email Triage

The first step is to review the basic email information.

The analyst examines:

- Sender
- Recipient
- Subject
- Reply-To address
- Return-Path
- Date and time
- Message-ID
- Mail client
- Email body
- Embedded URLs
- Attachments

### Initial Questions

The analyst asks:

1. Who sent the email?
2. Does the sender domain match the claimed organization?
3. Does the Reply-To address match the sender?
4. Is the subject creating unusual urgency?
5. Does the email request credentials, payment, or sensitive information?
6. Are there suspicious links or attachments?

---

# 2. Header Analysis

Email headers provide information about how the message travelled
through the mail infrastructure.

Important headers include:

- Return-Path
- Received
- From
- Reply-To
- Message-ID
- Authentication-Results
- X-Originating-IP

The analyst reviews the `Received` headers from the bottom upward to
understand the apparent delivery path.

---

# 3. SPF Analysis

Sender Policy Framework (SPF) is checked using the authentication
results in the email headers.

Example:

    spf=fail

A failed SPF result can indicate that the sending server is not
authorized to send email for the claimed domain.

However:

> SPF failure alone does not prove that an email is phishing.

It should be correlated with other evidence.

---

# 4. DKIM Analysis

DomainKeys Identified Mail (DKIM) provides cryptographic verification
of an email.

Possible results include:

- DKIM PASS
- DKIM FAIL
- DKIM NONE

A missing or failed DKIM result can increase suspicion, but it is not
automatically proof of malicious activity.

---

# 5. DMARC Analysis

DMARC helps determine whether the sender's domain passes authentication
and alignment checks.

The analyst records:

- DMARC result
- Domain policy
- Header From domain
- SMTP envelope domain

Example:

    dmarc=fail
    p=reject

A DMARC failure is an important indicator when investigating possible
sender impersonation.

---

# 6. Sender and Reply-To Analysis

The analyst compares:

    From:
    Return-Path:
    Reply-To:

A mismatch can be suspicious.

For example:

    From: security@example.com
    Reply-To: account.verify@unrelated-domain.com

This may indicate that the attacker wants responses sent to another
mailbox.

However, legitimate organizations can also use different Reply-To
addresses, so additional investigation is required.

---

# 7. Domain Analysis

The sender domain and URL domain are examined for:

- Typosquatting
- Character substitution
- Extra words
- Suspicious subdomains
- Unusual TLDs
- Look-alike domains
- Newly registered domains

Example:

    microsoft.com

versus:

    micros0ft-verify.com

The second domain uses a visually similar character and additional
text to imitate the legitimate organization.

---

# 8. URL Analysis

URLs contained in the email are extracted and documented.

The analyst checks:

- Domain
- URL path
- Parameters
- Redirects
- HTTPS usage
- Domain reputation
- Certificate information
- Hosting information

Important:

> HTTPS does not automatically mean that a URL is legitimate.

A phishing website can also use HTTPS.

URLs should be investigated in an authorized and isolated environment.

---

# 9. Social Engineering Analysis

The email body is analyzed for psychological manipulation.

Common indicators include:

- Urgency
- Fear
- Account suspension threats
- Password expiration warnings
- Financial pressure
- Confidentiality claims
- Authority impersonation
- Requests for immediate action

Example:

    "Your password expires in 24 hours."

This creates time pressure and attempts to reduce the recipient's
likelihood of independently verifying the request.

---

# 10. IOC / Observable Extraction

The analyst extracts useful observables from the email.

Examples:

- Domains
- IP addresses
- Email addresses
- URLs
- File hashes
- Attachment names
- Message IDs

Each observable is documented with its source and investigation context.

An observable should not automatically be labelled malicious.

---

# 11. Evidence Correlation

The analyst combines multiple indicators.

Example:

    Typosquatted domain
          +
    SPF failure
          +
    DMARC failure
          +
    Suspicious URL
          +
    Credential request
          =
    High-confidence phishing

This approach reduces false positives.

---

# 12. Verdict

The investigation concludes with a clear verdict.

Possible classifications:

### Benign

No significant malicious indicators identified.

### Suspicious

Some unusual indicators exist, but additional evidence is required.

### Phishing

Multiple independent indicators strongly support malicious intent.

---

# 13. Confidence

The analyst records confidence separately from the verdict.

Example:

    Verdict: PHISHING
    Confidence: HIGH

or:

    Verdict: SUSPICIOUS
    Confidence: MEDIUM

Confidence should reflect the strength and quantity of the available
evidence.

---

# 14. Detection Engineering

After manual investigation, recurring indicators can be converted into
detection logic.

This project uses Sigma rules to represent detection logic.

The detection process is:

    Investigation
          ↓
    Identify recurring patterns
          ↓
    Create detection logic
          ↓
    Write Sigma rule
          ↓
    Test rule
          ↓
    Tune false positives

Detection rules should not rely on a single weak indicator.

---

# 15. MITRE ATT&CK Mapping

Where appropriate, phishing activity can be mapped to MITRE ATT&CK.

Example:

    T1566.002
    Phishing: Spearphishing Link

The mapping is included to demonstrate how observed email behavior
relates to a standardized threat framework.

---

# 16. Investigation Safety

Email investigations should be performed using authorized samples and
controlled environments.

Analysts should avoid opening suspicious URLs or attachments directly
from a production workstation.

Recommended approach:

    Raw Email
       ↓
    Extract Indicators
       ↓
    Analyze Safely
       ↓
    Correlate Evidence
       ↓
    Determine Verdict
       ↓
    Document Findings

---

# 17. Project Scenarios

This methodology is demonstrated through two training scenarios.

## Scenario 01

A Microsoft 365-themed credential phishing email containing:

- Brand impersonation
- Typosquatted domain
- SPF failure
- DKIM absence
- DMARC failure
- Reply-To mismatch
- Urgency
- Credential verification URL

Final assessment:

    PHISHING — HIGH CONFIDENCE

## Scenario 02

A business-themed email requesting review of a Q4 OKR document.

The email contains:

- Business urgency
- Document-access request
- External URL
- Originating IP

However, SPF, DKIM and DMARC pass.

Final assessment:

    SUSPICIOUS — MEDIUM CONFIDENCE
