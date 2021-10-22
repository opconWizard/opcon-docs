# Adding Schedule Completion Events

To add a new schedule completion event:

Double-click on **Schedule Master** under the **Administration** topic.
The **Schedule Master** screen displays.

Select the **schedule** in the **Schedule** drop-down list.

Click on the **Events** tab in the **Schedule Details** frame.

Click the **Add** button. The **Event Definition Wizard** displays.

Select an [OpCon]{.GeneralOpConGlobalName style="font-weight: bold;"} **event template** from the **Event Template** drop-down list. For more
information, refer to the [OpCon Events](../../../events/introduction.md) online help.

  --------------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------
  ![White pencil icon on green circular background](../../../Resources/Images/example-icon(48x48).png "Example icon")   **EXAMPLE:** [$JOB:ADD,\<schedule date\>,\<schedule name\>,\<job name\>,\<frequency name\>]{.statement2}
  --------------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------

[]{#Place_your_mouse_cursor}Place your mouse cursor at the beginning of a **\<syntax placeholder\>** displayed in the **Event Parameters** text
box then drag the cursor to the right to select the entire syntax
placeholder, excluding any surrounding commas. For example: ,[\<schedule name\>]{style="background-color: #1e90ff; color: #ffffff;"}, .

Replace the selected syntax placeholder with valid
OpCon event information.

If you wish to replace the syntax placeholder with a token, then do the
following:

Follow [Step 6]{.ul} to select the syntax placeholder.

Click the ![Insert Token buton](../../../Resources/Images/EM/EMinserttoken.png "Insert Token button")
**Insert token** button or press **Ctrl/t** on the keyboard to list
available global properties.

Locate the global property in the selector by:

i.  Scrolling to it.
ii. Using the search field and filter criteria to find it. You can use
    Windows wildcard characters in the search field to expand the search
    and filter the search by property name, property value, or both
    (default).

Double-click on the **global property** (e.g., $SCHEDULE DATE).

:::note
Double brackets will automatically be placed around the placeholder for the token that is defined.
:::

  --------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------
  ![White pencil icon on green circular background](../../../Resources/Images/example-icon(48x48).png "Example icon")   **EXAMPLE:** [$JOB:ADD,\[\[$SCHEDULE DATE\]\],Payroll,Emp1,15thofMonth]{.statement2}
  --------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------

Click **Reset** to reset the parameters to their original states.

Click **Finish** to save changes or click **Cancel** to discard the
changes made in the wizard.

Click **Close ☒** (to the right of the **Schedule Master** tab) to close
the **Schedule Master** screen.
