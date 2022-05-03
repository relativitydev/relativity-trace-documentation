---
layout: default
title: Reviewing Communications
parent: Review
grand_parent: User Guide
nav_order: 2
---

# Reviewing Communications
{: .no_toc }

Communications can be reviewed manually to determine whether midconduct occured.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview
When clicking on a Document within Relativity Trace, the Document Viewer will display that communication in its native format. The Viewer supports the display of more than 900 different file types and is consistent across formats. More information on the Viewer can be found [here](https://help.relativity.com/RelativityOne/Content/Relativity/Viewer/Viewer.htm).

### Text Cleansing Transparency
Content within a communication that has been deemed by our Text Cleansing functionality as either irrelevant (confidentiality disclaimers, headers, email signatures) or duplicative (email segments analyzed in a previous email) will be deemphasized in the viewer. This content was ignored by our Alert Rules and will not generate alerts. This visual treatment allows for compliance teams to focus on the content that matters within the communication.

![viewerScreenshot](/viewerScreenshot.png)

More information on how to enable this functionality can be found [here]({{ site.baseurl }}{% link docs/administrator_guide/enrichment/data_transforms.md %}) at the bottom of the "AI Extracted Text Cleansing Data Transformation" section.
