---
layout: default
title: System Requirements
parent: Setup
grand_parent: Administrator Guide
nav_order: 1
---

# System Requirements
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

Prerequisites
=============

Ensure the default Relativity infrastructure has been set up and is fully operational. In addition, Relativity Trace utilizes the following components for its processes:

### Agents

-   dtSearch Index Manager

-   dtSearch Index Worker

-   dtSearch Search

-   Application Installation Manager

-   Auto Batch Manager

-   Integration Points Agent (need to install [Relativity Integration Points](https://platform.relativity.com/9.6/Content/Relativity_Integration_Points/Get_started_with_integration_points.htm?) first)
    
-   Integration Points Manager (need to install [Relativity Integration Points](https://platform.relativity.com/9.6/Content/Relativity_Integration_Points/Get_started_with_integration_points.htm?) first)

If you plan to use `Analytics` functionality, please also make sure the following agents are set up:

-   Relativity Analytics Index Manager

-   Relativity Analytics Cluster Manager

-   Analytics Categorization Manager

-   Analytics Index Progress Manager

-   Active Learning Manager

-   Active Learning Worker

-   Structured Analytics Manager (need to install [Relativity Analytics](https://help.relativity.com/9.6/Content/Relativity/Analytics/Structured_analytics_set_tab.htm) first)
    
-   Structured Analytics Worker (need to install [Relativity Analytics](https://help.relativity.com/9.6/Content/Relativity/Analytics/Structured_analytics_set_tab.htm) first)

### Applications

-   [Relativity Integration Points](https://help.relativity.com/RelativityOne/Content/Relativity/Relativity_Integration_Points/Relativity_Integration_Points.htm)
1.  Relativity Integration Points is a required application for Relativity Trace and should be installed in all Trace workspaces BEFORE installing Trace
    2.  Used by Trace Data Sources
    3.  See this [page](https://help.relativity.com/9.6/Content/Relativity_Integration_Points/RIP_9.6/Installing_Integration_Points.htm) for details on how to install Integration Points
-   [Relativity Analytics](https://help.relativity.com/RelativityOne/Content/Relativity/Analytics/Structured_analytics_set_tab.htm#Setting_up_your_environment)
    1.  Used by Trace after ingestion to perform Structured Analytics workflows (language identification, repeated content identification, etc)
    
-   [Active Learning](https://help.relativity.com/RelativityOne/Content/Relativity/Active_Learning/Active_Learning.htm)
    1. Used by Trace after ingestion to analyze documents against Machine Learning models.


    Setting up Relativity Trace
===========================

1.  Install [Relativity Integration Points](https://platform.relativity.com/9.6/Content/Relativity_Integration_Points/Get_started_with_integration_points.htm?) in all the workspaces that will Run Trace.
    
2. [Install](https://help.relativity.com/9.6/Content/Relativity/Applications/Installing_applications.htm) the `Trace_<version>.rap` from the Application Library tab in the Admin case to all workspaces
   that will run Trace 
   > **NOTE** Using the Relativity Applications tab from within a workspace to install Trace is NOT recommended. Always install Trace from the Application Library.

3. Wait until application Status switches to `Installed` in the target workspaces ![](media/cada62f5fd9156449b21a32c2a9e34f2.png)
    
4. Create Trace agents

   > Trace agents are Resource Pool aware.  A single resource pool supports only one `Trace Manager Agent` and an unlimited number of `Trace Worker Agents`

   1.  Trace Manager Agent
       1.  Agent Type = `Trace Manager Agent`
       2.  Number of Agents = `1` 
       3.  Agent Server = Select the agent server you would like the agent deployed on (see “Infrastructure and Environment Considerations” section for optimal performance)
       4.  Run Interval = `60`
       5.  Logging level of event details = `Log all messages`
   2.  Trace Worker Agent
       1. Agent Type = `Trace Worker Agent`
       2. Number of Agents = `No more than 2x #of CPU cores per agent server (Ex. 4 CPU agent server should host no more than 2 Trace Worker agents`
       3. Agent Server = Select the agent server you would like the agent deployed on (see “Infrastructure and Environment Considerations” section for optimal performance)
       4. Run Interval = `60`
       5. Logging level of event details = `Log all messages`
   3.  Integration Points Manager Agent
       1. Agent Type = `Integration Points Manager`
       2. Number of Agents = `1`
       3. Agent Server = Select the agent server you would like the agent deployed on (see “Infrastructure and Environment Considerations” section for optimal performance)
       4. Run Interval = `60`
       5. Logging level of event details = `Log critical errors only`
   4.  Integration Points Agent
       1. Agent Type = `Integration Points Agent`
       2. Number of Agents = `up to 4` (start with 1 and add more if data batches get backed up)
       3. Agent Server = Select the agent server you would like the agent deployed on (see “Infrastructure and Environment Considerations” section for optimal performance)
       4. Run Interval = `60`
       5. Logging level of event details = `Log critical errors only`
   
5. Please review the [Considerations](#infrastructure-and-environment-considerations) for system impact information. By default system processes (Tasks) are scheduled to run every 5 minutes (configurable per workspace).

   > Please reach out to `support@relativity.com` for additional information

6. On the `Agents` tab, view the Message of `Trace Manager Agent` until there are no longer any workspaces listed as `Updating` (this is necessary because the manager agent makes additional modifications to target workspaces after application install that are needed in the next steps) ![1571073733941](./media/user_documentation/1571073733941.png)
> **NOTE:** On upgrades, the workspaces with existing data could take considerable time but should not take longer than 20-30 minutes to finish upgrading.  Please reach out support@relativity.com if the upgrade takes longer. 

7. In the workspace, navigate to the `Trace`->`Setup` tab and set the `Run Option` to `Continuous`

![image-20200622103606164](media/user_documentation/image-20200622103606164.png)

 > **WARNING:** Changing the “Run Option” to “Continuous” will automatically build a dtSearch index for this workspace for all documents present. Only change this setting to "Continuous" when appropriate agent infrastructure is configured and disk space available to build a corresponding dtSearch Index. Please reach out to `support@relativity.com` for support on installing Trace into workspaces with existing data.


 Considerations
==============

Usability Considerations
------------------------


- Once a document is associated with a Rule, it will never be disassociated unless there are document updates to extracted text or metadata. The `Trace Document Retry` (mass operation) procedure will also reset the associations automatically.

-   Every Data Source has capability to be `Reset` via console buttons. Once a data source is reset,
    Trace will pull all available data again, beginning with the Start Date defined on the data source (if the Start Date is relevant to the data source type). **Depending on import profile settings, this could duplicate data in the Workspace.**
    
- Task processes (Indexing, Term Searching, Rule Evaluation, etc) run simultaneously (in parallel). It may take several task cycles (based on configured `Run Interval` for each task) for the end-to-end workflow to complete fully.

- Deleting a Trace Rule does not delete any of the corresponding Relativity infrastructure and objects that were created (i.e. dtSearch Index, Saved Searches, Batch Sets). 

- The global dtSearch index `Trace Search Index` (created by Trace application during installation) is supported for ad-hoc searching and will be incrementally built as part of Indexing task. All dtSearch indexes whose name begins with `Trace`, but not `TraceTemp` will incrementally build automatically.

> **NOTE:** `Trace Search Index` settings are propagated to all of Term Searching in Trace.  The index MUST be named exactly `Trace Search Index` in order to apply the settings correctly (noise words, alphabet, etc)!

## 	General Infrastructure and Environment Considerations

| **Tasks:**                       | **Ingestion**                                                                          | **Ingestion**      |    **Running Rules**                                                      |   **Running Rules**                                                                   |
|----------------------------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------------------------------------|
|                                  | **`Ingestion`, `Data Validation`, `Data Enrichment`, `Data Retrieval`, `Text Analysis`, and `Data Transformation`** | **`Indexing`**                                                                                                                                                                                        | **`Term Searching`**                                       | **`Rule Evaluation`**                                                  |
| Summary                          | Powers the Proactive Ingestion Framework                                               | Incrementally builds Trace Search Index and Temporary Search Indexes with batches of documents Optionally: Incrementally builds and runs Analytics Jobs (Conceptual, Classification and Structured) | Searches and tags Terms in workspace on an ongoing basis | Rule will run and tag all matching documents and perform actions     |
| Task Operations                  | *`Ingestion Task`*<br>-Looks for batches that need to be imported and kicks off import<br>-Creates RIP job per batch<br>*`Data Validation Task`*<br>-Updates Data Batch status<br>*`Data Retrieval Task`*<br>-Pulls data for enabled Data Sources <br>*`Data Enrichment Task`*<br>-extracts/expands/enriches source native document and prepares import load file (executed by `Trace Worker Agent`)<br/>*`Text Analysis Task`*<br>-performs any external text processing on data before ingestion task imports the data<br>*`Data Transformation`*<br>-performs data transformations on data batches before ingestion task imports the data<br> | *`Indexing Task`*<br>-Kicks off dtSearch incremental build<br>-Kicks off temporary (internal) dtSearch index builds for Term evaluation<br>-Kicks off Analytics Jobs (if configured)<br>**NOTE:** Run Interval controls frequency of temp indexes creation ONLY. Global dtSearch and Analytics Indexes are built every 60 minutes by default.                                                                                                                                                                                   | *`Term Searching Task`*<br>-Runs (searches and tags) Terms in the workspace<br>**NOTE:** Each Term Searching run interval will search up to 5 available document batches (default 10,000 documents per batch). These settings are configurable on Term Searching task.                                    | *`Rule Evaluation Task`*<br>-Evaluates each rule in the workspaces and triggers configured actions                                              |
| Recommended Run Interval         | `60` seconds                                                                             | `300` seconds                                                                                                                                                                                         | `300` seconds                                              | `300` seconds                                                          |
| Considerations and System Impact | -Speed of ingestion is determined by number of Integration Points Agents (max of 4 per instance) | -Ongoing index builds use shared instance queue, agents and Fileshare across multiple workspaces (resource pool)<br>-Every incremental build makes the old build obsolete - cleaned up by Case Manager nightly                                                                                  |                                                          | -Very complex/nested underlying Saved Searches can affect performance<br>-Saved Searches that return many documents can affect performance<br>-Many rules being evaluated often can put pressure on SQL server |

> **NOTE:** The Recommended Run Interval for the **`Reporting Task`** is 300 seconds.

Large Workspaces Infrastructure and Environment Considerations
---------------------------------------------

> **NOTE:** Use these additional recommendations to tune your environment for workspaces housing more than `10 Million` documents.


| Recommendation                                               | Explanation                                                  | Additional Notes                                             |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Separate dedicated infrastructure for `Web`, `Agent`, `SQL server` and Fileshare | Trace relies on Relativity infrastructure. In cases of shared resources (`Agent Servers`, `Fileshares`, `SQL queues`) it is recommended to dedicate separate infrastructure to limit effect on other workspaces within instance. | It is recommended to include these as a separate Resource Pool if deploying in existing environment |
| Limit Trace Task `Run Intervals` \>=`5 minutes` (300 seconds) | Each Task generates audits, SQL queries executions, creates tables, etc. and can put unnecessary pressure on the system when run too frequently | End-to-end workflow will require multiple Run Intervals for the cycle to complete |
| Limit maximum number of Rules: `50` per workspace, `500` per instance | The design of Rule Evaluation Task limits concurrent execution of multiple rules. This effect is compounded by running multiple workspaces with Rules concurrently. | Future iterations will remove this limitation                |
| Update dtSearch sub-index size to be `500K` OR `1M` (Advanced Settings) | Default sub-index size is `250K` docs, when you have more than `10` sub-indexes searches can become slow because of the number of sub-indexes<br>![1564672221173](media/1564672221173.png)<br><br>![1564672354757](media/1564672354757.png) | General rule is to keep number of sub-indexes under `10` total |
| Ensure [Data Grid for Audit](https://help.relativity.com/RelativityOne/Content/Relativity/Data_Grid/Data_Grid_for_Audit.htm) is setup OR use [Database Partitioning for Archiving Audit Records](https://community.relativity.com/s/contentdocument/06950000002JezyAAC) | Audits are generated frequently, outside of RelativityOne, they are stored in SQL which at scale creates very large tables.  It's best practice to set up table partitioning for your audits, or to deploy Data Grid solution | Data Grid for Audit is used natively in RelativityOne        |
