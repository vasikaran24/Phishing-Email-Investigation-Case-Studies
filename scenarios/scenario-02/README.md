# Scenario 02 — Business Email Phishing Investigation

## Overview

This case study documents the investigation of a business-themed email
that claims to be from **Sarah Chen, VP of Operations at Company
Partners Ltd.**

The email asks department heads to review a Q4 OKR document before an
end-of-week deadline.

At first glance, the message appears to be a normal business email.
However, the presence of an external document link, deadline-based
urgency, and an unusual originating IP makes further investigation
necessary.

This investigation demonstrates how a SOC analyst can evaluate a
potential phishing email using email headers, authentication results,
sender information, URLs, and social-engineering indicators.

> **Source:** InfoSecLabs training scenario  
> **Purpose:** Educational / defensive security analysis  
> **Data classification:** Sanitized training data

---

## Investigation Objective

The primary objective of this investigation is to determine whether the
email represents a legitimate business communication, a suspicious
message, or a phishing attempt.

The investigation focuses on:

1. Validating the sender identity.
2. Examining the email delivery path.
3. Reviewing SPF, DKIM, and DMARC results.
4. Checking for sender and domain inconsistencies.
5. Investigating the originating IP address.
6. Analyzing the URL contained in the email.
7. Identifying social-engineering techniques.
8. Extracting relevant security observables.
9. Determining the appropriate analyst verdict.
10. Identifying additional investigation steps required before
   considering the email trusted.

---

## Investigation Scope

The following email components were reviewed:

- Email headers
- Return-Path
- From address
- Received headers
- Authentication-Results
- SPF
- DKIM
- DMARC
- Subject
- Message body
- Embedded URL
- X-Originating-IP
- Mail client information
- Social-engineering characteristics

---

## Email Summary

| Field | Value |
|---|---|
| Sender | s.chen@company-partners.com |
| Display Name | Sarah Chen |
| Claimed Role | VP of Operations |
| Recipient | analyst@infoseclabs.io |
| Subject | Q4 OKR Review - Action Required by EOD Friday |
| SPF | PASS |
| DKIM | PASS |
| DMARC | PASS |
| X-Originating-IP | 185.143.223.67 |
| Mail Client | Microsoft Outlook 16.0 |
| URL Domain | company-partners.com |

---

## Investigation Methodology

The investigation follows a basic SOC email-triage workflow:

```text
Email Received
      |
      v
Header Analysis
      |
      v
Sender Validation
      |
      v
SPF / DKIM / DMARC Analysis
      |
      v
Mail-Flow Analysis
      |
      v
URL Analysis
      |
      v
Social-Engineering Analysis
      |
      v
IOC Extraction
      |
      v
Evidence Correlation
      |
      v
Final Verdict
