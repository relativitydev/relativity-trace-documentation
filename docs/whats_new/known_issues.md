---
layout: default
title: Known Issues
parent: What's New
nav_order: 2
---

# Known Issues
{: .no_toc }

The following list provides descriptions of known issues in Relativity Trace. For a list of Relativity Trace enhancements and resolved issues, please visit the [Release Notes](/release_notes.md).
{: .fs-6 .fw-300 }

---

| Date Added | Issue # | Feature      | Description                                                  | Resolved |
| ---------- | ------- | ------------ | ------------------------------------------------------------ | -------- |
| 9/6/2021   | 1178    | Data Sources | Documents protected with Azure Information Protection (AIP) are currently not showing in the Relativity Viewer. | No       |
| 9/15/2021  | 2501    | Data Transformations | `AI Extracted Text Cleansing` Data Transforms are being added to the `Trace Data Transformations` document field, letting you know that the Data Transform was applied to the document. In the interim you can look to the `Trace AI Exctracted Text Cleansing Status` for similar information. | Yes |
| 4/28/2022  | 4097    | Trace Searching Task Configuration | `Perform Term Searching On Trace Cleansed Extracted Text` checkbox does not control the text that is used for Term Searching, instead the fields set in the `Trace All Documents` Saved Search will still be honored. | Yes |
