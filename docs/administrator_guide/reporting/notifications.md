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

### JSON Configuration
Supported Reports Types: NonAlertedDocumentReviewReport & SystemHealthAlertsReport

Each Report Accepts
- Enabled - a true/false value. Technically deleting the entry from the json will also disable, but to preserve expected settings the preferred method to stop a report is to set this value to false
- Recipients - a semi-colon-separated list of email addresses to send this report to, or <<EMAIL_TO_INSTANCE_SETTING>> to override with the EmailTo Relativity Instance setting
- FrequencyInMinutes - how often the report should run, i.e. 15 for every 15 minutes
- EmailFrom - email address the report should come from, or <<EMAIL_FROM_INSTANCE_SETTING>>  to override with the EmailFrom Relativity Instance setting
- IncludeDetails - a true/false value which is used by some reports to provide extra detail. Currently only used by the SystemHealthAlertsReport to provide extra details on the error each Task encountered

#### Example JSON Configuration

```
{"NonAlertedDocumentReviewReport":{"Enabled":true,"Recipients":"user@domain.com","FrequencyInMinutes":1440,"EmailFrom":"noreply@relativity.one"},
"RuleChangeReport": {"Enabled":true,"Recipients":"user@domain.com","FrequencyInMinutes":1440,"EmailFrom":"noreply@relativity.one"}, "SystemHealthReport": {"Enabled":true,"Recipients":"user@domain.com","FrequencyInMinutes":1440,"EmailFrom":"noreply@relativity.one"}}
```

#### Example JSON Configuration with All Reports
![](media/notifications/Updated Configuration.PNG)

- If there is nothing to report an email will not be sent, but an Automated Report object will still be created within the product
- The Non-Alerted Document Review Report only analyzes events that occured the previous day, and cannot gather historical results
- To see what the report looks like in Trace, see the [User Guide](docs/user_guide/reporting/)
{: .info}
