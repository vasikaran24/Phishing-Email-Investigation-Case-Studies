
# Scenario 02 — Business Email

## Verdict

SUSPICIOUS — REQUIRES FURTHER INVESTIGATION

## Confidence

Medium

## Summary

The email presents itself as a business communication from Sarah Chen
at Company Partners Ltd regarding a Q4 OKR review.

Unlike Scenario 01, the email does not contain obvious authentication
failures. SPF, DKIM, and DMARC all pass, and the sender and URL use the
same domain.

However, the originating IP and the document-access request require
additional validation before the message can be considered trusted.

## Positive Legitimacy Indicators

- SPF authentication passed
- DKIM authentication passed
- DMARC authentication passed
- From and Return-Path use the same domain
- No suspicious Reply-To address
- Microsoft Outlook/Exchange indicators are present
- URL domain matches the sender domain
- Business context is plausible

## Investigation Concerns

- X-Originating-IP requires validation
- Email creates deadline pressure
- Message requests access to an important business document
- URL contains authentication-related parameters
- Sender identity should be independently verified

## Recommended Analyst Actions

1. Validate the originating IP against known corporate infrastructure.
2. Verify whether Sarah Chen actually sent the message.
3. Inspect the destination URL in an authorized isolated environment.
4. Check authentication and web-proxy logs for the recipient.
5. Search for similar messages sent to other users.
6. Review any authentication activity associated with the sender.
