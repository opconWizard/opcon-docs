# OpCon Server Options

The **Enterprise Manager Administration** supports management of Server Options in OpCon. Only the OpCon administrative users in the ocadm role can access the options. Refer to [Managing Server Options](../Files/UI/Enterprise-Manager/Managing-Server-Options.md) in the **Enterprise Manager** online help.

## General Settings

The General category contains default behavior settings for the SAM.

|||||
|--- |--- |--- |--- |
|Job Dependency Offset Type|Calendar Days|Y|This parameter determines if the Job Dependencies with Offset values are calculated with calendar days or with occurrence of the job.If Calendar Days is selected, OpCon will look for the job on the specified number of calendar days offset from the current schedule date.If Occurrence is selected, OpCon will look for the job on the numbered occurrence of the schedule. JobB depends on JobA from yesterday's schedule, or if there were holidays in between - the last time Job A was on the schedule).The Calendar Days option would not meet this need because of the holiday requirement. With calendar days on a 5-day work week, the Tuesday through Friday jobs would resolve properly to the previous calendar day. However, the job on Monday would be looking for JobA on Sunday because it is one Calendar Day back.This customer should choose to use the Occurrence option for job dependency offset calculation. OpCon will look back to the last occurrence of Job A before "today", thus resolving properly for Monday through Friday on a 5-day schedule. Valid values are Calendar Days and Occurrence.|
|Alternate Odd and Even Weeks|False|Y|The alternate to the Odd/Even Weeks frequency is Every Other Week. By setting the Server Option "Alternate Odd and Even Weeks" to "True," jobs using the Odd/Even Weeks frequency will be treated as Every Other Week frequency.|
|Number of Runs Included in Job Average Calculations|10|Y|Defines the number of most recent job history records to use when SAM Calculates Job Averages. Valid values range from 1 to 999.|
|SAM Calculates Job Averages|False|Y|Determines if SAM calculates job start and run time averages after each job run. If this value is set to True:SAM calculates the average times the way the SMA_JOBAVG stored procedure does. For more information, refer to SMA_JOBAVG in the Database Information online help. SAM passes the following parameters for the calculation: SW1: The value from Server Options for Number of Runs Included in Job Average Calculations.SW2: 1SW3: 2SW4: The Schedule Name for the job that just ran.SW5: The Job Name that just ranSpecial: SAM passes a special parameter for the Frequency of the job that just ran.The job start and run time averages will only be recalculated for jobs that are in use in the Daily. This will keep the times more current, but may cause slight processing delays in SAM depending on the job processing load. If this value is set to False, set up the job SMA JOB AVERAGE on the SMAUtility schedule to run once per day. For more information, refer to SMA Job Average. Valid values are True and False.|
|Remove Period in Abbreviated Months and Days|False|Y|SAM will check this setting for resolving Tokens that contain abbreviated months and abbreviated days.
                                    Valid values are True and False.If True, SAM strips the period from abbreviated months and days.If False, SAM leaves the period on abbreviated months and days.
                                
                                Note: This setting should only be set to True for customers requiring backward compatibility to older versions of SAM used in the few locales where periods are now included by default with some abbreviations.|
|Allow Wild Cards in Events|False|Y|This parameter indicates whether or not * (asterisk) and ? (question mark) are treated as wild cards in Schedule, Job, and Machine Names within Events.

                                    If True, * (asterisk) and ? (question mark) are treated as wild cards.
                                    If False, * (asterisk) and ? (question mark) are not treated as wild.|
|TLS Certificate Serial Number|*blank*|Y|This parameter is an identifier of the digital certificate that is optionally assigned to the OpCon server's SMANetCom program, required only when TLS Client Validation has been selected by one or more LSAMs.
                                    This number can be found in the certificate store of the machine where the OpCon server is installed.
                                    When blank, the OpCon server's SMANetCom program will not supply a TLS Client certificate to any LSAM.

                                Note: If an LSAM requires TLS Client validation, but SMANetCom does not provide its certificate, then the communication link with that LSAM will fail to connect.|
|Login Security Message|*blank*|Y|This parameter  configures a security message to display to users after logging into  the application.

                                    If a value is not specified, then no security message is configured.
                                    If a value is specified, then this value is shown in the  security message that is displayed to users after login.
                                
                                Note: This parameter configures the security message to display in both the Enterprise Manager and Solution Manager applications.|
|Incident Management System|*blank*|Y|This parameter identifies the name of the ticketing system that is used for incident management.
                                    If a value is specified, then this value  is used  as a label to replace the "Incident Ticket ID" label in the Daily Job Information dialog.|
|Allow Job Events to Restart Schedules|False|Y|This parameter configures the SAM to allow an event to start a completed schedule.
                                    If this option is activated, the following events cause the restart of a completed schedule:$JOB:ADD$JOB:RESTART$JOB:RESCHEDULE
                                    By default, the SAM does not restart a completed schedule and logs the event as an error in the Critical.log.
                                    When this option is activated, the SAM restarts a schedule to allow events to process if they are received after a schedule is completed.
                                    Valid values are True and False.|
|Failed jobs should keep the Schedule "In Process"|False|Y|This parameter configures the SAM to keep schedules In Process that contain Failed jobs and Marked Failed jobs.
                                    By default, the SAM closes a schedule when all jobs are in one of the following job status categories: Cancelled, Skipped, Finished OK, or Failed. Refer to Jobs Status Change Commands.
                                    Valid values are True and False.|
|Number of Days to Keep a Service Request Execution|7|Y|This parameter defines the number of days to retain service request execution history.|
|Solution Manager URL|*blank*|N|This parameter defines the Solution Manager URL to allow opening Solution Manager within the Enterprise Manager.
                                    If a value is specified, a Solution Manager option will appear in the Navigation frame.

                                Note: After defining a URL and saving the value, you must log out then log in to the Enterprise Manager for the Solution Manager option to appear in the Navigation frame.|

## Logging Options

The Logging category contains log and trace settings for the SAM.

+--------------------+---------+---------------+--------------------+
| Option Parameter   | Default | Dynamic (Y/N) | Description        |
+====================+:=======:+:=============:+====================+
| Log Critical       | False   | Y             | -   This parameter |
| messages to NT     |         |               |     enables        |
| Events             |         |               |     writing of all |
|                    |         |               |     SAM critical   |
|                    |         |               |     errors to the  |
|                    |         |               |     Application    |
|                    |         |               |     Log in the     |
|                    |         |               |     Microsoft      |
|                    |         |               |     Event Log.     |
|                    |         |               | -   To minimize    |
|                    |         |               |     overhead, the  |
|                    |         |               |     SAM does not   |
|                    |         |               |     write critical |
|                    |         |               |     messages to    |
|                    |         |               |     the Windows    |
|                    |         |               |     event log by   |
|                    |         |               |     default.       |
|                    |         |               | -   Valid values   |
|                    |         |               |     are True and   |
|                    |         |               |     False.         |
+--------------------+---------+---------------+--------------------+
| Log job dependency | True    | Y             | -   This parameter |
| errors to          |         |               |                    |
| Critical.log       |         |               |   enables/disables |
|                    |         |               |     logging job    |
|                    |         |               |     dependency     |
|                    |         |               |     errors to the  |
|                    |         |               |     critical log.  |
|                    |         |               | -   Valid values   |
|                    |         |               |     are True and   |
|                    |         |               |     False.         |
|                    |         |               |     -   If True,   |
|                    |         |               |         the SAM    |
|                    |         |               |         logs all   |
|                    |         |               |         job        |
|                    |         |               |         dependency |
|                    |         |               |         errors to  |
|                    |         |               |                    |
|                    |         |               |      Critical.log. |
|                    |         |               |     -   If False,  |
|                    |         |               |         the SAM    |
|                    |         |               |         stops      |
|                    |         |               |         logging    |
|                    |         |               |         job        |
|                    |         |               |         dependency |
|                    |         |               |         errors to  |
|                    |         |               |         the        |
|                    |         |               |                    |
|                    |         |               |      Critical.log. |
|                    |         |               |         When the   |
|                    |         |               |         SAM        |
|                    |         |               |         Message    |
|                    |         |               |         Logging    |
|                    |         |               |         Level is   |
|                    |         |               |         set to     |
|                    |         |               |         Verbose or |
|                    |         |               |         Debug, the |
|                    |         |               |         SAM writes |
|                    |         |               |         job        |
|                    |         |               |         dependency |
|                    |         |               |         errors to  |
|                    |         |               |         the        |
|                    |         |               |         SAM.log.   |
|                    |         |               |         Refer to   |
|                    |         |               |         [SAM       | |                    |         |               |         Message    |
|                    |         |               |         Logging    |
|                    |         |               |         Level]     |
|                    |         |               | (#SAM_Message_Logg |
|                    |         |               | ing_Level) |
|                    |         |               |              |
|                    |         |               |         below.     |
+--------------------+---------+---------------+--------------------+
| []{#Maximum_n      | 10      | Y             | -   This parameter | | umber_of_days_arch |         |               |     sets the       |
| ived_SAM_logs_shou |         |               |     maximum number |
| ld_be_kept}Maximum |         |               |     of archive     |
| number of days     |         |               |     folders (i.e., |
| archived SAM logs  |         |               |     days) for all  |
| should be kept     |         |               |     log archives.  |
|                    |         |               | -   By default,    |
|                    |         |               |     the SAM        |
|                    |         |               |     deletes        |
|                    |         |               |     archived logs  |
|                    |         |               |     older than 10  |
|                    |         |               |     days.          |
|                    |         |               | -   The SAM        |
|                    |         |               |     archives log   |
|                    |         |               |     files once per |
|                    |         |               |     day.           |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 365.        |
|                    |         |               |                    |
|                    |         |               | **CAUTION:** This  |
|                    |         |               | number must be     |
|                    |         |               | less than the      |
|                    |         |               | ArchiveDaysToKeep  |
|                    |         |               | setting in the     |
|                    |         |               | SMAServMan         |
|                    |         |               | configuration      |
|                    |         |               | file. Refer to     |
|                    |         |               | [License           | |                    |         |               | Type               |
|                    |         |               | s](../Server-Pro |
|                    |         |               | grams/Licensing.ht |
|                    |         |               | m#License) |
|                    |         |               |  in the      |
|                    |         |               | **Server           |
|                    |         |               | Programs** online  |
|                    |         |               | help.              |
+--------------------+---------+---------------+--------------------+
| Maximum number of  | 10      | Y             | -   This parameter |
| days Schedule      |         |               |     sets the       |
| Build logs should  |         |               |     maximum number |
| be kept            |         |               |     of days to     |
|                    |         |               |     keep Schedule  |
|                    |         |               |     Manager logs.  |
|                    |         |               | -   By default,    |
|                    |         |               |     the SAM        |
|                    |         |               |     deletes logs   |
|                    |         |               |     older than 10  |
|                    |         |               |     days.          |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 365.        |
+--------------------+---------+---------------+--------------------+
| []{#SAM_Message    | Terse   | Y             | -   This parameter | |_Logging_Level}SAM |         |               |     determines the |
| Message Logging    |         |               |     amount of SAM  |
| Level              |         |               |     processing     |
|                    |         |               |     information    |
|                    |         |               |     written to the |
|                    |         |               |     SAM log files. |
|                    |         |               | -   Valid values   |
|                    |         |               |     are *Terse*,   |
|                    |         |               |     *Verbose*, and |
|                    |         |               |     *Debug*.       |
|                    |         |               |     -   *Terse* is |
|                    |         |               |         the        |
|                    |         |               |         default    |
|                    |         |               |         setting    |
|                    |         |               |         providing  |
|                    |         |               |         only       |
|                    |         |               |                    |
|                    |         |               |       job/schedule |
|                    |         |               |         start and  |
|                    |         |               |         finish     |
|                    |         |               |                    |
|                    |         |               |       information. |
|                    |         |               |     -   *Verbose*  |
|                    |         |               |         provides   |
|                    |         |               |         additional |
|                    |         |               |                    |
|                    |         |               |        information |
|                    |         |               |         regarding  |
|                    |         |               |         machine    |
|                    |         |               |                    |
|                    |         |               |        processing. |
|                    |         |               |     -   *Debug*    |
|                    |         |               |         provides   |
|                    |         |               |         verbose    |
|                    |         |               |         messaging  |
|                    |         |               |         plus more  |
|                    |         |               |         detailed   |
|                    |         |               |                    |
|                    |         |               |        information |
|                    |         |               |         on SAM     |
|                    |         |               |                    |
|                    |         |               |        processing. |
+--------------------+---------+---------------+--------------------+

## Time Settings

The Time Settings category contains time-related settings for the SAM.

+--------------------+---------+---------------+--------------------+
| Option Parameter   | Default | Dynamic (Y/N) | Description        |
+====================+:=======:+:=============:+====================+
| Hour of each day   | 0       | Y             | -   By default, at |
| SAM should detect  |         |               |     midnight the   |
| Schedules to build |         |               |     SAM detects    |
|                    |         |               |     schedules to   |
|                    |         |               |     build.         |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 23.         |
|                    |         |               | -   The hours are  |
|                    |         |               |     based on a     |
|                    |         |               |     24-hour format |
|                    |         |               |     starting from  |
|                    |         |               |     0 (midnight)   |
|                    |         |               |     to 23 (11      |
|                    |         |               |     p.m.).         |
|                    |         |               | -   The SAM only   |
|                    |         |               |     processes the  |
|                    |         |               |     builds once    |
|                    |         |               |     per day. If    |
|                    |         |               |     this hour      |
|                    |         |               |     changes after  |
|                    |         |               |     the build      |
|                    |         |               |     process, SAM   |
|                    |         |               |     does not       |
|                    |         |               |     consider this  |
|                    |         |               |     parameter      |
|                    |         |               |     until the next |
|                    |         |               |     day.           |
|                    |         |               | -   Set specific   |
|                    |         |               |     times for      |
|                    |         |               |     individual     |
|                    |         |               |     schedules to   |
|                    |         |               |     build on the   |
|                    |         |               |     schedule       |
|                    |         |               |     definitions.   |
|                    |         |               |     For more       |
|                    |         |               |     information,   |
|                    |         |               |     refer to       |
|                    |         |               |     [Schedule      | |                    |         |               |     Maintenance](S |
|                    |         |               | chedule-Definiti |
|                    |         |               | on.md#Schedule_Ma |
|                    |         |               | intenance) |
|                    |         |               |     .        |
|                    |         |               |                    |
|                    |         |               | **Note:** To       |
|                    |         |               | enable             |
|                    |         |               | notification for   |
|                    |         |               | failed schedule    |
|                    |         |               | build processes,   |
|                    |         |               | define             |
|                    |         |               | [OpCon]{.Gener     | |                    |         |               | alOpConGlobalName} |
|                    |         |               | events on the      |
|                    |         |               | SMA_SKD_BUILD job  |
|                    |         |               | on the AdHoc       |
|                    |         |               | schedule.          |
|                    |         |               |                    |
|                    |         |               |                    |
|                    |         |               |                    |
|                    |         |               | [SMA               | |                    |         |               | Technologies]{.G   |
|                    |         |               | eneralCompanyName} |
|                    |         |               | provides template  |
|                    |         |               | jobs for AdHoc     |
|                    |         |               | with the           |
|                    |         |               | **AdHoc**.mdb      |
|                    |         |               | file. For more     |
|                    |         |               | information, refer |
|                    |         |               | to [SMA_SKD Jobs   | |                    |         |               | on the AdHoc       |
|                    |         |               | Schedule](A        |
|                    |         |               | dHoc-Schedule.ht |
|                    |         |               | m#SMA_SKD) |
|                    |         |               | .            |
+--------------------+---------+---------------+--------------------+
| Minutes between    | 5       | Y             | -   This parameter |
| checking running   |         |               |     determines the |
| jobs               |         |               |     maximum time   |
|                    |         |               |     period for the |
|                    |         |               |     SAM to wait    |
|                    |         |               |     before         |
|                    |         |               |     inquiring      |
|                    |         |               |     about job      |
|                    |         |               |     status.        |
|                    |         |               |     -   SAM only   |
|                    |         |               |         inquires   |
|                    |         |               |         about the  |
|                    |         |               |         job status |
|                    |         |               |         if         |
|                    |         |               |         SMANetCom  |
|                    |         |               |         has not    |
|                    |         |               |         received a |
|                    |         |               |         valid      |
|                    |         |               |         message    |
|                    |         |               |         from the   |
|                    |         |               |         [L         | |                    |         |               | SAM]{.GeneralLSAM} |
|                    |         |               |         in the     |
|                    |         |               |         configured |
|                    |         |               |         amount of  |
|                    |         |               |         time.      |
|                    |         |               | -   When jobs are  |
|                    |         |               |     processing,    |
|                    |         |               |     the status     |
|                    |         |               |     responses      |
|                    |         |               |     update the     |
|                    |         |               |     timestamp of   |
|                    |         |               |     the last time  |
|                    |         |               |     the SAM        |
|                    |         |               |     received job   |
|                    |         |               |     information.   |
|                    |         |               |     For short      |
|                    |         |               |     jobs, there is |
|                    |         |               |     no need for    |
|                    |         |               |     the SAM to     |
|                    |         |               |     request job    |
|                    |         |               |     status. If the |
|                    |         |               |     SAM does not   |
|                    |         |               |     receive a      |
|                    |         |               |     status for the |
|                    |         |               |     job within the |
|                    |         |               |     specified      |
|                    |         |               |     time-out       |
|                    |         |               |     value, it      |
|                    |         |               |     requests the   |
|                    |         |               |     job status.    |
|                    |         |               | -   This timer is  |
|                    |         |               |     necessary for  |
|                    |         |               |     jobs that run  |
|                    |         |               |     for long       |
|                    |         |               |     periods of     |
|                    |         |               |     time. It is    |
|                    |         |               |     also necessary |
|                    |         |               |     for possible   |
|                    |         |               |     losses in      |
|                    |         |               |     communication  |
|                    |         |               |     between        |
|                    |         |               |     SMANetCom and  |
|                    |         |               |     the            |
|                    |         |               |     [LS            | |                    |         |               | AM]{.GeneralLSAM}. |
|                    |         |               | -   If             |
|                    |         |               |     job-processing |
|                    |         |               |     issues are     |
|                    |         |               |     suspected, set |
|                    |         |               |     this timer to  |
|                    |         |               |     three minutes  |
|                    |         |               |     for debugging. |
|                    |         |               |     When finished  |
|                    |         |               |     debugging, set |
|                    |         |               |     the timer back |
|                    |         |               |     to five        |
|                    |         |               |     minutes.       |
|                    |         |               | -   If all is      |
|                    |         |               |     running well,  |
|                    |         |               |     this timer can |
|                    |         |               |     be increased   |
|                    |         |               |     to a           |
|                    |         |               |     recommended    |
|                    |         |               |     maximum of 10  |
|                    |         |               |     minutes.       |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 1   |
|                    |         |               |     to 1440.       |
|                    |         |               |                    |
|                    |         |               | **Note:** Jobs in  |
|                    |         |               | a "Start          |
|                    |         |               | Attempted" status |
|                    |         |               | are not subject to |
|                    |         |               | this timer because |
|                    |         |               | they are checked   |
|                    |         |               | in as timely a     |
|                    |         |               | fashion as         |
|                    |         |               | possible.          |
+--------------------+---------+---------------+--------------------+
| Seconds SAM should | 180     | Y             | -   This parameter |
| wait between       |         |               |     determines the |
| PreRun attempts    |         |               |     amount of time |
|                    |         |               |     in seconds     |
|                    |         |               |     between prerun |
|                    |         |               |     attempts.      |
|                    |         |               | -   By default,    |
|                    |         |               |     the SAM        |
|                    |         |               |     re-attempts    |
|                    |         |               |     prerun jobs    |
|                    |         |               |     every 180      |
|                    |         |               |     seconds (3     |
|                    |         |               |     minutes) until |
|                    |         |               |     the job        |
|                    |         |               |     succeeds.      |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 32000.      |
+--------------------+---------+---------------+--------------------+

## SMTP Server Settings

The SMTP Server Settings category contains configuration options the SMA
Notify Handler will use to send email and/or SMS notifications.

+-------------------+-----------+---------------+-------------------+
| Option Parameter  | Default   | Dynamic (Y/N) | Description       |
+===================+:=========:+:=============:+===================+
| JORS Attachment   | 120       | Y             | -   Defines the   |
| Timeout           |           |               |     number of     |
|                   |           |               |     seconds the   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler       |
|                   |           |               |     should wait   |
|                   |           |               |     for an        |
|                   |           |               |     attachment to |
|                   |           |               |     return from a |
|                   |           |               |     JORS request. |
|                   |           |               | -   Valid values  |
|                   |           |               |     range from 60 |
|                   |           |               |     to 3600       |
|                   |           |               |     seconds.      |
+-------------------+-----------+---------------+-------------------+
| []{#Authenticatio | \<blank\> | Y             | -   Defines the   | | n_User_(UNC_Acces |           |               |     Windows user  |
| s)}Authentication |           |               |     account the   |
| User (UNC Access) |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     use to gain   |
|                   |           |               |     access to     |
|                   |           |               |     machines and  |
|                   |           |               |     UNC paths on  |
|                   |           |               |     the network.  |
|                   |           |               | -   This user is  |
|                   |           |               |     required if   |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler has   |
|                   |           |               |     to send Email |
|                   |           |               |     attachments   |
|                   |           |               |     from network  |
|                   |           |               |     shares.       |
|                   |           |               | -   This user is  |
|                   |           |               |     required if   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     send Network  |
|                   |           |               |     Message       |
|                   |           |               |                   |
|                   |           |               |    notifications. |
|                   |           |               |     Refer to      |
|                   |           |               |     [Sending      | |                   |           |               |     Network       |
|                   |           |               |     Messages](    |
|                   |           |               | ../Files/UI/Enterprise% |
|                   |           |               | 20Manager/Sending |
|                   |           |               | -Network-Mess |
|                   |           |               | ages.md) |
|                   |           |               |      in the |
|                   |           |               |     **Enterprise  |
|                   |           |               |     Manager**     |
|                   |           |               |     online help.  |
|                   |           |               | -   The user must |
|                   |           |               |     have          |
|                   |           |               |     privileges to |
|                   |           |               |     "Read" all  |
|                   |           |               |     network       |
|                   |           |               |     shares from   |
|                   |           |               |     which the SMA |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     pick up       |
|                   |           |               |     files. The    |
|                   |           |               |     user must     |
|                   |           |               |     also have     |
|                   |           |               |     "Write"     |
|                   |           |               |     privileges to |
|                   |           |               |     the \<Output  |
|                   |           |               |     Dire          |
|                   |           |               | ctory\>\\SAM\\Log |
|                   |           |               |     folder.       |
|                   |           |               |                   |
|                   |           |               | **Note:** The     |
|                   |           |               | Output Directory  |
|                   |           |               | was configured    |
|                   |           |               | during            |
|                   |           |               | installation. For |
|                   |           |               | more information, |
|                   |           |               | refer to [File    | |                   |           |               | Locati            |
|                   |           |               | ons](File-Locat |
|                   |           |               | ions.md) |
|                   |           |               |  in this    |
|                   |           |               | online help.      |
+-------------------+-----------+---------------+-------------------+
| []{#Authentica    | \<blank\> | Y             | -   Defines the   | | tion_Encrypted_Pa |           |               |     encrypted     |
| ssword_(UNC_Acces |           |               |     password for  |
| s)}Authentication |           |               |     the Windows   |
| Encrypted         |           |               |     user the SMA  |
| Password (UNC     |           |               |     Notify        |
| Access)           |           |               |     Handler will  |
|                   |           |               |     use to gain   |
|                   |           |               |     access to     |
|                   |           |               |     machines and  |
|                   |           |               |     UNC paths on  |
|                   |           |               |     the network.  |
|                   |           |               | -   This user is  |
|                   |           |               |     required if   |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler has   |
|                   |           |               |     to send Email |
|                   |           |               |     attachments   |
|                   |           |               |     from network  |
|                   |           |               |     shares.       |
|                   |           |               | -   This user is  |
|                   |           |               |     required if   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     send Network  |
|                   |           |               |     Message       |
|                   |           |               |                   |
|                   |           |               |    notifications. |
|                   |           |               |     Refer to      |
|                   |           |               |     [Sending      | |                   |           |               |     Network       |
|                   |           |               |     Messages](    |
|                   |           |               | ../Files/UI/Enterprise% |
|                   |           |               | 20Manager/Sending |
|                   |           |               | -Network-Mess |
|                   |           |               | ages.md) |
|                   |           |               |      in the |
|                   |           |               |     **Enterprise  |
|                   |           |               |     Manager**     |
|                   |           |               |     online help.  |
|                   |           |               | -   To encrypt    |
|                   |           |               |     the password  |
|                   |           |               |     manually, use |
|                   |           |               |     the Password  |
|                   |           |               |     encryption    |
|                   |           |               |     tool in the   |
|                   |           |               |     Enterprise    |
|                   |           |               |     Manager. Then |
|                   |           |               |     copy and      |
|                   |           |               |     paste the     |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the value of  |
|                   |           |               |     this setting. |
|                   |           |               |     For more      |
|                   |           |               |     information,  |
|                   |           |               |     refer to      |
|                   |           |               |     [Encrypting   | |                   |           |               |                   |
|                   |           |               |    Passwords](../ |
|                   |           |               | UI/Enterprise-M |
|                   |           |               | anager/Menus.md# |
|                   |           |               | Encrypti) |
|                   |           |               |      in the |
|                   |           |               |     **Enterprise  |
|                   |           |               |     Manager**     |
|                   |           |               |     online help.  |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Name  | \<blank\> | Y             | -   Defines the   |
| (Primary Email)   |           |               |     name of the   |
|                   |           |               |     Primary SMTP  |
|                   |           |               |     server for    |
|                   |           |               |     sending       |
|                   |           |               |     email. If no  |
|                   |           |               |     SMS servers   |
|                   |           |               |     are defined,  |
|                   |           |               |     this server   |
|                   |           |               |     will also     |
|                   |           |               |     send SMS text |
|                   |           |               |     messages.     |
|                   |           |               | -   If the value  |
|                   |           |               |     is blank, the |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler       |
|                   |           |               |     cannot send   |
|                   |           |               |     email or text |
|                   |           |               |                   |
|                   |           |               |    notifications. |
|                   |           |               | -   Default:      |
|                   |           |               |     Blank         |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Port  | 25        | Y             | -   Defines the   |
| (Primary Email)   |           |               |     server port   |
|                   |           |               |     that SMA      |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use when      |
|                   |           |               |     sending email |
|                   |           |               |     through the   |
|                   |           |               |     Primary SMTP  |
|                   |           |               |     server.       |
|                   |           |               | -   The user can  |
|                   |           |               |     set the value |
|                   |           |               |     for this      |
|                   |           |               |     option.       |
|                   |           |               |     -   Valid     |
|                   |           |               |         values    |
|                   |           |               |         range     |
|                   |           |               |         from 0 to |
|                   |           |               |         9999, and |
|                   |           |               |         must be   |
|                   |           |               |         positive. |
|                   |           |               |     -   If no     |
|                   |           |               |                   |
|                   |           |               |      user-defined |
|                   |           |               |         value is  |
|                   |           |               |                   |
|                   |           |               |        specified, |
|                   |           |               |         then the  |
|                   |           |               |         default   |
|                   |           |               |         port (25) |
|                   |           |               |         will be   |
|                   |           |               |         used.     |
+-------------------+-----------+---------------+-------------------+
| SMTP Notification | noreply   | Y             | -   Defines the   |
| Address (Primary  |           |               |     email address |
| Email)            |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use as the    |
|                   |           |               |     "From"      |
|                   |           |               |     address when  |
|                   |           |               |     sending       |
|                   |           |               |     E-mail or     |
|                   |           |               |     Text Messages |
|                   |           |               |     through the   |
|                   |           |               |     Primary Email |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     this setting  |
|                   |           |               |     is ignored    |
|                   |           |               |     and the       |
|                   |           |               |     administrator |
|                   |           |               |     must          |
|                   |           |               |     configure the |
|                   |           |               |     SMTP          |
|                   |           |               |                   |
|                   |           |               |    Authentication |
|                   |           |               |     User and      |
|                   |           |               |     Password for  |
|                   |           |               |     the Primary   |
|                   |           |               |     Email server. |
|                   |           |               | -   If a value is |
|                   |           |               |     not           |
|                   |           |               |     specified,    |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     default to    |
|                   |           |               |     noreply.      |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     that "From" |
|                   |           |               |     address,      |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines an    |
| Authentication    |           |               |     email address |
| User (Primary     |           |               |     for           |
| Email)            |           |               |                   |
|                   |           |               |    authentication |
|                   |           |               |     to the        |
|                   |           |               |     Primary Email |
|                   |           |               |     SMTP server.  |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here.         |
|                   |           |               | -   If a value is |
|                   |           |               |     not specified |
|                   |           |               |     when required |
|                   |           |               |     by the SMTP   |
|                   |           |               |     server, the   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     not be able   |
|                   |           |               |     to send       |
|                   |           |               |     emails or     |
|                   |           |               |     text          |
|                   |           |               |     messages.     |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     the user and  |
|                   |           |               |     password      |
|                   |           |               |     specified,    |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines the   |
| Authentication    |           |               |     password for  |
| Encrypted         |           |               |     the SMTP      |
| Password (Primary |           |               |                   |
| Email)            |           |               |    Authentication |
|                   |           |               |     User for the  |
|                   |           |               |     Primary Email |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here that     |
|                   |           |               |     provides the  |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the user.     |
|                   |           |               | -   To encrypt    |
|                   |           |               |     the password  |
|                   |           |               |     manually, use |
|                   |           |               |     the Password  |
|                   |           |               |     encryption    |
|                   |           |               |     tool in the   |
|                   |           |               |     Enterprise    |
|                   |           |               |     Manager. Then |
|                   |           |               |     copy and      |
|                   |           |               |     paste the     |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the value of  |
|                   |           |               |     this setting. |
|                   |           |               |     For more      |
|                   |           |               |     information,  |
|                   |           |               |     refer to      |
|                   |           |               |     [Encrypting   | |                   |           |               |                   |
|                   |           |               |    Passwords](../ |
|                   |           |               | UI/Enterprise-M |
|                   |           |               | anager/Menus.md# |
|                   |           |               | Encrypti) |
|                   |           |               |      in the |
|                   |           |               |     **Enterprise  |
|                   |           |               |     Manager**     |
|                   |           |               |     online help.  |
+-------------------+-----------+---------------+-------------------+
| SMTP              | False     | Y             | -   Determines if |
| Authentication    |           |               |     the SMA       |
| -Enable SSL       |           |               |     Notify        |
| (Primary Email)   |           |               |     Handler will  |
|                   |           |               |     use SSL       |
|                   |           |               |     encryption    |
|                   |           |               |     when          |
|                   |           |               |     connecting to |
|                   |           |               |     the Primary   |
|                   |           |               |     Email SMTP    |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires SSL  |
|                   |           |               |     Encryption,   |
|                   |           |               |     the value     |
|                   |           |               |     must be set   |
|                   |           |               |     to True.      |
+-------------------+-----------+---------------+-------------------+
| SMTP Total        | 10        | Y             | -   Determines    |
| Attachment Size   |           |               |     the maximum   |
| in MB (Primary    |           |               |     total of MB   |
| Email)            |           |               |     in the        |
|                   |           |               |     attachments   |
|                   |           |               |     for an email  |
|                   |           |               |     attachments   |
|                   |           |               |     notification  |
|                   |           |               |     from the      |
|                   |           |               |     Primary Email |
|                   |           |               |     SMTP server.  |
|                   |           |               | -   This value    |
|                   |           |               |     should match  |
|                   |           |               |     the limit set |
|                   |           |               |     by the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP Maximum      | 50        | Y             | -   Determines    |
| Number of         |           |               |     the maximum   |
| Attachments       |           |               |     number of     |
| (Primary Email)   |           |               |     attachments   |
|                   |           |               |     allowed per   |
|                   |           |               |     email on a    |
|                   |           |               |     notification  |
|                   |           |               |     from the      |
|                   |           |               |     Primary Email |
|                   |           |               |     SMTP server.  |
|                   |           |               | -   This value    |
|                   |           |               |     should match  |
|                   |           |               |     the limit set |
|                   |           |               |     by the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Name  | \<blank\> | Y             | -   Defines the   |
| (Secondary Email) |           |               |     name of the   |
|                   |           |               |     Secondary     |
|                   |           |               |     SMTP server   |
|                   |           |               |     for sending   |
|                   |           |               |     email. If     |
|                   |           |               |     messages fail |
|                   |           |               |     to send       |
|                   |           |               |     through the   |
|                   |           |               |     Primary Email |
|                   |           |               |     server, the   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     attempt to    |
|                   |           |               |     send the      |
|                   |           |               |     message again |
|                   |           |               |     through the   |
|                   |           |               |     Secondary     |
|                   |           |               |     Email server. |
|                   |           |               |     If no SMS     |
|                   |           |               |     servers are   |
|                   |           |               |     defined, this |
|                   |           |               |     server will   |
|                   |           |               |     also serve as |
|                   |           |               |     a Secondary   |
|                   |           |               |     server to     |
|                   |           |               |     send SMS text |
|                   |           |               |     messages.     |
|                   |           |               | -   If the value  |
|                   |           |               |     is blank, the |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     not attempt   |
|                   |           |               |     messages      |
|                   |           |               |     through a     |
|                   |           |               |     Secondary     |
|                   |           |               |     server.       |
|                   |           |               | -   Default:      |
|                   |           |               |     Blank         |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Port  | 25        | Y             | -   Defines the   |
| (Secondary Email) |           |               |     server port   |
|                   |           |               |     that SMA      |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use when      |
|                   |           |               |     sending email |
|                   |           |               |     through the   |
|                   |           |               |     Secondary     |
|                   |           |               |     SMTP server.  |
|                   |           |               | -   The user can  |
|                   |           |               |     set the value |
|                   |           |               |     for this      |
|                   |           |               |     option.       |
|                   |           |               |     -   Valid     |
|                   |           |               |         values    |
|                   |           |               |         range     |
|                   |           |               |         from 0 to |
|                   |           |               |         9999, and |
|                   |           |               |         must be   |
|                   |           |               |         positive. |
|                   |           |               |     -   If no     |
|                   |           |               |                   |
|                   |           |               |      user-defined |
|                   |           |               |         value is  |
|                   |           |               |                   |
|                   |           |               |        specified, |
|                   |           |               |         then the  |
|                   |           |               |         default   |
|                   |           |               |         port (25) |
|                   |           |               |         will be   |
|                   |           |               |         used.     |
+-------------------+-----------+---------------+-------------------+
| SMTP Notification | noreply   | Y             | -   Defines the   |
| Address           |           |               |     email address |
| (Secondary Email) |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use as the    |
|                   |           |               |     "From"      |
|                   |           |               |     address when  |
|                   |           |               |     sending       |
|                   |           |               |     E-mail or     |
|                   |           |               |     Text Messages |
|                   |           |               |     through the   |
|                   |           |               |     Secondary     |
|                   |           |               |     Email server. |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     this setting  |
|                   |           |               |     is ignored    |
|                   |           |               |     and the       |
|                   |           |               |     administrator |
|                   |           |               |     must          |
|                   |           |               |     configure the |
|                   |           |               |     SMTP          |
|                   |           |               |                   |
|                   |           |               |    Authentication |
|                   |           |               |     User and      |
|                   |           |               |     Password for  |
|                   |           |               |     the Secondary |
|                   |           |               |     Email server. |
|                   |           |               | -   If a value is |
|                   |           |               |     not           |
|                   |           |               |     specified,    |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     default to    |
|                   |           |               |     noreply.      |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     that "From" |
|                   |           |               |     address,      |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines an    |
| Authentication    |           |               |     email address |
| User (Secondary   |           |               |     for           |
| Email)            |           |               |                   |
|                   |           |               |    authentication |
|                   |           |               |     to the        |
|                   |           |               |     Secondary     |
|                   |           |               |     Email SMTP    |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here.         |
|                   |           |               | -   If a value is |
|                   |           |               |     not specified |
|                   |           |               |     when required |
|                   |           |               |     by the SMTP   |
|                   |           |               |     server, the   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     not be able   |
|                   |           |               |     to send       |
|                   |           |               |     emails or     |
|                   |           |               |     text messages |
|                   |           |               |     through the   |
|                   |           |               |     Secondary     |
|                   |           |               |     server.       |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     the user and  |
|                   |           |               |     password      |
|                   |           |               |     specified,    |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines the   |
| Authentication    |           |               |     password for  |
| Encrypted         |           |               |     the SMTP      |
| Password          |           |               |                   |
| (Secondary Email) |           |               |    Authentication |
|                   |           |               |     User for the  |
|                   |           |               |     Secondary     |
|                   |           |               |     Email server. |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here that     |
|                   |           |               |     provides the  |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the user.     |
|                   |           |               | -   To encrypt    |
|                   |           |               |     the password  |
|                   |           |               |     manually, use |
|                   |           |               |     the Password  |
|                   |           |               |     encryption    |
|                   |           |               |     tool in the   |
|                   |           |               |     Enterprise    |
|                   |           |               |     Manager. Then |
|                   |           |               |     copy and      |
|                   |           |               |     paste the     |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the value of  |
|                   |           |               |     this setting. |
|                   |           |               |     For more      |
|                   |           |               |     information,  |
|                   |           |               |     refer to      |
|                   |           |               |     [Encrypting   | |                   |           |               |                   |
|                   |           |               |    Passwords](../ |
|                   |           |               | UI/Enterprise-M |
|                   |           |               | anager/Menus.md# |
|                   |           |               | Encrypti) |
|                   |           |               |      in the |
|                   |           |               |     **Enterprise  |
|                   |           |               |     Manager**     |
|                   |           |               |     online help.  |
+-------------------+-----------+---------------+-------------------+
| SMTP              | False     | Y             | -   Determines if |
| Authentication    |           |               |     the SMA       |
| -Enable SSL       |           |               |     Notify        |
| (Secondary Email) |           |               |     Handler will  |
|                   |           |               |     use SSL       |
|                   |           |               |     encryption    |
|                   |           |               |     when          |
|                   |           |               |     connecting to |
|                   |           |               |     the Secondary |
|                   |           |               |     Email SMTP    |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires SSL  |
|                   |           |               |     Encryption,   |
|                   |           |               |     the value     |
|                   |           |               |     must be set   |
|                   |           |               |     to True.      |
+-------------------+-----------+---------------+-------------------+
| SMTP Total        | 10        | Y             | -   Determines    |
| Attachment Size   |           |               |     the maximum   |
| in MB (Secondary  |           |               |     total of MB   |
| Email)            |           |               |     in the        |
|                   |           |               |     attachments   |
|                   |           |               |     for an email  |
|                   |           |               |     attachments   |
|                   |           |               |     notification  |
|                   |           |               |     from the      |
|                   |           |               |     Secondary     |
|                   |           |               |     Email SMTP    |
|                   |           |               |     server.       |
|                   |           |               | -   This value    |
|                   |           |               |     should match  |
|                   |           |               |     the limit set |
|                   |           |               |     by the SMTP   |
|                   |           |               |     Server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP Maximum      | 50        | Y             | -   Determines    |
| Number of         |           |               |     the maximum   |
| Attachments       |           |               |     number of     |
| (Secondary Email) |           |               |     attachments   |
|                   |           |               |     allowed per   |
|                   |           |               |     email on a    |
|                   |           |               |     notification  |
|                   |           |               |     from the      |
|                   |           |               |     Secondary     |
|                   |           |               |     Email SMTP    |
|                   |           |               |     server.       |
|                   |           |               | -   This value    |
|                   |           |               |     should match  |
|                   |           |               |     the limit set |
|                   |           |               |     by the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Name  | \<blank\> | Y             | -   Defines the   |
| (Primary SMS)     |           |               |     name of the   |
|                   |           |               |     Primary SMTP  |
|                   |           |               |     server for    |
|                   |           |               |     sending SMS   |
|                   |           |               |     text          |
|                   |           |               |     messages. If  |
|                   |           |               |     this server   |
|                   |           |               |     is defined,   |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not only      |
|                   |           |               |     attempt SMS   |
|                   |           |               |     messages      |
|                   |           |               |     through the   |
|                   |           |               |     defined SMS   |
|                   |           |               |     server(s)     |
|                   |           |               |     (the email    |
|                   |           |               |     servers will  |
|                   |           |               |     only be used  |
|                   |           |               |     for email     |
|                   |           |               |     messages).    |
|                   |           |               | -   If the value  |
|                   |           |               |     is blank, the |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     try to use    |
|                   |           |               |     the Primary   |
|                   |           |               |     Email SMTP    |
|                   |           |               |     server for    |
|                   |           |               |     SMS text      |
|                   |           |               |     messages.     |
|                   |           |               | -   Default:      |
|                   |           |               |     Blank         |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Port  | 20        | Y             | -   Defines the   |
| (Primary SMS)     |           |               |     server port   |
|                   |           |               |     that SMA      |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use when      |
|                   |           |               |     sending SMS   |
|                   |           |               |     text messages |
|                   |           |               |     through the   |
|                   |           |               |     Primary SMS   |
|                   |           |               |     server.       |
|                   |           |               | -   The user can  |
|                   |           |               |     set the value |
|                   |           |               |     for this      |
|                   |           |               |     option.       |
|                   |           |               |     -   Valid     |
|                   |           |               |         values    |
|                   |           |               |         range     |
|                   |           |               |         from 0 to |
|                   |           |               |         9999, and |
|                   |           |               |         must be   |
|                   |           |               |         positive. |
|                   |           |               |     -   If no     |
|                   |           |               |                   |
|                   |           |               |      user-defined |
|                   |           |               |         value is  |
|                   |           |               |                   |
|                   |           |               |        specified, |
|                   |           |               |         then the  |
|                   |           |               |         default   |
|                   |           |               |         port (20) |
|                   |           |               |         will be   |
|                   |           |               |         used.     |
+-------------------+-----------+---------------+-------------------+
| SMTP Notification | noreply   | Y             | -   Defines the   |
| Address (Primary  |           |               |     email address |
| SMS)              |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use as the    |
|                   |           |               |     "From"      |
|                   |           |               |     address when  |
|                   |           |               |     sending SMS   |
|                   |           |               |     Text Messages |
|                   |           |               |     through the   |
|                   |           |               |     Primary SMS   |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     this setting  |
|                   |           |               |     is ignored    |
|                   |           |               |     and the       |
|                   |           |               |     administrator |
|                   |           |               |     must          |
|                   |           |               |     configure the |
|                   |           |               |     SMTP          |
|                   |           |               |                   |
|                   |           |               |    Authentication |
|                   |           |               |     User and      |
|                   |           |               |     Password for  |
|                   |           |               |     the Primary   |
|                   |           |               |     SMS server.   |
|                   |           |               | -   If a value is |
|                   |           |               |     not           |
|                   |           |               |     specified,    |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     default to    |
|                   |           |               |     noreply.      |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     that "From" |
|                   |           |               |     address,      |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines an    |
| Authentication    |           |               |     email address |
| User (Primary     |           |               |     for           |
| SMS)              |           |               |                   |
|                   |           |               |    authentication |
|                   |           |               |     to the        |
|                   |           |               |     Primary SMS   |
|                   |           |               |     SMTP server.  |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here.         |
|                   |           |               | -   If a value is |
|                   |           |               |     not specified |
|                   |           |               |     when required |
|                   |           |               |     by the SMTP   |
|                   |           |               |     server, the   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     not be able   |
|                   |           |               |     to send SMS   |
|                   |           |               |     text          |
|                   |           |               |     messages.     |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     the user and  |
|                   |           |               |     password      |
|                   |           |               |     specified,    |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines the   |
| Authentication    |           |               |     password for  |
| Encrypted         |           |               |     the SMTP      |
| Password (Primary |           |               |                   |
| SMS)              |           |               |    Authentication |
|                   |           |               |     User for the  |
|                   |           |               |     Primary SMS   |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here that     |
|                   |           |               |     provides the  |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the user.     |
|                   |           |               | -   To encrypt    |
|                   |           |               |     the password  |
|                   |           |               |     manually, use |
|                   |           |               |     the Password  |
|                   |           |               |     encryption    |
|                   |           |               |     tool in the   |
|                   |           |               |     Enterprise    |
|                   |           |               |     Manager. Then |
|                   |           |               |     copy and      |
|                   |           |               |     paste the     |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the value of  |
|                   |           |               |     this setting. |
|                   |           |               |     For more      |
|                   |           |               |     information,  |
|                   |           |               |     refer         |
|                   |           |               |     [Encrypting   | |                   |           |               |                   |
|                   |           |               |    Passwords](../ |
|                   |           |               | UI/Enterprise-M |
|                   |           |               | anager/Menus.md# |
|                   |           |               | Encrypti) |
|                   |           |               |      in the |
|                   |           |               |     **Enterprise  |
|                   |           |               |     Manager**     |
|                   |           |               |     online help.  |
+-------------------+-----------+---------------+-------------------+
| SMTP              | False     | Y             | -   Determines if |
| Authentication    |           |               |     the SMA       |
| -Enable SSL       |           |               |     Notify        |
| (Primary SMS)     |           |               |     Handler will  |
|                   |           |               |     use SSL       |
|                   |           |               |     encryption    |
|                   |           |               |     when          |
|                   |           |               |     connecting to |
|                   |           |               |     the Primary   |
|                   |           |               |     SMS SMTP      |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires SSL  |
|                   |           |               |     Encryption,   |
|                   |           |               |     the value     |
|                   |           |               |     must be set   |
|                   |           |               |     to True.      |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Name  | \<blank\> | Y             | -   Defines the   |
| (Secondary SMS)   |           |               |     name of the   |
|                   |           |               |     Secondary     |
|                   |           |               |     SMTP server   |
|                   |           |               |     for sending   |
|                   |           |               |     SMS text      |
|                   |           |               |     messages. If  |
|                   |           |               |     messages fail |
|                   |           |               |     to send       |
|                   |           |               |     through the   |
|                   |           |               |     Primary SMS   |
|                   |           |               |     server, the   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     attempt to    |
|                   |           |               |     send the      |
|                   |           |               |     message again |
|                   |           |               |     through the   |
|                   |           |               |     Secondary SMS |
|                   |           |               |     server. If    |
|                   |           |               |     the Primary   |
|                   |           |               |     SMS server is |
|                   |           |               |     not defined,  |
|                   |           |               |     this server   |
|                   |           |               |     will send SMS |
|                   |           |               |     text          |
|                   |           |               |     messages.     |
|                   |           |               | -   If the value  |
|                   |           |               |     is blank, the |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     not attempt   |
|                   |           |               |     messages      |
|                   |           |               |     through a     |
|                   |           |               |     Secondary     |
|                   |           |               |     server.       |
|                   |           |               | -   Default:      |
|                   |           |               |     Blank         |
+-------------------+-----------+---------------+-------------------+
| SMTP Server Port  | 20        | Y             | -   Defines the   |
| (Secondary SMS)   |           |               |     server port   |
|                   |           |               |     that SMA      |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use when      |
|                   |           |               |     sending SMS   |
|                   |           |               |     text messages |
|                   |           |               |     through the   |
|                   |           |               |     Secondary SMS |
|                   |           |               |     server.       |
|                   |           |               | -   The user can  |
|                   |           |               |     set the value |
|                   |           |               |     for this      |
|                   |           |               |     option.       |
|                   |           |               |     -   Valid     |
|                   |           |               |         values    |
|                   |           |               |         range     |
|                   |           |               |         from 0 to |
|                   |           |               |         9999, and |
|                   |           |               |         must be   |
|                   |           |               |         positive. |
|                   |           |               |     -   If no     |
|                   |           |               |                   |
|                   |           |               |      user-defined |
|                   |           |               |         value is  |
|                   |           |               |                   |
|                   |           |               |        specified, |
|                   |           |               |         then the  |
|                   |           |               |         default   |
|                   |           |               |         port (20) |
|                   |           |               |         will be   |
|                   |           |               |         used.     |
+-------------------+-----------+---------------+-------------------+
| SMTP Notification | noreply   | Y             | -   Defines the   |
| Address           |           |               |     email address |
| (Secondary SMS)   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     use as the    |
|                   |           |               |     "From"      |
|                   |           |               |     address when  |
|                   |           |               |     sending Text  |
|                   |           |               |     Messages      |
|                   |           |               |     through the   |
|                   |           |               |     Secondary SMS |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     this setting  |
|                   |           |               |     is ignored    |
|                   |           |               |     and the       |
|                   |           |               |     administrator |
|                   |           |               |     must          |
|                   |           |               |     configure the |
|                   |           |               |     SMTP          |
|                   |           |               |                   |
|                   |           |               |    Authentication |
|                   |           |               |     User and      |
|                   |           |               |     Password for  |
|                   |           |               |     the Secondary |
|                   |           |               |     SMS server.   |
|                   |           |               | -   If a value is |
|                   |           |               |     not           |
|                   |           |               |     specified,    |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     default to    |
|                   |           |               |     noreply.      |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     that "From" |
|                   |           |               |     address,      |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines an    |
| Authentication    |           |               |     email address |
| User (Secondary   |           |               |     for           |
| SMS)              |           |               |                   |
|                   |           |               |    authentication |
|                   |           |               |     to the        |
|                   |           |               |     Secondary SMS |
|                   |           |               |     SMTP server.  |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here.         |
|                   |           |               | -   If a value is |
|                   |           |               |     not specified |
|                   |           |               |     when required |
|                   |           |               |     by the SMTP   |
|                   |           |               |     server, the   |
|                   |           |               |     SMA Notify    |
|                   |           |               |     Handler will  |
|                   |           |               |     not be able   |
|                   |           |               |     to send text  |
|                   |           |               |     messages      |
|                   |           |               |     through a     |
|                   |           |               |     secondary     |
|                   |           |               |     server.       |
|                   |           |               | -   Customers     |
|                   |           |               |     should        |
|                   |           |               |     specify an    |
|                   |           |               |     email address |
|                   |           |               |     consistent    |
|                   |           |               |     with their    |
|                   |           |               |     domain name.  |
|                   |           |               | -   The SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler will  |
|                   |           |               |     not validate  |
|                   |           |               |     the email     |
|                   |           |               |     address       |
|                   |           |               |     specified; it |
|                   |           |               |     will only     |
|                   |           |               |     send the      |
|                   |           |               |     message with  |
|                   |           |               |     the user and  |
|                   |           |               |     password      |
|                   |           |               |     specified,    |
|                   |           |               |     leaving the   |
|                   |           |               |     validation up |
|                   |           |               |     to the SMTP   |
|                   |           |               |     server.       |
+-------------------+-----------+---------------+-------------------+
| SMTP              | \<blank\> | Y             | -   Defines the   |
| Authentication    |           |               |     password for  |
| Encrypted         |           |               |     the SMTP      |
| Password          |           |               |                   |
| (Secondary SMS)   |           |               |    Authentication |
|                   |           |               |     User for the  |
|                   |           |               |     Secondary SMS |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires      |
|                   |           |               |                   |
|                   |           |               |   authentication, |
|                   |           |               |     a value must  |
|                   |           |               |     specified     |
|                   |           |               |     here that     |
|                   |           |               |     provides the  |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the user.     |
|                   |           |               | -   To encrypt    |
|                   |           |               |     the password  |
|                   |           |               |     manually, use |
|                   |           |               |     the Password  |
|                   |           |               |     encryption    |
|                   |           |               |     tool in the   |
|                   |           |               |     Enterprise    |
|                   |           |               |     Manager. Then |
|                   |           |               |     copy and      |
|                   |           |               |     paste the     |
|                   |           |               |     encrypted     |
|                   |           |               |     password for  |
|                   |           |               |     the value of  |
|                   |           |               |     this setting. |
|                   |           |               |     For more      |
|                   |           |               |     information,  |
|                   |           |               |     refer to      |
|                   |           |               |     [Encrypting   | |                   |           |               |                   |
|                   |           |               |    Passwords](../ |
|                   |           |               | UI/Enterprise-M |
|                   |           |               | anager/Menus.md# |
|                   |           |               | Encrypti) |
|                   |           |               |      in the |
|                   |           |               |     **Enterprise  |
|                   |           |               |     Manager**     |
|                   |           |               |     online help.  |
+-------------------+-----------+---------------+-------------------+
| SMTP              | False     | Y             | -   Determines if |
| Authentication    |           |               |     the SMA       |
| -Enable SSL       |           |               |     Notify        |
| (Secondary SMS)   |           |               |     Handler will  |
|                   |           |               |     use SSL       |
|                   |           |               |     encryption    |
|                   |           |               |     when          |
|                   |           |               |     connecting to |
|                   |           |               |     the Secondary |
|                   |           |               |     SMS SMTP      |
|                   |           |               |     server.       |
|                   |           |               | -   If the SMTP   |
|                   |           |               |     server        |
|                   |           |               |     requires SSL  |
|                   |           |               |     Encryption,   |
|                   |           |               |     the value     |
|                   |           |               |     must be set   |
|                   |           |               |     to True.      |
+-------------------+-----------+---------------+-------------------+

## Notification Settings

The Notification Settings category contains configuration options for
the SMA Notify Handler.

+-------------------+-----------+---------------+-------------------+
| Option Parameter  | Default   | Dynamic (Y/N) | Description       |
+===================+:=========:+:=============:+===================+
| M                 | 150000    | Y             | -   Defines the   |
| aximumLogFileSize |           |               |     maximum size  |
| (bytes)           |           |               |     in bytes for  |
|                   |           |               |     each log      |
|                   |           |               |     file.         |
|                   |           |               | -   Determines    |
|                   |           |               |     when the      |
|                   |           |               |     current log   |
|                   |           |               |     file is       |
|                   |           |               |     closed and a  |
|                   |           |               |     new file is   |
|                   |           |               |     started. When |
|                   |           |               |     the file      |
|                   |           |               |     reaches this  |
|                   |           |               |     maximum size, |
|                   |           |               |     it is         |
|                   |           |               |     "rolled      |
|                   |           |               |     over."       |
|                   |           |               | -   This setting  |
|                   |           |               |     creates small |
|                   |           |               |     manageable    |
|                   |           |               |     log files.    |
|                   |           |               | -   SMA           |
|                   |           |               | NotifyHandler.log |
|                   |           |               |     resides in    |
|                   |           |               |     the \<Output  |
|                   |           |               |     Direct        |
|                   |           |               | ory\>\\SAM\\Log\\ |
|                   |           |               |     directory.    |
|                   |           |               |                   |
|                   |           |               | ```{=html}        |
|                   |           |               | <!-- -->          |
|                   |           |               |```               |
|                   |           |               | -   When the log  |
|                   |           |               |     file reaches  |
|                   |           |               |     the maximum   |
|                   |           |               |     size, the SMA |
|                   |           |               |     Notify        |
|                   |           |               |     Handler       |
|                   |           |               |     archives the  |
|                   |           |               |     file. The SAM |
|                   |           |               |     then          |
|                   |           |               |     maintains the |
|                   |           |               |     archive       |
|                   |           |               |     folders.      |
|                   |           |               | -   Minimum Value |
|                   |           |               |     = 50000 bytes |
|                   |           |               | -   Maximum Value |
|                   |           |               |     = 500000      |
|                   |           |               |     bytes         |
+-------------------+-----------+---------------+-------------------+
| Trace Level       | None      | Y             | -   Determines    |
|                   |           |               |     the detail of |
|                   |           |               |     debug trace   |
|                   |           |               |     logs.         |
|                   |           |               | -   Valid         |
|                   |           |               |     Selections:   |
|                   |           |               |     -   None      |
|                   |           |               |     -   Basic     |
|                   |           |               |                   |
|                   |           |               |     (non-detailed |
|                   |           |               |         trace)    |
|                   |           |               |     -   Detailed  |
|                   |           |               |     -   Very      |
|                   |           |               |         Detailed  |
|                   |           |               |         (Traces   |
|                   |           |               |         all the   |
|                   |           |               |         possible  |
|                   |           |               |         debug     |
|                   |           |               |                   |
|                   |           |               |       information |
|                   |           |               |         in the    |
|                   |           |               |                   |
|                   |           |               |     application.) |
+-------------------+-----------+---------------+-------------------+
| Include Labels in | True      | Y             | -   This          |
| Notifications     |           |               |     parameter     |
|                   |           |               |                   |
|                   |           |               |  enables/disables |
|                   |           |               |     the inclusion |
|                   |           |               |     of labels for |
|                   |           |               |     Machine Name, |
|                   |           |               |     Schedule      |
|                   |           |               |     Name, Job     |
|                   |           |               |     Name, and so  |
|                   |           |               |     forth in      |
|                   |           |               |     notification  |
|                   |           |               |     messages.     |
|                   |           |               | -   By default,   |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler       |
|                   |           |               |     includes all  |
|                   |           |               |     labels to     |
|                   |           |               |     enhance the   |
|                   |           |               |     clarity of    |
|                   |           |               |     the           |
|                   |           |               |     information.  |
|                   |           |               | -   This setting  |
|                   |           |               |     applies to    |
|                   |           |               |     all           |
|                   |           |               |     notification  |
|                   |           |               |     types         |
|                   |           |               |     [except]{.ul} | |                   |           |               |     "Text        |
|                   |           |               |     Message."    |
|                   |           |               | -   Valid values  |
|                   |           |               |     are True and  |
|                   |           |               |     False.        |
+-------------------+-----------+---------------+-------------------+
| Include Machine   | True      | Y             | -   This          |
| Name in           |           |               |     parameter     |
| Notifications     |           |               |                   |
|                   |           |               |  enables/disables |
|                   |           |               |     inclusion of  |
|                   |           |               |     the Machine   |
|                   |           |               |     Name in       |
|                   |           |               |     notification  |
|                   |           |               |     messages.     |
|                   |           |               | -   By default,   |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler       |
|                   |           |               |     includes the  |
|                   |           |               |     machine name  |
|                   |           |               |     to identify   |
|                   |           |               |     the job's    |
|                   |           |               |     machine.      |
|                   |           |               | -   This setting  |
|                   |           |               |     applies to    |
|                   |           |               |     all           |
|                   |           |               |     notification  |
|                   |           |               |     types         |
|                   |           |               |     [except]{.ul} | |                   |           |               |     "Text        |
|                   |           |               |     Message."    |
|                   |           |               | -   Valid values  |
|                   |           |               |     are True and  |
|                   |           |               |     False.        |
+-------------------+-----------+---------------+-------------------+
| Notification      | \|        | Y             | -   This          |
| Delimiter         |           |               |     parameter     |
|                   |           |               |     determines    |
|                   |           |               |     the delimiter |
|                   |           |               |     used between  |
|                   |           |               |     fields in     |
|                   |           |               |     notification  |
|                   |           |               |     messages.     |
|                   |           |               | -   This          |
|                   |           |               |     delimiter     |
|                   |           |               |     allows        |
|                   |           |               |     third-party   |
|                   |           |               |     notification  |
|                   |           |               |     tools to      |
|                   |           |               |     easier read   |
|                   |           |               |     messages.     |
|                   |           |               | -   Valid values  |
|                   |           |               |     are the tilde |
|                   |           |               |     (\~), the     |
|                   |           |               |     "at" symbol |
|                   |           |               |     (@), the      |
|                   |           |               |     exclamation   |
|                   |           |               |     mark (!), the |
|                   |           |               |     pound sign    |
|                   |           |               |     (\#), the     |
|                   |           |               |     dollar sign   |
|                   |           |               |     ($), the     |
|                   |           |               |     caret symbol  |
|                   |           |               |     (\^), and the |
|                   |           |               |     pipe symbol ( |
|                   |           |               |     \| ).         |
|                   |           |               | -   The default   |
|                   |           |               |     is the pipe   |
|                   |           |               |     symbol ( \|   |
|                   |           |               |     ).            |
+-------------------+-----------+---------------+-------------------+
| Seconds between   | 20        | Y             | -   This          |
| Checking for New  |           |               |     parameter     |
| Notifications     |           |               |     defines the   |
|                   |           |               |     delay in      |
|                   |           |               |     seconds       |
|                   |           |               |     between       |
|                   |           |               |     searches for  |
|                   |           |               |     new events in |
|                   |           |               |     the NOTIFY    |
|                   |           |               |     table.        |
|                   |           |               | -   Valid values  |
|                   |           |               |     range from 5  |
|                   |           |               |     to 20.        |
+-------------------+-----------+---------------+-------------------+
| Days to Keep      | 14        | Y             | -   Defines the   |
| Notification      |           |               |     number of     |
| History           |           |               |     days of       |
|                   |           |               |     Notification  |
|                   |           |               |     history to    |
|                   |           |               |     keep in the   |
|                   |           |               |     database.     |
|                   |           |               | -   The           |
|                   |           |               |     notification  |
|                   |           |               |     history table |
|                   |           |               |     shows the     |
|                   |           |               |     notification  |
|                   |           |               |     ID and        |
|                   |           |               |     trigger that  |
|                   |           |               |     caused each   |
|                   |           |               |     notification  |
|                   |           |               |     so users can  |
|                   |           |               |     research how  |
|                   |           |               |     a             |
|                   |           |               |     notification  |
|                   |           |               |     was           |
|                   |           |               |     generated.    |
|                   |           |               | -   Valid values  |
|                   |           |               |     range from    |
|                   |           |               |     1 - 35.       |
+-------------------+-----------+---------------+-------------------+
| Event Source for  | OPCON_ENS | Y             | -   This          |
| Windows Event Log |           |               |     parameter     |
| Messages          |           |               |     defines the   |
|                   |           |               |     event source  |
|                   |           |               |     that show up  |
|                   |           |               |     in the Source |
|                   |           |               |     column in the |
|                   |           |               |     Windows Event |
|                   |           |               |     Viewer.       |
|                   |           |               | -   Valid values  |
|                   |           |               |     are OPCON_ENS |
|                   |           |               |     or            |
|                   |           |               |                   |
|                   |           |               | SMANotifyHandler. |
+-------------------+-----------+---------------+-------------------+
| SPO Notifications | False     | Y             | -   This          |
| Enabled           |           |               |     parameter     |
|                   |           |               |                   |
|                   |           |               |  enables/disables |
|                   |           |               |     processing of |
|                   |           |               |     SPO events by |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler.      |
|                   |           |               | -   Valid values  |
|                   |           |               |     are True and  |
|                   |           |               |     False.        |
+-------------------+-----------+---------------+-------------------+
| Path and File     | \<blank\> | Y             | This parameter    |
| Name of SPO       |           |               | defines the full  |
| Executable        |           |               | path to the       |
|                   |           |               | executable        |
|                   |           |               | responsible for   |
|                   |           |               | processing SPO    |
|                   |           |               | messages.         |
+-------------------+-----------+---------------+-------------------+
| SPO Default Alarm | \<None\>  | Y             | -   This          |
| ID                |           |               |     parameter is  |
|                   |           |               |     the default   |
|                   |           |               |     machine name  |
|                   |           |               |     for SPO       |
|                   |           |               |     Events.       |
|                   |           |               | -   By default,   |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler does  |
|                   |           |               |     not send a    |
|                   |           |               |     machine name  |
|                   |           |               |     with SPO      |
|                   |           |               |     events.       |
|                   |           |               | -   The maximum   |
|                   |           |               |     is 24         |
|                   |           |               |     characters.   |
+-------------------+-----------+---------------+-------------------+
| Stack SPO Events  | True      | Y             | -   This          |
|                   |           |               |     parameter     |
|                   |           |               |                   |
|                   |           |               |  enables/disables |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler to    |
|                   |           |               |     make the      |
|                   |           |               |     ALARM         |
|                   |           |               |     qualifier     |
|                   |           |               |     unique across |
|                   |           |               |     multiple job  |
|                   |           |               |     states.       |
|                   |           |               | -   Valid values  |
|                   |           |               |     are True and  |
|                   |           |               |     False.        |
|                   |           |               |     -   If False, |
|                   |           |               |         the SMA   |
|                   |           |               |         Notify    |
|                   |           |               |         Handler   |
|                   |           |               |         sends the |
|                   |           |               |         ALARM     |
|                   |           |               |                   |
|                   |           |               |        qualifier, |
|                   |           |               |         specified |
|                   |           |               |         in the    |
|                   |           |               |                   |
|                   |           |               |     notification, |
|                   |           |               |         to SPO.   |
|                   |           |               |                   |
|                   |           |               |        Subsequent |
|                   |           |               |         status    |
|                   |           |               |         changes   |
|                   |           |               |         for the   |
|                   |           |               |         same job  |
|                   |           |               |         will      |
|                   |           |               |         overwrite |
|                   |           |               |         the       |
|                   |           |               |         previous  |
|                   |           |               |                   |
|                   |           |               |      notification |
|                   |           |               |         in SPO.   |
|                   |           |               |     -   If True,  |
|                   |           |               |         the SMA   |
|                   |           |               |         Notify    |
|                   |           |               |         Handler   |
|                   |           |               |         appends   |
|                   |           |               |         the       |
|                   |           |               |         EventID   |
|                   |           |               |         to the    |
|                   |           |               |         ALARM     |
|                   |           |               |                   |
|                   |           |               |        qualifier, |
|                   |           |               |         specified |
|                   |           |               |         in the    |
|                   |           |               |                   |
|                   |           |               |     notification, |
|                   |           |               |         to SPO.   |
|                   |           |               |                   |
|                   |           |               |        Subsequent |
|                   |           |               |         status    |
|                   |           |               |         changes   |
|                   |           |               |         for the   |
|                   |           |               |         same job  |
|                   |           |               |         will      |
|                   |           |               |         produce   |
|                   |           |               |         new       |
|                   |           |               |         unique    |
|                   |           |               |                   |
|                   |           |               |     notifications |
|                   |           |               |         to SPO.   |
+-------------------+-----------+---------------+-------------------+
| SNMP              | False     | Y             | -   This          |
| Notifications     |           |               |     parameter     |
| Enabled           |           |               |                   |
|                   |           |               |  enables/disables |
|                   |           |               |     processing of |
|                   |           |               |     SNMP events   |
|                   |           |               |     by the SMA    |
|                   |           |               |     Notify        |
|                   |           |               |     Handler.      |
|                   |           |               | -   Valid Values  |
|                   |           |               |     are True and  |
|                   |           |               |     False.        |
+-------------------+-----------+---------------+-------------------+
| Write SPO and     | True      | Y             | -   This          |
| SNMP Event        |           |               |     parameter     |
| Failures to the   |           |               |                   |
| Windows Event Log |           |               |  enables/disables |
|                   |           |               |     the SMA       |
|                   |           |               |     Notify        |
|                   |           |               |     Handler to    |
|                   |           |               |     write SNMP or |
|                   |           |               |     SPO event     |
|                   |           |               |     failures to   |
|                   |           |               |     the Windows   |
|                   |           |               |     Event Log.    |
|                   |           |               | -   Valid values  |
|                   |           |               |     are True and  |
|                   |           |               |     False.        |
+-------------------+-----------+---------------+-------------------+

## Automatic License Notifications

The Automatic License Notifications category contains settings to
determine if and how the SAM will send automatic license notifications.

:::note
SMA Technologies]{.GeneralCompanyName} [strongly recommends]{.ul} enabling automatic license notifications. If for any reason the license is compromised and this feature is not enabled, only SAM Critical log will report the problem. Notifying SMA Technologies and local OpCon administrators automatically will ensure action can be taken before the license expires.
:::

+-------------------+-----------+---------------+-------------------+
| Option Parameter  | Default   | Dynamic (Y/N) | Description       |
+===================+:=========:+:=============:+===================+
| [Send Email to    | Disabled  | Yes           | -   This          | | SMA               |           |               |     parameter     |
| Off               |           |               |     determines if |
| ice]{.GeneralSend |           |               |     SAM will      |
| EmailtoSMAOffice} |           |               |     automatically |
|                   |           |               |     send email    |
|                   |           |               |     notifications |
|                   |           |               |     to            |
|                   |           |               |     [(Undefined   | |                   |           |               |     variable:     |
|                   |           |               |     General.Comp  |
|                   |           |               | anyNameFullNameAn |
|                   |           |               | Lowercase)]{.Gene |
|                   |           |               | ralCompanyNameFul |
|                   |           |               | lNameAnLowercase} |
|                   |           |               |     office when:  |
|                   |           |               |     -   The       |
|                   |           |               |         license   |
|                   |           |               |         is        |
|                   |           |               |         expiring  |
|                   |           |               |     -   At the    |
|                   |           |               |         beginning |
|                   |           |               |         of the    |
|                   |           |               |         month,    |
|                   |           |               |         the task  |
|                   |           |               |         count     |
|                   |           |               |         report is |
|                   |           |               |         due for   |
|                   |           |               |         Task      |
|                   |           |               |         Based     |
|                   |           |               |         licensed  |
|                   |           |               |                   |
|                   |           |               |        customers. |
|                   |           |               | -   The value of  |
|                   |           |               |     Disabled will |
|                   |           |               |     disable the   |
|                   |           |               |     SAM from      |
|                   |           |               |     automatically |
|                   |           |               |     sending email |
|                   |           |               |     to [SMA       | |                   |           |               |     T             |
|                   |           |               | echnologies]{.Gen |
|                   |           |               | eralCompanyName}. |
|                   |           |               |     Instead, the  |
|                   |           |               |     SAM will      |
|                   |           |               |     write the     |
|                   |           |               |     information   |
|                   |           |               |     to the        |
|                   |           |               |     SAM.log and   |
|                   |           |               |     Critical.log  |
|                   |           |               |     files.        |
|                   |           |               | -   To enable     |
|                   |           |               |     this option,  |
|                   |           |               |     choose the    |
|                   |           |               |     [SMA          | |                   |           |               |                   |
|                   |           |               | Technologies]{.Ge |
|                   |           |               | neralCompanyName} |
|                   |           |               |     Office that   |
|                   |           |               |     provides      |
|                   |           |               |     sales and     |
|                   |           |               |     support for   |
|                   |           |               |     this site.    |
|                   |           |               | -   Valid values  |
|                   |           |               |     include:      |
|                   |           |               |     -   Disabled  |
|                   |           |               |     -   [SMA      | |                   |           |               |                   |
|                   |           |               |   France]{.Genera |
|                   |           |               | lSMAOfficeFrance} |
|                   |           |               |     -   [SMA      | |                   |           |               |                   |
|                   |           |               |   Europe]{.Genera |
|                   |           |               | lSMAOfficeEurope} |
|                   |           |               |     -   [SMA      | |                   |           |               |         USA]{.Gen |
|                   |           |               | eralSMAOfficeUSA} |
+-------------------+-----------+---------------+-------------------+
| Send Email Cc     | \<Blank\> | Yes           | -   For all       |
|                   |           |               |     customers,    |
|                   |           |               |     this          |
|                   |           |               |     parameter     |
|                   |           |               |     configures    |
|                   |           |               |     the list of   |
|                   |           |               |     email         |
|                   |           |               |     addresses     |
|                   |           |               |     that will be  |
|                   |           |               |     copied when   |
|                   |           |               |     the SAM       |
|                   |           |               |     automatically |
|                   |           |               |     sends license |
|                   |           |               |     expiration    |
|                   |           |               |     notices.      |
|                   |           |               | -   For customers |
|                   |           |               |     with a        |
|                   |           |               |     Task-based    |
|                   |           |               |     license, this |
|                   |           |               |     parameter     |
|                   |           |               |     also          |
|                   |           |               |     configures    |
|                   |           |               |     the list of   |
|                   |           |               |     email         |
|                   |           |               |     addresses     |
|                   |           |               |     that will be  |
|                   |           |               |     copied when   |
|                   |           |               |     SAM           |
|                   |           |               |     automatically |
|                   |           |               |     sends the     |
|                   |           |               |     license       |
|                   |           |               |     notification  |
|                   |           |               |     at the        |
|                   |           |               |     beginning of  |
|                   |           |               |     each month to |
|                   |           |               |     [SMA          | |                   |           |               |     T             |
|                   |           |               | echnologies]{.Gen |
|                   |           |               | eralCompanyName}. |
|                   |           |               | -   Enter one or  |
|                   |           |               |     more SMTP     |
|                   |           |               |     email         |
|                   |           |               |     addresses     |
|                   |           |               |     separated by  |
|                   |           |               |     semicolons    |
|                   |           |               |     (;).          |
+-------------------+-----------+---------------+-------------------+
| Encrypt Task      | False     | Yes           | -   For customers |
| License Report    |           |               |     with a        |
|                   |           |               |     Task-based    |
|                   |           |               |     license, this |
|                   |           |               |     parameter     |
|                   |           |               |     determines if |
|                   |           |               |     the SAM will  |
|                   |           |               |     encrypt the   |
|                   |           |               |     data for the  |
|                   |           |               |     license       |
|                   |           |               |     reports.      |
|                   |           |               | -   Valid values  |
|                   |           |               |     include       |
|                   |           |               |     True and      |
|                   |           |               |     False.        |
|                   |           |               |     -   If False, |
|                   |           |               |         the SAM   |
|                   |           |               |         will      |
|                   |           |               |         write the |
|                   |           |               |         Task      |
|                   |           |               |         License   |
|                   |           |               |                   |
|                   |           |               |       information |
|                   |           |               |         in clear  |
|                   |           |               |         text.     |
|                   |           |               |     -   If True,  |
|                   |           |               |         the SAM   |
|                   |           |               |         will      |
|                   |           |               |         write the |
|                   |           |               |         Task      |
|                   |           |               |         License   |
|                   |           |               |         Report    |
|                   |           |               |                   |
|                   |           |               |       information |
|                   |           |               |         with      |
|                   |           |               |                   |
|                   |           |               |       encryption. |
|                   |           |               |         Only [SMA | |                   |           |               |                   |
|                   |           |               | Technologies]{.Ge |
|                   |           |               | neralCompanyName} |
|                   |           |               |         will be   |
|                   |           |               |         able to   |
|                   |           |               |         decrypt   |
|                   |           |               |         and read  |
|                   |           |               |         the       |
|                   |           |               |                   |
|                   |           |               |      information. |
+-------------------+-----------+---------------+-------------------+

## Password Requirements

The Password Requirements category contains the requirements for
OpCon Login passwords.

+--------------------+---------+---------------+--------------------+
| Option Parameter   | Default | Dynamic (Y/N) | Description        |
+====================+:=======:+:=============:+====================+
| (Password cannot   | True    | N             | -   This parameter |
| be the same as the |         |               |     is a hidden,   |
| User Login ID)     |         |               |     static         |
|                    |         |               |     password       |
|                    |         |               |     requirement.   |
|                    |         |               | -   You may not    |
|                    |         |               |     set your       |
|                    |         |               |     password to    |
|                    |         |               |     match your     |
|                    |         |               |     login ID.      |
+--------------------+---------+---------------+--------------------+
| Minimum number of  | 0       | Y             | This parameter     |
| lower-case         |         |               | defines the        |
| characters         |         |               | minimum number of  |
| required           |         |               | lower-case         |
|                    |         |               | characters         |
|                    |         |               | required in a      |
|                    |         |               | password.          |
+--------------------+---------+---------------+--------------------+
| Minimum number of  | 0       | Y             | This parameter     |
| upper-case         |         |               | defines the        |
| characters         |         |               | minimum number of  |
| required           |         |               | upper-case         |
|                    |         |               | characters         |
|                    |         |               | required in a      |
|                    |         |               | password.          |
+--------------------+---------+---------------+--------------------+
| Minimum number of  | 0       | Y             | This parameter     |
| days between       |         |               | defines the        |
| password changes   |         |               | minimum number of  |
|                    |         |               | days before a user |
|                    |         |               | can change a       |
|                    |         |               | password.          |
|                    |         |               |                    |
|                    |         |               |                    |
|                    |         |               |                    |
|                    |         |               | **Note**: If the   |
|                    |         |               | value is set to 0, |
|                    |         |               | this parameter is  |
|                    |         |               | disabled.          |
+--------------------+---------+---------------+--------------------+
| Requires numeric   | False   | Y             | -   This parameter |
| characters         |         |               |     determines if  |
|                    |         |               |     the password   |
|                    |         |               |     must contain   |
|                    |         |               |     numeric        |
|                    |         |               |     characters.    |
|                    |         |               | -   Valid values   |
|                    |         |               |     are True and   |
|                    |         |               |     False.         |
+--------------------+---------+---------------+--------------------+
| Requires alpha     | False   | Y             | -   This parameter |
| characters         |         |               |     determines if  |
|                    |         |               |     the password   |
|                    |         |               |     must contain   |
|                    |         |               |     alphabetical   |
|                    |         |               |     characters.    |
|                    |         |               | -   Valid values   |
|                    |         |               |     are True and   |
|                    |         |               |     False.         |
+--------------------+---------+---------------+--------------------+
| Requires special   | False   | Y             | -   This parameter |
| characters         |         |               |     determines if  |
|                    |         |               |     the password   |
|                    |         |               |     must contain   |
|                    |         |               |     special        |
|                    |         |               |     characters.    |
|                    |         |               | -   Valid values   |
|                    |         |               |     are True and   |
|                    |         |               |     False.         |
+--------------------+---------+---------------+--------------------+
| Number of times a  | 2       | Y             | -   This parameter |
| character can      |         |               |     determines the |
| repeat             |         |               |     number of      |
| consecutively      |         |               |     times a        |
|                    |         |               |     character can  |
|                    |         |               |     repeat         |
|                    |         |               |     consecutively  |
|                    |         |               |     in a password. |
|                    |         |               |     For example,   |
|                    |         |               |     if set to 2,   |
|                    |         |               |     the password   |
|                    |         |               |     "jjj" would  |
|                    |         |               |     be invalid.    |
|                    |         |               | -   Setting the    |
|                    |         |               |     value to 0     |
|                    |         |               |     disables the   |
|                    |         |               |     setting.       |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 1   |
|                    |         |               |     to 12.         |
+--------------------+---------+---------------+--------------------+
| Number of days a   | 0       | Y             | -   This parameter |
| password is valid  |         |               |     determines the |
|                    |         |               |     number of days |
|                    |         |               |     a password is  |
|                    |         |               |     valid from the |
|                    |         |               |     time users     |
|                    |         |               |     changes their  |
|                    |         |               |     password.      |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 365.        |
|                    |         |               | -   Setting the    |
|                    |         |               |     value to 0     |
|                    |         |               |     disables the   |
|                    |         |               |     setting.       |
+--------------------+---------+---------------+--------------------+
| Number of days     | 0       | Y             | -   This parameter |
| before password    |         |               |     determines the |
| expiration to warn |         |               |     number of days |
| user               |         |               |     in advance of  |
|                    |         |               |     password       |
|                    |         |               |     expiration     |
|                    |         |               |     that the       |
|                    |         |               |     primary        |
|                    |         |               |     graphical user |
|                    |         |               |     interfaces     |
|                    |         |               |     will warn      |
|                    |         |               |     users that     |
|                    |         |               |     their password |
|                    |         |               |     is about to    |
|                    |         |               |     expire.        |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 30.         |
|                    |         |               | -   Setting the    |
|                    |         |               |     value to 0     |
|                    |         |               |     disables the   |
|                    |         |               |     setting.       |
+--------------------+---------+---------------+--------------------+
| Minimum number of  | 8       | Y             | -   This parameter |
| characters         |         |               |     defines the    |
|                    |         |               |     minimum number |
|                    |         |               |     of characters  |
|                    |         |               |     allowed for    |
|                    |         |               |     every user's  |
|                    |         |               |     password in    |
|                    |         |               |                    |
|                    |         |               |    [OpCon]{.Genera | |                    |         |               | lOpConGlobalName}. |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 1   |
|                    |         |               |     to 12.         |
+--------------------+---------+---------------+--------------------+
| Number of          | 0       | Y             | -   This parameter |
| passwords to       |         |               |     determines the |
| retain in history  |         |               |     number of      |
|                    |         |               |     passwords for  |
|                    |         |               |     [OpCon]{.Gener | |                    |         |               | alOpConGlobalName} |
|                    |         |               |     to retain in   |
|                    |         |               |     history. When  |
|                    |         |               |     a user changes |
|                    |         |               |     their          |
|                    |         |               |     password, they |
|                    |         |               |     will not be    |
|                    |         |               |     able to reuse  |
|                    |         |               |     any of the in  |
|                    |         |               |     the history.   |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 20.         |
|                    |         |               | -   Setting the    |
|                    |         |               |     value to 0     |
|                    |         |               |     disables the   |
|                    |         |               |     setting.       |
+--------------------+---------+---------------+--------------------+
| Number of failed   | 0       | Y             | -   This parameter |
| logon attempts     |         |               |     determines the |
| before account     |         |               |     number of      |
| lockout            |         |               |     password       |
|                    |         |               |     attempts       |
|                    |         |               |     before the     |
|                    |         |               |     account is     |
|                    |         |               |     locked.        |
|                    |         |               | -   Valid values   |
|                    |         |               |     range from 0   |
|                    |         |               |     to 10.         |
|                    |         |               | -   Setting the    |
|                    |         |               |     value to 0     |
|                    |         |               |     disables the   |
|                    |         |               |     setting.       |
+--------------------+---------+---------------+--------------------+

## HTML Documentation

The HTML Documentation category contains the setting for the web-based
documentation.

+-------------------+-----------+---------------+-------------------+
| Option Parameter  | Default   | Dynamic (Y/N) | Description       |
+===================+:=========:+:=============:+===================+
| Root URL for      | \<blank\> | Y             | -   Defines the   |
| Documentation     |           |               |     root URL to   |
|                   |           |               |     use to access |
|                   |           |               |     the           |
|                   |           |               |     documentation |
|                   |           |               |     from the      |
|                   |           |               |     local         |
|                   |           |               |     network.      |
|                   |           |               | -   Applications  |
|                   |           |               |     such as the   |
|                   |           |               |     Enterprise    |
|                   |           |               |     Manager (EM)  |
|                   |           |               |     use this URL  |
|                   |           |               |     to access the |
|                   |           |               |                   |
|                   |           |               |    documentation. |
|                   |           |               |     -   Any       |
|                   |           |               |         desktop   |
|                   |           |               |         having EM |
|                   |           |               |         must be   |
|                   |           |               |         able to   |
|                   |           |               |         reach     |
|                   |           |               |         this URL  |
|                   |           |               |         in order  |
|                   |           |               |         to access |
|                   |           |               |         the OpCon |
|                   |           |               |                   |
|                   |           |               |    documentation. |
+-------------------+-----------+---------------+-------------------+

## Vision Settings

The Vision category contains the settings for the Solution Manager
Vision module.

  Option Parameter                            Default   Dynamic (Y/N)  Description
  ------------------------------------------ --------- --------------- -------------------------------------------------------------------------------
  Days of Vision History to Keep               3650           Y        Defines the number of days Vision data will be retained.
  Days in Past to Trigger Vision Actions         1            Y        Defines the number of days in the past to use for triggering Vision Actions.
  Days in Future to Trigger Vision Actions       1            Y        Defines the number of days in the future to use for triggering Vision Action.
