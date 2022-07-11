---
layout: default
title: Data Source Template
nav_exclude: true
---

# Data Source Template
{: .no_toc }

This topic provides details on how to capture XYZ data sources via Collect.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Requirements 

Before using this data source, note the following license requirements, version support, and special considerations.

### License requirements

The following licenses are required to use this data source:

- XYZ

### Versions supported

We support XYZ version and above.

## Considerations

Note the following considerations about this data source:

### Mailbox Collection
- The connector only supports XYZ

### Email Collection
- The connector collects all items XYZ

### Email Content
- Formatted text is captured as XYZ
  
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

### Activities not captured

The following table lists activities not captured by this data source:

| Activity not captured            | Notes                                                        |
| -------------------------------- | ------------------------------------------------------------ |
| Participant removed from channel | A participant who leaves or is removed from a channel event is not captured. The participant is captured only if they wrote a message |

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

#### Data transfer prerequisites

You must have the following information to complete the data transfer.

- An application ID

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
2. Click **Add a permission**

Grant Admin consent for the API: 
1. Click the **API Permissions** tab. 


Generate Client Secret:
1. In the left navigation menu, select **Certificates & secrets**. 
2. Select **New client secret**.


You will need the following information to complete setup of the data source from the Trace front end: 
  - Application ID 

### Setup in Trace

The following sections provide the steps for installing Collect and configuring the data source.

#### Collect
Prior to creating the Data Source, install the Collect application and configure the appropriate instance settings by following the [Using Relativity Collect]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/using_relativity_collect.md %}) page.

#### Data source

Most parameters work the same for all Collect Data Sources. Follow the instructions from [common_collect_data_source_functionality]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/common_collect_data_source_functionality.md %}) section. 

O365 Mail and Calendar specific parameters: 

General section: 

1. **Data Source Type**: Select Microsoft O365 Mail or Calendar. 

​	![](media/Office_365_email_and_calendar_via_Collect/DataSourceType.png)

Credentials section: 

1. **Application Secret:** The Client Secret provided by the client (see [Authentication](#authentication) for more details). 
2. Data Source Specific Fields section
   - **Collect Draft items**: True or False (default)**.** False is default setting due to the nature of drafts (they are not sent we don’t want to risk false positives). 
   - **Domain**: The O365 domain name provided by the client. 
   - **Application Id**: Application / Client ID provided by the client. 
   - **Use Quick Discovery**: True 
   - **Frequency in Minutes**: 60 
   - **Number of Monitored Individual Per job**: 100 
   - **Collection Period Offset in Minutes**: 0 

 ![](media/Office_365_email_and_calendar_via_Collect/DataSourceSpecificFields.png)
