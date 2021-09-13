---
layout: default
title: Integration Profiles
parent: Ingestion
grand_parent: Administrator Guide
nav_order: 3
---

# Integration Profiles
{: .no_toc }


Ingestion profiles store configuration for ingesting content into Relativity Trace.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Ingestion Profile Fields

Most fields have a default value that will not need to be changed except for advanced use cases.

`Name` - The name of the ingestion profile. 

`Workspace Destination Folder` - The folder in the workspace to which documents will be imported.

`Data Mappings` - A list of data mappings used for mapping columns in the loadfile to fields in Relativity.

`Overwrite Behavior` - describes how importing documents with the same identifier should be handled

​	**Append Only** - only add documents with no identifier collisions to the workspace

​	**Overlay Only** - only update documents with identifier collisions

​	**Append/Overlay** - Adds documents without collisions and updates the ones with collisions

`FieldOverlayBehavior` - This field only applies if either Overlay Only or Append/Overlay are selected for overwrite behavior. This field describes how specific fields are updated when a collision occurs.

​	**Merge Values** - Merges values for all multi-choice and multi-object fields with corresponding choices/values in the workspace

​	**Replace Values** - Replaces all values for all multi-choice and multi-object fields with corresponding choices/values in the workspace

​	**Use Field Settings** - Merges or replaces multi-choice and multi-object fields with corresponding choices/values in the workspace based on the settings on the field

`Native File Path Location` - A data mapping containing the name of the column in the loadfile that specifies the native file path. The selected data mapping MUST be in the data mappings list on the Ingestion Profile

`Import Natives` - A yes/no field specifying whether or not Natives should be linked to any documents imported with the Ingestion Profile. If Yes, `Native File Path Location` is required to be linked to a data mapping of type NativeFilePath. If No, `Native File Path` MUST be unlinked. 

Importing Native files is required for [Deduplication](#deduplication-data-transformation), [Communication Direction](#communication-direction-data-transformation), and [Exempt List](#exempt-list-data-transformation) Data Transformations.
{: .info }


`Column Containing File Location` - A data mapping containing the name of the column in the loadfile that contains a text file location. The imported field on the document will display the contents of the text file instead of the file path. This field is optional.

`Encoding for Undetectable Files` - Encoding for the text file specified in the Column Containing File Location. 

`Loadfile Encoding` - The encoding for the loadfile that will be used with this ingestion profile

`Column` - The ascii character that will be used as a column delimiter in the loadfile

`Quote` - The ascii character that will be used as a quote delimiter in the loadfile

`Multivalue` - The ascii character used to delimit choices in a given column

`Nested Value` - The ascii character used to delimit different levels of a multi-choice hierarchy

## Data Mappings

Data mappings are a link between a column in a loadfile and a field in Relativity. 

### Data Mapping Fields

`Source Field Name` - The name of the column in the loadfile that will be used with the ingestion profile

The Source Field Name is case sensitive when matching with a column in the loadfile.
{: .info }

`Relativity Field` - The field in Relativity that will have it's value populated

`Type` - Data mapping type indicates if there is anything special about the data mapping. 

​	**None** - Standard data mappings will have this type. A source field and Relativity field are both required for this type.

​	**Native File Path** - This indicates that the source field column in the loadfile contains the native file path. This field does not require a destination Relativity field. Only one data mapping of this type can exist on an ingestion profile. The single data mapping of this type must also be selected on ingestion profile's `Native File Path Location` field. 

​	**Identifier** - This indicates that the destination Relativity field is the document identifier for the workspace. A source field and Relativity field are both required for this type. Only one data mapping of this type can exist on an ingestion profile.

**Read From Other Metadata Column** - If this field is checked, this data mapping will not read from the load file column with the same name as the source field name. Instead, it will read from the "Other Metadata" field, if it exists, and search for a key with the same name as the source field name. If a matching key is found, then the value associated with the key will be imported into the destination Relativity Field.

The "Other Metadata" field is populated by Trace during extraction. It consists of a JSON list of key value pairs.
`[{Key: "This should match source field name", Value: "This value will be read into Relativity"}]`
{: .info }

Unlike standard data mappings that read directly from the load file, it is possible that the "Other Metadata" field JSON will not contain the key specified by Source Field Name. In this case, Trace will not error, it will import an empty value.
{: .info }

Contents of the "Other Metadata" field will change from file to file, especially between different file types. To understand possible headers and other metadata that can be pulled from this field, create a standard Data Mapping to import the contents of the "Other Metadata" field. You can then decide which metadata keys you would like to pull by adding a Data Mapping with 'Read From Other Metadata Column' checked.
{: .info }

### Adding Encoding Choices

By default, Trace only ships with two encodings (UTF-8 and Windows-1252). More encoding choices can be added for the Ingestion Profile single choice fields `Loadfile Encoding` and `Encoding for Undetectable Files`. The name of the encoding choice you wish to add must be able to be parsed as a valid encoding. See [here](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?view=netframework-4.6.2#list-of-encodings) for a list of supported encodings. When choosing from the supported encoding list, you must use the `Name` of the encoding as the choice name (e.g. IBM037, **not** IBM EBCDIC). Encoding support is validated when saving the Ingestion Profile with the specific encoding choice selected.
