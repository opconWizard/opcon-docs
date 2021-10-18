---
lang: en-us
title: Configuring Automatic Schedule Maintenance
viewport: width=device-width, initial-scale=1.0
---

#  Configuring Automatic Schedule Maintenance

To configure auto maintenance:

1.  Double-click on **Schedule Master** under the **Administration**
    topic. The **Schedule Master** screen displays.
2.  Select the **schedule** in the **Schedule Selection** drop-down
    list.
3.  Ensure that the **Schedule** tab is in focus.
4.  Select the **[Auto Build[[]{.MCTextPopupArrow}Indicates if OpCon     should automatically build the schedule. When this setting is on,
    the graphical interfaces provide fields to set the number of days in
    advance to start the build and the number of days to build from that
    point forward. If auto build is enabled, the log file is named
    Auto_Build\_\<Schedule Date\>\_\<Schedule Name\>.log in the \<target
    directory\>\\OpConxps\\SAM\\Log\\SMASchedMan\\ directory on the SAM
    application server.]{.MCTextPopupBody .MCTextPopupBody_Closed
    .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** checkbox in the **Schedule Properties Build** frame.
5.  Select/enter the **number of days in advance** to auto build.
6.  Select/enter the **number of days** to auto build.
7.  *(Optional)* Select the **[Overwrite     Existing[[]{.MCTextPopupArrow}When the auto build executes and the
    schedule is found on the target date, this setting indicates if the
    schedule should be overwritten. When this setting is on, OpCon
    overwrites the schedule if it is in a Completed status. If the
    schedule is In Process, it will not be
    overwritten.]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie
    .popupBody aria-hidden="true"}](javascript:void(0)){.MCTextPopup
    .popup .popupHead}** checkbox.
8.  *(Optional)* Select the **[Build On     Hold[[]{.MCTextPopupArrow}Indicates if the schedule should be built
    with a status of \"On Hold.\" The SAM will not process the schedule
    until it is released manually or through an OpCon
    event.]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie
    .popupBody aria-hidden="true"}](javascript:void(0)){.MCTextPopup
    .popup .popupHead}** checkbox.
9.  *(Optional)* Enter an *[Auto Build     Time[[]{.MCTextPopupArrow}Defines the clock time to build the
    schedule. The default value of 00:00 will build at the time
    indicated by the Server Option setting for \"Hour of each day SAM
    should detect Schedules to build.\" To define a specific time for
    this schedule to build, change the value from 00:00 to a time that
    would be later than the Server Option for SAM\'s build time. Note:
    To enable notification for failed schedule build processes, define
    OpCon events on the SMA_SKD_BUILD job on the AdHoc schedule. SMA
    Technologies provides template jobs for AdHoc with the AdHoc.mdb
    file. ]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie
    .popupBody aria-hidden="true"}](javascript:void(0)){.MCTextPopup
    .popup .popupHead}* to define an auto build time for this schedule
    only.
10. *(Optional)* Select the **[Auto     Delete[[]{.MCTextPopupArrow}Indicates if OpCon should automatically
    delete the schedule. When this setting is on, the graphical
    interfaces provide a field to set the number of days in the past to
    delete the schedule. If a Schedule has a status of \"On Hold\" and
    has never been released, it will be deleted in the automatic delete
    process. If a schedule is \"On Hold\" after previously being
    released, it will not be deleted in the automatic delete process. If
    auto delete is enabled, the log file is named
    Auto_Delete\_\<Schedule Date\>\_\<Schedule Name\>.log in the
    \<target directory\>\\OpConxps\\SAM\\Log\\SMASchedMan\\ directory on
    the SAM application server.]{.MCTextPopupBody
    .MCTextPopupBody_Closed .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** checkbox.
11. Select/enter the **number of days ago** to delete.
12. Click ![Green circle with white checkmark     inside](../../../Resources/Images/EM/EMsave.png "Save icon")
    **Save** on the **Schedule Master** toolbar.
13. Click **Close ☒** (to the right of the **Schedule Master** tab) to
    close the **Schedule Master** screen.
:::

 

