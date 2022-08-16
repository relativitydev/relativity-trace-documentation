---
layout: default
title: Data Sources
parent: Collection
grand_parent: Administrator Guide
nav_order: 2
---

# Data Sources
{: .no_toc }


A Data Source allows you to define where and how you are pulling data from a communication channel.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
 A Data Source stores the configuration necessary to retrieve data from a communication channel, process that data, and ingest it into Relativity Trace. **Click on the Data Source name to see more extensive details on how to configure.**

## Data Sources List
This list covers the most common Data Sources. To better understand the holistic Data Source support contact [support@relativity.com](mailto:support@relativity.com).

Currently unsupported communication channels can be added in as quickly as two weeks depending on the channel's openness and integration capabilities. To have a currently unsupported communication channel added as a supported data source please contact [support@relativity.com](mailto:support@relativity.com).
{: .info }

### Generic Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Generic | [Zip Drop]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/generic_data_sources/zip_drop.md %}) |


### Email Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Email | [Microsoft O365 Email and Calendar]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/office_365_email_and_calendar_via_collect.md %}) |
| Email | [Microsoft O365 Mail Archive Mailbox]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/microsoft_office_365_mail_archive_mailbox.md %}) |
| Email | [Google Suite]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/google_gsuite_via_collect.md %}) |
| Email | [Bloomberg Mail]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/bloomberg_mail_via_collect.md %}) |
| Email | [Microsoft Exchange Server]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/microsoft_exchange_server_via_verqu.md %}) |
| Email | HCL Notes and Domino |
| Email | Zimbra |

### Chat Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Chat | [Bloomberg Chat and PChat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/bloomberg_chat_pchat_via_collect.md %}) |
| Chat | [ICE Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/ice_chat_via_collect.md %}) |
| Chat | [Refinitiv Eikon Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/refinitiv_eikon_chat_and_fxt_via_collect.md %}) |
| Chat | [Mattermost Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/mattermost_via_verqu.md %}) |
| Chat | Symphony |
| Chat | Skype for Business |
| Chat | [Microsoft O365 Teams Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/microsoft_office_365_teams_chat_via_collect.md %}) |
| Chat | Zoom Chat |
| Chat | FXConnect |
| Chat | [Cisco WebEx Teams Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/cisco_webex_teams_via_collect.md %}) |
| Chat | ServiceNow |
| Chat | Google Chat |
| Chat | Salesforce Chatter |
| Chat | [Slack Enterprise Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/slack_enterprise_via_collect.md %}) |
| Chat | Microsoft Yammer |
| Chat | Facebook Workplace |

### Voice Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Voice | Zoom Audio |
| Voice | Symphony Audio |
| Voice | WebEx Teams Audio |
| Voice | Vodafone |
| Voice | Avaya |
| Voice | Cloud 9 |
| Voice | Verba/Verint |
| Voice | Mitel |
| Voice | Liquid Voice |
| Voice | O2 |
| Voice | Microsoft Teams Audio |
| Voice | Skype for Business Audio |
| Voice | [Generic Audio Data]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/voice_data_sources/generic_audio_data.md %}) |


### Mobile Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Mobile | WhatsApp |
| Mobile | WeChat |
| Mobile | SMS/MMS |
| Mobile | iMessage |
| Mobile | Telegram |
| Mobile | Signal |

### Collaboration Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Collaboration | OneDrive for Business |
| Collaboration | SharePoint |
| Collaboration | Google Drive |
| Collaboration | Box |
| Collaboration | AWS S3 |
| Collaboration | Dropbox |

### Archives Data Sources

| Type | Data Source      |
|:----:|:------------------:|
| Archive | [Proofpoint]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/archive_data_sources/proofpoint_via_verqu.md %}) |
| Archive | [Enterprise Vault]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/archive_data_sources/veritas_enterprise_vault_on_premises_via_verqu.md %}) |
| Archive | MimeCast |
| Archive | Smarsh |
| Archive | Google Vault |
| Archive | Dell Vault |
| Archive | OpenText |
| Archive | CommVault |
| Archive | Barracuda |
| Archive | Quest |
| Archive | Dell SourceOne |

Some Data Sources are supported through partners.
{: .info}


## Data Source Details

### Sections of a Data Source

1. **General**: this tab houses general identifying information and status for the data source. These fields are described in further detail below.

    * **Data Source Type:** Type of the data source
    * **Name:** The name of the Data Source
    * **Document Type Name:** A non-required name that will propagate to the Trace Type field on the documents that come in through this Data Source
      * If this field is left empty, the name of the Data Source will be used instead
    * **Provider Type:** The type fo communications that are being collected (Audio, Written, etc.)
    * **Ingestion Profile:** Ingestion Profile used to load data from this Data Source
    * **Start Date:** Date from which data will be pulled/pushed into Relativity
    * **End Date:** Optional date to which data will be pulled/pushed into Relativity.

      - If both dates are provided, data will be collected between “Start Date” and “End Date”. If “Ingestion State” is later than “Start Date”, then data will be collected between “Ingestion State” and “End Date”. 
      - If only “Start Date” is provided, data will be collected between “Start Date” and now. If “Ingestion State” is later than “Start Date”, then data will be collected between “Ingestion State” and now. 
      - If only “End Date” is provided, data will be collected between “Ingestion State” and “End Date”. 
      - If none of them is provided, data will be collected between “Ingestion State” and now.
      {: .info}
    
    * **Last Runtime (UTC):** The timestamp when this Data Source was last executed
    * **Enabled Time:** The timestamp when this Data Source was last enabled
    * **Disabled Reason:** An explanation for why a data source was automatically disabled by the system
    * **Status:** The last status message recorded by the Data Source
    * **Last Error Date:** Timestamp of the last time this Data Source failed, if it happened recently (based on Last Error Retention in Hours setting under Data Source Specific Fields)
    * **Last Error:** Error message from the last time this Data Source failed, if it happened recently (based on Last Error Retention in Hours setting under Data Source Specific Fields)

1. **Settings**: Configures standard settings required for the specific Data Source Type. These settings can be found on specific data source documentation pages.

1. **Trace Monitored Individuals:** Configures which monitored individual’s data should be retrieved from the data source. See [Monitored Individuals](#monitored-individuals) for more information.

1. **Data Transformations:** Determines which data transformations to apply to documents prior to ingestion into Relativity by this data source. See [Data Transformations](#data-transformations) for more information.

1. **Data Batches:** The data batches which have been generated by this data source. See [Data Batches](#data-batches) for more information.

1. **Advanced Configuration**: Different data source types have different configuration options. This section updates dynamically to allow access to these configuration options. See [Advanced Configuration](#advanced-configuration) and the documentation of your specific Data Source Type for more information.

1. **Console**
   
    - **Enable/Disable Data Source:** Enables (or disables) data retrieval for a particular data source.
    - **Reset Data Source:** Disables *and* resets data source to retrieve data from the specified Start Date. 

      Depending on Import settings, enabling a reset Data Source could duplicate data in the Workspace.
      {: .info }

### Advanced Configuration

This section contains additional settings which are not associated with specific Relativity Fields. The settings described here are common across all Data Source Types. Type-specific settings are documented under their respected Data Source sections.

- **Password Bank** Used to specify known passwords to attempt while encountering protected native files. Multiple passwords can be separated by the pipe character, `|`. Passwords containing the pipe character are supported through escaping the pipe character with a second pipe. Pipes are always escaped left to right.
    
  **Example Password Bank:** `passw0rd|Trace1234!|aaa|bb|cccc||dd||eee|||ff|||ggg||||hhh|||||`
    Yields the following passwords:
      - `passw0rd`
      - `Trace1234!`
      - `aaa`
      - `bb`
      - `cccc|dd|eee|`
      - `ff|`
      - `ggg||hhh||`

- **Extraction Thread Count:** The number of documents to extract in parallel.
- **Enrich Documents:** Whether or not to extract metadata and children from original documents. Valid values: `true` or `false`
- **Embedded File Behavior:** Embedded files are defined as attachments without file names. Most commonly these are in-line images. This setting changes the import behavior for embedded files. Valid options are:
  - **`Import`** - Import all embedded files (top level and child) as separate documents in Relativity Trace.
  - **`DoNotImportFromAttachments`** - Import embedded files from top level documents *only*. Do not extract embedded files from child documents.
  - **`DoNotImport`** - Do not import any embedded files.

      Both the `Import` and `DoNotImportFromAttachments` settings will greatly increase document volumes in Relativity Trace.
      {: .info}

- **Discover Monitored Individuals:** See [Discovery of Monitored Individuals](#discovery-of-monitored-individuals)
- **Include Monitored Individuals Not Linked to Data Source:** See [Discovery of Monitored Individuals](#discovery-of-monitored-individuals)
- **Discover Monitored Individuals Ignores Case:** See [Discovery of Monitored Individuals](#discovery-of-monitored-individuals)
- **Last Error Retention In Hours:** The length of time to persist any message in the `Last Error` field.
- **Health Check Failure Window Length in Minutes:** See [Data Source Auto-Disable] (#data-source-auto-disable)
- **Aip Application Id:** Contact [support@relativity.com](mailto:support@relativity.com) for more information on Azure Information Protection support.
- **Aip Tenant Id:** Contact [support@relativity.com](mailto:support@relativity.com) for more information on Azure Information Protection support.

### Data Source Auto-Disable

Trace will automatically disable data sources that are identified as unhealthy or have critical configuration errors that will require intervention by the user. Trace will automatically disable a data source for the following reasons:

- Data source has not had any successful data batches in the number of minutes configured on the `Health Check Failure Window Length in Minutes` field (if not set, default is 24 hours)
- Globanet data source is enabled without enabling Globanet (Merge1) at the workspace level

Auto-disabled data sources will have their Disabled Reason field populated to show that it was disabled by the system. The data source will also have error details outlining the failures that caused the system to disable it.

### Discovery of Monitored Individuals

Some Data Sources combine data from several places into a single import flow. In that scenario, it may not be clear which Monitored Individual is the source of a given document and no Monitored Individual will be tagged. To address this issue, Trace has introduced the `Discover Monitored Individuals` option on every Data Source. If enabled, Trace will look inside of the document and tag Monitored Individuals defined on the Data Source if they are found in headers inside the document. Monitored Individuals are recognized by identifier and all secondary identifiers. 

There is also the option to discover Monitored Individuals that are not linked to the Data Source with the setting `Include Monitored Individuals Not Linked To Data Source`. If `Discover Monitored Individuals` is false, this setting will take no action. If `Discover Monitored Individuals` is true and `Include Monitored Individuals Not Linked To Data Source` is false, this setting will take no action and it will only discover Monitored Individuals that are linked to that Data Source. If `Discover Monitored Individuals` is true and `Include Monitored Individuals Not Linked To Data Source` is true, it will use all of the Monitored Individuals in the workspace to tag documents.

By default, Monitored Individual discovery ignores case in the domain portion of the email address but not the name portion. For example, John.DOE@URL.COM will match John.DOE@url.com, but not john.doe@url.com.
{: .info }

To ignore case in the entire email address during Monitored Individual discovery, use the `Discover Monitored Individuals Ignores Case` setting. For example, John.DOE@URL.COM  will match always John.DOE@url.com, but only match john.doe@url.com if Discover Monitored Individuals Ignores Case is set to true.
{: .info }

![](media\data_sources\updated_data_source_specific_fields.png)

**Monitored Individual Discovery On Merge1 Data Sources**

Merge1's EWS Data Source only looks for Monitored Individuals in the `X-UserMailbox` header of an email. This header is provided by Merge1 and typically contains exactly one Monitored Individual.

**Monitored Individual Discovery On Other Data Sources**

All other data sources discover Monitored Individuals based on the `FROM`, `TO`, `CC`, and `BCC` headers. Any Monitored Individual on the Data Source with an identifier (primary or secondary) contained in any of these headers will be associated with the document.

**Supported File Formats**

Discovery of monitored individuals is based on finding the email addresses of monitored individuals in the headers of an email file. Therefore, it will only work properly on .eml, .msg, and .rsmf (Relativity Short Message Format) files. Any other file format is not currently supported.

[comment]: <> (Line 46-47 - No links)
[comment]: <> (Line 57-58 - No links)
[comment]: <> (Line 60-61 - No links)
[comment]: <> (Line 63-65 - No links)
[comment]: <> (Line 67-68 - No links)
[comment]: <> (Line 74-85 - No links)
[comment]: <> (Line 93-98 - No links)
[comment]: <> (Line 104-109 - No links)
[comment]: <> (Line 117-125 - No links)
[comment]: <> (Line 140-142 - Check paragraph formatting)
[comment]: <> (Line 172 - No information provided for Console)
[comment]: <> (Lines 211 - No Link) 
[comment]: <> (Line 217 - No link)
[comment]: <> (Lines 236 - Image sits over text)
