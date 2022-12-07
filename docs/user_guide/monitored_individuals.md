---
layout: default
title: Monitored Individuals
parent: User Guide
nav_order: 4
---
# Monitored Individuals
{: .no_toc }

A Monitored Indidual is a person within the organization whose communications are being analyzed for misconduct.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
Monitored Individuals can be added an removed manually within Relativity Trace. They can be assigned to multiple Data Sources to collect data for that individual from a specific communication channel.

## Creating or Updating a Monitored Individual

Monitored Individuals can be automatically added, updated and removed via Trace Extensible API's. More information can be found [here]({{ site.baseurl }}{% link docs/administrator_guide/proactive_ingestion_api_documentation.md %}).
{: .info } 

**Manually Creating a Monitored Individual**

1. Navigate to the `Monitored Individuals` tab and click `New Monitored Individual`.
2. Fill out the fields related to the Monitored Individual and click save.

## Monitored Individual Fields

| **Field Name** | **Description**          | **Notes**    |
| ------------------------ | ----------------------------- | ----------------- |
| Identifier | Unique Monitored Individual identifier. Typically the employee's email address.  | **Case-sensitive** with the exception of the domain of an email address (e.g. `Test@test.com` and `test@test.com` are treated as two different email addresses / identifiers, while `test@Test.com` and `test@test.com` are treated as the same email addresses / identifiers).      |
| Secondary Identifier | Alternative Monitored Individual identifiers. Typically alternate email adresses.   | Accepts multiple email addresses delimited with a semi-colon (;).      |
| Language    |  Primary language used by Monitored Individual    |  Multiple-choice. Used in Audio data sources to identify language model used for transcription for particular Monitored Individual. More information [here]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/voice_data_sources/generic_audio_data.md#transcription %}).    |
| Full Name    |     | For display purpose only.        |
| First Name    |      | For display purpose only.         |
| Last Name    |      | For display purpose only.         |
| Email    |     | For display purpose only.          |


