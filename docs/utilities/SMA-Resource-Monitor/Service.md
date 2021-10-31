# SMA Resource Monitor Service

The SMA Resource Monitor service reads the Rule files to determine what
to monitor. When a monitored resource rule is met, the service reads the
Actn files to send OpCon events to the SAM.

:::note
When a mapped drive or UNC path is specified in File Name Path, the Resource Monitor Service needs to be running as a domain user who has access to mapped drives or the UNC path being monitored.
:::

## Configure the SMA Resource Monitor Service Log On

Use menu path: **Start \> Settings \> Control Panel**.

Double-click the **Administrative Tools** icon.

Double-click the **Services** icon to run the Service Control Manager.

Double-click the **SMA Microsoft Resource Monitor** in the **Services**
list.

If not selected already, select **Automatic (Delayed Start)** from the
**Startup Type** drop-down list box.

:::warning
SMA Technologies recommends leaving the SMA Microsoft Resource Monitor service set to Automatic (Delayed Start) to avoid potential issues at startup time while other services and programs start up.
:::

Click the **Log On** tab.

To run the service as the Local System Account:

a.  Click **Local System** account radio button.
b.  Click **OK**.

To run the service as a Domain User:

a.  Click **This account** radio button.
b.  Click **Browse** to find the *Domain User*.
c.  Click the **Domain User**.
d.  Click **OK**.

**Close ☒** the **Services** window.

## Start the SMA Resource Monitor Service

1. Use menu path: **Start \> Settings \> Control Panel**.
2. Double-click the **Administrative Tools** icon.
3. Double-click the **Services** icon to run the Service Control
    Manager.
4. Click the **SMA Microsoft Resource Monitor** in the Services list.
5. Use menu path: **Action \> Start**.
6. Confirm the SMA Microsoft Resource Monitor's **Status** is
    **Started**.
7. **Close ☒** the **Services** window.

## Stop the SMA Resource Monitor

1. Use menu path: **Start \> Settings \> Control Panel**.
2. Double-click the **Administrative Tools** icon.
3. Double-click the **Services** icon to run the Service Control
    Manager.
4. Click the **SMA Microsoft Resource Monitor** in the Services list.
5. Use menu path: **Action \> Stop**.
6. Confirm the SMA Microsoft Resource Monitor's **Status** is
    **Stopped**.
7. **Close ☒** the **Services** window.

## Logging

:::note
The Output Directory was configured during installation. For more information, refer to [File Locations](../../file-locations.md) in the **Concepts** online help.
:::

The SMA Resource Monitor creates a single log file located in the: `<Output Directory\>\\SMAResourceMonitor\\Log\\` directory.

The log file is named SMAResourceMonitor.log

The SMA Resource Monitor archives log files when they reach the maximum
log file size configured in the .ini file. All archived log files reside
in the: `<Output Directory\>\\SMAResourceMonitor\\Log\\Archive` folder.

If an archive folder for the day does not already exist, the SMA
Resource Monitor creates one. The folder names use the following naming
convention: yyyy_mm_dd (Weekday). The logging mechanism generates the
weekday name matching the format recognized by the regional settings of
the user running the SMA Resource Monitor service.

:::tip Example
Make sure the file is done arriving before it is created.

For large file transfers, it takes time for the complete file to arrive. Set the 'Wait Verify' value high enough to make sure that the file should not have changed size in that time. As soon as the size matches the same previous size and the file is no longer in use, the action group(s) will be triggered.
:::

As a log file fills up, SMA Resource Monitor moves it to the current
archive folder and renames it using the following naming convention: SMA
Resource Monitor StartTime - StopTime.log.

:::tip Example
An SMA Resource Monitor archive file for the time range of 12:58:16 to 13:58:00 would be named SMAResourceMonitor 125816 - 135800.log.
:::

Once per day the SMA Resource Monitor deletes old archive folders. The
SMA Resource Monitor retains 10 days of archived logs by default. If
desired, change the Log Archive Max Retention setting in the .ini file.

## Configuration

The configuration for the SMA Resource Monitor service and UI is managed
through a single .ini file named SMAResouceMonitor.ini.

### Modify the SMAResourceMonitor.ini File

1. Right-click on **Start** and select **Explore** from the menu.
2. Browse to the <Configuration Directory\>\\SMAResourceMonitor\\
    directory on the OpCon server.
3. Find the **SMAResourceMonitor.ini** file.
4. Right-click the file and select **Open With**.
5. Select an ASCII text editor (e.g., Notepad) from the **Choose the
    program you want use** list box.
6. Make any necessary modifications to the .ini file in the text
    editor. For complete information on the SMAResourceMonitor.ini
    settings, see the tables in the next section.
7. Use menu path: **File \> Save**.
8. **Close ☒** the text editor.

### SMAResourceMonitor.ini

The SMAResourceMonitor.ini file resides in the <Configuration
Directory\>\\SMAResourceMonitor\\ directory.

:::note
The Configuration Directory location is based on where you installed your programs. For more information, refer to [File Locations](../../file-locations.md) in the **Concepts** online help.
:::

All settings in the configuration file apply to the machine on which the
file resides. The INI file contains the following major sections:
*General* and *Debug Options*.

#### General

The General table contains basic information for SMA Resource Monitor
processing.

+-------------+-------------+-------------+-------------+----------+
| General     | Default     | Description | Dynamic     | Required |
|             |             |             | (Y/N)       |          |
+=============+=============+=============+=============+==========+
| ShortS      | SMA_MSRESOU | Defines the | N           | Y        |
| erviceName= | RCE_MONITOR | hidden      |             |          |
|             |             | internal    |             |          |
|             |             | (e.g.,      |             |          |
|             |             | registry)   |             |          |
|             |             | service     |             |          |
|             |             | name        |             |          |
|             |             | Windows     |             |          |
|             |             | refers to.  |             |          |
+-------------+-------------+-------------+-------------+----------+
| DisplayS    | SMA         | Defines the | N           | Y        |
| erviceName= | Microsoft   | service     |             |          |
|             | Resource    | name        |             |          |
|             | Monitor     | displayed   |             |          |
|             |             | in the      |             |          |
|             |             | Service     |             |          |
|             |             | Control     |             |          |
|             |             | Manager.    |             |          |
+-------------+-------------+-------------+-------------+----------+
| Pa          | \           | -   Defines | N           | Y        |
| thToRuleAnd | ".\\Rules" |     the     |             |          |
| ActionFiles |             |     full    |             |          |
|             |             |     path to |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |   directory |             |          |
|             |             |             |             |          |
|             |             |  containing |             |          |
|             |             |     the     |             |          |
|             |             |     Rules   |             |          |
|             |             |     and     |             |          |
|             |             |     Actions |             |          |
|             |             |     files.  |             |          |
|             |             | -   The     |             |          |
|             |             |     default |             |          |
|             |             |     path is |             |          |
|             |             |     a       |             |          |
|             |             |             |             |          |
|             |             |    relative |             |          |
|             |             |     path    |             |          |
|             |             |     from    |             |          |
|             |             |     your    |             |          |
|             |             |     <Co    |             |          |
|             |             | nfiguration |             |          |
|             |             |             |             |          |
|             |             | Directory\> |             |          |
|             |             |     to a    |             |          |
|             |             |     sub     |             |          |
|             |             |     folder  |             |          |
|             |             |     named   |             |          |
|             |             |             |             |          |
|             |             |  "Rules". |             |          |
|             |             |             |             |          |
|             |             | **Note:**   |             |          |
|             |             | The         |             |          |
|             |             | Co          |             |          |
|             |             | nfiguration |             |          |
|             |             | Directory   |             |          |
|             |             | location    |             |          |
|             |             | was         |             |          |
|             |             | configured  |             |          |
|             |             | during      |             |          |
|             |             | in          |             |          |
|             |             | stallation. |             |          |
|             |             | For more    |             |          |
|             |             | i           |             |          |
|             |             | nformation, |             |          |
|             |             | refer to    |             |          |
|             |             | [File       |             |          | |             |             | Locations]( |             |          |
|             |             | ../../Conce |             |          |
|             |             | pts/File- |             |          |
|             |             | Locations.h |             |          |
|             |             | tm) |             |          |
|             |             |  in   |             |          |
|             |             | the         |             |          |
|             |             | *|             |          |
|             |             |*Concepts**|             |          |
|             |             | online      |             |          |
|             |             | help.       |             |          |
+-------------+-------------+-------------+-------------+----------+
| MSG         | N/A         | Defines the | N           | Y        |
| INDirectory |             | path to the |             |          |
|             |             | <Co        |             |          |
|             |             | nfiguration |             |          |
|             |             | Di          |             |          |
|             |             | rectory\\MS |             |          |
|             |             | LSAM\\MSGIN |             |          |
|             |             | directory   |             |          |
|             |             | for placing |             |          |
|             |             | OpCon       |             |          |
|             |             | Events.     |             |          |
|             |             |             |             |          |
|             |             |             |             |          |
|             |             |             |             |          |
|             |             |**Note:**|             |          |
|             |             | The         |             |          |
|             |             | Co          |             |          |
|             |             | nfiguration |             |          |
|             |             | Directory   |             |          |
|             |             | location    |             |          |
|             |             | was         |             |          |
|             |             | configured  |             |          |
|             |             | during      |             |          |
|             |             | in          |             |          |
|             |             | stallation. |             |          |
|             |             | For more    |             |          |
|             |             | i           |             |          |
|             |             | nformation, |             |          |
|             |             | refer to    |             |          |
|             |             | [File       |             |          | |             |             | Locations]( |             |          |
|             |             | ../../Conce |             |          |
|             |             | pts/File- |             |          |
|             |             | Locations.h |             |          |
|             |             | tm) |             |          |
|             |             |  in   |             |          |
|             |             | the         |             |          |
|             |             | *           |             |          |
|             |             | *Concepts** |             |          |
|             |             | online      |             |          |
|             |             | help.       |             |          |
+-------------+-------------+-------------+-------------+----------+
| Extern      | <blank\>   | -   Defines | N           | Y        |
| alEventUser |             |     the     |             |          |
|             |             |     OpCon   |             |          |
|             |             |     user    |             |          |
|             |             |     for all |             |          |
|             |             |     events  |             |          |
|             |             |     sent by |             |          |
|             |             |     the SMA |             |          |
|             |             |             |             |          |
|             |             |    Resource |             |          |
|             |             |             |             |          |
|             |             |    Monitor. |             |          |
|             |             | -   You may |             |          |
|             |             |     specify |             |          |
|             |             |     a       |             |          |
|             |             |     clear-  |             |          |
|             |             |     text    |             |          |
|             |             |             |             |          |
|             |             |    password |             |          |
|             |             |     and if  |             |          |
|             |             |     the     |             |          |
|             |             |     SMAReso |             |          |
|             |             | urceMonitor |             |          |
|             |             |     service |             |          |
|             |             |     reads   |             |          |
|             |             |     the INI |             |          |
|             |             |     file    |             |          |
|             |             |     and     |             |          |
|             |             |     finds   |             |          |
|             |             |     an      |             |          |
|             |             |             |             |          |
|             |             | unencrypted |             |          |
|             |             |             |             |          |
|             |             |   password, |             |          |
|             |             |     it will |             |          |
|             |             |     encrypt |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |    password |             |          |
|             |             |     and     |             |          |
|             |             |     update  |             |          |
|             |             |     the ini |             |          |
|             |             |     file.   |             |          |
|             |             | -   To      |             |          |
|             |             |             |             |          |
|             |             |    manually |             |          |
|             |             |     encrypt |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |   password, |             |          |
|             |             |     use the |             |          |
|             |             |             |             |          |
|             |             |    Password |             |          |
|             |             |             |             |          |
|             |             |  encryption |             |          |
|             |             |     tool in |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |  Enterprise |             |          |
|             |             |             |             |          |
|             |             |    Manager. |             |          |
|             |             |     Then,   |             |          |
|             |             |     copy    |             |          |
|             |             |     and     |             |          |
|             |             |     paste   |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |   encrypted |             |          |
|             |             |             |             |          |
|             |             |    password |             |          |
|             |             |     for the |             |          |
|             |             |     value   |             |          |
|             |             |     of this |             |          |
|             |             |             |             |          |
|             |             |    setting. |             |          |
|             |             |     For     |             |          |
|             |             |     more    |             |          |
|             |             |     i       |             |          |
|             |             | nformation, |             |          |
|             |             |     refer   |             |          |
|             |             |     to      |             |          |
|             |             |             |             |          |
|             |             | [Encrypting |             |          | |             |             |             |             |          |
|             |             |  Passwords] |             |          |
|             |             | (../../Files/UI/E |             |          |
|             |             | nterprise%2 |             |          |
|             |             | 0Manager/En |             |          |
|             |             | crypting- |             |          |
|             |             | Passwords.h |             |          |
|             |             | tm) |             |          |
|             |             |       |             |          |
|             |             |     in the  |             |          |
|             |             |     *|             |          |
|             |             |*Enterprise |             |          |
|             |             |             |             |          |
|             |             |   Manager**|             |          |
|             |             |     online  |             |          |
|             |             |     help.   |             |          |
|             |             | -   Maximum |             |          |
|             |             |             |             |          |
|             |             |  characters |             |          |
|             |             |             |             |          |
|             |             |    allowed: |             |          |
|             |             |     15      |             |          |
+-------------+-------------+-------------+-------------+----------+
| ExternalEv  | <blank\>   | -   Defines | N           | Y        |
| entPassword |             |     the     |             |          |
|             |             |     OpCon   |             |          |
|             |             |             |             |          |
|             |             |    External |             |          |
|             |             |     Event   |             |          |
|             |             |             |             |          |
|             |             |    Password |             |          |
|             |             |     for the |             |          |
|             |             |     OpCon   |             |          |
|             |             |     User.   |             |          |
|             |             |     This    |             |          |
|             |             |             |             |          |
|             |             |    password |             |          |
|             |             |     is used |             |          |
|             |             |     for all |             |          |
|             |             |     events  |             |          |
|             |             |     sent by |             |          |
|             |             |     the SMA |             |          |
|             |             |             |             |          |
|             |             |    Resource |             |          |
|             |             |             |             |          |
|             |             |    Monitor. |             |          |
|             |             | -   You may |             |          |
|             |             |     specify |             |          |
|             |             |     a       |             |          |
|             |             |     clear-  |             |          |
|             |             |     text    |             |          |
|             |             |             |             |          |
|             |             |    password |             |          |
|             |             |     and if  |             |          |
|             |             |     the     |             |          |
|             |             |     SMAReso |             |          |
|             |             | urceMonitor |             |          |
|             |             |     service |             |          |
|             |             |     reads   |             |          |
|             |             |     the INI |             |          |
|             |             |     file    |             |          |
|             |             |     and     |             |          |
|             |             |     finds   |             |          |
|             |             |     an      |             |          |
|             |             |             |             |          |
|             |             | unencrypted |             |          |
|             |             |             |             |          |
|             |             |   password, |             |          |
|             |             |     it will |             |          |
|             |             |     encrypt |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |    password |             |          |
|             |             |     and     |             |          |
|             |             |     update  |             |          |
|             |             |     the ini |             |          |
|             |             |     file.   |             |          |
|             |             | -   To      |             |          |
|             |             |             |             |          |
|             |             |    manually |             |          |
|             |             |     encrypt |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |   password, |             |          |
|             |             |     use the |             |          |
|             |             |             |             |          |
|             |             |    Password |             |          |
|             |             |             |             |          |
|             |             |  encryption |             |          |
|             |             |     tool in |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |  Enterprise |             |          |
|             |             |             |             |          |
|             |             |    Manager. |             |          |
|             |             |     Then,   |             |          |
|             |             |     copy    |             |          |
|             |             |     and     |             |          |
|             |             |     paste   |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             |   encrypted |             |          |
|             |             |             |             |          |
|             |             |    password |             |          |
|             |             |     for the |             |          |
|             |             |     value   |             |          |
|             |             |     of this |             |          |
|             |             |             |             |          |
|             |             |    setting. |             |          |
|             |             |     For     |             |          |
|             |             |     more    |             |          |
|             |             |     i       |             |          |
|             |             | nformation, |             |          |
|             |             |     refer   |             |          |
|             |             |     to      |             |          |
|             |             |             |             |          |
|             |             | [Encrypting |             |          | |             |             |             |             |          |
|             |             |  Passwords] |             |          |
|             |             | (../../Files/UI/E |             |          |
|             |             | nterprise%2 |             |          |
|             |             | 0Manager/En |             |          |
|             |             | crypting- |             |          |
|             |             | Passwords.h |             |          |
|             |             | tm) |             |          |
|             |             |       |             |          |
|             |             |     in the  |             |          |
|             |             |     *       |             |          |
|             |             | *Enterprise |             |          |
|             |             |             |             |          |
|             |             |   Manager** |             |          |
|             |             |     online  |             |          |
|             |             |     help.   |             |          |
|             |             | -   Maximum |             |          |
|             |             |             |             |          |
|             |             |  characters |             |          |
|             |             |             |             |          |
|             |             |    allowed: |             |          |
|             |             |     20      |             |          |
+-------------+-------------+-------------+-------------+----------+
| Samp        | 5           | -   Defines | N           | Y        |
| leFrequency |             |     (in     |             |          |
|             |             |             |             |          |
|             |             |    seconds) |             |          |
|             |             |     how     |             |          |
|             |             |     often   |             |          |
|             |             |     samples |             |          |
|             |             |     are     |             |          |
|             |             |     taken   |             |          |
|             |             |     for     |             |          |
|             |             |     Counter |             |          |
|             |             |             |             |          |
|             |             |    Monitors |             |          |
|             |             |     in      |             |          |
|             |             |     order   |             |          |
|             |             |     to      |             |          |
|             |             |             |             |          |
|             |             |   establish |             |          |
|             |             |     an      |             |          |
|             |             |             |             |          |
|             |             |    average. |             |          |
|             |             | -   Minimum |             |          |
|             |             |     Value:  |             |          |
|             |             |     -1      |             |          |
|             |             | -   Maximum |             |          |
|             |             |             |             |          |
|             |             |    Value: - |             |          |
|             |             |     300     |             |          |
+-------------+-------------+-------------+-------------+----------+
| Networ      | 30          | Defines the | N           | Y        |
| kRetryTimer |             | number of   |             |          |
|             |             | seconds to  |             |          |
|             |             | wait before |             |          |
|             |             | retrying a  |             |          |
|             |             | network     |             |          |
|             |             | connection  |             |          |
|             |             | that is     |             |          |
|             |             | down (this  |             |          |
|             |             | is a        |             |          |
|             |             | connection  |             |          |
|             |             | on which    |             |          |
|             |             | the SMA     |             |          |
|             |             | Resource    |             |          |
|             |             | Monitor is  |             |          |
|             |             | monitoring  |             |          |
|             |             | a file.)    |             |          |
+-------------+-------------+-------------+-------------+----------+
| Initializ   | Blank       | -   The     | N           | N        |
| ationScript |             |     full    |             |          |
|             |             |     path to |             |          |
|             |             |     the     |             |          |
|             |             |     ini     |             |          |
|             |             | tialization |             |          |
|             |             |     script. |             |          |
|             |             | -   The     |             |          |
|             |             |     ini     |             |          |
|             |             | tialization |             |          |
|             |             |     script  |             |          |
|             |             |             |             |          |
|             |             |    executes |             |          |
|             |             |     when    |             |          |
|             |             |     the     |             |          |
|             |             |     SMAReso |             |          |
|             |             | urceMonitor |             |          |
|             |             |     service |             |          |
|             |             |     starts. |             |          |
|             |             | -   [SMA    |             |          | |             |             |     T       |             |          |
|             |             | echnologies |             |          |
|             |             | ]{.GeneralC |             |          |
|             |             | ompanyName} |             |          |
|             |             |             |             |          |
|             |             |  recommends |             |          |
|             |             |     using   |             |          |
|             |             |     this    |             |          |
|             |             |     script  |             |          |
|             |             |     to map  |             |          |
|             |             |     network |             |          |
|             |             |     drives  |             |          |
|             |             |     or to   |             |          |
|             |             |     perform |             |          |
|             |             |     any     |             |          |
|             |             |     other   |             |          |
|             |             |             |             |          |
|             |             |    required |             |          |
|             |             |     ini     |             |          |
|             |             | tialization |             |          |
|             |             |             |             |          |
|             |             |  procedure. |             |          |
|             |             | -   Enclose |             |          |
|             |             |     the     |             |          |
|             |             |     path in |             |          |
|             |             |     double  |             |          |
|             |             |     quotes  |             |          |
|             |             |     ("\    |             |          |
|             |             | <path\>"). |             |          |
+-------------+-------------+-------------+-------------+----------+
| Termin      | Blank       | -   The     | N           | N        |
| ationScript |             |     full    |             |          |
|             |             |     path to |             |          |
|             |             |     the     |             |          |
|             |             |             |             |          |
|             |             | termination |             |          |
|             |             |     script. |             |          |
|             |             | -   The     |             |          |
|             |             |             |             |          |
|             |             | termination |             |          |
|             |             |     script  |             |          |
|             |             |             |             |          |
|             |             |    executes |             |          |
|             |             |     when    |             |          |
|             |             |     the     |             |          |
|             |             |     SMAReso |             |          |
|             |             | urceMonitor |             |          |
|             |             |     service |             |          |
|             |             |     stops.  |             |          |
|             |             | -   [SMA    |             |          | |             |             |     T       |             |          |
|             |             | echnologies |             |          |
|             |             | ]{.GeneralC |             |          |
|             |             | ompanyName} |             |          |
|             |             |             |             |          |
|             |             |  recommends |             |          |
|             |             |     using   |             |          |
|             |             |     this    |             |          |
|             |             |     script  |             |          |
|             |             |     to      |             |          |
|             |             |             |             |          |
|             |             |  disconnect |             |          |
|             |             |     network |             |          |
|             |             |     drives  |             |          |
|             |             |     or to   |             |          |
|             |             |     perform |             |          |
|             |             |     any     |             |          |
|             |             |     other   |             |          |
|             |             |             |             |          |
|             |             |    required |             |          |
|             |             |             |             |          |
|             |             | termination |             |          |
|             |             |             |             |          |
|             |             |  procedure. |             |          |
|             |             | -   Enclose |             |          |
|             |             |     the     |             |          |
|             |             |     path in |             |          |
|             |             |     double  |             |          |
|             |             |     quotes  |             |          |
|             |             |     ("\    |             |          |
|             |             | <path\>"). |             |          |
+-------------+-------------+-------------+-------------+----------+
| We          | Blank       | Defines the | N           | N        |
| bServiceURL |             | web         |             |          |
|             |             | services    |             |          |
|             |             | URL for the |             |          |
|             |             | OpCon Web   |             |          |
|             |             | Services.   |             |          |
|             |             |             |             |          |
|             |             | Example:    |             |          |
|             |             | <http://l>    |             |          |
|             |             | ocalhost:85 |             |          |
+-------------+-------------+-------------+-------------+----------+

#### Debug Options

+---------------+---------+---------------+---------------+----------+
| Debug Options | Default | Description   | Dynamic (Y/N) | Required |
+===============+=========+===============+===============+==========+
| Arch          | 10      | -             | Y             | N        |
| iveDaysToKeep |         |    Determines |               |          |
|               |         |     the       |               |          |
|               |         |     number of |               |          |
|               |         |     days of   |               |          |
|               |         |     history   |               |          |
|               |         |     (i.e.,    |               |          |
|               |         |     archive   |               |          |
|               |         |     folders)  |               |          |
|               |         |     to keep.  |               |          |
|               |         | -   Each Time |               |          |
|               |         |     it        |               |          |
|               |         |     archives  |               |          |
|               |         |     a log,    |               |          |
|               |         |     the SMA   |               |          |
|               |         |     Resource  |               |          |
|               |         |     Monitor   |               |          |
|               |         |     checks    |               |          |
|               |         |     for       |               |          |
|               |         |     expired   |               |          |
|               |         |     archive   |               |          |
|               |         |     folders   |               |          |
|               |         |     to        |               |          |
|               |         |     delete.   |               |          |
+---------------+---------+---------------+---------------+----------+
| Maxim         | 15000   | -   Defines   | Y             | N        |
| umLogFileSize |         |     the       |               |          |
|               |         |     maximum   |               |          |
|               |         |     size in   |               |          |
|               |         |     bytes for |               |          |
|               |         |     each log  |               |          |
|               |         |     file.     |               |          |
|               |         | -             |               |          |
|               |         |    Determines |               |          |
|               |         |     when the  |               |          |
|               |         |     current   |               |          |
|               |         |     log file  |               |          |
|               |         |     is closed |               |          |
|               |         |     and a new |               |          |
|               |         |     file is   |               |          |
|               |         |     started.  |               |          |
|               |         |     When the  |               |          |
|               |         |     file      |               |          |
|               |         |     reaches   |               |          |
|               |         |     this      |               |          |
|               |         |     maximum   |               |          |
|               |         |     size, it  |               |          |
|               |         |     is        |               |          |
|               |         |     "rolled  |               |          |
|               |         |     over".   |               |          |
|               |         | -   This      |               |          |
|               |         |     setting   |               |          |
|               |         |     creates   |               |          |
|               |         |     small     |               |          |
|               |         |               |               |          |
|               |         |    manageable |               |          |
|               |         |     log       |               |          |
|               |         |     files.    |               |          |
|               |         | -   SMAResour |               |          |
|               |         | ceMonitor.log |               |          |
|               |         |     resides   |               |          |
|               |         |     in the    |               |          |
|               |         |     <Output  |               |          |
|               |         |               |               |          |
|               |         |    Directory\ |               |          |
|               |         | >\\SMAResourc |               |          |
|               |         | eMonitor\\Log |               |          |
|               |         |               |               |          |
|               |         |    directory. |               |          |
|               |         | -   Once per  |               |          |
|               |         |     day the   |               |          |
|               |         |     SMA       |               |          |
|               |         |     Resource  |               |          |
|               |         |     Monitor   |               |          |
|               |         |     deletes   |               |          |
|               |         |     old       |               |          |
|               |         |     archive   |               |          |
|               |         |     folders.  |               |          |
+---------------+---------+---------------+---------------+----------+
| TraceLevel    | 0       | -             | Y             | N        |
|               |         |    Determines |               |          |
|               |         |     the       |               |          |
|               |         |     detail of |               |          |
|               |         |     debug     |               |          |
|               |         |     trace     |               |          |
|               |         |     logs.     |               |          |
|               |         | -   Valid     |               |          |
|               |         |     Values:   |               |          |
|               |         |     -   0 =   |               |          |
|               |         |         None  |               |          |
|               |         |     -   1 =   |               |          |
|               |         |         Basic |               |          |
|               |         |               |               |          |
|               |         | (non-detailed |               |          |
|               |         |               |               |          |
|               |         |        trace) |               |          |
|               |         |     -   2 =   |               |          |
|               |         |               |               |          |
|               |         |      Detailed |               |          |
|               |         |     -   3 =   |               |          |
|               |         |         Very  |               |          |
|               |         |               |               |          |
|               |         |      Detailed |               |          |
|               |         |               |               |          |
|               |         |       (Traces |               |          |
|               |         |         all   |               |          |
|               |         |         the   |               |          |
|               |         |               |               |          |
|               |         |      possible |               |          |
|               |         |         debug |               |          |
|               |         |               |               |          |
|               |         |   information |               |          |
|               |         |         in    |               |          |
|               |         |         the   |               |          |
|               |         |               |               |          |
|               |         | application.) |               |          |
+---------------+---------+---------------+---------------+----------+
:::
