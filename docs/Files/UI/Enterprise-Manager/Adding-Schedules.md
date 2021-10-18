---
lang: en-us
title: Adding Schedules
viewport: width=device-width, initial-scale=1.0
---

#  Adding Schedules

To add a schedule:

1.  Double-click on **Schedule Master** under the **Administration**
    topic. The **Schedule Master** screen displays.
2.  Click ![](../../../Resources/Images/EM/EMadd.png) **Add** on the
    **Schedule Master** toolbar.
3.  Enter a *schedule name* in the **[Name[[]{.MCTextPopupArrow}Defines     the name of the schedule. It is suggested that the schedule name be
    descriptive of the jobs on that schedule.]{.MCTextPopupBody
    .MCTextPopupBody_Closed .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** text box.
4.  *(Optional)* Enter *any text* in the
    **[Documentation[[]{.MCTextPopupArrow}Provides an area for     descriptions, explanations, and notes that can be updated for the
    defined schedule.]{.MCTextPopupBody .MCTextPopupBody_Closed
    .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** text box.
5.  Ensure that the **Schedule** tab is in focus.
6.  *(Optional)* Enter the *time* in the **[Start     Time[[]{.MCTextPopupArrow}Provides the start time for the schedule
    and is based on a 24-hour clock. The popular choice is to leave this
    start time at midnight because all jobs on the schedule have a start
    time that is offset from the schedule start time. At the appointed
    time, the SAM will start examining the schedule to determine whether
    any jobs qualify to start. Note: For a SubSchedule, the SAM does not
    use the Start Time value to control the SubSchedule's actual start
    time. When the Container Job calling the SubSchedule qualifies to
    start, the SAM force-starts the SubSchedule. When the Start Time
    value is defined for a SubSchedule, SAM only uses the value for
    calculating the start times of the jobs on the SubSchedule. This
    provides a way for the jobs on the SubSchedule to extend beyond the
    24-hour period of the Parent schedule. ]{.MCTextPopupBody
    .MCTextPopupBody_Closed .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** text box of the **Schedule Details** frame. If start
    time is not specified, the default of 00:00 (midnight) is used.
7.  Select the **[Workdays per Week[[]{.MCTextPopupArrow}Defines the     schedule's working days. Note: The Workdays per Week setting
    directly affects all job and schedule frequencies.
    ]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** for the schedule to run.
8.  *(Optional)* Select the
    **[Multi-Instance[[]{.MCTextPopupArrow}Determines if multiple     instances of the same schedule (business process) are allowed. When
    turning this setting on, the graphical interface validates that
    there are no cross-sched-ule dependencies to this schedule
    (cross-schedule dependencies on Multi-Instance Schedule's jobs are
    invalid).]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie
    .popupBody aria-hidden="true"}](javascript:void(0)){.MCTextPopup
    .popup .popupHead}** checkbox.
9.  *(Optional)* Select the
    **[SubSchedule[[]{.MCTextPopupArrow}Determines if copies of the     schedule are allowed to be contained inside other schedules in
    OpCon. If this setting is turned on, the schedule must be called by
    a Container Job on any other schedule. When this setting is off, the
    graphical interface validates that the schedule is not being called
    by a Container Job as a SubSchedule. If the schedule is defined as a
    SubSchedule on one or more Container Jobs, the schedule must remain
    configured as a SubSchedule. When turning this setting on, the
    graphical interface validates that there are no cross-schedule
    dependencies to this schedule (cross-schedule dependencies on
    Multi-Instance Schedule's jobs are invalid).]{.MCTextPopupBody
    .MCTextPopupBody_Closed .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** checkbox.
10. *(Optional)* Select the **[Conflict with other     days[[]{.MCTextPopupArrow}Determines if a schedule is allowed to run
    if the same schedule is still run-ning on a different day. Note:
    OpCon does not support the Conflict with Other Days setting for
    SubSchedules.]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie
    .popupBody aria-hidden="true"}](javascript:void(0)){.MCTextPopup
    .popup .popupHead}** checkbox.
11. *(Optional)* Select the **[Use Master     Holiday[[]{.MCTextPopupArrow}Determines if Master Holiday Calendar
    dates will be applied to the schedule's Holiday Calendar. When
    turning this setting off, the graphical interface will present the
    option to add the master holiday dates to the schedule's holiday
    calendar before disassociating the calendar from the schedule.
    ]{.MCTextPopupBody .MCTextPopupBody_Closed .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** checkbox.
12. *(Optional)* select an **additional holiday
    calendar** in the **[Additional     Holidays[[]{.MCTextPopupArrow}Defines the name of a calendar that
    contain the specific 'Additional Holidays' to apply to the
    schedule. The default name is \<None\> (HC: Only).]{.MCTextPopupBody
    .MCTextPopupBody_Closed .needs-pie .popupBody
    aria-hidden="true"}](javascript:void(0)){.MCTextPopup .popup
    .popupHead}** drop-down list.
13. Click ![Green circle with white check mark     inside](../../../Resources/Images/EM/EMsave.png "Save icon")
    **Save** on the **Schedule Master** toolbar and click **OK**.
14. Click **Close ☒** (to the right of the **Schedule Master** tab) to
    close the **Schedule Master** screen.
:::

 

