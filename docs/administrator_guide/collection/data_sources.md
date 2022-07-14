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
 A Data Source stores the configuration necessary to retrieve data from a communication channel, process that data, and ingest it into Relativity Trace. Click on the Data Source name to see more extensive details on how to configure.

## Data Sources List
This list covers the most common Data Sources. To better understand the holistic Data Source support contact [support@relativity.com](mailto:support@relativity.com).

Currently unsupported communication channels can be added in as quickly as two weeks depending on the channel's openness and integration capabilities. To have a currently unsupported communication channel added as a supported data sources please contact [support@relativity.com](mailto:support@relativity.com).
{: .info }

### Generic Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Generic | [Zip Drop]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/generic_data_sources/zip_drop.md %}) |


### Email Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Email | [Microsoft O365 Email and Calendar]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/office_365_email_and_calendar_via_collect.md %}) |
| Email | [Microsoft O365 Mail Archive Mailbox data source]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/microsoft_office_365_mail_archive_mailbox.md %}) |
| Email | [Google GSuite]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/google_gsuite_via_collect.md %}) |
| Email | [Bloomberg Mail]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/bloomberg_mail_via_collect.md %}) |
| Email | [Microsoft Exchange Server]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/email_data_sources/microsoft_exchange_server_via_verqu.md %}) |
| Email | HCL Notes and Domino |
| Email | Zimbra |

### Chat Data Sources

| Type  | Data Source      |
|:-------:|:------------------:|
| Chat | [Bloomberg Chat and PChat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/bloomberg_chat_pchat_via_collect.md %}) |
| Chat | [ICE Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/ice_chat_via_collect.md %}) |
| Chat | [Refinitiv Eikon Chat and FXT]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/cisco_webex_teams_via_collect.md %}) |
| Chat | [Mattermost Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/refinitiv_eikon_chat_and_fxt_via_collect.md %}) |
| Chat | Symphony |
| Chat | Skype for Business |
| Chat | [Microsoft Teams Chat]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/chat_data_sources/microsoft_office_365_teams_chat_via_collect.md %}) |
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
| Voice | Microsoft Teams Audio |
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
   * **Name:** The name of Data Source
   * **Document Type Name:** A non-required name that will propagate to the Trace Type field on the documents that come in through this Data Source
     * If this field is left empty, the name of the Data Source will be used instead
   * **Data Source Type:** Type of the data source
   * **Ingestion Profile:** Ingestion Profile used to load data from this Data Source
* **Start Date:** Date from which data will be pulled/pushed into Relativity
* **End Date:** Optional date to which data will be pulled/pushed into Relativity.
  
* **Last Runtime (UTC):** The timestamp when this Data Source was last executed
  
   * **Status:** The last status message recorded by the Data Source

   * **Last Error Date:** Timestamp of the last time this Data Source failed, if it happened recently (based on Last Error Retention in Hours setting under Data Source Specific Fields)
   
   * **Last Error:** Error message from the last time this Data Source failed, if it happened recently (based on Last Error Retention in Hours setting under Data Source Specific Fields)
2. **Credentials:** this tab is used to securely input and store credential information. This includes username and password as well as OAuth client secrets, should they be used. Not all Data Sources require credential information.
   
    * **Username:** Optional field used for authentication of a data source.
    
    * **Password:** Optional field used for authentication of a data source.
    
    * **AIP Client Secret:** Optional field used for authentication of AIP decryption using OAuth. See [Trace and Azure Information Protection](#trace-and-azure-information-protection) for more information. 
    
    * **EWS Client Secret:** Optional field used for authentication of exchange email retrieval using OAUT.
    
      > EWS Client Secret is used only on Microsoft Exchange type Data Sources. See [Microsoft Exchange Data Source](#microsoft-exchange-data-source) for specifics on authentication.
3. **Trace Monitored Individuals:** Configures which monitored individual’s data should be retrieved from the data source. See [Monitored Individuals](#monitored-individuals) for more information.
4. **Data Transformations:** Determines which data transformations to apply to documents prior to ingestion into Relativity by this data source. See [Data Transformations](#data-transformations) for more information.
5. **Data Batches:** The data batches which have been generated by this data source. See [Data Batches](#data-batches) for more information.
6. **Data Source Specific Settings**: Different data source types have different configuration options. This section updates dynamically to allow access to these configuration options. See [Data Source Specific Settings](#data-source-specific-settings) and the documentation of your specific Data Source Type for more information.
7. **Console**
   
    - **Enable/Disable Data Source:** Enables (or disables) data retrieval for a particular data source.
    - **Reset Data Source:** Disables *and* resets data source to retrieve data from the specified Start Date. 
    
      > Depending on Import settings, enabling a reset Data Source could duplicate data in the Workspace.
      {: .info }

### Data Source Specific Settings

This section contains additional settings which are not associated with specific Relativity Fields. The settings described here are common across all Data Source Types. Type-specific settings are documented under their respected Data Source sections.

-   **Password Bank** Used to specify known passwords to attempt while encountering protected native files. Multiple passwords can be separated by the pipe character, `|`. Passwords containing the pipe character are supported through escaping the pipe character with a second pipe. Pipes are always escaped left to right.
    
    > **Example Password Bank:** `passw0rd|Trace1234!|aaa|bb|cccc||dd||eee|||ff|||ggg||||hhh|||||`
    >
    > Yields the following passwords:
>
    > * `passw0rd`
    > * `Trace1234!`
    > * `aaa`
    > * `bb`
    > * `cccc|dd|eee|`
    > * `ff|`
    > * `ggg||hhh||`

- **Extraction Thread Count:** The number of documents to extract in parallel.

- **Enrich Documents:** Whether or not to extract metadata and children from original documents. Valid values: 

  -   `true`
  -   `false`

- **Embedded File Behavior:** Embedded files are defined as attachments without file names. Most commonly these are in-line images. This setting changes the import behavior for embedded files. Valid options are:

  -   **`Import`** - Import all embedded files (top level and child) as separate documents in Relativity Trace.
  -   **`DoNotImportFromAttachments`** - Import embedded files from top level documents *only*. Do not extract embedded files from child documents.
  -   **`DoNotImport`** - Do not import any embedded files.
>   Both the `Import` and `DoNotImportFromAttachments` settings will greatly increase document volumes in Relativity Trace.
{: .info}

- **Discover Monitored Individuals:** See [Discovery of Monitored Individuals](#discovery-of-monitored-individuals)
- **Include Monitored Individuals Not Linked to Data Source:** See [Discovery of Monitored Individuals](#discovery-of-monitored-individuals)
- **Discover Monitored Individuals Ignores Case:** See [Discovery of Monitored Individuals](#discovery-of-monitored-individuals)
- **Last Error Retention In Hours:** The length of time to persist any message in the `Last Error` field.
- **Aip Application Id:** See [Trace and Azure Information Protection](#trace-and-azure-information-protection) 
- **Aip Tenant Id:** See [Trace and Azure Information Protection](#trace-and-azure-information-protection)

### Data Source Auto-Disable

Trace will automatically disable data sources that are identified as unhealthy or have critical configuration errors that will require intervention by the user. Trace will automatically disable a data source for the following reasons:

- Data source has not had any successful data batches in a configured amount of time (default 24 hours)
- Globanet data source is enabled without enabling Globanet (Merge1) at the workspace level

Auto-disabled data sources will have their Disabled Reason field populated to show that it was disabled by the system. The data source will also have error details outlining the failures that caused the system to disable it.