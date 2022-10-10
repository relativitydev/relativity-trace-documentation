---
layout: default
title: Sync Monitored Individuals from any source using Trace ZipDrop
nav_exclude: true
---

# Monitored Individuals from any sources via Trace ZipDrop
{: .no_toc }

Sync Monitored Individuals generically from any data source using [Trace ZipDrop]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/generic_data_sources/zip_drop.md %})

[Trace ZipDrop]({{ site.baseurl }}{% link docs/administrator_guide/collection/all_data_sources/generic_data_sources/zip_drop.md %}) data source can be used to import Monitored Individuals data. Trace is shipped with ingestion profile named `Default Monitored Individuals Sync` which is set to import objects of type `Monitored Individual` and by design should be used together with `Monitored Individuals Sync` data transformation. 
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Mandatory columns names that need to be included in the load file are:

| Load Fille column name | Relativity Field | Comments |
|:----------------------------:|:----------------------:|:--------:|
| userPrincipalName          | Identifier           | Email Address                                                                                                                                                                                                        |
| displayName                | Full Name            |                                                                                                                                                                                                                      |
| givenName                  | First Name           |                                                                                                                                                                                                                      |
| surname                    | Last Name            |                                                                                                                                                                                                                      |
| ADGroupIDs                 |                      | List of active directory group ids (separated by default with semi-colon). Not ingested into relativity by default. Used with ‘Monitored Individuals Sync’ data transformation to map ids to Data Source names |


`Monitored Individuals Sync` data transformation which should be associated with
Zip Drop data source does the following:

1.  Maps active directory ids specified in ADGroupIDs column to data
    source names
2.  Creates SecondaryIdentifier field by combining existing fields in the load
    file
3.  Unlinks all monitored individuals that are not present in the load file from
    data sources specified in the mapping in point 1, but preserves their
    relationship with other data sources, not set in the transformation settings

Fields created in the load file by the transformation which can be used in
ingestion profile include:

| Load Fille column name | Relativity Field |   Comments    |
|:----------------------------:|:----------------------:|:------------:|
| TraceDataSource            | Data Sources         | Multi value field containing list of data source names generated based on `Group Id To Data Source Name Mapping Json` setting on the data transformation |
| SecondaryIdentifier        | Secondary Identifier | Semi-colon separated list of other load file fields values which are provided in ‘Secondary Identifier User Fields Json’ setting                         |

## Settings of `Monitored Individuals Sync` data transformation:

### Group Id To Data Source Name Mapping Json
User needs to specify how to map active directory group id (specified in
the ADGroupIDs load file field) to Trace Data Source name. One to one mappings
are specified in the JSON format in the fashion similar to this:

```json
[  
    {
        "GroupId":"89e02ec8-e03e-4da7-a637-0ee497d44513",
        "DataSourceName":"Bloomberg Mail"
    },
    {
        "GroupId":"89e02ec8-e03e-4da7-a637-0ee497d44513",
        "DataSourceName":"Bloomberg Chat"
    },
]
```

In this case MI belonging to group 89e02ec8-e03e-4da7-a637-0ee497d44513 will be
mapped into 2 data sources: ‘Bloomberg Mail’ and ‘Bloomberg Chat’

### Secondary Identifier User Fields Json

Json list of column names already existing in the load file that will be
combined into be semicolon separated list and put into SecondaryIdentifier load
file field.

Example setting:

```json
["mail","mobilePhone"]
```

Please note that those columns needs to exist and should be provided by the
customer in the load file.
