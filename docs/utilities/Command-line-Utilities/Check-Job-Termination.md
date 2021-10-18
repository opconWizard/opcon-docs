# Check Job Termination

The Check Job Termination utility (SMACheckTerm.exe) allows the
comparison of the termination description of a completed job to a
specific value(s). Based on whether the job\'s exit code matches the
comparison expression, the utility either fails or succeeds. If it
fails, the utility returns one of the failure exit codes listed in the
[Exit Codes](#Exit) table; otherwise, it returns a 0. As
a consequence, this utility enables branching to different jobs or to
different OpCon events based on the details
of a job\'s exit code.

## Rules

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** If formatting an    | | circular                         | SMACheckTerm command line to     |
| background](../../../Reso        | check a UNIX job, the command    |
| urces/Images/example-icon(48x48) | line would look something like   |
| .png "Example icon") | this:                            |
|                                  |                                  |
|                                  | SMACheckTerm.exe JobA ScheduleA  |
|                                  | \"\[\[\$SCHEDULE DATE\]\]\"      | |                                  | \"+000000001:0000:N\"            |
+----------------------------------+----------------------------------+

## Logging

:::note
The Output Directory was configured during installation. For more information, refer to [File Locations](../../file-locations.md) in the **Concepts** online help.
:::

The SMACheckTerm log file provides detailed information of errors
generated during the utility\'s execution. The log file resides in the
\<Output Directory\>\\SAM\\Log\\ directory. The syntax for the log file
name is SMACheckTerm\_\<date-time stamp\>.log.

All archived log files reside in the \<Output
Directory\>\\SAM\\Log\\Archive\\ folder. If an archive folder for the
day does not already exist, the utility creates one. The folder names
use the following naming convention: yyyy_mm_dd (Weekday). The logging
mechanism generates the weekday name according to the Regional Settings
of the user executing the utility.

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** If the Regional     | | circular                         | Settings are set to English, an  |
| background](../../../Reso        | archive folder would have the    |
| urces/Images/example-icon(48x48) | following name: 2008_01_11       |
| .png "Example icon") | (Friday).                        |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | If the Regional Settings are set |
|                                  | to French, an archive folder     |
|                                  | would have the following name:   |
|                                  | 2008_01_11 (Vendredi).           |
+----------------------------------+----------------------------------+

Once per day the SAM deletes old archive folders. The SAM retains 10
days of archived logs by default. If desired, change the Logging
settings in the Global Options. Refer to the [Maximum number of days archived SAM logs should be kept](../../administration/server-options.md#logging)
 setting in the **Concepts** online help.

:::note
The SAM does not purge any Archive folders if any files other than archived files are present.
:::

## Exit Codes

The SMACheckTerm.exe program uses the following exit codes:

  Exit Code   Exit Description
  ----------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0           Criterion is true.
  33001       No matching records found. The criterion is false. Review the command line for schedule name, schedule status, job name, and job status and make sure all of the parameters are valid.
  33002       Command-line syntax error in the parameters. Parsing error.
  33003       Database Connection Information, Usercode, and Password information is incorrect or SMAODBCConfiguration.dat file is missing.
  33004       Unknown.

  : SMACheckTerm Exit Codes
:::
