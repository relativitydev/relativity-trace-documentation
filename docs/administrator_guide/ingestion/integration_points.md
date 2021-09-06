---
layout: default
title: Integration Points
parent: Ingestion
grand_parent: Administrator Guide
nav_order: 2
---

# Integration Points
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

Trace Proactive Ingestion Framework
===================================

The Proactive Ingestion Framework allows Administrators to automatically and continually ingest data into Relativity from various Data Sources. The framework is built on top of [Relativity Integration Points](https://help.relativity.com/9.6/Content/Relativity_Integration_Points/RIP_9.6/Installing_Integration_Points.htm).

The key benefits of the Proactive Ingestion Framework include:

-   Data reconciliation from Data Source through transcription/normalization to Relativity
    
-   Data can be autonomously and continuously ingested

-   Data can be pushed from a 3rd party data processor in a generic format

-   Data is broken into batches improving stability and throughput

-   Data can be manually previewed to facilitate field mapping troubleshooting

-   Data can be re-imported into Relativity at any point (asynchronously from
    retrieval from the Data Source)

-   Data can be transformed by replacing redundant / irrelevant blocks of text or removing duplicate documents from consideration
    
-   Performance monitoring of entire data ingestion pipeline (bottleneck identification, SLA metrics, proactive alerting)

Reach out to <support@relativity.com> for help integrating with the Proactive
Ingestion Framework


Appendix C: Create Email Fields Data Mappings and Ingestion Profile
=============================================================

> **NOTE:** Make sure the Integration Points application is installed in this
Workspace before proceeding.

> **NOTE:** Trace uses default Relativity fields for email and attachment data that ship with `Create & Map Field Catalog – Full` (v0.0.1.5+). **Trace recommends use of this application, however it is totally optional and one can choose to create custom fields or re-use fields from an existing template.** You can install it to the target workspace like any other application which will bring in all
the needed fields with standardized names. If you don’t see this application in
your library, reach out to `support@relativity.com`.
![](media/045f66f33011aa62ff7d00b2e05274c2.png)

## Setup Ingestion Profile

**Warning:** Ingestion Profiles are susceptible to corruption by modification of Relativity Fields and Data Mappings which are referenced in the profile.  Any time a Relativity Field or Data Mapping which is used in an Ingestion Profile is edited or deleted, it is imperative to validate the integrity of each of the related Ingestion Profiles. Automatic validation occurs during the Data Retrieval task and may cause a data source to be automatically disabled if it is found to have been corrupted.

1. Go to the Trace: Ingestion Profile tab
2. Click “New Ingestion Profile”
3. Enter a name for the Profile “Email Fields Map Profile”
4. Fill in preferred Workspace Destination Folder
5. Most advanced settings can be left as their default values
   1. Column Containing File Location - Create or select a data mapping with Source Field Identifier "Extracted Text" mapped to a long text Relativity Field and a type of "None"
   2. Native File Path Location - Create or select a data mapping with Source Field Identifier "Native File Path" and type of "Native File Path". This data mapping is not required to have a destination field in Relativity, but may have one if you so choose.
6. Click "Save"
7. On the layout for your new Ingestion Profile, add/link required Data Mappings
   1.  Add/Link a data mapping of type Identifier (the Relativity Field will likely be Control Number)
   2. Add/Link a data mapping of type Native File Path (the same data mapping you set in the 'Advanced Settings' section)
   3. If you specified a data mapping for Column Containing File Location, make sure to add it to the list of data mappings as well.
   4. Add/Link data mappings for any other unmapped fields in the loadfile to the appropriate. It is not required to map every field.
         For any missing fields in your Workspace, create them in the Workspace
         Administration: Fields Tab. See [Appendix B: Load File Fields for Emails and Attachments](#appendix-b-trace-document-extraction-fields) for a list and associated definition for all Trace
         fields.

> **NOTE:** You can edit the Ingestion Profile settings at any time, however existing completed Data Batches will not automatically re-import the data with new settings/mappings.
