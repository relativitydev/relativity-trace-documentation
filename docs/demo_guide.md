---
layout: default
title: Relativity Trace Demo Guide
parent: Support
nav_order: 4
---

# Relativity Trace Demo Guide
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Demo Environment and Login Information

Reach out to `support@relativity.com`

Relativity Trace: An Overview of Relativity for Compliance
----------------------------------------------------------

Relativity today is primarily used for e-discovery, investigations and
regulatory inquiries: typically reactive and transactional workflows.  Trace is
built for **proactive compliance and surveillance workflows**.

Trace is a Compliance product on top of Relativity used to **monitor all forms
of communication** (audio, email, and chat plus their attachments) with an
extensible engine that gets better at filtering out false positives over time.
Trace can monitor and pull data from **40+ data origins**. In addition, Trace
can automatically extract text and meta-data from monitored content, **900+ file
types are supported**.

Goals of the Demo
-----------------

-   See how Trace can automatically and proactively pull data from a live Office
    365 instance for several Trace Monitored Individuals.

-   Highlight Trace’s capabilities of automatically extracting text and
    meta-data from Office 365 emails and attachments.

-   Show overall data flow from ingestion, indexing, searching, tagging
    (reviewing) and ultimately data disposal.

-   Introduction of the Trace Rules Engine – a way to define what type of
    information gets flagged upon ingestion and auto-batched out to a reviewer.

-   Familiarize you with broad Trace capabilities in a **sample compliance
    workflow**.

## Demo A 

In this demo we will be monitoring for “Market Abuse” conversations and
automatically flag those documents as they propagate though Trace flow.

This demo has 4 simple steps:

1.  Enabling pre-configured “Market Abuse” rule

2.  Enabling live ingestion from pre-configured Office 365 Data Source

3.  Viewing extracted text and meta-data that Trace automatically extracted from
    ingested emails and attachments

4.  Viewing the results of the Trace Rules Engine (tagged documents)

## Demo B

In this demo we will be enabling a disposal rule that is based on Data Disposal
action to automatically delete data outside of a configured data retention
policy.

## Workspace overview 

-   **Trace Demo**: Workspace with multiple pre-created rules and Office 365
    Data Source.

# DEMO A: Enabling Office 365 Data Source and auto-tagging documents (alerts)

## Section 1: Rules Overview

1.  Go into the **Trace Demo** workspace
    ![](media/e0c6e9c767be9be77cafb3db4eebef9b.png)

2.  Click into the **Trace:Rules** tab to see sample rules in the workspace.
    Rules are how you define the type of content that is relevant to you. The
    **Market Abuse** rule has been pre-created for you along with a few others.
    

![](media/demo_guide/Section1.2-1571771958433.png)
    
3. Click into the **Market Abuse** rule and see the options that make up this
   rule:

   -   **Searchable Set:** A Saved Search that the rule runs against

   -   **Associated Actions:** A set of actions to take on matched documents (this
   rule will move the matched documents to a separate folder)

   -   **Terms**: Allows you to link Trace Terms to refine your document filter
   criteria with an e-discovery grade searching engine (dtSearch)

   -   The rule is currently **Disabled**
   ![](media/demo_guide/Section1.3.png)

4. Click the **Enable Rule** console button under **Trace Rule Management** section:

   -   The rule is now **Enabled**

   -   As data is ingested, this rule will be automatically applied to all incoming
   documents
   ![](media/demo_guide/Section1.4.png)

## Section 2: Importing Data and Running Rules

1.  Now let’s test our rules by adding live stream of data into the workspace
    with Office 365 Data Source. Go to the **Trace:Data Sources** tab
    ![](media/demo_guide/Section2.1.png)

2. Click on the **Office 365 Exchange** data source to see how it is configured

   -   **Data Source Type**: You can choose which type of data you want to ingest.
   This instance has been setup with a few basic types. Trace can support 40+
   different Data Source Types

   - **Ingestion Profile:** Used for mapping loadfile columns to fields in Relativity and other loadfile specific configuration.

     ![image-20201001154812502](media\demo_guide\image-20201001154812502.png)

   - **Username / Password:** secure way to enter authentication information for various Data Sources (on the Credentials tab of the Data Source Layout)

     ![image-20201001154932635](media\demo_guide\image-20201001154932635.png)

   - **Trace Monitored Individuals:** lets you select which people to monitor

   -   The Data Source is currently **Disabled**

3.  Click **Enable Data Source** on the right hand side
    ![](media/demo_guide/Section2.2a.png)

4.  Data will begin to get pulled from the exchange server for each of the defined Monitored Individuals. Refreshing the page will show data batches as they are pulled from the data source and processed (it may take several minutes for first data batch to be fully created). You can see how much data each Data Batch retrieved and corresponding statuses. Once you have a few Data Batches in “Completed” state the rest of the Trace workflow automatically triggers.
    
    ![](media/demo_guide/Section2.4.png)

As time goes on, more batches with data will be created and ingested:
![](media/c3ef4b4a771fbfd3d7b25c7dc5ccf4dc.png)

## Section 3: Viewing Results

1. Click on **Documents** tab:

   1. Data is proactively being retrieved, extracted and ingested

   2. For this demo, all ingested documents are routed to the **Ingestion Folder**

      ![1571775679888](media/demo_guide/1571775679888.png)

   3. Documents matched to the **Market Abuse** rule will have the **Default Move To Folder** action execute. The matched documents will appear under the **Alerted Documents** folder.

      ![1571775810589](media/demo_guide/1571775810589.png)

   4. Navigate to the **Trace Demo** root folder. You will find the “**Trace Search Index**” is built automatically for your ad-hoc searching.
      ![](media/69cbd4e87b452afd74276bba27660db4.png)

3.  Explore Dashboards
    ![](media/demo_guide/Section3.3.png)

    1. Once all the data is ingested and analyzed about 8.5% of ingested documents have
        matched the rules:
        ![](media/demo_guide/Section3.3i.PNG)

      **(blank)** denotes the number of documents where no Rules were matched.
    
2. All of the Rules that matched:
      <br>![](media/demo_guide/Section3.4i.PNG)
    
3. File type breakdown of ingested documents:
      ![](media/demo_guide/Section3.3iii.PNG)
    
3. Review matched documents

   1.  Click on “Market Abuse” bar on the Rules widget
   ![1571776936298](media/demo_guide/1571776936298.png)
   2.  Click on “Revenue Sharing” on the Terms widget
   ![1571777044365](media/demo_guide/1571777044365.png)
   3.  Click on the top document in the list:
   ![1571777162502](media/demo_guide/1571777162502.png)
   4.  Explore document details:
   ![1571777552542](media/demo_guide/1571777552542.png)
   ![1571777717924](media/demo_guide/1571777717924.png)

   - Matched terms are automatically highlighted in the document

   - Document text and meta-data was automatically extracted

   - Related documents are displayed in the “Family” section


## Section 4: Recap

Thanks for completing Demo A! Quick recap, here’s what we did:

1.  Enabled **Market Abuse** rule for continuous evaluation

2.  Viewed rules that are based on Saved Searches and Trace Terms that have
    an associated action of moving the document to another folder.

3.  Enabled ingestion of documents, proactively from live Office 365 instance

4.  Validated that the documents were ingested into the workspace, automatically
    indexed, searched, tagged and moved

5.  Reviewed a matched document in the viewer with extracted data, related
    documents and highlighted terms

Let us know what you think! Reach out to `trace@relativity.com` with any
feedback. Thanks!

# DEMO B: Running a Disposal Rule

1.  Go into the **Trace Demo** workspace

2.  Let’s check out our “Non-alerted Documents” Saved Search. Go to **Saved
    Search** browser in the **Documents** tab and select the “**Non-alerted
    Documents**” Saved Search. You’ll notice there are \~5k documents that are
    currently in this Saved Search.
    ![1571779546803](media/demo_guide/1571779546803.png)
    
> **NOTE:** Count on non-alerted documents might vary

3.  Click into the **Trace:Rules** tab to see all rules in the workspace. The
    **Delete Rule** has been pre-created for you. Click into the **Delete
    Rule**.
    ![1571779609579](media/demo_guide/1571779609579.png)

4.  You’ll notice that the **Delete Rule** follows a similar format to the prior
    demo. The rule runs on the “Non-alerted Documents” Saved Search and has the
    “Default Data Disposal” action associated with it. Once enabled, This action will delete
all documents in the Saved Search that were created before the set retention length. This will enable you to have an **automated retention
    policy** in Relativity.
    
    > **NOTE:** For this demo retention has be purposely set to 0 hours, which means that all of the `non-alerted` data will be delete as soon as the rule runs
    >
    > For Saved Search recommendations, see [Data Disposal Action Type in User Documentation](user_documentation.md#data-disposal-action-type)
    
5.  Now let’s enable the rule so Trace can start enforcing your Data Disposal
    policy. Go to the **Trace:Rules** tab again and click on the “**Delete
    Rule**”
    ![1571779615711](media/demo_guide/1571779615711.png)

6.  Click on **Enable Rule** in console button under **Trace Rule Management** section
    ![1571779666116](media/demo_guide/1571779666116.png)

7.  Go back to the Saved Search Browser in the Documents tab and select the
    “Non-alerted Documents” Saved Search. Within a few minutes you’ll start to
    see documents getting deleted from this workspace.
    

![1571779733791](media/demo_guide/1571779733791.png)
    
8. Go to **Trace:Rules** , navigate to the Delete Rule and Disable it
   ![1571779820919](media/demo_guide/1571779820919.png)

Let us know what you think! Reach out to `support@relativity.com` with any
feedback. Thanks!
