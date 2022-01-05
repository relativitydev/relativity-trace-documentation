---
layout: default
title: Notifications
parent: Reporting
grand_parent: Administrator Guide
nav_order: 1
---

# Notifications
{: .no_toc }


Trace offers predifined notification reports for complete defensibility and reporting.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Monitor Your Surveillance Team
Trace has functionality that allows companies to better detect risk by monitoring actions taken by their surveillance team. Now companies can track if surveillance team members have viewed documents that should not have been viewed. Trace will send an email report or real-time notifications regarding privacy issues where reviewers are looking at non-alerted documents. 

The following is how to enable the feature

1. Go to *Setup Tab*
2. Click *Reporting Tasks* ![](media/notifications/Non-Alerted Doc Reports Tab in Setup.png)
3. Reporting Type Configuration set to enabled and enter the recipients in the json ![](media/notifications/Non-Alerted Doc Configuration.png)

### JSON Configuration Notes
Supported Reports Types: NonAlertedDocumentReviewReport & SystemHealthAlertsReport

Each Report Accepts
- Enabled - a true/false value. Technically deleting the entry from the json will also disable, but to preserve expected settings the preferred method to stop a report is to set this value to false
- Recipients - a semi-colon-separated list of email addresses to send this report to, or <<EMAIL_TO_INSTANCE_SETTING>> to override with the EmailTo Relativity Instance setting
- FrequencyInMinutes - how often the report should run, i.e. 15 for every 15 minutes
- EmailFrom - email address the report should come from, or <<EMAIL_FROM_INSTANCE_SETTING>>  to override with the EmailFrom Relativity Instance setting
- IncludeDetails - a true/false value which is used by some reports to provide extra detail. Currently only used by the SystemHealthAlertsReport to provide extra details on the error each Task encountered

**General Notes:** If there are no incidents, the email will be sent but not have content
{: .info}

**General Notes:** This feature only reviews the previous 24 hours, not historical data. This adds improtance for having the reporting tasks up for each client
{: .info}

**General Notes:** Ensure retention in audits is at least 24 hours for this feature to work
{: .info}
