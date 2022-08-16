---
layout: default
title: Document Statuses
parent: Data Flow
grand_parent: Administrator Guide
nav_order: 2
---

# Document Statuses
{: .no_toc }


Documents get a status as they progress through the data flow.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Status Descriptions
Trace has a six-step Document Analysis process. Status is tracked on the `Trace Document Status` field. When a document status is changed the timestamp on the `Trace Document Status Updated On` field is updated.

| Step | Status                 |  Type        | Overview                                                    |
| :--: | ----------------------- |------------|------------------------------------------------------------ |
|  1   | NEW                     | Transient  | Documents that are brand new to the workspace and are part of `Trace All Documents` saved search. Documents not included in the `Trace All Documents` saved search will not be included in the data flow. |
|  2   | INDEXED                 | Transient  | Documents that have been successfully indexed. |
|  3   | TERM SEARCHED           | Transient  | Documents where Terms have been successfully searched for. |
|  4   | NORMALIZED              | Transient  | Documents that meet the criteria of the `Normalized Saved Search` configuration in the `Rule Evaluation` task. <br/><br/>**NOTE:** Documents can only be moved to the `Normalized status` if they and all their family members are in the `Term Searched` status.<br/><br/>**NOTE:** If `Normalized Saved Search` is not configured, documents will move to `Normalized` once they and all their family members have the `Term Searched` status. |
|  5   | READY FOR RULE ANALYSIS | Terminal   | Documents that have the `Normalized` status and don't meet the criteria of the `Omit from Alert Rules Saved Search` configured in the `Rule Evaluation` task. Both `Alert` and `Workflow` `Rules` will analyze documents with the `Ready for Rules` status. |
|  6   | ALERT RULES COMPLETE    | Terminal   |Parent Document that meet the criteria of the `Omit from Alert Rules Saved Search` configuration in the `Rule Evaluation` task and all of their children. `Alert Rules` will NOT analyze these documents. <br/><br/>**NOTE:** If ``Omit from Alert Rules Saved Search`` is not configured, no documents will be marked with the `Alert Rules Complete` status. |

To identify documents that are stuck in the flow and no longer progressing through the statuses, it is advised that you create a document view that shows documents with a status of  `1 - New`, `2 - Indexed`, OR `3 - Term Searched` and sort the documents in ascending order by the `Trace Document Status Updated On` field, so that documents that have been stuck in a non-terminal status for a significant period of time are identified at the top of your view.
{: .info }
