# Phishing Email Investigation & Detection Case Studies

A practical SOC analyst portfolio project focused on phishing email
triage, header analysis, IOC extraction, investigation, verdict
development, and Sigma detection engineering.

> **Important:** The scenarios in this repository are based on
> sanitized training material from InfoSecLabs. They are provided for
> educational and defensive security analysis only.

---

| Skill                        | Demonstrated |
| ---------------------------- | ------------ |
| Email Header Analysis        | ✅            |
| Phishing Triage              | ✅            |
| SPF Analysis                 | ✅            |
| DKIM Analysis                | ✅            |
| DMARC Analysis               | ✅            |
| Sender Analysis              | ✅            |
| Reply-To Analysis            | ✅            |
| Domain Analysis              | ✅            |
| URL Analysis                 | ✅            |
| IOC Extraction               | ✅            |
| Social Engineering Analysis  | ✅            |
| Evidence Correlation         | ✅            |
| Incident Verdict Development | ✅            |
| Sigma Detection Engineering  | ✅            |
| MITRE ATT&CK Mapping         | ✅            |
| False Positive Analysis      | ✅            |
| SOC Documentation            | ✅            |

Investigation Scenarios
-------------------------

Scenario 01 — Microsoft 365 Credential Phishing
----------------------------------------------

Scenario Type

Credential phishing / brand impersonation

Key Indicators
Microsoft 365 impersonation
Typosquatted domain
SPF failure
DKIM absent
DMARC failure
Reply-To mismatch
Password expiration theme
Account suspension threat
Credential verification URL
Verdict
PHISHING
Confidence: HIGH
MITRE ATT&CK
T1566.002 — Phishing: Spearphishing Link
Investigation

See:

scenarios/scenario-01/

Scenario 02 — Suspicious Business Document Request
-------------------------------------------------
Scenario Type

Business-themed suspicious email

Key Indicators
---------------

Action-oriented subject
Business deadline
Document review request
External URL
Originating IP
Business-sensitive information
Authentication Results
SPF  = PASS
DKIM = PASS
DMARC = PASS

Unlike Scenario 01, this scenario does not contain obvious email
authentication failures.

This demonstrates an important investigation principle:

Authentication success does not automatically mean an email is
completely safe.

Verdict
SUSPICIOUS
Confidence: MEDIUM

Additional validation is required before classifying the message as
confirmed phishing.

Investigation
| Indicator                 |  Scenario 01 |    Scenario 02 |
| ------------------------- | -----------: | -------------: |
| Brand impersonation       |            ✅ |              ❌ |
| Typosquatting             |            ✅ |              ❌ |
| SPF failure               |            ✅ |              ❌ |
| DKIM failure/absence      |            ✅ |              ❌ |
| DMARC failure             |            ✅ |              ❌ |
| Reply-To mismatch         |            ✅ |              ❌ |
| Urgency                   |            ✅ |              ✅ |
| External URL              |            ✅ |              ✅ |
| Business document request |            ❌ |              ✅ |
| Credential request        |            ✅ |              ❌ |
| Final verdict             | **PHISHING** | **SUSPICIOUS** |
| Confidence                |     **HIGH** |     **MEDIUM** |

