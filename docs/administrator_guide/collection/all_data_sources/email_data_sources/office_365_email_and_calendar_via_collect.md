---
layout: default
title: Microsoft Office 365 Email and Calendar
nav_exclude: true
---

# Microsoft Office 365 Email and Calendar
{: .no_toc }

This topic provides details on how to capture Microsoft Office 365 Email and Calendar messages via Collect.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Requirements 

Before using this data source, note the following license requirements, version support, and special considerations.

### License requirements

The following licenses are required to use this data source:

- Microsoft 365 E3 or higher is required.
  - If you are using Microsoft 365 E3, you also need to add the Compliance module. 

### Versions supported

We support Microsoft 365 Enterprise 3 and above.

## Considerations

Note the following considerations about this data source:

### Mailbox Collection
- The connector only supports accessing active mailboxes.
- The connector does **NOT** support collection from Archive mailboxes
- You can collect from unlicensed custodians, but the mailbox must still be active in the case where the user is unlicensed.
- Guest mailboxes can only be collected if they are active & licensed.
- Shared mailboxes can only be captured if they are active.

The Microsoft Office O365 Archive data source should always be enabled alongside the Microsoft Office 365 Email and Calendar data source to ensure holistic collection is performed. Without Microsoft Office O365 Archive data source enabled you may miss data that is quickly archived either by a rule or manual action.
{: .warn}

### Email Collection
- The connector collects all items in visible folders within Outlook’s inbox and custom folders. 
- Deleted items can be collected. 
- Deleted items from deleted folder (deleted and purged items) can be collected. Users must set their "Deleted items retention" to at least 14 days (Microsoft default). 
- Hidden folders cannot be collected. 

### Email Content
- Formatted text is captured as plain text. 
- Numbered rows are captured as a single line. 
- Emojis are collected as plain text. 
  
### Data Filtering
- There are two levels of filtering data: 
  - Data Source - only data linked to a Data Source Monitored Individuals will be captured. 
  - Data Batch - only messages which have “Date Received” within Data Batch collection period will be captured. 

## Information captured 

This section lists what activities and, if applicable, metadata are captured when you use this data source.

### Activities captured

The following table lists activities captured by this data source:

| Activity                    | Notes                                                        |
| --------------------------- | ------------------------------------------------------------ |
| Messages with attachments   | A participant is only captured if they wrote a message.      |
| Meeting request             | A team meeting request is captured as a message placeholder. |
| Meeting cancellations       |                                                              |
| Calendar events (vCalendar) |                                                              |
| Deleted items               | Users must set their Deleted items retention to at least 14 days (MSFT default).  If this is not set, Trace cannot collect data that has been triple deleted by user. |
| Permanently deleted items   |                                                              |
| Distribution list emails    | A copy of any email sent to a distribution list is captured from each mailbox that is on the distribution list. A distribution list itself is not a mailbox. |

### Activities not captured

The following table lists activities not captured by this data source:

| Activity not captured            | Notes                                                        |
| -------------------------------- | ------------------------------------------------------------ |
| Participant removed from channel | A participant who leaves or is removed from a channel event is not captured. The participant is captured only if they wrote a message |
| Distribution lists               | A distribution list itself is not a mailbox.                 |

## Setup instructions

This section provides details on the prerequisites and steps for setting up this data source.

### Prerequisites

You must have the following in order to complete the setup instructions for this data source.

#### Standard prerequisites

You must have Collect installed in the workspace to set up this data source, since Collect will be used for data retrieval. 

For details on installing Collect, see [Collect]().

#### Company specific prerequisites

You must have the following company-provided information to complete the authentication steps that precede setting up the data source:

- Access to the Azure portal and an active account
- A Client Secret
- An O365 domain name
- An Application / Client ID

#### Data transfer prerequisites

You must have the following information to complete the data transfer.

- An application ID
- A Client secret
- An O365 domain name

### Authentication

Before configuring the data source complete the following authentication steps. 

We strongly recommend registering a separate Azure Application for each Data Source.
{: .info }

To register your app:
1. Open your [Azure Portal](https://portal.azure.com/). 
1. Click **More Services**. 
1. Search for and select **Azure Active Directory**. 
1. In the left-navigation menu, click **App registrations**. 
1. Click **New Registration**. This will open the Register an application page. 
1. Enter an application name in the **Name** field. 
1. Select **Accounts** in this organizational directory only as the supported account type. 
1. Enter the redirect URL, http://localhost/ or https://localhost/, as the sign-on URL. 
1. Click **Register**. For more information on registering an application in Azure, see [Microsoft's documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app). 

From the app's page, add permissions to the web API: 
1. Click **API Permissions**. 
2. Click **Add a permission**. 
3. Click **Microsoft Graph**. 
4. Select **Application Permissions**. 
5. Select the following options from the **Application Permissions** section: 
   - **Mail** - Read. 
   - **User** - Read.All 
   - **Calendars** - Read. For the Email only option, this permission is not needed 

6. Click **Add permissions**. 
7. Click **Grant Permission**. 

Grant Admin consent for the API: 
1. Click the **API Permissions** tab. 
2. Click **Grant admin consent** for [tenant]. 
3. In the pop-up window, click **Accept**. If you do not have the ability to grant Admin consent for application permissions, you will need to find an Admin that can consent. 
4. Once clicked, the window will show all permissions granted. 
5. Verify all permissions have been granted. 
6. Click **Accept** to grant the permissions. 

Generate Client Secret:
1. In the left navigation menu, select **Certificates & secrets**. 
2. Select **New client secret**.
3. Enter a description in the **Description** text box. 
4. Set the expiration time frame to **Never**. 
5. Click **Add**. 
6. Click on the clipboard and copy secret to clipboard to paste in your text document. Save this secret, as you will need it to set up your data sources in Trace. 

Microsoft will only show this secret this one time; there is no way to recover a secret if it is forgotten or lost. Make a note of the Application ID that Microsoft assigned to the app registration. This ID is also required for setup of data sources in Trace.
{: .info }

You will need the following information to complete setup of the data source from the Trace front end: 
  - Application ID 
  - Client Secret (copy the **Value** field) 
  - Domain (mycompanydomain.com)

Make sure you copy the **Value** field item for your Client Secret. Do not accidentally copy the Secret ID item as this is not the your Client Secret.
{: .warn }

Limit the access of Relativity Collect to specific Microsoft user accounts and mailboxes by using the New-ApplicationAccessPolicy Powershell cmdlet. For more information, see [Microsoft documentation](https://docs.microsoft.com/en-us/graph/auth-limit-mailbox-access).
{: .info }

### Setup in Trace

The following sections provide the steps for installing Collect and configuring the data source.

#### Collect

Before configuring the required instance settings and the data source, install the Collect RAP from the Application Library in Relativity via the following steps.

 ![](media/Office_365_email_and_calendar_via%20Collect/InstallCollectApp.png)

1. Navigate to the workspace where you want to install the application.
2. Navigate to the **Application Admin** tab.
3. Click **New Relativity Application** to display an application form.
4. Click the **Select from Application Library** radio button in the Application Type section.
5. Click the ellipses in the **Choose from Application Library** field.
6. Select **Collect** on the Select Library Application dialog. This dialog only displays applications added to the Application Library. 
7. Click Ok to display the application in the Choose from Application Library field.
8. Click **Import** to install Collect into the workspace.
9. Review the import status of the application. Verify that the install was successful or resolve errors.

##### Instance settings

Configure the following instance settings: 

- Configure Collect Queue Depth: 

- **Name**: MaxNumberOfRunningStandaloneCollections 
- **Section**: Relativity.Collection 
- **Value Type**: Integer 32-bit 
- **Value**: 10 

 ![](media/Office_365_email_and_calendar_via%20Collect/CollectInstanceSetting1.png)

Configure Data Batch Automatic Retry Policy: 

- **Name**: TraceWorkspaceSetting 
- **Section**: Trace.Workspace 
- **Value Type**: Text 
- **Value**: “DataBatchRetryIntervals”:[10,30,60] 

 ![](media/Office_365_email_and_calendar_via%20Collect/CollectInstanceSetting2.png)

Toggle On/Off Auto Batch Split functionality: 

- **Name**: EnableCollectDataBatchSplit. 
- **Section**: Trace.Workspace. 
- **Value Type**: True/False. 
- **Value**: False (auto split disabled) or True (auto split enabled). 

![](media/Office_365_email_and_calendar_via%20Collect/CollectInstanceSetting3.png)

#### Data source

Most parameters work the same for all Collect Data Sources. Follow the instructions from [Common Collect Data Source Functionality](https://usc-word-edit.officeapps.live.com/we/wordeditorframe.aspx?ui=en-US&rs=en-US&wopisrc=https%3A%2F%2Fkcura-my.sharepoint.com%2Fpersonal%2Fdavid_bachmann_relativity_com%2F_vti_bin%2Fwopi.ashx%2Ffiles%2F8077c5fa29d1469ea6506ce3df735cdd&wdenableroaming=1&mscc=1&wdodb=1&hid=8AFF3CA0-908D-1000-AACB-EFC268F94A9E&wdorigin=ItemsView&wdhostclicktime=1652451692337&jsapi=1&jsapiver=v1&newsession=1&corrid=29e99580-431c-435c-8525-71c6894c27b1&usid=29e99580-431c-435c-8525-71c6894c27b1&sftc=1&cac=1&mtf=1&sfp=1&instantedit=1&wopicomplete=1&wdredirectionreason=Unified_SingleFlush&rct=Medium&ctp=LeastProtected#_Common_Collect_Data) section. 

O365 Mail and Calendar specific parameters: 

General section: 

1. **Data Source Type**: Select Microsoft O365 Mail or Calendar. 

​	![](media/Office_365_email_and_calendar_via_Collect/DataSourceType.png)

Credentials section: 

1. **Application Secret:** The Client Secret provided by the client (see [Authentication (Set up Azure Application)](https://usc-word-edit.officeapps.live.com/we/wordeditorframe.aspx?ui=en-US&rs=en-US&wopisrc=https%3A%2F%2Fkcura-my.sharepoint.com%2Fpersonal%2Fdavid_bachmann_relativity_com%2F_vti_bin%2Fwopi.ashx%2Ffiles%2F8077c5fa29d1469ea6506ce3df735cdd&wdenableroaming=1&mscc=1&wdodb=1&hid=8AFF3CA0-908D-1000-AACB-EFC268F94A9E&wdorigin=ItemsView&wdhostclicktime=1652451692337&jsapi=1&jsapiver=v1&newsession=1&corrid=29e99580-431c-435c-8525-71c6894c27b1&usid=29e99580-431c-435c-8525-71c6894c27b1&sftc=1&cac=1&mtf=1&sfp=1&instantedit=1&wopicomplete=1&wdredirectionreason=Unified_SingleFlush&rct=Medium&ctp=LeastProtected#Step) for more details). 
2. Data Source Specific Fields section (see also [Common Collect Data Source Functionality](https://usc-word-edit.officeapps.live.com/we/wordeditorframe.aspx?ui=en-US&rs=en-US&wopisrc=https%3A%2F%2Fkcura-my.sharepoint.com%2Fpersonal%2Fdavid_bachmann_relativity_com%2F_vti_bin%2Fwopi.ashx%2Ffiles%2F8077c5fa29d1469ea6506ce3df735cdd&wdenableroaming=1&mscc=1&wdodb=1&hid=8AFF3CA0-908D-1000-AACB-EFC268F94A9E&wdorigin=ItemsView&wdhostclicktime=1652451692337&jsapi=1&jsapiver=v1&newsession=1&corrid=29e99580-431c-435c-8525-71c6894c27b1&usid=29e99580-431c-435c-8525-71c6894c27b1&sftc=1&cac=1&mtf=1&sfp=1&instantedit=1&wopicomplete=1&wdredirectionreason=Unified_SingleFlush&rct=Medium&ctp=LeastProtected#_Common_Collect_Data)): 
   - **Collect Draft items**: True or False (default)**.** False is default setting due to the nature of drafts (they are not sent we don’t want to risk false positives). 
   - **Domain**: The O365 domain name provided by the client. 
   - **Application Id**: Application / Client ID provided by the client. 
   - **Use Quick Discovery**: True 
   - **Frequency in Minutes**: 60 
   - **Number of Monitored Individual Per job**: 100 
   - **Collection Period Offset in Minutes**: 0 

 ![](media/Office_365_email_and_calendar_via_Collect/DataSourceSpecificFields.png)
