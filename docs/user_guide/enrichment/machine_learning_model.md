---
layout: default
title: Machine Learning Models
parent: Enrichment
grand_parent: User Guide
nav_order: 2
---

# Machine Learning Models
{: .no_toc }


Machine Learning Models can help detect risky content that isn't captured by term searching or identify irrelevant content that shouldn't be alerted on to reduce false-positive alerting.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Machine Learning Models
Check the Machine Learning Models tab to see what Models have been enabled by administrators. Enabled Machine Learning Models are those that have an Active Version set.

## Machine Learning Model Results
The following document fields are created for each Machine Learning Model once the model is enabled (Active Version set).
   1. [Model Name] Decision = Yes or No value on whether the communication is a positive example of the model based on the Rank and the Positive Rank Cutoff value
   2. [Model Name] Score = 0-100 rank on the likelihood the expected outcome occurred with 100 being a high and 0 being low
   3. [Model Name] Version = the Model Version that was set as the Active version when the document was analyzed
   ![Example](media/machine_learning_model/machine_learning_model_fields.PNG)  

[comment]: <> (IMAGE broken line 29) 

### Viewing Machine Learning Model Results
Find the `[Machine Learning Model] Decision` and `[Machine Learning Model] Rank` fields within your views, layouts, and coding pane to understand the model results.

## Additional Information

For setup or detailed information, please see the [Administrator Guide]({{ site.baseurl }}{% link docs/administrator_guide/enrichment/machine_learning_models.md %}).


