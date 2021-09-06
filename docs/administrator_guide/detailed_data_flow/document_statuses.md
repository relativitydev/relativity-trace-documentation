---
layout: default
title: Document Statuses
parent: Detailed Data Flow
grand_parent: Administrator Guide
nav_order: 1
---

# Document Statuses
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

Trace Document Flow Overview
============================
Trace has a six-step Document analysis process. Status is tracked on the `Trace Document Status` field. When a document status is changed the timestamp on the `Trace Document Status Updated On` field is updated.

| Step | Status:                 | Overview:                                                    |
| :--: | ----------------------- | ------------------------------------------------------------ |
|  1   | NEW                     | Documents that are brand new to the workspace and are part of `Trace All Documents` saved search. |
|  2   | INDEXED                 | Documents that have been successfully indexed.               |
|  3   | TERM SEARCHED           | Documents that have been successfully searched by Term Searching task. |
|  4   | NORMALIZED              | Documents and their family that have completed all normalization processes, as defined by the `Normalized Saved Search` field criteria configured in the `Rule Evaluation` task. <br/><br/>**NOTE:** Documents can only be moved to the `Normalized status` if they and all their family members are in the `Term Searched` status. <br/><br/>**NOTE:** If `Normalized Saved Search` is not populated, documents will move to `Normalized` once they and all their family members are in the `Term Searched` status. |
|  5   | READY FOR RULE ANALYSIS | Documents that have been `Normalized` and don't meet the criteria of the  `Omit from Alert Rules Saved Search` configured in `Rule Evaluation` task. Both `Alert` and `Workflow` `Rules` will analyze these documents. |
|  6   | ALERT RULES COMPLETE    | Documents which are returned by `Omit from Alert Rules Saved Search` configured in `Rule Evaluation` task along with their family. `Alert` `Rules` will NOT analyze these documents. <br/><br/>**NOTE:** If ``Omit from Alert Rules Saved Search`` is not configured, no documents will be marked with the `Alert Rules Complete` status. Only `Workflow` `Rules` will analyze these documents. |

> **TIP:** To identify documents that are stuck in the flow and no longer progressing through the statuses, it is advised that you create a document view that shows documents with a status of  `1 - New`, `2 - Indexed`, OR `3 - Term Searched` and sort the documents in ascending order by the `Trace Document Status Updated On` field, so that documents that have been stuck in a non-terminal status for a significant period of time are identified at the top of your view.
