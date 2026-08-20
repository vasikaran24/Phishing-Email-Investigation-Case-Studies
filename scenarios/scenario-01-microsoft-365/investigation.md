# Scenario 01 — Phishing Email Investigation

## Investigation Summary

I received an email that appeared to be a Microsoft 365 password
expiration notification. The email asked the recipient to verify their
credentials within 24 hours or the account would supposedly be
suspended.

At first glance, the email looked like a normal Microsoft 365
notification. However, when I checked the sender and email headers,
several things did not look right.

I started the investigation with the sender address and then checked
the authentication results, Reply-To address, and URL.

---

## 1. Sender Analysis

The email claims to be from:

`"Microsoft 365 Team" <no-reply@micros0ft-verify.com>`

The first thing I noticed was the domain.

Instead of:

`microsoft.com`

the email uses:

`micros0ft-verify.com`

The `o` in "Microsoft" has been replaced with a `0`.

This looks like an attempt to make the domain look legitimate at a
quick glance.

### My finding

I identified this as a Microsoft brand impersonation / typosquatting
indicator.

---

## 2. Return-Path Analysis

The Return-Path is:

`bounce@micros0ft-verify.com`

It uses the same suspicious domain as the sender.

The fact that the Return-Path matches the From domain does not make the
email legitimate. The domain itself is still suspicious.

### My finding

The Return-Path provides another reference to the suspicious domain,
which I would include in my IOC list.

---

## 3. Received Header Analysis

The headers show the message coming through:

`mail.micros0ft-verify.com`

with the external IP:

`103.224.182.251`

I also noticed the header contains:

`192.168.1.105`

This is a private IP address, so I would not treat it as the actual
public source of the email.

For my investigation, the more useful external indicator is:

`103.224.182.251`

### My finding

I would record `103.224.182.251` as an IOC and investigate it further
using approved threat-intelligence sources in a real SOC environment.

---

## 4. SPF Analysis

The Authentication-Results header shows:

`SPF = FAIL`

The header also states that `103.224.182.251` is not authorized to
send email for `micros0ft-verify.com`.

This was another important finding.

The sending server failed the domain's SPF authorization check.

### My finding

SPF failure is a strong supporting indicator that the email was not
sent through an authorized mail server for the claimed domain.

I would not make the phishing decision based on SPF alone, but it adds
significant evidence when combined with the other findings.

---

## 5. DKIM Analysis

The header shows:

`DKIM = NONE`

There is no DKIM signature available for this message.

DKIM being absent does not automatically mean that an email is
phishing. Some legitimate email systems may not use DKIM.

However, in this case I found it together with SPF failure and DMARC
failure.

### My finding

I treated the missing DKIM as a supporting indicator rather than
the main reason for the phishing verdict.

---

## 6. DMARC Analysis

The authentication results show:

`DMARC = FAIL`

The policy shown in the header is:

`p=REJECT`

This means the message failed the domain's DMARC authentication
requirements.

At this point, the authentication results were:

- SPF — FAIL
- DKIM — NONE
- DMARC — FAIL

That combination increased my confidence that the message was not a
legitimate Microsoft 365 email.

### My finding

The DMARC failure is another strong indicator supporting the phishing
classification.

---

## 7. Reply-To Analysis

The From address is:

`no-reply@micros0ft-verify.com`

But the Reply-To address is:

`account-verify@webmail-support.net`

These are completely different domains.

This caught my attention because the email claims to represent
Microsoft, but replies would be sent to another unrelated domain.

### My finding

I identified this as a suspicious Reply-To mismatch.

This could be used to redirect communication to infrastructure
controlled by the attacker.

---

## 8. Subject and Social Engineering

The subject says:

`Action Required: Your Microsoft 365 password expires in 24 hours`

The email also says that the account will be suspended if the user
does not verify their credentials.

The 24-hour deadline creates pressure on the recipient.

Instead of giving the user time to verify the notification through
normal Microsoft 365 channels, the email encourages them to act
immediately.

### My finding

I identified the following social-engineering techniques:

- Urgency
- Fear of account suspension
- Short deadline
- Request for immediate action

These are common warning signs in credential-phishing emails.

---

## 9. URL Analysis

The email contains this URL:

`https://micros0ft-verify.com/o365/verify`

The domain has the same typo that I found in the sender address:

`micros0ft`

instead of:

`microsoft`

The `/o365/verify` path also makes the URL appear related to Microsoft
365.

The link is asking the recipient to verify their credentials.

I would not open this URL directly from a normal workstation. If I
needed to investigate the destination further, I would use an isolated
analysis environment and approved security tools.

### My finding

I classified the URL as a suspicious credential-phishing URL.

---

## 10. Email Body Analysis

The main message says:

"Your password will expire in 24 hours."

It then asks the user to:

"verify your credentials immediately."

This is important because the email is not just informing the user
about a password policy. It is directing the user to a link where they
are expected to verify credentials.

Combined with the suspicious domain, this strongly suggests that the
purpose of the link is to capture the user's credentials.

### My finding

The likely objective is credential theft.

---

## 11. X-Mailer Analysis

The email contains:

`X-Mailer: PHPMailer 6.8.0`

I would not treat this as proof of phishing.

PHPMailer is a legitimate email-sending library and can be used by
both legitimate applications and malicious actors.

In this case, I consider it supporting information only.

---

# IOC Collection

During the investigation, I identified the following indicators:

| Type | Indicator | Why I recorded it |
|---|---|---|
| Domain | `micros0ft-verify.com` | Microsoft look-alike domain |
| IP | `103.224.182.251` | External sending IP |
| Sender | `no-reply@micros0ft-verify.com` | Suspicious sender |
| Reply-To | `account-verify@webmail-support.net` | Different domain |
| URL | `https://micros0ft-verify.com/o365/verify` | Suspicious credential link |

---

# Why I Classified It as Phishing

I did not classify the email as phishing because of just one suspicious
indicator.

The decision came from looking at all the evidence together.

I found:

- A Microsoft look-alike domain
- SPF failure
- No DKIM signature
- DMARC failure
- A different Reply-To domain
- A 24-hour deadline
- An account-suspension threat
- A request to verify credentials
- A suspicious Microsoft 365-looking URL

Each finding adds more confidence to the overall assessment.

---

# Final Verdict

**Verdict:** PHISHING

**Confidence:** HIGH

**Likely Objective:** Credential Theft

**MITRE ATT&CK:** T1566.002 — Phishing: Spearphishing Link

---

# What I Would Do Next in a SOC

If I received this email in a real SOC environment, I would not stop
after identifying it as phishing.

My next steps would be:

1. Search the mail system to see who else received the email.
2. Check whether any user clicked the URL.
3. Search DNS/proxy logs for the suspicious domain.
4. Check whether credentials were submitted.
5. Investigate affected Microsoft 365 accounts for unusual sign-ins.
6. Quarantine similar messages.
7. Block the confirmed malicious domain where appropriate.
8. Reset credentials if a user was compromised.
9. Continue monitoring affected accounts.
10. Document the incident and preserve the original email as evidence.

---

# Analyst Conclusion

After reviewing the email headers, sender information, authentication
results, message content, and URL, I classified this as a
high-confidence phishing email impersonating Microsoft 365.

The strongest evidence for my decision was the combination of the
typosquatted domain, SPF failure, missing DKIM, DMARC failure,
Reply-To mismatch, urgency, credential request, and suspicious URL.

The email appears to be designed to convince the recipient that their
Microsoft 365 password is about to expire and push them into providing
their credentials through the supplied link.
