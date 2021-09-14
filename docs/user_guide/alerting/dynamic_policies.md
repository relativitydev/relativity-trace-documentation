---
layout: default
title: Dynamic Policies
parent: Alerting
grand_parent: User Guide
nav_order: 4
---

# Dynamic Policies
{: .no_toc }

Policies can be created that change based on changes to external data such as control room data, human resources data, or expense data.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
Dynamic Policies can be defined using a Rule Generator, which automatically creates and updates Rules based on new structured data being ingested into Relativity Trace. Examples of Dynamic Policies are policies that alert on someone sharing material non-public information (MNPI) related to an ongoing deal managed by the control room team, or alert on someone retaliating after a human resource report is filed, or alert on someone discussing the true usage of expensed funds after and expense report is filed.

## Configuring a Dynamic Policy
Dynamic Policies are configured by a Relativity Trace Administrator. Administrator information on how to configure a Dynamic Policy can be found [here]({{ site.baseurl }}{% link docs/administrator_guide/alerting/dynamic_rules.md %}).