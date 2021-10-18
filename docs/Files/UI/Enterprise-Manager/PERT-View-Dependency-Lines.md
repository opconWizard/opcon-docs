# PERT View Dependency Lines

In **[PERT](Using-PERT-View.md)** view, each dependency type is
represented by a different line style and image at the end.

+----------------------------------+----------------------------------+
| ![Requires Failed Dependency     | **Requires Failed**: By default, | | Line](../../../Resources         | a solid red line with arrow      |
| /Images/EM/EMrequiresdep3.png "R | indicates a *Requires Failed*    |
| equires Failed Dependency Line") | dependency.                      |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | For this dependency type, the    |
|                                  | following applies:               |
|                                  |                                  |
|                                  | -   The job on the end with the  |
|                                  |     arrow pointing towards it    |
|                                  |     (the selected job) has the   |
|                                  |     \"Requires\" dependency on   |
|                                  |     the job where the line       |
|                                  |     starts (the dependent job).  |
|                                  |     In other words, the          |
|                                  |     *dependent job* is the job   |
|                                  |     that the line begins and the |
|                                  |     *selected job* is the job to |
|                                  |     which the arrow points.      |
|                                  | -   The dependent job            |
|                                  |     [must]{.ul} exist in the     | |                                  |     Daily tables and [must]{.ul} |
|                                  |     fail after executing before  |
|                                  |     the selected job will run.   |
|                                  | -   If the dependent job is not  |
|                                  |     on a schedule in the Daily   |
|                                  |     tables, then the selected    |
|                                  |     job will not execute unless  |
|                                  |     it is overridden.            |
|                                  |                                  |
|                                  | **Note:**[The dependency color   | |                                  | can be changed in the Enterprise |
|                                  | Manager **Preferences** dialog.  |
|                                  | Refer to [Setting Preferences    | |                                  | for Workflow Designer and        |
|                                  | PERT](Preferences-for-       |
|                                  | Workflow-Designer.md) |
|                                  |  (complete Steps 1-4 then  |
|                                  | Steps 8 and 9).]     |
+----------------------------------+----------------------------------+
| ![Requires Finished OK           | **Requires Finished OK**: By     | | Dependency                       | default, a solid green line with |
| Line](../../../Resources/Imag    | arrow indicates a *Requires      |
| es/EM/EMrequiresdep2.png "Requir | Finished OK* dependency.         |
| es Finished OK Dependency Line") |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | For this dependency type, the    |
|                                  | following applies:               |
|                                  |                                  |
|                                  | -   The job on the end with the  |
|                                  |     arrow pointing towards it    |
|                                  |     (the selected job) has the   |
|                                  |     \"Requires\" dependency on   |
|                                  |     the job where the line       |
|                                  |     starts (the dependent job).  |
|                                  |     In other words, the          |
|                                  |     *dependent job* is the job   |
|                                  |     that the line begins and the |
|                                  |     *selected job* is the job to |
|                                  |     which the arrow points.      |
|                                  | -   The dependent job            |
|                                  |     [must]{.ul} exist in the     | |                                  |     Daily tables and [must]{.ul} |
|                                  |     complete successfully before |
|                                  |     the selected job will run.   |
|                                  | -   If the dependent job is not  |
|                                  |     on a schedule in the Daily   |
|                                  |     tables, then the selected    |
|                                  |     job will not execute unless  |
|                                  |     it is overridden.            |
|                                  |                                  |
|                                  | **Note:**[The dependency color   | |                                  | can be changed in the Enterprise |
|                                  | Manager **Preferences** dialog.  |
|                                  | Refer to [Setting Preferences    | |                                  | for Workflow Designer and        |
|                                  | PERT](Preferences-for-       |
|                                  | Workflow-Designer.md) |
|                                  |  (complete Steps 1-4 then  |
|                                  | Steps 8 and 9).]     |
+----------------------------------+----------------------------------+
| ![Requires Ignore Exit Code      | **Requires Ignore Exit Code**:   | | Dependency                       | By default, a solid black line   |
| Li                               | with arrow indicates a *Requires |
| ne](../../../Resources/Images/EM | Ignore Exit Code* dependency.    |
| /EMrequiresdep1.png "Requires Ig |                                  |
| nore Exit Code Dependency Line") |                                  |
|                                  |                                  |
|                                  | For this dependency type, the    |
|                                  | following applies:               |
|                                  |                                  |
|                                  | -   The job on the end with the  |
|                                  |     arrow pointing towards it    |
|                                  |     (the selected job) has the   |
|                                  |     \"Requires\" dependency on   |
|                                  |     the job where the line       |
|                                  |     starts (the dependent job).  |
|                                  |     In other words, the          |
|                                  |     *dependent job* is the job   |
|                                  |     that the line begins and the |
|                                  |     *selected job* is the job to |
|                                  |     which the arrow points.      |
|                                  | -   The dependent job            |
|                                  |     [must]{.ul} exist in the     | |                                  |     Daily tables. The selected   |
|                                  |     job will run when the        |
|                                  |     dependent job completes,     |
|                                  |     regardless of the exit       |
|                                  |     status.                      |
|                                  | -   If the dependent job is not  |
|                                  |     on a schedule in the Daily   |
|                                  |     tables, then the selected    |
|                                  |     job will not execute unless  |
|                                  |     it is overridden.            |
|                                  |                                  |
|                                  | **Note:**[The dependency color   | |                                  | can be changed in the Enterprise |
|                                  | Manager **Preferences** dialog.  |
|                                  | Refer to [Setting Preferences    | |                                  | for Workflow Designer and        |
|                                  | PERT](Preferences-for-       |
|                                  | Workflow-Designer.md) |
|                                  |  (complete Steps 1-4 then  |
|                                  | Steps 8 and 9).]     |
+----------------------------------+----------------------------------+
| ![After Failed Dependency        | **After Failed**: By default, a  | | Line](../../../Res               | dashed red line with arrow       |
| ources/Images/EM/EMafterdep3.png | indicates an *After Failed*      |
|  "After Failed Dependency Line") | dependency.                      |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | For this dependency type, the    |
|                                  | following applies:               |
|                                  |                                  |
|                                  | -   The job on the end with the  |
|                                  |     arrow pointing towards it    |
|                                  |     (selected job) has an        |
|                                  |     \"After\" dependency on the  |
|                                  |     job where the line starts    |
|                                  |     (dependent job). In other    |
|                                  |     words, the *dependent job*   |
|                                  |     is the job that the line     |
|                                  |     begins and the *selected     |
|                                  |     job* is the job to which the |
|                                  |     arrow points.                |
|                                  | -   If the dependent job is in   |
|                                  |     the Daily tables, then the   |
|                                  |     selected job waits until the |
|                                  |     dependent job fails to       |
|                                  |     complete successfully.       |
|                                  | -   If the dependent job is not  |
|                                  |     on a schedule in the Daily   |
|                                  |     tables, then the selected    |
|                                  |     job runs without waiting for |
|                                  |     that dependent job.          |
|                                  |                                  |
|                                  | **Note:**[The dependency color   | |                                  | can be changed in the Enterprise |
|                                  | Manager **Preferences** dialog.  |
|                                  | Refer to [Setting Preferences    | |                                  | for Workflow Designer and        |
|                                  | PERT](Preferences-for-       |
|                                  | Workflow-Designer.md) |
|                                  |  (complete Steps 1-4 then  |
|                                  | Steps 8 and 9).]     |
+----------------------------------+----------------------------------+
| ![After Finished OK Dependency   | **After Finished OK**: By        | | Line](../../../Resource          | default, a dashed green line     |
| s/Images/EM/EMafterdep2.png "Aft | with arrow indicates an *After   |
| er Finished OK Dependency Line") | Finished OK* dependency.         |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | For this dependency type, the    |
|                                  | following applies:               |
|                                  |                                  |
|                                  | -   The job on the end with the  |
|                                  |     arrow pointing towards it    |
|                                  |     (selected job) has an        |
|                                  |     \"After\" dependency on the  |
|                                  |     job where the line starts    |
|                                  |     (dependent job). In other    |
|                                  |     words, the *dependent job*   |
|                                  |     is the job that the line     |
|                                  |     begins and the *selected     |
|                                  |     job* is the job to which the |
|                                  |     arrow points.                |
|                                  | -   If the dependent job is in   |
|                                  |     the Daily tables, then the   |
|                                  |     selected job waits until the |
|                                  |     dependent job completes      |
|                                  |     successfully.                |
|                                  | -   If the dependent job is not  |
|                                  |     on a schedule in the Daily   |
|                                  |     tables, then the selected    |
|                                  |     job runs without waiting for |
|                                  |     that dependent job.          |
|                                  |                                  |
|                                  | **Note:**[The dependency color   | |                                  | can be changed in the Enterprise |
|                                  | Manager **Preferences** dialog.  |
|                                  | Refer to [Setting Preferences    | |                                  | for Workflow Designer and        |
|                                  | PERT](Preferences-for-       |
|                                  | Workflow-Designer.md) |
|                                  |  (complete Steps 1-4 then  |
|                                  | Steps 8 and 9).]     |
+----------------------------------+----------------------------------+
| ![After Ignore Exit Code         | **After Ignore Exit Code**: By   | | Dependency                       | default, a dashed black line     |
| Line](../../../Resources/Ima     | with arrow indicates an *After   |
| ges/EM/EMafterdep1.png "After Ig | Ignore Exit Code* dependency.    |
| nore Exit Code Dependency Line") |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | For this dependency type, the    |
|                                  | following applies:               |
|                                  |                                  |
|                                  | -   The job on the end with the  |
|                                  |     arrow pointing towards it    |
|                                  |     (selected job) has an        |
|                                  |     \"After\" dependency on the  |
|                                  |     job where the line starts    |
|                                  |     (dependent job). In other    |
|                                  |     words, the *dependent job*   |
|                                  |     is the job that the line     |
|                                  |     begins and the *selected     |
|                                  |     job* is the job to which the |
|                                  |     arrow points.                |
|                                  | -   If the dependent job is in   |
|                                  |     the Daily tables, then the   |
|                                  |     selected job waits until the |
|                                  |     dependent job completes,     |
|                                  |     regardless of the exit       |
|                                  |     status.                      |
|                                  | -   If the dependent job is not  |
|                                  |     on a schedule in the Daily   |
|                                  |     tables, then the selected    |
|                                  |     job runs without waiting for |
|                                  |     that dependent job.          |
|                                  |                                  |
|                                  | **Note:**[The dependency color   | |                                  | can be changed in the Enterprise |
|                                  | Manager **Preferences** dialog.  |
|                                  | Refer to [Setting Preferences    | |                                  | for Workflow Designer and        |
|                                  | PERT](Preferences-for-       |
|                                  | Workflow-Designer.md) |
|                                  |  (complete Steps 1-4 then  |
|                                  | Steps 8 and 9).]     |
+----------------------------------+----------------------------------+
| ![Resource Dependency            | **Resource Dependency**: A solid | | Line](../../../R                 | gold line with arrow indicates a |
| esources/Images/EM/EMresourcedep | *Resource* dependency. The job   |
| .png "Resource Dependency Line") | on the end with the arrow        |
|                                  | pointing towards it has a        |
|                                  | requirement for the resource     |
|                                  | where the line starts.           |
+----------------------------------+----------------------------------+
| ![Threshold Dependency           | **Threshold Dependency**: A      | | Line](../../../                  | solid royal blue line with arrow |
| Resources/Images/EM/EMthreshdep. | indicates a *Threshold*          |
| png "Threshold Dependency Line") | dependency. The job on the end   |
|                                  | with the arrow pointing towards  |
|                                  | it has a dependency on the       |
|                                  | threshold where the line starts. |
+----------------------------------+----------------------------------+
:::
