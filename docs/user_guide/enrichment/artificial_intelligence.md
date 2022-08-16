---
layout: default
title: Artifical Intelligence
parent: Enrichment
grand_parent: User Guide
nav_order: 1
---

# Artifical Intelligence
{: .no_toc }

1. TOC
{:toc}

---

## Overview

Trace provides out-of-the-box Artifical Intelligence (AI) to improve the user experience, reduce review time, pinpoint risk. 

## Models

| **Trace Model Category**   | **Trace Model Type**   | **Relativity Model**          | **Model Type**    | **Model Description**           |
| -------------------------- |----------------------- | ----------------------------- | ----------------- | --------------------------------|
| Irrelevant Content Dection | Standard               | AI Extracted Text Cleansing   | NLP    | Identifies non-authored or duplicative content, email headers, email signatures, and confidentiality footers |
| Irrelevant Content Dection | Standard               | Spam Detection                | Classification    | Spam is defined as irrelevant communications that could not contain misconduct |
| Irrelevant Content Dection | Pre-Built              | Newsletter Detection          | Classification    | Detect widely disseminated and recurring messages that summarize world and market news (“Newsletters”) that do not need to be reviewed, to reduce false positives               |
| Irrelevant Content Dection | Pre-Built              | Financial Research Report Detection| Classification    | Detect widely disseminated documents prepared by investment research firms that describe a company and often provide a particular recommendation (“Research Reports”) that do not need to be reviewed, to reduce false positives               |
| Reviewer Understanding     | Standard               | Language Identification       | NLP               | Identifies the primary and other languages in a communication|
| Reviewer Understanding     |Pre-Built               | Audio Trascription            | NLP               | Transcibes audio communciations into text                    |
| Risk Detection             | Pre-Built              | Change of Venue               | Classification    | Detect an attempt to avoid discovery by changing the communication venue|
| Risk Detection             | Pre-Built              | Rumors And Speculation        | Classification    | Detect the distribution or discussion of unverified and doubtfully true information|
| Risk Detection             | Pre-Built              | Collaborative Discussions     | Classification    | Detect employees working together to prevent the discovery of misconduct and sharing of client identifying data |
| Risk Detection             | Pre-Built              | Boasting Financial            | Classification    | Detect excessively proud and self-satisfied talk by a trader of their achievements|
| Risk Detection             | Pre-Built              | General Tipping               | Classification    | Detect the sharing of potential material nonpublic information regarding company & financial information      |
| Risk Detection             | Pre-Built              | Prearranged Trading           | Classification    | Detect traders agreeing on trade price in advance of execution    |
| Risk Detection             | Pre-Built              | Price and Benchmark Fixing    | Classification    | Detect agreements between traders to collectively manipulate the price of a financial product or a benchmark to adjust market conditions   |
| Risk Detection             | Pre-Built              | Front Running                 | Classification    | Detect traders attempting to buy or sell financial products ahead of other orders to lock in a better price      |
| Risk Detection             | Pre-Built              | Mirror Trading                | Classification    | Detect simultaneous buy and sell trades of the same stock on different exchanges by the same entity, as a way to move money between jurisdictions      |
| Risk Detection             | Pre-Built              | Forex Collusion - Trade Fixing| Classification    | Detect agreements between traders to collectively manipulate benchmark foreign exchange rates (FX) to artificial levels     |

## Trace Model Type

### Standard

AI functionality enabled for all customers that is built by Trace and requires no customer training. Standard models are focused on understanding that doesn’t change across customers or industries

### Pre-Built

AI functionality avaliable to all customers that is built by Trace and can be improved by a customer. These models support validation and are focused on common compliance requirements. 

### On-Demand

AI functionality that a customer can define and build. These are focused on customer specific requirements. 

## Fields
Document fields are created for each enrichment method. These document fields can be used as part of the Omit from Alert Rules functionality or Rules. See more information on AI fields [here](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/fields.html).

## Model Details

Below is supplemental information to help understand and implement the models above. 

### Risk Detection

All Risk Detection information can be found [here](https://relativitydev.github.io/relativity-trace-documentation/docs/user_guide/enrichment/machine_learning_model.html)

### Language Identification

For infromation on enablment can be found [here](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/enrichment/data_transforms.html)

### Spam Detection

For infromation on enablment can be found [here](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/enrichment/data_transforms.html)

### AI Extracted Text Cleansing

For infromation on enablment can be found [here](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/enrichment/data_transforms.html#ai-extracted-text-cleansing-data-transformation)

## Additional Information

For more information on how Trace' AI models are enabled, please see the [Admin Guide](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/enrichment/data_transforms.html)
