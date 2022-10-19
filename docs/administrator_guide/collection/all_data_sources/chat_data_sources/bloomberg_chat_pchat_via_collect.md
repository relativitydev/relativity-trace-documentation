---
layout: default
title: Bloomberg Chat and PChat
nav_exclude: true
---

# Bloomberg Chat and PChat
{: .no_toc }

Collect Bloomberg Chat and PChat messages via Relativity Collect.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---
 
## Overview

The connector is pulling data directly from Cloud.

![](media/BloombergChatPchat_viaCollect/BloomChat_DeplymtB_Diagrm.png)

## Versions Supported

We support 1.3 as well as the latest 1.9 version.

## Activities Captured

The following activities are captured:
- Attachments (.att).
- Disclaimers (.dscl).
- Instant Bloomberg Messages (Chat & PChat) (.ib).

## Metadata

In addition to standard (O365 Mail) metadata populated during extracting data, the Bloomberg Chat Data Source captures the following ones:
- **DATE** - start date of a chat or start date of a slice in the chat split into slices.
- **SUBJECT** - friendly name of the team and channel.
- **FROM** - the first person to send a message in that respective slice.
- **TO** - chat attendees.
- **CONVERSATION-ID** - the unique identifier. When creating a Data Mapping, set “Read From Other Metadata Column” to **Yes**.
- **X-RSMF-EndDate** - end date of the chat / slice. When creating a Data Mapping, set “Read From Other Metadata Column” to **Yes**.
- **X-RSMF-EventCount** - number of messages in the chat / slice. When creating a Data Mapping, set “Read From Other Metadata Column” to **Yes**.
- **X-RSMF-AttachmentCount** - number of attachments in the chat / slice. When creating a Data Mapping, set “Read From Other Metadata Column” to **Yes**.

## Document View

Bloomberg Chat messages are captured as RMFS (Relativity Short Message Format) files. Relativity has created a Viewer experience to help reviewing RSMF data. See [Relativity Short Message Format](https://help.relativity.com/RelativityOne/Content/System_Guides/Relativity_Short_Message_Format/Relativity_Short_Message_Format.htm) for more details.

![](media/BloombergChatPchat_viaCollect/BloomChat_DocumtView.png)

## Data Filtering

There are two levels of filtering data, which are the same for Bloomberg Mail (via Collect):

- **Data Source -** Data is being filtered according to specified Monitored Individuals (MI). No filter is applied at the message level. So, if MI exists in a channel, we will ingest the whole conversation for a given slice. If the conversation does not have any MIs in participants for that day, we do not ingest conversation at all.

- **Data Batch -** Only messages with data for the date that matches Data Batch collection period will be captured. For example, a message that has been exported for 10/1/2021 will be captured by the Data Batch that has collection period from “10/1/2021 00:00” to “10/2/2021 00:00”.

## Setup in Trace

This section provides details on the prerequisites and steps for setting up this data source.

### Obtaining Credentials

Obtain the following information about the Bloomberg SFTP server:
- Host name.
- Path.
- TCP Port.
- Username and password.

If Bloomberg messages are encrypted, then obtain the following information:
- PGP Key (Private Key is required).
- Passphrase (used to encrypt/decrypt PGP key).

### Whitelist Relativity IP Addresses

Bloomberg must add Relativity IP addresses to a whitelist so the system can connect and collect data. Please refer to the [IP Address Whitelisting Pre-work](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/collection/general_data_source_information/common_collect_data_source_functionality.html#ip-address-whitelisting-pre-work) for more details.

### Collect

Prior to creating the Data Source, install the Collect application and configure the appropriate instance settings by following the [Using Relativity Collect](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/collection/general_data_source_information/using_relativity_collect.html) page.

### Data source

Most parameters work the same for all Collect Data Sources. Follow the instructions from [Sections of a Data Source]( https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/collection/data_sources.html#data-source-details).

**Bloomberg Chat specific parameters:**

In **General** section, select **Bloomberg Chat** for the **Data Source Type**.

![](media/BloombergChatPchat_viaCollect/General_BloomChat_DataSourceType.png)

In **Settings** section, do the following:

1. **Use Unc Path**:
    - **False** - if data is collected from external SFTP server.
    - **True** - if data is collected directly from the RelativityOne Fileshare. Use this option if client is dropping data directly to Fileshare using SFTP server hosted by Relativity.
2. **Use PGP Encryption** - select this check box to decrypt a source file with the PGP Key and PGP Passphrase; otherwise, leave it blank.
3. **PGP Key** - if **Use PGP Encryption** is set to **True**, enter the PGP Key used for message encryption. Otherwise, leave it empty.

For instance, if the PGP/GPG key looks like below:
```
-----BEGIN PGP PRIVATE KEY BLOCK-----
lQdGBGKRw94BEADeO1Fle0W0lqki3DyVDOfVcHXRzWl6TpVxlZO7mxLYDp/myUzK
1txcDvMzF506zK6cmeIkanpDkWjoVP6kpopRbQfhF9UMNUURPw416ORhxiQ4eDX2
W6Tf7Sxgjm/jI9RAooXT938DbKRPcIgRL5nLuaQXvL7WxZVa2Y6jyxt1uG9w7ZUQ
WEMqau6d3+B6q+g0WZg2tPkmQI84LCGio3uo/WpjjLWdOeUJjB/rR+3bFwxNOCCwX
...
CCZ0nburBylUt7VEjjvIuMWsaCC3GYhjvM8owUExAGrns4+FHeGQ6wmtVRH/Ekqf
3GIW6fh0/KXLsDhNnG2ZA+doI0Eg6j4UGZQMFkdmeYlL+6xlE28SWxFY4JZ79NBo
j5r+T+V2idFXxw==
=pDiN
-----END PGP PRIVATE KEY BLOCK-----
-----BEGIN PGP PUBLIC KEY BLOCK-----mQINBGKRw94BEADeO1Fle0W0lqki3DyVDOfVcHXRzWl6TpVxlZO7mxLYDp/myUzK
1txcDvMzF506zK6cmeIkanpDkWjoVP6kpopRbQfhF9UMNUURPw416ORhxiQ4eDX2
W6Tf7Sxgjm/jI9RAooXT938DbKRPcIgRL5nLuaQXvL7WxZVa2Y6jyxt1uG9w7ZUQ
WEMqau6d3+B6q+g0WZg2tPkmQI84LCGio3uo/WpjjLWdOeUJjB/rR+3bFwxNOCCw
...
h/67uxBLZP9BEyk+UYsIJnSdu6sHKVS3tUSOO8i4xaxoILcZiGO8zyjBQTEAauez
j4Ud4ZDrCa1VEf8SSp/cYhbp+HT8pcuwOE2cbZkD52gjQSDqPhQZlAwWR2Z5iUv7
rGUTbxJbEVjglnv00GiPmv5P5XaJ0VfH
=D22y
-----END PGP PUBLIC KEY BLOCK-----
```

Only text between BEGIN PGP PRIVATE KEY BLOCK and END PGP PRIVATE KEY BLOCK needs to be entered:

```
lQdGBGKRw94BEADeO1Fle0W0lqki3DyVDOfVcHXRzWl6TpVxlZO7mxLYDp/myUzK
1txcDvMzF506zK6cmeIkanpDkWjoVP6kpopRbQfhF9UMNUURPw416ORhxiQ4eDX2
W6Tf7Sxgjm/jI9RAooXT938DbKRPcIgRL5nLuaQXvL7WxZVa2Y6jyxt1uG9w7ZUQ
WEMqau6d3+B6q+g0WZg2tPkmQI84LCGio3uo/WpjjLWdOeUJjB/rR+3bFwxNOCCwX
```
```
CCZ0nburBylUt7VEjjvIuMWsaCC3GYhjvM8owUExAGrns4+FHeGQ6wmtVRH/Ekqf
3GIW6fh0/KXLsDhNnG2ZA+doI0Eg6j4UGZQMFkdmeYlL+6xlE28SWxFY4JZ79NBo
j5r+T+V2idFXxw==
```

4. **Passphrase** - if **Use PGP Encryption** is set to **True**, enter the PGP Passphrase used for message encryption. Otherwise, leave it empty.

Other parameter values depend on **Use Unc Path** setting.

If **Use Unc Path** is set to **False**:

5. **Username** - enter the SFTP username.
6. **Password** - enter the SFTP password.
7. **Host** - enter the SFTP location.
8. **Path** - enter the folder path on the SFTP.
9. **Port** - enter the TCP port number. Default value is 22.

![](media/BloombergChatPchat_viaCollect/BloomChat_CredentialsTab.png)

If **Use Unc Path** is set to **True**:

5. **Username** - leave empty.
6. **Password** - leave empty.
7. **Host** - leave empty.
8. **Path** - enter the folder path on the RelativityOne Fileshare relative to workspace folder. Usually it will be drop folder exposed in internal SFTP server. For example *DataTransfer/Import/SFTP/BloombergChat/Drop* (while SFTP server is set up to expose following path relative to Fileshare: */Files/EDDS1020064/DataTransfer/Import/SFTP* where *EDDS1020064* is a workspace where data source is created).
9. **Port** - enter any intiger value e.g. **22**.

In **Advanced Configuration** section, do the following:

If **Use Unc Path** is set to **False**:

1. **Batch Size** - enter 1.
2. **Frequency in Minutes** - enter 1440.
3. **Merge Batches During Cold Start**: enter True.
4. **Max Number of Batches To Merge** - enter 1.
5. **Collection Period Offset in Minutes** - enter 1440.

If **Use Unc Path** is set to **True**:

1. **Batch Size** - enter 1.
2. **Frequency in Minutes** - enter 480.
3. **Merge Batches During Cold Start**: enter True.
4. **Max Number of Batches To Merge** - enter 1.
5. **Collection Period Offset in Minutes** - enter 0.