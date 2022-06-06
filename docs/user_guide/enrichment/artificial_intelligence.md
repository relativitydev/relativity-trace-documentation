---
layout: default
title: Artifical Intelligence
parent: Enrichment
grand_parent: User Guide
nav_order: 5
---

# Artifical Intelligence
{: .no_toc }

1. TOC
{:toc}

---

## Overview

Trace provides out-of-the-box Artifical Intelligence (AI) to improve the user experience, reduce review time, pinpoint risk. 

## Models

| **Trace Model Category** | **Relativity Model**    | **Model Type** | **Model Description**                          |**Model Implementation**                     |
| ------------------------ | ------------------------| ---------------| -----------------------------------------------| --------------------------------------------|
| Irrelevant Content       | Spam Detection          | Classification | Identifies spam and not spam communications    | Map field to coding panel (must add to [Omit from Alert Rules](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/alerting/omit_from_alert_rules.html) to prevent spam from being alerted on) | 
| Irrelevant Content       | Text Cleansing          | Classification | Identifies non-authored or duplicative content | See [Data Transformations](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/enrichment/data_transforms.html#ai-extracted-text-cleansing-data-transformation) |
| Context                  | Language Identification | NLP            | Identifies primary and other languages         | Map desired fields to coding panel, view, etc. Could add "Trace Language Switching Detected" to a [Worfklow](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/workflow_rules.html) or [Alert Rule](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/alerting/alert_rules.html)      |
| Transciption             | Audio                   | NLP            | Transcibes audio communciations into text      | Contact Trace Support                       |

## Fields
Document fields are created for each enrichment method. These document fields can be used as part of the Omit from Alert Rules functionality or Rules. See more information on AI fields [here](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/fields.html).

Fields are populated automatically, there is not transformation or action requried
{: .info }

