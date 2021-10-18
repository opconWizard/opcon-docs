---
lang: en-us
title: Data Transformation Services (DTS)
viewport: width=device-width, initial-scale=1.0
---

# Data Transformation Services (DTS)

[]{#aanchor604} Microsoft Data Transformation Services (DTS) transforms data from one database to another. [SMA
Technologies]{.GeneralCompanyName} has found some situations requiring
this procedure; however, there may be several other applicable
situations. DTS resolves the following issues:

- Databases that have been upgraded from MSSQL 7.0 to MSSQL 2000 (or
    higher) have an issue with a command in MSSQL 7.0 (and higher)
    called "TOP".
- Databases that are being moved from a Binary sort order to a
    non-Binary sort order may have collation conflicts (SQL error 446)
    during processing.

## Transforming a Database

To transform the database, address the following issues:

- Disconnect Applications
- Back Up the Database
- Run the Schema Installation Script

### Disconnecting Applications

Perform the DTS procedure on the machine where the OpCon database
resides. Before beginning the DTS procedure, disconnect all applications
from the OpCon database.

[Disconnection Applications from the OpCon Database]{.ul}

1. Log in as a *Windows user with Local Administrative Rights*.
2. Use menu path: **Start \> Control Panel**.
3. Double-click the **Administrative Tools** icon.
4. Double-click the **Server Manager** icon.
5. Expand (+) the **Configuration** option.
6. Double-click the **Services** icon.
7. Scroll down to the **SMA Service Manager** service.
8. Select **Stop** (■) on the toolbar.
9. Click **OK** to exit.
10. Exit all OpCon graphical interfaces.
11. Close any **SQL Server Management Studio** windows connected to the
    OpCon database.

### Backing up the Database

[Locate the Server in Management Studio]{.ul}
On the OpCon Database Server:

Use menu path: **Start \> All Programs \> SQL Server Management
Studio**.

On the Connect to Server screen:

Select **Database Engine** in the **Server type** drop-down list.

Select the desired \[OpCon Database Server\] in the **Server name** drop-down list.

Select one of the following options in the **Authentication**drop-down
list:

- **Windows Authentication** to log in with the current Windows User
    with local administrative authority **- or -**
- **SQL Server Authentication** then enter *sa* in the **Login** text
    box and the *sa's password* in the **Password** text box.

Click the **Connect** button.

In the Microsoft SQL Server Management Studio window:

Expand (+) the **Databases** folder.

Identify the OpCon database.

[Back Up the Database]{.ul}

1. Right-click the **OpCon database** and choose **Tasks \> Back Up**.
2. Go to the **Source** frame.
3. Confirm the **OpCon database** is the database selection.
4. Select **Full** in the **Backup type** drop-down list for a complete
    backup.
5. Go to the **Backup set** frame.
6. Enter the *backup job name* in the **Name** text box.
7. Go to the **Destination** frame.
8. Click the **Disk** radio button.
9. Click **Add** to add the location and name of the backup file if the
    default destination is not desired. You should see the default
    directory for SQL backups listed in the **Select Backup
    Destination** window.
10. Enter, in the **File name** text box, a *file name* followed by a
    *.bak* file extension at the end of the file path. If this is not
    the desired location, enter the *full path* and *file name* followed
    by a *.bak* file extension (e.g., D:\\MSSQL\\Backup\\Opconxps.bak).
11. Click **OK** to accept the backup (.bak) filename.
12. Click the **Options** tab in the **Select a page** menu.
13. Go to the **Overwrite media** frame.
14. Select the **Append to the existing backup set** or **Overwrite all
    existing backup sets** radio button. Either option is acceptable.
    The database administrator should make this decision.
15. Click **OK**.
16. When the backup completes successfully, click **OK**.

### Transferring a Database

[]{#Create_a_Transfer_Database}[Create a Transfer Database]{.ul}
The DTS procedure requires the creation of a new database.

1. Right-click the **Databases** folder under the OpCon Database Server
    Name.
2. Select **New Database**.
3. Enter a *new database name* (e.g., DTSOPCONXPS) in the **Database
    name** text box.
4. If setting the collation to support special characters, [SMA     Technologies]{.GeneralCompanyName} recommends choosing
    **SQL_Latin1_General \_CP1_CS_AS** from the **Collation name**
    drop-down list.
5. Click **OK**.

[Transfer the OpCon Data]{.ul}
In the Microsoft SQL Server Management Studio window:

Expand the **Databases** folder.

Right-click the **database** (e.g., DTSOPCONXPS) created in the [Create a Transfer Database](#Create_a_Transfer_Database)
procedure and choose **Tasks \> Import Data**.

In the SQL Server Import and Export Wizard window:

Click **Next**.

In the Choose a Data Source screen:

Select the desired \[OpCon Database Server\] in the **Server name** drop-down list.

In the Authentication frame:

Select one of the following radio button options for authentication:

- **Use Windows Authentication** to log in with the current Windows
    User with local administrative authority.
- **Use SQL Server Authentication** and enter *sa* in the **Login**
    text box and the *sa's password* in the **Password** text box.

Select the **original OpCon database** in the **Database** drop-down
list and click **Next**.

In the Choose a Destination screen:

Select the desired \[OpCon Database Server\] in the **Server name** drop-down list.

In the Authentication frame:

Select one of the following radio button options for authentication:

- **Use Windows Authentication** to log in with the current Windows
    User with local administrative authority.
- **Use SQL Server Authentication** and enter *sa* in the **Login**
    text box and the *sa's password* in the **Password** text box.

Click **Next**.

In the Specify Table Copy or Query screen:

Select the **Copy data from one or more tables or views** radio button
and click **Next**.

In the Select Source Tables and Views screen:

Select the **Source** checkbox and click **Next**.

In the Save and Execute Package screen:

Select the **Execute immediately** checkbox and click **Next**.

Verify the information and click **Finish**.

Wait until it completes successfully then click **Close** when it
completes.

Back Up the Transfer Database

1. Right-click the **Transfer Database** database and choose **Tasks \>
    Back Up**.
2. Confirm the **Transfer Database** is the database selection.
3. Enter the *backup job name* in the **Name** combo box.
4. Select **Full** in the **Backup type** drop-down list for a complete
    backup.
5. Go to the **Destination** frame.
6. Select the **Disk** radio button.
7. Click **Add** to add the location and name of the backup file if the
    default destination is not desired. You should see the default
    directory for SQL backups listed in the **Select Backup
    Destination** window.
8. Enter, in the **File name** text box, a *file name* followed by a
    *.bak* file extension at the end of the file path. If this is not
    the desired location, enter the full path and file name followed by
    a *.bak* file extension (e.g., D:\\MSSQL\\Backup\\DTSOpconxps.bak).
9. Click **OK** to accept the backup (.bak) filename.
10. Click the **Options** tab in the **Select a page** menu.
11. On the Options tab's screen:
12. Go the **Overwrite media** frame.
13. Select the **Append to the existing backup set** or **Overwrite all
    existing backup sets** radio button. Either option is acceptable.
    The database administrator should make this decision.
14. Click **OK**.
15. When the backup completes successfully, click **OK**.

[Delete the Original Database]{.ul}

1. Go to the right-hand frame.
2. Right-click the **original OpCon database** and select **Delete**.
3. Click **OK** to confirm the deletion.

Restore the Transfer Database as the OpCon Database

1. Go to the **Object Explorer** frame.
2. Right-click the **Databases** folder and select **Restore
    Database**.
3. Type the *name of the original OpCon database* in the **To
    database** combo box.
4. Go to the **Source for restore** frame.
5. Select the **From device** radio button.
6. Click the **ellipsis (...)** button to browse (beside the **From
    device** radio button).
7. Select the **Transfer Database Backup (.bak)** file in the **Backup
    location** box.
8. If the **Transfer Database Backup (.bak)** file is not found in the
    box, then click **Add**.
9. Browse through the folders and select the **Transfer Database Backup
    (.bak)** file.
10. Click **OK**.
11. Click **OK**.
12. Go to the **Select the backup sets to restore** frame.
13. Select the desired **backup (.bak) file** checkbox.
14. Click the **Options** tab in the **Select a page** menu.
15. Select the **Overwrite the existing database** checkbox.
16. Go to the **Restore the database files as** frame.
17. Rename the data and log file names to match the original OpCon
    database name.
18. Go to the **Recovery state** frame.
19. Select the radio button by **Leave the database ready to use by
    rolling back uncommitted transactions. Additional transaction logs
    cannot be restored. (RESTORE WITH RECOVERY)**.
20. Click **OK**.
21. When the restore completes successfully, click **OK**.

[Delete the DTS Database]{.ul}

1. Go to the right-hand frame.
2. Right-click the **transferred OpCon database** (e.g., DTSOPCONXPS)
    created in the [Create a Transfer     Database](#Create_a_Transfer_Database) procedure and
    select **Delete**.
3. Click **OK** to confirm the deletion.

### Running the Schema Installation Scripts

Now that the data has been transferred, run the database update scripts
through the SMA Database Configuration.

[Upgrade the OpCon Database]{.ul}
The DB_Update.cmd and DB_Update_WinAuth.cmd files execute the scripts to
update the database schema, data, and stored procedures for OpCon (refer
below). In the case of errors, the command file produces several output
files in the \<Output Directory\>\\SAM\\Log\\ directory to aid in
support. Each log file is named for its respective SQL script.

  ----------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ![White pencil/paper icon on gray circular background](../../Resources/Images/note-icon(48x48).png "Note icon")   **NOTE:** [The Output Directory was configured during installation. For more information, refer to [File Locations](../../file-locations.md) in the **Concepts** online help.]
  ----------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The following scripts are located in the \<Configuration
Directory\>\\Utilities\\Database\\ directory:

- Schema Installation Script
- SMALOOKUP Script
- Database Stored Procedures Script
- Database Functions Script
- PDSA Framework Scrip
- PDSA Framework Data Script

  ----------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ![White pencil/paper icon on gray circular background](../../Resources/Images/note-icon(48x48).png "Note icon")   **NOTE:** [The Configuration Directory location is based on where you installed your programs. For more information, refer to [File Locations](../../file-locations.md) in the **Concepts** online help.]
  ----------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

For additional information on the SQL scripts, refer to [OpCon Database Scripts](../Installation/OpCon-Database-Scripts.md)
in the **OpCon Installation** online help.

#### Determine Command Line Parameters

After customizing the scripting variables command files, determine the
command line parameters required for executing the DB_Update.cmd or
DB_Update_WinAuth.cmd file.

If using [SQL Authentication]{.ul}, use the DB_Setup.cmd with the following syntax:

DB_Update.cmd PathToOpconDataDir userName userPassword

If using [Windows Authentication to SQL]{.ul}, use the DB_Setup_WinAuth.cmd file with the following syntax:

DB_Update_WinAuth.cmd PathToOpconDataDir

The following list describes the parameters for the commands:

- **PathToOpconDataDir:** The directory path of the \<Configuration
    Directory\>**\\Utilities\\Database\\** directory. Exclude the
    trailing backslash (\\) and always enclose this parameter in double
    quotes (e.g., "C:\\ProgramData\\OpConxps\\Utilities\\Database").
- **userName**: For the DB_Update.cmd file only, this is the user name
    with privileges to update the OpCon database.
- **saPassword**: For the DB_Update.cmd file only, this is the
    password for the userName defined in the previous parameter.

#### Execute the Command Script

  ----------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ![White pencil/paper icon on gray circular background](../../Resources/Images/note-icon(48x48).png "Note icon")   **NOTE:** [To successfully execute the DB_Update_WinAuth.cmd file, the administrator must be logged in to the SAM application server as an Active Directory User with privileges to the "sysadmin" server role on the SQL Server.]
  ----------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Use menu path: **Start \> Run**.
2. Enter *cmd* in the **Open** text box.
3. Click **OK**.
4. Change directories to the \<Configuration
    Directory\>**\\Utilities\\Database\\** directory by entering: cd
    OpCon/xpsDatabaseScriptDir.
5. Enter *DB_Update.cmd* or *DB_Update_WinAuth.cmd* and the
    *parameters*.
6. Read the logs for each of the SQL scripts to verify success.

### Restarting Applications

After updating the database schema, restart the SMA Service Manager and
allow users to connect to the database. All OpCon processing should
continue normally.

[Start the SMA Service Manager]{.ul}

1. Use menu path: **Start \> Control Panel**.
2. Double-click **Administrative Tools**.
3. Double-click the **Services** icon.
4. Click **SMA Service Manager**.
5. Click **Start** on the toolbar to start the service.
6. Click **Close ☒** on the **Services** window.
:::
