# OpCon Server Configuration

This chapter contains the information you will need to configure the OpCon Server after new installation. After an upgrade,
please review these items to ensure the server is still configured
correctly.

## Implement Temporary License

For a new installation, the temporary license will allow you run OpCon
immediately while you wait for your permanent license. Later in this
chapter, you will find the procedure to request a permanent license
file.

[Copy in Temporary License]{.ul}

1. Copy the **0.lic** file from the root of the distribution media.
2. Paste the file to the \<Configuration Directory\>**\\SAM\\** folder.

## Configure Database Scripts

As part of the database scripts installation, the database environment
and installation scripting variables are updated. To update the database
maintenance, mirroring, and replication scripts, however, you will need
to use the SMA OpCon Configuration Utility.

[Update Scripting Variables]{.ul}

1. Use menu path: **Start \> All Programs \> OpConxps \> Utilities \>
    SMA OpCon Configuration Utility**.
2. Ensure that the **Database Scripts** option \[left side of utility\]     is selected.
3. Click the **Maintenance** tab to configure Database Maintenance
    information. If the database is on the same machine as the SAM, you
    can browse to the folders.
4. Select the **Maintenance Variables Verified** checkbox and click
    **Update Scripts**.
5. Click the **New** button in the **Profiles** section at the button
    of the screen.
6. Enter a name for the profile and click **Save**. This will store all
    your Database Script settings for future use by this program.

## Configure Database Connections

OpCon uses a single database to manage all data for the system. You must
configure all the components to connect to that database.

### Server and User Interface Connections

You will need to make sure the Enterprise Manager is configured to
communicate with the OpCon database.

:::note
The OpCon Server component's database connection should have been automatically configured during the SMA OpCon SAM installation. For more information, refer to the [SMA Connection Configuration Tool](../server-programs/schedule-activity-monitor.md#SMA) in the **Server Programs** online help.
:::

[Configure the Database Connection Information for the OpCon Server]{.ul}

Use menu path: **Start \> All Programs \> OpConxps \> Utilities\> SMA
Connection Config**.

In the SMA Connection Configuration window:

In the **Server\\Instance Name** field, enter the *Server Name* (include
the instance name if necessary using the Server\\Instance Name syntax).

Enter the *database name* in the **Database Name** field.

Configure the authentication method:

Select the **Use Windows Authentication** checkbox **- or -**

:::note
If you want to use Windows Authentication, then you must make sure that the SMA Service Manager runs as a user that has privileges to the OpCon database. For more information, refer to [OpCon Server Configuration](#Add).
:::

Enter the **SQL Authentication** credentials.

i.  Enter *opconsam* in the **Database Login ID** field.
ii. Enter *opconsam's password* in the **Database Password** field.

Configure the database connection by selecting one of the following
**Configuration** drop-down options:

a.  **None**: Specifies no setting. This is the default.
b.  **SQL Always On**: Specifies that SQL Server has been configured to
    use SQL high availability.
c.  **SQL Mirroring**: Specifies that SQL Server has been configured to
    use mirroring.

Click **Connect**.

Click **OK** to confirm the connection.

Click **OK** to close the program.

[[]{#Create_a_Profile_for_the_EM_to_Connect_to_the_Database}Create a Profile for the EM to Connect to the Database]{.ul}

The EM does not use ODBC for connectivity to the database, so a separate
profile must be configured. Set up the EM profile to connect to the same
database as the SAM as per the procedure to [Create System DSNs](#Create_System_DSNs).

Use menu path: **Start \> All Programs \> OpConxps \> Enterprise
Manager**.

On the Welcome screen:

Click **OK**.

On the Database Connection Profile screen:

Enter a *Profile Name* in the **Profile Name** text box.

Choose your authentication method and connect to the database. Choose
option *a* or *b* .

a.  To use SQL Authentication, enter *opconui* in the **Username** field
    and enter *opconui's password* in the **Password** text box.
b.  To use Windows Authentication, select the **Use Windows
    Authentication** checkbox.

Enter the *Server name* or *IP Address* in the **SQL Server text box**.

:::caution
If connecting to a Server with a backslash (\\) in the name, this means the server uses SQL Instance Names. The SQL Server Browser services must be running on that server for the EM to successfully connect to the database.
:::

Select the **database** in the **Database** drop-down list or click the
**Database** button to show the available databases.

:::note
The list of databases will only be made available once each of the previous text boxes have been filled in.
:::

*(Optional)* Type the [Timeout (sec)]{._Override style="font-style: italic;"} (It is set to 30 by default).

*(Optional)* Click on the **Color** button, select the
desired [Profile color]{._Override style="font-style: italic;"}, and click **OK**.

Click **Next** to advance to the next window.

:::note
The next window will indicate whether the database connection has tested successfully.
:::

If the test was not successful:

Click the **Back** button to correct the problem and try again.

If the test was successful:

Click the **Next** button to go on to set up the OpCon Installation
details.

:::note
For the default \[\[SERVER\]\] token in the UNC path to the OpCon directory on the SAM server, the EM will automatically replace that token with the database server IP/Hostname specified in the profile (refer to Step 4a). With this token in place, if you change the database server in the profile you will not need to change the UNC path (as long as the share directory is the same).
:::

On the OpCon installation details screen:

Confirm the path to the OpCon directory on the SAM server.

Click **Finish** to save the profile.

:::note
The OpCon Installation details can be set up in Profiles or Preferences. Refer to [Setting up New Profiles](../Files/UI/Enterprise-Manager/Setting-up-New-Profiles.md) in the **Enterprise Manager** online help.
:::

### Utilities Connections

Set Privileges for Utilities

Before configuring database connections, you will need to configure some
utilities for compatibility with the Windows operating system.

1. Locate the executable for Legacy Audit (LegacyAudit.exe) in the
    following location: **\<Target Directory\>\\OpConxps\\Utilities\\**.
2. Right-click **LegacyAudit.exe**.
3. Select **Properties** from the menu.
4. Click on the **Compatibility** tab.
5. Select the **Run this program as an administrator** checkbox and
    click **OK**.
6. Locate the executable for SMA ODBC Configuration tool
    (SMAODBCConfig.exe) in the following location: **\<Target
    Directory\>\\OpConxps\\DDI\\**.
7. Right-click **SMAODBCConfig.exe**.
8. Select **Properties** from the menu.
9. Click on the **Compatibility** tab.
10. Select the **Run this program as an administrator** checkbox and
    click **OK**.

[]{#Create_System_DSNs}Create System DSNs
All of the utilities require a system data source name (DSN). If the
required system DSNs do not exist, complete the procedures below.

:::note
Verify that the most recent Open Database Connectivity (ODBC) driver for Microsoft SQL Server is installed before creating the system Data Source Name (DSN).
:::

Select a Driver

Use Schedule Import Export to configure the System DSNs for the server.
The utility must Run as Administrator to have the privileges to
configure the DSNs. The SQL DSNs are shared by multiple utilities.

1. Log in as a *Windows user with Local Administrative Rights*.
2. Locate ImpEx.exe in the following location: **\<Target
    Directory\>\\Opconxps\\Utilities\\**.
3. Right-click **ImpEx.exe** and select **Run as administrator** from
    the menu.
4. Click the **ODBC** button.
5. Click the **System DSN** tab.
6. Click **Add**.
7. Select the **SQL Server Native Client** driver in the **Name**
    column and click **Finish**.

Define ODBC Details

In the Create a New Data Source to SQL Server window:

Enter a unique *Data Source name* in the **Name** field. SMA Technologies suggests using the name of the
database.

:::warning
Do not use the same name as the SQL server instance name.
:::

*(Optional)* Enter *Connection to the OpCon scheduling
database* in the **Description** field.

Enter, in the **Server** field, the *Host Name* of the server hosting
the database with which the SAM will be communicating and click
**Next**.

Select the **With SQL Server authentication using a login ID and
password entered by the user** radio button.

Enter *opconui* in the **Login ID** field.

Enter *opconui's password* in the **Password** field then click
**Next**.

:::note
The default opconui password is 0pC0nxp$. The '0's are zeros, and the character after the 'p' is a dollar sign.
:::

Select the **Change the default database to** checkbox.

Select the **OpCon database**.

Accept the remaining default values on the screen and click the **Next**
button.

Accept all default values on the last screen and click the **Finish**
button.

In the ODBC MS SQL Server Setup window:

Click the **Test Data Source** button.

If the test succeeds, exit the ODBC administrator by clicking **OK** on
subsequent screens.

If the test fails, click **Cancel**.

i.  Click the **Back** button until the screen from Step 7 is displayed.
ii. Repeat [Steps 7 -- 17]{.ul} until the test is successful.

In the ODBC Data Source Administrator window:

Click **OK**.

Create a DSN for an Access Database

To set up System DSNs to the Access databases for the Schedule Import
Export utility, follow these steps:

1. Click **Add**.
2. Select **Microsoft Access Driver (\*.mdb)** in the drop-down list
    and click **Finish**.
3. Enter a *data source* name in the **Data Source Name** text box.
4. *(Optional)* In the **Description** text box, enter
    a *description*.
5. Click the **Select** button.
6. Go to the **Directories** frame and browse to the **Utilities**
    directory (e.g., C:\\Program Files (x86)\\OpConxps\\Utilities\\).
7. Click the **IMPEX.mdb** file in the **Database Name** frame and
    click **OK**.
8. Click **OK**.
9. Click **OK**.
10. Select the **new data source**in the list box and click **OK**.

[Configure SMADDI]{.ul}
If you chose to include SMADDI in your OpCon Server installation, refer
to [Configuring the Database Connection](../utilities/SMA-Dynamic-Data-Input/Configuration.md#Configur2)
 in the **Utilities** online help.

[Configure SMA Resource Monitor]{.ul}
If you chose to include SMA Resource Monitor in your OpCon Server
installation, refer to the information about configuration beginning
with the [Modify the SMAResourceMonitor.ini File](./components.md#Modify_the_SMAResourceMonitor.ini_File)
 procedure.

## Configure SQL Permissions

You can configure SQL Permissions for either of the following:

- [SQL Authentication](#SQL)
- [Windows Authentication](#Windows)

### SQL Authentication

To execute SMA Technologies' database maintenance scripts using SQL Authentication, the SQL user who will
execute the commands for those scripts must have the db_owner database
role. The users are defined in the Maintenance Scripting Variables file
through the DB Backup User and DB Restore User variables. By default,
**opconsam** is the DB Backup User, and **sa** is the DB Restore User.
If you use **sa** for either of these users, you can skip this
procedure.

[[]{#Grant_db_owner_Permissions_for_SQL_Users}Grant db_owner Permissions for SQL Users]{.ul}

On the preferred Database Server:

Log in as a *local administrative user*.

Use menu path: **Start \> All Programs \> Microsoft SQL Server \> SQL
Server Management Studio**.

In the Connect to Server window:

Select **Database Engine**in the **Server type** list box.

Select the **OpCon Database Server**in the **Server name** list box.

Choose your authentication type in the **Authentication** section and
provide credentials.

a.  Log in as **sa** if you choose *SQL Server Authentication* **-
    or -**
b.  Make sure the Windows User for Authentication has system
    administration privileges.

Click the **Connect** button.

In the Object Explorer frame:

Expand the **SQL Server** hosting the OpCon database.

Expand the **Security** folder.

Expand the **Logins** folder.

Right-click on the **user** that you are setting as the DB Backup User
and select **Properties**.

In the Select a page panel on the left:

Click **User Mapping**.

In the Users mapped to this login table:

Select the checkbox for the **OpCon Database**.

In the Database role membership for:

Select the checkbox for **db_owner** permissions.

In the Users mapped to this login table:

Select the **master** database if this user will back up the system
databases.

In the Database role membership for:

Select the checkbox for **db_owner** permissions.

In the Users mapped to this login table:

Select the **msdb** databases if this user will back up the system
databases.

In the Database role membership for:

Select the checkbox for **db_owner** permissions and click **OK**.

In the Object Explorer frame under Logins:

Right-click on the **user** that you are setting as the DB Restore User
and select **Properties**.

In the Select a page panel on the left:

Click **User Mapping**.

In the Users mapped to this login table:

Select the checkbox for the **OpCon Database**.

In the Database role membership for:

Select the checkbox for **db_owner** permissions and click **OK**.

### Windows Authentication

Complete the procedures so that the OpCon
user applications can authenticate.

[[]{#Add_the_OpConxps_Active_Directory_Group_to_the_SQL_Server}Add the OpConxps Active Directory Group to the SQL Server]{.ul}

On the SQL Server Machine:

Log on as a *local administrative user*.

Use menu path: **Start \> All Programs \> Microsoft SQL Server \> SQL
Server Management Studio**.

In the Connect to Server window:

Select **Database Engine**in the **Server type** list box.

Select the **OpCon Database Server**in the **Server name** list box.

Choose your authentication type in the **Authentication** section and
provide credentials.

a.  Log in as **sa** if you choose *SQL Server Authentication* **-
    or -**
b.  Make sure the Windows User for Authentication has system
    administration privileges.

Click the **Connect** button.

In the Microsoft SQL Server Management Studio window:

Click the menu bar path: **View \> Object Explorer**.

In the Object Explorer frame:

Expand the **SQL Server** hosting the OpCon database.

Expand the **Security** folder.

Right-click the **Logins** folder and select **New Login** from the
menu.

In the Login - New window:

Click the **Search** button next to the **Login Name** field.

In the Select User or Group window:

Click the **Object Types** button.

In the Object Types window:

Select the **Groups** checkbox and click **OK**.

In the Select User or Group window:

Click the **Locations** button.

In the Locations window:

Expand **Entire Directory**, select the preferred **directory name**,
and click **OK**.

In the Select User or Group window:

Click the **Advanced** button.

Click the **Find Now** button.

Select the **OpCon Group** in the list at the bottom of the window that
was created in the procedure to [Create the OpConxps Active Directory Group](./system-requirements.md#Create_the_OpConxps_Active_Directory_Group)
 and click **OK**.

Click **OK** again.

In the Login - New window:

Select the **OpCon database** in the **Default database** list.

Select the **User Mapping** page in the **Select a page** navigation
pane.

In the Users mapped to this login table:

Select the **OpCon Database** checkbox in the **Map** column.

In the Database role membership for:

Select the checkbox for the **opconxps** role.

Select the **Securables** page in the **Select a page** navigation pane.

Click **Search**.

Select the **The server '*Servername\\Instance*'** radio button and
click **OK**.

:::note
The bottom box will be populated with Explicit permissions for **ServerName\\Instance**.
:::

Scroll to the bottom of the list.

Select the **Grant** checkbox for the **View Server State Permission**.

[[]{#Add_the_SQL_Server_Logins_for_SMA_Service_Manager}Add the SQL Server Logins for SMA Service Manager]{.ul}

If you want to run SMA Service Manager as the local system account (NT
AUTHORITY\\SYSTEM) and you want to use Windows Authentication for the
database connection, then you have to make sure the service has a login
to SQL Server. There are different options when SQL Server is local or
remote.

In the Microsoft SQL Server Management Studio window:

Expand (+) the **Database Engine containing the OpCon Database**.

Expand (+) the **Security** folder.

If the SAM and the database are on a different machine:

:::tip Example
On a domain named "ABCCompany" with a SAM Application Server named "OpConxpsServer", the Login name for the SQL server would be:

ABCCompany\OpConxpsServer$
:::

a.  Right-click **Logins** and select **New Login** from the menu.
b.  Enter the *domain* and *SAM Application Server name* in the **Login
    name** text box, using the following syntax:
    [DomainName\\ServerName$]{style="font-family: 'Courier New';"} c.  Proceed to Step 5.

*- or -*

If the SAM and the database are on the same machine, double-click on
**NT AUTHORITY\\SYSTEM** under the **Logins** folder.

Select the **OpCon Database** in the **Default database** list box.

Select the **User Mapping** page in the **Select a page** navigation
pane.

In the Users mapped to this login table:

Select the **OpCon Database** checkbox in the **Map** column.

In the Database role membership for:

Select the **opconxps** role checkbox.

If you are creating the user:

a.  Click **OK**.
b.  Double-click on the newly-created user under the **Logins** folder.

Select the **Securables** page in the **Select a page** navigation pane.

In the Permissions for \<Server\> Explicit table:

In the **Grant** column, select the **Grant** checkbox for the **View
server state** permission.

Click **OK**.

[[]{#Grant_db_owner_Permissions_for_a_Windows_User}Grant db_owner Permissions for a Windows User]{.ul}

To execute SMA Technologies' database maintenance scripts using Windows Authentication, the Windows user who
will execute the jobs for those scripts must have the db_owner database
role.

1. Expand (+) the **Database Engine containing the OpCon Database**.
2. Expand (+) the **Security** folder.
3. Expand the **Logins** folder.
4. Right click on **Windows Account that will execute the scripts** and
    select **Properties**.
5. Click **User Mappings**.
6. Select the checkbox for the **OpCon Database**.
7. Select the checkbox for **db_owner** permissions.
8. Select the **master** database if this user will back up the system
    databases.
9. Select the checkbox for **db_owner** permissions.
10. Select the **msdb** databases if this user will back up the system
    databases.
11. Select the checkbox for **db_owner** permissions.
12. Click **OK**.

## Configure Optional Services

If you chose to enable any of the optional services when configuring the
OpCon Server, you must configure them for proper operation. If you do
not have optional service enabled, skip down to [Configure OpCon](#Configur5).

[Configure SMA LDAP Monitor]{.ul}
If you chose to enable the LDAP Monitor when configuring the OpCon
Server, you must configure this component to connect to your LDAP
environment. For information on the details of the SMA LDAP Monitor
configuration, refer to [SMA LDAP Monitor Configuration](../server-programs/optional.md#SMA4)
 in the **Server Programs** online help.

1. Right-click the **Start** button and select **Explore** from the
    menu.
2. Browse to the \<Configuration Directory\>**\\SAM** directory.
3. Double-click the **SMALDAPMon.ini** file.
4. Define the **DirectoryType**. Valid values are ADS and OpenLDAP.
5. Add the *Host* and *Port* settings.
6. *(Optional)* Define the *UserNamePrefix* (required
    for automatic sign-on) and *Domain*.
7. Enter the secure information. **UserName**, **Password**, and
    **DefaultUserPassword** must be encrypted in the INI file. To
    encrypt these values, you can either use the Enterprise Manager
    password encryption tool (refer to [Encrypting     Passwords](../Files/UI/Enterprise-Manager/Encrypting-Passwords.md)
     in the **Enterprise Manager** online help) or the built-in
    [\--credentials]{style="font-family: 'Courier New';"} command-line     option with SMA LDAP Monitor using the following example:

If you wish to change the default RefreshInterval behavior of 60
seconds, delete the value and enter the interval (in seconds) that you
would like SMA LDAP Monitor to wait between synchronizations. Values
must be more than 60 seconds.

[Upgrade SMA LDAP Monitor]{.ul}
When upgrading to OpCon version 15.1 or higher, the following INI
settings will need to be removed or replaced:

Under the \[General Settings\]:
For **LDAPPath**, replace this setting with two new settings: **Host**
and **Domain**.

- [Host=\[Domain name or Domain controller DNS name or     IP\]]{style="font-family: 'Courier New';"}
- [Port=\[Port number LDAP is listening     on\]]{style="font-family: 'Courier New';"}

For **LDAPUser** and **LDAPPassword**, replace **LDAPUser** with
**UserName** and replace **LDAPPassword** with **Password**. Re-enter
the values either by copying and pasting from the Enterprise Manager
Encryption screen or by using the \--credentials command-line argument.

For **LDAPOpConGroupName** and **DefaultOpConRole**, replace these two
settings with the following:

\

A new Sync category with:

- [Group=\[Value for     LDAPOpConGroupName\]]{style="font-family: 'Courier New';"}
- [Role=\[Value for     DefaultOpConRole\]]{style="font-family: 'Courier New';"}

For **LDAPGroupUseHash**, this setting can be removed and the program
will correctly read the '\#' character in a Group name.

Add **DefaultUserPassword**. Set the value to the encrypted value for
default password for OpCon users that will be added by SMALDAPMon. Use
EM Encryption screen or the
[\--credentials]{style="font-family: 'Courier New';"} command-line argument to encrypt the value.

Add **DefaultEventPassword**. Set the value to the encrypted value for
default password to submit external events for OpCon users that will be
added by SMALDAPMon. Use EM Encryption screen or the
[\--credentials]{style="font-family: 'Courier New';"} command-line argument to encrypt the value.

1. Remove the **Trace=ON\|OFF** setting.
2. Set **TraceLevel=4**.

The following is an example of upgrading configuration from SMA LDAP
Monitor version 15.0 or below to SMA LDAP Monitor version 15.1 or
higher:

Previous INI File:

\[General Settings\]
LDAPPath=LDAP://dc=domain,dc=org

LDAPUser=ldap

LDAPPassword=password

LDAPOpConGroupName=OpConUsers

LDAPGroupUseHash=True

DefaultOpConRole=OpConAdmins

RefreshInterval=60

\[Debug Options\]
ArchiveDaysToKeep=10

MaximumLogFileSize=150000

Trace=OFF

TraceLevel=0

New INI File:

\[General Settings\]
Host=domain.org

Port=389

UserName=

Password=

RefreshInterval=60

\[Debug Options\]
ArchiveDaysToKeep=10

MaximumLogFileSize=150000

TraceLevel=4

\[Sync1\]
Group=\#OpConUsers

Role=OpConAdmins

Once the steps above have been completed, run the following from the
command line:

SMALDapMon.exe \--credentials \--user=ldap \--password=password
\--defaultpassword=\[your default user password\]

[Configure SMASAPProxy]{.ul}
If you chose to enable the Connector for SAP and/or SAP BW when
configuring the OpCon Server, you must configure the component to
connect to your SAP environments. For information on the details of the
SAPQueryProcessor configuration, refer to
[SAPQueryProcessor.ini](../server-programs/request-router.md#SAPQUERY)
in the **Server Programs** online help.

1. Right-click the **Start** button and select **Explore** from the
    menu.
2. Browse to the \<Configuration Directory\>\\**SAM** directory.
3. Double-click the **SAPQueryProcessor.ini** file.
4. Under the \[TCP/IP Parameters\]:
5. *(Optional)* Set the value for **SocketNumber** for
    connecting to the SAP R/3 environment.
6. *(Optional)* Set the value for **BWSocketNumber**
    for connecting to the SAP BW environment.
7. Use menu path: **File \> Save**.
8. **Close ☒** **Notepad**.

## Configure OpCon

Since the majority of the SAM configuration options are in the database,
the administrator must configure the options through the Enterprise
Manager.

[[]{#Change_the_ocadm_Password_and_Configure_SAM_Options}Change the ocadm Password and Configure SAM Options]{.ul}

Use menu path: **Start \> All Programs \> OpConxps \> Enterprise
Manager**.

On the OpCon Login screen:

Enter *ocadm* in the **Username** text box.

Enter, in the **Password** text box, *12 asterisks*
(\*\*\*\*\*\*\*\*\*\*\*\*) as the default password.

Select, in the **Profile** list box, the **profile** created in the
[Create a Profile for the EM to Connect to the Database](#Create_a_Profile_for_the_EM_to_Connect_to_the_Database)
 procedure.

Click **Login**.

In the OpCon Enterprise Manager window:

Use menu path: **EnterpriseManager \> Password Update \> Change User
Password**.

In the Password Update window:

Enter *12 asterisks* (\*\*\*\*\*\*\*\*\*\*\*\*) in the **Old Password**
text box.

Enter a *new password* in the **New Password** text box.

Reenter the *new password* in the **Confirm Password** text box and
click **OK**.

In the Navigation Panel under Administration:

Double-click **Server Options**.

In the Server Options editor:

Verify that the **General** tab is selected.

Review all parameters for correctness. Review all
[General](../administration/server-options.md#general) settings in the
**Concepts** online help for details.

To modify a parameter's value:

a.  Click on the preferred **parameter** in the parameter table.
b.  Enter a *valid value* in the frame at the bottom of the screen.
c.  Click the **Update** button save the parameter changes, the
    **Cancel** button to disregard the changes, or the **Defaults**
    button to reset the parameter to the system default.
d.  *(Optional)* Select another **parameter category**
    from the tabs across the top of the editor.
e.  Repeat [Steps a - d]{.ul} to modify other parameter(s).

Click on the **SMTP Server Settings** tab.

Review all parameters for correctness, and specifically look at the
following parameters:

a.  Specify the *SMTP Server Name (Primary Email)*.
b.  If the SMTP server requires SSL Encryption, set the value for **SMTP
    Authentication - Enable SSL (Primary Email)** to **True**.
c.  If the **Enable SSL for SMTP Authentication (Primary Email)** value
    is **True** or if the SMTP server requires authentication, then
    specify the *SMTP Authentication User* and *Password (Primary
    Email)*.
d.  If the SMTP server [does not]{.ul} require authentication, specify     the *SMTP Notification Address (Primary Email)*.
e.  If a Secondary SMTP server is available, repeat [Steps a - d]{.ul}
    for the **(Secondary Email)** settings with the same names.
f.  If alternate servers should be used for all Text Messaging, repeat
    [Steps a - d]{.ul} for all **(Primary SMS)** and **(Secondary SMS)**
    settings with the same names.

If an email address is not specified, **noreply\@mycorp.com** is the
default. Modify this address to specify the correct domain for your
environment.

:::note
If the SMTP server requires authentication, the SMTP Notification Address is ignored.
:::

Click the **Automatic License Notifications** tab.

:::note
SMA Technologies [strongly recommends]{.ul} enabling automatic license notifications. If for any reason the license is compromised and this feature is not enabled, only SAM Critical log will report the problem. Notifying SMA Technologies and local OpCon administrators automatically will ensure action can be taken before the license expires.
:::

Review the **[Send Email to SMA Office]{.GeneralSendEmailtoSMAOffice}** parameter.

Leave the value set to **Disabled** if SMA Technologies should not be automatically notified
through email when:

i.  The license is expiring **- or -**
ii. At the beginning of the month, the task count report is due for Task
    Based licensed customers.

To enable automatic notifications, select the **[SMA Office]{.GeneralSMAOffice}** that provides your sales and support from
the list. The SAM will automatically send email notifications to the
selected office when:

i.  The license is expiring **- or -**
ii. At the beginning of the month, the task count report is due for Task
    Based licensed customers.

Review the **Send Email Cc** parameter.

a.  If the value for [Send Email to SMA     Office]{.GeneralSendEmailtoSMAOffice} is Disabled, then leave the
    value for Send Email Cc blank.
b.  If the value for [Send Email to SMA     Office]{.GeneralSendEmailtoSMAOffice} has an SMA
    Technologies office selected, set
    the value for Send Email Cc to one or more email addresses,
    separated by semicolons (;). These email addresses will be copied
    any time an automatic email is sent to the SMA Technologies office.

For **Task-based Licensed** customers, review the **Encrypt Task License
Report** parameter.

a.  Leave the value set to **False** to keep the task license report
    readable in plain text.
b.  Set the value to **True** to encrypt the task license report. Only
    SMA Technologies will be able to decrypt the     report and read the information.

In the top right-hand corner of the Server Options editor:

Click the **Save** ![Save Button](../Resources/Images/Installation/EMsave.png)
button.

**Close ☒** **Server Options**.

[[]{#Create_the_Machine_in_OpCon_for_the_Windows_Agent_on_the_Server}Create the Machine in OpCon for the Windows Agent on the Server]{.ul}

Because the SMA OpCon Agent for Windows was installed on the Server, you
need to create a machine record with a unique Machine name and Socket
number in OpCon so the Server can communicate with the Agent.

1. Double-click on **Machines**.
2. Click the **Add** ![Add Button](../Resources/Images/Installation/EMadd.png)
    button on the **Machines** toolbar.
3. Enter, in the **Name** text box, the *official host name* or *alias*
    based on the OpCon Server machine.
4. Enter, in the **Documentation** text box, any relevant documentation
    for this LSAM machine.
5. Select **Windows**in the **Machine Type** drop-down list.
6. Set the value to a *unique number* (e.g., 3100) in the **Socket
    Number** box.
7. *(Optional)* Enter the *IPv4 or IPv6 address* in the
    **IP Address** field.
8. *(Optional)* Enter the *name*in the **Fully
    Qualified Domain Name** field.
9. Click the **Save**
    ![Save Button](../Resources/Images/Installation/EMsave.png) button on the
    **Machines** toolbar.
10. Click **Open Advanced Settings Panel**.
11. Click the **Communication Settings** tab.
12. Click the **Requires XML Escape Sequences** parameter.
13. Verify the value for this setting is **True**. If the value is
    **False**, select **True** and click **Update**.
14. Click the **Save** button to save and close the Advanced Settings
    Panel.

[Configure Replication or Mirroring]{.ul}
If SQL replication is chosen as a failover method at this site,
configure the OpCon database for replication. Refer to [Manual Setup for Microsoft SQL
Replication](../Files/Database-Information/Manual-Setup-for-Microsoft-SQL-Replication.md)
 or [Setup for Automatic Microsoft SQL Replication](../Files/Database-Information/Setup-for-Automatic-Microsoft-SQL-Replication.md)
 in the **Database Information** online help.

If SQL mirroring is chosen as a failover method at this site, configure
the OpCon database for mirroring. Refer to [Setup for Automatic Microsoft SQL
Mirroring](../Files/Database-Information/Setup-for-Automatic-Microsoft-SQL-Mirroring.md)
 in the **Database Information** online help.

### Import the OpCon Maintenance and Report Jobs

For the optimal performance of OpCon, SMA Technologies requires the scheduling of
maintenance utilities. SMA Technologies provides two different transport databases with job templates for maintenance and
report jobs in OpCon. If you have previously imported these schedules,
skip this section and proceed to [OpCon Server Configuration](#Finish).

- The AdHoc.MDB file contains three jobs for managing OpCon events for
    schedule builds, checks, and deletes. For additional information,
    refer to [SMA_SKD Jobs on the AdHoc Schedule](../objects/schedules#adhoc-schedule)
    in the **Concepts** online help.
- The SMAReports.MDB file contains a job to automate every OpCon
    Report provided by SMA Technologies. For     additional information, refer to [Report Generator
    Schedule](../objects/schedules.md#report-generator-schedule)
     in the **Concepts** online help.

:::warning
Backing up the OpCon database and the transaction log regularly is an extremely important aspect of operating OpCon. If the transaction log is not backed up regularly, the hard drive eventually fills up and OpCon discontinues processing.
:::

[Create DSNs for the Transport Databases]{.ul}
The first time the utility is activated, there is a prompt to select a
DSN for the Microsoft Access database. If this is not the first time the
utility has been activated, log in to the OpCon database and create the
DSN for the AdHoc database.

1. Use menu path: **Start \> All Programs \> OpConxps \> Utilities \>
    Schedule Import Export**.
2. Click the **ODBC** button.
3. Click the **System DSN** tab.
4. Click the **Add** button.
5. Select **Microsoft Access Driver (\*.mdb)** in the drop-down list
    and click **Finish**.
6. Enter a *data source* name (e.g., IMPEX) in the **Data Source Name**
    text box.
7. *(Optional)* Enter a *description* in the
    **Description** text box.
8. Click the **Select** button.
9. Go to the **Directories** frame and browse to the **Utilities**
    directory (e.g., C:\\Program Files x86\\OpConxps\\Utilities\\).
10. Click the **IMPEX.mdb** file in the **Database Name** frame and
    click **OK**.
11. Click **OK**.
12. Click the **Add** button.
13. Select **Microsoft Access Driver (\*.mdb)** in the drop-down list
    and click **Finish**.
14. Enter *AdHoc* in the **Data Source Name** text box.
15. *(Optional)* Enter a *description* in the
    **Description** text box.
16. Click the **Select** button.
17. Go to the **Directories** frame and browse to the **Utilities**
    directory (e.g., C:\\Program Files x86\\OpConxps\\Utilities\\).
18. Click the **AdHoc.mdb** file in the **Database Name** frame and
    click **OK**.
19. Click **OK**.
20. Click the **Add** button.
21. Select **Microsoft Access Driver (\*.mdb)** in the drop-down list
    and click **Finish**.
22. Enter *SMAReports* in the **Data Source Name** text box.
23. *(Optional)* Enter a *description* in the
    **Description** text box.
24. Click the **Select** button.
25. Go to the **Directories** frame and browse to the **Utilities**
    directory (e.g., C:\\Program Files x86\\OpConxps\\Utilities\\).
26. Click the **SMAReports.mdb** file in the **Database Name** frame and
    click **OK**.
27. Click **OK**.
28. Click **OK**.
29. Select the **SMAReports** DSN and click **OK**.

[Import the AdHoc Schedule]{.ul}
If you would like notification when any Schedule Build, Check, or Delete
processes fail, then complete this procedure.

1. Use menu path: **File \> Select Access DSN**.
2. Select the **AdHoc** datasource in the list box and click **OK**.
3. Select the **AdHoc** schedule in the **Transport Database**.
4. Click the **Import from Transport Database** button on the toolbar.
5. Click the **Import** button.
6. Click **OK** on the warning message about Batch User IDs.
7. Click **Yes** to *purge* the jobs or click **No** to *merge* the
    jobs.
8. Click **Yes** to *purge* the dates or click **No** to *merge* the
    dates.
9. Click **OK** on the termination message.

[Import the SMAReports Schedule]{.ul}
If you would like to automate OpCon reports, complete the procedure
provided here.

1. Use menu path: **File \> Select Access DSN**.
2. Select the new **SMAReports** data source in the list box and click
    **OK**.
3. Select the **Report Generator** schedule in the **Transport
    Database**.
4. Click the **Import from Transport Database** button on the toolbar.
5. On the **Machine** tab, click the **localhost** machine in the left
    frame.
6. In the right frame, click the **Machine Name** defined with the
    procedure to [Create the Machine in OpCon for the Windows Agent on     the
    Server](#Create_the_Machine_in_OpCon_for_the_Windows_Agent_on_the_Server)
    .
7. Click the **Import** button.
8. Click **OK** on the warning message about Batch User IDs.
9. Click **OK** on the termination message.

Validate Property Definitions

In the EM Navigation Panel under Administration:

Double-click **Global Properties**.

On the Global Properties screen:

Select **SMADBCredentials** in the **Select Global Property** list box.

In the **Global Property Value** text box, verify the *User Name* and
*Password*.

a.  **-uocadm** is the default user name for logging in. SMA Technologies recommends updating the default
    value to a user other than ocadm.
b.  **-w\*\*\*\*\*\*\*\*\*\*\*\*** is the default password for ocadm.
    Replace the 12 asterisks with the actual password for ocadm. The
    password should have been set in an earlier process. Refer to the
    procedure to [OpCon Server     Configuration](#Change_the_MaintenanceUser_Password).
c.  Click **Save** ![Save Button](../Resources/Images/Installation/EMsave.png) .

Select **SMAOpConDataPath** in the **Select Global Property** list box.

In the **Global Property Value** text box, verify the path to the
\<Configuration Directory\> on the SAM Application server.

a.  If the path on the SAM Application server is different from the
    default (i.e., C:\\ProgramData\\OpConxps\\), modify the value to
    match the correct path.
b.  Click **Save** ![Save Button](../Resources/Images/Installation/EMsave.png).

Select **SMAOpConOutputPath** in the **Select Global Property** list
box.

In the **Global Property Value** text box, verify the path to \<Output
Directory\> on the SAM Application server.

a.  If the path on the SAM Application server is different from the
    default (i.e., C:\\ProgramData\\OpConxps\\), modify the value to
    match the correct path.
b.  Click **Save** ![Save Button](../Resources/Images/Installation/EMsave.png).

Select **SMAOpConPath** in the **Select Global Property** list box.

In the **Global Property Value** text box, verify the path to the
Utilities folder on the SAM Application server.

a.  If the path on the SAM Application server is different from the
    default (i.e., C:\\Program Files\\OpConxps\\), modify the value to
    match the correct path.
b.  Click **Save** ![Save Button](../Resources/Images/Installation/EMsave.png).

Select **SMAAdminEmail** in the **Select Global Property** list box.

In the **Global Property Value** text box:

a.  Enter an *email address* for the OpCon administrator.
b.  If desired, enter *multiple address separated with semicolons* (;).
c.  Click the **Save**
    ![Save Button](../Resources/Images/Installation/EMsave.png) button.

If **UNIX LSAMs** exist in the environment:

a.  Select **UNIXLSAMPath** in the **Select Global Property** list box.
b.  In the **Global Property Value** text box, verify the path to the
    "bin" directory on the UNIX machine.

Select **DB_SERVER_NAME** in the **Select Global Property** list box.

In the **Global Property Value** text box, verify the
OpCon database server name.

a.  If the name of the database server is different from the default,
    modify the value to match the correct database server.
b.  Click **Save**![Save Button](../Resources/Images/Installation/EMsave.png).

Select **SqlMaintUser** in the **Select Global Property** list box.

In the **Global Property Value** text box, verify the SQL maintenance
user name.

a.  If the user name is different from the default, modify the value to
    match the correct user name.
b.  Click **Save**![Save Button](../Resources/Images/Installation/EMsave.png).

Select **SqlMaintPassword** in the **Select Global Property** list box.

In the **Global Property Value** text box, verify the SQL maintenance
password.

a.  If the password is different from the default, modify the value to
    match the correct password.
b.  Click **Save**![Save Button](../Resources/Images/Installation/EMsave.png).

Select **DatabaseName** in the **Select Global Property** list box.

In the **Global Property Value** text box, verify the
OpCon database name.

a.  If the name of the database is different from the default, modify
    the value to match the correct database name.
b.  Click **Save**![Save Button](../Resources/Images/Installation/EMsave.png).

Select **PathToFullBackupFile** in the **Select Global Property** list
box.

In the **Global Property Value** text box, verify the path to the full
backup file.

a.  If the name of the path to the full backup file is different from
    the default (C:\\Program Files\\Microsoft SQL
    Server\\MSSQL14.MSSQLSERVER\\MSSQL\\Backup\\SMADB_Backup.bak),
    modify the value to match the correct path.
b.  Click **Save**![Save Button](../Resources/Images/Installation/EMsave.png).

Select **PathToTranLogBackupFile** in the **Select Global Property**
list box.

In the **Global Property Value** text box, verify the path to the
transaction log backup file.

a.  If the name of the path to the full backup file is different from
    the default (C:\\Program Files\\Microsoft SQL
    Server\\MSSQL14.MSSQLSERVER\\MSSQL\\Backup\\SMATLog_Backup.bak),
    modify the value to match the correct path.
b.  Click **Save**![Save Button](../Resources/Images/Installation/EMsave.png).

[Configure Jobs and Set Up Notification for All Maintenance Jobs]{.ul}
While most of the maintenance jobs will execute without further
configuration, there are several jobs that will need configuration. For
details on each job and the required configuration, refer to [OpCon Data Maintenance](../Files/Database-Information/OpCon-Data-Maintenance.md)
 in the **Database Information** online help. Additionally, there
are no notifications set up by default for the imported jobs other than
the AdHoc jobs. Use either [Event Notification](../notifications/Components.md) in
the **Concepts** online help to configure notifications for groups of
jobs, or go to the [Job Events](../Files/UI/Enterprise-Manager/Job-Events.md) in
the **Enterprise Manager** online help to configure for each job with
the $NOTIFY:\<Action\> events. Refer to additional information about
[Defining Events](../events/defining.md)
 in the **OpCon Events** online help.

:::caution
If notifications are not configured, nobody will be notified when schedule builds or other critical maintenance processes fail.
:::

## Start the Services and Finalize Setup

The SMA Service Manager will only process if you have a good license
file from SMA Technologies. Before completing the next procedures, review the following:

- For an upgrade, your existing license file will continue to work.
- For new installations:
  - If you have been supplied with a temporary license file, save it
        to the SAM folder before completing this procedure.
  - If you do not have a temporary license file, complete the
        procedure to start the service for the first time so that you
        can get the information needed to request a full license file.

[[]{#Configure_the_SMA_Service_Manager_and_Start_the_Service}Configure the SMA Service Manager and Start the Service]{.ul}

Since the SAM and all supporting services are managed by the SMA Service
Manager, the only service requiring start up is the SMA Service Manager.
The configuration of the startup type varies when implementing failover.

1. Use menu path: **Start \> Control Panel**.
2. Double-click the **Administrative Tools** icon.
3. Double-click the **Services** icon.
4. Scroll down to the **SMA OpCon Service Manager** service in the
    **Services** list.
5. Double-click on **SMA OpCon Service Manager**.
6. Change the **Startup type** to **Automatic (Delayed Start)**.
7. Click the **OK** button.
8. Click on **SMA OpCon Service Manager**.
9. Click the **Start** button on the toolbar.
10. View the various log files to verify the SAM-SS has connected
    successfully to the database. Use menu path: **Start \> All
    Programs \> OpConxps \> Log Monitors** to view the Log File names.

[Request a License File]{.ul}
Log in to the **Enterprise Manager**.

Use menu path: **Help \> About OpCon Enterprise Manager**.

Click the **License Information** tab.

Select the **System ID \[e.g., (SMAServer_1234)\]** at the end of the first line.

Right-click and select **Copy**.

Send an email to <license@smatechnologies.com> with the subject line
**License File Request**. Include the following information in the
message:

a.  Environment for the SAM and database (e.g., Production)
b.  The System ID copied from the **License Information** tab (press
    **Ctrl + V** to paste the value from the clipboard)
c.  Your company's name

[Place the License File in the SAM Directory]{.ul}
After SMA Technologies responds to the license request, save the license file to the SAM directory.

:::caution
If the license file is encrypted after being received from SMA Technologies (e.g., saved to a Windows folder set with the "Encrypt contents to secure data" option), SAM will not be able to read the license file.
:::

1. Open your email program to get the license file from SMA Technologies.
2. Open the email message containing the license file.
3. Right-click the **license file** and select **Save As**.
4. Browse to the \<Configuration Directory\>**\\SAM** directory.
5. Click the **Save** button.

[Start the SMA Service Manager after Applying the License File for the First Time]{.ul}

If this was a new installation and you have received a license file for
the first time, you will need to start the SMA Service Manager.

1. Use menu path: **Start \> Control Panel**.
2. Double-click the **Administrative Tools** icon.
3. Double-click the **Services** icon.
4. Scroll down to the **SMA Service Manager** service in the
    **Services** list.
5. Click on **SMA Service Manager**.
6. Click the **Start** button on the toolbar.
7. View the various log files to verify the SAM-SS has connected
    successfully to the database. Use menu path: **Start \> All
    Programs \> OpConxps \> Log Monitors** to view the Log File names.

### Create User Scripts and Custom Programs

SMA Technologies recommends placing user scripts and custom programs in folders provided during installation. Placing
scripts in these folders prevents them from being deleted during an
upgrade.

- Place user scripts in the \<Configuration Directory\>**\\Scripts\\**
    folder.
- Place custom programs in the \<Target Directory\>\\OpConxps\\Binn\\
    folder.
