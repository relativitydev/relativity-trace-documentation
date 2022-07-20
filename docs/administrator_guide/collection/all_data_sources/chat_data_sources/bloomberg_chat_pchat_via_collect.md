---
layout: default
title: Bloomberg Chat and PChat
nav_exclude: true
---

# Bloomberg Chat and PChat
{: .no_toc }

This topic provides details on how to capture Bloomberg Chat and PChat messages  via Collect. 
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Requirements
Before using this data source, note the following license requirements, version support, and special considerations.

### Versions Supported

We support 1.3 as well as the latest 1.9 version.

## Considerations

### Data Filtering

There are two levels of filtering data, which are the same for Bloomberg Chat (via Collect):

- **Data Source -** Data is being filtered according to specified Monitored Individuals (MI). No filter is applied at the message level. So, if MI exists in a channel, we will ingest the whole conversation for a given slice. If the conversation does not have any MIs in participants for that day, we do not ingest conversation at all.

- **Data Batch -** Only messages with data for the date that matches Data Batch collection period will be captured. For example, a message that has been exported for 10/1/2021 will be captured by the Data Batch that has collection period from “10/1/2021 00:00” to “10/2/2021 00:00”.

## Information captured

This section lists what activities and, if applicable, metadata are captured when you use this data source.

### Activities captured

The following activities are captured by this data source:

- Attachments (.att)
- Disclaimers (.dscl)
- Instant Bloomberg Messages (Chat & PChat) (.ib)

### Metadata captured

The following table lists metadata captured by this data source:

| Field                  | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| DATE                   | Start date of a chat or start date of a slice in the chat split into slices |
| SUBJECT                | Friendly name of the team and channel                        |
| FROM                   | The first person to send a message in that respective slice  |
| TO                     | Chat attendees                                               |
| CONVERSATION-ID        | Unique identifier. When creating a data mapping, set **Read From Other Metadata Column** to Yes. |
| X-RSMF-EndDate         | End date of the chat/slice. When creating a data mapping, set **Read From Other Metadata Column** to Yes. |
| X-RSMF-MessageCount    | Number of messages in the chat/slice. When creating a data mapping, set **Read From Other Metadata Column** to Yes. |
| X-RSMF-AttachmentCount | Number of attachments in the chat/slice. When creating a data mapping, set **Read From Other Metadata Column** |

## Setup Instructions

### Prerequisites

Obtain the following information about the Bloomberg SFTP server:

- Host name and Port number
- Username and password

If Bloomberg messages are encrypted, then obtain the following information:

- PGP Key (Private Key is required)
- Passphrase (used to encrypt/decrypt PGP key)

 ### Setup in Trace

The following sections provide the steps for installing Collect and configuring the data source.

#### Collect
Prior to creating the Data Source, install the Collect application and configure the appropriate instance settings by following the [Using Relativity Collect]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/using_relativity_collect.md %}) page.

#### Data source

Most parameters work the same for all Collect Data Sources. Follow the instructions from [common_collect_data_source_functionality]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/common_collect_data_source_functionality.md %}) section. 

Bloomberg Chat specific parameters: 

General section: 

- Data Source Type: **Bloomberg Chat**.

![](media/bloomberg_chat_pchat_via_collect/General_BloomChat_DataSourceType.png)

Credentials section: 

![](media/bloomberg_chat_pchat_via_collect/BloomChat_CredentialsTab.png)

**Username**: Enter the SFTP username.

**Password**: Enter the SFTP password.

**PGP Key**: Enter the PGP Key used for message encryption.

For instance, if the PGP/GPG looks like below, only the information between the Begin PGP Private Key Block and End PGP Private Key Block needs to be entered.

 ``-----BEGIN PGP PRIVATE KEY BLOCK-----lQdGBGKRw94BEADeO1Fle0W0lqki3DyVDOfVcHXRzWl6TpVxlZO7mxLYDp/myUzK`
 `1txcDvMzF506zK6cmeIkanpDkWjoVP6kpopRbQfhF9UMNUURPw416ORhxiQ4eDX2`
 `W6Tf7Sxgjm/jI9RAooXT938DbKRPcIgRL5nLuaQXvL7WxZVa2Y6jyxt1uG9w7ZUQ`
 `WEMqau6d3+B6q+g0WZg2tPkmQI84LCGio3uo/WpjjLWdOeUJjB/rR+3bFwxNOCCwX`
 `...`
 `CCZ0nburBylUt7VEjjvIuMWsaCC3GYhjvM8owUExAGrns4+FHeGQ6wmtVRH/Ekqf`
 `3GIW6fh0/KXLsDhNnG2ZA+doI0Eg6j4UGZQMFkdmeYlL+6xlE28SWxFY4JZ79NBo`
 `j5r+T+V2idFXxw==`
 `=pDiN`
 -----END PGP PRIVATE KEY BLOCK-----`
 ``-----BEGIN PGP PUBLIC KEY BLOCK-----mQINBGKRw94BEADeO1Fle0W0lqki3DyVDOfVcHXRzWl6TpVxlZO7mxLYDp/myUzK`
 `1txcDvMzF506zK6cmeIkanpDkWjoVP6kpopRbQfhF9UMNUURPw416ORhxiQ4eDX2`
 `W6Tf7Sxgjm/jI9RAooXT938DbKRPcIgRL5nLuaQXvL7WxZVa2Y6jyxt1uG9w7ZUQ`
 `WEMqau6d3+B6q+g0WZg2tPkmQI84LCGio3uo/WpjjLWdOeUJjB/rR+3bFwxNOCCw`
 `...`
 `h/67uxBLZP9BEyk+UYsIJnSdu6sHKVS3tUSOO8i4xaxoILcZiGO8zyjBQTEAauez`
 `j4Ud4ZDrCa1VEf8SSp/cYhbp+HT8pcuwOE2cbZkD52gjQSDqPhQZlAwWR2Z5iUv7`
 `rGUTbxJbEVjglnv00GiPmv5P5XaJ0VfH`
 `=D22y`
 -----END PGP PUBLIC KEY BLOCK-----`

**Passphrase**: Enter the PGP Passphrase used for message encryption.

Data Source Specific Fields section:

![](media/bloomberg_chat_pchat_via_collect/BloomChat_DataSourceSpecificFields.png)



- **Host**: Enter the SFTP location.
- **Path**: Enter the folder path on the SFTP.
- **Port**: The TCP port number. Default value is 22.
- **Use PGP Encryption**: Select this check box to decrypt a source file with the PGP Key and PGP Passphrase; otherwise, leave it blank.
- **Frequency in Minutes**: 1440
- **Max Number of Batches To Merge**: 1
- **Collection Period Offset in Minutes**: 1440
