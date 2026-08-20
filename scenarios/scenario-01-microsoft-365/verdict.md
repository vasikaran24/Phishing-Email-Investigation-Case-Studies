# Scenario 01 — Final Verdict

## Classification

**PHISHING**

## Confidence

**HIGH**

## Likely Objective

Credential theft through a fake Microsoft 365 verification page.

## Key Evidence

1. Microsoft look-alike domain
2. SPF failure
3. DKIM absent
4. DMARC failure
5. Reply-To mismatch
6. Urgent password-expiration message
7. Account suspension threat
8. Suspicious credential verification URL

## Primary IOC

`micros0ft-verify.com`

## Additional IOC

`103.224.182.251`

## MITRE ATT&CK

**T1566.002 — Phishing: Spearphishing Link**

## Recommended Response

- Quarantine the message
- Search for other recipients
- Search DNS/proxy logs for the domain
- Determine whether the URL was accessed
- Check for credential submission
- Investigate affected accounts
- Block confirmed malicious infrastructure
- Reset compromised credentials
- Monitor affected accounts

## Analyst Conclusion

I classified this email as a high-confidence phishing attempt because
multiple independent indicators point toward the same conclusion.

The suspicious Microsoft look-alike domain, failed email
authentication, unrelated Reply-To address, urgency, credential
request, and suspicious URL make the message unsafe to trust.
