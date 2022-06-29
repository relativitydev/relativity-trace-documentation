---
layout: default
title: Monitored Individual Automated Sync from Microsoft Azure Active Directory
nav_exclude: true
---

# Monitored Individual Automated Sync from Microsoft Azure Active Directory
{: .no_toc }

Sync Monitored Individuals with Microsoft Azure Active Directory.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview

Deployment option B, depicted below, is required to use these data sources.

 ![](media/MonitoredIndiv/Monitored_DeploymtB_Diagrm.png)

Note the following current limitations:

- All data sources in a workspace can be run only fully automated or only manually; not both simultaneously.
- Guest user types in Azure Active Directory are not yet supported (supported from Trace 15.0)

 

## Configuring Collect

Collect is used for data retrieval. Make sure Collect is installed in the workspace before configuring the data source.

For detailed installation steps see Installing Collect.

## Configuring Users and Groups in Azure Portal and O365 Admin Center

Azure AD MI automated sync will sync only employees (Users):

- From given Groups
- Who have valid O365 License assigned
- Have “Access enabled” 

**Note:** To configure an employee (User) to sync with Trace, you must have access to Azure Portal and O365 Portal with O365 Administrator rights.



You will configure the following in this topic:

- *Configure Users in O365*
- *Configure Users and Groups in Azure*
- *Map Azure Active Directory Group identifier (Object Id) to Data Source with JSON*
- *Register Azure App with specific permission* 
- *Configure Monitored Individual on “Restricted” or “Non-Restricted” group*
- *Configure Data Mapping and Ingestion Profile*
- *Set-up Data Transformation*
- *Set-up Data Source*

 

##### Configure Users in O365

Follow the steps below to configure Users in O365.

1. Sign into **O365 Portal**.

2. Navigate to **Admin** > **Active Users** and verify the employee is assigned to the O365 License.

![](media/MonitoredIndiv/O365_Admin_ActiveUsers.png)

3. If needed, to assign an employee (User) to the License, go to **User details** > **Licenses and apps**, select the appropriate **License**, and click **Save**. Otherwise, skip this step.
    ![](media/MonitoredIndiv/O365_ActiveUsers_LicAndApps_JohnDoe.png)

4. Sign out of **O365 Portal**.

5. Proceed to the next section to configure user and groups in Azure.
     

##### Configure Users and Groups in Azure

Follow the steps below to configure Users and Groups in Azure.

1. Sign into **Azure Portal**.

2. Navigate to **Azure Active Directory** > **Users**.

For Azure AD MI automated sync to sync only employees (Users), make sure all monitored employees (Users) have **Account enabled** field set to **Yes**.

![](media/MonitoredIndiv/Azure_Users_AllUsers table_AcctEnabledYes_box.png)

3. If you need to modify an employee’s (User) account, go to **User details**, click **Edit** and change **Block sign in** to **Yes** (access enabled) if it is set to **No** (access disabled).
   ![](media/MonitoredIndiv/Azure_Settings_UserDetails_BlockSignIn_box.png)



4. Navigate to **Azure Active Directory** > **Groups**.

   ![](media/MonitoredIndiv/Azure_ActiveDir_Groups__AllGroups table.png)
    

5. Create one or more Groups which will represent the mapping between employees (Users) and Trace Data Sources. Note the following:

   - Group Type must be set to **Microsoft 365**.

   - If there is only one Data Source, then only one Group is needed.

   - For multiple Data Sources, if all employees are linked to all Data Sources, then only one Group is needed.

   - One Group can be linked to one or more Data Sources.

   - One employee (User) can be linked to one or more Groups.

To create a new Group, navigate to **Azure Active Directory** > **Groups,** click **New Group,** enter a name, enter **Microsoft 365**, and save.

![](media/MonitoredIndiv/Azure_NewGroup.png)



6. To assign employees (Users) to a Group, navigate to **Azure Active Directory > Groups**, go to **Group** **details**, go to **Members**, click **Add Members** and select employees.

![](media/MonitoredIndiv/Azure_AddMembers_box_arrow.png)

7. For each Group, capture the **Group identifier (Object Id)**. It will be needed to create mapping of Azure Active Directory Group identifier towards Data Sources. See next step.

![](media/MonitoredIndiv/Azure_Groups_AllGroups_ObjectID_box.png)

8. Proceed to the next section to map Azure Active Directory Group identifier (Object Id) towards Data Sources to sync with JSON.
    

##### Map Azure Active Directory Group identifier (Object Id) to Data Source with JSON

Create mapping of the Azure Active Directory Group identifier (Object Id) to the Data Source with a JSON config file where:

- **GroupID**: Group identifier (**Object Id**) captured from Azure Portal.
- **DataSourceName**: name of Trace Data Source that will be created in Relativity Trace.

![](media/MonitoredIndiv/AzureAD_JSON.png)

*Examples*

- Example 1 – Using only one Data Source:

Azure Active Directory Users from “9ccf…” group will be linked to “Collect O365 Mail” Data Source.

![](media/MonitoredIndiv/AzureAD_JSON_Ex1.png)

- Example 2 – Using multiple Data Sources:

Users from “9ccf…” group will be linked to “Collect O365 Mail,” “Collect O365 Calendar,” and other Data Sources.

![](media/MonitoredIndiv/AzureAD_JSON_Ex2.png)



- Example 3 – Populate “Restricted” and “Non-Restricted” group info:

  - Users from “9ccf…” group will be linked to “Collect O365 Mail” and “Collect O365 Teams” Data Sources.

  - Additionally, indication if a user belongs to “Restricted” (13be) or “Non-Restricted” (b324) group will be populated. This requires changes to: Monitored Individual, Data Mapping, and Ingestion Profile. See further instructions.

  ![](media/MonitoredIndiv/AzureAD_JSON_Ex3.png)



##### Register Azure App with specific permission 

Follow the instructions from [O365 Mail and Calendar via Collect](#Step ) to register Azure App with specific permission.

**Notes:** 

- **If you already created an Azure application for O365 or any other Azure data source, you do not need to create another one!** You could reuse the same Azure Application *if the client saved the Application Secret when they created it.* 

- If the client did not store the Application Secret, or they have misplaced it, then proceed with creating a new Application.

- When registering your app, ensure the following permissions are set:

  - Group.Read.All

  - User.Read

  - User.Read.All

 

##### Configure Monitored Individual on “Restricted” or “Non-Restricted” group

This step is only necessary if tagging Monitored Individual on “Restricted” or “Non-Restricted” group. You need to create an **ADGroupIDsPlusNames** multi-choice field on Monitored Individual object. Make sure the following parameters are set as shown below:

![](media/MonitoredIndiv/ConfigMonitrIndiv_ADGroupIDsPlusNames.png)

- **Name:** Enter **ADGroupIDsPlusNames**.
- **Object Type:** Select **Monitored Individual**.
- **Field Type:** Select **Multiple Choice**.
- **Default Overlay Behavior:** Choose **Replace Values**.
- **Enable Group By:** Toggle on for Yes.
- **Enable Pivot:** Toggle on for Yes.
- **Open to Associations:** Yes

 

##### Configure Data Mapping and Ingestion Profile

Follow the steps below if tagging Monitored Individual on “Restricted” or “Non-Restricted” group.

1. Create **ADGroupIDsPlusNames** Data Mapping that points to **ADGroupIDsPlusNames** field on Monitor Individual RDO.

![](media/MonitoredIndiv/ConfigMonitrIndiv_ADGroupIDsPlusNames.png)

2. Link **ADGroupIDsPlusNames** Data Mapping with **Default Monitored Individuals Sync** Profile.

 

**Notes:**

- Do not modify default Data Mappings: **userPrincipalName**, **SecondaryIdentifier**, **displayName**, **givenName**, surname and **TraceDataSource**.
- It is possible to synchronize more employee data from Azure Active Directory. To configure that, Monitored Individual object and the default Ingestion Profile needs to be extended by additional fields and corresponding Data Mappings. [Here](https://docs.microsoft.com/en-us/graph/api/resources/user?view=graph-rest-1.0#properties) is a list of all supported fields.
- Custom attributes are also supported in the form of: extension_APPID_attributeName, where APPID is the application ID (without hypens) of the app registration storing custom attributes with the name that can be searched by using the following pattern: “*-extensions-app. Do not modify*”. More info here: [custom attributes.](https://docs.microsoft.com/en-us/azure/active-directory-b2c/user-flow-custom-attributes?pivots=b2c-user-flow)

 

In the example below, the Ingestion Profile has been extended by three additional fields:

- **Id**: additional Azure Active Directory field
- **hireDate**: additional Azure Active Directory field
- **ADGroupIDsPlusNames**: user Groups

![](media/MonitoredIndiv/ConfigDataMapAndIngestProfile_DataMappings.png)

 

##### Set-up Data Transformation

To create a new Data Transformation, make sure the following parameters are set as shown below.

![](media/MonitoredIndiv/SetupDataTransf_Definition.png)

- **Name**: Enter **MI Sync**.
- **Transformation Type**: Select **Monitored Individual Sync**.
- **Content**: leave this field blank.
- **Associated Data Source**: leave it not selected.
- **Group Id To Data Source Name Mapping Json**: Copy the JSON config file created in the *“Map Azure Active Directory Group identifier (Object Id) to Data Source with JSON”* section above.
- **Secondary Identifier User Fields Json**: leave the default value.

 

##### Set-up Data Source

Most parameters work the same for all Collect Data Sources. Follow the instructions from [Common Collect Data Source Functionality](#_Common_Collect_Data) section.

Below are Azure AD Directory specific parameters:

1. In the **General** section, select **Microsoft Azure Active Directory** for the **Data Source Type**.

 ![](media/MonitoredIndiv/SetupDataSource_DataSourceType.png)

2. **Ingestion Profile:** Default Monitored Individuals Sync.

3. Credentials section:

- **Application Secret**: The Client Secret provided by the client (see [Authentication (Set up Azure Application)](#Step ) for more details).

  

**Note 1:** If you already created an Azure application for O365 or any other Azure data source, you do not need to create another one! You could reuse the same Azure Application *if the client saved the Application Secret when they created it.* 

**Note 2:** If the client did not store the Application Secret, or they have misplaced it, proceed with creating a new Application.

4. Data Source Specific Fields section:


   ![](media/MonitoredIndiv/SetupDataSource_DataSourceSpecificFields.png)
   

- **Domain**: The O365 domain name provided by the client.
- **Application Id**: Application / Client ID provided by the client.
- **Group Id To Data Source Name Mapping JSON**: Paste JSON config file created in the *“Map Azure Active Directory Group identifier (Object Id) to Data Source with JSON”* section above.
- **Frequency in Minutes**: 60
- **Pull Unlicensed Users:** Disabled by default. Enable to be able to pull shared mailboxes. To double check with customer if in given groups there are no other unlicensed accounts other than shared accounts
- **Pull Disabled Users:** Disabled by default. Enable if customer is aware of the risk of pulling disabled users for some use case.
- **Active Directory User Fields Json:** leave default values.

5. **Data Transformations:** Add **MI Sync** Data Transformation to **Azure Active Directory Sync** Data Source.
   ![](media/MonitoredIndiv/Set-up Data Source_DataTransformations.png)



 

 
