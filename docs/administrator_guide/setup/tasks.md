---
layout: default
title: Tasks
parent: Setup
grand_parent: Administrator Guide
nav_order: 2
---

# Tasks
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

Tasks 
------

Tasks are ongoing background processes that are triggered by agents and run on the agent servers. They each have Run Intervals and configurations can be adjusted at a workspace level.

Each task is designed to be auto-recoverable and self-healing. For example, if there are temporary network connection issues that prevent `Data Retrieval` task from retrieving data, Trace will keep trying until network issues are resolved. No manual intervention is needed.

- **Data Retrieval:** Responsible for pulling data for Data Sources

- **Text Analysis:** Responsible for orchestrating external process that provides metadata about extracted text

- **Data Transformation:** Responsible for performing data transformations on Data Batches

- **Ingestion:** Responsible for triggering import of the Data Batches into Relativity (part of Proactive Ingestion Framework). Any Data Transformations configured for the corresponding Data Source will be performed prior to ingestion in the Data Transformation task.
  
-   **Data Validation:** Responsible for updating statuses of the Data Batches (part of Proactive Ingestion Framework)
    
- **Indexing:** Responsible for indexing data needed for searching

-   **Term Searching:** Responsible for executing searching of the Terms for Rule evaluations
    
-   **Rule Evaluation:** Responsible for evaluating configured Rules within the workspace 
    
    > **NOTE:** The Rule Evaluation task queues up work via the Service Bus framework if the Data Disposal action is in use. Trace supports any queueing framework supported by Relativity. Data Disposal  tasks are performed by the `Trace Worker Agent`. Additional Trace Worker Agents can be added to increase capacity. For more information, contact support@relativity.com.
    
-   **Reporting**: Responsible for reporting on the state of the system via email
    
- **Data Enrichment:** Responsible for extracting and enriching nested files (attachments, contents of zip files), generating extracted text, metadata and preparing the load file that is ready for import process.  For security reasons, embedded content that refers to external URL links do not get extracted.
  
  > **NOTE:** The Data Enrichment task queues up work via the Service Bus framework. Trace supports any queueing framework supported by Relativity. Enrichment tasks are performed by the `Trace Worker Agent`. Additional Trace Worker Agents can be added to increase capacity. For more information, contact support@relativity.com. 
