---
layout: default
title: Monitored Individuals
parent: Collection
grand_parent: Administrator Guide
nav_order: 1
---

# Monitored Individuals
{: .no_toc }


A Monitored Indidual is a person within the organization whose communications are being analyzed for misconduct.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
A Monitored Individual allows administrators to define a person that can be monitored across Data Sources by importing and analyzing data that belongs to them. Monitored Individuals can be linked to multiple Data Sources.

The only two fields on Monitored Individual currently used in application logic are the `Identifier` and `Secondary Identifier` fields. All other fields are simply for display purposes. Each Monitored Individual must have a unique value in the Identifier field. Typically the Identifier is the employee’s email address. Identifier is **case-sensitive**, with the exception of the domain of an email address (e.g. `Test@test.com` and `test@test.com` are treated as two different email addresses / identifiers, while `test@Test.com` and `test@test.com` are treated as the same email addresses / identifiers). The Secondary Identifier field is used to list other email addresses that may be associated with this Monitored Individual. Email addresses in the Secondary Identifier field should be delimited with a semi-colon (;).
{: .info }

It is also possible to automatically add / update / remove Monitored Individuals via [Extensible API's]({{ site.baseurl }}{% link docs/administrator_guide/proactive_ingestion_api_documentation.md %}).
{: .info } 

## Billing
Monitored Individuals are used as a unit of billing by Relativity Trace. Generally a Relativity Trace license will specify a number of Monitored Individuals available and the number of data sources they can be used on.