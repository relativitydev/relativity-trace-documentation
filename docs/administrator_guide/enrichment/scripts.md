---
layout: default
title: Scripts
parent: Enrichment
grand_parent: Administrator Guide
nav_order: 2
---

# Scripts
{: .no_toc }


Relativity Scripts enable you to write and run SQL-based scripts to augment standard enrichment capabilities.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
More information on Relativity Scripts can be found [here](https://help.relativity.com/RelativityOne/Content/Relativity/Scripts.htm).

### Automate the Running of Scripts
Scripts can be automated through Actions. See [Actions]({{ site.baseurl }}{% link docs/administrator_guide/actions.md %}) page for more information.


### Custom Relativity Trace Scripts

Several useful Relativity Scripts are shipped by default with Trace application.

| **Script Name**       | **Description**                                              | **Inputs and Outputs**                                       |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Trace Date Parser     | This script parses system CreatedOn Date Time field into a Trace Day Of Week field and Trace Hour Of Day field | **INPUT:** Timezone<br>**INPUT:** Saved Search to execute on (passed from Rule)<br>**OUTPUT:** TraceHourOfDay Field Name<br>**OUTPUT:** TraceDayOfWeek Field Name <br><br>The SQL Query ```SELECT * FROM sys.time_zone_info``` will return all time zones available on the SQL Server. Use any of the Time zone names in the `Timezone` Input. |
| Trace AI Calculations | **Contact your support@relativity.com prior to using this script.**<br/>This script calculates Precision and Recall across all rank cutoffs for your Active Learning project you can better understand the accuracy and what rank cutoff you should be using in your Rules. | **INPUT:** Rank Field (This should be the CSR Rank field from the Active Learning Project)<br/>**INPUT:** Decision Field (A Yes/No field that denotes whether a document is a true positive)<br/>**OUTPUT:** A table calculating Precision and Recall for all Cutoff Ranks. |