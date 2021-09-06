---
layout: default
title: System Health
parent: Setup
grand_parent: Administrator Guide
nav_order: 3
---

# System Health
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---
Setup
=====

The `Setup` tab aggregates the most important information about configuration, health and overall status of Trace for a workspace. It shows the currently installed version,  active tasks and their configuration, and a snapshot of instance infrastructure that’s relevant to Trace. In addition, you can manage Logging configuration and run a built-in self-test (`BIST`) to verify basic flow.

![1571087647200](media/user_documentation/1571087647200.png)

If an update to a new version of Trace is in progress, the Setup page will show a large red bar indicating an Update is in progress:

![1571088232926](media/user_documentation/1571088232926.png)

System Health Reporting
------------------------

The Reporting task is designed to email designated administrators information regarding the health of the Trace system every 24 hours, to ensure they are aware of any outages or delays in processes. Email configurations for this task default to instance settings, but can be manually overridden from the Reporting task page. See below sample configuration for example.

![](media/23b1404cbe20203f82f17154a8685bf1.png)

-   **Recipients:** List of emails to send the report to, separated by
    semi-colons (;) (the token \<\<EMAIL_TO_INSTANCE_SETTING\>\> will be
    replaced with the configured email address in Instance Setting: “EmailTo”
    under “kCura.Notification” section)

-   **Include Details:** Flag to determine if you want to see the details in the
    email report (default: false)

-   **Frequency In Minutes:** How often should an email report be sent out
    (default: 24hrs)

-   **Email From:** Email address to send the report from (the token
    \<\<EMAIL_FROM_INSTANCE_SETTING\>\> will be replaced with the configured
    email address in Instance Setting: `EmailTo` under `kCura.Notification`
    section)

> **NOTE:** It is required to fill in the `kCura.Notification` instance settings
`SMTPUserName`, `SMTPPassword`, `SMTPServer`, `SMTPPort` and `SMTPSSLisRequired` with
details of a functioning email delivery system in order to receive important
notifications and alerts from Relativity and Trace.
![](media/f1d0a0d1fda68815093c96764927b0df.png)

