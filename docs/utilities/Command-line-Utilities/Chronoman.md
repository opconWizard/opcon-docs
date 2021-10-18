# Chronoman

:::note
The information presented in this topic pertains largely to running the Chronoman utility as a Windows job. For instructions on running this utility in the OpCon Docker container, please refer to [Running on OpCon in Docker](#Running).
:::

OpCon user-defined properties can be updated
with calculated dates using an executable called Chronoman
(Chronoman.exe). The SAM can calculate simple dates based on calendar
offsets from the \$SCHEDULE DATE or \$DATE; however, Chronoman is used
to make complex date calculations (e.g., a property may need to be
updated with the date of the last working day of the month).

Chronoman.exe is installed in the \<Target
Directory\>\\OpConxps\\MSLSAM\\ directory. Chronoman should be scheduled
using a Windows OpCon job. Any jobs requiring
the property value should be dependent on the associated Chronoman job.
For information on setting up job dependencies, refer to [Adding Job Dependencies](../../Files/UI/Enterprise-Manager/Adding-Job-Dependencies.md)
 in the **Enterprise Manager** online help.

## Configuration

To configure Chronoman, update the Chronoman configuration file
(Chronoman.ini) and set up the DSN information.

### Configuration File Settings

The Chronoman configuration file (Chronoman.ini) is used to configure
the utility.

+----------------+----------+----------------------------------------+
| Setting        | Default  | Definition                             |
+================+==========+========================================+
| PathToMsgInDir | .\\MSGIN | -   Location of the MSGIN directory of |
|                |          |     the Microsoft LSAM.                |
|                |          | -   Chronoman uses this directory to   |
|                |          |     communicate any errors to the SAM. |
+----------------+----------+----------------------------------------+
| PathToLogDir   | .\\Log   | -   The directory to which Chronoman   |
|                |          |     logs errors.                       |
|                |          | -   The default directory is the Log   |
|                |          |     subdirectory below the             |
|                |          |     installation directory.            |
+----------------+----------+----------------------------------------+

: Chronoman Configuration: General Settings

+---------+-----------+----------------------------------------------+
| Setting | Default   | Definition                                   |
+=========+===========+==============================================+
| Q1      | \<blank\> | -   Defines the first day of the First       |
|         |           |     Fiscal Quarter.                          |
|         |           | -   Specify the date with the Month and Day  |
|         |           |     to start. The date must match the syntax |
|         |           |     recognized by the regional settings of   |
|         |           |     the user running the utility. Do not     |
|         |           |     define the year. Chronoman automatically |
|         |           |     calculates the year each time it         |
|         |           |     executes based Fiscal the current Fiscal |
|         |           |     year.                                    |
+---------+-----------+----------------------------------------------+
| Q2      | \<blank\> | -   Defines the first day of the Second      |
|         |           |     Fiscal Quarter.                          |
|         |           | -   Specify the date with the Month and Day  |
|         |           |     to start. The date must match the syntax |
|         |           |     recognized by the regional settings of   |
|         |           |     the user running the utility. Do not     |
|         |           |     define the year. Chronoman automatically |
|         |           |     calculates the year each time it         |
|         |           |     executes based Fiscal the current Fiscal |
|         |           |     year.                                    |
+---------+-----------+----------------------------------------------+
| Q3      | \<blank\> | -   Defines the first day of the Third       |
|         |           |     Fiscal Quarter.                          |
|         |           | -   Specify the date with the Month and Day  |
|         |           |     to start. The date must match the syntax |
|         |           |     recognized by the regional settings of   |
|         |           |     the user running the utility. Do not     |
|         |           |     define the year. Chronoman automatically |
|         |           |     calculates the year each time it         |
|         |           |     executes based Fiscal the current Fiscal |
|         |           |     year.                                    |
+---------+-----------+----------------------------------------------+
| Q4      | \<blank\> | -   Defines the first day of the Fourth      |
|         |           |     Fiscal Quarter.                          |
|         |           | -   Specify the date with the Month and Day  |
|         |           |     to start. The date must match the syntax |
|         |           |     recognized by the regional settings of   |
|         |           |     the user running the utility. Do not     |
|         |           |     define the year. Chronoman automatically |
|         |           |     calculates the year each time it         |
|         |           |     executes based Fiscal the current Fiscal |
|         |           |     year.                                    |
+---------+-----------+----------------------------------------------+

: Chronoman Configuration: Fiscal Quarter Begin Dates

### Configuration File Example

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | Here is an example showing       | | circular                         | updated configuration file       |
| background](../../../Reso        | settings. For the dates with     |
| urces/Images/example-icon(48x48) | Regional settings configured to  |
| .png "Example icon") | use English (United States), the |
|                                  | Fiscal Q1 begins on July 1, Q2   |
|                                  | begins on October 1, Q3 begins   |
|                                  | on January 1, and Q4 begins on   |
|                                  | April 1.                         |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | \[General\]                      | |                                  |                                  |
|                                  | PathToMsgInDir=.\\MSGIN          |
|                                  |                                  |
|                                  | PathToLogDir=.\\Log              |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | \[Fiscal Quarter Begin Dates\]   | |                                  |                                  |
|                                  | Q1=07/01                         |
|                                  |                                  |
|                                  | Q2=10/01                         |
|                                  |                                  |
|                                  | Q3=01/01                         |
|                                  |                                  |
|                                  | Q4=04/01                         |
+----------------------------------+----------------------------------+

## Command-line Syntax

Chronoman uses the following command-line syntax:

chronoman =t\<Property Name\> =o\<Sign\>\<Number\> =u\<unit\>
=f\<format\> \[=b\<Date and Time\>\]\[=c\<File Path\>\]\[=j\< Julian Date and Time\>\]\[=n\<Date and
Time\>\]\[=s\<Schedule\>\]\[=z\<insertion_point, desired_length_of_string\>\] ↵

:::note
The wrapping of the syntax in this document does not indicate the location of a carriage return; the ↵ indicates the location of a carriage return. Parameters always begin with the equals sign (=).
:::

### Required Parameters

+-----------+---------------------------------------------------------+
| Parameter | Description                                             |
+===========+=========================================================+
| =f        | This parameter is the output format to use when         |
|           | updating the property. For valid date format            |
|           | characters, refer to [System                            | |           | Pr                                                      |
|           | operties](../../objects/properties.md#System) |
|           |  in the **Concepts** online help. The format      |
|           | parameter can be omitted if the format is defined in    |
|           | the command file (=c).                                  |
+-----------+---------------------------------------------------------+
| =o        | This parameter is the plus (+) or minus (-) the number  |
|           | of units by which to change the base time. Do           |
|           | [not]{.ul} use the offset parameter if a command file   | |           | (=c) is specified. If it has been specified, the        |
|           | command file contains the required date manipulations.  |
+-----------+---------------------------------------------------------+
| =t        | -   This parameter is the name of the property to set.  |
|           |     Do not specify any of the system properties         |
|           |     (including managed system properties).              |
|           | -   The property name must conform to the rules for     |
|           |     User -defined Property names. For more information, |
|           |     refer to                                            |
|           |     [Prop                                               | |           | erties](../../objects/properties.md#Defining) |
|           |      in the **Concepts** online help.             |
|           | -   If the property does not exist in the database,     |
|           |     Chronoman will automatically create it.             |
|           | -   The property parameter can be omitted if the        |
|           |     property name is defined in the command file (=c).  |
|           | -   If specifying the property name with the =t switch  |
|           |     and the property name requires quotes (\") because  |
|           |     it contains a period (.), escape the quotes with a  |
|           |     backslash (\\) on the command line.                 |
+-----------+---------------------------------------------------------+
| =u        | This parameter is the type of unit to use with the      |
|           | offset parameter (=o). Refer to the [Chronoman Offset   | |           | Parameters](#Chronoma2) table for valid  |
|           | units of offset. Do not use the units of offset if a    |
|           | command file (=c) is specified. If it has been          |
|           | specified, the command file contains the required date  |
|           | manipulations. The characters below are valid for the   |
|           | units of offset (=u). Only WD should be upper case. All |
|           | other characters should be lower case.                  |
+-----------+---------------------------------------------------------+

### Chronoman Offset Parameters

  Units of Offset   Definition
  ----------------- ----------------------
  yyyy              Year
  q                 Quarter
  m                 Month
  y                 Day of year (Julian)
  d                 Day
  w                 Weekday
  ww                Week
  h                 Hours
  n                 Minutes
  s                 Seconds
  WD                Working days

### Optional Parameters

+-----------+---------------------------------------------------------+
| Parameter | Description                                             |
+===========+=========================================================+
| =b        | This parameter is the base date on which to calculate   |
|           | the value for the property. The date is formatted using |
|           | the syntax recognized by the regional settings of the   |
|           | user running the utility.                               |
|           |                                                         |
|           | -   If the =b parameter is not specified and the format |
|           |     (=f) contains months, days, and years, the current  |
|           |     date and time is used.                              |
|           | -   When specifying a value for the =b parameter, the   |
|           |     SMA Technologies recommends  | |           |     using a date format of one of the following:        |
|           |     -   For default English locale: **mmm/dd/yyyy** or  |
|           |         **mm/dd/yyyy**                                  |
|           |     -   For default Dutch or French locales:            |
|           |         **dd/mmm/yyyy** or **dd/mm/yyyy**               |
|           |     -   For default Greek locale: **dd/mm/yyyy**        |
|           | -   Do [not]{.ul} specify =j and =b together.           | +-----------+---------------------------------------------------------+
| =c        | This parameter is the path to the command file. If the  |
|           | =c parameter is specified, do [not]{.ul} specify =o or  | |           | =u. If it has been specified, the command file contains |
|           | the required date manipulations.                        |
+-----------+---------------------------------------------------------+
| =j        | This parameter is the base date in Julian format on     |
|           | which to calculate the output for the property. The     |
|           | format parameter (=f) must be set to YYYYy. If the =j   |
|           | parameter is not specified and the format (=f)          |
|           | specifies Julian, current Julian date and time is used. |
|           | Do [not]{.ul} specify =j and =b together.               | +-----------+---------------------------------------------------------+
| =n        | This parameter is the name of the Negative Annual Plan  |
|           | Calendar. In addition to the Holiday Calendar,          |
|           | Chronoman includes the Negative Annual Plan dates to    |
|           | determine non-working days.                             |
+-----------+---------------------------------------------------------+
| =s        | This parameter is the name of the schedule to use if    |
|           | the \<units of offset\> are WD (Working Days) or if a   |
|           | command file computes working days. Chronoman uses the  |
|           | schedule\'s Holiday Calendar to determine non-working   |
|           | days. The schedule parameter can be omitted if a        |
|           | command file is specified and the command file defines  |
|           | the name of the schedule prior to performing a          |
|           | calculation requiring Working Days. This parameter is   |
|           | not needed if Working Days are not calculated.          |
+-----------+---------------------------------------------------------+
| =z        | This parameter is the final formatting of the string    |
|           | done by padding it with zeros. Specify the column where |
|           | leading zeros should be inserted and the length the     |
|           | string should be. The insertion point must be between 1 |
|           | and the current length of the string.                   |
|           |                                                         |
|           |                                                         |
|           |                                                         |
|           | **Syntax:** Insertion_point,desired_length_of_string    |
+-----------+---------------------------------------------------------+

### Command-line Example

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** [chronoman          | | circular                         | =tTestProperty =o-1 =uh =fmmddyy |
| background](../../../Reso        | hh:nn =b09/15/2017               |
| urces/Images/example-icon(48x48) | 05:00]{.statement2               |
| .png "Example icon") | styl                             |
|                                  | e="font-family: 'Courier New';"} |
|                                  |                                  |
|                                  | -   This example changes the     |
|                                  |     value of a token called      |
|                                  |     TestProperty.                |
|                                  | -   The value of the property is |
|                                  |     the base time (09/15/2017    |
|                                  |     05:00) plus the offset (-1)  |
|                                  |     hour.                        |
|                                  | -   The property is in the       |
|                                  |     format \"mmddyy hh:nn\".     |
|                                  | -   When the calculation is      |
|                                  |     complete, TestProperty has a |
|                                  |     value of 091517 04:00.       |
+----------------------------------+----------------------------------+

## Command File Syntax

The command file is an ASCII text file containing date manipulations.
The date manipulations are in the form of one or more lines of
directives on how to modify the base time. The first directive is
executed on the base time. Successive directives are executed on the
computed date from the previous directive.

:::note
Command file directives override the equivalent command-line parameters if both are specified. The exception to this is the *units of offset* and *offset* must be specified in either the command file or on the command line. An error is generated if a conflict is found.
:::

The basic format for the command file is: [\<Units of offset\>]{style="font-family: 'Courier New';"},
[\<offset\>]{style="font-family: 'Courier New';"}

- **\<Units of offset\>**: This field is the type of unit to use with
    the offset parameter. Refer to [Chronoman Offset     Parameters](#Chronoma2).
- **\<offset\>**: This field is a positive or negative integer.

If special calculations on the date are required, the following syntax
is also supported:

\<Special Directive\>, \<argument if applicable\>

### Special Directives

There are several special directives that allow for necessary date/time
control.

+-------------------------------+-------------------------------------+
| Special Directive             | Description                         |
+===============================+=====================================+
| COMPUTE_ELAPSED_DAYS          | -   Computes the number of elapsed  |
|                               |     days between the base time and  |
|                               |     the computed date from all      |
|                               |     prior directives.               |
|                               | -   The format (=f) must be         |
|                               |     specified as an integer, not a  |
|                               |     date. If this directive is      |
|                               |     used, it must be the last one   |
|                               |     in the command file.            |
|                               | -   The computation is not accurate |
|                               |     if any directives follow        |
|                               |     COMPUTE_ELAPSED_DAYS.           |
+-------------------------------+-------------------------------------+
| FILL_DIRECTIVE                | -   Inserts characters into the     |
|                               |     computed date to achieve the    |
|                               |     desired final format for the    |
|                               |     property.                       |
|                               | -   Specify the character to be     |
|                               |     inserted, where characters      |
|                               |     should be inserted, and the     |
|                               |     desired length of the string.   |
|                               | -   The insertion point can be      |
|                               |     specified past the length of    |
|                               |     the computed date.              |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q1_BEGIN        | -   The date is set to the first    |
|                               |     day of the first quarter of the |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q1_BEGIN  |
|                               |     would set the date to January 1 |
|                               |     of the current calendar year.   |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q1_END          | -   The date is set to the last day |
|                               |     of the first quarter of the     |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q1_END    |
|                               |     would set the date to March 31  |
|                               |     of the current calendar year.   |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q2_BEGIN        | -   The date is set to the first    |
|                               |     day of the second quarter of    |
|                               |     the year for the computed date  |
|                               |     from all previous steps.        |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q2_BEGIN  |
|                               |     would set the date to April 1   |
|                               |     of the current calendar year.   |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q2_END          | -   The date is set to the last day |
|                               |     of the second quarter of the    |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q2_END    |
|                               |     would set the date to June 30   |
|                               |     of the current calendar year.   |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q3_BEGIN        | -   The date is set to the first    |
|                               |     day of the third quarter of the |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q3_BEGIN  |
|                               |     would set the date to July 1 of |
|                               |     the current calendar year.      |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q3_END          | -   The date is set to the last day |
|                               |     of the third quarter of the     |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q3_END    |
|                               |     would set the date to September |
|                               |     30 of the current calendar      |
|                               |     year.                           |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q4_BEGIN        | -   The date is set to the first    |
|                               |     day of the fourth quarter of    |
|                               |     the year for the computed date  |
|                               |     from all previous steps.        |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q4_BEGIN  |
|                               |     would set the date to October 1 |
|                               |     of the current calendar year.   |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_Q4_END          | -   The date is set to the last day |
|                               |     of the fourth quarter of the    |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_Q3_END    |
|                               |     would set the date to December  |
|                               |     31 of the current calendar      |
|                               |     year.                           |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_QUARTER_BEGIN   | -   The date is set to the first    |
|                               |     day of the quarter for the      |
|                               |     computed date from all previous |
|                               |     steps.                          |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25,                         |
|                               |     FIND_CALENDAR_QUARTER_BEGIN     |
|                               |     would set the date to April 1   |
|                               |     of the current calendar year.   |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_QUARTER_END     | -   The date is set to the last day |
|                               |     of the quarter for the computed |
|                               |     date from all previous steps.   |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25,                         |
|                               |     FIND_CALENDAR_QUARTER_END would |
|                               |     set the date to June 30 of the  |
|                               |     current calendar year.          |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_YEAR_BEGIN      | -   The date is set to the first    |
|                               |     day of the year for the         |
|                               |     computed date from all previous |
|                               |     steps.                          |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25,                         |
|                               |     FIND_CALENDAR_YEAR_BEGIN would  |
|                               |     set the date to January 1 of    |
|                               |     the computed date\'s current    |
|                               |     year.                           |
+-------------------------------+-------------------------------------+
| FIND_CALENDAR_YEAR_END        | -   The date is set to the last day |
|                               |     of the year for the computed    |
|                               |     date from all previous steps.   |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_CALENDAR_YEAR_END  |
|                               |     would set the date to December  |
|                               |     31 of the computed date\'s      |
|                               |     current year.                   |
+-------------------------------+-------------------------------------+
| FIND_DAY_OF_WEEK_BACKWARD     | -   Finds the date of the first     |
|                               |     occurrence of the specified day |
|                               |     of the week prior to the        |
|                               |     computed date.                  |
|                               | -   If the computed date from all   |
|                               |     previous steps matches the      |
|                               |     specified day of week,          |
|                               |     processing stops and the date   |
|                               |     is used in future steps (or     |
|                               |     returned).                      |
|                               | -   If the computed date does not   |
|                               |     match the day of week, the date |
|                               |     is decremented and tested until |
|                               |     the day of week specified is    |
|                               |     found.                          |
|                               | -   A day of week argument must be  |
|                               |     passed to this directive.       |
|                               | -   Day of Week arguments range     |
|                               |     from 1 to 7 (i.e., Sunday to    |
|                               |     Saturday).                      |
+-------------------------------+-------------------------------------+
| FIND_DAY_OF_WEEK_FORWARD      | -   Finds the date of the first     |
|                               |     occurrence of the specified day |
|                               |     of the week after the computed  |
|                               |     date.                           |
|                               | -   If the computed date from all   |
|                               |     previous steps matches the      |
|                               |     specified day of week,          |
|                               |     processing stops and the date   |
|                               |     is used in future steps (or     |
|                               |     returned).                      |
|                               | -   If the computed date does not   |
|                               |     match the day of week, the date |
|                               |     is incremented and tested until |
|                               |     the day of week specified is    |
|                               |     found.                          |
|                               | -   A day of week argument must be  |
|                               |     passed as an argument to this   |
|                               |     directive.                      |
|                               | -   Day of Week arguments range     |
|                               |     from 1 to 7 (i.e., Sunday to    |
|                               |     Saturday).                      |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_QUARTER_BEGIN     | -   The date is set to the first    |
|                               |     day of the fiscal quarter for   |
|                               |     the computed date from all      |
|                               |     previous steps.                 |
|                               | -   The date for the first day of   |
|                               |     each fiscal quarter must be     |
|                               |     defined in the Chronoman.ini    |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q1   |
|                               |     begin date is set to July 1 in  |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was August 3,         |
|                               |     FIND_FISCAL_QUARTER_BEGIN would |
|                               |     set the date to July 1 of the   |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_QUARTER_END       | -   The date is set to the last day |
|                               |     of the fiscal quarter for the   |
|                               |     computed date from all previous |
|                               |     steps.                          |
|                               | -   The date for the first day of   |
|                               |     each fiscal quarter must be     |
|                               |     defined in the Chronoman.ini    |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q1   |
|                               |     begin date is set to July 1 in  |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was August 3,         |
|                               |     FIND_FISCAL_QUARTER_END would   |
|                               |     set the date to September 30 of |
|                               |     the current fiscal year.        |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q1_BEGIN          | -   The date is set to the first    |
|                               |     day of the first fiscal quarter |
|                               |     of the year for the computed    |
|                               |     date from all previous steps.   |
|                               | -   The date for the first day of   |
|                               |     the first fiscal quarter must   |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q1   |
|                               |     begin date is set to July 1 in  |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was June 3,           |
|                               |     FIND_FISCAL_Q1_BEGIN would set  |
|                               |     the date to July 1 of the       |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q1_END            | -   The date is set to the last day |
|                               |     of the first fiscal quarter of  |
|                               |     the year for the computed date  |
|                               |     from all previous steps.        |
|                               | -   The date for the first day of   |
|                               |     the first fiscal quarter must   |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q1   |
|                               |     begin date is set to July 1 in  |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was June 3,           |
|                               |     FIND_FISCAL_Q1_END would set    |
|                               |     the date to September 30 of the |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q2_BEGIN          | -   The date is set to the first    |
|                               |     day of the second fiscal        |
|                               |     quarter of the year for the     |
|                               |     computed date from all previous |
|                               |     steps.                          |
|                               | -   The date for the first day of   |
|                               |     the second fiscal quarter must  |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to Refer to         |
|                               |     [Configuration File             | |                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q2   |
|                               |     begin date is set to October 1  |
|                               |     in the Chornoman.ini file and   |
|                               |     the base date was June 3,       |
|                               |     FIND_FISCAL_Q2_BEGIN would set  |
|                               |     the date to October 1 of the    |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q2_END            | -   The date is set to the last day |
|                               |     of the second quarter of the    |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   The date for the first day of   |
|                               |     the second fiscal quarter must  |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q2   |
|                               |     begin date is set to October 1  |
|                               |     in the Chornoman.ini file and   |
|                               |     the base date was June 3,       |
|                               |     FIND_FISCAL_Q2_END would set    |
|                               |     the date to December 31 of the  |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q3_BEGIN          | -   The date is set to the first    |
|                               |     day of the third quarter of the |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   The date for the first day of   |
|                               |     the third fiscal quarter must   |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q3   |
|                               |     begin date is set to January 1  |
|                               |     in the Chornoman.ini file and   |
|                               |     the base date was June 3,       |
|                               |     FIND_FISCAL_Q3_BEGIN would set  |
|                               |     the date to January 1 of the    |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q3_END            | -   The date is set to the last day |
|                               |     of the third quarter of the     |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   The date for the first day of   |
|                               |     the third fiscal quarter must   |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q3   |
|                               |     begin date is set to January 1  |
|                               |     in the Chornoman.ini file and   |
|                               |     the base date was June 3,       |
|                               |     FIND_FISCAL_Q3_END would set    |
|                               |     the date to March 31 of the     |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q4_BEGIN          | -   The date is set to the first    |
|                               |     day of the fourth quarter of    |
|                               |     the year for the computed date  |
|                               |     from all previous steps.        |
|                               | -   The date for the first day of   |
|                               |     the fourth fiscal quarter must  |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q4   |
|                               |     begin date is set to April 1 in |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was June 3,           |
|                               |     FIND_FISCAL_Q4_BEGIN would set  |
|                               |     the date to April 1 of the      |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_Q4_END            | -   The date is set to the last day |
|                               |     of the fourth quarter of the    |
|                               |     year for the computed date from |
|                               |     all previous steps.             |
|                               | -   The date for the first day of   |
|                               |     the fourth fiscal quarter must  |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q4   |
|                               |     begin date is set to April 1 in |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was June 3,           |
|                               |     FIND_FISCAL_Q4_END would set    |
|                               |     the date to June 30 of the      |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_YEAR_BEGIN        | -   The date is set to the first    |
|                               |     day of the first fiscal quarter |
|                               |     for the computed date from all  |
|                               |     previous steps.                 |
|                               | -   The date for the first day of   |
|                               |     the first fiscal quarter must   |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q1   |
|                               |     begin date is set to July 1 in  |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was February 3,       |
|                               |     FIND_FISCAL_YEAR_BEGIN would    |
|                               |     set the date to July 1 of the   |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_FISCAL_YEAR_END          | -   The date is set to the last day |
|                               |     of the fourth fiscal quarter    |
|                               |     for the computed date from all  |
|                               |     previous steps.                 |
|                               | -   The date for the first day of   |
|                               |     the fourth fiscal quarter must  |
|                               |     be defined in the Chronoman.ini |
|                               |     file. Refer to [Configuration   | |                               |     File                            |
|                               |     Settings](#Configur2)   |
|                               |     .                         |
|                               | -   For example, if the Fiscal Q4   |
|                               |     begin date is set to April 1 in |
|                               |     the Chornoman.ini file and the  |
|                               |     base date was August 3,         |
|                               |     FIND_FISCAL_YEAR_END would set  |
|                               |     the date to June 30 of the      |
|                               |     current fiscal year.            |
+-------------------------------+-------------------------------------+
| FIND_MONTH_BEGIN              | -   The date is set to the first    |
|                               |     day of the month for the        |
|                               |     computed date from all previous |
|                               |     steps.                          |
|                               | -   For example, if the base date   |
|                               |     was June 3 and previous         |
|                               |     directives moved the date to    |
|                               |     May 25, FIND_MONTH_BEGIN would  |
|                               |     set the date to May 1.          |
+-------------------------------+-------------------------------------+
| FIND_MONTH_END                | -   The date is set to the last day |
|                               |     of the month for the computed   |
|                               |     date from all previous steps.   |
|                               | -   For example, if the base date   |
|                               |     was June 29 and previous        |
|                               |     directives moved the date to    |
|                               |     July 3, FIND_MONTH_END would    |
|                               |     set the date to July 31.        |
+-------------------------------+-------------------------------------+
| FIND_WORKING_DAY_BACKWARD     | -   Finds the date of the first     |
|                               |     working day prior to the        |
|                               |     computed date if it is not a    |
|                               |     working day.                    |
|                               | -   If the computed date from all   |
|                               |     previous steps is a working     |
|                               |     date, processing stops and the  |
|                               |     date is used in future steps    |
|                               |     (or returned).                  |
|                               | -   If the computed date is not a   |
|                               |     working date, the date is       |
|                               |     decremented and tested until a  |
|                               |     working date is found.          |
+-------------------------------+-------------------------------------+
| FIND_WORKING_DAY_FORWARD      | -   Finds the date of the first     |
|                               |     working day after the computed  |
|                               |     date if it is not a working     |
|                               |     day.                            |
|                               | -   If the computed date from all   |
|                               |     prior steps is a working date,  |
|                               |     processing stops and the date   |
|                               |     is used in future steps (or     |
|                               |     returned).                      |
|                               | -   If the computed date is not a   |
|                               |     working date, the date is       |
|                               |     incremented and tested until a  |
|                               |     working date is found.          |
+-------------------------------+-------------------------------------+
| SET_COMPUTED_DATE             | -   The calculated date value can   |
|                               |     be overridden at any time by    |
|                               |     setting its value explicitly or |
|                               |     to the value of a property.     |
|                               | -   Chronoman can only resolve      |
|                               |     user-defined.                   |
|                               | -   Chronoman cannot resolve any    |
|                               |     System or user-defined System.  |
+-------------------------------+-------------------------------------+
| SET_COMPUTED_DATE_JULIAN      | -   The calculated date value can   |
|                               |     be overridden at any time by    |
|                               |     setting its value explicitly or |
|                               |     to the value of a property.     |
|                               | -   The format of the date must be  |
|                               |     YYYYy.                          |
+-------------------------------+-------------------------------------+
| SET_FORMAT_STRING             | -   The output format for the       |
|                               |     computed date.                  |
|                               | -   This directive is the same as   |
|                               |     the =f parameter on the command |
|                               |     line.                           |
|                               | -   The output format string MUST   |
|                               |     be specified either in the      |
|                               |     command file or on the command  |
|                               |     line.                           |
+-------------------------------+-------------------------------------+
| SET_NEGATIVE_ANNUAL_PLAN_NAME | -   The name of the Negative Annual |
|                               |     Plan calendar to be used when   |
|                               |     determining non-working days.   |
+-------------------------------+-------------------------------------+
| SET_SCHEDULE_NAME             | -   The name of the schedule to be  |
|                               |     used when determining working   |
|                               |     days.                           |
|                               | -   This directive is the same as   |
|                               |     the =s parameter on the command |
|                               |     line.                           |
|                               | -   The schedule name MUST be       |
|                               |     specified either in the command |
|                               |     file or on the command line if  |
|                               |     working days are to be          |
|                               |     calculated.                     |
+-------------------------------+-------------------------------------+
| SET_TOKEN_NAME                | -   The name of the property to     |
|                               |     update with the computed date.  |
|                               | -   This directive is the same as   |
|                               |     the =t parameter on the command |
|                               |     line.                           |
|                               | -   If specifying a property name   |
|                               |     that contains a period (.),     |
|                               |     surround the name with double   |
|                               |     quotes. For Example:            |
|                               | -   The property name MUST be       |
|                               |     specified either in the command |
|                               |     file or on the command line.    |
+-------------------------------+-------------------------------------+
| ZERO_FILL_DIRECTIVE           | -   Inserts zeros into the computed |
|                               |     date to achieve the desired     |
|                               |     final format for the property.  |
|                               | -   Specify the character where     |
|                               |     zeros should be inserted and    |
|                               |     the desired length of the       |
|                               |     string.                         |
|                               | -   The insertion point must be     |
|                               |     between 1 and the current       |
|                               |     length of the string.           |
|                               | -   The first directive of this     |
|                               |     command file takes the base     |
|                               |     date/time and adds two days.    |
|                               | -   The second directive advances   |
|                               |     the computed date to the next   |
|                               |     Thursday.                       |
|                               | -   The last directive computes the |
|                               |     number of days elapsed between  |
|                               |     the base date and the computed  |
|                               |     date.                           |
|                               | -   The property is updated with    |
|                               |     the value of elapsed days.      |
+-------------------------------+-------------------------------------+

: Chronoman Special Directive

This next table shows the command line/command file equivalency. In the
table, the **R/O** column header represents \"Required/Optional\".

+-------------------+-------------------+-----+-------------------+
| Command-line      | Command File      | R/O | Comments/Defaults |
| Parameter         | Directive         |     |                   |
+===================+===================+=====+===================+
| =b                | N/A               | O   | Current date in   |
|                   |                   |     | the format of the |
|                   |                   |     | Regional          |
|                   |                   |     | Settings.         |
+-------------------+-------------------+-----+-------------------+
| =c                | N/A               | O   | Do not specify =o |
|                   |                   |     | and =u            |
|                   |                   |     | command-line      |
|                   |                   |     | parameters if =c  |
|                   |                   |     | is specified.     |
+-------------------+-------------------+-----+-------------------+
| =f                | SET_FORMAT_STRING | R   | Command file      |
|                   |                   |     | overrides command |
|                   |                   |     | line.             |
+-------------------+-------------------+-----+-------------------+
| =j                | N/A               | O   | Current date in   |
|                   |                   |     | Julian format.    |
+-------------------+-------------------+-----+-------------------+
| =n                | SET_NEGATIVE      | O   | None              |
|                   |_ANNUAL_PLAN_NAME |     |                   |
+-------------------+-------------------+-----+-------------------+
| =o                | \<offset\>        | O   | -   Entered after |
|                   |                   |     |     \<units of    |
|                   |                   |     |     offset\> in   |
|                   |                   |     |     the command   |
|                   |                   |     |     file.         |
|                   |                   |     | -   Do not        |
|                   |                   |     |     specify =o    |
|                   |                   |     |     parameter if  |
|                   |                   |     |     \<offset\> is |
|                   |                   |     |     in the        |
|                   |                   |     |     command file. |
+-------------------+-------------------+-----+-------------------+
| =s                | SET_SCHEDULE_NAME | O   | Command file      |
|                   |                   |     | overrides command |
|                   |                   |     | line.             |
+-------------------+-------------------+-----+-------------------+
| =t                | SET_TOKEN_NAME    | R   | Command file      |
|                   |                   |     | overrides command |
|                   |                   |     | line.             |
+-------------------+-------------------+-----+-------------------+
| =u                | \<units of        | O   | -   Entered       |
|                   | offset\>          |     |     before        |
|                   |                   |     |     \<offset\> in |
|                   |                   |     |     the command   |
|                   |                   |     |     file.         |
|                   |                   |     | -   Do not        |
|                   |                   |     |     specify =u    |
|                   |                   |     |     parameter if  |
|                   |                   |     |     \<units of    |
|                   |                   |     |     offset\> is   |
|                   |                   |     |     in the        |
|                   |                   |     |     command file. |
+-------------------+-------------------+-----+-------------------+
| =z                | ZE                | O   | Command file      |
|                   | RO_FILL_DIRECTIVE |     | overrides command |
|                   |                   |     | line.             |
+-------------------+-------------------+-----+-------------------+
| N/A               | COM               | O   | Must be the last  |
|                   | PUTE_ELAPSED_DAYS |     | directive in the  |
|                   |                   |     | command file.     |
+-------------------+-------------------+-----+-------------------+
| N/A               | FILL_DIRECTIVE    | O   | None              |
+-------------------+-------------------+-----+-------------------+
| N/A               | FIND_DAY          | O   | None              |
|                   | _OF_WEEK_BACKWARD |     |                   |
+-------------------+-------------------+-----+-------------------+
| N/A               | FIND_DA           | O   | None              |
|                   | Y_OF_WEEK_FORWARD |     |                   |
+-------------------+-------------------+-----+-------------------+
| N/A               | FIND_MONTH_BEGIN  | O   | None              |
+-------------------+-------------------+-----+-------------------+
| N/A               | FIND_MONTH_END    | O   | None              |
+-------------------+-------------------+-----+-------------------+
| N/A               | FIND_WOR          | O   | None              |
|                   | KING_DAY_BACKWARD |     |                   |
+-------------------+-------------------+-----+-------------------+
| N/A               | FIND_WO           | O   | None              |
|                   | RKING_DAY_FORWARD |     |                   |
+-------------------+-------------------+-----+-------------------+
| N/A               | SET_COMPUTED_DATE | O   | None              |
+-------------------+-------------------+-----+-------------------+
| N/A               | SET_COM           | O   | None              |
|                   | PUTED_DATE_JULIAN |     |                   |
+-------------------+-------------------+-----+-------------------+

: Chronoman Command Line/Command File Equivalency

Arguments in the command file can be represented by tokens. Chronoman
can resolve only tokens referencing user-defined properties. Chronoman
cannot resolve any System or user-defined System tokens.

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** A property could be | | circular                         | created called DAYS_BEFORE_CLOSE |
| background](../../../Reso        | with a value of -3. If it were   |
| urces/Images/example-icon(48x48) | decided to start the period      |
| .png "Example icon") | close processing four days       |
|                                  | early, only this value would     |
|                                  | need to be changed. To calculate |
|                                  | the actual date for this value,  |
|                                  | assuming that closing occurs on  |
|                                  | the last work day of a month,    |
|                                  | the command file would contain:  |
|                                  |                                  |
|                                  | FIND_MONTH_END                   |
|                                  |                                  |
|                                  | FIND_WORKING_DAY_BACKWARD        |
|                                  |                                  |
|                                  | WD,\[\[DAYS_BEFORE_CLOSE\]\]     | +----------------------------------+----------------------------------+

### Command File Examples

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **SCENARIO 1:** If today is a    | | circular                         | working day, set the property to |
| background](../../../Reso        | today\'s date. If today is NOT a |
| urces/Images/example-icon(48x48) | working day, set the property to |
| .png "Example icon") | the date of the next working     |
|                                  | day.                             |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **OpCon Command Line**:          |
|                                  |                                  |
|                                  | \"C:\\Program                    |
|                                  | File                             |
|                                  | s\\Opconxps\\MSLSAM\\Chronoman\" |
|                                  | =t\\\"WK.Day\\\" =cC:\\Chronoman |
|                                  | Files\\WkDayCommand.txt          |
|                                  | =sTestSchedule                   |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Chronoman Command File**:      |
|                                  |                                  |
|                                  | SET_FORMAT_STRING,mmddyy\        |
|                                  | FIND_WORKING_DAY_FORWARD         |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Summary**: The base date of    |
|                                  | today is assumed because it is   |
|                                  | not specified on the command     |
|                                  | line or in the command file. The |
|                                  | property to be updated is called |
|                                  | WK.Day. The schedule to be used  |
|                                  | for determining working days is  |
|                                  | called \"TestSchedule\".         |
|                                  |                                  |
|                                  | -   The WK.Day property is       |
|                                  |     surrounded with escaped      |
|                                  |     quotes in the =t parameter   |
|                                  |     on the command line because  |
|                                  |     the name contains a period.  |
|                                  | -   [SET_FORMAT_STRING]{styl     | |                                  | e="font-family: 'Courier New';"} |
|                                  |     specifies the format for     |
|                                  |     output to the property as a  |
|                                  |     date format using numbers    |
|                                  |     only.                        |
|                                  | -                                |
|                                  |  [FIND_WORKING_DAY_FORWARD]{styl | |                                  | e="font-family: 'Courier New';"} |
|                                  |     uses the value of the        |
|                                  |     computed date if it is a     |
|                                  |     workday, otherwise the next  |
|                                  |     workday is found to arrive   |
|                                  |     at the final value for the   |
|                                  |     property.                    |
+----------------------------------+----------------------------------+

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **SCENARIO 2:** Set the property | | circular                         | to the date of the first day     |
| background](../../../Reso        | after the next working day.      |
| urces/Images/example-icon(48x48) |                                  |
| .png "Example icon") |                                  |
|                                  |                                  |
|                                  | **OpCon Command Line**:          |
|                                  |                                  |
|                                  | \"C:\\Program                    |
|                                  | File                             |
|                                  | s\\Opconxps\\MSLSAM\\Chronoman\" |
|                                  | =tNextDay =cC:\\Chronoman        |
|                                  | Files\\NextDayCommand.txt        |
|                                  | =sTestSchedule                   |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Chronoman Command File**:      |
|                                  |                                  |
|                                  | SET_FORMAT_STRING,mm/dd/yy\      |
|                                  | d,1\                             |
|                                  | FIND_WORKING_DAY_FORWARD\        |
|                                  | d,1                              |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Summary:** The base date of    |
|                                  | today is assumed because it is   |
|                                  | not specified on the command     |
|                                  | line or in the command file. The |
|                                  | property to be updated is called |
|                                  | NextDay. The schedule to be used |
|                                  | for determining working days is  |
|                                  | called TestSchedule.             |
|                                  |                                  |
|                                  | -   [SET_FORMAT_STRING]{styl     | |                                  | e="font-family: 'Courier New';"} |
|                                  |     specifies the format for     |
|                                  |     output to the property as a  |
|                                  |     standard date format. d,1    |
|                                  |     adds one day to the computed |
|                                  |     date.                        |
|                                  | -                                |
|                                  |  [FIND_WORKING_DAY_FORWARD]{styl | |                                  | e="font-family: 'Courier New';"} |
|                                  |     uses the value of the        |
|                                  |     computed date if it is a     |
|                                  |     working day; otherwise, the  |
|                                  |     next workday is found. d,1   |
|                                  |     adds one more day to the     |
|                                  |     computed date to arrive at   |
|                                  |     the final value for the      |
|                                  |     property.                    |
+----------------------------------+----------------------------------+

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **SCENARIO 3:** Set the property | | circular                         | to tomorrow\'s date.             |
| background](../../../Reso        |                                  |
| urces/Images/example-icon(48x48) |                                  |
| .png "Example icon") |                                  |
|                                  | **OpCon Command Line**:          |
|                                  |                                  |
|                                  | \"C:\\Program                    |
|                                  | File                             |
|                                  | s\\Opconxps\\MSLSAM\\Chronoman\" |
|                                  | =tTomorrow =cC:\\Chronoman       |
|                                  | Files\\TomorrowCommand.txt       |
|                                  | =sTestSchedule                   |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Chronoman Command File**:      |
|                                  |                                  |
|                                  | SET_FORMAT_STRING,mm/dd/yy\      |
|                                  | d,1                              |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Summary**: The base date of    |
|                                  | today is assumed because it is   |
|                                  | not specified on the command     |
|                                  | line or in the command file. The |
|                                  | property to be updated is called |
|                                  | *Tomorrow*. The schedule to be   |
|                                  | used for determining working     |
|                                  | days is called *TestSchedule*.   |
|                                  |                                  |
|                                  | -   [SET_FORMAT_STRING]{styl     | |                                  | e="font-family: 'Courier New';"} |
|                                  |     specifies the format for     |
|                                  |     output to the property as a  |
|                                  |     standard date format. d,1    |
|                                  |     adds one day to the computed |
|                                  |     date to arrive at the final  |
|                                  |     value for the property.      |
+----------------------------------+----------------------------------+

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **SCENARIO 4:** Set the property | | circular                         | to the first working day of the  |
| background](../../../Reso        | month in the format of a         |
| urces/Images/example-icon(48x48) | seven-character Julian date.     |
| .png "Example icon") |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | For this example, a user-defined |
|                                  | System property was created in   |
|                                  | the Enterprise Manager. The      |
|                                  | property was given a Name of     |
|                                  | \$SCHEDULE DATE JUL and a value  |
|                                  | of YYYYj.                        |
|                                  |                                  |
|                                  | -   The property can be passed   |
|                                  |     to a command file from the   |
|                                  |     OpCon command line.          |
|                                  | -   This property cannot be used |
|                                  |     in the command file because  |
|                                  |     only the SAM can resolve     |
|                                  |     system.                      |
|                                  | -   The command file must        |
|                                  |     contain a variable that can  |
|                                  |     be replaced by an entry on   |
|                                  |     the OpCon command line.      |
|                                  | -   The command file for this is |
|                                  |     called JulianFirst.cmd. The  |
|                                  |     contents of the command file |
|                                  |     should all be on one line.   |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **OpCon Command Line**:          |
|                                  |                                  |
|                                  | \"C:\\Chronoman                  |
|                                  | Files\\JulianFirst.cmd\"         |
|                                  | \[\[\$SCHEDULE DATE JUL\]\]      | |                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **JulianFirst.cmd File**:        |
|                                  |                                  |
|                                  | \"C:\\Program                    |
|                                  | File                             |
|                                  | s\\OpConxps\\MSLSAM\\Chronoman\" |
|                                  | =cC:\\Chronoman                  |
|                                  | Files\\JulianFirstCommand.txt    |
|                                  | =sTestSchedule =j%1              |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **JulianFirstCommand.txt File**: |
|                                  |                                  |
|                                  | SET_FORMAT_STRING, YYYYy\        |
|                                  | SET_TOKEN_NAME,                  |
|                                  | \"Julian.First\"\                |
|                                  | FIND_MONTH_BEGIN\                |
|                                  | FIND_WORKING_DAY_FORWARD\        |
|                                  | ZERO_FILL_DIRECTIVE,5,7          |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Summary**: The base date is    |
|                                  | set to the Schedule Date in a    |
|                                  | Julian format (i.e., 2008025).   |
|                                  | The schedule to be used for      |
|                                  | determining working days is      |
|                                  | called TestSchedule.             |
|                                  |                                  |
|                                  | -   [SET_FORMAT_STRING]{styl     | |                                  | e="font-family: 'Courier New';"} |
|                                  |     specifies the format for     |
|                                  |     output to the property as a  |
|                                  |     Julian date beginning with   |
|                                  |     the four-digit year.         |
|                                  | -   [SET_TOKEN_NAME]{styl        | |                                  | e="font-family: 'Courier New';"} |
|                                  |     defines the property to be   |
|                                  |     updated as Julian.First. The |
|                                  |     name is surrounded in quotes |
|                                  |     as \"Julian.First\" because  |
|                                  |     there is a period in the     |
|                                  |     name.                        |
|                                  | -   [FIND_MONTH_BEGIN]{styl      | |                                  | e="font-family: 'Courier New';"} |
|                                  |     finds the first day of the   |
|                                  |     month of the computed date.  |
|                                  | -                                |
|                                  |  [FIND_WORKING_DAY_FORWARD]{styl | |                                  | e="font-family: 'Courier New';"} |
|                                  |     uses the value of the        |
|                                  |     computed date if it is a     |
|                                  |     working day, otherwise the   |
|                                  |     next workday is found.       |
|                                  | -   [ZERO_FILL_DIRECTIVE]{styl   | |                                  | e="font-family: 'Courier New';"} |
|                                  |     inserts zeros into the       |
|                                  |     computed date at the fifth   |
|                                  |     character and continuing     |
|                                  |     until the final string is    |
|                                  |     seven characters. The result |
|                                  |     of this directive is output  |
|                                  |     to the property. If the base |
|                                  |     date were 2008025, the value |
|                                  |     of the property would be     |
|                                  |     updated with 2008001.        |
+----------------------------------+----------------------------------+

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **SCENARIO 5:** Set the property | | circular                         | to the number of elapsed days    |
| background](../../../Reso        | between the first day of March   |
| urces/Images/example-icon(48x48) | and the second Thursday of the   |
| .png "Example icon") | month.                           |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **OpCon Command Line**:          |
|                                  |                                  |
|                                  | C:\\Program                      |
|                                  | Fi                               |
|                                  | les\\Opconxps\\MSLSAM\\Chronoman |
|                                  | =b03/01/2017 =tDays              |
|                                  | =cC:\\Chronoman                  |
|                                  | Files\\DaysCommand.txt           |
|                                  | =sTestSchedule                   |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **DaysCommand.txt File**:        |
|                                  |                                  |
|                                  | SET_FORMAT_STRING,\#\#\          |
|                                  | w,1\                             |
|                                  | FIND_DAY_OF_WEEK_FORWARD,5\      |
|                                  | COMPUTE_ELAPSED_DAYS             |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | **Summary**: The base date of    |
|                                  | March 1, 2017 is used for the    |
|                                  | computation. The property to be  |
|                                  | updated is called Days. The      |
|                                  | schedule to be used for          |
|                                  | determining working days is      |
|                                  | called TestSchedule.             |
|                                  |                                  |
|                                  | -   [SET_FORMAT_STRING]{styl     | |                                  | e="font-family: 'Courier New';"} |
|                                  |     specifies the format for     |
|                                  |     output to the property as an |
|                                  |     integer. W,1 adds one week   |
|                                  |     to the computed date.        |
|                                  | -   [                            | |                                  | FIND_DAY_OF_WEEK_FORWARD,5]{styl |
|                                  | e="font-family: 'Courier New';"} |
|                                  |     uses the value of the        |
|                                  |     computed date if it is       |
|                                  |     Thursday, otherwise the next |
|                                  |     Thursday are found.          |
|                                  | -   [COMPUTE_ELAPSED_DAYS]{styl  | |                                  | e="font-family: 'Courier New';"} |
|                                  |     calculate the number of days |
|                                  |     between the base date and    |
|                                  |     the computed date. The       |
|                                  |     number of elapsed days are   |
|                                  |     output to the property.      |
+----------------------------------+----------------------------------+

## Logging

:::note
The Output Directory was configured during installation. For more information, refer to [File Locations](../../file-locations.md) in the **Concepts** online help.
:::

The Chronoman log file provides detailed information regarding the
Chronoman processing.

- The log file resides in the \<Output Directory\>\\MSLSAM\\Log\\
    directory.
- Each time the Chronoman.exe runs, it creates a log file name with
    the following syntax: Chronoman_CCYYMMDD_HHmmssss.log. The \"ssss\"
    in syntax represents seconds and tenths of seconds (e.g.,
    Chronoman_20110513_15263142.log).
- Upon startup, Chronoman.exe checks the MSLSAM\\Log folder for log
    files older than today and moves them to the appropriate archive
    subfolder.
- All archived log files reside in the \<Output
    Directory\>\\MSLSAM\\Log\\Archive\\\<Day\> folder.
- If the Chronoman log files in the MSLSAM\\Log are older than the
    oldest Archive folder, the old logs are simply deleted.

## Error Codes

Chronoman exits with a value of 0 if it succeeds and an error code if
errors are detected. Refer to the [Chronoman Command-line and Command-file
Errors](#Chronoman_Command_Line_and_Command_File_Errors)
table for a complete list of errors. Chronoman writes all errors to the
Chronoman.log file placed in the directory specified in the
Chronoman.ini configuration file. Also, as long as the communication
with SAM through the MSGIN directory is working, Chronoman sends all
errors to the SAM.log. Chronoman writes these errors to the SAM.log with
the following syntax:

Chronoman ERROR: \#\#\#\#\# Supplemental Data: \[xxxxxxxxxx\]
+--------------+------------------------------------------------------+
| Error Number | Error Description                                    |
+==============+======================================================+
| -1           | One or more of the following issues will cause this  |
|              | error:                                               |
|              |                                                      |
|              | -   Database connection made, but unable to read the |
|              |     table to resolve the token.                      |
|              | -   Critical system error - GetModuleFileName ()     |
|              |     failed                                           |
|              | -   Error reading Database Configuration file - it   |
|              |     appears to be damaged                            |
|              | -   The Property Name exceeded 64 characters         |
+--------------+------------------------------------------------------+
| 1            | Database connection made, but unable to read the     |
|              | table to resolve the property.                       |
+--------------+------------------------------------------------------+
| 3            | Zero Fill Directives incorrectly specified.          |
+--------------+------------------------------------------------------+
| 4            | Zero Fill Directives insertion point not numeric.    |
+--------------+------------------------------------------------------+
| 5            | Zero Fill Directives insertion point less than 1.    |
+--------------+------------------------------------------------------+
| 6            | Zero fill Directives insertion point must be less    |
|              | than length of string.                               |
+--------------+------------------------------------------------------+
| 7            | Zero Fill Directives desired string length not       |
|              | numeric.                                             |
+--------------+------------------------------------------------------+
| 8            | Zero Fill Directives desired length less than 1.     |
+--------------+------------------------------------------------------+
| 9            | Julian date not in format (=f) YYYYy or non-numeric  |
|              | characters in Julian date.                           |
+--------------+------------------------------------------------------+
| 11           | Julian date must be between 1 and 366.               |
+--------------+------------------------------------------------------+
| 13           | Unable to add/subtract specified offset and units    |
|              | combination from time.                               |
+--------------+------------------------------------------------------+
| 14           | No arguments specified on command line.              |
+--------------+------------------------------------------------------+
| 15           | Missing or incomplete arguments on command line.     |
+--------------+------------------------------------------------------+
| 16           | Invalid Offset (=o) specified.                       |
+--------------+------------------------------------------------------+
| 17           | Unknown option specified.                            |
+--------------+------------------------------------------------------+
| 18           | Command File and Offset (=o) specified -- illegal    |
|              | combination.                                         |
+--------------+------------------------------------------------------+
| 20           | The Specified Command File does not exist or cannot  |
|              | be found.                                            |
|              |                                                      |
|              | -   A possible cause for this problem can be from    |
|              |     copying and pasting a working directory from an  |
|              |     email or PDF file as opposed to manually typing  |
|              |     the correct information.                         |
|              | -   Hidden characters in the Working Directory are a |
|              |     known cause for this problem.                    |
+--------------+------------------------------------------------------+
| 21           | Offset (=o) not specified or offset set to zero.     |
+--------------+------------------------------------------------------+
| 23           | Working days are needed, but the Schedule Name (=s)  |
|              | is missing.                                          |
+--------------+------------------------------------------------------+
| 24           | The SMAODBCConfig.dat file is missing. Please use    |
|              | the SMAODBCConfig.exe program to configure the       |
|              | database connection.                                 |
+--------------+------------------------------------------------------+
| 26           | Property Name parameter not defined or invalid.      |
|              | Specify the =t parameter on the command line or the  |
|              | SET_TOKEN_NAME special directive in the command      |
|              | file.                                                |
|              |                                                      |
|              |                                                      |
|              |                                                      |
|              | The Property Name cannot contain the following       |
|              | characters:\                                         |
|              | \' ( ) \\ , = ; \|                                   |
+--------------+------------------------------------------------------+
| 27           | Time format not specified.                           |
+--------------+------------------------------------------------------+
| 30           | Unable to create a valid start date/time from        |
|              | specified value.                                     |
+--------------+------------------------------------------------------+
| 31           | One or more of the following issues will cause this  |
|              | error:                                               |
|              |                                                      |
|              | -   Unable to format date/time combination using     |
|              |     specified format.                                |
|              | -   Unable to format value using specified format.   |
|              | -   Error occurred trying to convert Julian date     |
+--------------+------------------------------------------------------+
| 34           | Computed date value not specified.                   |
+--------------+------------------------------------------------------+
| 35           | Computed date (Julian) value not specified.          |
+--------------+------------------------------------------------------+
| 36           | Format value not specified.                          |
+--------------+------------------------------------------------------+
| 37           | Schedule name not specified.                         |
+--------------+------------------------------------------------------+
| 38           | Property Name is empty. The value for the =t         |
|              | parameter on the command line or the SET_TOKEN_NAME  |
|              | special directive in the command file does not have  |
|              | a value.                                             |
+--------------+------------------------------------------------------+
| 39           | Zero fill directives not completely specified.       |
+--------------+------------------------------------------------------+
| 40           | Day of week must be between 1 and 7.                 |
+--------------+------------------------------------------------------+
| 42           | Unable to read Command File.                         |
+--------------+------------------------------------------------------+
| 43           | Invalid value in Command File.                       |
+--------------+------------------------------------------------------+
| 44           | Character fill directives not completely specified.  |
+--------------+------------------------------------------------------+
| 45           | Character fill directives desired string length not  |
|              | numeric.                                             |
+--------------+------------------------------------------------------+
| 46           | Character fill directives insertion point not        |
|              | numeric.                                             |
+--------------+------------------------------------------------------+
| 47           | Character fill directives insertion point less than  |
|              | 1.                                                   |
+--------------+------------------------------------------------------+
| 48           | Character fill directives desired length less than   |
|              | 1.                                                   |
+--------------+------------------------------------------------------+
| 49           | Negative Annual Plan not specified.                  |
+--------------+------------------------------------------------------+
| 50           | Fiscal Quarter dates not specified in the config     |
|              | (INI) file.                                          |
+--------------+------------------------------------------------------+
| 51           | Invalid format for Fiscal Quarter dates in the       |
|              | config (INI) file.                                   |
+--------------+------------------------------------------------------+
| 52           | There is an overlap in fiscal quarter dates.         |
+--------------+------------------------------------------------------+
| 53           | One or more of the following issues will cause this  |
|              | error:                                               |
|              |                                                      |
|              | -   Unable to find Database Configuration Parameters |
|              |     file                                             |
|              | -   Error reading Database Configuration parameters  |
|              | -   Invalid Log File Path                            |
|              | -   Invalid MSGIN Path                               |
+--------------+------------------------------------------------------+

: []{#Chronoman_Command_Line_and_Command_File_Errors}Chronoman Command-line and Command-file Errors

## Running on OpCon in Docker

In order to run the utility successfully in a Docker container, using
the Linux agent embedded in it, keep the following things in mind:

1. When running in Docker, the Linux job needs to be set up similar to
    a Windows job with the same parameters.
2. The start image for the Linux job should be: *dotnet
    /app/Chronoman.dll \<arguments\>*.
3. The Chronoman.ini file will be located in the **/app/config**
    directory in the container, mapped to any folder on the host machine
    just like all other INI files.
4. The Chronoman command file can use the same location as the INI file
    (or any location on the host machine with a mapping to a directory
    in the container).
5. Use the default **OpConOnLinux** agent machine (available in the
    container) to run the utility jobs.
6. Logs are found in **/app/log/Utilities** in the container.
