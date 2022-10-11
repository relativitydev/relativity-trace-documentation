---
layout: default
title: Release Notes
parent: What's New
nav_order: 1
---

# Release Notes
{: .no_toc }

New features, enhancements, and defect fixes are released in each monthly update.
{: .fs-6 .fw-300 }

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

**General Compatibility:** Transfer API Services RAP (for Trace Shipper): 1.0.1.11
{: .info}

# 15.7.0.0 (11 October 2022)

**Features**

- Added broad support for Journal Wrapped Email files extracted from archives to ensure metadata robustness and accuracy
- Validation will be performed when saving a new Term, to ensure the dtSearch syntax on the term is valid for searching
 
**Enhancements**

- Improved error reporting when performing Trade Reconstruction
- Reduced data ingestion speeds through enhancements to automated retry process

**Defect Fixes**

- Fixed issue with the "Optional" condition in Trade Reconstruction Configurations did not function properly
- Fixed defect that caused AI Text Cleansing for Relativity Short Message Format (RSMF) messages to occasionally fail

# 15.6.40.0 (6 Sept 2022)

**Features**

- The following pre-build risk detection AI models can be enabled within our Machine Learning framework to identify key misconduct:
  - Prearranged Trading Detection
  - Price and Benchmark Fixing Detection
  - Front Running Detection
  - Mirror Trading Detection 
  - Trade Fixing Detection

**Enhancements**

- Expand Trace AI Text Cleansing to remove disclaimers, Join and Leave tags, usernames, headers, and timestamps from chat data in the Relativity Short Message Format (RSMF) 
- Added support for publicly accessible SFTP, alongside our more secure SFTP with VPN approach

**Defect Fixes**
- Fixed known issues with Language Identification Transformation `Trace Other Languages` results
- Fixed known issues with Machine Learning Model Data Mapping and Tab

# 15.5.11.0 (2 Aug 2022)

**Features**

- The following pre-build irrelevant content detection AI models can be enabled within our Machine Learning framework to further reduce false-positive alerts:
  - Newsletter Detection: detect widely disseminated and recurring messages that summarize world and financial market news
  - Financial Research Report Detection: detect widely disseminated documents prepared by investment research firms that describe a company and often provide a particular recommendation
- Identify financial products (tickers, stocks, companies), pharmaceutical products (drugs, chemicals, competitors), or projects (names, lists) mentioned in communications using [Product Identification]({{ site.baseurl }}{% link docs/administrator_guide/enrichment/data_transforms.md %}) to create more targeted alerts, provide greater context for reviewers, or expose trends for investigation

**Enhancements**

- Excluded certain communications from "Non-Alerted Document Review Report" [Notifications]({{ site.baseurl }}{% link docs/administrator_guide/reporting/notifications.md %}) using the `Trace Type` field value to reduce false positive notifications

**Defect Fixes**
- Fixed known issues with Language Identification Transformation `Trace Other Languages` results
- Fixed known issues with Machine Learning Model Data Mapping and Tab

# 15.3.32.0 (31 May 2022)

**Features**

- Identifying the languages used within a communication and the detection of language switching is now enabled by default with no need for configuration within Structured Analytics.
- Spam detection is now automatically run across all communications without the need for configuration through Active Learning.

# 15.4.14.0 (28 June 2022)

**Features**

- The following pre-built risk detection AI models can be enabled within our new Machine Learning framework: 
  - Change of Venue: an attempt to avoid discovery by changing the communication venue (e.g., moving from email to phone call)
  - Rumors and Speculation: the distribution or discussion of unverified and doubtfully true information 
  - Collaborative Discussion: employees working together to prevent the discovery of misconduct and sharing of client identifying data
  - Boasting: excessively proud and self-satisfied talk by a trader of their achievements in regard to someone less fortunate
  - General Tipping: the sharing of potential material nonpublic information (MNPI) regarding general company information, financial information, or corporate actions 
- Customers can define and implement their own AI models through our self-service Machine Learning framework to detect risky or irrelevant content

**Enhancements**

- The Data Source auto-disable time period can now be set per Data source rather than across all Data Sources

# 15.3.32.0 (31 May 2022)

**Features**

- Identifying the languages used within a communication and the detection of language switching is now enabled by default with no need for configuration within Structured Analytics.
- Spam detection is now automatically run across all communications without the need for configuration through Active Learning.

**Enhacements**

- Expanded the audio metadata formats accepted (past JSON)
- Made it easier to use the Cleansed Extracted Text for alerting by configuring this on Term Searching Task rather than in the `Trace All Documents` saved search. 
 
 **Defect Fixes**

- Fixed an issue with our in-house O365 Mail and Calendar data source, where email data that is created and moved to the Archive folder (mailbox) between Data Retrieval task runs is not collected (fixed through the introduction of the separate O365 Archive data source)

# 15.2.0.0 (19 April 2022)

**Enhancements**
- Simplified the process of data source creation in Trace to minimize possible configuration error, speed implementation time and reduce need for specialist support
- Enabled cloud-to-cloud support for Thomson Reuters Chat
- Introduced capabilities to accept different formats of Audio files

# 15.1.23.0 (15 March 2022)

**Features**

- A Reviewer can now email a monitored individual directly within the system to let them know that they are in breach of a policy or to get more information about an event.
- Communications are now classified as either being sent or received from a personal email address (gmail, yahoo, etc.), so it’s easier to identify scenarios where employees are sending corporate content outside the organization either to themselves or others.
- To accelerate the pace at which reviewers can clear alerts, we’ve added the ability to set default review decisions that are automatically populated when a communication is viewed.

**Enhancements**
 
- Improved our Password Bank functionality to specify when a document was encrypted but was successfully decrypted using one of the passwords. This allows for compliance teams to better understand the volume of communications that are being encrypted as a potential risk indicator.
- Ability to see communications that exist within the same email thread in the relational pane in the viewer after Email Thread Deduplication is performed. This reduces the need for running the Email Threading Structured Analytics operation.
- Added more detailed auditing for when a Trade Reconstruction action is performed to capture the links made between a trade and all its related communications. This enables users to review historic Trade Reconstruction results regardless of whether they’ve rerun the operation.

# 15.0.10.1 (8 February 2022)

**Features**

- Rule change report: Generate a report that can also be sent via email whenever a change is made to a rule so that compliance can monitor those who have permissions to update controls for any types of misconduct.
- System Health Report: Generate a report that can also be sent via email whenever a current task status failure occurs so that compliance can monitor system performance or if something is not working as anticipated. 
- Expanded ZipDrop data sources to be able to collect non-communication data (structured data) such as terms, trades, human resource information, or expense data.

**Enhancements**
 
- Enabled support for GSuite Cloud-to-Cloud Connection 
- A new Trace Email Action field can be used within Rules to alert differently on Sent, Forwarded, Replies, Replies to All, or Draft emails to further pinpoint risk and reduce false positive alerts
- Improved the viewer experience for cleansed block highlighting by no longer highlighting the header envelop
- Add new fields to NonAlerted Document Notification Reports

**Defect Fixes**

- Fixed an issue where block highlighting fails when switching back documents too fast

# 14.7.2.2 (20 December 2021)

**Features**

- Trace added functionality to track if team members viewed documents that should not have been viewed, Trace will send an email report or real-time notifications regarding privacy issues
- Automated management of Monitored Individuals with Azure Active Directory 
- Added Trace Surveillance Policies to identify risk and misconduct that contains lexicons specifically used in audio, in order to aid current out of the box policies. This will allow for better alerting and less false positives. 

**Enhancements**
 
- Enabled support for Slack Cloud-to-Cloud Connection 
- Developed an easy and quick way to view what data soruce a document is sourced from

**Defect Fixes**

- Fixed Persistent Highlighting issue where go to next highlight functionality does not work when block highlighting is collapsed  
- Fixed an AI Cleansing failing issue that caused documents to not be parsed, this is not a failure though because the system defaults to alerting on Extracted Text as Trace always has 

# 14.6.0.0 (9 November 2021)

**Features**

- Enhanced metadata filtering within Trace Surveillance Policies to further reduce false-positive alerts
- Added a Trace Surveillance Policy that targets risks associated with financial services employees discussing content on social platforms like Twitter and Reddit. This policy is based on recent regulatory discussions around social platform’s influence on market trading 
- Added Trace Surveillance Policies in Dutch to identify misconduct within global organizations 

**Enhancements**
 
- Change sort order on the documents list within the Rules layout to show the most recent alerts first  
- Enabled support for Cloud9 Audio for in-house collection, transcription generation, and review 
- Enabled support for O2 Cloud Audio for in-house collection, transcription generation, and review 

**Defect Fixes**

- Fixed a rare issue where Data Batch metadata is not updated when the Data Batch completes 
- Fixed an issue where the Data Batch “Job Completion Error” field is overwritten by a generic message after an error occurs 

# 14.5.3.1 (5 October 2021)

**Features**

- Added Trace Surveillance Policies targeting the Research Desk to identify misconduct where monitored individuals are providing unauthorized investment advice within firm publications.  
- Added Trace Surveillance Policies targeting new Hires, Internal Transfers, and Terminations of Monitored Individuals to identify monitored individuals who are breaching internal policies around the sharing of information.
- New Trace Data Sources for Bloomberg Chat and Mail Data Source surveillance that allows for in-house collection without a 3rd party application. 
- All Trace pages now support the new Relativity Aero design system for simpler user experience and better performance 

**Enhancements**

- Improved O365 cloud-to-cloud data source performance for large numbers of Monitored Individuals 
- Add Group By and Pivot On for "Trace AI Extracted Text Cleansing Status" field to enable use in dashboard widgets 
- New Monitored Individual Linking that discovers MIs within a data source and connects them to the entire workspace

**Defect Fixes**

- Fixed rare issue where Data Batches fail due to identifiers not being considered unique 
- Fixed Data Source Type naming conflict that impacted existing data sources when new cloud-to-cloud data sources were added 

# 14.4.1.2 (31 August 2021)

**Features**

- Automatic email thread deduplication removes old emails from new replies or forwards to reduce duplicative alerting 
- Added Trace Surveillance Policies in Russian and Italian to identify misconduct within global organizations
- Added Trace Surveillance Policies for Social Trading platforms to monitor users attempting to manipulate the markets, breach code of conduct policies, and other types of risks

**Enhancements**

- Introduced dedicated “Trade” and “Trade Reconstruction Configuration” object types for performing Trade Reconstruction
- Pivot and Group By the “Trace Document Status Updated On” field for added reporting capabilities within dashboard widgets
- Added the ability to pull data for a specific date range on cloud-to-cloud Data Sources
- Improved resiliency of cloud-to-cloud Data Sources with improved retry

**Defect Fixes**

- Fixed a rare issue where a Data Batch would get stuck in the non-terminal Retrieval status rather than move to CompletedWithErrors
- Fixed a rare issue where Data Batches in the non-terminal Retrieval status would wrongfully move to Abandoned
- Fixed a performance issue in Data Retrieval for the O365 Data Source 

# 14.3.0.4 (27 July 2021)

**Features**

- Added Trace Surveillance Policies in Spanish and German to identify misconduct within global organizations
- Added Trace Surveillance Policies targeting the wrongful sharing of Personally Identifiable Information (PII)
- New Trace Data Source for Microsoft Teams that allows for surveillance of O365 Teams without a 3rd party collection application
- Automatic removal of email headers (From, To, etc.) and email signatures that could otherwise trigger false positive alerts

**Enhancements**

- Improved support of Object and Choice fields in Dynamic Rules search criteria

**Defect Fixes**

- Fixed an issue where extra whitespace could prevent Exempt List matches
- Fixed an intermittent issue with Active Learning that caused indexes to fall into a failure state

# 14.2.0.5 (24 June 2021)

**Features**

- Added Trace Surveillance Policies in Japanese and French to identify misconduct within global organizations
- Collect data using our new Relativity Trace native O365 (Email & Calendar) data source and no longer need 3rd party on-premises applications for O365 surveillance
- Automatically remove confidentiality disclaimers from communications that could otherwise trigger false positive alerts

**Enhancements**

- Updated the generated names for dynamically created Rules to make them easier to understand
- No longer automatically create a “Trace Persistent Highlight Set” to limit confusion with the “Trace Rules Persistent Highlight Set”
- Introduced a “Data Transformation” Task to complete all file analysis during ingestion
- Password protected files that cannot be decrypted no longer report as document errors, but rather report their encryption status on the Password Protected field
- You can now use reflected document fields within the search criteria of Dynamic Rules to improve the accuracy of both Trade Reconstruction and Control Room surveillance
- Improved the ability of Trace Shipper to self-recover when faced with authentication challenges
- You can now delete Rule Generator objects

**Defect Fixes**

- Fixed an issue with the “Trace Machine Learning Statistical Sample” Script that caused it not to run successfully
- Fixed an issue where extremely large data batches would fail after successfully importing documents
- Fixed an issue where Scripts with certain types of input parameters would fail to run within Advanced Actions

# 14.1.0.6 (18 May 2021)

**Features**

- Added [Proofpoint Enterprise Archive](https://www.proofpoint.com/us/products/archiving-and-compliance/enterprise-archive) as a new supported data source
- Added [Mattermost](https://mattermost.com/) as a new supported data source

**Enhancements**

- Added the ability to include static search conditions in Rule Generators for improved Trade Reconstruction, Control Room, and Dynamic Rule results
- Updated multiple Data Source, Data Batch, Exempt Entry, Rule, and Document fields to be open to “Sort/Tally”, “Group By”, and “Pivot” functionality for greater reporting capabilities
- Removed the need to manually add and maintain a Trace License on the Setup page

**Defect Fixes**

- Fixed an issue where a categorization set related to an automated Active Learning project would fall into an errored state and not self-recover
- Fixed an issue with Trace Rule auditing that could cause system slowness
- Fixed an issue where the Rule Generators were not included in copied workspaces

# 14.0.0.4 (13 April 2021)

**Features**

- Launch of **Control Room Surveillance**. Leverage Restricted Lists, Insider Lists, Gray Lists, Watchlist, and Wall Crossing Lists to automatically alert on breaches of information barriers, inappropriate sharing of material non-public information (MNPI), and violations of trading restrictions
- Launch of **Trade Reconstruction**. Automatically link trades together with related communications to simplify the Trade Reconstruction process so you can respond to regulators faster and with more confidence
- Automatically connect Trade or Transaction alerts within your **Trade Surveillance** or **Anti-money Laundering** systems to related communications to better understand the intent around an event that led to an alert
- Create **dynamic Rules** based on any integrated structured data (CRM system, Time & Expense system, HR System, Excel, in-house tools, etc.) to automatically alert on communications that are related to events in other enterprise systems

**Enhancements**

- Improved Machine Learning Validation Test process with new statistical sampling for review population and added output metrics to enhance precision and recall understanding
- Improved Trace Shipper Web protocol transfer speeds

**Defect Fixes**

- Fixed an issue with Data Batch Retry that caused the operation to fail under certain conditions
- Fixed an issue where the “Omit from Alerts” field was not being cleared when Trace Document Retry was run

# 13.4.0.6 (9 March 2021)

**Features**

- Added native “Microsoft Exchange On-Premises” data sources for Email, Calendar, and Skype data
- Added a native “Enterprise Vault On-Premises” data source for Archive data

**Enhancements**

- Improved Data Batch resiliency to significantly improve completion success rate
- Added audits for when a document receives the “1- New” Trace Document Status
- Trace Document Retry automatically includes all family members of the document selected so families remain together through the Trace Document Flow
- Batch sizing is now exposed within Trace Shipper for Web protocol

**Defect Fixes**

- Fixed an issue where documents have multiple Trace Document Statuses causing them to get stuck in the Trace Document Flow
- Fixed an issue where Trace Document Retry failure causes operation to fall into unrecoverable state
- Fixed an issue where “Trace AI Calculation Script” failed to calculate precision and recall when Rank values reflected multiple object fields

# 13.3.0.18 (5 February 2021)

**Features**

- You can now mark repetitive extracted documents, like those company logo images that are included in email signatures on every email, so they are no longer ingested into your workspace to reduce document volumes and noise in the system.
- Ensure that custom scripts, analytics, and other pre-calculations complete prior to analyzing a document for an alert by setting a `Normalized Saved Search` on the `Rule Evaluation` task.
- Remove irrelevant content like spam, exempt communications, email blasts, and specific file types up front before running alert analysis to increase performance and reduce the complexity of your Rule saved searches.

**Enhancements**

- New Trace Document Status fields have been added to represent new stages of the Trace Data Flow. Status are now: `1 – New`, `2 – Indexed`, `3 – Term Searched`, `4 – Normalized`, `5 – Ready for Rule Analysis`, `6 – Alert Rules Complete`.
- Know the time at which the Trace Document Status field last changed with the `Trace Document Status Updated On` field, allowing you to understand the amount of time it takes for a document to be analyzed or report on documents stuck in specific stages of analysis.
- Now you can calculate Precision and Recall for your machine learning models ad-hoc with our `Trace AI Calculations` script to better understand the accuracy and select the appropriate rank cutoff based on your organization risk tolerance.
- Active Learning projects no longer delete old rank results when documents are removed from the Classification Index, allowing you to remove document after they’ve been ranked to reduce the size of the index, increase performance, and have greater stability.
- Know whether a document is an original file or extracted content from an original file with the Boolean `Trace Is Extracted` field. 

**Defect Fixes**

- Improved error handling for data batches that are wrongly created without a loadfile.
- Fixed issue where data batch retry could not be run for custom data sources.

# 13.2.0.3 (15 December 2020)

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

  

# 13.1.0.2 (2 November 2020)

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

  

# 13.0.0.8 (5 October 2020)

**Features**

- Introducing new Trace Ingestion Profiles to simplify the setup of Data Sources and increase the resiliency of automated data ingestion

**Enhancements**

- SQL views are now created for choice tables (ZCodeArtifact) and can be used when creating Relativity Scripts
- Improved handling of an edge case where Data Batch load files are missing (occasionally observed when swapping out file shares)

**Defect Fixes**

- Fixed an intermittent issue where “term hits” would be added to the *Trace Terms* field, but not the *Trace Rule Terms* field. This defect didn’t impact the alerting of a communication but would reduce the transparency of why an alert was generated

**Upgrade Considerations**

- On upgrade, new Ingestion Profiles will be created from your existing Relativity Integration Point Profiles and linked to your Data Sources

  

# 12.5.0.6 (17 August 2020)

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

  

# 12.4.1.1 (14 July 2020)

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



# 12.3.0.3 (1 June 2020)

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

# 12.2.0.13 (27 April 2020)

**Features**

- Added configuration retrieval and log file visibility to the Trace Shipper Service (BETA)

**Enhancements**

- Added support for changing the workspace fileshare for existing Data Batches
- To preserve system resources, Data Sources will be disabled if they have not produced a successful Data Batch in 24 hours

**Defect Fixes**

- Fixed issue where Terms and Rules could have names that were not unique

**Deprecated**

- The unsupported workflow of adding a deduplication transform to a Relativity Native Data Source is no longer possible due to data integrity concerns

# 12.1.0.13 (30 March 2020)

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

# 12.0.8.2 (24 February 2020)

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

# 12.0.5.2 (24 October 2019)

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

# 11.2.11.1 (13 September 2019)

**Defect Fixes**

- Fixed an issue where Email action was automatically adding trace@relativity.com to recipient list


# 11.2.10.1 (12 August 2019)

**Defect Fixes**

- Fixed an issue where under certain failures of Data Retrieval task, Globanet based data sources would delete retrieved data without extracting it

# 11.2.9.2 (15 July 2019)

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

# 11.2.6.1 (17 June 2019)

**Features**

- Ability to overwrite GUID for Group Identifier field - some instances have
  non-standard Group Identifier field

**Enhancements**

- BIST now includes testing for email message with large number of email
  addresses (more than what OI can support at the moment)

**Defect Fixes**

- Data Extraction will include full email header information. Large header
  information was previous truncated due to OI bug
  
  -  > Relativity Viewer will still display truncated header
    information, however relativity fields (EmailTo, EmailFrom,
    EmailCC, EmailBCC will have full non-truncated data)
    {: .info }
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
