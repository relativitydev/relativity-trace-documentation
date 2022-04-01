---
layout: default
title: Auto Coding Communication
parent: Review
grand_parent: User Guide
nav_order: 4
---

# Auto Coding Communication
{: .no_toc }

For increasing efficiency of the review, user can reduce number of fields in need for coding through setting default review decisions that are automatically populated when a communication is viewed.

{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview

User can set up default decision for a given field placed on the coding layout. Field will be automatically populated with this value when communication is viewed. Every automatically populated decision can be changed during the review at any time. There could be seperate auto coding decisions for the same field across different layouts.

For setting defualt coding decision:

1. Navigate to `Auto Code Configuration` tab in the given workspace.
![Document Action Menu](media/auto_coding_communication/auto_coding_1.png)

2. Click "New Auto Code Configuration" button.

3. Provide "Layout Name", "Field Name" and preffered coding "Value" (expected defualt value for the field).
![Document Action Menu](media/auto_coding_communication/auto_coding_2.png)

4. When done click "Save" 

From this moment when reviewing communication under given layout given field will be automatically popoulated with the provided value.

Supprted field types are limited to (Single Choice, Multiple Choice, Fixed Text Length, Long Text Length, Yes/No, Whole Number, Decimal, Currency)
{: .info }

If “Copy from Previous” is enabled for any of the fields in the default coding decision configuration then auto coding will not be applied to that field
{: .info }