---
layout: default
title: Errors and Logging
parent: Setup
grand_parent: Administrator Guide
nav_order: 4
---

# Errors and Logging
{: .no_toc }


Description here...
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

Errors and Logging
------------------

You can adjust the logging level to get more information about the system performance specific to Trace. The Default logging level is Error. The management of the Logging infrastructure can be adjusted via the UI console button “Manage Logs”. In order to adjust the logging level use the “Update Trace Log Level” option. In order to collect and display logging data use the “Trace Logs” option. You can export the logs to a csv file with a mass operation “Export to File” at the bottom of the list.
![](media/8373e739309804e21560cad5d48100e8.png)
![](media/9c4b600add345fd8c2200544796ac735.png)
![](media/187cb16f17210c7e4105f4df34955731.png)

> **CAUTION:** The more verbose logging levels (information/debug) can place substantial load on infrastructure in terms of number of writes and disk space usage (particularly if logs are being written to the EDDSLogging database in SQL, which is the default configuration in new Relativity instances). Don’t forget to adjust your logging level back up to Warning or Error once low level information is no longer needed.


## Restart Trace Agents

You can restart all Trace agents via the "Restart Trace Agents" button on the console within the Setup page. This will disable then re-enable all Agents associated with the Trace application. It will not restart agents associated with other applications that are required as a part of Trace.

> **CAUTION:** Restarting Trace agents will abort all threads for all workspaces. Any in progress Trace work will error. Specifically, in progress Data Batches will be marked Completed With Errors and will have to be retried. 
