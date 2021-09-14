---
layout: default
title: Detailed Data Flow
parent: Data Flow
grand_parent: Administrator Guide
nav_order: 1
---

# Detailed Data Flow
{: .no_toc }


Each communication flows through Relativity Trace in a consistent repeatible way to produce a defensible and explainable surveillance process.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---
## Overview

Every communication for the individuals being monitored flows through the following steps within the system. Each step can be heavily configured based on an organization's structure, team, and risk tolerances, but the flow stays constant. 

| # | Category | Step | Description |
|:---:|:------:|:-------------:|:-----|
| 1 | Collection | Data Sources | Define the communication channels that need to be monitored |
| 2 | Collection | Monitored Individuals | Define the individuals that need to be monitored and for what Data Source |
| 3 | Collection | Collect | Configure underlying collection method either through Relativity Collect capabilities or third party collection tools |
| 4 | Enrichment | Data Transformations | Analyze native communication files to ignore, manipulate , or derive content prior to communication becoming a document  |
| 5 | Ingestion | Load File | Generate a ingestion configuration file for a set of communications |
| 6 | Ingestion | Data Batches| Define a unit of ingestion work to be performed |
| 7 | Ingestion | Integration Points | Ingest data defined in Data Batch into Relativity Trace|
| 9 | Enrichment | Index & Term Search | Create search indexes and search for Trace Terms in extracted text |
| 9 | Enrichment | Scripts | Run scripts to create new metadata on documents |
| 10 | Enrichment | Analytics & Machine Learning | Run analytics capabilities to create new metadata on documents |
| 11 | Enrichment | Normalize | Verify that communication have undergone all enrichment actions and are ready for alerting |
|12 | Alerting | Omit from Alert Rules | Identify communications that could not possibly contain any misconduct and remove them from alert analysis |
| 11 | Alerting | Alert Rules | Locate communications that contain misconduct and mark them as alerts |
| 12 | Workflow | Workflow Rules | Perform workflow actions to move alerted communications to the appropriate queues for manual review |
| 13 | Review | Manual User Review | Users manually review alerted communications and add their review decisions on the document |
| 14 | Workflow | Workflow Rules | Communications are moved through the system based on their review decision |
| 15 | Retention | Disposal | Communications are removed from Relativity Trace based on defined retention policies |