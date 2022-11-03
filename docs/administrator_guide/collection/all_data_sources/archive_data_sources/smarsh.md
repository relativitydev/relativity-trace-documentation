---
layout: default
title: Veritas Enterprise Vault On-Premises Archive
nav_exclude: true
---

# Smarsh
{: .no_toc }

This topic provides details on how to capture Smarsh archive data via Smarsh's built in automated scheduled export
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Requirements

Before using this data source, note the following license requirements, version support, and special considerations.

### License requirements

Smarsh license

### Supported versions

All Smarsh versions that support Scheduled Export: https://central.smarsh.com/s/article/How-to-Schedule-Exports

## Considerations

Smarsh outputs data in ZIP with EMLs. Trace currently supports plain EMLs only. ZIP needs to be unpacked prior to deliverying data to Trace


## Setup instructions

1. Configure scheduled export: https://central.smarsh.com/s/article/How-to-Schedule-Exports
   1. Underlying saved search must have a condition to select only specified group of monitored people
   2. Run schedule is daily
2. Data will need to flow into RelativityOne Trace SFTP location
3. Data must be unzipped into plain EMLs (ZIP is not currently supported)
