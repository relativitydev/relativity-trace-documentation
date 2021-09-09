---
layout: default
title: Azure Authorization
parent: Collection
grand_parent: Administrator Guide
nav_order: 3
---

# Azure Authorization
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

# Overview

This document lists various methods of authorization with Azure services including Exchange Web Services (EWS) and Azure Information Protection (AIP).

# Exchange Web Services (EWS)

Trace offers three methods for authentication and authorization with Exchange: Basic Authentication and 2 forms of OAuth 2.0 using application registrations in Azure.

## Basic Authentication

With Basic Authentication, Trace will use the username and password configured on the data source to authenticate directly with the configured Exchange server. This authentication method allows Exchange admins to scope which mailboxes Trace has access to by modifying the configured user's permissions.

### Required Fields on Data Source:

- Username
- Password

> **NOTE:** Microsoft will no longer allow basic username/password authentication in O365 starting in October 2020 and Data Sources using it will begin failing.

## OAuth 2.0 - Resource Owner Password Credentials Grant

Using the Resource Owner Password Credentials Grant, Trace will use the username and password configured on the data source to authenticate against an Azure Active Directory authorization server. The authorization server will return an authorization token that Trace will use to make calls against the Exchange server. This authentication method also allows Exchange admins to scope which mailboxes Trace has access to by modifying the configured user's permissions.

### Required Fields on Data Source:

- Username
- Password
-  Exchange Settings - Authorization Client Id 
-  Exchange Settings - Authorization Tenant Id 

## OAuth 2.0 -  Client Credentials Grant

Using the Client Credentials Grant, Trace will act as a service principal instead of a user. This means the Trace application will have it's own credentials that are unique to it. Trace will use its own credentials to authenticate against an Azure Active Directory authorization server. The authorization server will return an authorization token that Trace will use to make calls against the Exchange server. This authentication method does not allow Exchange admins to scope which mailboxes Trace has access to and Trace will have access to all mailboxes within the configured Azure Active Directory.

### Required Fields on Data Source:

- Exchange Settings - Authorization Client Id 
- Exchange Settings - Authorization Tenant Id 
- EWS Client Secret



# Azure Information Protection (AIP)

Trace can authenticate against Azure Information Protection services using only the two OAuth 2.0 authorization methods listed above. The authorization flow is identical to that of each OAuth method EWS, but the authorization token will be used against AIP services instead of Exchange. Additionally, the required fields on the data source differ.

## OAuth 2.0 - Resource Owner Password Credentials Grant

### Required Fields on Data Source:

- Username
- Password
- AIP Client Id
- AIP Tenant Id

## OAuth 2.0 -  Client Credentials Grant

### Required Fields on Data Source:

- AIP Application Id 
- AIP Tenant Id
- AIP Client Secret

# Trace and Azure Application Registrations (OAuth 2.0)

Application Registrations in Azure are a way of authorizing users and services to use certain Azure resources. This documentation assumes a familiarity with Azure Application Registrations. For information on creating an Application Registration, please see here: https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app#register-a-new-application-using-the-azure-portal. 



## Application Registration Configurations Required by Trace

### General

Trace relies on specific configurations of application registrations to be used for authorization using OAuth 2.0. The following parameters must be set while creating an application registration:

- **Name** : This is the name of your app registration and can be anything. Trace does not rely on the name to identify the app registration.
- **Account Type** : This should be set to "Accounts in this organizational directory only". If using the ROPC flow, this means that configured user on the data source in Trace must belong to the Azure Active Directory where you are creating the application registration.
- **Redirect URI** : A redirect URI is not required for use with Trace. This may be left as a default value.

If using the ROPC authorization method, the application registration must be enabled be treated as a public client. This can be done under the advanced settings on the "Authentication" blade in your application registration by selecting "Yes" next to "Treat application as a public client".

![1590532045656](media/authorization/1590532045656.png)

### API Permissions

The API Permissions blade in the application registrations config allows you to assign permissions to API endpoints in Azure. Each permission can be added by navigating to the API permissions blade and clicking "Add a permission". This will cause a pop-up where you can navigate to the API endpoint that is needed scoped permissions can be granted.

#### Exchange Web Services (EWS)

The API permissions required by Trace for Exchange vary depending on the authorization flow you are using.

##### Resource Owner Password Credential

To configure ROPC authorization in Trace, your application registration will need the following permission:

- API : Exchange
  - Delegated permissions
    - EWS
      - EWS.AccessAsUser.All

##### Client Credential

To configure Client Credential authorization in Trace, your application registration will need the following permission:

- API : Exchange
  - Application permissions
    - full_access_as_app

This permission will require an Azure Portal admin to grant consent for your application registration to use it.

#### Azure Information Protection (AIP)

The API permissions required by Trace for AIP vary depending on the authorization flow you are using.

##### Resource Owner Password Credential

To configure ROPC authorization in Trace, your application registration will need the following permissions:

- API : Azure Rights Management Services
  - Delegated permissions 
    -  user_impersonation
- API: Microsoft Information Protection Sync Service
  - Delegate permissions
    - UnifiedPolicy
      - UnifiedPolicy.User.Read

These permissions will require an Azure Portal admin to grant consent for your application registration to use them.

##### Client Credential

To configure Client Credential authorization in Trace, your application registration will need the following permission:

- API : Azure Rights Management Services
  - Application permissions
    - Content
      - Content.SuperUser
- API: Microsoft Information Protection Sync Service
  - Application permissions
    - UnifiedPolicy
      - UnifiedPolicy.Tenant.Read

These permissions will require an Azure Portal admin to grant consent for your application registration to use them.

## Configuration in Trace

To use either OAuth 2.0 authorization method in Trace, you will need to supply all of the required fields listed under the required fields section above. 

The Client ID required fields for both AIP and EWS refer to the ID of your application registration. This value is unique per app registration and can be found on the landing page of your application registration in Azure next to "Application (client) ID" (it will be a GUID).



The Tenant ID required fields for both AIP and EWS refer to the ID of your Azure Active Directory. This value is shared by all app registrations in your Azure Active Directory and can be found on the landing page of your application registration in Azure nex to "Directory (tenant) ID" (it will be a GUID).



### Client Secret for Client Credentials Grant

If using the Client Credentials grant with AIP or EWS, there is a Client Secret value required. To get a value for your Client Secret, navigate to the "Certificates & secrets" blade under your application registration. Once there, you can click "New client secret", which will generate a random client secret string. Copy the value and paste it into the corresponding Client Secret field in Trace. You will not be able to view the secret value after leaving the page.



# Trace and Azure Information Protection

Trace Data Sources can be configured to decrypt documents that are protected by Azure Information Protection. The Azure Information Protection Instance must have specific configuration applied in order for Trace to decrypt and read AIP protected documents. 

This configuration requires the following access / permissions:

- Administrative access to the Azure Information Protection Instance
- Access to the Azure Portal with permissions to create Application Registrations

## Configuring Azure Information Protection Instance

#### Enable Unified Labeling

It is required that the Azure Information Protection Instance being used is backed by the unified labeling platform. To see if your instance is backed by the unified labeling platform or to migrate your label to the unified labeling platform, follow these instructions:  https://docs.microsoft.com/en-us/azure/information-protection/configure-policy-migrate-labels 

#### Configure Super User

In order for Trace to be able to read AIP protected documents, the Trace Data Source must be associated with a Super User in your AIP Service. The Super User can be either a real user account in your directory, or a service principal associated with an Azure Application Registration (service principal). You can enable Super Users and set permissions by following this guide :  https://docs.microsoft.com/en-us/azure/information-protection/configure-super-users.

#### Add an Application Registration for Super User

In order for Trace to interact with the Azure Information Protection API, you will need to create an Application Registration in the Azure Active Directory instance associated with your AIP instance. 

Please follow the documentation in authorization.md to create an application registration for AIP.

## Configuring Trace for Azure Information Protection

After finishing the configuration of the Azure Information Protection instance, you're ready to start configuring Trace for consuming AIP protected data. AIP is configured at the Data Source level. Please populate the required fields listed in authorization.md for your intended authorization grant.
