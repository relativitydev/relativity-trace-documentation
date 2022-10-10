---
layout: default
title: Tasks
parent: Setup
grand_parent: Administrator Guide
nav_order: 2
---

# Tasks
{: .no_toc }

Tasks are ongoing background processes that both manage and complete work.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

Types of Tasks
------

- **Data Retrieval:** Responsible for pulling data from Data Sources

- **Data Enrichment:** Responsible for extracting and enriching nested files (attachments, contents of zip files), generating extracted text, metadata and preparing the load file that is ready for import process. For security reasons, embedded content that refers to external URL links do not get extracted.

  > The Data Enrichment task queues up work via the Service Bus framework. Trace supports any queueing framework supported by Relativity. Enrichment tasks are performed by the `Trace Worker Agent`. Additional Trace Worker Agents can be added to increase capacity. For more information, contact [support@relativity.com](mailto:support@relativity.com).
  {: .info }
  
- **Transcription:** Responsible for transcribing audio files into text

- **Text Analysis:** Responsible for orchestrating AI processes that provide information about a communication's extracted text

- **Data Transformation:** Responsible for performing data transformations on Data Batches

- **Ingestion:** Responsible for triggering import of the Data Batches into Relativity (part of Proactive Ingestion Framework). Any Data Transformations configured for the corresponding Data Source will be performed prior to ingestion in the Data Transformation task.

- **Data Validation:** Responsible for updating statuses of the Data Batches (part of Proactive Ingestion Framework)

- **Indexing:** Responsible for indexing data needed for searching

  > It's recommended that the Indexing task runs more frequently than the Term Searching task. The run interval may differ between workspaces, but the default value for Term Searching should be 300 seconds (5 minutes).
  > {: .info }

- **Term Searching:** Responsible for executing searching of the Terms for Rule evaluations

- **Rule Evaluation:** Responsible for evaluating configured all Rules except ones with data disposal action assigned within the workspace 

  > Run interval should be set to a value at least 50% higher than average execution time of the task, for example, if rule evaluation task typically runs for about 600 seconds, set run interval to be at least 900 seconds. Max Documents Per Execution parameter should be set to match or exceed document ingestion rate, for example if daily ingestion rate is 96000 documents and run interval is set to 15 minutes, then Max Documents per Execution should be at least 1000.
  {: .info }
  
- **Data Disposal:** Responsible for evaluating configured Rules which have data disposal action assigned within the workspace.

  > Run interval and Max Documents Per Execution should be set using same suggestions as for Rule Evaluation task. The Data Disposal task queues up work via the Service Bus framework. Trace supports any queueing framework supported by Relativity. Data Disposal  tasks are performed by the `Trace Worker Agent`. Additional Trace Worker Agents can be added to increase capacity. For more information, contact [support@relativity.com](mailto:support@relativity.com).
  {: .info }

- **Reporting**: Responsible for generating reports (e.g. state of the system, user actions, etc.) and sending those reports via email

- **Trade Reconstruction**: Responsible for identifying and linking communications that relate to trades

## Task Attributes

Tasks have Run Intervals and configurations can be adjusted at a workspace level.

Each task is designed to be auto-recoverable and self-healing. For example, if there are temporary network connection issues that prevent `Data Retrieval` task from retrieving data, Trace will keep trying until network issues are resolved. No manual intervention is needed.
