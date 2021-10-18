# SMAGetServiceStatus

The SMAGetServiceStatus utility (SMAGetServiceStatus.exe) monitors the
status of windows services. The utility is useful for notifications and
recovery actions.

## Syntax

[]{#aanchor72} Use the following syntax for the SMAGetServiceStatus.exe program in the \<Target Directory\>\\OpConxps\\Utilities\\:

SMAGetServiceStatus.exe "*\<Service Display Name\>*"

### Parameters

The following describes the command-line parameters:

**SMAGetServiceStatus.exe**: The name of the command.

**\<Service Display Name\>**: The "Display Name" for a service (in the
Properties \> General tab) in the Services window. For more details,
refer to [Getting Service Display Names](#Getting_Service_Display_Names).

[]{#Getting_Service_Display_Names}[Getting Service Display Names]{.ul}
To perform the procedure:

1. Use menu path: **Start \> Control Panel \> Administrative Tools \>
    Services**.
2. Scroll through the **Service** list and select the desired
    **Service**.
3. Right-click on the **Service Name** and select **Properties**.
4. Verify that the **General** tab is selected.
5. View the **Display name**.
6. Repeat [Steps 2 -- 5]{.ul} for additional service names.
7. Click **Close ☒**.

### Example

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** Settings for a job  | | circular                         | monitoring SMA Microsoft         |
| background](../../../Reso        | Resource Monitor. If SMA         |
| urces/Images/example-icon(48x48) | Microsoft Resource Monitor is    |
| .png "Example icon") | stopped,                         |
|                                  | OpCon |
|                                  | notifies the administrator by    |
|                                  | way of email.                    |
|                                  |                                  |
|                                  | In the Job Details screen, the   |
|                                  | Command Line is:                 |
|                                  |                                  |
|                                  | "\<Target                       |
|                                  | Directory\>\\OpConxps\\Util      |
|                                  | ities\\SMAGetServiceStatus.exe" |
|                                  | "SMA Microsoft Resource         |
|                                  | Monitor"                        |
|                                  |                                  |
|                                  | In the Job Details screen, the   |
|                                  | Exit Code is EQ -2.              |
|                                  |                                  |
|                                  | In the Events screen:            |
|                                  |                                  |
|                                  | a.  The status is                |
|                                  |     '**Failed**'.              |
|                                  | b.  The Event is                 |
|                                  |     $                           |
|                                  | NOTIFY:EMAIL,Admin\@Company.com, |
|                                  |     SMA Microsoft Resource       |
|                                  |     Monitor, SMA Microsoft       |
|                                  |     Resource Monitor is Down.    |
|                                  |                                  |
|                                  | If desired, create other events  |
|                                  | for notification actions within  |
|                                  | ENS manager.                     |
+----------------------------------+----------------------------------+

## Scheduling

A job should be added to the SMAUtility schedule to run the
SMAGetServiceStatus utility at regular intervals each day (e.g., Once
per hour, or once every 15 minutes). For additional information, refer
to [SMAUtility Schedule](../../objects/schedules.md#smautility-schedule) in
the **Concepts** online help.

### Job Details

- The Command Line is:
- The Working Directory is:

## Exit Values

The SMAGetServiceStatus.exe program uses the following exit values:

  Code                                   Value
  -------------------------------------- -------
  RUNNING                                0
  NO_SERVICE_SPECIFIED_ON_COMMAND_LINE   -1
  STOPPED                                -2
  START_PENDING                          -3
  STOP_PENDING                           -4
  CONTINUE_PENDING                       -5
  PAUSE_PENDING                          -6
  SERVICE_PAUSED                         -7

  : Service Status Codes

  Code                         Value
  ---------------------------- -------
  PATH_NOT_FOUND               3
  ACCESS_DENIED                5
  INVALID_HANDLE               6
  INVALID_PARAMETER            87
  SERVICE_IS_PAUSED            928
  DEPENDENT_SERVICES_RUNNING   1051
  INVALID_SERVICE_CONTROL      1052
  SERVICE_REQUEST_TIMEOUT      1053
  NO_THREAD                    1054
  SERVICE_DATABASE_LOCKED      1055
  SERVICE_ALREADY_RUNNING      1056
  SERVICE_DISABLED             1058
  SERVICE_DOES_NOT_EXIST       1060
  SERVICE_CANNOT_ACCEPT_CTRL   1061
  SERVICE_NOT_ACTIVE           1062
  SERVICE_SPECIFIC_ERROR       1066
  SERVICE_DEPENDENCY_FAIL      1068
  SERVICE_LOGON_FAILED         1069
  SERVICE_START_HANG           1070
  SERVICE_MARKED_FOR_DELETE    1072
  SERVICE_EXISTS               1073
  SERVICE_DEPENDENCY_DELETED   1075
  SERVICE_NEVER_STARTED        1077
  SERVICE_NOT_IN_EXE           1083
  SHUTDOWN_IN_PROGRESS         1115
  SERVICE_NOT_FOUND            1243

  : Unable to Connect to Service Control Manager and Service State
  Change Errors
:::
