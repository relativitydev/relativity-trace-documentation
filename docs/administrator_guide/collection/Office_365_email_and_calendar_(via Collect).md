# **Office 365 email and calendar (via Collect)**  

Via Collect, you can use Office 365 email and calendar items as data sources. 

Deployment option B, depicted below, is required to use these data sources. 

 ![](media/Office_365_email_and_calendar_(via Collect) /DeploymentBOffice.png)

## **Mailbox collection** 

Note the following details regarding mailbox collection: 

- The connector supports accessing active, licensed mailboxes. It does not support accessing inactive and archived mailboxes. 
  - Archived collection to be included in a future release. 
- Hidden folders cannot be collected. 
- Deleted items can be collected. 
  - Users must set their "Deleted items retention" to at least 14 days (MSFT default). 

  - If this is not set, Trace cannot collect data that has been “triple deleted by user.” 
- Permanently deleted items can be collected. 
- Shared mailboxes can be collected if they are active. 
- Distribution lists: a copy of any email sent to distribution lists will be picked up from each mailbox that is on the distribution list; a distribution list itself is not a mailbox. 
- Guest accounts can only be collected if they are active & licensed. 

 Note the following current limitations: 

- Archive folder 

  - Currently we are not capturing archive folder. 

  - New O365 Archive Data Source which will be released on May 24th will allow collection) 

- Formatted text is captured as plain text. 
- Numbered rows are captured as a single line. 
- Participant leaving/being deleted from the channel event not collected (participant is captured only if wrote a message). 
- Team meetings captured as message placeholder. 
- Emojis are collected as plain text. 

## **Activities captured** 

The following activities are captured: 

- Messages with attachments 
- Meeting Requests 
- Meeting Cancellations 

- Calendar events (vCalendar) 

## **Data Filtering** 

There are two levels of filtering data: 

- **Data Source** - only data linked to a Data Source Monitored Individuals will be captured. 

- **Data Batch** - only messages which have “Date Received” within Data Batch collection period will be captured. 

## **License Requirements** 

The following license is required: 

- Microsoft 365 E3 or higher (if E3, also need the compliance module) 

- You can collect from unlicensed custodians 

- The mailbox must still be active in the case where the user is unlicensed 

## **Configuring Collect** 

Collect is used for data retrieval. Make sure Collect is installed in the workspace before configuring the data source. 

For detailed installation steps see Installing Collect. 

## **Authorizing Azure** 

Before configuring the data source, register your app through the following steps: 

1. Open your [Azure Portal](https://portal.azure.com/). 

1. Click **More Services**. 

1. Search for and select **Azure Active Directory**. 

1. In the left-navigation menu, click **App registrations**. 

1. Click **New Registration**. This will open the Register an application page. 

1. Enter an application name in the **Name** field. 

1. Select **Accounts** in this organizational directory only as the supported account type. 

1. Enter the redirect URL, http://localhost/ or https://localhost/, as the sign-on URL. 

1. Click **Register**. For more information on registering an application in Azure, see [Microsoft's documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app). 

 From the app's page, add permissions to the web API through the following steps: 

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

 Grant Admin consent for the API through the following steps: 

1. Click the **API Permissions** tab. 
2. Click **Grant admin consent** for [tenant]. 
3. In the pop-up window, click **Accept**. If you do not have the ability to grant Admin consent for application permissions, you will need to find an Admin that can consent. 
4. Once clicked, the window will show all permissions granted. 
5. Verify all permissions have been granted. 
6. Click **Accept** to grant the permissions. 
7. In the left navigation menu, select **Certificates & secrets**. 
8. Select **New client secret**. 

![](media/Office_365_email_and_calendar_(via Collect) /NewClientSecret.png)

9. Enter a description in the **Description** text box. 
10. Set the expiration time frame to **Never**. 
11. Click **Add**. 

12. Click on the clipboard and copy secret to clipboard to paste in your text document. 

    - You should copy the secret and save it, as you will need it to set up your data sources in Trace. Microsoft will only show this secret this one time; there is no way to recover a secret if it is forgotten or lost. Make a note of the Application ID that Microsoft assigned to the app registration. This ID is also required for setup of data sources in Trace. 

    - You will need the following information to complete setup of the data source from the Trace front end: 

      - Application ID 

      - Client Secret (copy the **Value** field) 

      - Domain e.g., mycompanydomain.com 

 Limit the access of Relativity Collect to specific Microsoft user accounts and mailboxes by using the New-ApplicationAccessPolicy Powershell cmdlet. For more information, see [Microsoft documentation](https://docs.microsoft.com/en-us/graph/auth-limit-mailbox-access). 

**Configuring the data source** 

Most parameters work the same for all Collect Data Sources. Follow the instructions from [Common Collect Data Source Functionality](https://usc-word-edit.officeapps.live.com/we/wordeditorframe.aspx?ui=en-US&rs=en-US&wopisrc=https%3A%2F%2Fkcura-my.sharepoint.com%2Fpersonal%2Fdavid_bachmann_relativity_com%2F_vti_bin%2Fwopi.ashx%2Ffiles%2F8077c5fa29d1469ea6506ce3df735cdd&wdenableroaming=1&mscc=1&wdodb=1&hid=8AFF3CA0-908D-1000-AACB-EFC268F94A9E&wdorigin=ItemsView&wdhostclicktime=1652451692337&jsapi=1&jsapiver=v1&newsession=1&corrid=29e99580-431c-435c-8525-71c6894c27b1&usid=29e99580-431c-435c-8525-71c6894c27b1&sftc=1&cac=1&mtf=1&sfp=1&instantedit=1&wopicomplete=1&wdredirectionreason=Unified_SingleFlush&rct=Medium&ctp=LeastProtected#_Common_Collect_Data) section. 

O365 Mail and Calendar specific parameters: 

General section: 

1. **Data Source Type**: Select Microsoft O365 Mail or Calendar. 

![](media/Office_365_email_and_calendar_(via Collect) /DataSourceType.png)

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


 ![](media/Office_365_email_and_calendar_(via Collect) /DataSourceSpecificFields.png)

