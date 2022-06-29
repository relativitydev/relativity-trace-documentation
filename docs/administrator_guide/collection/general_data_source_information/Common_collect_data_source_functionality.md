---
layout: default
title: Common Collect Data Source Functionality
nav_exclude: true
---

# Common Collect Data Source Functionality
{: .no_toc }


This topic provides information on functionality common to most or all data sources.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## IP whitelisting pre-work 

For data sources such as Bloomberg, ICE Chat, and Eikon Messenger, before you can start collection, you must be able to make a connection to the native SFTPs. 

- For every instance you need to whitelist a unique IP. 
- For multiple SFTP data sources within a single instance you need to whitelist same IP. 
- You need to whitelist IP with every Data Source provider using SFTP, with a separate request to Bloomberg and a separate request to ICE.

## Current known IPs

The following table lists all current known IPs and their regions.

| Region         | IP address                                            |
| -------------- | ----------------------------------------------------- |
| Western Europe | 51.137.31.63                                          |
| UK South       | 20.49.169.44 Changed on 8.12 to extended list         |
| UK South       | 20.90.71.165 (f45f41bb-3e0a-4ba5-8f9d-87ac18571fe3)   |
| UK South       | 20.108.81.140 (12ef80db-dd2d-4757-af5a-4e1856d4bcb9)  |
| UK South       | 20.108.81.222 (ba80b8c0-cf34-487f-be10-53f6c17266b2)  |
| UK South       | 20.49.169.44 (d3519a85-903e-4065-9dc8-f3a666c26568)   |
| UK South       | 20.108.80.206 (b1202455-5a23-477f-ba56-27d4469d8aa5)  |
| UK South       | 20.108.81.7 (5bf1d130-4154-43d2-9df4-286ff0195efa)    |
| UK South       | 20.108.80.180 (e0e80560-1348-418c-9932-d403c8af4a17)  |
| UK South       | 20.108.81.12 (4cefd6d5-9439-4030-9591-41f492f5cc46)   |
| UK South       | 20.108.80.253 (5d482b33-7441-4a72-8a80-f8195388be4e)  |
| UK South       | 20.108.80.213 (ee885425-5d9f-4b1c-8fa7-9e1dd24e311f)  |
| UK South       | 20.108.81.108 (319850e5-1785-469a-b787-be930a2b8415)  |
| UK South       | 20.108.80.3 (e23b7367-26d8-46c3-903f-37ddfe6ea852)    |
| UK South       | 20.108.81.17 (13daef45-9917-4a56-99a7-826d5b6b7e6e)   |
| UK South       | 20.108.80.199 (daabd64b-6e66-4a0c-99bd-b5589ca2d16b)  |
| UK South       | 20.108.80.251 (b98de8a5-9d81-4107-9acd-a77b78750ea6)  |
| UK South       | 20.108.82.9 (a1e9f89b-efe8-4535-9020-5c7b0b9a4e51)    |
| UK South       | 20.108.80.57 (2bf9ef5a-0c72-4184-9da0-8fc18fe37735)   |
| UK South       | 20.108.81.137 (79d7f1d0-078e-4a56-a08e-70e25c8a90a5)  |
| UK South       | 20.108.81.22 (20996acb-f11d-4936-8069-6c957db8fb60)   |
| UK South       | 20.108.81.9 (613be307-2018-458a-9003-55c9ef97b654)    |
| UK South       | 20.108.81.185 (fc5586db-6619-47c1-aa53-53aca51e0fce)  |
| UK South       | 20.108.80.165 (a381f5da-8026-49e3-b762-670c095d8b51)  |
| UK South       | 20.108.80.167 (b93f3dc7-a901-4eec-986a-e7ebd5737d5e)  |
| UK South       | 20.108.80.229 (0e12424c-5ca2-4aae-8a05-412cc4b4db5d)  |
| UK South       | 20.108.82.4 (2884d311-af9b-4978-b054-0c3b9fe47535)    |
| UK South       | 20.108.82.7 (1e55bd5c-03c1-4b50-a298-ab9f4a38912e)    |
| UK South       | 20.108.81.225 (012fd72e-bfe7-4452-a1c4-05b64f135625)  |
| UK South       | 20.108.80.120 (42cd77cd-be7a-40e7-b0d3-0902ab2c7c0e)  |
| UK South       | 20.108.80.160 (09817a51-ded7-4fee-97a5-35f1617b8e35)  |
| UK South       | 20.108.81.45 (0a306961-d290-46bf-8688-6761c3d90b0c)   |
| UK South       | 20.108.81.232 (e3bd9fe7-fbb1-4ae7-ae94-1751a3c2b014)  |
| UK South       | 20.108.81.202 (66f8bb70-7c84-4a6e-a512-0f5010d4f6da)  |
| UK South       | 20.108.80.62 (7b635276-8f3e-4ee1-9cba-8b3610c954bb)   |
| UK South       | 20.108.80.195 (83bf28da-efb3-43c1-8dfc-2c7d96d14899)  |
| UK South       | 20.108.80.230 (2b0b2735-32c7-4eac-ac1c-32432875a65a)  |
| UK South       | 20.108.81.124 (8c959027-b45d-4575-ae83-f031a799b06a)  |
| UK South       | 20.108.80.71 (7895159d-7b7e-41d7-a7c7-da3ec880fcad)   |
| UK South       | 20.108.81.33 (dd11cf42-0429-4fb4-85e4-cbd5b867fcbc)   |
| East U.S.      | 40.76.129.217 (5c8d07ec-1287-425e-a84b-f6ed8b4af86b)  |
| East U.S.      | 40.76.130.40 (aa40ce81-6737-4b26-8df3-7851df796429)   |
| East U.S.      | 40.76.130.137 (0bd925f8-bb2c-4166-9fd1-b75f48053c6e)  |
| East U.S.      | 40.76.131.166 (3cf95b31-96b7-426c-b88a-d56d0d851ac9)  |
| East U.S.      | 40.76.129.126 (bae764c1-a63e-4e95-b179-574140b42263)  |
| East U.S.      | 40.76.131.39 (1b055f96-4f8e-4ce8-a1ca-2cdd76fe31d3)   |
| East U.S.      | 40.76.131.59 (1b8b1f69-5ca1-43fe-89ea-5812c4a12a9e)   |
| East U.S.      | 40.76.130.182 (94e009c2-191f-47cb-8597-0676c673be95)  |
| East U.S.      | 40.76.130.52 (daf60382-2e00-4366-965e-e6031107dfcb)   |
| East U.S.      | 40.76.131.104 (b7acb242-9c41-4b3f-a2d5-d0b3278b3563)  |
| East U.S.      | 40.76.131.52 (adca369d-1f96-4e0d-9aa6-6106da88835c)   |
| East U.S.      | 40.76.131.128 (90b099fd-6d33-4fe7-b155-ab5e77c6980b)  |
| East U.S.      | 40.76.131.35 (70af60eb-8363-4bb7-93f2-b1b8b98488a3)   |
| East U.S.      | 40.76.129.245 (8fde9aed-0a9b-4a64-b493-37a14c5b716a)  |
| East U.S.      | 40.76.130.159 (97039629-676e-48dc-a99d-3b89e43232bc)  |
| East U.S.      | 40.76.129.219 (fc10acad-59b6-4b49-bbcb-c62a6f4c908f)  |
| East U.S.      | 40.76.130.229 (c95971b3-2522-46fe-a57c-affb1cbae2d4)  |
| East U.S.      | 40.76.129.248 (e7c02e37-fa25-4a13-b4ee-036d6aca4975)  |
| East U.S.      | 40.76.130.126 (365cd9f6-5d4b-4069-ba70-8ce37a2078d8)  |
| East U.S.      | 40.76.131.11 (a7d02a12-6eae-4545-b35e-9ba5b3a75aeb)   |
| East U.S.      | 40.76.129.122 (de71deca-2573-4792-8dc8-44cd21c3ff0d)  |
| East U.S.      | 40.76.130.46 (8331cacf-4ef7-4201-a1d7-904121ed1fcd)   |
| East U.S.      | 40.76.130.212 (71ae1399-9013-468d-8e80-7714e0f77e96)  |
| East U.S.      | 40.76.130.145 (169aa70a-9a37-4510-8944-772add905dd1)  |
| East U.S.      | 40.76.130.190 (03da8459-19a3-45e9-8e3b-9eef02b3785a)  |
| East U.S.      | 40.76.131.20 (ab95d37c-1d46-40f0-8974-ac14ed974cf3)   |
| East U.S.      | 40.76.129.31 (6253f9d5-5abc-4bee-a21b-98c3dc4d04c5)   |
| East U.S.      | 40.76.130.80 (28454479-3053-4a7a-ae33-3f6f575fb357)   |
| East U.S.      | 40.76.130.223 (574051bb-99ad-4faf-b951-f2d9845cf420)  |
| East U.S.      | 40.76.130.198 (cb43351d-76cd-4ada-8d75-9913e4258a68)  |
| East U.S.      | 40.76.131.62 (05a2c555-0c03-4ce1-83ae-1f603652779b)   |
| East U.S.      | 40.76.129.61 (b245767e-cb24-4314-a2ed-c5d46604e4d4)   |
| East U.S.      | 40.76.130.39 (cabb5b89-13b2-4064-9d7a-96cfbaf0b852)   |
| East U.S.      | 40.76.129.242 (8a1e998a-c51c-48a4-ab36-8132029dbc79)  |
| East U.S.      | 40.76.131.84 (bc8f2d46-017d-41e5-8a22-c1984f547f2d)   |
| East U.S.      | 40.76.130.178 (5dadca7f-161b-40ef-9404-bc6e5bcc6187)  |
| East U.S.      | 40.76.131.221 (74a5ac25-ad49-47dc-8ffc-46d3e4ffed0f)  |
| East U.S.      | 40.76.129.51 (014b9512-af08-419e-b4d6-d35d90cc718f)   |
| East U.S.      | 52.191.224.135 (4ed56f5e-d958-40cf-a8ee-46a078a321b4) |
| East U.S.      | 40.76.130.49 (4e42cfc1-d602-4381-87a2-aa712ee9358c)   |
| East U.S.      | 40.76.130.238 (67c135b2-3205-440e-b9cf-fc3c54f5327e)  |
| East U.S.      | 40.76.131.225 (0c992eaf-9b1b-422a-a7eb-6be9c98a9c88)  |
| East U.S.      | 40.76.131.26 (80bd6a53-21bb-4a1e-8cde-1922a3c145dc)   |
| East U.S.      | 40.76.129.196 (32ca8144-0dcb-488d-bf45-fde4de4921da)  |
| East U.S.      | 40.76.131.100 (3950bcc0-1de4-4321-bd04-1d0f35723e1b)  |
| East U.S.      | 40.76.129.28 (96d31820-bf74-4082-a051-665cfb956c4d)   |
| East U.S.      | 40.76.129.24 (4e485f95-0ad2-43bf-ad49-36e49e5f48b6)   |
| East U.S.      | 40.76.129.185 (a9490c54-15f8-4dba-ad87-51ae9cb13e1a)  |
| East U.S.      | 40.76.130.175 (717bfb2f-3a88-4830-9923-e532f22e84e0)  |
| East U.S.      | 40.76.128.55 (23d97011-2a8f-4ac7-b16e-fe10001ce1c9)   |
| East U.S.      | 40.76.129.99 (bd27c15e-4697-4c6e-8090-98d138088a01)   |
| East U.S.      | 40.76.129.235 (e60cd5aa-d6cc-4ca4-a0b3-d94a434c8915)  |
| East U.S.      | 40.76.130.143 (19bd3875-b2e8-428d-bc58-5fe2c1d5f245)  |
| East U.S.      | 40.76.130.121 (89f86edb-cbdf-4f9e-a1a0-eccc5d05d29b)  |
| East U.S.      | 40.76.131.79 (e43a2c2f-cbe7-46a3-a852-3410f1a9cfd4)   |
| East U.S.      | 40.76.130.251 (58f4270c-c5ce-40d6-aa86-3911752f4368)  |
| East U.S.      | 40.76.131.70 (1f2b6f6a-92a4-47b0-a988-01810c6de1d7)   |
| East U.S.      | 40.76.130.217 (29b665c4-71b0-42e9-8dc9-f8de42edef39)  |
| East U.S.      | 40.76.131.161 (1cbfb880-e443-48d4-a19b-ee927845423e)  |
| East U.S.      | 40.76.129.142 (8cf36018-6848-4e8a-8e9c-9ae72cd3053d)  |
| East U.S.      | 40.76.131.159 (6aac3069-698e-4e29-90cb-016e5d07168b)  |
| East U.S.      | 40.76.130.247 (8d306f73-513f-47d7-8117-9f59862a3f7e)  |
| East U.S.      | 40.76.131.97 (cec0af63-cee7-452f-8b74-5470310d8735)   |
| East U.S.      | 40.76.129.163 (46826d7c-aac7-43b0-8441-c84a7b0835ee)  |

The following is a future static IP range that is not yet enabled:

- 52.226.235.64/28 

## Data retrieval

Data is retrieved from the source via data batches. The data batch collection period is controlled by the following parameters on the data source: 

- Ingestion State - the date to which data has been retrieved. This parameter is only visible in Date Source Layout (dev).
- Frequency in Minutes - the data batch duration (size) in minutes. 

In the following example, the Frequency in Minutes was set to 240 and the Ingestion State was 00:00. Once enabled, the data source started retrieving data. During data retrieval execution, there was the first data batch created, from 00:00 to 04:00. The Ingestion State was changed to 04:00. During the next data retrieval run, there was another Batch created, from 04:00 to 08:00, and the Ingestion State was set to 08:00. Then, during two more data retrieval runs, more data batches were created, with the final Ingestion State set to 16:00. 

![](media/Common_collect_data_source_functionality/IngestionStates.png)

Now, when the Merge Batches During Cold Start is set to True, then the Data Batch collection period will be modified to improve performance. 

In the following example , a data source was run at 04:00 on Day-2. Because the Ingestion State was Day-1 00:00, there were two merged data batches created. The first was between 00:00 and 12:00 on Day-1 and the second was between 12:00 and 24:00 on Day-1. Then, there was a third data batch created to cover the remaining period from 00:00 to 04:00 on Day-2, and the Ingestion State was changed to 04:00 on Day-2. 

![](media/Common_collect_data_source_functionality/Day2IngestionStates.png)

## Collection period offset

If data is not available for retrieval immediately, the Collection Period Offset needs to be applied on the data source. For example, if chat data is available with 24-hour delay, then a 24-hour offset needs to be configured on the data source. The Collection Period Offset is controlled by the Offset in Minutes parameter on the data source. 

## Data batch split

A data batch that has completed with errors and displays a status of CompletedWithErrors will be automatically split into two Data Batches: 

- Batch #1 - the batch that contains mailboxes that were retrieved successfully. The status of this batch is Completed. There is no action that needs to be taken on it. 

- Batch #2 - the batch that contains mailboxes that were failed during data retrieval. The status of that batch is Abandoned. Depending on the reason for failure, that batch can be retried manually. 

## Message slicing – Chat only  

To handle dynamics and continuity of the communication in chat channels, Trace uses a slicing strategy to divide chats while keeping needed context for analysis. If the first message in a slice is a reply to the previously captured message, then the parent message is replaced by an empty message placeholder. 

In the following example: 

- Message sent by Hogan Lovells on 7/26/2021 12:00AM is the first message of the slice. 
- Message sent by Misha Kogan on 7/25/2021 11:58PM is the parent message, previously captured. It doesn’t contain text. 
- Start date of this slice is 7/26/201 12:00AM. 

![](media/Common_collect_data_source_functionality/MessageSlicing.png)