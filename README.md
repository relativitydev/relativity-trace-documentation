---
layout: default
title: Contribute to Documentation
nav_order: 6
---

# Contribute to Documentation
{: .no_toc }


Relativity Trace Documentation is open source, meaning anyone can contribute updates to improve the content.
{: .fs-6 .fw-300 }
{:toc}


---

## Documentation Approach

This documentation process was inspired by: [Microsoft Docs contributor guide](https://docs.microsoft.com/en-us/contribute/) and is based on Markdown language which is lightweight and portable. See more info [here](https://docs.microsoft.com/en-us/contribute/how-to-write-use-markdown).

## What is required to start contributing?

1. Setup GitHub
2. Create a PR
> Please make all enhancements in the **"develop"** branch.
{: .info }
3. Use GitHub UI (for Quick Edits) OR [https://typora.io](https://typora.io/) for more involved changes
4. Submit changes for review and get PR approved

### Quick Edits

Follow this guide: https://docs.microsoft.com/en-us/contribute/#quick-edits-to-existing-documents

### More Involved Edits

1. Download [https://typora.io](https://typora.io/)
2. Open it and then `File` -> `Preferences`
3. Update `Image` Settings according to below
   1. ![image-20210909150142204](media/README/image-20210909150142204.png)
4. ^ this will allow for copying and pasting of images **directly** into Typora


## Key Standard Principles that MUST be followed

If these standard principles are not met the project will not build successfully.
{: .warn }

### Images

Image links MUST reference relative `media` folder AND images must be placed in the folder named after the name of `.MD` file  within relative `media` folder

   1. Example mardown: 
      ```markdown
      ![](media/dynamic_rules/RuleGeneratorLayout.PNG)
      ```
   2. ![image-20210909153552766](media/README/image-20210909153552766.png)
   3. ![image-20210909153615643](media/README/image-20210909153615643.png)
   4. ![image-20210909153640922](media/README/image-20210909153640922.png)

### Links

All `links` MUST be either relative OR refernce root

   1. example: 

      ```markdown
      {% raw %}
          ---
          ---
          [Extensible API's]({{ site.baseurl }}{% link docs/administrator_guide/proactive_ingestion_api_documentation.md %})
      {% endraw %}
      ```

### Callouts

Callouts such as `warn`, `info`, etc...

   Usage (`.info`,` .warn`, `.danger` are currently supported):

   ```markdown
   Do not blah blah blah...
   {: .warn }
   ```

   Information
   {: .info }

   Warning
   {: .warn }

   Danger
   {: .danger }

   


