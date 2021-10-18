# BIRT Report Generator

The BIRT Report Generator utility (BIRTRptgen.exe) calls the
BIRTPROCESSOR handler to execute reports created with the Business
Intelligence and Reporting Tools (BIRT). SMA Technologies distributes many predefined reports
with OpCon that can be scheduled using the
BIRT Report Generator program. BIRTrptgen.exe is installed with the SAM
to the \<Target Directory\>\\OpConxps\\Utilities\\ directory. All
reports executed by the BIRT Report Generator must exist in the
following folder:

\<Target
Directory\>\\OpConxps\\SAM\\BIRT\\ReportEngine\\OpConXPS_Reports

During installation, the Report Generator schedule should have been
imported. On this schedule, SMA Technologies has provided one template job for every distributed report. For more
information, refer to [Report Generator Schedule](../../objects/schedules.md#report-generator-schedule)
 in the **Concepts** online help.

## Syntax

Use the following syntax for the BIRTRptgen.exe program in the \<Target
Directory\>\\OpConxps\\Utilities\\:

BIRTRptgen.exe --r\<report\> \[-j\[\[\$JOBID\]\]\] \[-t\<file type\]
\[-o\<output target file\>\] \[-p\<parameters\>\]

### Parameters

The following describes the command-line parameters:

- **BIRTRptgen.exe**: The name of the BIRT Report Generator program.
- **-r** \<report\>: Defines file name for the report to run.
  - This parameter is required.
  - No file extension needs to be given.
- **-j\[\[\$JOBID\]\]**: The unique internal job number for the job     when it executes. Define this parameter if you would like to see the
    final output location and file name in the \"Additional Job
    Information\" for a job from any Operations Job Information view.
  - The value of \[\[\$JOBID\]\] is the only way to accurately         retrieve the unique internal job number on each execution of the
        job.
- **-t** \<file type\>: Defines the format of the file.
  - This parameter is optional. If not specified, the default is
        PDF.
  - Valid options are PDF, HTML, and XLS.

    +----------------------------------+----------------------------------+
    | ![White pencil/paper icon on     | **NOTE:** [When reports are      |     | gray circular                    | exported to XLS format, the      |
    | background](../../.              | following limitations are        |
    | ./Resources/Images/note-icon(48x | applied: ]           |
    | 48).png "Note icon") |                                  |
    |                                  | -   [The final XLS file will not |     |                                  |     contain the report header    |
    |                                  |     and footer. ]    |
    |                                  | -   [Report charts are not       |     |                                  |     exported into the XLM        |
    |                                  |     format.]         |
    +----------------------------------+----------------------------------+

**-o** \<output target file\>: Defines the path or email address to send
the report to.

- This parameter is optional. If not specified, the default path is
    the \<Output Directory\>\\SAM\\Log\\Reports folder.
- The default report name is \<report\>\_\<message bus ID\>.\<format
    type\>.
- Use a path for the target folder and file name on any network
    machine that the system account on the SAM server has access to
    (e.g., C:\\My Reports\\new report name). Use a full path or a UNC;
    however, only UNC shares shared to \"Everyone\" will be successful.
    The BIRTPROCESSOR runs as the local system account on the SAM
    application server and will have limited network access.
- Use an email address. To send to multiple addresses, separate them
    with semicolons (e.g.,
    test\@smatechnologies.com;testgrp\@smatechnologies.com).
  - The attached file name will always be \<report\>\_\<message bus
        ID\>.\<format type\>.

**-p** \<parameters\>: Defines all of the connection and selection
criteria for the job. Refer to the next section for a
[Parameters](#Paramete). For information on the required
parameters for each report, refer to the descriptions in the
[Reports](../../reports/predefined.md) online help.

:::note
Date ranges should be written as oldest to newest date.
:::

#### Parameters

[]{#-p_Driver_URL}-p **Driver_URL**
Definition: Defines the connection path to the database. Only specify
this parameter to connect to some other database than this
OpCon database.

For SQL Authentication, use the following syntax and also supply the
User_Name and User_Password parameters:\
\
-p \"Driver_URL=jdbc:jtds:sqlserver://servername/databasename\"

For Windows Authentication, use the following syntax and also supply the
User_Name and User_Password parameters:\
\
-p
\"Driver_URL=jdbc:jtds:sqlserver://servername/databasename;domain=\<name\>\"

+----------------------------------+----------------------------------+
| ![White pencil/paper icon on     | **NOTE:** [If the SAM is         | | gray circular                    | installed on a 32-bit machine    |
| background](../../.              | and the SQL Database is on a     |
| ./Resources/Images/note-icon(48x | remote machine, you must choose  |
| 48).png "Note icon") | one of the following options to  |
|                                  | enable BIRTrptGen.exe to run     |
|                                  | reports using Windows            |
|                                  | Authentication:]     |
|                                  |                                  |
|                                  | -   [Configure SMA Service       | |                                  |     Manager to run as a domain   |
|                                  |     user that is in the Active   |
|                                  |     Directory Group that was     |
|                                  |     configured during            |
|                                  |     installation.For more        |
|                                  |     information, refer to [OpCon | |                                  |     Server                       |
|                                  |     Configuration](..            |
|                                  | /../Installation/OpCon-Server% |
|                                  | 20Configuration.md#Add) |
|                                  |      in the **OpCon        |
|                                  |     Installation** online        |
|                                  |     help.]           |
|                                  | -   [Add a Login named \"NT      | |                                  |     AUTHORITY\\ANONYMOUS LOGON\" |
|                                  |     to SQL Server. Type the name |
|                                  |     into the Login name field,   |
|                                  |     and do not use the Search    |
|                                  |     button. This is not a login  |
|                                  |     that is searchable. In User  |
|                                  |     Mapping, select the OpConxps |
|                                  |     database and \"opconxps\"    |
|                                  |     role                         |
|                                  |     membership.]     |
+----------------------------------+----------------------------------+

[]{#-p_User_Name}-p **User_Name**

- Definition: Defines SQL or Windows User ID to connect to the
    database. Only specify this parameter to connect to some other
    database than this OpCon database.
- Syntax for SQL: -p \"User_Name=UserName\"

[]{#-p_User_Password}-p **User_Password**

- Definition: Defines the a clear text password for SQL or Windows
    User ID to connect to the database. Only specify this parameter to
    connect to some other database than this
    OpCon database.
- Syntax: -p \"User_Password=UserPassword\"

[]{#-p_SKDDATE}-p **SKDDATE**

- Definition: Defines the schedule date(s) for the report.
- Syntax: -p \"SKDDATE=\<date\>\"
- The \<date\> can be either a Microsoft formatted date or in the
    format of CCYY-MM-DD. For the current schedule date, use the
    \[\[\$SCHEDULE DATEMS\]\] token. -   For all dates, use: -p \"SKDDATE\>0\"
- For a range of Dates, use: -p \"SKDDATE=\<date\> to \<date\>\"

[]{#-_p_SKDID}-p **SKDID**

- Definition: Defines the schedule ID(s) for the report.
- Syntax: -p \"SKDID=\<schedule\>\"
- The \<schedule\> can be a Schedule ID or a Schedule Name. For
    current schedule ID, use the \[\[\$SCHEDULE ID\]\] token. -   For all schedules, use: -p \"SKDID\>0\"
- For multiple schedules, separate the list of IDs or Names with
    commas (e.g., -p \"SKDID=1,2,3\" **- or -**\
    -p \"SKDID=MySchedule1,MySchedule2)

[]{#-p_DEPTID}-p **DEPTID**

- Definition: Defines the department ID(s) for the report.
- Syntax: -p \"DEPTID=\<department\>\"
- The \<department\> can be a Department ID or a Department Name.
- For all departments, use: -p \"DEPTID\>0\"
- For multiple departments, separate the list of IDs or Names with
    commas (e.g., -p \"DEPTID=1,2,3\" **- or -**\
    -p \"DEPTID=MyDepartment1,MyDepartment2)

[]{#-p_JOBTYPEID}-p **JOBTYPEID**
This is an optional parameter.

Definition: Defines the job type ID(s) for the report.

Syntax: -p \"JOBTYPEID=\<job type\>\"

The \<job type\> can be one of the following:

- -1 = Null
- 1 = File Transfer
- 3 = Windows
- 4 = OpenVMS
- 5 = IBM i
- 6 = UNIX
- 7 = OS 2200
- 9 = MCP
- 11 = BIS
- 12 = z/OS
- 13 = SAP R/3 and CRM
- 14 = SAP BW
- 15 = Container
- 17 = Java
- 18 = Tuxedo ART

```{=html}
<!-- -->
```

- For multiple job types, separate the list of IDs with commas (e.g.,
    -p \"JOBTYPEID=1,2,3\")

[]{#-p_ENSOPTIONS_OPTION}-p **ENSOPTIONS_OPTION**

- Definition: Defines the tab from Notification Management against
    which to run the report.
- Syntax: -p \"ENSOPTION_OPTION=\<option\>\"
- The \<option\> can be **M** (Machines), **S** (Schedules), or **J**
    (Jobs)

[]{#-p_MACHS_MACHID}-p **MACHS_MACHID**

- Definition: Defines the machine ID(s) for the report.
- Syntax: -p \"MACHS_MACHID=\<machine\>\"
- The \<machine\> can be a Machine ID or a Machine Name.
- For all machines, use: -p \"MACHS_MACHID\>0\"
- For multiple machines, separate the list of IDs or Names with
    commas\
    (e.g., -p \"MACHS_MACHID=1,2,3\" **- or -**\
    -p \"MACHS_MACHID=Windows1,Windows2)

[]{#-p_MACHGRPS_MACHGRPID}-p **MACHGRPS_MACHGRPID**

- Definition: Defines the machine group ID(s) for the report.
- Syntax: -p \"MACHGRPS_MACHGRPID=\<group\>\"
- The \<group\> can be a Machine Group ID or a Machine Group Name.
- For all machine groups, use: -p \"MACHGRPS_MACHGRPID\>0\"
- For multiple machine groups, separate the list of IDs or Names with
    commas\
    (e.g., -p \"MACHGRPS_MACHGRPID=1,2,3\" **- or -**\
    -p \"MACHGRPS_MACHGRPID=WindowsGRP1,WindowsGRP2)

[]{#-p_HISTORY_JSTART}-p **HISTORY_JSTART**

- Definition: Defines the month in job history for the report.
- Syntax: -p \"History_JSTART=CCYYMM\"
- Example: -p \"History_JSTART=201103\"

[]{#-p_HISTARC_SKDDATE}-p **HISTARC_SKDDATE**

- Definition: Defines the date(s) in the history archive table for the
    report.
- Syntax: -p \"HISTARC_SKDDATE=\<date\>\"
- Example: -p \"HISTARC_SKDDATE=2011-03-31\"
- The \<date\> can be either a Microsoft formatted date or in the
    format of CCYY-MM-DD.
- For all dates, use: -p \"HISTARC_SKDDATE\>0\"
- For a range of Dates, use: -p \"HISTARC_SKDDATE=\<date\> to
    \<date\>\"

[]{#-p_HISTORY_SKDDATE}-p **HISTORY_SKDDATE**

- Definition: Defines the date(s) in the history table for the report.
- Syntax: -p \"HISTORY_SKDDATE=\<date\>\"
- Example: -p \"HISTORY_SKDDATE=2011-03-31\"
- The \<date\> can be either a Microsoft formatted date or in the
    format of CCYY-MM-DD.
- For all dates, use: -p \"HISTORY_SKDDATE\>0\"
- For reports that support a range of Dates, use: -p
    \"HISTORY_SKDDATE=\<date\> to \<date\>\"

[]{#-p_AUDITHST_SQLDATE}-p **AUDITHST_SQLDATE**

- Definition: Defines the date(s) in the history view table for the
    report.
- Syntax: -p \"AUDITHST_SQLDATE=\<date\>\"
- Example: -p \"AUDITHST_SQLDATE=2011-03-31\"
- The \<date\> can be either a Microsoft formatted date or in the
    format of CCYY-MM-DD.
- For all dates, use: -p \"AUDITHST_SQLDATE\>0\"
- For a range of Dates, use: -p \"AUDITHST_SQLDATE=\<date\> to
    \<date\>\"

[]{#-p_CALDESC_CALID}-p **CALDESC_CALID**

- Definition: Defines the calendar ID(s) for the report.
- Syntax: -p \"CALDESC_CALID=\<calendar\>\"
- The \<calendar\> can be a Calendar ID or a Calendar Name.
- For all calendars, use: -p \"CALDESC_CALID\>0\"
- For multiple calendars, separate the list of IDs or Names with
    commas\
    (e.g., -p \"CALDESC_CALID=1,2,3\" **- or -**\
    -p \"CALDESC_CALID=Master Holiday,Fiscal)

[]{#-p_TAGNAME}-p **TAGNAME**

- Definition: Defines the Tag Name(s) for the report.
- Syntax: -p \"TAGNAME=\<tag name\>\"
- For multiple Tags, separate the list of Tag Names with commas\
    (e.g., -p \"TAGNAME=Critical,Accounting\")

[]{#-p_JOB_BUILD_STATUS}-p **JOB_BUILD_STATUS**

- Definition: Defines the build status of the job.
- Syntax: -p\"JOB_BUILD_STATUS=\<build status ID\>\"
- The \<build status ID\> can be one of the following:
  - 0 = On Hold
  - 99 = Releases
  - -1 = To Be Skipped
  - -99 = Disable Frequency
  - 1000 = Disable Build (in the Job Details frame)

[]{#-p_JAFC}-p **JAFC**

- Definition: Defines the JAFC for the report.
- Syntax: -p\"JAFC=\<field code\>\"
- The \<field code\> can be one of the following:
  - 3003 = Windows: Command Line
  - 3004 = Windows: Working Directory
  - 5008 = IBMi: Job Information (Job Description Name)
  - 5010 = IBMi: Job Information (Job Queue Name)
  - 5022 = IBMi: Call Information (Call)
  - 6001 = Unix: Start Image
  - 6002 = Unix: Parameters

[]{#-p_VALUE}-p **VALUE**

- Definition: Defines the user-defined text filter for the report.
- Syntax: -p\"VALUE=\<search text\>\"
- The \<search text\> is the string to use when filtering the report
    data.
  - SQL wildcard characters are supported. Use percent (%) for
        substitution of one or more characters. Use underscore (\_) for
        substitution of a single character.
- Example: To filter for all the items which contain \"gen\", use
    -p\"VALUE=%gen%\"

[]{#-p_ADV_FREQUENCY}-p **ADV_FREQUENCY**

- Definition: Defines the advanced frequency option to use for the
    report.
- Syntax: -p\"ADV_FREQUENCY=\<advanced frequency code\>\"
- The \<advanced frequency code\> must be one of the following:
  - 103 = Start Scheduling on
  - 104 = End Scheduling on
  - 105 = Include in Schedule on
  - 106 = Exclude from Schedule on
  - 107 = Exclude Month from Schedule
  - Example: -p\"ADV_FREQUENCY=103\"

[]{#-p_YEAR}-p **YEAR**

- Definition: Defines the history year for the report.
- Syntax: -p \"YEAR=\<year\>\"
- The \<year\> is a four-digit year. For example:
  - -p \"YEAR=2015\"
- For the current schedule year, use the \[\[\$SCHEDULE DATE yyyy\]\]     global property.

[]{#-p_JOB_STATUS}-p **JOB_STATUS**

- Definition: Defines the job status.
- Syntax: -p\"JOB_STATUS=\<job status code\>\"
- The \<job status code\> must be one of the following:
  - 900 = Finished OK
  - 910 = Failed
  - 920 = Marked Finished OK
  - 921 = Marked Failed
  - 940 = Skipped
  - Example: -p\"JOB_STATUS=910\"

[]{#-p_MONTH}-p **MONTH**

- Definition: Defines the history month for the report.
- Syntax: -p \"MONTH=\<month\>\"
- The \<month\> is the digit number for the month. For example:
  - 01: January
  - 02: February
- For the current schedule month, use the \[\[\$SCHEDULE DATE mm\]\]     global property.

[]{#-p_TOP}-p **TOP**

- Definition: Defines the maximum number of occurrences to show for
    the report.
- Syntax: -p \"TOP=\<number\>\"
- The \<number\> is a positive integer value.
- Default Value: 10

[]{#-p_HIGHLIGHT}-p **HIGHLIGHT**

- Definition: Highlights the grid cell in the report if the number in
    that cell is greater than or equal to the defined number.
- Syntax: -p\"HIGHLIGHT=\<number\>\"
- Default Value: 10
- The \<number\> is a positive integer value.
- Example: -p\"HIGHLIGHT=20\"

## Exit Codes

:::note
The Output Directory was configured during installation. For more information, refer to [File Locations](../../file-locations.md) in the **Concepts** online help.
:::

The BIRTRptGen.exe program uses the following exit codes:

  Status Number   Status Description
  --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0               Batch Run successful.
  -1              Program aborted. Review the BIRTRptGen.log file in the \<Output Directory\>\\Utilities\\Log folder and possibly the MSLSAM.log file in the \<Output Directory\>\\MSLSAM\\Log folder for information.
  -101            General program error in the wrapper program. Review the BIRTRptGen.log file in the \<Output Directory\>\\Utilities\\Log folder.
  -102            General program error in the SMA Processor handler. Review the SMAProcessor.log on the SAM server in the \<Output Directory\>\\SAM\\Log folder.

  : BIRT Report Generator Exit Codes
:::
