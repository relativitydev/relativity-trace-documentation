---
layout: default
title: Monitored Individuals
parent: User Guide
nav_order: 4
---
# Monitored Individuals
{: .no_toc }

Under Construction
{: .label .label-yellow }

A Monitored Indidual is a person within the organization whose communications are being analyzed for misconduct.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
Monitored Individuals can be added an removed manually within Relativity Trace. They can be assigned to multiple Data Sources to collect data for that individual from a specific communication channel.

The only two fields on Monitored Individual currently used in application logic are the `Identifier` and `Secondary Identifier` fields. All other fields are simply for display purposes. Each Monitored Individual must have a unique value in the Identifier field. Typically the Identifier is the employee’s email address. Identifier is **case-sensitive**, with the exception of the domain of an email address (e.g. `Test@test.com` and `test@test.com` are treated as two different email addresses / identifiers, while `test@Test.com` and `test@test.com` are treated as the same email addresses / identifiers). The Secondary Identifier field is used to list other email addresses that may be associated with this Monitored Individual. Email addresses in the Secondary Identifier field should be delimited with a semi-colon (;).
{: .info }

It is also possible to automatically add / update / remove Monitored Individuals via [Extensible API's]({{ site.baseurl }}{% link docs/administrator_guide/proactive_ingestion_api_documentation.md %}).
{: .info } 