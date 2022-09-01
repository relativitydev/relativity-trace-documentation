---
layout: default
title: Microsoft Active Directory
nav_exclude: true
---

# Microsoft Active Directory Sync
{: .no_toc }

Sync Monitored Individuals with Microsoft Active Directory.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---


## Requirements

Before using this data source, note the following license requirements, version support, and special considerations.

### License requirements

A valid  license is required to use this data source. 

### Supported versions

Versions are supported. 


## Considerations


## Information captured

This section lists what activities and, if applicable, metadata are captured when you use this data source.

### Activities captured

The following table lists activities captured by this data source:

| Activity | Notes |
| -------- | ----- |
|  Users from AD Groups     |      |
|  Metadata associated with Users     |      |


### Activities not captured

The following table lists activities that are not captured by this data source:

| Activity | Notes |
| -------- | ----- |
|          |       |


## Setup instructions

This section provides details on the prerequisites and steps for setting up this data source.

### Prerequisites

You must have the following access configuration.

#### Access Prerequisites
You must have the following access in Enterprise Vault to configure this data source:


#### Microsoft Active Directory specific prerequisites



### Setup in Trace

The following sections provide the steps for installing the VerQu On-Premises Application to collect the data locally, how to use a data transfer method for moving data to RelativityOne, and how to configure the data source in Relativity Trace.

#### VerQu On-Premises Application for Data Collection

1. Navigate to the [Using VerQu]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/using_verqu.md %}) and install, configure, and schedule VerQu.

Some data source specific configuration is required while following the [Using VerQu]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/using_verqu.md %}) steps. That configuration can be found below.


1. Locate the **EntityManagement.AD** file

1. Use the table below as a guide to update the values within that file.

      | Setting                           | Notes                                                        |
      | --------------------------------- | ------------------------------------------------------------ |
      | **ADGroupsToLoad**                 | Comma-separated list of AD Group Names             |
      | **IncludeSubgroups**                     | Optional field that if set to `true` will capture all users in nested groups |

AD Groups MUST have one of the **extended attributes** configured with the value of a respective Trace Data Source name. This will automatically associate the individuals within an AD Group as Monitored Individuals on that Data Source.
{ :warn. }

1. Save the .json configuration files and navigate back to the [Using VerQu]({{ site.baseurl }}{% link docs/administrator_guide/collection/general_data_source_information/using_verqu.md %}) documentation to complete the steps to configure VerQu.

### Data Transfer

[Shipper]({{ site.baseurl }}{% link docs/administrator_guide/collection/shipper.md %}) will be used to transfer on-premises data collected by the VerQu application to Relativity Trace in the cloud.

### Data Source

Use the "Setting Up Data Sources in Relativity" section of the [Shipper]({{ site.baseurl }}{% link docs/administrator_guide/collection/shipper.md %}) documentation to configure the Data Source.
