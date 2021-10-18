# Graphical Utilities

## Graphical Utilities Introduction

OpCon includes the following graphical utilities:

- [Legacy Audit Management](Legacy-Audit-Management.md)
- [Schedule Import/Export](Schedule-Import_Export.md)
- [SMA OpCon Configuration Utility](SMA-OpCon-Configuration-Utility.md)

All of these utilities, except SMA Data Collector, require a system data
source name (DSN) to connect to the OpCon database. If a system DSN does
not exist, refer to [Create System DSNs](../../installation/configuration.md#Create_System_DSNs)
 in the **OpCon Installation** online help for procedures on
configuring the SQL and Access DSNs.

:::note
Verify that the most recent Open Database Connectivity (ODBC) driver for Microsoft SQL Server is installed before creating the system Data Source Name (DSN).
:::

[Setting Compatibility on Windows Vista]{.ul}
If any of these utilities were installed on a Vista machine, complete
this procedure to set compatibility.

1. Log in as a *Windows user with Local Administrative Rights*.
2. Right-click on **Start** and select **Explore**.
3. Browse to the **\<Target Directory\>\\OpConxps\\Utilities\\**
    directory.
4. Right-click on the **executable for the utility** (e.g.,
    History.exe) and select **Properties** from the menu.
5. Click the **Compatibility** tab.
6. Select the **Run this program in compatibility mode for** checkbox.
7. Select **Windows XP (Service Pack 2)** in the drop-down list and
    click **OK**.
