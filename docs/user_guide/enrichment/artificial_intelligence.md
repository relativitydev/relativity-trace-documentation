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

| **Trace Model Category** | **Relativity Model**    | **Model Type** | **Model Description**                          |**Model Implementation**                     | **Model Fields** |
| ------------------------ | ------------------------| ---------------| -----------------------------------------------| --------------------------------------------|---------------|
| Irrelevant Content       | Spam Detection          | Classification | Identifies spam and not spam communications    | Map field to coding panel (must add to [Omit from Alert Rules](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/alerting/omit_from_alert_rules.html) to prevent spam from being alerted on) |Trace Is Spam|
| Irrelevant Content       | Text Cleansing          | Classification | Identifies non-authored or duplicative content | See [Data Transformations](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/enrichment/data_transforms.html#ai-extracted-text-cleansing-data-transformation) |Trace Primary Language, Trace Other Languages, Trace Language Switching Detected|
| Context                  | Language Identification | NLP            | Identifies primary and other languages ([Support Languages](https://help.relativity.com/RelativityOne/Content/Solutions/Supported_languages_matrix.htm))        | Map desired fields to coding panel, view, etc. Could add "Trace Language Switching Detected" to a [Worfklow](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/workflow_rules.html) or [Alert Rule](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/alerting/alert_rules.html).|             |
| Transciption             | Audio                   | NLP            | Transcibes audio communciations into text      | Contact Trace Support                       |             |

## Fields
Document fields are created for each enrichment method. These document fields can be used as part of the Omit from Alert Rules functionality or Rules. See more information on AI fields [here](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/fields.html).

Fields are populated automatically, there is not transformation or action requried
{: .info }

## Testing Model Outcomes

Users may want to test the result before adding a field to their standard workflow, whether that be in a view, coding panel, or in alerting. One can do this by creating a Saved Search

1. Click "Crete New Search"
2. Name the search (for example, "Spam Detection")
3. Add any condition (for example, alerts in the past 30 days)
4. Add "Trace is Spam" to Fields
5. Click "Save & Search"
6. From here, you can see what alerts would have been caught via the Spam Detection model

To only see results from that model, create a condition where that field value "is set" or "is" Spam/Not Spam
{: .info }
