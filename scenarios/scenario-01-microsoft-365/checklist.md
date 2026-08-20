# Scenario 01 — Phishing Investigation Checklist

## Email Authentication

| Check | Result | Assessment |
|---|---|---|
| SPF | FAIL | Suspicious |
| DKIM | NONE | Supporting indicator |
| DMARC | FAIL | Suspicious |

## Sender Analysis

| Check | Result | Assessment |
|---|---|---|
| Sender domain | `micros0ft-verify.com` | Typosquatting |
| Return-Path | Same suspicious domain | Suspicious |
| Reply-To | Different domain | Suspicious |

## Content Analysis

| Check | Result | Assessment |
|---|---|---|
| Urgency | 24-hour deadline | Suspicious |
| Account threat | Account suspension | Suspicious |
| Credential request | Yes | High-risk indicator |
| Brand impersonation | Microsoft 365 | Suspicious |

## URL Analysis

| Check | Result | Assessment |
|---|---|---|
| URL domain | `micros0ft-verify.com` | Suspicious |
| Credential page | `/o365/verify` | High-risk |
| Domain impersonation | Yes | Suspicious |

---

## Final Checklist

- [x] Sender spoofing / impersonation
- [x] SPF authentication failure
- [x] DKIM absent
- [x] DMARC authentication failure
- [x] Typosquat domain
- [x] Urgency / social engineering
- [x] Suspicious URL
- [x] Credential request
- [x] Reply-To mismatch

## Verdict

**PHISHING**

## Confidence

**HIGH**
