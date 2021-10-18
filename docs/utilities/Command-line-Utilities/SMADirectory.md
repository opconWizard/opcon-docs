# SMADirectory

SMADirectory utility (SMADirectory.exe) is used to manage OpCon
directories. The utility is specifically useful for keeping log and
report directories from using too much disk space.

Based upon user criteria and filters, the utility can be used to:

- Delete files
- Zip (compress) files
- Move files (for full recursive directories)
- Recover files (for full recursive directories)

## Backwards Compatibility

This directory cleanup utility is compatible with SMADeleteOldFiles and
ClearDir. Customers who wish to convert should contact SMA Technologies.

## Requirements

The SMADirectory utility requires the following:

- Microsoft LSAM
- Microsoft .NET Framework 4.5

## Syntax

This utility supports the following types of arguments: dash, forward
slash, and comma delimited.

:::note
SMADirectory is standardized to use (US) English localization, exclusively. The utility only accepts US settings or command-line values.
:::

### Dash Argument

The SMADirectory.exe program accepts arguments using dash.

The following is an example of the command-line syntax:

SMADirectory.exe -d "c:\\Test" -r -u -e \*.\*

:::note
To get the full capability of this utility, SMA Technologies recommends using the dash (-) argument.
:::

#### Parameters

The next table identifies all the acceptable parameters for this
argument.

+-----------+----------------+-----------------+-----------------+
| Parameter | Name           | Default         | Description     |
+===========+================+=================+=================+
| -b        | Bin            | By default, the | This parameter  |
|           |                | program will    | indicates to    |
|           |                | recover the     | recover the     |
|           |                | files.          | files in the    |
|           |                |                 | default         |
|           |                |                 | location:       |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | \<d             |
|           |                |                 | riveTarget\>\\P |
|           |                |                 | rogramData\\OpC |
|           |                |                 | onxps\\MSLSAM\\ |
|           |                |                 |                 |
|           |                |                 | SMA             |
|           |                |                 | Directory\\\<di |
|           |                |                 | rectoryTarget\> |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | **Note:** If    |
|           |                |                 | you wish to set |
|           |                |                 | a custom        |
|           |                |                 | location, you   |
|           |                |                 | may do so using |
|           |                |                 | the -o switch.  |
+-----------+----------------+-----------------+-----------------+
| -B        | No Bin         |                 | This parameter  |
|           |                |                 | indicates that  |
|           |                |                 | no recovery     |
|           |                |                 | will be         |
|           |                |                 | performed.      |
|           |                |                 |                 |
|           |                |                 | -   If you      |
|           |                |                 |     enter -B    |
|           |                |                 |     (No         |
|           |                |                 |     recycle),   |
|           |                |                 |     then the    |
|           |                |                 |     program     |
|           |                |                 |     will not    |
|           |                |                 |     save a copy |
|           |                |                 |     of the      |
|           |                |                 |     directory   |
|           |                |                 |     in the      |
|           |                |                 |     default     |
|           |                |                 |     location.   |
|           |                |                 |     You may be  |
|           |                |                 |     explicit    |
|           |                |                 |     about       |
|           |                |                 |     recovery    |
|           |                |                 |     using -b    |
|           |                |                 |     (recover).  |
+-----------+----------------+-----------------+-----------------+
| -c        | Time to Retain | 5D              | This parameter  |
|           |                |                 | specifies the   |
|           |                |                 | length of time  |
|           |                |                 | that files      |
|           |                |                 | should be       |
|           |                |                 | retained within |
|           |                |                 | the timespan.   |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | The value must  |
|           |                |                 | be in the       |
|           |                |                 | following form: |
|           |                |                 |                 |
|           |                |                 | \<Numbe         |
|           |                |                 | r\>\<TimeSpan\> |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | With TimeSpan   |
|           |                |                 | represented as: |
|           |                |                 |                 |
|           |                |                 | D (day), H      |
|           |                |                 | (hour), X       |
|           |                |                 | (month), M      |
|           |                |                 | (minute), S     |
|           |                |                 | (second), or Y  |
|           |                |                 | (year)          |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | For example:    |
|           |                |                 |                 |
|           |                |                 | 5D (for 5 days) |
+-----------+----------------+-----------------+-----------------+
| -d        | Directory Name |                 | This            |
|           |                |                 | \[required\]    | |           |                |                 | parameter       |
|           |                |                 | specifies the   |
|           |                |                 | folder to be    |
|           |                |                 | cleaned up or   |
|           |                |                 | moved.          |
+-----------+----------------+-----------------+-----------------+
| -e        | Extensions     |                 | This            |
|           |                |                 | \[required\]    | |           |                |                 | parameter       |
|           |                |                 | accepts "\|" to |
|           |                |                 | separate        |
|           |                |                 | extensions and  |
|           |                |                 | / or filters.   |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | For example:    |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | .txt\|.log      |
|           |                |                 |                 |
|           |                |                 | **- or -**      |
|           |                |                 |                 |
|           |                |                 | txt \| log      |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | The program     |
|           |                |                 | also matches    |
|           |                |                 | wildcard        |
|           |                |                 | patterns as     |
|           |                |                 | follows:        |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | \*File\*.\*     |
|           |                |                 |                 |
|           |                |                 | **- or -**      |
|           |                |                 |                 |
|           |                |                 | name\*.log      |
|           |                |                 |                 |
|           |                |                 | **- or -**      |
|           |                |                 |                 |
|           |                |                 | "."           |
+-----------+----------------+-----------------+-----------------+
| -F        | TimeType       | FM              | This parameter  |
|           |                |                 | specifies the   |
|           |                |                 | time type       |
|           |                |                 | information on  |
|           |                |                 | files for       |
|           |                |                 | processing.     |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 |                 |
|           |                |                 | The available   |
|           |                |                 | values are:     |
|           |                |                 |                 |
|           |                |                 | -   FA (for     |
|           |                |                 |     last Access |
|           |                |                 |     date)       |
|           |                |                 | -   FM (for     |
|           |                |                 |     last        |
|           |                |                 |                 |
|           |                |                 |    Modification |
|           |                |                 |     date)       |
|           |                |                 | -   FC (for     |
|           |                |                 |     Creation    |
|           |                |                 |     date)       |
+-----------+----------------+-----------------+-----------------+
| -h        | No Hidden      | By default, the | This parameter  |
|           |                | program will    | specifies not   |
|           |                | process hidden  | to process      |
|           |                | and system      | system and      |
|           |                | files.          | hidden files.   |
+-----------+----------------+-----------------+-----------------+
| -m        | Move           | Null            | This parameter  |
|           |                |                 | specifies the   |
|           |                |                 | path to which a |
|           |                |                 | folder will be  |
|           |                |                 | moved.          |
|           |                |                 |                 |
|           |                |                 | -   If the -m   |
|           |                |                 |     and/or -z   |
|           |                |                 |     switches    |
|           |                |                 |     are         |
|           |                |                 |     entered,    |
|           |                |                 |     then the    |
|           |                |                 |     program     |
|           |                |                 |     will        |
|           |                |                 |     perform a   |
|           |                |                 |     move        |
|           |                |                 |     operation   |
|           |                |                 |     instead of  |
|           |                |                 |     a delete    |
|           |                |                 |     operation.  |
|           |                |                 |     -   If the  |
|           |                |                 |         zip     |
|           |                |                 |         command |
|           |                |                 |         was     |
|           |                |                 |                 |
|           |                |                 |        entered, |
|           |                |                 |         the     |
|           |                |                 |         program |
|           |                |                 |         will    |
|           |                |                 |         zip the |
|           |                |                 |         folder. |
|           |                |                 |         This    |
|           |                |                 |         case is |
|           |                |                 |         the     |
|           |                |                 |         only    |
|           |                |                 |                 |
|           |                |                 |        scenario |
|           |                |                 |         where   |
|           |                |                 |         the -x  |
|           |                |                 |                 |
|           |                |                 |        (delete) |
|           |                |                 |         switch  |
|           |                |                 |         may be  |
|           |                |                 |                 |
|           |                |                 |        entered. |
+-----------+----------------+-----------------+-----------------+
| -o        | RecoverPath    | %Program        | If recovery is  |
|           |                | Data%/OpConxps/ | on, this        |
|           |                |                 | parameter       |
|           |                | SMADirectory    | allows you to   |
|           |                |                 | specify a       |
|           |                |                 | location for a  |
|           |                |                 | recovery copy   |
|           |                |                 | of the          |
|           |                |                 | Directory to    |
|           |                |                 | process. This   |
|           |                |                 | process will    |
|           |                |                 | only recover    |
|           |                |                 | qualifying      |
|           |                |                 | files.          |
+-----------+----------------+-----------------+-----------------+
| -r        | Recursive      | The process     | This parameter  |
|           |                | does not run    | specifies to    |
|           |                | recursively.    | process         |
|           |                |                 | subfolders and  |
|           |                |                 | files under     |
|           |                |                 | subfolders.     |
+-----------+----------------+-----------------+-----------------+
| -u        | Debug          |                 | This parameter  |
|           |                |                 | places the      |
|           |                |                 | program in      |
|           |                |                 | Debug mode.     |
+-----------+----------------+-----------------+-----------------+
| -v        | Verbose        | No              | This parameter  |
|           |                |                 | to print        |
|           |                |                 | non-deleted     |
|           |                |                 | file names.     |
+-----------+----------------+-----------------+-----------------+
| -x        | Delete         | By default,     | When -m (move)  |
|           |                | moved files are | or -z (zip) is  |
|           |                | not deleted.    | specified, the  |
|           |                |                 | moved files can |
|           |                |                 | be also deleted |
|           |                |                 | by setting this |
|           |                |                 | switch.         |
|           |                |                 |                 |
|           |                |                 | -   The user    |
|           |                |                 |     can use the |
|           |                |                 |     -x command  |
|           |                |                 |     to delete   |
|           |                |                 |     the files   |
|           |                |                 |     after the   |
|           |                |                 |     move path   |
|           |                |                 |     location if |
|           |                |                 |     desired.    |
|           |                |                 |                 |
|           |                |                 | -   The -x      |
|           |                |                 |     command     |
|           |                |                 |     will delete |
|           |                |                 |     the files   |
|           |                |                 |     under the   |
|           |                |                 |     MOVE path.  |
|           |                |                 |     The -x      |
|           |                |                 |     command is  |
|           |                |                 |     useful when |
|           |                |                 |     the user    |
|           |                |                 |     only needs  |
|           |                |                 |     a zip file  |
|           |                |                 |     as the      |
|           |                |                 |     result.     |
|           |                |                 |                 |
|           |                |                 |     -   Since   |
|           |                |                 |         we move |
|           |                |                 |         the     |
|           |                |                 |         files   |
|           |                |                 |         to the  |
|           |                |                 |         MOVE    |
|           |                |                 |         PATH    |
|           |                |                 |                 |
|           |                |                 |       location, |
|           |                |                 |         then we |
|           |                |                 |         create  |
|           |                |                 |         the zip |
|           |                |                 |         file    |
|           |                |                 |         the     |
|           |                |                 |         files   |
|           |                |                 |         under   |
|           |                |                 |         the     |
|           |                |                 |         MOVE    |
|           |                |                 |         PATH    |
|           |                |                 |         can be  |
|           |                |                 |         deleted |
|           |                |                 |         using   |
|           |                |                 |         this    |
|           |                |                 |         option. |
+-----------+----------------+-----------------+-----------------+
| -z        | Zip            | By default, no  | This parameter  |
|           |                | file            | compresses      |
|           |                | compression     | (zips) the      |
|           |                | occurs.         | files moved.    |
|           |                |                 | Enter the name  |
|           |                |                 | of the zip.     |
|           |                |                 |                 |
|           |                |                 | -   If the zip  |
|           |                |                 |     command was |
|           |                |                 |     entered,    |
|           |                |                 |     the program |
|           |                |                 |     will zip    |
|           |                |                 |     the folder. |
|           |                |                 | -   This        |
|           |                |                 |     program is  |
|           |                |                 |     built with  |
|           |                |                 |     .Net 4.5    |
|           |                |                 |     for         |
|           |                |                 |     windows;    |
|           |                |                 |     therefore,  |
|           |                |                 |     the         |
|           |                |                 |     compression |
|           |                |                 |     process     |
|           |                |                 |     requires    |
|           |                |                 |     the         |
|           |                |                 |     compression |
|           |                |                 |     utility     |
|           |                |                 |     that comes  |
|           |                |                 |     with any    |
|           |                |                 |     Windows     |
|           |                |                 |     operation   |
|           |                |                 |     system.     |
|           |                |                 | -   When the    |
|           |                |                 |     user enters |
|           |                |                 |     the -z      |
|           |                |                 |     command,    |
|           |                |                 |     the user    |
|           |                |                 |     can also    |
|           |                |                 |     include the |
|           |                |                 |     -m command. |
|           |                |                 |     The user    |
|           |                |                 |     can only    |
|           |                |                 |     enter the   |
|           |                |                 |     -x command  |
|           |                |                 |     when both   |
|           |                |                 |     -m and -z   |
|           |                |                 |     are         |
|           |                |                 |     included.   |
|           |                |                 | -   The -z      |
|           |                |                 |     command     |
|           |                |                 |     requires    |
|           |                |                 |     the name of |
|           |                |                 |     the file    |
|           |                |                 |     resulted on |
|           |                |                 |     the         |
|           |                |                 |     compression |
|           |                |                 |     when there  |
|           |                |                 |     is no -m    |
|           |                |                 |                 |
|           |                |                 |  (move) command |
|           |                |                 |     entered. If |
|           |                |                 |     there is no |
|           |                |                 |     zip         |
|           |                |                 |     filename    |
|           |                |                 |     specified,  |
|           |                |                 |     then the    |
|           |                |                 |     program     |
|           |                |                 |     will use    |
|           |                |                 |     the         |
|           |                |                 |     following   |
|           |                |                 |     naming      |
|           |                |                 |     convention  |
|           |                |                 |     to set the  |
|           |                |                 |     filename:   |
|           |                |                 |                 |
|           |                |                 |  [zip.currentda | |           |                |                 | te.zip]{style=" |
|           |                |                 | font-family: 'C |
|           |                |                 | ourier New';"}. |
|           |                |                 | -   The         |
|           |                |                 |     compression |
|           |                |                 |     only occurs |
|           |                |                 |     after the   |
|           |                |                 |     Move        |
|           |                |                 |     process is  |
|           |                |                 |     completed   |
|           |                |                 |     and the     |
|           |                |                 |     files are   |
|           |                |                 |     compressed  |
|           |                |                 |     in the -m   |
|           |                |                 |     path        |
|           |                |                 |     entered by  |
|           |                |                 |     the user.   |
+-----------+----------------+-----------------+-----------------+

### Forward Slash Argument

The forward slash argument is supported for backwards compatibility with
cleardir.exe and can be used in the same way as the dash switches.

The following is an example of the command-line syntax:

SMADirectory.exe /d "c:\\Test" /r /u /e \*.\*

### Comma Delimited Argument

The comma delimited argument is supported for backwards compatibility
with the SMADeleteOldFiles and can only be used to delete files (not
move or compress them). This mode requires three (3) parameters to run
successfully.

The following command-line syntax can be used:

\<Target Directory\>\\OpConxps\\MSLSAM\\SMADirectory.exe
Directory,DaysToRetain,FileExtensions

#### Parameters

The following describes the command-line parameters:

- **\<Target Directory\>**: The path to the OpCon installation folder
    (e.g., "C:\\Program Files\").
- **Directory**: The path to the directory to examine.
- **DaysToRetain**: The number of days to keep in the directory.
  - The counter must be entered in English. For example, 5d.
  - The value must be greater than zero, but less than 32,757.
- **FileExtensions**: The file extensions to apply this retention
    period to (e.g., "log" would look for files with the log
    extension).
  - One or more file extensions can be specified (separated by
        commas).
  - The wildcard (\*) character can be specified to apply this
        retention period to all files in this directory.

#### Example

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | The following command line would | | circular                         | delete any files with an         |
| background](../../../Reso        | extension of "log" that were   |
| urces/Images/example-icon(48x48) | older than 5 days:               |
| .png "Example icon") |                                  |
|                                  | "C:\\Program                    |
|                                  | Files\\                          |
|                                  | OpConxps\\MSLSAM\\SMADirectory" |
|                                  |                                  |
|                                  | "C:\\Program                    |
|                                  | Data\\OpConxps\\SAM\\Log,5,log" |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | Notice that there is no period   |
|                                  | in front of log.                 |
+----------------------------------+----------------------------------+

## Exit Codes

The SMADirectory.exe program can exit with the following codes:

+-----------+-----------------+-----------------+-----------------+
| Exit Code | Sample Command  | Message         | Status          |
|           |                 |                 | Description     |
+===========+=================+=================+=================+
| 202       | -e              |                 | Less parameters |
+-----------+-----------------+-----------------+-----------------+
| 203       | -d C:\\Source   | \[G             | Wrong Counter   | |           | -c 20W          | etTimeCounter\] | Letter          |
|           |                 | Invalid         |                 |
|           |                 | Counter. Cannot |                 |
|           |                 | be equal or     |                 |
|           |                 | less than       |                 |
|           |                 | zero\...        |                 |
|           |                 |                 |                 |
|           |                 | \[G             |                 | |           |                 | etTimeOptions\] |                 |
|           |                 | Error while     |                 |
|           |                 | loading         |                 |
|           |                 | settings.       |                 |
+-----------+-----------------+-----------------+-----------------+
| 203       | -d C:\\Source   | \[G             | Negative        | |           | -c -5D          | etTimeCounter\] | Counter         |
|           |                 | Invalid         |                 |
|           |                 | Counter. Cannot |                 |
|           |                 | be equal or     |                 |
|           |                 | less than       |                 |
|           |                 | zero\...        |                 |
|           |                 |                 |                 |
|           |                 | \[G             |                 | |           |                 | etTimeOptions\] |                 |
|           |                 | Error while     |                 |
|           |                 | loading         |                 |
|           |                 | settings.       |                 |
+-----------+-----------------+-----------------+-----------------+
| 204       | -d C:\\Source   | \[G             | Zero Counter    | |           | -c 0D           | etTimeCounter\] |                 |
|           |                 | Invalid Counter |                 |
+-----------+-----------------+-----------------+-----------------+
| 205       | -d              | The Directory   | Directory       |
|           | C:              | does not exits  | specified is    |
|           | \\InvalidFolder |                 | invalid.        |
|           | -c 5d -e \*.\*  |                 |                 |
+-----------+-----------------+-----------------+-----------------+
| 206       | -d C:\\Source   |                 | Invalid Option. |
|           | -c5D -e \*.log  |                 | Zip File Name   |
|           | -2              |                 | is Required.    |
+-----------+-----------------+-----------------+-----------------+
| 206       | -d C:\\Source   |                 | Invalid         |
|           | -c5D            |                 | Options. The -e |
|           |                 |                 | is Required.    |
+-----------+-----------------+-----------------+-----------------+

: Exit Codes when using Dash/Forward Slash Argument

  Exit Code   Sample Command            Message                                                                                        Status Description
  ----------- ------------------------- ---------------------------------------------------------------------------------------------- ---------------------------------
  202         C:\\Source                \[Main\] Invalid number of arguments                                                           Less parameters   203         C:\\Source,5W,log         \[ParseComaDelimited\]\[SetCounter\] Invalid Counter. Cannot be equal or less than zero\....   Invalid Counter Letter
  203         C:\\Source,W,log          \[ParseComaDelimited\]\[SetCounter\] Invalid Counter. Counter is not numeric                   Counter is a letter   204         C:\\Source,0,log          \[ParseComaDelimited\]\[SetCounter\] Invalid Counter. Cannot be equal or less than zero\....   Zero Counter
  204         C:\\Source,-5,log         \[ParseComaDelimited\]\[SetCounter\] Invalid Counter. Cannot be equal or less than zero\....   Negative Counter   205         C:\\InvalidFolder,0,log   The Directory does not exits                                                                   Directory specified is invalid.
  206         -d C:\\Source,5,log       Exit Status 206                                                                                Invalid Options

  : Exit Codes when using Comma Argument
:::
