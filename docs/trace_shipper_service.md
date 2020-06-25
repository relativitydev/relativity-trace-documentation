# Trace Shipper Service Documentation

The Trace Shipper Service is a Windows service released by Trace that delivers data from the client network to a remote Relativity Trace workspace. The service monitors configured source folders on the local network and ships files that appear in the source folders to predetermined file share locations within a Relativity workspace that are associated with Trace Data Sources. The files are deleted from the source folder once they have been transmitted to Relativity successfully. 

### Overview

![TraceShipperOverview](media/TraceShipperOverview.png)

### Trace Data Shipper Advantages
1. Fully managed Windows service with Trace specific semantics and configuration
   1. Integration with IT policies managing Windows reporting/alerting
   2. Robust mechanism for retrying in case of data transfer failures
   3. Integration of Data Source configuration from Relativity side
2. No need for VPN setup
   1. Faster onboarding of clients
   2. Fewer dependent components in data transfer
3. Fast data transfer rates
4. Secure (data encrypted in flight)

### Prerequisites Before Installing

- Identify/provision a Windows machine to run the Trace Shipper Service
> **NOTE:** This should be the same machine as Globanet appliance VM
- Identify what source folder(s) on your local network need their files shipped to a Relativity
> **NOTE:** Windows service must have read/write/modify permission on the folders
- Create/identify a Windows user to run the service (Log on as...) that has access to all folders that need to be shipped and that can be allowed access to Relativity user credentials stored in configuration
- Lookup the destination Relativity Instance(s), Workspace(s) and Target folder(s) on the destination fileshare(s) where the files should be shipped (configured as part of creating Trace Data Sources)

> **NOTE:** A document will fail to ship if a file with the same name already exists in the destination folder. Care should be taken to avoid duplicate file names both when initially retrieving data and when shipping multiple source folders to a single destination folder.

- Create a designated Relativity username and password for each destination that can be used to authenticate against a Relativity API with appropriate rights
> **NOTE:** To view the file shares the user must be in a group, other than the System Administrator group, that is added to at least one workspace built on the Resource Pool with the associated file shares.
- Request the Trace Shipper deployment package by submitting a ticket to support@relativity.com
- Download and install ROSE (Staging Explorer) and run Test Connectivity (https://help.relativity.com/RelativityOne/Content/Relativity/RelativityOne_Staging_Explorer/RelativityOne_Staging_Explorer.htm#connection)

### Data Transfer Protocols
Transfer API (TAPI) is the underlying method of data delivery to RelativityOne.  TAPI supports multiple protocols of data transfer including:
1. Direct - only available on-premise
2. Aspera (FASP protocol) - default for RelativityOne

### Ports and Firewall settings
For the Aspera data transfer protocol, the following ports must be configured:
1. Allow outbound connections to the server on the TCP port 33001, 9092.
2. Allow outbound connections to the server on the UDP ports 33001 - 33050, 33101, 33102.
3. Allow outbound connections to the server on HTTPS (443)

For details on the IP ranges for your specific RelativityOne instance please contact support@relativity.com


### Installation Steps

1. Extract `TraceShipperService_(version).zip` to a folder called `Trace Shipper Service` on the machine that will be running the service. Make sure that the files are directly under the `Trace Shipper Service` directory with no extra nested folders.
2. Run a command prompt AS ADMINISTRATOR, navigate to the `Trace Shipper Service` folder in the command prompt, and run `TraceShipperService.exe /i`
3. Go to Services on the machine and verify that the service was installed (`Trace Shipper Service`)
4. From the Services window, right click on the `Trace Shipper Service` and select Properties, and then on the Log On tab configure the service to run as the user with proper access to the local folders
5. In the `Trace Shipper Service` folder, edit the `TraceShipperService.exe.config` file. 
   1. In the `<trace.shipper>` section, copy the default <add> node so that there are as many nodes as folders that need to ship files (if there is just one folder, no need to copy, we will edit the example)
   2. For each folder that needs to ship, edit each attribute in the <add> node to be correct
      1. **localDirectoryPath** - the locally accessible path of the folder that needs to ship files (note the user running the service must have access)
      2. **remoteRelativityPath** - the path relative to the workspace fileshare root of the destination workspace where all files should be stored
      3. **retrieveConfigurationIntervalInMinutes** -- the interval between Data Source configuration pulls from Relativity. Values less than or equal to 0 turns off this feature. Defaults to 0 (off) if not present. This setting is used to synchronize, for example, monitored individuals from Relativity One to a local Globanet instance. For further customization of Data Source configuration pulling, contact support@relativity.com.
      3. **cacheLengthInMinutes** - how long a file is ignored by monitoring before Trace Shipper Service attempts to send it to Relativity again (provides a buffer for long transfer times and surges in volume as well as automatic retries of failed transfers)
      4. **logLevel** - the minimum message level to include in the log file (Verbose/Debug/Information/Warning/Error/Fatal), increase if log files are too large, decrease when troubleshooting
      5. **logFilePath** - a local file path **ACCESSIBLE TO THE SERVICE USER** where the log files for the application should be stored (note, the log files roll automatically every 100MB, so there will be more than one file, it is best to make a folder) (note 2, it recommended to use a different log file path for each configured local folder to make the logs easier to read)
      6. **clientType** - Transfer API client type to use, current supported options are Aspera and Fileshare, contact support@relativity.com for more information
      7. **relativityUserName** - the username used to connect to Relativity to upload files (note, it is recommended to secure the TraceShipperService folder as a way to reduce risk of exposing these credentials)
      8. **relativityPassword** - the password used to connect to Relativity to upload files (note, it is recommended to secure the TraceShipperService folder as a way to reduce risk of exposing these credentials)
   > **NOTE:** The user/password fields must comply with CDATA XML standard (XML friendly).  Special characters that break XML configuraiton are now allowed.
      9. **relativityUrl** - the url of the Relativity Instance where the files will be shipped
      10. **workspaceId** - the workspace ID of the workspace where the files will be shipped
6. From the Services window, Start the `Trace Shipper Service`. If all configuration is correct, files should start departing the local source folders and showing up on the Relativity fileshare as configured.
7. If the Service fails to start, look at the Application Event Logs (Event Viewer > Windows Logs > Application) to see any errors.
8. If the Service starts but does not ship files, look at the log files (as configured in the logFilePath setting) to see what messages are logged.
9. Finally, once everything is running well, use Windows permissions to secure the `Trace Shipper Service` folder and the configured logs folder to only users that should be able to access the sensitive information contained within (Relativity credentials, file paths, etc.).

### Starting/Stopping Service
The service can be managed directly from the Services application in Windows (you can quickly navigate to the window by executing `services.msc` in the Windows task bar)

### Uninstall Steps

1. Run a command prompt AS ADMINISTRATOR
2. Navigate to the `Trace Shipper Service` folder in the command prompt
3. Run `TraceShipperService.exe /u`
