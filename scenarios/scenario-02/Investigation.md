# Scenario 02 — Business Email Investigation

## Case Overview

This case involves an email apparently sent by Sarah Chen,
identified as VP of Operations at Company Partners Ltd.

The email asks department heads to review a Q4 OKR document
before an end-of-week deadline.

At first glance, the message appears to be a normal business
communication. I therefore examined the sender, authentication
results, mail flow, originating IP, URL, and social-engineering
characteristics before reaching a verdict.

---

## 1. Sender Analysis

### From

`"Sarah Chen" <s.chen@company-partners.com>`

### Return-Path

`s.chen@company-partners.com`

The From address and Return-Path use the same domain.

I did not identify an obvious sender/Return-Path mismatch.

### Initial Assessment

No direct evidence of sender spoofing was identified from these
fields alone.

---

## 2. Email Authentication Analysis

### SPF

Result:

`PASS`

The authentication result states that `203.0.113.45` is
authorized to send mail for `company-partners.com`.

### DKIM

Result:

`PASS`

The DKIM signature was successfully verified for:

`company-partners.com`

### DMARC

Result:

`PASS`

The message passed DMARC authentication.

### Analyst Assessment

The authentication results are significantly different from a
typical spoofed phishing email.

SPF, DKIM, and DMARC all passed, so there is no authentication
failure that would independently indicate sender spoofing.

However, successful authentication does not automatically prove
that the message itself is safe.

---

## 3. Mail Flow Analysis

The headers show the following mail path:

`EXCH-CAS-02.corp.local`

↓

`relay.company-partners.com`

↓

`mx.infoseclabs.io`

↓

`mail.infoseclabs.io`

The headers indicate that the message passed through infrastructure
associated with `company-partners.com`.

The following originating IP was also observed:

`185.143.223.67`

This IP requires additional validation.

The available email headers alone do not establish whether this IP
belongs to authorized corporate infrastructure.

---

## 4. Subject Analysis

Subject:

`Q4 OKR Review - Action Required by EOD Friday`

The subject contains an action-oriented request and a deadline.

The phrase:

`Action Required`

combined with:

`EOD Friday`

creates pressure for the recipient to act quickly.

This is a potential social-engineering indicator.

However, business emails can legitimately contain deadlines, so this
indicator should not be treated as proof of phishing.

---

## 5. Body Analysis

The sender claims that the recipient needs to review:

- Q4 OKRs
- KPIs
- Budget allocations

The business context appears plausible.

The message does not request a password directly and does not contain
an obvious grammatical or formatting problem.

However, the recipient is encouraged to access an external document
through a supplied link.

This makes the URL an important part of the investigation.

---

## 6. URL Analysis

The email contains:

`https://company-partners.com/okrs/q4-2024/review?auth=s.chen&ref=okr-review-2024`

The URL uses the same domain as the sender:

`company-partners.com`

This is not an obvious look-alike domain.

However, the URL contains authentication-related parameters:

`auth=s.chen`

and:

`ref=okr-review-2024`

The destination should therefore be validated in an authorized,
isolated analysis environment before it is considered safe.

---

## 7. Social Engineering Indicators

The email contains:

- `Action Required`
- `EOD Friday deadline`
- Business-critical KPI information
- Budget information
- A document-access request

These characteristics can encourage a recipient to act without
independently verifying the request.

At this stage, they are supporting indicators rather than proof
of malicious activity.

---

## 8. Indicators of Compromise / Observables

| Type | Value | Source | Assessment |
|---|---|---|---|
| Domain | company-partners.com | From / Return-Path | Sender domain |
| IP | 203.0.113.45 | Received header | Mail relay |
| IP | 185.143.223.67 | X-Originating-IP | Requires validation |
| Email | s.chen@company-partners.com | From header | Claimed sender |
| URL | company-partners.com/okrs/q4-2024/review | Email body | Requires validation |

---

## 9. Investigation Findings

### Positive / Legitimate Indicators

- SPF passed.
- DKIM passed.
- DMARC passed.
- From and Return-Path match.
- Sender and URL use the same domain.
- Business context is plausible.
- Microsoft Outlook is identified as the mail client.

### Suspicious Indicators

- The message creates deadline pressure.
- The email requests access to a business document.
- The originating IP requires validation.
- The supplied URL has authentication-related parameters.

---

## 10. Analyst Assessment

Based only on the supplied evidence, I would not classify this email
as confirmed phishing.

The authentication controls passed and there is no obvious
look-alike sender domain or Reply-To mismatch.

However, the originating IP and destination URL require additional
investigation.

The message should therefore remain in a suspicious/unconfirmed state
until those indicators are validated.

---

## Final Verdict

**SUSPICIOUS — REQUIRES FURTHER INVESTIGATION**

### Confidence

**Medium**

### Primary Reason

There are some social-engineering and URL-related concerns, but the
available authentication evidence does not support a high-confidence
phishing verdict.

---

## Recommended SOC Actions

1. Validate `185.143.223.67`.
2. Confirm whether Sarah Chen actually sent the email.
3. Investigate the destination URL in an isolated environment.
4. Search the SIEM for similar messages.
5. Check whether other employees received the same email.
6. Review authentication activity associated with the sender.
7. Review DNS/proxy logs for access to the URL.
8. Compare the sender's normal communication pattern with this message.

---

## Analyst Conclusion

This case demonstrates why phishing investigations should not depend
on a single indicator.

SPF, DKIM, and DMARC passing does not automatically make an email safe.

Likewise, an urgent deadline does not automatically make an email
malicious.

A SOC analyst should correlate authentication results, sender identity,
mail flow, infrastructure, URLs, message context, and additional
security telemetry before assigning a final verdict.
