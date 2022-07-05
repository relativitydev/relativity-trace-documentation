---
layout: default
title: Dynamic Searching
parent: Enrichment
grand_parent: Administrator Guide
nav_order: 6
---
# Dynamic Searching
{: .no_toc }

Dynamic Searching is a feature, which allows user to perform search for different objects than Trace Terms. 

1. TOC
{:toc}

---
## Dynamic Searching Configuration
Dynamic Searching can be configured in `Data Transformation` task using `Dynamic Searching Object Types Json` setting. In this setting user can set up a list of object types and object types' fields for which searching should be performed. 

![](media/dynamic_searching/DynamicSearchingConfigurationSetup.PNG)

### Dynamic Search Configuration Parameters

`Dynamic Searching Object Types Json` field is inputted as JSON with each `{}` representing a single object type and field in that object type.

**Parameters of `Dynamic Searching Object Types Json`:**
- `ObjectTypeName` - [Required] an object type for which search will be performed
- `FieldName` - [NotRequired] a field which value will be used to perform search (by default it is set to `Identifier`)


**Example `Dynamic Searching Object Types Json` configuration:**
```json
[
   {
      "ObjectTypeName":"Financial Products",
      "FieldName":"Identifier"
   },
   {
      "ObjectTypeName":"Pharmaceutical Product"
   }
]
```

> **`Dynamic Searching Object Types Json` Validation Rules:**
>
> - `ObjectTypeName` must be a name of object type which exists in the workspace
> - One object type can occur only once in `Dynamic Searching Object Types Json` configuration
> - `FieldName` must be a field which exists for gived object type, also it must be a fixed-length field which is an object type's identifer
> - Object type can't be saved in configuration if there are no RDOs of gived object type
> - Object type can't be saved in configuration if there are RDOs of this object type with duplicated values in identifer field

## Dynamic Searching Execution

After saving dynamic search configuration

