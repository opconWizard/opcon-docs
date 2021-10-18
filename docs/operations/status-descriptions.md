# Schedule and Job Status Descriptions and Allowed Status Changes

All schedules and jobs in Schedule Operations have a status. These statuses communicate what is happening and also determine what status changes are allowed.

## Schedule Statuses

The table contains definitions of OpCon schedule statuses. The last column contains permitted status changes.

+--------------------+-----------------------+-----------------------+
| Schedule Status    | Description           | Allowed Status        |
|                    |                       | Changes               |
+====================+=======================+=======================+
| Completed          | All jobs on the       | Hold                  |
|                    | schedule have         |                       |
|                    | completed and the     | Close                 |
|                    | schedule is closed.   |                       |
|                    |                       |                       |
|                    |                       |                       |
|                    |                       | **Note:** The Close   |
|                    |                       | schedule option is    |
|                    |                       | needed when there are |
|                    |                       | failed jobs in the    |
|                    |                       | schedule and the      |
|                    |                       | \'Failed jobs should  |
|                    |                       | keep the schedule     |
|                    |                       | open\' option is set  |
|                    |                       | to true (in Server    |
|                    |                       | Options). The         |
|                    |                       | schedule stays in the |
|                    |                       | status of \"In        |
|                    |                       | Process - Contains    |
|                    |                       | Failed Jobs\" in this |
|                    |                       | scenario. If all the  |
|                    |                       | jobs are actually     |
|                    |                       | completed, then the   |
|                    |                       | administrator may     |
|                    |                       | choose to close the   |
|                    |                       | schedule. This option |
|                    |                       | does not cause the    |
|                    |                       | Schedule Completion   |
|                    |                       | Events for that       |
|                    |                       | schedule to run, and  |
|                    |                       | it also keeps the     |
|                    |                       | History from being    |
|                    |                       | written for the       |
|                    |                       | Schedule Completion.  |
+--------------------+-----------------------+-----------------------+
| In Process         | One or more jobs on   | Hold                  |
|                    | the schedule have not |                       |
|                    | completed.            |                       |
+--------------------+-----------------------+-----------------------+
| On Hold            | The schedule is       | Release               |
|                    | suspended from        |                       |
|                    | processing.           |                       |
+--------------------+-----------------------+-----------------------+
| Unknown            | The SAM is unable to  | N/A                   |
|                    | determine the status  |                       |
|                    | of the schedule.      |                       |
+--------------------+-----------------------+-----------------------+
| Parent Hold        | A parent schedule one | None (The subschedule |
|                    | or more levels above  | will release when the |
|                    | the subschedule has   | parent is Released    |
|                    | been placed on Hold,  | from Hold.)           |
|                    | causing the           |                       |
|                    | SubSchedule to be     |                       |
|                    | placed on Parent      |                       |
|                    | Hold.                 |                       |
+--------------------+-----------------------+-----------------------+
| Started by User    | Indicates that a job  | Hold                  |
|                    | on the schedule was   |                       |
|                    | manually restarted by |                       |
|                    | a user and forced the |                       |
|                    | schedule back open.   |                       |
+--------------------+-----------------------+-----------------------+
| Wait to Start      | The start time of the | Hold                  |
|                    | schedule has not      |                       |
|                    | arrived or the SAM    | Start                 |
|                    | and supporting        |                       |
|                    | services (SAM-SS) are |                       |
|                    | not active.           |                       |
+--------------------+-----------------------+-----------------------+
| Wait Container Job | The Container job     | None                  |
|                    | that controls the     |                       |
|                    | subschedule has not   |                       |
|                    | started. The schedule |                       |
|                    | can only be started   |                       |
|                    | by the Container job. |                       |
+--------------------+-----------------------+-----------------------+

: Schedule Statuses and Allowed Changes

## Job Statuses

There are several general categories of job statuses. Each category
contains more specific job status descriptions. The last column contains
permitted status changes.

+----------------+----------------+----------------+----------------+
| Category       | Job Status     | Description    | Allowed Status |
|                |                |                | Changes        |
+================+================+================+================+
| Held           | On Hold        | The job is     | Release        |
|                |                | suspended from |                |
|                |                | processing.    | Start          |
|                |                |                |                |
|                |                |                | Cancel         |
|                |                |                |                |
|                |                |                | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
| Waiting        | Job to be      | When the start | Start          |
|                | Skipped        | time of the    |                |
|                |                | job arrives,   | Cancel         |
|                |                | the SAM places |                |
|                |                | it in a        | Mark Finished  |
|                |                | Skipped        | OK             |
|                |                | status. All    |                |
|                |                | subsequent     | Mark Failed    |
|                |                | jobs with a    |                |
|                |                | dependency on  | Restart (all   |
|                |                | the skipped    | commands)      |
|                |                | job will       |                |
|                |                | process        |                |
|                |                | normally.      |                |
+----------------+----------------+----------------+----------------+
|                | Late to Start  | Indicates that | Hold           |
|                |                | the time is    |                |
|                |                | now past the   | Start          |
|                |                | late to start  |                |
|                |                | time for the   | Cancel         |
|                |                | job, and the   |                |
|                |                | job has not    | Skip           |
|                |                | yet started.   |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Qualifying     | Every job      | Hold           |
|                |                | begins in this |                |
|                |                | status until   | Start          |
|                |                | the SAM        |                |
|                |                | determines its | Cancel         |
|                |                | appropriate    |                |
|                |                | status. For    | Skip           |
|                |                | information on |                |
|                |                | the way the    | Mark Finished  |
|                |                | SAM analyzes   | OK             |
|                |                | jobs to        |                |
|                |                | submit, refer  | Mark Failed    |
|                |                | to [Job        |                | |                |                | Qualification  |                |
|                |                | Proces         |                |
|                |                | s](../Server%2 |                |
|                |                | 0Programs/Sche |                |
|                |                | dule-Activit |                |
|                |                | y-Monitor.ht |                |
|                |                | m#Job) |                |
|                |                |  in the  |                |
|                |                | **Server       |                |
|                |                | Programs**     |                |
|                |                | online help.   |                |
+----------------+----------------+----------------+----------------+
|                | Prerun Failed  | The job        | Hold           |
|                |                | submitted      |                |
|                |                | contains a     | Start          |
|                |                | Prerun job and |                |
|                |                | that prerun    | Cancel         |
|                |                | reported       |                |
|                |                | failure.       | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Released       | The job has    | Hold           |
|                |                | been removed   |                |
|                |                | from a Held    | Start          |
|                |                | status.        |                |
|                |                |                | Cancel         |
|                |                |                |                |
|                |                |                | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Wait Job       | The job is     | Hold           |
|                | Conflict       | waiting for    |                |
|                |                | another job to | Start          |
|                |                | complete where |                |
|                |                | a Conflict     | Cancel         |
|                |                | Dependency     |                |
|                |                | exists.        | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Wait Job       | The job is     | Hold           |
|                | Dependency     | waiting for    |                |
|                |                | the completion | Start          |
|                |                | of another     |                |
|                |                | job.           | Cancel         |
|                |                |                |                |
|                |                |                | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Wait Start     | The job start  | Hold           |
|                | Time           | time has not   |                |
|                |                | arrived.       | Start          |
|                |                |                |                |
|                |                |                | Cancel         |
|                |                |                |                |
|                |                |                | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Wait           | The job is     | Hold           |
|                | Thre           | waiting for a  |                |
|                | shold/Resource | threshold      | Start          |
|                | Dependency     | value to be    |                |
|                |                | met or for a   | Cancel         |
|                |                | resource to    |                |
|                |                | become         | Skip           |
|                |                | available.     |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Wait           | The job is     | Hold           |
|                | Expression     | waiting for an |                |
|                | Dependency     | expression     | Start          |
|                |                | dependency to  |                |
|                |                | evaluate with  | Cancel         |
|                |                | a true result. |                |
|                |                |                | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Wait Machine   | The job is     | Hold           |
|                |                | waiting for    |                |
|                |                | the LSAM to    | Start          |
|                |                | become         |                |
|                |                | available.     | Cancel         |
|                |                | Either the     |                |
|                |                | LSAM is        | Skip           |
|                |                | processing its |                |
|                |                | maximum number | Mark Finished  |
|                |                | of jobs or     | OK             |
|                |                | SMANetCom is   |                |
|                |                | not            | Mark Failed    |
|                |                | communicating  |                |
|                |                | with the LSAM. |                |
+----------------+----------------+----------------+----------------+
|                | Wait to Start  | The job has    | Hold           |
|                |                | qualified to   |                |
|                |                | process, but   | Start          |
|                |                | is waiting for |                |
|                |                | SMANetCom to   | Cancel         |
|                |                | send the start |                |
|                |                | message to the | Skip           |
|                |                | LSAM.          |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Wait to Start; | Forces a job   | Hold           |
|                | Forced         | to start       |                |
|                |                | regardless of  | Start          |
|                |                | Job            |                |
|                |                | Dependencies   | Cancel         |
|                |                | or whether the |                |
|                |                | machine has an | Skip           |
|                |                | available job  |                |
|                |                | slot.          | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
| Running        | Attempt to     | The first step | Mark Finished  |
|                | Start          | towards        | OK             |
|                |                | starting the   |                |
|                |                | job. When the  | Mark Failed    |
| **Note:**      |                | job is sent to |                |
| Remember that  |                | the Agent, the |                |
| even though    |                | status is      |                |
| Kill is listed |                | changed to     |                |
| for all        |                | Start          |                |
| Running        |                | Attempted.     |                |
| statuses, Kill |                |                |                |
| is only valid  |                |                |                |
| for Machines   |                |                |                |
| that have      |                |                |                |
| enabled this   |                |                |                |
| feature.       |                |                |                |
+----------------+----------------+----------------+----------------+
|                | Job Running    | The LSAM has   | Kill           |
|                |                | successfully   |                |
|                |                | started the    | Mark Finished  |
|                |                | job.           | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | [Job Running;  | This status    | Mark Finished  | |                | To be          | alerts SAM to  | OK             |
|                | Terminate      | send a Kill    |                |
|                | d]{.TableText} | command to the | Mark Failed    |
|                |                | Agent. Once    |                |
|                |                | sent, the Job  |                |
|                |                | reverts back   |                |
|                |                | to a Job       |                |
|                |                | Running status |                |
|                |                | until          |                |
|                |                | confirmation   |                |
|                |                | is received    |                |
|                |                | from the Agent |                |
|                |                | that the job   |                |
|                |                | was killed.    |                |
+----------------+----------------+----------------+----------------+
|                | Late to Finish | Indicates that | Kill           |
|                |                | the time is    |                |
|                |                | now past the   | Mark Finished  |
|                |                | late to finish | OK             |
|                |                | time for the   |                |
|                |                | job to finish, | Mark Failed    |
|                |                | and the job is |                |
|                |                | still running. |                |
+----------------+----------------+----------------+----------------+
|                | Prerun Active  | The LSAM has   | Kill           |
|                |                | successfully   |                |
|                |                | started the    | Mark Finished  |
|                |                | prerun job.    | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Start          | The SAM has    | Kill           |
|                | Attempted      | submitted the  |                |
|                |                | job (via       | Mark Finished  |
|                |                | SMANetCom) to  | OK             |
|                |                | the LSAM for   |                |
|                |                | processing.    | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Still          | The SAM has    | Kill           |
|                | Attempting     | submitted the  |                |
|                | Start          | job (via       | Mark Finished  |
|                |                | SMANetCom) to  | OK             |
|                |                | the LSAM for   |                |
|                |                | processing,    | Mark Failed    |
|                |                | and waited the |                |
|                |                | \"number of    |                |
|                |                | minutes        |                |
|                |                | between        |                |
|                |                | checking       |                |
|                |                | running jobs\" |                |
|                |                | and found the  |                |
|                |                | job to still   |                |
|                |                | be in a Start  |                |
|                |                | Attempted      |                |
|                |                | status.        |                |
+----------------+----------------+----------------+----------------+
| Cancelled      | Cancelled      | The job has    | Restart (all   |
|                |                | been disabled  | commands)      |
|                |                | and will not   |                |
|                |                | be processed   |                |
|                |                | unless         |                |
|                |                | manually       |                |
|                |                | restarted. The |                |
|                |                | job            |                |
|                |                | dependencies   |                |
|                |                | of all         |                |
|                |                | subsequent     |                |
|                |                | jobs will      |                |
|                |                | [not]{.ul} be  |                | |                |                | met.           |                |
+----------------+----------------+----------------+----------------+
| Missed Start   | Missed Start   | The latest     | Start          |
| Time           | Time           | start time for |                |
|                |                | the job has    | Cancel         |
|                |                | passed.        |                |
|                |                |                | Skip           |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
| Skipped        | Skipped        | The job is     | Restart (all   |
|                |                | cancelled and  | commands)      |
|                |                | the job        |                |
|                |                | dependency of  |                |
|                |                | all subsequent |                |
|                |                | jobs will be   |                |
|                |                | met.           |                |
+----------------+----------------+----------------+----------------+
| Finished OK    | Finished OK    | The job has    | Restart (all   |
|                |                | completed      | commands)      |
|                |                | successfully.  |                |
|                |                |                | Mark Failed    |
+----------------+----------------+----------------+----------------+
|                | Marked         | A user placed  | Restart (all   |
|                | Finished OK    | the job in a   | commands)      |
|                |                | Finished OK    |                |
|                |                | status.        | Mark Failed    |
+----------------+----------------+----------------+----------------+
| Failed         | Initialization | The LSAM       | Restart (all   |
|                | Error          | attempted to   | commands)      |
|                |                | start the job, |                |
|                |                | but received   | Mark Finished  |
|                |                | an error from  | OK             |
|                |                | the operating  |                |
|                |                | system or the  | Mark Failed    |
|                |                | LSAM failed    |                |
|                |                | the            | Cancel         |
|                |                | pre-submission |                |
|                |                | editing        | Skip           |
|                |                | process (e.g., |                |
|                |                | missing        |                |
|                |                | required       |                |
|                |                | fields).       |                |
+----------------+----------------+----------------+----------------+
|                | Failed         | The job ended  | Cancel         |
|                |                | with an error. |                |
|                |                |                | Restart (all   |
|                |                |                | commands)      |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Skip           |
+----------------+----------------+----------------+----------------+
|                | Marked Failed  | A user placed  | Cancel         |
|                |                | the job in a   |                |
|                |                | Failed status. | Restart (all   |
|                |                |                | commands)      |
|                |                |                |                |
|                |                |                | Mark Finished  |
|                |                |                | OK             |
|                |                |                |                |
|                |                |                | Skip           |
+----------------+----------------+----------------+----------------+
| Under Review   | Under Review   | A user placed  | Mark Failed    |
|                |                | the job in an  |                |
|                |                | Under Review   | Failed         |
|                |                | status to      |                |
|                |                | indicate that  | Initialization |
|                |                | the job is     | Error          |
|                |                | being          |                |
|                |                | reviewed.      |                |
+----------------+----------------+----------------+----------------+
| Fixed          | Fixed          | A user placed  | Mark Failed    |
|                |                | the job in a   |                |
|                |                | Fixed state to | Failed         |
|                |                | indicate that  |                |
|                |                | the job is     | Initialization |
|                |                | considered     | Error          |
|                |                | fixed.         |                |
|                |                |                | Under Review   |
+----------------+----------------+----------------+----------------+

: Job Statuses and Allowed Changes
:::
