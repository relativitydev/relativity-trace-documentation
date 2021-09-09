---
layout: default
title: Omit from Alert Rules
parent: Detailed Data Flow
grand_parent: Administrator Guide
nav_order: 3
---

# Omit from Alert Rules
{: .no_toc }

Quickly identify and clear exempt communications, junk, large emails blasts and other irrelevant content prior to running rule evaluation.

1. TOC
{:toc}

---
## Omit from Alert Rules Configuration
By adding a saved search to the `Omit from Alert Rules Saved Search` setting on the `Rule Evaluation` task, you can locate documents that should not have alert rule evaluation performed. Only parent documents are considered when locating documents that should be omitted from alert rules using the critia in the saved search. Once parents are located all of their children are also omitted from alert rule evaluation. Any document that is omitted from alert rules will get the `Alert Rules Complete` document status and will have the `Trace Omit from Alert Rules` document field populate with a value of `YES`. Only documents with a document status of `Normalized` will be evaluated by the Omit from Alert Rules Saved Search critia.

### Deciding on Criteria
When setting Omit from Alert Rules Save Search criteria you should be confident that there is no reason this critia could be met and a valid alert could be generated on this content. Alert Rules will not run across these documents, so there is no way an alert could be generated for a document that meets this criteria.

#### Example Criteria
-   Document has `Trace Exempt` set to `Exempt`
-   Document has `Recipient Count` greater than `10`
-   Document has Spam score above threshold