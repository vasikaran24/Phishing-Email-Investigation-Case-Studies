# Scenario 02 — Detection Engineering

## Objective

The objective of this detection is to identify business-themed emails
that combine multiple characteristics commonly associated with
phishing or suspicious email activity.

The rule is designed for analyst triage rather than automatic
classification.

## Detection Signals

The rule evaluates:

- Urgent/action-oriented subject
- Business document request
- External URL
- Originating IP information

Authentication failures are treated as an additional investigation
signal.

## Why Multiple Signals Are Used

A single indicator such as an external URL or an urgent subject can
occur in legitimate business emails.

Combining multiple signals reduces the likelihood of generating an
alert for every normal business message.

## Scenario 02 Result

The sample contains:

- Urgent subject: YES
- Business document request: YES
- External URL: YES
- Originating IP: YES
- SPF failure: NO
- DKIM failure: NO
- DMARC failure: NO

## Analyst Interpretation

The detection should identify the message for further review.

It should not automatically classify the message as confirmed
phishing.

## False Positives

Potential false positives include:

- Legitimate OKR notifications
- Corporate document-sharing emails
- Security-awareness simulations
- Normal deadline-driven business communications

## Recommended Response

When the rule generates an alert, the analyst should:

1. Validate the sender.
2. Investigate the originating IP.
3. Analyze the destination URL.
4. Search for similar messages.
5. Review authentication activity.
6. Correlate with proxy, DNS, and SIEM logs.
7. Assign the final verdict based on combined evidence.
