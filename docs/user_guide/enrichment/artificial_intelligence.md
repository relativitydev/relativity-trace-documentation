---
layout: default
title: Artificial Intelligence
parent: Enrichment
grand_parent: User Guide
nav_order: 5
---

# Artificial Intelligence
{: .no_toc }

1. TOC
{:toc}

---

## Overview

Trace provides out-of-the-box Artificial Intelligence (AI) to improve the uncover real risk, reduce review time, and build confidence. 

What does this mean for you? Trace goes beyond lexicon-based surveillance systems with powerful AI models specifically designed to uncover true risk and reduce review time. Trace AI models learn and improve over time, delivering smarter alerts your compliance team can rely on. And with fully transparent results, analysts will understand the alerts and compliance teams can easily explain outcomes to stakeholders.


## Models

| **Trace Model Category** | **Relativity Model**    | **Model Type** | **Model Description**                          |**Model Implementation**                     | **Model Fields** |
| ------------------------ | ------------------------| ---------------| -----------------------------------------------| --------------------------------------------|---------------|
| Reduce Review Time       | Spam Detection          | Classification | Identifies spam and not spam communications    | Map field to coding panel (must add to [Omit from Alert Rules](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/alerting/omit_from_alert_rules.html) to prevent spam from being alerted on) |Trace Is Spam|
| Reduce Review Time       | Text Cleansing          | Classification | Identifies non-authored or duplicative content | See [Data Transformations](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/enrichment/data_transforms.html#ai-extracted-text-cleansing-data-transformation) |Trace Primary Language, Trace Other Languages, Trace Language Switching Detected|
| Build Confience          | Language Identification | NLP            | Identifies primary and other languages ([Support Languages](https://help.relativity.com/RelativityOne/Content/Solutions/Supported_languages_matrix.htm))        | Map desired fields to coding panel, view, etc. Could add "Trace Language Switching Detected" to a [Worfklow](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/workflow_rules.html) or [Alert Rule](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/alerting/alert_rules.html).|             |
| Transcription             | Audio                   | NLP            | Transcibes audio communciations into text      | Contact Trace Support                       |             |
| Uncover Real Risk        | Change of Venue         | Classification | Detect an attempt to avoid discovery by changing the communication venue (i.e., moving from email to phone call)| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Rumors and Speculation  | Classification | Detect the distribution or discussion of unverified and doubtfully true information| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Collaborative Discussion| Classification | Detect employees working together to prevent the discovery of misconduct and sharing of client identifying data| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Boasting                | Classification | Detect the excessively proud and self-satisfied talk by a trader of their achievements in regard to someone less fortunate| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | General Tipping         | Classification | Detect the sharing of potential material nonpublic information (MNPI) regarding general company information, financial information, or corporate actions| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Prearranged Trading     | Classification | Detect traders agreeing on trade price in advance of execution | Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Price & Benchmark Fixing| Classification | Detect agreements between traders to collectively manipulate the price of a financial product or a benchmark to adjust market conditions| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Coercion & Intimidation | Classification | Detect persuasion through force or threats     | Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Mirror Trading          | Classification | Detect simultaneous buy and sell trades of the same stock on different exchanges by the same entity, as a way to move money between jurisdictions| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Trade Fixing            | Classification | Detect agreements between traders to collectively manipulate benchmark foreign exchange rates (FIX) to artificial levels| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Layering & Spoofing     | Classification | Detect traders placing and then cancelling orders that they never intended to execute, with the intention of influencing the price| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Front Running           | Classification | Detect traders attempting to buy or sell financial products ahead of other orders to lock in a better price| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Pump & Dump             | Classification | Detect traders attempting to boost the price of a financial product after establishing a large long position by sharing false or misleading information| Please contact Trace Support to Implement   |na          |
| Uncover Real Risk        | Short & Distort         | Classification | Detect traders attempting to decrease the price of a financial product after establishing a large short position by sharing false or misleading information| Please contact Trace Support to Implement   |na          |

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
