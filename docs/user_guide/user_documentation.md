---
layout: default
title: User Documentation
parent: User Guide
nav_order: 1
---

# User Documentation
{: .no_toc }


Best Info ever
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Introduction to Relativity Trace
================================

Relativity Trace is an application built on the Relativity platform for built for proactive communication surveillance workflows.

Relativity Trace is an [ADS Deployable Application](https://platform.relativity.com/9.5/Content/Building_Relativity_applications/Building_Relativity_applications.htm) containing [RDOs](https://platform.relativity.com/9.5/Content/Managing_Relativity_dynamic_objects/RDO_9.5/Relativity_objects.htm), Custom [Agents](https://help.relativity.com/9.5/Content/System_Guides/Agents_Guide/Agents.htm), [Event Handlers](https://help.relativity.com/9.5/Content/Relativity/Event_Handler_Express/Relativity_Event_Handler_Express.htm) and other relevant infrastructure.





























   


Reporting
=========

The `Trace`->`Reports` tab serves as a place for reporting capabilities. More reports will be added to this section in the future.

Trace Terms Report
------------------
![](media/316284f452e265e8db7521909b4c00b0.png)

The Trace Terms Report provides distinct counts on how many documents matched per Rule per Term. In other words, you can quickly see current state of your Rules and associated terms.

- **Document Date Field** - the date field used to determine if a document is in the specified date range for the report
- **Date Begin** - the beginning of the date range (at 12:00AM in the Time Zone used by the selected Date Field) to use for documents in the report
- **Date End** - the ending of the date range (until 11:59PM in the Time Zone used by the selected Date Field) to use for documents in the report

# Trace and Azure Information Protection

Trace Data Sources can be configured to decrypt documents that are protected by Azure Information Protection. The Azure Information Protection Instance must have specific configuration applied in order for Trace to decrypt and read AIP protected documents. 

This configuration requires the following access / permissions:

- Administrative access to the Azure Information Protection Instance
- Access to the Azure Portal with permissions to create Application Registrations

## Configuring Azure Information Protection Instance

#### Enable Unified Labeling

It is required that the Azure Information Protection Instance being used is backed by the unified labeling platform. To see if your instance is backed by the unified labeling platform or to migrate your label to the unified labeling platform, follow these instructions:  https://docs.microsoft.com/en-us/azure/information-protection/configure-policy-migrate-labels 

#### Configure Super User

In order for Trace to be able to read AIP protected documents, the Trace Data Source must be associated with a Super User in your AIP Service. The Super User can be either a real user account in your directory, or a service principal associated with an Azure Application Registration (service principal). You can enable Super Users and set permissions by following this guide :  https://docs.microsoft.com/en-us/azure/information-protection/configure-super-users.

#### Add an Application Registration for Super User

In order for Trace to interact with the Azure Information Protection API, you will need to create an Application Registration in the Azure Active Directory instance associated with your AIP instance. 

Please follow the documentation in authorization.md to create an application registration for AIP.

## Configuring Trace for Azure Information Protection

After finishing the configuration of the Azure Information Protection instance, you're ready to start configuring Trace for consuming AIP protected data. AIP is configured at the Data Source level. Please populate the required fields listed in authorization.md for your intended authorization grant.

Considerations
==============

Usability Considerations
------------------------


- Once a document is associated with a Rule, it will never be disassociated unless there are document updates to extracted text or metadata. The `Trace Document Retry` (mass operation) procedure will also reset the associations automatically.

-   Every Data Source has capability to be `Reset` via console buttons. Once a data source is reset,
    Trace will pull all available data again, beginning with the Start Date defined on the data source (if the Start Date is relevant to the data source type). **Depending on import profile settings, this could duplicate data in the Workspace.**
    
- Task processes (Indexing, Term Searching, Rule Evaluation, etc) run simultaneously (in parallel). It may take several task cycles (based on configured `Run Interval` for each task) for the end-to-end workflow to complete fully.

- Deleting a Trace Rule does not delete any of the corresponding Relativity infrastructure and objects that were created (i.e. dtSearch Index, Saved Searches, Batch Sets). 

- The global dtSearch index `Trace Search Index` (created by Trace application during installation) is supported for ad-hoc searching and will be incrementally built as part of Indexing task. All dtSearch indexes whose name begins with `Trace`, but not `TraceTemp` will incrementally build automatically.

> **NOTE:** `Trace Search Index` settings are propagated to all of Term Searching in Trace.  The index MUST be named exactly `Trace Search Index` in order to apply the settings correctly (noise words, alphabet, etc)!

## 	General Infrastructure and Environment Considerations

| **Tasks:**                       | **Ingestion**                                                                          | **Ingestion**      |    **Running Rules**                                                      |   **Running Rules**                                                                   |
|----------------------------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------------------------------------|
|                                  | **`Ingestion`, `Data Validation`, `Data Enrichment`, `Data Retrieval`, `Text Analysis`, and `Data Transformation`** | **`Indexing`**                                                                                                                                                                                        | **`Term Searching`**                                       | **`Rule Evaluation`**                                                  |
| Summary                          | Powers the Proactive Ingestion Framework                                               | Incrementally builds Trace Search Index and Temporary Search Indexes with batches of documents Optionally: Incrementally builds and runs Analytics Jobs (Conceptual, Classification and Structured) | Searches and tags Terms in workspace on an ongoing basis | Rule will run and tag all matching documents and perform actions     |
| Task Operations                  | *`Ingestion Task`*<br>-Looks for batches that need to be imported and kicks off import<br>-Creates RIP job per batch<br>*`Data Validation Task`*<br>-Updates Data Batch status<br>*`Data Retrieval Task`*<br>-Pulls data for enabled Data Sources <br>*`Data Enrichment Task`*<br>-extracts/expands/enriches source native document and prepares import load file (executed by `Trace Worker Agent`)<br/>*`Text Analysis Task`*<br>-performs any external text processing on data before ingestion task imports the data<br>*`Data Transformation`*<br>-performs data transformations on data batches before ingestion task imports the data<br> | *`Indexing Task`*<br>-Kicks off dtSearch incremental build<br>-Kicks off temporary (internal) dtSearch index builds for Term evaluation<br>-Kicks off Analytics Jobs (if configured)<br>**NOTE:** Run Interval controls frequency of temp indexes creation ONLY. Global dtSearch and Analytics Indexes are built every 60 minutes by default.                                                                                                                                                                                   | *`Term Searching Task`*<br>-Runs (searches and tags) Terms in the workspace<br>**NOTE:** Each Term Searching run interval will search up to 5 available document batches (default 10,000 documents per batch). These settings are configurable on Term Searching task.                                    | *`Rule Evaluation Task`*<br>-Evaluates each rule in the workspaces and triggers configured actions                                              |
| Recommended Run Interval         | `60` seconds                                                                             | `300` seconds                                                                                                                                                                                         | `300` seconds                                              | `300` seconds                                                          |
| Considerations and System Impact | -Speed of ingestion is determined by number of Integration Points Agents (max of 4 per instance) | -Ongoing index builds use shared instance queue, agents and Fileshare across multiple workspaces (resource pool)<br>-Every incremental build makes the old build obsolete - cleaned up by Case Manager nightly                                                                                  |                                                          | -Very complex/nested underlying Saved Searches can affect performance<br>-Saved Searches that return many documents can affect performance<br>-Many rules being evaluated often can put pressure on SQL server |

> **NOTE:** The Recommended Run Interval for the **`Reporting Task`** is 300 seconds.

Large Workspaces Infrastructure and Environment Considerations
---------------------------------------------

> **NOTE:** Use these additional recommendations to tune your environment for workspaces housing more than `10 Million` documents.


| Recommendation                                               | Explanation                                                  | Additional Notes                                             |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Separate dedicated infrastructure for `Web`, `Agent`, `SQL server` and Fileshare | Trace relies on Relativity infrastructure. In cases of shared resources (`Agent Servers`, `Fileshares`, `SQL queues`) it is recommended to dedicate separate infrastructure to limit effect on other workspaces within instance. | It is recommended to include these as a separate Resource Pool if deploying in existing environment |
| Limit Trace Task `Run Intervals` \>=`5 minutes` (300 seconds) | Each Task generates audits, SQL queries executions, creates tables, etc. and can put unnecessary pressure on the system when run too frequently | End-to-end workflow will require multiple Run Intervals for the cycle to complete |
| Limit maximum number of Rules: `50` per workspace, `500` per instance | The design of Rule Evaluation Task limits concurrent execution of multiple rules. This effect is compounded by running multiple workspaces with Rules concurrently. | Future iterations will remove this limitation                |
| Update dtSearch sub-index size to be `500K` OR `1M` (Advanced Settings) | Default sub-index size is `250K` docs, when you have more than `10` sub-indexes searches can become slow because of the number of sub-indexes<br>![1564672221173](media/1564672221173.png)<br><br>![1564672354757](media/1564672354757.png) | General rule is to keep number of sub-indexes under `10` total |
| Ensure [Data Grid for Audit](https://help.relativity.com/RelativityOne/Content/Relativity/Data_Grid/Data_Grid_for_Audit.htm) is setup OR use [Database Partitioning for Archiving Audit Records](https://community.relativity.com/s/contentdocument/06950000002JezyAAC) | Audits are generated frequently, outside of RelativityOne, they are stored in SQL which at scale creates very large tables.  It's best practice to set up table partitioning for your audits, or to deploy Data Grid solution | Data Grid for Audit is used natively in RelativityOne        |

Glossary
========

-   **Action:** a customized activity that happens when a rule is triggered

-   **Action Type:** different activities have different Action Types which can
    be customized into Actions that are associated with a Rule

-   **Agent:** process manager that runs in the background of Relativity to
    complete tasks

-   **Data Source:** setup and settings needed for a particular data source
    (e.g. Microsoft Exchange, Bloomberg, Office 365, Lync, etc.…)

-   **Data Batch:** a set of data (typically a load file) that is generated by a
    data processor as part of the Proactive Ingestion Framework

-   **Data Transformation:** an operation that can be performed on a Data Batch
    during Data Transformation task that alters the documents in some way
    (Deduplication or Replace) before being imported

-   **Monitored Individual:** a person of interest whose data is being ingested
    into Trace for monitoring

-   **Rule:** a preconfigured set of triggers that run on a regular basis and
    kick off actions

-   **Task:** an ongoing background process that is triggered by an agent

-   **Term:** search (dtSearch) condition that can be applied to Rule evaluation
    to further cull down results

Appendix A: Trace Object Architecture
=====================================

![](media/c961c7a2692a2b4f30a91566d902a2f6.png)

Appendix B: Trace Document Extraction Fields
============================================

Trace automatically extracts metadata information for Microsoft Office 365 Data Source and Relativity Data Extraction Data Source. Below is the list of all the supported fields. There are four major categories for fields:

-   `Email` Only – fields that apply to emails only

-   `Email` and `Document` – fields that apply to emails and other documents (Word,
    Excel, PowerPoint, etc...)

-   `Document` Only – fields that apply to documents but not to emails

-   `Calculated` – fields that are calculated dynamically by Trace

| **Trace Field Category** | **Relativity Field**          | **Field Type**    | **Field Description**                                        |
| ------------------------ | ----------------------------- | ----------------- | ------------------------------------------------------------ |
| Email Only               | Attachment List               | Long Text         | Attachment file names of all child items in a family group, delimited by semicolon, only present on parent items. |
| Email Only               | BCC                           | Long Text         | The name(s) (when available) and email address(es) of the Blind Carbon Copy recipient(s) of an email message. |
| Email Only               | Can Forward                   | Yes/No            | The indicator whether the mail message can be forwarded.     |
| Email Only               | CC                            | Long Text         | The name(s) (when available) and email address(es) of the Carbon Copy recipient(s) of an email message. |
| Email Only               | Conversation Index            | Long Text         | Email thread created by the email system. This is a 44-character string of numbers and letters that is created in the initial email and has 10 characters added for each reply or forward of an email. |
| Email Only               | Conversation                  | Long Text         | Normalized subject of email messages. This is the subject line of the email after removing the RE and FW that are added by the system when emails are forwarded or replied to. |
| Email Only               | Creator Email Entry ID        | Long Text         | The unique Identifier of creator an email in an email store  |
| Email Only               | Delivery Receipt Requested    | Yes/No            | The yes/no indicator of whether a delivery receipt was requested for an e-mail. |
| Email Only               | Email Categories              | Long Text         | Category(ies) assigned to an email message.                  |
| Email Only               | Email Created Date/Time       | Date              | The date and time at which an email was created (converted to UTC). |
| Email Only               | Email Format                  | Single Choice     | The indicator of whether an email is HTML, Rich Text, or Plain Text. |
| Email Only               | Email In Reply To ID          | Long Text         | The internal metadata value within an email for the reply to ID. |
| Email Only               | Email Last Modified Date/Time | Date              | Date and time that the email message last modified (converted to UTC). |
| Email Only               | Email Sensitivity             | Single Choice     | The indicator set on an email to denote the email's level of privacy. |
| Email Only               | From Address                  | Long Text         | The e-mail address for the messaging user represented by the sender. |
| Email Only               | From                          | Fixed-Length Text | The name (when available) and email address of the sender of an email message. |
| Email Only               | From                          | Date              | Date and time that the email message was sent (converted to UTC). |
| Email Only               | Importance                    | Single Choice     | Notation created for email messages to note a higher level of importance than other email messages added by the email originator. |
| Email Only               | Last Modifier Email Entry ID  | Long Text         | The unique Identifier of last modifier of an email in an mail store |
| Email Only               | Message Class                 | Single Choice     | A single choice field that can be one of: Email, Edoc, or Attach. |
| Email Only               | Message ID                    | Fixed-Length Text | The message number created by an email application and extracted from the email's metadata. |
| Email Only               | Priority                      | Single Choice     | The priority of the email message.                           |
| Email Only               | Read Receipt Requested        | Yes/No            | The yes/no indicator of whether a read receipt was requested for an e-mail. |
| Email Only               | Received By Email Entry ID    | Long Text         | The unique Identifier of an email in an mail store           |
| Email Only               | Received Date/Time            | Date              | Date and time that the email message was received (converted to UTC). |
| Email Only               | Sender Email Entry ID         | Long Text         | The unique Identifier of an email in an mail store           |
| Email Only               | Subject                       | Long Text         | Subject of the email message.                                |
| Email Only               | To                            | Long Text         | The name(s) (when available) and email address(es) of the recipient(s) of an email message. |
| Email and Document       | Author                        | Fixed-Length Text | Original composer of document or sender of email message.    |
| Email and Document       | Created Date/Time             | Date              | Date and time from the Date Created property extracted from the original file or email message (UTC). |
| Email and Document       | Extracted Text                | Long Text         | Complete text extracted from content of electronic files or OCR data field. This field holds the hidden comments of MS Office files. |
| Document Only            | Comments                      | Long Text         | Comments extracted from the metadata of the native file.     |
| Document Only            | Company                       | Fixed-Length Text | The internal value entered for the company associated with a Microsoft Office document. |
| Document Only            | Document Subject              | Long Text         | Subject of the document extracted from the properties of the native file. |
| Document Only            | Document Title                | Long Text         | The title of a non-email document. This is blank if there is no value available. |
| Document Only            | Keywords                      | Long Text         | The internal value entered for keywords associated with a Microsoft Office document. |
| Document Only            | Last Printed Date/Time        | Date              | Date and time that the document was last printed.            |
| Document Only            | Last Saved By                 | Fixed-Length Text | The internal value indicating the last user to save a document. |
| Document Only            | Last Saved Date/Time          | Date              | The internal value entered for the date and time at which a document was last saved. |
| Calculated               | Container ID                  | Fixed-Length Text | Unique identifier of the container file in which the document originated. This is used to identify or group files that came from the same container. |
| Calculated               | Container Name                | Fixed-Length Text | Name of the container file in which the document originated. |
| Calculated               | Control Number                | Fixed-Length Text | The identifier of the document.                              |
| Calculated               | Email Has Attachments         | Yes/No            | The yes/no indicator of whether an email has children (attachments). |
| Calculated               | Email Store Name              | Fixed-Length Text | Any email, contact, appointment, etc. that is extracted from an email container (PST, OST, NSF, MBOX, etc) will have this field populated with the name of that email container. |
| Calculated               | Extracted Text Size in KB     | Decimal           | Indicates the size of the extracted text field in kilobytes  |
| Calculated               | Group Identifier                  | Fixed-Length Text | Family Group the file belongs to (used to identify the group if attachment fields are not used). |
| Calculated               | File Extension                | Fixed-Length Text | The extension of the file, as assigned by the processing engine after it reads the header information from the original file |
| Calculated               | File Name                     | Fixed-Length Text | The original name of the file                                |
| Calculated               | File Size                     | Decimal           | **DO NOT MAP** this field in ingestion profile. A value for this field is automatically calculated by Relativity on import. |
| Calculated               | File Type                     | Fixed-Length Text | Description that represents the file type to the Windows Operating System |
| Calculated               | Native File                   | Long Text         | The path to a copy of a file for loading into Relativity.    |
| Calculated               | Number of Attachments         | Decimal           | Number of files attached to a parent document.               |
| Calculated               | Other Metadata                | Long Text         | Additional metadata extracted during processing beyond the list of standard fields available for mapping. See the "Read From Other Metadata Column" setting on Data Mappings to import values from Other Metdata to a field in Relativity. |
| Calculated               | Parent Document ID            | Fixed-Length Text | Document ID (Control Number) of the parent document. Empty for top level (original native) documents. For multiple levels of descendants, this field will always be populated with the Document ID (Control Number) of the top level (original native) document for every descendant document. |
| Calculated               | Password Protected            | Single Choice     | Indicates the documents that were password protected. It contains the value Decrypted if the password was identified, Encrypted if the password was not identified, or no value if the file was not password protected. |
| Calculated               | Recipient Count               | Decimal           | The total count of unique recipients in an email across the To, CC, and BCC fields |
| Calculated               | Trace Data Transformations    | Multiple Object   | Data Transformations that have been applied to the document  |
| Calculated               | Trace Document Hash           | Fixed-Length Text | Calculated hash value that is used to determine if a document is a duplicate of another document. Original documents use a partial hash of metadata, while extracted documents use a binary hash. |
| Calculated               | Trace Error Details           | Long Text         | Details of errors encountered during the extraction/expansion |
| Calculated               | Trace Has Errors              | Yes/No            | Indicates if any errors occurred during extraction/expansion |
| Calculated               | Trace Monitored Individuals   | Multiple Object   | Monitored individuals associated with Data Source (used for retrieval and billing) |
| Calculated               | Trace Exempt              | Yes/No            | Indicates exempt list data transformation classification |
| Calculated               | Trace Communication Direction           | Fixed-Length Text | Indicates communication direction data transformation classification (Internal |
| Calculated               | Trace Is Extracted           | Yes/No | Indicates whether a document is a Native or was Extracted |
| Calculated               | Trace Original Extracted Text           | Long Text | Holds the original content of extracted text file before any transforms or cleansing occur |
| Calculated               | Trace AI Extracted Text Cleansing Status           | Single Choice | Indicates the cleansing status of a document that has undergone AI Extracted Text Cleansing |
| Calculated               | Trace AI Extracted Text Cleansing Error Details | Long Text | Holds any error details that may have occurred during AI Extracted Text Cleansing |

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
