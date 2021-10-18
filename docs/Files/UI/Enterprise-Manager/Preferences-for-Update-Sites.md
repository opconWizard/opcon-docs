---
lang: en-us
title: Setting Preferences for Update Sites
viewport: width=device-width, initial-scale=1.0
---

# Setting Preferences for Update Sites

[]{#aanchor459} The Enterprise Manager can automatically check for updates. The OpCon administrator should
define the update site(s) allowed for the environment. EM supports
update sites through an http site, FTP site, or a local network
directory.

 

+----------------------------------+----------------------------------+
| ![White triangle icon on yellow  | **CAUTION:** [If choosing a      | | circlular                        | local directory, do not place    |
| background](../../../Reso        | the Update directory inside the  |
| urces/Images/caution-icon(48x48) | directory structure for an EM    |
| .png "Caution icon") | that will be updated. If the     |
|                                  | update location will be on the   |
|                                  | SAM server, [SMA                 | |                                  | Te                               |
|                                  | chnologies]{.GeneralCompanyName} |
|                                  | recommends using a path similar  |
|                                  | to the following: C:\\EM         |
|                                  | Updates\\]           |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | [The repository will exist       | |                                  | inside this directory after      |
|                                  | extraction from the zip file     |
|                                  | provided by [SMA                 | |                                  | Technologies]{.G                 |
|                                  | eneralCompanyName}.] |
+----------------------------------+----------------------------------+

 

When the administrator receives a new version from SMA Technologies, they can update the repository
locations to distribute it to all EM installations in the network. If
database updates are also required, the administrator should update the
database before updating the EM repository.

 

  -------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ![White pencil/paper icon on gray circular background](../../../Resources/Images/note-icon(48x48).png "Note icon")   **NOTE:** [On some Windows 7 machines and Windows Servers, the automatic updates will fail because of lack of privileges on the machine. If this happens, modify the privileges on the EnterpriseManager folder to grant \"Full Control\" to \"Creator Owner,\" \"Users,\" and \"LogonUser.\"]
  -------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

![White \"person reading\" icon on blue circular background](../../../Resources/Images/moreinfo-icon(48x48).png "More Info icon")
Related Topics

-   [Updating the Repository for Update     Sites](Updating-the-Repository-for-Update-Sites.md)
-   [Managing Update Sites](Managing-Update-Sites.md)
:::

 

