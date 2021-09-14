---
layout: default
title: Detailed Data Flow
parent: Administrator Guide
nav_order: 2
has_children: true
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
|:---:|:------:|:-------------:|:-----:|
| 1 | Collection | Data Sources | Define the communication channels | |
| 2 | Collection | Monitored Individuals | set them on data source | |
| 3 | Collection | Shipper, collect, third party | |
| 4 | Enrichment | Data Transformations | |
| 5 | Ingestion | Load File | |
| 6 | Ingestion | Data Batches| |
| 7 | Ingestion | Integration Points | |
| 8 | Workflow | Workflow Rules | |
| 9 | Enrichment | Scripts | |
| 10 | Enrichment | Analytics & Machine Learning | |
| 11 | Alerting | Alert Rules | |
| 12 | Workflow | Workflow Rules | |
| 13 | Workflow | Actions | |
| 14 | Review | Manual User Review | |
| 15 | Workflow | Workflow Rules | |
| 16 | Retention | Disposal | |


