# TryHackMe SOC Simulator - Phishing Analysis

**Platform:** TryHackMe SOC Simulator  
**Difficulty:** Easy  
**Type:** Blue Team / SOC Alert Triage  
**Date:** 2026-03-25

---

## Overview

This lab uses the TryHackMe SOC Simulator to practice real-world phishing alert triage. Five alerts were investigated across two data sources: email logs and firewall logs ingested into Splunk. Each alert required pivoting between data sources to determine whether the activity was a true positive or false positive, document findings, and make escalation decisions. The scenario was completed with 260 points and a first place finish.

---

## Target Environment

| Field | Value |
|---|---|
| Organization | TheTryDaily |
| Data Sources | Email logs, Firewall logs |
| SIEM | Splunk |
| Total Alerts | 5 |
| True Positives | 3 |
| False Positives | 2 |

---

## Alert Summary

| Alert | Type | Verdict | Escalated |
|---|---|---|---|
| 1 | Inbound email with external link (hrconnex.thm) | False Positive | No |
| 2 | Inbound email with external link (hrconnex.thm resend) | False Positive | No |
| 3 | Inbound email with external link (m1crosoftsupport.co) | True Positive | Yes |
| 4 | Outbound connection to blacklisted URL (bit.ly) | True Positive | Yes |
| 5 | Inbound email with external link (urgents@amazon.biz) | True Positive | Yes |

---

## Investigation

### Alert 1 and 2: Legitimate HR Onboarding Emails

Both alerts were triggered by inbound emails sent to j.garcia@thetrydaily.thm from onboarding@hrconnex.thm containing an external onboarding link. The emails were sent at 18:31 and 18:37, the second being a resend of the first.

<img src="01-alert-details.png" width="800">

Pivoting to Splunk to investigate the sender domain returned three events including a critical internal email from h.harris to the IT team confirming that hrconnex.thm is the organization's legitimate third-party HR partner for onboarding.

<img src="02-splunk-investigation.png" width="800">

No firewall logs showed j.garcia attempting to access the link, confirming no endpoint activity occurred. Both alerts were closed as false positives.

<img src="03-false-positive-closure.png" width="800">

<img src="04-alert2-details.png" width="800">

<img src="05-alert2-false-positive-closure.png" width="800">

**Verdict: False Positive**

The alerts fired due to the presence of an external link, which is expected behavior for a legitimate third-party onboarding platform. The internal email from h.harris independently confirmed the vendor relationship.

---

### Alert 3: Microsoft Account Phishing - m1crosoftsupport.co

An inbound email was sent to c.allen@thetrydaily.thm from no-reply@m1crosoftsupport.co with the subject "Unusual Sign-In Activity on Your Microsoft Account."

<img src="07-alert3-details.png" width="800">

**Phishing indicators identified:**
- Sender domain m1crosoftsupport.co replaces the letter "i" with the number 1 to impersonate Microsoft
- Top level domain is .co instead of .com
- Urgency language: "secure your account immediately"
- Fabricated sign-in alert from Lagos, Nigeria to create panic
- Link directed to m1crosoftsupport.co/login, a credential harvesting page

Firewall log investigation confirmed that c.allen's endpoint 10.20.2.17 attempted to access the phishing URL. The connection was blocked by the Blocked Websites firewall rule.

<img src="06-alert3-splunk-investigation.png" width="800">

<img src="07-alert3-closure-part1.png" width="800">

<img src="08-alert3-closure-part2.png" width="800">

**Verdict: True Positive - Escalated**

Although the firewall blocked the outbound connection, c.allen clicked the phishing link indicating the email bypassed email security controls. The user requires phishing awareness training and the domain m1crosoftsupport.co should be permanently blocked at the email gateway and firewall.

---

### Alert 4 and 5: Amazon Package Phishing - urgents@amazon.biz

Alert 4 was a firewall alert triggered when endpoint 10.20.2.17 attempted to access a blacklisted bit.ly shortened URL. Alert 5 was the corresponding email alert for the same incident.

<img src="09-alert4-details.png" width="800">

Splunk investigation revealed two events from 10.20.2.17: a Google search for "how to set up payroll system for small business" at 18:33, and an outbound connection attempt to the bit.ly URL at 18:36 which was blocked.

<img src="10-alert4-investigation.png" width="800">

The email log confirmed the source: h.harris@thetrydaily.thm received a phishing email from urgents@amazon.biz impersonating Amazon with the subject "Your Amazon Package Couldn't Be Delivered - Action Required." The email contained the bit.ly URL and used a 48-hour deadline to create urgency.

**Phishing indicators identified:**
- Sender domain amazon.biz impersonating amazon.com using a lookalike domain
- URL shortener used to hide the real malicious destination
- Generic greeting "Dear Customer" instead of recipient's name
- Urgency language: "48 hours or your package will be returned"
- Firewall classified destination IP 67.199.248.11 as a known threat

<img src="11-alert4-closure-part1.png" width="800">

<img src="12-alert4-closure-part2.png" width="800">

<img src="13-alert5-details.png" width="800">

<img src="14-alert5-closure.png" width="800">

<img src="15-alert5-closure2.png" width="800">

**Verdict: True Positive - Escalated**

The phishing email bypassed email security controls and h.harris clicked the malicious link. The firewall blocked the connection before the destination was reached. Escalation was warranted to block the amazon.biz domain at the email gateway, notify h.harris, and provide phishing awareness training. Given two phishing campaigns observed within the same investigation window, a broader employee notification was also recommended.

---

### Scenario Completed

<img src="16-completed-scenario.png" width="800">

---

## Key Takeaways

- Pivoting between email logs and firewall logs is essential for phishing triage. The email log tells you what was sent, the firewall log tells you what the user did with it
- Internal corroborating emails are valuable evidence when determining false positives. The h.harris email confirming hrconnex.thm as a legitimate vendor immediately resolved alerts 1 and 2
- Typosquatting and lookalike domains are the most common phishing technique in this scenario. m1crosoftsupport.co and amazon.biz both rely on visual similarity to trusted brands
- URL shorteners like bit.ly are a red flag in email context because they hide the real destination from both users and email filters
- A blocked firewall connection does not mean no escalation is needed. The user still clicked the link and the email still bypassed controls, both of which require follow-up
- Multiple phishing attempts targeting the same organization in a short window suggests an active campaign and should trigger broader employee notification