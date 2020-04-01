# Relativity Trace Release Notes

- [12.1.0 (30 March 2020)](#1210-30-march-2020)
- [12.0.8.2 (24 February 2020) - DEPRECATED](#12082-24-february-2020---deprecated)
- [12.0.5.2 (24 October 2019) - DEPRECATED](#12052-24-october-2019---deprecated)
- [11.2.11.1 (13 September 2019) - DEPRECATED](#112111-13-september-2019---deprecated)
- [11.2.10.1 (12 August 2019) - DEPRECATED](#112101-12-august-2019---deprecated)
- [11.2.9.2 (15 July 2019) - DEPRECATED](#11292-15-july-2019---deprecated)
- [11.2.6.1 (17 June 2019) - DEPRECATED](#11261-17-june-2019---deprecated)
- [11.2.4.4 (10 June 2019) - DEPRECATED](#11244-10-june-2019---deprecated)

# 12.1.0 (30 March 2020)

**Relativity Compatibility**

- \> 9.6.202.10

**Features**

- Trace Shipper completes the Globanet connector use case as a way to move files from customer network servers to RelativityOne file shares (BETA)
- Added the ability to link a Term to a Rule on the Term layout page

**Enhancements**

- Added support for parsing rare date formats from email headers and PDF files
- Improved error messaging when a configured Monitored Individual has no mailbox or the mailbox is inaccessible
- Improved error messaging when an index build fails

**Defect Fixes**

- Relativity Native Data Source no longer overwrites the Trace Document Hash values provided during ingestion by external data sources
- Rules no longer execute in parallel to alleviate SQL database contention and inconsistent execution order
- Fixed an issue where data batches could not always be retried if deduplication had been performed on them
- Fixed an issue for non-US customers where automated analytics index builds were not always kicked off at the correct times
- Improved the data disposal action to be more thorough about removing files from the file share in error scenarios
- Fixed an issue where documents could not be tagged with monitored individuals by deduplication if more than 1000 monitored individuals were being tagged at once
- Fixed an issue where the file size field was erroneously being populated with the extracted text size

**Deprecated**

- The "Term Category" object type is no longer associated with or used by the Trace application (schema for the object type and all data will remain in existing Trace workspaces, nothing will be deleted)
- Removed support for the undocumented File Share data source type

**Upgrade Considerations**

- Update an existing Term view or create a new one if you would like to display the now orphaned "Term Category" field

# 12.0.8.2 (24 February 2020) - DEPRECATED

**Relativity Compatibility**

- \> 9.6.202.10

**Features**

- Azure Information Protection support (PREVIEW)
- Trace now supports automated builds for multiple Structured Analytics Sets at the same time in the same workspace
- Monitored Individuals can now be defined with a list of Secondary Identifiers that will also map to the Monitored Individual
- Monitored Individual Auto-Discovery is now available for Relativity Short Message Format (RSMF) documents
- Improved billing flow for customers that cannot support Telemetry
- Relativity Trace now supports RabbitMQ and Azure Service Bus messaging infrastructure

**Enhancements**

- Trace now removes all but the most relevant email headers from extracted text
- Data Batches now show a CompletedWithDocumentLevelErrors status if there are document-level errors in the Data Batch
- Renamed Data Archive action to Data Disposal and drastically improved its scalability and reliability
- Trace Term Report now works with System date fields and shows only fields that will work with the report
- Improved parsing of international dates in email headers in many formats
- Trace will now provide a unique value for the Group Identifier field in external data sources if the value given is too long
- The Terms list on the Rule layout is now sorted by Error Status and Name
- Trace Document Retry is no longer supported if Run Option is not set to Continuous
- Can now configure Documents tab to display the Data Source associated with every document
- Globanet data sources now read monitored individual from custom email header
- Monitored Individual Discovery can now ignore the casing of the email addresses in question
- Data Batches now show a Completed With Errors status if there are document-level errors in the Data Batch
- Implemented TraceRecordOriginIdentifier to allow document reconciliation for more data sources
- Errors on Rule Evaluation task now show the associated rule name
- Custom data batches no longer require specific column names in load file
- Audit messages resulting from actions taken by a user in the Relativity Trace UI now reflect the users ID

**Defect Fixes**

- Fixed an issue where Parent Document ID field was not populated with Control Number of parent document
- Restructured how Trace creates Relativity Integration Points to support latest Relativity One release
- Trace is now more careful about creating too many Integration Points in scenarios where the Integration Point Workers are backed up
- Fixed an issue where Trace Logs and Update Trace Log Level scripts would fail in certain Workspaces (Incorrect Syntax error)
- Fixed some billing issues with Instance Name and Data Source Type
- Fixed an issue where Monitored Individuals could not be edited
- Fixed an issue where a malformed TraceWorkspaceSettings instance setting would cause errors across the application
- Fixed an issue where certain characters were not supported in Password Bank
- Fixed an issue where Data Transformations field gets populated with extra delimiters in the load file after replacement transformations
- Fixed an issue where an incorrect popup warning would show when saving a Rule with no Associated Actions
- Fixed a rare issue where files could be copied incorrectly when generating Data Batches
- Fixed an issue where Deduplication would fail if it was necessary to remove more than 1000 duplicate documents from a single data batch
- Fix issue where Relativity Scripts used with Advanced Action Type require unused parameters
- Fix issue with failing Data Batches that were created via API
- Workspaces must be configured for Globanet before Globanet data sources can be used
- Data Batches are now marked Abandoned or Completed With Errors (depending on whether data is present) if they spend more than the configured time sitting in a non-completed status
- Fix issue where Trace Manager Agent crashes when experiencing temporary connectivity issues with Secret Store
- Fix issue where TraceWorkspaceSettings instance setting could not be edited
- Fix issue where Agent Statuses were reported incorrectly on Setup page in Relativity Instances with multiple resource pools
- Fix issue where Data Batch retry did not work properly if Data Transformations were used on the Data Source
- Fix issue where Trace Manager Agent could crash if a Trace task timed out in the right conditions

**Deprecated**

- N/A

**Upgrade Considerations**

- None, if upgrading from a currently supported release

# 12.0.5.2 (24 October 2019) - DEPRECATED

**Relativity Compatibility**

- \> 9.6.202.10

**Features**

- New Data Enrichment Task performs data extraction independently of data retrieval, allows for better throughput and scalability of data ingestion pipeline
- Trace Agents (Manager and Worker) now fully support resource pools which allows to designate multiple agent servers to scale out Trace workflow as needed

**Enhancements**

- Rule Type field can now be specified per rule. This allows to tag different MO field depending on rule configuration. Workflow rule configuration are used to drive workflow within the Relativity workspace
  Alert rule configuration is used for standard e-com/a-com identification
- Eliminated redundant query/read audits generated by Trace operations which reduces pressure on SQL server and audit infrastructure
- All actions associated with any rule now operate on net new data that is reflected on dedicated saved search
  - RelativityScript (advanced) action now operates on the same saved search, yielding incremental data only
- Conceptual and Classification index automation now takes into account any in-progress activities that lock the index resulting in better robustness
- dtSearch indexes will now perform Full Build automatically (no user interaction) on newly created indexes that are subject to automation
- Data Transformation failures on set of docs (in data batch) now reports detailed per document failures and allows for partial import of successful transformations
- Application installation time is now significantly faster, per workspace upgrade logic now is done by the Trace Manager agent
- BIST testing coverage is now expanded to include:
  - Explicit tests of successful Data Retention action execution
  - Monitored Individual auto-discovery propagation
  - Ingestion flow via Integration Points (as production)
- Monitored Individuals can now take advantage of Secondary Identifier to accommodate variable identifiers across multiple data sources (see documentation)

**Defect Fixes**

- Long text truncation of ingestion state for data sources with large number of Monitored Individuals when updating via UI
- Continuous BIST execution no longer generates orphaned resources and now correctly notifies of errors via Reporting task
- BIST import dependencies were updated to be compatible with RelOne Goatsbeard (10.3+) release
- Monitored Individual Auto-discovery no longer breaks the whole data batch on failures and reports errors on all extracted documents. Additionally, discovered monitored individuals are now properly associated with all documents that were extracted (including sub-attachments)

**Deprecated**

- Tag Action is now explicitly done as part of every rule evaluation and is not available in UI

**Upgrade Considerations**

- This is a **major** version change of Relativity Trace.

# 11.2.11.1 (13 September 2019) - DEPRECATED

> **DEPRECATION NOTE:** This version of Trace is **no longer supported**

**Relativity Compatibility**

- \> 9.6.202.10

**Defect Fixes**

- Fixed an issue where Email action was automatically adding trace@relativity.com to recipient list


# 11.2.10.1 (12 August 2019) - DEPRECATED

> **DEPRECATION NOTE:** This version of Trace is **no longer supported**

**Relativity Compatibility**

- \> 9.6.202.10

**Defect Fixes**

- Fixed an issue where under certain failures of Data Retrieval task, Globanet based data sources would delete retrieved data without extracting it

# 11.2.9.2 (15 July 2019) - DEPRECATED

> **DEPRECATION NOTE:** This version of Trace is **no longer supported**

**Relativity Compatibility**

- \> 9.6.202.10

**Features**

- BIST auto-run automation
- In production, you can dedicate a workspace for continuous integration
  testing and enable automatic execution of tests ensuring the infrastructure
  is in good shape
- Configuration of tasks, actions, data sources and data transformations is
  now entered and validated within text fields (instead of JSON) using the
  custom fields UI

**Enhancements**

- BIST now includes additional coverage and verification
- Reporting task and Email (alert) action now utilize kCura.Notification
  encrypted instance settings for email (SMTP) configuration
- Data Sources now report data retrieval errors directly on the Data Source
  object and no longer generate data batches with errors, reducing the number
  of failed data batches and the amount of manual resolution required
- Various performance optimizations for workspaces containing a large number
  of documents
- Additional metrics surrounding data retrieval and extraction processes are
  now added as part of Telemetry reporting
- Data Extraction can now discover monitored individuals within emails if they
  are not specified in the load file(s) generated by the Data Source
- Configuration of monitored individuals for Globanet data sources is now
  streamlined via CSV file

**Defect Fixes**

- Fixed an issue where .NET thread count (resource usage) would climb if
  Microsoft Exchange Data Source was misconfigured
- Embedded attachments inside of MS Office files and other containers are now
  correctly extracted
- Addressed feedback from security penetration testing

**Deprecated**

- Microsoft Office 365 data source (based on GraphAPI) is deprecated, use
  Microsoft Exchange data source instead

**Upgrade Considerations**

- In order to enable BIST functionality on a workspace you will need to enable
  it via *TraceWorkspaceSettings* instance setting
- Data Sources that requires source folder now required to be within the
  default workspace fileshare base folder. You must adjust the Source Path
  settings for each impacted data source to be a relative folder path within
  the default file share configured for the workspace.

# 11.2.6.1 (17 June 2019) - DEPRECATED

> **DEPRECATION NOTE:** This version of Trace is **no longer supported**

**Relativity Compatibility**

- \> 9.6.202.10

**Features**

- Ability to overwrite GUID for Group Identifier field - some instances have
  non-standard Group Identifier field

**Enhancements**

- BIST now includes testing for email message with large number of email
  addresses (more than what OI can support at the moment)

**Defect Fixes**

- Data Extraction will include full email header information. Large header
  information was previous truncated due to OI bug
  
  -  > NOTE: Relativity Viewer will still display truncated header
    information, however relativity fields (EmailTo, EmailFrom,
    EmailCC, EmailBCC will have full non-truncated data)
- App Installation now will fail properly if expected Group Identifier fields is
  not present in the workspace

**Deprecated**

- Microsoft Office 365 data source (based on GraphAPI) is deprecated, use
  Microsoft Exchange data source instead

**Upgrade Considerations**

- In order to enable BIST functionality on a workspace you will need to enable
  it via *TraceWorkspaceSettings* instance setting
- Data Sources that requires source folder now required to be within the
  default workspace fileshare base folder. You must adjust the Source Path
  settings for each impacted data source to be a relative folder path within
  the default file share configured for the workspace.

# 11.2.4.4 (10 June 2019) - DEPRECATED

> **DEPRECATION NOTE:** This version of Trace is **no longer supported**
