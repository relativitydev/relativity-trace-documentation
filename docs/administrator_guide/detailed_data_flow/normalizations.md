---
layout: default
title: Normalization
parent: Detailed Data Flow
grand_parent: Administrator Guide
nav_order: 2
---

# Normalization
{: .no_toc }


Prior to running Rules across a document we must ensure all analysis is complete.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---
## Normalization Configuration
By adding a saved search to the `Normalized Save Search` setting on the `Rule Evaluation` task, you can require document criteria to be met prior to rule evaluation being performed. All family members must meet the saved search criteria for rule evaluation to be performed. This setting is optional, and if it's not populated rule evaluation will be performed once term searching is complete.

### Deciding on Criteria
When setting Normalized Save Search criteria you should consider what field values are used within your rules and whether they are populated by Scripts, Analytics, or other scheduled processes. You should also consider what documents will never have these field values populated or why a document may not have the field values populated"

#### Example Criteria
Required Criteria
-   Document has Structured Analytics result fields set
-   Document has script output field populated
Pass-through
-   Document has more than 30mb of text
-   Document has Structured Analytics errors
-   Document is an attachment