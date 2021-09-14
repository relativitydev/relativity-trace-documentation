---
layout: default
title: Data Transformations
parent: Enrichment
grand_parent: Administrator Guide
nav_order: 1
---

# Data Transformations
{: .no_toc }


Data Transformations analyze and enrich communications before they become a document and have the ability to adjust underlying content.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Data Transformations

Data Transformations allow administrators to specify a way data should be transformed while it is being imported by the data source. Trace Data Transformations are attached to a Data Source by clicking Link in the Data Transformations section of the Data Source Layout.

### Replace Data Transformation

Data Transformations of type *Replace* allow you to strip exact blocks of text out of the Extracted Text for any documents imported by the associated Data Source. This allows for removal of things like email signatures and other frequently occurring, benign text so that they do not match Terms. A Data Source can be associated with multiple Data Transformations of type Replace.

By Default, content will simply be replaced with nothing (empty string). This can be changed by entering Match Replacement Text in the Configuration section.

![](media/data_transforms/5c3b02bf2c121e73f3a3916db799b306.png)

Replacement of the Extracted Text (application of replace data transformation) happens on a new copy of the Extracted Text (referenced as *<original_file_name>.replaced.txt*).  Newly generated Extracted Text is referenced in a separate loadfile (`loadfile.replaced.dat`).  In addition, if original loadfile.dat contains a column named `Extracted Text Size in KB` , ONLY then `Extracted Text Size in KB` field is re-generated with updated length.  **Previously generated/supplied data for `Extracted Text Size in KB` is overwritten in this case.**
{: .info}

### Deduplication Data Transformation

Data Transformations of type `Deduplication` prevent a Data Source from importing an original document and its extractions if the same document already exists in the workspace. Only one Data Transformation of type Deduplication should be associated with each Data Source.

For Trace native [Data Sources](#data-sources), deduplication is driven by a SHA256 hashing algorithm that populates the Trace Document Hash field on each document. By Default, if the document is an email, the algorithm will hash together the sender, subject, recipients, sent date, email body and attachment list to create the hash value. If the document is not an email, then the hash will be done directly on the bytes of the file. It is possible to configure the exact hashing algorithm used for emails using the settings in the Configuration section:

![](media/data_transforms/70b0ae9c6debe35956d4988dffaae892.png)

When additional documents are ingested (either within the same Data Batch or different Data Batches), hashes of original documents will be compared to those on documents that already exist in the workspace. If there is a match, the duplicate document will not be ingested. Instead, the Trace Monitored Individuals field on the document will be updated to include the Monitored Individual that was the source of the duplicate in addition to the Monitored Individual that was the source of the original.

#### Required Fields for Deduplication

Deduplication of a Data Source requires that the following Relativity fields be mapped in the Data Source's associated Ingestion Profile.

1. Trace Document Hash
2. Group Identifier
3. Native File Path -- must be specified, but not necessarily mapped.
   
   Because of this requirement, Deduplication is incompatible with [Ingestion Profiles](#Ingestion-Profiles) where Import Natives is set to no.
   {: .info}

### Communication Direction Data Transformation

Data Transformations of type `Communication Direction` can be used to populate the `Trace Communication Direction` field on documents with a communication direction value based on the `Internal Email Domain` objects in the workspace and values in the To, From, CC, and BCC fields in the load file. A specific email address is considered **internal** if the portion of the value to the right of the first `@` matches one of the defined `Internal Email Domains` (NOT case-sensitive), and **external** if it does not match any of the defined `Internal Email Domains`. Here are the possible `Trace Communication Direction` values:

- **Internal** ALL of the email addresses in the From, To, CC, and BCC fields are **internal**
- **Inbound** the From address is **external**, and ONE OR MORE of the email addresses in the To, CC, and BCC fields is **internal**
- **Outbound** the From address is **internal**, and ONE OR MORE of the email addresses in the To, CC, and BCC fields is **external**
- **External** ALL of the email addresses in the From, To, CC, and BCC fields are **external** (unlikely to happen unless `Internal Email Domains` change)
- **Undefined** the From field must contain an email address with a domain and at least one of the To, CC, or BCC fields must contain an email address with a domain or the `Trace Communication Direction` is considered **Undefined** (need one domain in each direction to determine `Communication Direction`)

When using the `Communication Direction` transformation type, analysis is performed only on native documents (top-level) and then the `Trace Communication Direction` value is populated on the native documents and inherited down to all child documents (attachments, embedded objects).

The `Trace Communication Direction` field will not be populated on documents unless it is mapped in the Ingestion Profile associated with the Data Source containing the `Communication Direction` transform.
{: .info}

Use of the `Communication Direction` Data Transformation type requires that columns named To, From, CC, and BCC exist in the load file. This is always true for Data Sources that ship with Relativity Trace but may not be true for certain external data sources.
{: .info}

Use of the `Communication Direction` Data Transformation type requires that a load file column be specified as a Native File Path in the Data Source's [Ingestion Profile](#Ingestion-Profiles). Because of this requirement, Communication Direction is incompatible with Ingestion Profiles where Import Natives is set to no.
{: .info}

### Exempt List Data Transformation

Data Transformations of type `Exempt List` can be used to populate the `Trace Exempt` field on documents with a Yes/No value that indicates whether a particular communication can be excluded from review. The `Trace Exempt` document field is populated based on the `Exempt Entry` objects defined in the workspace. `Exempt List` transformations can specify the `Exempt List Categories` that should apply to the Data Source, or the `Exempt List Categories` field can be left blank in which case all `Exempt Entry` objects in the workspace will be considered. Only one `Exempt List` Data Transformation can be applied to each `Data Source`.

![image-20200602160740161](media/data_transforms/image-20200602160740161.png)

A communication is considered exempt if the `From ` field matches one or more of the `Exempt Entry` objects in the `Exempt List Categories` specified on the `Exempt List` transform.  An `Exempt Entry` has a value in the `Name` field and an `Entry Type` of **Username** (the part before the `@`) **Domain** (the part after the `@`) or the entire **Email Address**. Regardless of the `Entry Type`, all entries are matched **case insensitive** . An `Exempt Entry` can be in one or more Associated Categories, or it can be left without a category in which case it will only apply for transforms that do not specify a category.

> **EXAMPLES:** Consider the email address `John.Doe@Trace.com`
>
> * The **Username** is `John.Doe`
> * The **Email Address** is `John.Doe@Trace.com`
> * The **Domain** is Trace.com
>
> Each of the following `Exempt Entry` objects would match this email address
>
> * `john.doe` of type Username
> * `john.doe@trace.com` of type Email Address
> * `trace.com` of type Domain
>
> Notice case is ignored in all three examples.

![image-20200602160404981](media/data_transforms/image-20200602160404981.png)

When using the `Exempt List` transformation type, analysis is performed only on native documents (top-level) and then the `Trace Exempt` value is populated on the native documents and inherited down to all child documents (attachments, embedded objects).

The `Trace Exempt` field will not be populated on documents unless it is mapped in the Ingestion Profile associated with the Data Source containing the `Exempt List` transform.
{: .info}

Having too many `Exempt Entry` objects in a workspace will increase the memory needs of the `Trace Manager Agent` when running `Exempt List` transformations. If your workspace has more than 5000 `Exempt Entry`  objects defined, please contact [support@relativity.com](mailto:support@relativity.com) to make sure you have adequate system resources available.
{: .info}

Use of the `Exempt List` Data Transformation type requires that a column named From exists in the load file. This is always true for Data Sources that ship with Relativity Trace but may not be true for certain external data sources.
{: .info}

Use of the `Communication Direction` Data Transformation type requires that a load file column be specified as a Native File Path in the Data Source's [Ingestion Profile](#Ingestion-Profiles). Because of this requirement, Exempt List is incompatible with Ingestion Profiles where Import Natives is set to no.
{: .info}

### AI Extracted Text Cleansing Data Transformation

Data Transformations of type `AI Extracted Text Cleansing` can be used to identify and remove non-authored content from the Extracted Text of a document. A single instance of this data transformation must be added to a data source to enable cleansing. It can be configured to remove confidentiality disclaimers, email signatures, and email headers, allowing users to review and run rules on only the relevant information, removing unnecessary text and noise.

When `Remove Email Headers` is enabled, cleansing will always act on the document since headers will always exist in an email, unlike email signatures or confidentiality disclaimers.
{: .info}

![remove-confdentiality-disclaimers-settings](media/user_documentation/remove-confdentiality-disclaimers-settings.png)

When AI Extracted Text Cleansing is performed on a document, `Trace AI Extracted Text Cleansing Status` and `Trace AI Extracted Text Cleansing Error Details` document fields will be populated. `Trace AI Extracted Text Cleansing Status` stores a status denoting whether extracted text was cleansed, not cleansed, or a warning if an error occurred. If an error occurred, information regarding the error will be populated on the `Trace AI Extracted Text Cleansing Error Details` document field.

![cleansing-status-outcome](media/data_transforms/cleansing-status-and-error-outcome.png)

AI Extracted Text Cleansing transformation occurs before any Replace transformations take place. This means, if there are Replace transform that target non-authored content, they will not take effect if that portion of the text is removed by the AI Extracted Text Cleansing transform first.
{: .info}

The long text field, `Trace Original Extracted Text`, stores the original contents of the extracted text prior to any data transformations, acting as a source for unaltered data after Text Extraction. It can be used in place of the Extracted Text field or used to verify results of cleansing.
{: .info}

### Group Identifier Truncation for External Data Sources

`Group Identifier` is a special field in Relativity Trace that is used to power several features including Deduplication. It is essential that a value for `Group Identifier` be provided for every document imported with Trace. Relativity imposes a restriction on the Group Identifier field where the value is not allowed to be longer than 400 characters. The Trace team has found that some external Data Sources populate Group Identifier with a value longer than 400 characters. Instead of failing to import documents from these Data Sources, if the value provided in the field mapped to Group Identifier is longer than 400 characters, Trace will calculate the SHA256 hash of the value and use the hashed value instead. If Group Identifier Truncation occurs, the document is marked as `Trace Has Errors` and the `Trace Error Details` field is filled with a message explaining that a hashed value was used instead of the original Group Identifier value provided.  The message template is of the following format: `{groupIdentifier_SourceFieldDisplayName} length ({groupIdentifierString.Length}) exceeded 400 characters - used hashed string instead`

`Group Identifier` Truncation occurs for EXTERNAL DATA SOURCES ONLY. External Data Sources have a `Provider` on their `Data Source Type` that is not equal to `Trace` or `Globanet`. Running `Group Identifier` Truncation will result in generation of a separate `loadfile.replaced.dat` load file even if no other Data Transformations are defined on the Data Source. For additional information, please contact [support@relativity.com](mailto:support@relativity.com).
{: .info}
