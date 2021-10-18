# Adding Jobs

To add a job:

Double-click on **Job Master** under the **Administration** topic. The
**Job Master** screen displays.

Click ![Add icon](../../../Resources/Images/EM/EMadd.png "Add icon") **Add** on the
**Job Master** toolbar.

Enter a *job name* in the **Name** text box.

Ensure that the **Job Details** tab is selected in the **Job
Properties** frame.

Select a **job type** in the **Job Type** drop-down list.

[]{#Select_a_department}Select a **department** in the **[Department[[]{.MCTextPopupArrow}Defines the department name assigned
to the job.]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie
.popupBody aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
.popupHead}** drop-down list.

*(Optional)* Select the **code** in the **[Access Code[[]{.MCTextPopupArrow}Defines the Access Code name assigned to the
job.]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie .popupBody
aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
.popupHead}** drop-down list.

*(Optional)* Select the **[Allow Multi-Instance[[]{.MCTextPopupArrow}Determines if the job can have
multiple instances of the same job on the same schedule date. To request
multiple instances of a job, refer to Schedule Instance Definition or
refer to the $JOB:ADD event. To make full use of Multi-Instance jobs,
SMA Technologies recommends using Job Instance Properties. Refer to
Multi-Instance Jobs. ]{.MCTextPopupBody .MCTextPopupBody_Closed
.needs-pie .popupBody
aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
.popupHead}** checkbox. For more information, refer to [Multi-Instance Jobs](../../../operations/job-names.md#Multi-In) in
the **Concepts** online help.

Select the **[Disable Build[[]{.MCTextPopupArrow}Determines, when a build is requested, if the job's frequencies are reviewed by
SMASchedMan to refer to if it qualifies for the build date. If the value
is False (default), when a build is requested, the job's frequencies
are reviewed by SMASchedMan to refer to if it qualifies for the build
date. If the value is True, when a build is requested, SMASchedMan
ignores the job. When the value is True, the job can still be added to a
daily schedule through manually adding it or through a $JOB:ADD(HLD)
event.]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie .popupBody
aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
.popupHead}** checkbox. For more information, refer to [Disable Build](../../../objects/jobs.md#disable-build) in the **Concepts** online
help.

Select a **[primary machine[[]{.MCTextPopupArrow}Defines the name of a single machine for the job to run on. If the Primary Machine is not
available at the job's run time, the job will not be able to run unless
Alternate machines are avail-able. Additionally, if a Primary Machine is
configured, the job cannot be configured to run on a Machine
group.]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie .popupBody
aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
.popupHead}** on which to run the job.

*(Optional)* Select (in the order from 1 to 3) the
**[alternate machines[[]{.MCTextPopupArrow}Defines the names of up to three Alternate Machines for the job to run on. At run time, the SAM
checks to refer to whether the Primary Machine is available to run the
job in question. If the Primary Machine is down, the SAM attempts to run
the job on one of the Alternate Machines.]{.MCTextPopupBody
.MCTextPopupBody_Closed .needs-pie .popupBody
aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
.popupHead}** on which to run the job.

Select the **Use Schedule Instance Machine** checkbox to define the job
to run on the machine for which the Schedule Instance is built.

:::note
The **Use Schedule Instance Machine** checkbox only appears when the Schedule Properties are set for **Multi-Instance** in the **Schedule Master** (refer to the steps to [Add a Schedule](Adding-Schedules.md)). The schedule must be [configured to build an instance for all machines in a group](Defining-Schedule-Instances-for-Machines.md) and the Job Type selected for the job must match the OS Type for the Machine Group configured for the schedule.
:::

*(Optional)* Select the **[machine group[[]{.MCTextPopupArrow}Defines the name of the Machine Group the Job
will run on. If a Machine Group is configured, the job cannot be
configured to run on a Primary Machine. There are two options for how a
machine group can be applied to a job.]{.MCTextPopupBody
.MCTextPopupBody_Closed .needs-pie .popupBody
aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
.popupHead}** in the **Machine Group Selection** drop-down list.

a.  Select the **[Run on Least Tasked Machine[[]{.MCTextPopupArrow}If     this option is set, OpCon determines the least tasked machine to run
    the job on. This option is useful for Failover and Workload
    Balancing scenarios.]{.MCTextPopupBody .MCTextPopupBody_Closed
    .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** radio button to run the job on one machine in the
    group.
b.  Select the **[Run on Each Machine[[]{.MCTextPopupArrow}If this     option is set, OpCon runs the job on every machine in the group.
    When the job's schedule is built and the job qualifies for the day,
    OpCon creates a copy of the job for each machine in the group while
    assigning a specific machine to each copy of the job. The copy of
    each job is named using the following syntax: Job Name_Machine Name.
    If the job also has predefined instances, OpCon creates all
    predefined instances for each machine in the group. The copy of each
    job is named using the following syntax: Job Name_First Property
    Value_Machine Name.]{.MCTextPopupBody .MCTextPopupBody_Closed
    .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** radio button to run the job on all machines in the
    group.

:::note
Once a machine group is selected, the primary machine is cleared (if previously selected). The Machine Group selection is not available for File Transfer jobs.
:::

[]{#Enter_the_job_definition_information}Enter the **job definition information** according to the **Job Type** selected in [Step 6]{.ul}.
Click any of the following quick links to access instructions for
defining platform-specific job information:

- [Defining BIS Job     Details](Job-Type-Management.md#Defining_BIS_Job_Details)
- [Defining Container Job     Details](Job-Type-Management.md#Defining_Container_Job_Details)
- [Defining File Transfer Job     Details](Job-Type-Management.md#Defining_File_Transfer_Job_Details)
- [Defining IBM i Job     Details](Job-Type-Management.md#Defining_IBM_i_Job_Details)
- [Defining Java Job     Details](Job-Type-Management.md#Defining_Java_Job_Details)
- [Defining MCP Job     Details](Job-Type-Management.md#Define_MCP_Job_Details)
- [Defining OpenVMS Job     Details](Job-Type-Management.md#Defining_OpenVMS_Job_Details)
- [Defining OS 2200 Job     Details](Job-Type-Management.md#Defining_OS_2200_Job_Details)
- [Defining SAP BW Job     Details](Job-Type-Management.md#Defining_SAP_BW_Job_Details)
- [Defining SAP R/3 and CRM Job     Details](Job-Type-Management.md#Defining_SAP_R/3_and_CRM_Job_Details)
- [Defining SQL Job     Details](Job-Type-Management.md#Defining_SQL_Job_Details)

- [Defining Tuxedo ART Job     Details](Job-Type-Management.md#Defining_Tuxedo_Job_Details)
- [Defining UNIX Job     Details](Job-Type-Management.md#Defining_UNIX_Job_Details)
- [Defining Windows Job     Details](Job-Type-Management.md#Defining_Windows_Job_Details)
- [Defining z/OS Job     Details](Job-Type-Management.md#Defining_z/OS_Job_Details)

For more information about entering the \<Job Type\> definition
information, refer to [Job Type Management](Job-Type-Management.md).

Click ![Save icon](../../../Resources/Images/EM/EMsave.png "Save icon") **Save** on
the **Job Master** toolbar.

Click **Close ☒** (to the right of the **Job Master** tab) to close the
**Job Master** screen.
