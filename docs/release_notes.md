# Relativity Trace Release Notes

- [13.3.0.13 (5 February 2021)](#133013-5-february-2021)

- [13.2.0.3 (15 December 2020 - DEPRECATED)](#13203-15-december-2020---deprecated)

- [13.1.0.2 (2 November 2020 - DEPRECATED)](#13102-2-november-2020---deprecated)

- [13.0.0.8 (5 October 2020 - DEPRECATED)](#13008-5-october-2020---deprecated)

- [12.5.0.6 (17 August 2020) - DEPRECATED](#12506-17-august-2020---deprecated)

- [12.4.1.1 (14 July 2020 - DEPRECATED)](#12411-14-july-2020---deprecated)

- [12.3.0.3 (1 June 2020) - DEPRECATED)](#12303-1-june-2020---deprecated)

- [12.2.0.13 (27 April 2020 - DEPRECATED)](#122013-27-april-2020---deprecated)

- [12.1.0.13 (30 March 2020) - DEPRECATED](#121013-30-march-2020---deprecated)

- [12.0.8.2 (24 February 2020) - DEPRECATED](#12082-24-february-2020---deprecated)

- [12.0.5.2 (24 October 2019) - DEPRECATED](#12052-24-october-2019---deprecated)

- [11.2.11.1 (13 September 2019) - DEPRECATED](#112111-13-september-2019---deprecated)

- [11.2.10.1 (12 August 2019) - DEPRECATED](#112101-12-august-2019---deprecated)

- [11.2.9.2 (15 July 2019) - DEPRECATED](#11292-15-july-2019---deprecated)

- [11.2.6.1 (17 June 2019) - DEPRECATED](#11261-17-june-2019---deprecated)

- [11.2.4.4 (10 June 2019) - DEPRECATED](#11244-10-june-2019---deprecated)

  

# 13.3.0.13 (5 February 2021)

**Compatibility**

- Relativity Version: **RelativityOne ONLY**
- Transfer API Services RAP (for Trace Shipper): **1.0.1.11**

**Features**

- You can now mark repetitive extracted documents, like those company logo images that are included in email signatures on every email, so they are no longer ingested into your workspace to reduce document volumes and noise in the system.
- Ensure that custom scripts, analytics, and other pre-calculations complete prior to analyzing a document for an alert by setting “Normalization Complete” criteria.
- Remove irrelevant content like spam, exempt communications, email blasts, and specific file types up front before running alert analysis to increase performance and reduce the complexity of your Rule saved searches.

**Enhancements**

- New Trace Document Status fields have been added to represent new stages of the Trace Data Flow. Status are now: 1 – New, 2 – Indexed, 3 – Term Searched, 4 – Normalized, 5 – Ready for Rule Analysis, 6 – Alert Rules Complete.
- Know the time at which the Trace Document Status field last changed with the “Trace Document Status Updated On” field, allowing you to understand the amount of time it takes for a document to be analyzed or report on documents stuck in specific stages of analysis.
- Now you can calculate Precision and Recall for your machine learning models ad-hoc with our Trace AI Calculations script to better understand the accuracy and select the appropriate rank cutoff based on your organization risk tolerance.
- Active Learning projects no longer delete old rank results when documents are removed from the Classification Index, allowing you to remove document after they’ve been ranked to reduce the size of the index, increase performance, and have greater stability.
- Know whether a document is an original file or extracted content from an original file with the Boolean “Trace Is Extracted” field. 

**Defect Fixes**

- Improved error handling for data batches that are wrongly created without a loadfile.
- Fixed issue where data batch retry could not be run for custom data sources.

# 13.2.0.3 (15 December 2020) - DEPRECATED

**Relativity Compatibility**

- **≥ 10.3.287.3**

**Features**

- When viewing a Rule, you can now click on the associated Saved Search to navigate directly to it.
- You can now ingest any email header metadata directly into Trace by simply adding a new Data Mapping to your Ingestion Profile.
- Trace Shipper now supports Web transfer protocol, as an on-premises and RelativityOne alternative to Direct or Aspera transfer.

**Enhancements**

- Admins can now Finalize a Data Batch to delete excess files on the Fileshare, reducing the infrastructure footprint and the frequency at which new Fileshares must be added.

**Defect Fixes**

- Fixed issue where the Password Protected field had a value of “Decrypted” even though the document remained encrypted because a matching password did not exist on the Data Source.
- Fixed issue where Exempt List Entries that had a username in all capital letters (e.g. USERNAME@domain.com) would not match communication From values that were exact matches or matches with different character cases.
- The ability to manually create a Data Batch has been removed from the UI.
- Fixed issue with loading dependencies in Shipper that was logging misleading error messages.

  

# 13.1.0.2 (2 November 2020) - DEPRECATED

**Relativity Compatibility**

- **≥ 10.3.287.3**

**Features**

- You can now identify when a document was first linked to an Alert Rule using the “Trace Alerted On” field
- The Exempt List Data Transform Type can now identify “Usernames” (content to the left of the @ symbol in an email address), making it easier to exclude generic “noreply”, “newsletter”, or “support” email addresses from alerting and review

**Enhancements**

- Global Dt Search Index build errors are now reported on the Trace Indexing Task to increase awareness of impactful failures
- Noise words are now omitted by default when creating a new dtSearch Index
- The ability to “Not Import Natives” has been added to Trace Ingestion Profiles

**Defect Fixes**

- Improved error handling when a Data Batched is retried and the linked Data Source has been deleted
- Fixed issue where an invalid Zip Drop Data Batch would be set to “Completed” on Retry when it should have been “CompletedWithErrors”
- Fixed issue where you could manually unlink documents from Trace Rule Terms, Trace Terms, and Monitored Individuals. Note that Audit would catch any of these actions
- Fixed issue where Exempt List entries of the “Email Address” Type considered character case when matching communication From values
- Copy and Replace mass operations have been removed from Rules, Terms, Monitored Individuals, Actions, and Data Batches to prevent creating objects with the same name or accidental linking between objects that are not related

  

# 13.0.0.8 (5 October 2020) - DEPRECATED

**Relativity Compatibility**

- **≥ 10.3.287.3**

**Features**

- Introducing new Trace Ingestion Profiles to simplify the setup of Data Sources and increase the resiliency of automated data ingestion

**Enhancements**

- SQL views are now created for choice tables (ZCodeArtifact) and can be used when creating Relativity Scripts
- Improved handling of an edge case where Data Batch load files are missing (occasionally observed when swapping out file shares)

**Defect Fixes**

- Fixed an intermittent issue where “term hits” would be added to the *Trace Terms* field, but not the *Trace Rule Terms* field. This defect didn’t impact the alerting of a communication but would reduce the transparency of why an alert was generated

**Upgrade Considerations**

- On upgrade, new Ingestion Profiles will be created from your existing Relativity Integration Point Profiles and linked to your Data Sources

  

# 12.5.0.6 (17 August 2020) - DEPRECATED

**Relativity Compatibility**

- **≥ 10.3.287.3**

**Features**

- Relativity Trace is now compatible with Aero UI (RelativityOne only)

**Enhancements**

- Enhanced Setup validation with clear messages for what's not configured for Trace
- Removed superfluous Monitored Individual fields that were causing conflicts after deployments
- Trace Shipper service
  - Now consumes local 3rd party data provider logs and makes them available in Relativity for troubleshooting
  - Improved re-queueing for items that were not previously available in source folder
  - Improved data delivery with efficient batching strategy
  - Graceful shutdown of the service of in-flight transfer jobs
  - Internal queue depth reporting appropriate logging
  - Propagation of data source configuration from Relativity to Trace Shipper (Enabled/Disabled/etc) to be consumed by data provider
- Additional logging to troubleshoot failing rules with custom query options on saved search
- Trace Document Hash field is now populated for attachments which allows for deduplication of generated alerts and review workflow
- Improved data extraction fidelity for email like file types to propagate all available metadata
- Trace Exchange data source now has a flag to exclude hidden MS Teams folder
- Trace Rule Terms field on document is now populated with terms that are associated with actual rule matches only (as opposed to all matching terms for all rules)

**Defect Fixes**

- BIST no longer breaks when deployed to workspaces with reserved names
- Correctly propagating Password Protected flag across all known file types
- In certain extreme failure modes, data validation task now correctly identifies and fails data batches with silent failures in import job (RIP)
- Renamed fields in Relativity that are associated with RIP profiles are now correctly identified as problematic with an appropriate error message
- Resolved handling of dtSearch temp indexes with document retry workflow

**Deprecated**

- Removed confusing Associate (link) Document to Rule button in the Rules tab UI

**Upgrade Considerations**

- If a rename of an ingested field is done in Relativity (**ex:** Email From -> From), **all** RIP profiles referencing that field **MUST** be updated to reference the new field name.

  

# 12.4.1.1 (14 July 2020) - DEPRECATED

**Relativity Compatibility**

- **≥ 10.3.287.3**

**Features**

- Created the Communication Direction Data Transformation Type, which can be used to determine the direction of communication (Inbound, Outbound, Internal, External, Undefined) based on the Internal Domains defined in the Trace workspace
- Created the Exempt List Data Transformation Type, which can be used to exempt messages from review if the sender is on the specified Exempt List
- (PREVIEW) Created the new Zip Drop Data Source Type, which can be used by customers and partners to import fully formed data batches (documents and metadata) into Trace by simply placing a ZIP file in a drop folder
- (PREVIEW) Created scripts that can be used to consolidate review outcomes across multiple fields into specific result fields

**Enhancements**

- All Trace usage of dtSearch has been rewritten to use modern dtSearch APIs instead of legacy references, reaping the benefit of many enhancements and bug fixes and ensuring future stability
- Trace Data Ingestion now validates and normalizes all date values in every load file before attempting import, eliminating painful repair/retry scenarios
- Trace Shipper Service configuration file now has placeholders for all configurable attributes
- Improved alerting on unhealthy Data Sources for RelativityOne customers
- Installed Version field on Setup object can now be edited to force Update logic to run in workspace
- Improved log messages when using AIP decryption

**Defect Fixes**

- Fixed some issues with the Data Disposal Action Type for external data sources involving file share migration and non-standard SQL schema
- Fixed an issue where Trace Recipient Count was incorrect for certain email messages
- Fixed an issue where deduplication would fail when using a non-standard load file column header for Trace Monitored Individuals

**Deprecated**

- Copy mass action is no longer available for the Data Source RDO type

**Upgrade Considerations**

- In order to take advantage of the new Communication Direction and Exempt data transformations you must re-create your Integration Profile to include corresponding (new) fields to be mapped and associate this new profile with the corresponding Data Source(s)
- All Office 365 customers should migrate to use of OAuth 2.0. Microsoft will no longer allow basic username/password authentication in O365 starting in October 2020 and Data Sources using it will begin failing. Review Relativity Trace Authorization documentation "authorization.md" for OAuth 2.0 information.



# 12.3.0.3 (1 June 2020) - DEPRECATED

**Relativity Compatibility**

- **≥ 10.3.287.3**

**Features**

- Microsoft Exchange/O365 Data Source now supports OAuth 2.0 including support for client credential flow where Relativity Trace is registered as a service principal
- Embedded File Behavior option on Data Sources allows customers to control extraction behavior of embedded content within communications and attachments to preventing the creation of excessive and unneeded files

**Enhancements**

- Data Disposal action is now supported for custom Data Sources
- Data Batch Retry is now supported across fileshares for custom Data Sources
- Added automatic retry of failures to decrypt AIP messages to improve reliability
- Increased security for storing credentials on Data Sources

**Defect Fixes**

- Fixed issue with load file path on failed Data Batches from custom Data Sources that would prevent retry
- Added an automatic retry of Data Batches stuck in Enriching status for more than 24 hours if they have not yet been retried
- Trace Shipper now logs an error instead of overwriting the existing file if a file with the same name already exists in the destination folder

**Upgrade Considerations**

- All Office 365 customers should migrate to use of OAuth 2.0. Microsoft will no longer allow basic username/password authentication in O365 starting in October 2020 and Data Sources using it will begin failing. Review [Relativity Trace Authorization](https://relativitydev.github.io/relativity-trace-documentation/authorization) documentation for OAuth 2.0 information.

# 12.2.0.13 (27 April 2020) - DEPRECATED

**Relativity Compatibility**

- **≥ 10.3.287.3**

**Features**

- Added configuration retrieval and log file visibility to the Trace Shipper Service (BETA)

**Enhancements**

- Added support for changing the workspace fileshare for existing Data Batches
- To preserve system resources, Data Sources will be disabled if they have not produced a successful Data Batch in 24 hours

**Defect Fixes**

- Fixed issue where Terms and Rules could have names that were not unique

**Deprecated**

- The unsupported workflow of adding a deduplication transform to a Relativity Native Data Source is no longer possible due to data integrity concerns

# 12.1.0.13 (30 March 2020) - DEPRECATED

**Relativity Compatibility**

- \> 9.6.202.10

**Features**

- Trace Shipper completes the Globanet connector use case as a way to move files from customer network servers to RelativityOne file share (BETA)
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
- dtSearch indexes will now perform Full Build automatically (no manual interaction) on newly created indexes that are subject to automation
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
