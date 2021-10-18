---
lang: en-us
title: Escalation
viewport: width=device-width, initial-scale=1.0
---

#  Escalation

An [escalation]{.GeneralEscalatedNotification} in OpCon is a notification that has been marked
for recurring notification, with an
[escalation]{.GeneralEscalatedNotification} rule, to one or more groups of people (defined within [escalation]{.GeneralEscalatedNotification}
groups). The [escalation]{.GeneralEscalatedNotification} must be acknowledged to stop the [escalation]{.GeneralEscalatedNotification}
process. When someone acknowledges an
[escalation]{.GeneralEscalatedNotification}, this indicates to OpCon that the user read the notification.
From there, it is up to the customer to take any required action.

 

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** There are a group   | | circular                         | of critical jobs that require    |
| background](../../Reso           | immediate attention if any of    |
| urces/Images/example-icon(48x48) | them fail. To ensure the proper  |
| .png "Example icon") | action takes place, the          |
|                                  | OpCon |
|                                  | administrator sets up the        |
|                                  | following:                       |
|                                  |                                  |
|                                  | -   In Escalation Manager, the   |
|                                  |     administrator:               |
|                                  |     -   Defines three            |
|                                  |         [escalation              | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |         groups to represent      |
|                                  |         **First**, **Second**,   |
|                                  |         and **Third** level      |
|                                  |         contacts.                |
|                                  |     -   Defines an               |
|                                  |         [escalation              | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |         rule named **Three       |
|                                  |         Level** where:           |
|                                  |         -   The delay between    |
|                                  |             all repeat           |
|                                  |             notifications is set |
|                                  |             to 5 minutes.        |
|                                  |         -   The **First** group  |
|                                  |             is given 3 chances   |
|                                  |             to acknowledge the   |
|                                  |             [escalation]         | |                                  | {.GeneralEscalatedNotification}. |
|                                  |             If the               |
|                                  |             [escalation          | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |             is not acknowledge   |
|                                  |             in time, then the    |
|                                  |             **Second** group     |
|                                  |             gets notified.       |
|                                  |         -   The **Second** group |
|                                  |             is also given 3      |
|                                  |             chances to           |
|                                  |             acknowledge the      |
|                                  |             [escalation]         | |                                  | {.GeneralEscalatedNotification}. |
|                                  |             If the               |
|                                  |             [escalation          | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |             is not acknowledge   |
|                                  |             in time, then the    |
|                                  |             **Third** group gets |
|                                  |             notified.            |
|                                  |         -   The **Third** group  |
|                                  |             is given 5 chances   |
|                                  |             to acknowledge the   |
|                                  |             [escalation]         | |                                  | {.GeneralEscalatedNotification}. |
|                                  |             If the               |
|                                  |             [escalation          | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |             is not acknowledge   |
|                                  |             in time, the         |
|                                  |             [escalation          | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |             process will be      |
|                                  |             exhausted.           |
|                                  | -   In Notification Manager, the |
|                                  |     administrator:               |
|                                  |     -   Defines a Job Group with |
|                                  |         the critical jobs        |
|                                  |         included.                |
|                                  |     -   Defines a trigger on the |
|                                  |         Job Group to detect a    |
|                                  |         "Job Failed" event.    |
|                                  |     -   Defines an Email         |
|                                  |         including all the        |
|                                  |         details explaining the   |
|                                  |         action to take when any  |
|                                  |         of the jobs fail.        |
|                                  |     -   Applies the **Three      |
|                                  |         Level**                  |
|                                  |         [escalation              | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |         rule for the trigger.    |
|                                  |                                  |
|                                  | As as result of this             |
|                                  | configuration:                   |
|                                  |                                  |
|                                  | -   When any of the jobs in the  |
|                                  |     Job Group fail,              |
|                                  |     notifications will go out to |
|                                  |     the **First** level          |
|                                  |     [escalation                  | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |     group right away.            |
|                                  | -   Anyone who can see the       |
|                                  |     [escalation                  | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |     in the Escalation            |
|                                  |     Acknowledgment view in the   |
|                                  |     EM can acknowledge the       |
|                                  |     notification.                |
|                                  | -   The person who stops the     |
|                                  |     [escalation                  | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |     process should then          |
|                                  |     immediately take care of the |
|                                  |     failed job.                  |
|                                  | -   If the                       |
|                                  |     [escalation                  | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |     is not acknowledge in time,  |
|                                  |     the                          |
|                                  |     [escalation                  | |                                  | ]{.GeneralEscalatedNotification} |
|                                  |     process continues to the     |
|                                  |     **Second** and **Third**     |
|                                  |     groups.                      |
+----------------------------------+----------------------------------+
:::

 

