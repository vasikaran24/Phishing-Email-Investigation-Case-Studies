# Detection Engineering — Scenario 01

## Detection Objective

The goal is to detect future phishing emails that use similar
characteristics to this investigation.

The detection should look for multiple signals instead of relying on
one indicator.

## Detection Signals

### 1. Microsoft Look-Alike Domain

Look for domains containing variations such as:

- micros0ft
- micros0ft-verify
- micros0ft-security
- micros0ft365-verify

These should be treated as suspicious indicators rather than automatic
proof of malicious activity.

### 2. Email Authentication Failure

Look for:

- SPF = FAIL
- DKIM = NONE/FAIL
- DMARC = FAIL

Multiple authentication failures increase confidence.

### 3. Reply-To Mismatch

Compare:

`From domain`

against:

`Reply-To domain`

A mismatch should increase the risk score.

### 4. Urgency

Look for phrases related to:

- password expiration
- account suspension
- verify immediately
- action required
- 24 hours
- account locked

### 5. Credential Request

Look for messages asking users to:

- verify credentials
- confirm password
- sign in
- verify account
- update password

### 6. Suspicious URL

Look for links where:

- the displayed brand does not match the destination
- the domain resembles a trusted brand
- the URL contains authentication-related paths

---

## Detection Logic

A single indicator should not automatically generate a high-confidence
phishing verdict.

Example scoring approach:

| Signal | Score |
|---|---:|
| Look-alike Microsoft domain | +3 |
| SPF failure | +2 |
| DKIM failure/absence | +1 |
| DMARC failure | +2 |
| Reply-To mismatch | +2 |
| Credential request | +2 |
| Urgent password/account message | +2 |
| Suspicious URL | +3 |

### Suggested Classification

0–3: Low Risk

4–6: Medium Risk

7–9: High Risk

10+: Critical / Investigate Immediately

This scoring model is intended for the lab and should be tuned before
production use.
