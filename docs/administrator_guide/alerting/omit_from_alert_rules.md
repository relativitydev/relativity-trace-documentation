---
layout: default
title: Omit from Alert Rules
parent: Alerting
grand_parent: Administrator Guide
nav_order: 1
---

# Omit from Alert Rules
{: .no_toc }

Quickly identify and clear exempt communications, junk, large emails blasts and other irrelevant content prior to running rule evaluation.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---
## Omit from Alert Rules Configuration
By adding a saved search to the `Omit from Alert Rules Saved Search` setting on the `Rule Evaluation` task, you can locate documents that should not have alert rule evaluation performed. Only parent documents are considered when locating documents that should be omitted from alert rules using the criteria in the saved search. Once parents are located all of their children are also omitted from alert rule evaluation. Any document that is omitted from alert rules will get the `Alert Rules Complete` document status and will have the `Trace Omit from Alert Rules` document field populate with a value of `YES`. Only documents with a document status of `Normalized` will be evaluated by the Omit from Alert Rules Saved Search criteria.

Using the `Includes drop-down` (aka Related Items Addition) functionality in the saved search used for "Omit from Alert Rules" is NOT supported and will result in over-inclusive removal of communications from alerting.
{: .danger }

### Deciding on Criteria
When setting Omit from Alert Rules Save Search criteria you should be confident that there is no reason this criteria could be met and a valid alert could be generated on this content. Alert Rules will not run across these documents, so there is no way an alert could be generated for a document that meets this criteria.

#### Example Criteria
-   Document has `Trace Exempt` set to `Exempt`
-   Document has `Recipient Count` greater than `10`
-   Document has Spam score above threshold



## Omit Extracted Documents from Alert Rules Configuration

There is also an option to add a saved search to the `Omit Extracted from Alert Rules Saved Search` setting, also located on the Rule Evaluation task. While the `Omit from Alert Rules Saved Seach` setting *only* considers **parent** documents when locating documents that should be omitted form alert rules (even if there are child documents that fit the search criteria), the `Omit Extracted from Alert Rules Saved Search` only considers **extracted** (child) documents. If an extracted document matches the search criteria of the saved search, it will be omitted from alert rules and the `Trace Document Status` field will be populated to `Alert Rules Complete`. The `Trace Omit from Alert Rules` document field will also populate with a value of `YES`. The extracted documents in this saved search will be skipped over by the `Omit from Alert Rules Saved Seach` setting and left as `Normalized`, then only extracted documents with a document status of `Normalized` in the saved search will be evaluated.

### How to Configure Omit Extracted from Alert Rules Saved Search Setting

By default, the `Omit Extracted from Alert Rules Saved Search` setting will be empty. Follow the steps below to configure the this setting:

1. Determine the criteria for extracted documents that need to be omitted from alert rules
2. Create a new saved search with this criteria

Since this setting **only** evaluates extracted documents, no parent documents will be affected by this setting even if they fit the criteria of this saved search. To avoid confusion, you may want to add the condition `Trace Is Extracted` is `Yes`, so that you will only see extracted documents in this saved search.
{: .info }

1. Navigate to the Rule Evaluation task
2. Set the `Omit Extracted from Alert Rules Saved Search` setting to the newly created saved search

![](media\omit_from_alert_rules\omit_extracted_from_alert_rules_saved_search.png)
