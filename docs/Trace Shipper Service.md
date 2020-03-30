# Trace Shipper Service

The Trace Shipper Service is a Windows service released by Trace that delivers data from on-premise client network to Relativity Trace enabled workspace.  The service monitors configured source folders on the local network and ships files that appear in the source folder to a predetermined file share location within a Relativity workspace that is associated with the data sources. The files are continuously deleted from the source folder once they have been transmitted to Relativity successfully. 

### Overview

![TraceShipperOverview](S:\SourceCode\relativity-trace-documentation\docs\media\TraceShipperOverview.png)


### Prerequisites Before Installing

- Identify/provision a Windows OS machine to run the Trace Shipper Service
> **NOTE:** This should be the same machine as Globanet appliance VM
- Identify what source folder(s) on your local network need their files shipped to a Relativity
> **NOTE:** Windows service must have read/write/modify permission on the folders
- Create/identify a Windows OS user to run the service as that has access to all folders that need to be shipped and that can be allowed access to Relativity user credentials stored in configuration
- Lookup the destination Relativity Instance(s), Workspace(s) and Target folder(s) on the destination fileshare(s) where the files should be shipped (configured as part of creating Trace Data Sources)
- Create a designated Relativity username and password for each destination that can be used to authenticate against a Relativity API with appropriate rights
- Request the Trace Shipper deployment package by submitting a ticket to support@relativity.com

### Installation Steps

1. Extract `TraceShipperService_vx.zip` to a folder called `Trace Shipper Service` on the machine that will be running the service. Make sure that the files are directly under the `Trace Shipper Service` directory with no extra nested folders.
2. Run a command prompt AS ADMINISTRATOR, navigate to the `Trace Shipper Service` folder in the command prompt, and run `TraceShipperService.exe /i`
3. Go to Services on the machine and verify that the service was installed (`Trace Shipper Service`)
4. From the Services window, right click on the `Trace Shipper Service` and select Properties, and then on the Log On tab configure the service to run as the user with proper access to the local folders
5. In the `Trace Shipper Service` folder, edit the `TraceShipperService.exe.config` file. 
   1. In the `<trace.shipper>` section, copy the default <add> node so that there are as many nodes as folders that need to ship files (if there is just one folder, no need to copy, we will edit the example)
   2. For each folder that needs to ship, edit each attribute in the <add> node to be correct
      1. **localDirectoryPath** - the locally accessible path of the folder that needs to ship files (note the user running the service must have access)
      2. **remoteRelativityPath** - the path relative to the workspace fileshare root of the destination workspace where all files should be stored
      3. **cacheLengthInMinutes** - how long a file is ignored by monitoring before Trace Shipper Service attempts to send it to Relativity again (provides a buffer for long transfer times and surges in volume as well as automatic retries of failed transfers)
      4. **logLevel** - the minimum message level to include in the log file (Verbose/Debug/Information/Warning/Error/Fatal), increase if log files are too large, decrease when troubleshooting
      5. **logFilePath** - a local file path **ACCESSIBLE TO THE SERVICE USER** where the log files for the application should be stored (note, the log files roll automatically every 100MB, so there will be more than one file, it is best to make a folder) (note 2, it recommended to use a different log file path for each configured local folder to make the logs easier to read)
      6. **clientType** - Transfer API client type to use, current supported options are Aspera and Fileshare, contact support@relativity.com for more information
      7. **relativityUserName** - the username used to connect to Relativity to upload files (note, it is recommended to secure the TraceShipperService folder as a way to reduce risk of exposing these credentials)
      8. **relativityPassword** - the password used to connect to Relativity to upload files (note, it is recommended to secure the TraceShipperService folder as a way to reduce risk of exposing these credentials)
      9. **relativityUrl** - the url of the Relativity Instance where the files will be shipped
      10. **workspaceId** - the workspace ID of the workspace where the files will be shipped
6. From the Services window, Start the `Trace Shipper Service`. If all configuration is correct, files should start departing the local source folders and showing up on the Relativity fileshare as configured.
7. If the Service fails to start, look at the Application Event Logs (Event Viewer > Windows Logs > Application) to see any errors.
8. If the Service starts but does not ship files, look at the log files (as configured in the logFilePath setting) to see what messages are logged.
9. Finally, once everything is running well, use Windows permissions to secure the `Trace Shipper Service` folder and the configured logs folder to only users that should be able to access the sensitive information contained within (Relativity credentials, file paths, etc.).

### Starting/Stopping Service
The service can be managed directly from Services window (you can quickly navigate to the window by executing `services.msc` in the Windows task bar)

### Uninstall Steps

1. Run a command prompt AS ADMINISTRATOR
2. Navigate to the `Trace Shipper Service` folder in the command prompt
3. Run `TraceShipperService.exe /u`