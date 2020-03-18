# Relativity Trace Proactive Ingestion Framework Documentation

- [Overview](#overview)
- [Glossary](#glossary)
- [Prerequisites: Load File and Integration Point Profile](#prerequisites-load-file-and-integration-point-profile)
- [Data Batch Overview](#data-batch-overview)
- [API Usage](#api-usage)
- [Data Batch creation (Quick Start)](#data-batch-creation-quick-start)
  * [Data Batch Statuses](#data-batch-statuses)
  * [Create Data Batch](#create-data-batch)
  * [Update Data Batch](#update-data-batch)
- [Workflow Recommendations](#workflow-recommendations)
  * [Security](#security)
  * [Load File Specifications](#load-file-specifications)
    + [Text Fields](#text-fields)
  * [Field Mappings stored in Relativity Integration Point Profile](#field-mappings-stored-in-relativity-integration-point-profile)
  * [Data Batches](#data-batches)
  * [Error Handling](#error-handling)

Overview
========

The Trace Proactive Ingestion Framework allows Administrators and Data Sources to automatically and continuously ingest data into Relativity. The framework is built on top of [Relativity Integration Points](https://help.relativity.com/9.6/Content/Relativity_Integration_Points/RIP_9.6/Installing_Integration_Points.htm).

The key benefits of the Proactive Ingestion Framework include:

-   Reconciliation from Data Source through Transcription/Normalization to
    Relativity

-   Data can be autonomously and continuously ingested

-   Data can be pushed from a 3rd party data processor in a generic format
    (instead of pulled from Relativity with custom connectors)

-   Data is broken into batches improving stability and throughput

-   Data can be manually previewed to facilitate field mapping troubleshooting

-   Data can be re-imported into Relativity at any point (asynchronously from
    retrieval from the Data Source)

-   Performance monitoring of entire data ingestion pipeline (bottleneck
    identification, SLA metrics, proactive alerting)

It is designed to work with Load Files as an intermediate step between Source and Relativity ingestion. Consumer of the IPI needs to produce a Load File and make an REST call to Relativity telling it the location of the Load File along with other ingestion configurations. After that, Trace will take the Load File and automatically import it using the provided configurations.

Glossary
========

-   **Data Batch:** RDO that contains all needed information about Load File and
    its ingestion status

-   **Load File:** Delimited data file on disk, usually CSV or DAT but can be
    anything with proper delimiters

-   **Integration Point:** System that executes data ingestion into Relativity, operated by Trace. Trace creates one integration point per Data Batch and monitors its status along with any retries and validation
    
-   **Data Source:** Any external system that works with Trace API. It is responsible for generating Load Files and creation of Data Batches
    
-   **Data Source Type:** Defines inputs to a particular data source. Data Source Type can be mapped to multiple Data Sources
    
-   **IPI:** Trace Proactive Ingestion

Prerequisites: Load File and Integration Point Profile
======================================================

1.  Install “Trace” application

2.  Install “Integration Points” application

3.  Generate sample Load File with all the needed fields

4.  Create Integration Point profile

    1.  Type: Import

    2.  Source: Load File

    3.  Reference sample load file location

    4.  Map Load File fields to Relativity fields

    5.  Adjust other settings (encoding, native file path field, etc.)

>   See the below screenshots to create an Integration Points Profile:

![](media/e24572c72556487f6e2f628f1299a60f.png)

![](media/a04bf444c81840c63e8506ddf9c4375d.png)

![](media/f49ffa92f4f23a13a8d2dbae9a21b2a8.png)

1.  Create Trace Data Source

    1.  Name: Data Source name that will be reference by Data Batches

    2.  Integration Point Profile Name: name of profile created in step 4

    3.  Username / Password: not required. Can be used to store credentials via
        Secret Store

    4.  Enabled: used to signal stop or start of the data source ingestion from
        external source

Data Batch Overview
===================

Data Batch is a unit of work in IPI, it has all the needed configuration and  status information to ingest data and monitor ingestion progress.

The below screenshot shows a sample Data Batch RDO in Relativity:

![](media/240abcbc64be3bc9404c200a39a343f5.png)

When a Data Source creates a Data Batch, several fields must be filled out:

1. Status

   1.  `ReadyForImport` signals Trace to start ingesting the data
       1.  All needed configuration is written on the Data Batch
           
       2.  Load File has been successfully copied to Relativity Fileshare
   
   2.  `Created`, `RetrievedFromSource` and `Normalized` can be used to track data flow in Relativity for reconciliation purposes by the Data Source
       
   3.  `Importing`, `Completed`, `CompletedWithErrors`, and `CompletedWithDocumentLevelErrors` statuses are populated by Trace automatically for ingestion tracking purposes

   4.  For each Status, Data Source can specify document count and time stamp (optional)

   ![](media/4a1b9ec9b71e8a2e1d07c4e901f2e867.png)

3.  Data Source

    1.  Specify Data Source of the Data Batch
        1.  ![](media/db43a876e56f862c4b2587b563f8e83a.png)
    2.  Load File Path
        1.  Specify path to the relativity location of the load file
            1.  ![](media/8770cf000865b61b94dc24002b7d49e5.png)

API Usage
=========

Working with TPI involves several steps in a base workflow:

1.  Create Load File with data in a Fileshare accessible by Relativity

2.  Create Data Batch RDO in Relativity

    1.  Status set to `ReadyforImport`

    2.  Data Source Selected to *Office 365 Email*

    3.  Load File Path filled
        `DataTransfer\Import\Office365Emails\20180511200815UTC-20180511210839UTC\loadfile.dat`

On next Ingestion task check-in Trace will automatically ingest the data by creating an Integration Point and will validate the import was successful.

Data Batch creation (Quick Start)
=================================

Since Data Batch is an RDO, standard Relativity API can be used to manage it. Sample below shows how to create Data Batches with Relativity REST (generic API). One can prototype with Relativity REST without  having to write any code. We recommend tools such as [Fiddler](https://www.telerik.com/fiddler) to prototype sample calls ahead of creating full solutions in code.

Data Batch Statuses
-------------------

Below status identifiers are needed to set a Data Batch to a particular stage of
processing. The identifiers are the same across all versions of Relativity and Trace application.

-   `29D19E38-8096-4A63-9496-F6E02D40FBFF` - GUID identifier for `Created` status

-   `5932D23F-697B-4950-AE55-1E38AFDD4D2C` - GUID identifier for `RetrievedFromSource` status
    
-   `B4680628-67EE-47F7-813C-51DEA69CB19A` - GUID identifier for `Normalized` status
    
-   `32452D3D-35D2-4FF5-92E6-1DD01D755482` – GUID identifier for `ReadyForImport` status
    
-   `68FCCFB2-6CE4-442C-A402-26A76E37A961` – GUID identifier for `Abandoned` status

Create Data Batch
-----------------

Below **sample request** will create a Data Batch associated with Load File
`DataTransfer\Import\Office365Email\20180511200815UTC-20180511210839UTC\loadfile.dat`

```json
POST https://REPLACE_WITH_RELATIVITY_ROOT/Relativity.REST/api/Relativity.REST/workspace/1017899/Data%20Batch HTTP/1.1
X-CSRF-Header:
Authorization: Basic ZGVtby51c2VyQHJlbGF0aXZpdHkuY29tOmRlbW9Vc2VyUGFzc3dvcmQ=
X-Kepler-Version: 2.0
Content-Type: application/json; charset=utf-8
Host: REPLACE_WITH_RELATIVITY_ROOT
Content-Length: 252
Expect: 100-continue

{
  "Name": "Test Data Batch",
  "Status": {
    "Guids": [
      "29D19E38-8096-4A63-9496-F6E02D40FBFF"
    ],
    "Artifact Type Name": "Choice"
  },
  "Load File Path": "DataTransfer\Import\Office365Email\20180511200815UTC-20180511210839UTC\loadfile.dat",
  "Data Source": {
    "Artifact ID": 3453563
  },
  "Parent Artifact": {
    "Artifact ID": 1003663
  },
  "RetryCount": 0,
  "Artifact Type Name": "Data Batch"
}
```

`1017899` – workspace ID

`ZGVtby51c2VyQHJlbGF0aXZpdHkuY29tOmRlbW9Vc2VyUGFzc3dvcmQ=` - base64 encoded *username:password* format

`29D19E38-8096-4A63-9496-F6E02D40FBFF` – GUID identifier for `Created` status

Above request must be executed using Fiddler, for example:

![](media/94b9bc1537ab80a8592c157df514b711.png)

Update Data Batch
-----------------

Below **sample requests** will update a Data Batch associated with Load File
`DataTransfer\Import\Office365Email\20180511200815UTC-20180511210839UTC\loadfile.dat` to `ReadyForImport` status

```json
PUT
https://REPLACE_WITH_RELATIVITY_ROOT/Relativity.REST/api/Relativity.REST/workspace/1017899/Data%20Batch/1017877 HTTP/1.1
X-CSRF-Header:
Authorization: Basic
ZGVtby51c2VyQHJlbGF0aXZpdHkuY29tOmRlbW9Vc2VyUGFzc3dvcmQ=
X-Kepler-Version: 2.0
Content-Type: application/json; charset=utf-8
Host: REPLACE_WITH_RELATIVITY_ROOT
Content-Length: 252
Expect: 100-continue

{
  "Status": {
    "Guids": [
      "32452D3D-35D2-4FF5-92E6-1DD01D755482"
    ],
    "Artifact Type Name": "Choice"
  },
  "DocumentCount_LoadFileGenerated": "500",
  "Timestamp_LoadFileGenerated": "3\/27\/2018 4:15:13 PM",
  "Parent Artifact": {
    "Artifact ID": 1003663
  },
  "Artifact Type Name": "Data Batch",
  "Artifact ID": 1017877
}
```

`1017899` – Workspace ID

`1017877` - Artifact ID of `Test Data Batch` create in the previous section

`ZGVtby51c2VyQHJlbGF0aXZpdHkuY29tOmRlbW9Vc2VyUGFzc3dvcmQ=` - base64 encoded username:password

`DataTransfer\Import\Office365Email\20180511200815UTC-20180511210839UTC\loadfile.dat` - load file location

`32452D3D-35D2-4FF5-92E6-1DD01D755482` – GUID identifier for `ReadyForImport` status

Above request must be executed using Fiddler, for example:

![](media/94b9bc1537ab80a8592c157df514b711.png)

After Data Batch is created or updated, it can be monitored in Relativity UI (or programmatically via identifier returned from Create API request)

![](media/409d8a386254a37e507eebd8042cf8cb.png)

![](media/661127765a65e979f55dd2574b10c603.png)

![](media/7c0804895ff95708ca6a5553e44277cf.png)

Workflow Recommendations
========================

Security
--------

In order to work with IPI in a secure manner, create a new user with limited permissions: enable access only to Relativity objects that are needed: Data Batch, Data Source and particular fields ( `Trace Has Errors` and `Trace Error Details` ) on a Document object.

Load File Specifications
------------------------

Full list of specifications:
<https://help.relativity.com/9.6/Content/Relativity/Relativity_Desktop_Client/Importing/Load_file_specifications.htm>

Recommended approach to generate **Load Files (.dat)** with the following specs:

| Value        | Character | ASCII Number | Notes                                    |
|--------------|-----------|--------------|------------------------------------------|
| Column       |           | 020          | Must replace this character in your data |
| Quote        | þ         | 254          | Must replace this character in your data |
| Newline      |           | 013 + 010    | Carriage Return + Line Feed Character    |
| Multi-Value  | ;         | 059          |                                          |
| Nested Value | \\        | 092          |                                          |

### Text Fields

All text fields in the load file must avoid special characters mentioned above. They are reserved as delimiters and will produce non-ingestible data. Those characters must be explicitly replaced. **Recommended approach is to replace Column (ASCII 020) and Quote (ASCII 254) characters with a space.** C\# sample below illustrates one way to replace special characters:

![](media/1a153ec4bda6645da5bbf95a89d8679a.png)

Field Mappings stored in Relativity Integration Point Profile
-------------------------------------------------------------

The following fields **must** be part of the Load File and must be mapped to appropriate Relativity fields:

**Required (absolute musts):**

1. `Object Type Identifier` - this is usually called a `Control Number`

2. `Trace Monitored Individuals` – list of monitored people associated with each record

3. `Trace Document Hash` - uniquely identifies a particular record. This will be used by Trace for [de-deduplication purposes](https://relativitydev.github.io/relativity-trace-documentation/user_documentation#deduplication-data-transformation)

   1. > **IMPORTANT:** column name in the load file must be called `Trace Document Hash`

4. `Trace Has Errors` – true/false. True, if particular document has errors
   (e.g. audio file too big to transcribe, etc…)
   
5. `Trace Error Details` – details of the individual item’s error (stack trace,
   retry information, etc)
   
6. `Trace Data Transformations` - must be set to empty string. This ensures that any Data Transformations tags are cleared.

7. `Relativity Attachment ID` - must be set to empty string  and mapped to `Relativity Attachment ID` field in Relativity. This field is needed for RSMF content.

8. `Group Identifier` - this must be mapped to a field that is responsible for grouping multiple items together (e.x. email thread id that groups all emails on the email chain together)

   1. >  **IMPORTANT:** column name in the load file must be called `Group Identifier`

**Recommended:**

1. `Trace Data Batch` – name of the batch
2. `Trace Checkout` – must be set to empty string. This ensures Trace can
   restart indexing and term searching for particular item in case of changes
   to an existing document (overlay scenario)
3. `Trace Rules` – must be set to empty string. This ensures that any Rule tags
   are cleared.
4. `Trace Rule Terms` – must be set to empty string. This ensures that any Rule Terms tags
   are cleared.
5. `Trace Terms` - must be set to empty string. This ensures that any Term tags
   are cleared.
6. `Trace Record Origin Identifier` - this should be an id of a record from it's data origin system. Once included, Trace will track this value across all Trace actions on a particular record. This helps to reconstruct audit trail for a particular record.

![](media/7beaeffb89e2aef4285696f44c7ff423.png)

Data Batches
------------

Recommended workflow for Data Batch creation ( `Created` -\> `RetrievedFromSource` -\> `Normalized` -\> `ReadyForImport` ):

1.  Create Data Batch with Status `Created` before starting data retrieval process
    
2.  Update Data Batch status to `RetrievedFromSource` when data is retrieved

3.  If data needs to be enriched or transformed, update Data Batch status to `Normalized`
    
4.  Once Load File is created, update Data Batch status to `ReadyForImport`. Include Import Configuration details. At this point Trace will pick it up and ingest the data into Relativity.

At any stage, you can use Metadata field on the Data Batch to capture information regarding the batch of documents as you go through the process.

Error Handling
--------------

1.  For item-level errors, always populate the following two fields

    1.  `Trace Has Errors` – true/false. True, if particular document has errors (e.g. audio file too big to transcribe, etc…)
    
2.  `Trace Error Details` – details of the individual item’s error (stack trace, retry information, etc)
    
2.  For batch-level error (e.g. connection failure to retrieve the data, etc...), update status of `Created` batch to `Abandoned` and populate batch `Error Details` with appropriate error.
