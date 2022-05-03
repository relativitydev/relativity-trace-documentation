---
layout: default
title: Retention
parent: Administrator Guide
nav_order: 11
---

# Retention
{: .no_toc }

Retention policies can be defined to dispose of communications after surveillance has been performed.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
Retention policies are defined using [Workflow Rules]({{ site.baseurl }}{% link docs/administrator_guide/workflow_rules.md %}) and the Data Disposal type of [Action]({{ site.baseurl }}{% link docs/administrator_guide/actions.md %}). 

### Data Disposal Action Type

The Data Disposal Action will permanently delete all documents that match the Rule conditions if they are outside the Data Retention window.

Data Disposal will only delete files located in valid Data Batch folders. Documents not ingested by Trace will not be deleted.

If a Document is disposed, but not its parent or children, only the disposed Documents files are deleted.

_Only_ documents which were imported as part of a Data Batch which is in the `Completed` or `CompletedWithDocumentLevelErrors` state will be deleted.
{: .info }

The Data Disposal Action Type follows the same Trace Rules Engine paradigm with one added condition:

-   You attach the Data Disposal action to a Rule

-   The rule executes the actions on documents that match the Rule conditions

    -   Searchable Set

    -   Term Searching (optional)

    -   *SPECIFIC TO DISPOSAL*: `Delete Documents Older Than Hours` setting

Any document that is newer than the specified number of hours (based on the System Created On field) will not be deleted even if the document is included in the Searchable Set / Search Term.

This action is used to:
1. Clear out old documents from the Trace workspace
2. Free disk space by deleting **ALL** disposed Document files from the File Share

**Action Configuration**

`Document Delete Batch Size` - controls number of documents to delete at once

All documents will be deleted in a single pass, this is a tweak to improve SQL performance.  Increasing this setting will only take affect if Rule Evaluation task setting (Max Documents Per Execution) is same or higher value.
{: .info }

`Delete Documents Older Than Hours` - controls age of a document (based on System Created On date/time) to delete

**Saved Search Recommendations for Data Disposal**

To protect yourself from disposing documents that have not yet been analyzed by the system or sufficiently reviewed, it is suggested that you add the following conditions to the saved search used for Data Disposal.

| # | Condition | Description |
|:---:|:------:|:-----|
| 1 | `Trace Has Errors` field is `False` | Prevent the disposal of documents that are in an errored stated |
| 2 | `Trace Document Status` any of these: `5 - Ready for Rule Analysis` OR `6 - Alert Rules Complete` | Prevent the disposal of documents that are still being processed by the system |
| 3 | `Trace Alerted On` field is Set AND _Customer Review Field_ is Set | Prevent the disposal of an alerted document that has not yet been reviewed |
