---
layout: default
title: Using Relativity Collect
nav_exclude: true
---

# Using Relativity Collect
{: .no_toc }

The Relativity Collect application is required for all cloud-to-cloud data sources. This page explains how to configure this dependency and prerequisite.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Setup in Trace

The following sections provide the steps for installing Collect and configuring appropriate instance settings.

### Collect

Before configuring the required instance settings and any data source, install the Collect RAP from the Application Library in Relativity via the following steps.

1. Navigate to the workspace where you want to install the application.
2. Navigate to the **Application Admin** tab.
3. Click **New Relativity Application** to display an application form.
4. Click the **Select from Application Library** radio button in the Application Type section.
5. Click the ellipses in the **Choose from Application Library** field.
6. Select **Collect** on the Select Library Application dialog. This dialog only displays applications added to the Application Library. 
7. Click Ok to display the application in the Choose from Application Library field.
8. Click **Import** to install Collect into the workspace.
9. Review the import status of the application. Verify that the install was successful or resolve errors.

#### Instance settings

Configure the following instance settings: 

- Configure Collect Queue Depth: 

- **Name**: MaxNumberOfRunningStandaloneCollections 
- **Section**: Relativity.Collection 
- **Value Type**: Integer 32-bit 
- **Value**: 10 

Configure Data Batch Automatic Retry Policy: 

- **Name**: TraceWorkspaceSetting 
- **Section**: Trace.Workspace 
- **Value Type**: Text 
- **Value**: “DataBatchRetryIntervals”:[10,30,60] 

Toggle On/Off Auto Batch Split functionality: 

- **Name**: EnableCollectDataBatchSplit. 
- **Section**: Trace.Workspace. 
- **Value Type**: True/False. 
- **Value**: False (auto split disabled) or True (auto split enabled). 