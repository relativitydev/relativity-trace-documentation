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

| **Trace Model Category** | **Relativity Model**          | **Model Type**    | **Model Description**                                        |
| ------------------------ | ----------------------------- | ----------------- | ------------------------------------------------------------ |
| Irrelevant Content       | Spam Detection                | Classification    | Identifies spam and not spam communications                  |
| Irrelevant Content       | Text Cleansing                | Classification    | Identifies non-authored or duplicative content               |
| Context                  | Language Identification       | NLP               | Identifies the primary and other languages in a communication|
| Transciption             | Audio                         | NLP               | Transcibes audio communciations into text                    |
| Risk Detection           | Change of Venue               | Classification    | Detect an attempt to avoid discovery by changing the communication venue|
| Risk Detection           | Rumors And Speculation        | Classification    | Detect the distribution or discussion of unverified and doubtfully true information|
| Risk Detection           | Collaborative Discussions     | Classification    | Detect employees working together to prevent the discovery of misconduct and sharing of client identifying data |
| Risk Detection           | Boasting Financial            | Classification    | Detect excessively proud and self-satisfied talk by a trader of their achievements|
| Risk Detection           | General Tipping               | Classification    | Detect the sharing of potential material nonpublic information regarding company & financial information      |

## Fields
Document fields are created for each enrichment method. These document fields can be used as part of the Omit from Alert Rules functionality or Rules. See more information on AI fields [here](https://relativitydev.github.io/relativity-trace-documentation/docs/administrator_guide/fields.html).

