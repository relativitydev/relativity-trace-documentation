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
| 9/15/2021  | 2501    | Data Transformations | `AI Extracted Text Cleansing` Data Transforms are being added to the `Trace Data Transformations` document field, letting you know that the Data Transform was applied to the document. In the interim you can look to the `Trace AI Extracted Text Cleansing Status` for similar information. | Yes |
| 4/28/2022  | 4097    | Trace Searching Task Configuration | `Perform Term Searching On Trace Cleansed Extracted Text` checkbox does not control the text that is used for Term Searching, instead the fields set in the `Trace All Documents` Saved Search will still be honored. | Yes |
| 6/28/2022  | 4564    | Machine Learning Model Data Mapping | If a user sets and then removes an active version for a 'Machine Learning Model', they will not be able to see results from another version. As a work around, do not have the 'Active Version' field be empty after set.| Yes |
| 6/28/2022  | 4569    | Build New Machine Learning Model | A user cannot put special characters into the 'New Machine Learning Model' Name field, for example the model cannot be "Trace's Model" | Yes |
| 6/28/2022  | 4567    | Machine Learning Model Tab | The Machine Learning Model tab is wrongfully set to Not Visible making it where the Machine Learning functionality cannot be used | Yes |
| 7/19/2022  | 4722    | Language Identification Transformation | The `Trace Other Langauges` field is misspelled and should be `Trace Other Languages` | Yes |
| 7/19/2022  | 4664    | Language Identification Transformation | The `Trace Other Languages` field results should not include the confidence scores and just be a list of languages. | Yes |
| 9/6/2022  | 5036    | AI Extracted Text Cleansing - Short Message | Trace fails to remove disclaimers from Reuters Chats | No |
