---
layout: default
title: Refinitiv Eikon Chat and FXT
nav_exclude: true

---

# Refinitiv Eikon Chat and FXT

{: .no_toc }

This topic provides details on how to capture Refinitiv Eikon Chat and FXTs via Collect.
{: .fs-6 .fw-300 }

1. TOC

{:toc}

---

## Considerations

### Current Limitations 

- Chat2email functionality no longer supported by Refinitiv.
- Not filtering out history requests. 

### Data Filtering

There are two levels of filtering data: 

- **Data Source** - Data is being filtered according to specified Monitored Individuals. No filter is applied at message level. So, if MI exists in a channel, we will ingest the whole conversation for a given slice. If conversation does not have any Mis in participants for that day, we don’t ingest conversation at all. 
- **Data Batch** - Only messages with data for the date that matches Data Batch collection period will be captured. For e.g., a message that has been exported for 10/1/2021 will be captured by the Data Batch that has collection period from “10/1/2021 00:00” to “10/2/2021 00:00”. 

## Information Captured

### Metadata 

In addition to standard metadata populated during extracting data, the Eikon Messanger Source captures the following ones: 

| Field                                       | Description                                                  |
| ------------------------------------------- | ------------------------------------------------------------ |
| DATE                                        | Start date of a chat or start date of a slice in the chat split into slices. |
| SUBJECT                                     | Friendly name of the team and channel.                       |
| FROM                                        | The first person to send a message in that respective slice. |
| TO                                          | Chat attendees.                                              |
| CONVERSATION-ID                             | The unique identifier. When creating a Data Mapping, set “Read From Other Metadata Column” to “Yes.” |
| X-RSMF-EndDate                              | Number of messages in the chat / slice. When creating a Data Mapping, set “Read From Other Metadata Column” to “Yes.” |
| Distribution list emailsX-RSMF-MessageCount | A copy of any email sent to a distribution list is captured from each mailbox that is on the distribution list. A distribution list itself is not a mailbox. |
| X-RSMF-AttachmentCount                      | Number of attachments in the chat / slice. When creating a Data Mapping, set “Read From Other Metadata Column” to “Yes.” |

## Setup instructions 

This section provides details on the prerequisites and steps for setting up this data source.

### Prerequisites

You must have the following in order to complete the setup instructions for this data source.

#### Standard prerequisites

You must have Collect installed in the workspace to set up this data source, since Collect will be used for data retrieval. 

For details on installing Collect, see [Collect]().

#### Configure Eikon Messenger 

Obtain the following information about Eikon Messenger SFTP server: 

1. Host
2. User and password

You need to whitelist the IP addresses with the data source provider (for details please refer to [IP whitelisting for Bloomberg & ICE Chat & Eikon Messenger pre-work](bookmark://_IP_whitelisting_for)) 

### Setup in Trace

The following sections provide the steps for installing Collect and configuring the data source.

#### Collect

Prior to creating the Data Source, install the Collect application and configure the appropriate instance settings by following the [Using Relativity Collect]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/using_relativity_collect.md %}) page.

#### Data source

Most parameters work the same for all Collect Data Sources. Follow the instructions from [common_collect_data_source_functionality]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/common_collect_data_source_functionality.md %}) section. 

Refinitiv Eikon Chat and FXT specific parameters: 

General section: 

- **Data Source Type:** Eikon Messenger.  

![](media/refinitiv_eikon_chat_and_fxt_viacollect/SelectItem_DataSourceType.png)

Settings section:

- **Username:** SFTP user.
- **Password:** SFTP password.
- **Host:** SFTP location.
- **Path:** Folder path on SFTP.
- **Port:** TCP port number. Default value is 22.

![](media/refinitiv_eikon_chat_and_fxt_via_collect/Settings.png)

 

