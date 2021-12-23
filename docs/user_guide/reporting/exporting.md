---
layout: default
title: Exporting
parent: Reporting
grand_parent: User Guide
nav_order: 3
---

# Exporting
{: .no_toc }

Any piece of data can be manually or automatically exported from Relativity Trace for stakeholder reporting, internal audits, or regulatory reporting.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---
## Overview
Exporting can be helpful to produce data for an audit or regulator, or for specific stakeholder reporting in business intelligence systems like PowerBI, Tableau, or Qlik.

## Ad-Hoc Exporting
Data can be exported directly from a [View]({{ site.baseurl }}{% link docs/user_guide/review/views.md %}) using the [Mass Export to File](https://help.relativity.com/RelativityOne/Content/Relativity/Mass_operations/Mass_export_to_file.htm) mass action. This can be a quick way to export everything from metadata to raw native files. 

## Relativity Integration Points Exporting
Relativity Integration Points can be used to export defined sets of document data including native files. More information on Relativity Integration Points can be found [here](https://help.relativity.com/RelativityOne/Content/Relativity/Relativity_Integration_Points/Exporting_data_through_Integration_Points.htm).

## Script Exporting
The `Trace`->`Reports` tab serves as a place for exporting specific SQL data.

### Terms Report
![](media/exporting/316284f452e265e8db7521909b4c00b0.png)

The Trace Terms Report provides distinct counts on how many documents matched per Rule per Term. In other words, you can quickly see current state of your Rules and associated terms.

- **Document Date Field** - the date field used to determine if a document is in the specified date range for the report
- **Date Begin** - the beginning of the date range (at 12:00AM in the Time Zone used by the selected Date Field) to use for documents in the report
- **Date End** - the ending of the date range (until 11:59PM in the Time Zone used by the selected Date Field) to use for documents in the report

## Automated Exporting
Data can be exported programatically using a robust set of open API's. For more information see [Extensible API's]({{ site.baseurl }}{% link docs/administrator_guide/proactive_ingestion_api_documentation.md %})


