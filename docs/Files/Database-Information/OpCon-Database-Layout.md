---
lang: en-us
title: OpCon Database Layout
viewport: width=device-width, initial-scale=1.0
---

# OpCon Database Layout

  --------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ![White "X" icon on red circular background](../../Resources/Images/warning-icon(48x48).png "Warning icon")   **WARNING:** [The information in this topic is correct; however, most of the Daily tables have an additional column for the Instance Number for schedules. This new column is part of the Primary Key for each of the affected tables. User defined Reports and SQL queries will be affected by this change.]
  --------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Disclaimer

The information in this topic is provided for purposes of data retrieval
only. Any other use, including database updates, could cause
unpredictable results to the OpCon software. Such results could include,
but are not limited to:

1. Stoppage of job processing
2. SQL database errors
3. SQL Server circular processing

SMA Technologies support may not be able to return the database to a working state if an undocumented user update
has been made. Contact SMA Technologies Support prior to any manual OpCon database updates other than [SMA
Technologies]{.GeneralCompanyName}-provided SQL scripts.

## Introduction

  --------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------
  ![White "X" icon on red circular background](../../Resources/Images/warning-icon(48x48).png "Warning icon")   **WARNING:** [Unauthorized updates to the OpCon database voids OpCon support and warranties.]
  --------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------

The Database is a dynamic component of OpCon (Operations
Control/Cross-platform Scheduler) and accommodates the objects used by
the graphical interfaces, OpCon utilities, and all SAM components. The
Database is implemented as a Relational DBMS, specifically as SQL
Server. The user security, limited to the functionality within the OpCon
context, does not extend to DBMS security (e.g., User IDs, passwords,
group privileges, and so forth).

### OpCon Database Roles and Login IDs

The OpCon database uses three roles. These roles include SQL login IDs
for OpCon components.

- **OpConxps**: This role has full control of the OpCon database.
  - **opconsam**: This login ID is the SAM and supporting service's
        (SAM-SS') ID for access to the database.
  - **opconui**: This login ID is the ID for the graphical
        interfaces to access the database.
- **opconspuser**: This role has EXEC permission to execute
    supplemental stored procedures.
- **opconreader**: This role has read-only access to the OpCon
    database.

### Auxiliary Table Usage

The following is the naming convention for each auxiliary table:
\<Primary Table Name\>\_AUX.

  ------------------------------------------------------------------------------------------------------------------------------ ------------------------------------------------------------------------------------------------------------------------------------
  ![White pencil icon on green circular background](../../Resources/Images/example-icon(48x48).png "Example icon")   **EXAMPLE:** [The auxiliary table for the JMASTER table is named [JMASTER_AUX]{style="font-family: 'Courier New';"}.]{.statement2}
  ------------------------------------------------------------------------------------------------------------------------------ ------------------------------------------------------------------------------------------------------------------------------------

Each of the auxiliary tables contains the following:

- Columns to construct enough unique data to cross-reference
    information in its respective primary table.
- A column to contain the data for the field.
- The two columns for lookup into SMALOOKUP have the naming
    conventions specified in the next table.

+----------------------------------+----------------------------------+
| Column Naming Convention         | Description                      |
+==================================+==================================+
| \<First Letter of the Primary    | -   This column contains the     |
| Table Name\>AFC                  |     Auxiliary Field Code.        |
|                                  | -   The corresponding SMAFC and  |
|                                  |     SMAVALUE in the SMALOOKUP    |
|                                  |     table represent the name of  |
|                                  |     the field in the graphical   |
|                                  |     interfaces.                  |
+----------------------------------+----------------------------------+
| \<First Letter of the Primary    | -   This column contains the     |
| Table Name\>ASEQNO               |     Auxiliary Sequence Number.   |
|                                  | -   The Auxiliary Sequence       |
|                                  |     Number provides a unique     |
|                                  |     identification number        |
|                                  |     allowing multiple fields of  |
|                                  |     the same name to be          |
|                                  |     presented on a single        |
|                                  |     screen.                      |
+----------------------------------+----------------------------------+

: Auxiliary Table Lookup Columns

### Date/Time Format

The date/time format adheres to Microsoft standards for storing the
information in an IEEE double-precision data type, as defined in the
C/C++ MFC COleDateTime class and used by Visual Basic. The integer part
of the date contains the number of days starting at zero from Saturday,
December 30, 1899. The decimal part contains the fraction of seconds
elapsed since midnight. One day has 86,400 seconds.

The database contains three kinds of date/time-related data types to
optimize for the different components of the date/time information. The
following are field data types:

- integer (4-byte int) SQL/C containing days, such as SKDDATE
- single precision (4-byte real) SQL/C containing time as decimal
- double precision (8-byte float) SQL/C containing the complete
    date/time signature

## Table Reference

Organized in alphabetical order, each section below contains information
on all the tables of the OpCon database. The information lists in order
of appearance the columns that compose each table of the OpCon database.
This format can aid a knowledgeable programmer to determine how to
construct SQL action queries for retrieving information from the
database.

### Document Conventions

In each section below, the information in the first table lists the
column name, a description of the purpose, and the SQL data type with
its length in parentheses.

The second table contains information on the available indexes and
component columns. Indexes with a *PK\_* prefix indicate a primary key.
Some columns contain comments for additional clarification.

### ACCESSCD

The primary table ACCESSCD contains base information describing Access
Codes. OpCon references the Access Codes by IDs assigned by the
Enterprise Manager at the time of Access Code creation.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| ACCESSCDID  | -   This column  | smallint (2) | None             |
|             |     contains     |              |                  |
|             |     Access Code  |              |                  |
|             |     IDs.         |              |                  |
|             | -   This column  |              |                  |
|             |     uniquely     |              |                  |
|             |     identifies   |              |                  |
|             |     each Access  |              |                  |
|             |     Code.        |              |                  |
|             | -   The          |              |                  |
|             |                  |              |                  |
|             |    ACCESSCD_AUX, |              |                  |
|             |     JMASTER,     |              |                  |
|             |     SMASTER, and |              |                  |
|             |     UACCESS      |              |                  |
|             |     tables       |              |                  |
|             |     reference    |              |                  |
|             |     this table.  |              |                  |
+-------------+------------------+--------------+------------------+
| ACCESSCD    | -   This column  | char (20)    | None             |
|             |     contains     |              |                  |
|             |     Access Code  |              |                  |
|             |     names.       |              |                  |
|             | -   This column  |              |                  |
|             |     contains the |              |                  |
|             |     Access Code  |              |                  |
|             |     names        |              |                  |
|             |     displayed in |              |                  |
|             |     the          |              |                  |
|             |     Security \>  |              |                  |
|             |     Access Codes |              |                  |
|             |     screen in    |              |                  |
|             |     the          |              |                  |
|             |     Enterprise   |              |                  |
|             |     Manager.     |              |                  |
+-------------+------------------+--------------+------------------+

: ACCESSCD Column Descriptions

  Index Code    Columns
  ------------- ------------
  PK_ACCESSCD   ACCESSCDID

  : ACCESSCD Index Descriptions

### ACCESSCD_AUX

The secondary table ACCESSCD_AUX contains auxiliary information
describing Access Codes. The Access Code ID links the auxiliary
information to the correct record in the ACCESSCD primary table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| ACCESSCDID  | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     Access Code |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     ACCESSCD    |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| AAFC        | This column     | smallint (2)   | None            |
|             | contains        |                |                 |
|             | auxiliary       |                |                 |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| AASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| AAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     values.     |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: ACCESSCD_AUX Column Descriptions

+----------------+------------+
| Index Code     | Columns    |
+================+============+
| PK_ACCESSCDAUX | ACCESSCDID |
|                |            |
|                | AAFC       |
|                |            |
|                | AASEQNO    |
+----------------+------------+

: ACCESSCD_AUX Index Descriptions

### AUDITARC

The primary table AUDITARC contains Audit history information archived
from the AUDITHST table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SQLDATE     | This column     | float (8)      | -   This column |
|             | contains the    |                |     contains    |
|             | dates and times |                |     the         |
|             | when the SQL    |                |     date/time   |
|             | queries took    |                |     stamp in    |
|             | place.          |                |     SQL format. |
|             |                 |                | -   The integer |
|             |                 |                |     part of the |
|             |                 |                |     number      |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
|             |                 |                | -   The         |
|             |                 |                |     fractional  |
|             |                 |                |     part of the |
|             |                 |                |     number      |
|             |                 |                |     represents  |
|             |                 |                |     the time in |
|             |                 |                |     seconds     |
|             |                 |                |     since       |
|             |                 |                |     midnight.   |
+-------------+-----------------+----------------+-----------------+
| USERID      | This column     | int (4)        | None            |
|             | contains the    |                |                 |
|             | OpCon User      |                |                 |
|             | Login IDs       |                |                 |
|             | performing the  |                |                 |
|             | SQL queries and |                |                 |
|             | cross-reference |                |                 |
|             | information for |                |                 |
|             | lookup into the |                |                 |
|             | USERS table.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| SQLTYPE     | This column     | char (8)       | SQL commands    |
|             | contains the    |                | include:        |
|             | SQL commands    |                |                 |
|             | performed.      |                | -   INSERT      |
|             |                 |                | -   UPDATE      |
|             |                 |                | -   DELETE      |
+-------------+-----------------+----------------+-----------------+
| SQLSTATUS   | This column     | int (4)        | -   An integer  |
|             | contains the    |                |     greater     |
|             | number of rows  |                |     than zero   |
|             | affected by the |                |     (\>0)       |
|             | SQL statements. |                |     represents  |
|             |                 |                |     a           |
|             |                 |                |     successful  |
|             |                 |                |     query.      |
|             |                 |                | -   A -1        |
|             |                 |                |     represents  |
|             |                 |                |     an          |
|             |                 |                |                 |
|             |                 |                |    unsuccessful |
|             |                 |                |     query due   |
|             |                 |                |     to a syntax |
|             |                 |                |     error or a  |
|             |                 |                |     con         |
|             |                 |                | nection-related |
|             |                 |                |     cause.      |
+-------------+-----------------+----------------+-----------------+
| SQLMSG      | This column     | varchar (4000) | None            |
|             | contains the    |                |                 |
|             | full SQL        |                |                 |
|             | statements      |                |                 |
|             | performed by    |                |                 |
|             | the legacy User |                |                 |
|             | Interface or    |                |                 |
|             | utilities.      |                |                 |
+-------------+-----------------+----------------+-----------------+

: AUDITARC Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_AUDITARC | SQLDATE |
|             |         |
|             | USERID  |
|             |         |
|             | SQLTYPE |
+-------------+---------+

: AUDITARC Index Descriptions

### AUDITCONNECTIONS

The primary table AUDITCONNECTIONS contains information about current
user connections to OpCon.

  Column Name     Explanation                                                                                                  Data Type       Additional Information
  --------------- ------------------------------------------------------------------------------------------------------------ --------------- ------------------------
  CONNECTIONID    This column contains the SQL Server SPIDs of the users' connections to the database                         int (4)         None
  OPCONUSERNAME   This column contains the OpCon User Logins                                                                   varchar (512)   None
  SQLUSERNAME     This column contains the names of the SQL Server logins used to establish the connections to the database.   varchar (128)   None
  HOSTNAME        This column contains the host names of the machines at which the SQL Server connections originated.          varchar (128)   None
  LOGINTIME       This column contains the dates and times that the connections were established                               datetime (4)    None

  : AUDITCONNECTIONS Column Descriptions

+---------------------+---------------+
| Index Code          | Columns       |
+=====================+===============+
| PK_AUDITCONNECTIONS | CONNECTIONID  |
|                     |               |
|                     | OPCONUSERNAME |
|                     |               |
|                     | LOGINTIME     |
+---------------------+---------------+

: AUDITCONNECTIONS Index Descriptions

### AUDITHST

The AUDITHST table contains Audit history from updates made prior to
OpCon 5.0. Use the LegacyAudit.exe to manage these records. The auditing
mechanism in OpCon has been replaced and now uses the AUDITRECS and
AUDITRECSVIEW tables.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SQLDATE     | This column     | float (8)      | -   This column |
|             | contains the    |                |     contains    |
|             | dates and times |                |     the         |
|             | when the SQL    |                |     date/time   |
|             | queries took    |                |     stamp in    |
|             | place.          |                |     SQL format. |
|             |                 |                | -   The integer |
|             |                 |                |     part of the |
|             |                 |                |     number      |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
|             |                 |                | -   The         |
|             |                 |                |     fractional  |
|             |                 |                |     part of the |
|             |                 |                |     number      |
|             |                 |                |     represents  |
|             |                 |                |     the time in |
|             |                 |                |     seconds     |
|             |                 |                |     since       |
|             |                 |                |     midnight.   |
+-------------+-----------------+----------------+-----------------+
| USERID      | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the OpCon   |                |                 |
|             |     User Login  |                |                 |
|             |     IDs         |                |                 |
|             |     performing  |                |                 |
|             |     the SQL     |                |                 |
|             |     queries.    |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     USERS       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| SQLTYPE     | This column     | char (8)       | SQL commands    |
|             | contains the    |                | include:        |
|             | SQL commands    |                |                 |
|             | performed.      |                | -   INSERT      |
|             |                 |                | -   UPDATE      |
|             |                 |                | -   DELETE      |
+-------------+-----------------+----------------+-----------------+
| SQLSTATUS   | This column     | int (4)        | -   An integer  |
|             | contains the    |                |     greater     |
|             | number of rows  |                |     than zero   |
|             | affected by the |                |     (\>0)       |
|             | SQL statements. |                |     represents  |
|             |                 |                |     a           |
|             |                 |                |     successful  |
|             |                 |                |     query.      |
|             |                 |                | -   A -1        |
|             |                 |                |     represents  |
|             |                 |                |     an          |
|             |                 |                |                 |
|             |                 |                |    unsuccessful |
|             |                 |                |     query due   |
|             |                 |                |     to a syntax |
|             |                 |                |     error or a  |
|             |                 |                |     con         |
|             |                 |                | nection-related |
|             |                 |                |     cause.      |
+-------------+-----------------+----------------+-----------------+
| SQLMSG      | This column     | varchar (4000) | None            |
|             | contains the    |                |                 |
|             | full SQL        |                |                 |
|             | statements      |                |                 |
|             | performed by    |                |                 |
|             | the legacy User |                |                 |
|             | Interface or    |                |                 |
|             | utilities.      |                |                 |
+-------------+-----------------+----------------+-----------------+

: AUDITHST Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_AUDITHST | SQLDATE |
|             |         |
|             | USERID  |
|             |         |
|             | SQLTYPE |
+-------------+---------+

: AUDITHST Index Descriptions

### AUDITRECS

The primary table AUDITRECS contains information about changes that have
been made to data in the OpCon database. Data in this table is
periodically moved to the AUDITRECSVIEW table to facilitate viewing and
analysis by users while minimizing impact on the operational systems.

  Column Name     Explanation                                                                                                     Data Type        Additional Information
  --------------- --------------------------------------------------------------------------------------------------------------- ---------------- ------------------------
  AUDITRECID      This column contains the unique numeric IDs for each row in the table.                                          int (4)          None
  UPDTIMESTAMP    This column contains the dates and times at which the actions that caused the audits took place.                datetime(4)      None
  OPCONUSERNAME   This column contains the OpCon User Logins of the users that initiated the actions.                             varchar (512)    None
  SQLUSERNAME     This column contains the names of the SQL Server logins under which the actions were initiated.                 varchar (128)    None
  HOSTNAME        This column contains the host names of the machines from which the actions were initiated.                      varchar (128)    None
  TBLNAME         This column contains the names of the affected database tables as they are known in the SMALOOKUP table.        varchar (128)    None
  REALTBLNAME     This column contains the is the names of the actual database tables affected by the actions.                    varchar (128)    None
  KEY1            This column contains the values in the first primary key column of the tables affected by the user actions.     varchar(1024)    None
  KEY2            This column contains the values in the second primary key column of the tables affected by the user actions.    varchar (1024)   None
  KEY3            This column contains the values in the third primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY4            This column contains the values in the fourth primary key column of the tables affected by the user actions.    varchar (1024)   None
  KEY5            This column contains the values in the fifth primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY6            This column contains the values in the sixth primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY7            This column contains the values in the seventh primary key column of the tables affected by the user actions.   varchar (1024)   None
  KEY8            This column contains the values in the eighth primary key column of the tables affected by the user actions.    varchar (1024)   None
  KEY9            This column contains the values in the ninth primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY10           This column contains the values in the tenth primary key column of the tables affected by the user actions.     varchar (1024)   None
  COLFC           This column contains the SMALOOKUP field code associated with the changed field.                                int              None
  BEFOREVALUE     This column contains the values in the fields before the change.                                                varchar (2000)   None
  AFTERVALUE      This column contains the values in the fields after the change.                                                 varchar (2000)   None

  : AUDITRECS Column Descriptions

+--------------+------------+
| Index Code   | Columns    |
+==============+============+
| PK_AUDITRECS | AUDITRECID |
|              |            |
|              |            |
+--------------+------------+

: AUDITRECS Index Descriptions

### AUDITRECSVIEW

The primary table AUDITRECSVIEW contains information about changes that
have been made to data in the OpCon database. Data in this table is
periodically populated from the AUDITRECS table to facilitate viewing
and analysis by users while minimizing impact on the operational
systems.

  Column Name     Explanation                                                                                                     Data Type        Additional Information
  --------------- --------------------------------------------------------------------------------------------------------------- ---------------- ------------------------
  AUDITRECID      This column contains the unique numeric IDs for each row in the table.                                          int (4)          None
  UPDTIMESTAMP    This column contains the dates and times at which the actions that caused the audits took place.                datetime (4)     None
  OPCONUSERNAME   This column contains the OpCon User Logins of the users that initiated the actions.                             varchar (512)    None
  SQLUSERNAME     This column contains the names of the SQL Server logins under which the actions were initiated.                 varchar (128)    None
  HOSTNAME        This column contains the host names of the machines from which the actions were initiated.                      varchar (128)    None
  TBLNAME         This column contains the names of the affected database tables as they are known in the SMALOOKUP table.        varchar (128)    None
  REALTBLNAME     This column contains the is the names of the actual database tables affected by the actions.                    varchar (128)    None
  KEY1            This column contains the values in the first primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY2            This column contains the values in the second primary key column of the tables affected by the user actions.    varchar (1024)   None
  KEY3            This column contains the values in the third primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY4            This column contains the values in the fourth primary key column of the tables affected by the user actions.    varchar (1024)   None
  KEY5            This column contains the values in the fifth primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY6            This column contains the values in the sixth primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY7            This column contains the values in the seventh primary key column of the tables affected by the user actions.   varchar (1024)   None
  KEY8            This column contains the values in the eighth primary key column of the tables affected by the user actions.    varchar(1024)    None
  KEY9            This column contains the values in the ninth primary key column of the tables affected by the user actions.     varchar (1024)   None
  KEY10           This column contains the values in the tenth primary key column of the tables affected by the user actions.     varchar (1024)   None
  COLFC           This column contains the SMALOOKUP field code associated with the changed field.                                int              None
  BEFOREVALUE     This column contains the values in the fields before the change.                                                varchar (2000)   None
  AFTERVALUE      This column contains the values in the fields after the change.                                                 varchar (2000)   None

  : AUDITRECSVIEW Column Descriptions

+----------------------+---------------+
| Index Code           | Columns       |
+======================+===============+
| PK_AUDITRECSVIEW     | AUDITRECID    |
|                      |               |
|                      |               |
+----------------------+---------------+
| AUDITRECSVIEW_HOST   | HOSTNAME      |
|                      |               |
|                      |               |
+----------------------+---------------+
| AUDITRECSVIEW_TIME   | UPDTIMESTAMP  |
|                      |               |
|                      |               |
+----------------------+---------------+
| AUDITRECSVIEW_USER   | OPCONUSERNAME |
|                      |               |
|                      |               |
+----------------------+---------------+
| AUDITRECSVIEW_DBUSER | SQLUSERNAME   |
|                      |               |
|                      |               |
+----------------------+---------------+
| AUDITRECSVIEW_TABLE  | REALTBLNAME   |
|                      |               |
|                      |               |
+----------------------+---------------+

: AUDITRECSVIEW Index Descriptions

### CALDATA

The secondary table CALDATA contains data relating to calendars. It
includes Holiday Calendar data as well as User Calendar data. The
Calendar ID links the calendar data to the correct record in the CALDESC
primary table.

+-------------+--------------------+-----------+--------------------+
| Column Name | Explanation        | Data Type | Additional         |
|             |                    |           | Information        |
+=============+====================+===========+====================+
| CALID       | -   This column    | int (4)   | None               |
|             |     contains       |           |                    |
|             |     calendar IDs.  |           |                    |
|             | -   This column    |           |                    |
|             |     contains       |           |                    |
|             |                    |           |                    |
|             |    cross-reference |           |                    |
|             |     information    |           |                    |
|             |     for lookup     |           |                    |
|             |     into the       |           |                    |
|             |     CALDESC table. |           |                    |
+-------------+--------------------+-----------+--------------------+
| CALDATE     | -   This column    | float (8) | -   This column    |
|             |     contains       |           |     contains the   |
|             |     calendar       |           |     date stamp in  |
|             |     dates.         |           |     SQL format.    |
|             | -   This column    |           | -   The integer    |
|             |     contains SQL   |           |     represents the |
|             |     dates defined  |           |     day count      |
|             |     in the         |           |     since          |
|             |     calendars.     |           |     Saturday,      |
|             |                    |           |     December       |
|             |                    |           |     30, 1899.      |
+-------------+--------------------+-----------+--------------------+

: CALDATA Column Descriptions

+------------+---------+
| Index Code | Columns |
+============+=========+
| PK_CALDATA | CALID   |
|            |         |
|            | CALDATE |
+------------+---------+

: CALDATA Index Descriptions

### CALDESC

The primary table CALDESC contains the Calendar description information
you generated through the Calendar option of the Administration module
in the Enterprise Manager.

+--------------+------------------+--------------+------------------+
| Column Name  | Explanation      | Data Type    | Additional       |
|              |                  |              | Information      |
+==============+==================+==============+==================+
| CALID        | -   This column  | int (4)      | None             |
|              |     contains     |              |                  |
|              |     calendar     |              |                  |
|              |     IDs.         |              |                  |
|              | -   This column  |              |                  |
|              |     uniquely     |              |                  |
|              |     identifies   |              |                  |
|              |     each         |              |                  |
|              |     calendar.    |              |                  |
|              | -   The CALDATA, |              |                  |
|              |     CALDESC_AUX, |              |                  |
|              |     JSKD, and    |              |                  |
|              |     SSYS tables  |              |                  |
|              |     reference    |              |                  |
|              |     this table.  |              |                  |
+--------------+------------------+--------------+------------------+
| SKDID        | -   This column  | int (4)      | -   A Schedule   |
|              |     contains     |              |     ID indicates |
|              |     schedule     |              |     a Holiday    |
|              |     IDs.         |              |     Calendar     |
|              | -   This column  |              |     associated   |
|              |     contains     |              |     with a       |
|              |                  |              |     schedule.    |
|              |  cross-reference |              | -   0: Indicates |
|              |     information  |              |     User         |
|              |     for lookup   |              |     Calendars    |
|              |     into the     |              |     including    |
|              |     SNAME table. |              |     the Master   |
|              |                  |              |     Holiday,     |
|              |                  |              |     Negative     |
|              |                  |              |     Annual Plan, |
|              |                  |              |     and Annual   |
|              |                  |              |     Plan         |
|              |                  |              |     Calendars.   |
+--------------+------------------+--------------+------------------+
| CALTYPE      | This column      | smallint (2) | -   0: Holiday   |
|              | contains the     |              |     Calendar     |
|              | calendar types.  |              | -   1: User      |
|              |                  |              |     Calendar     |
+--------------+------------------+--------------+------------------+
| CALNAME      | -   This column  | char (50)    | The Holiday      |
|              |     contains the |              | Calendar's name |
|              |     calendar     |              | includes the     |
|              |     names.       |              | prefix "HC:"   |
|              | -   The          |              | and the Schedule |
|              |     Enterprise   |              | Name.            |
|              |     Manager      |              |                  |
|              |     requires     |              |                  |
|              |     unique       |              |                  |
|              |     calendar     |              |                  |
|              |     names in     |              |                  |
|              |     this column. |              |                  |
+--------------+------------------+--------------+------------------+
| CALUSEMASTER | -   This column  | char (1)     | -   Y: Yes       |
|              |     contains the |              | -   N: No        |
|              |     "Use Master |              |                  |
|              |     Holiday      |              |                  |
|              |     Calendar"   |              |                  |
|              |     flag for     |              |                  |
|              |     each         |              |                  |
|              |     calendar.    |              |                  |
|              | -   This column  |              |                  |
|              |     determines   |              |                  |
|              |     if each      |              |                  |
|              |     schedule     |              |                  |
|              |     holiday      |              |                  |
|              |     calendar     |              |                  |
|              |     incorporates |              |                  |
|              |     the Master   |              |                  |
|              |     Holiday      |              |                  |
|              |     calendar.    |              |                  |
+--------------+------------------+--------------+------------------+

: CALDESC Column Descriptions

  Index Code   Columns
  ------------ ---------
  PK_CALDESC   CALID

  : CALDESC Index Descriptions

### CALDESC_AUX

The secondary table CALDESC_AUX contains auxiliary information
describing Calendars. The Calendar ID links the auxiliary information to
the correct record in the CALDESC primary table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| CALID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     Calendar    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     CALDESC     |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| CAFC        | This column     | smallint (2)   | 0:              |
|             | contains        |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| CASEQNO     | -   This column | smallint (2)   |                 |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| CAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: CALDESC_AUX Column Descriptions

+---------------+---------+
| Index Code    | Columns |
+===============+=========+
| PK_CALDESCAUX | CALID   |
|               |         |
|               | CAFC    |
|               |         |
|               | CASEQNO |
+---------------+---------+

: CALDESC_AUX Index Descriptions

### DEPTS

The primary table DEPTS contains base information describing
Departments. The Departments are referenced by IDs assigned by the
Enterprise Manager at the time of creation.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| DEPTID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     department   |              |                  |
|             |     IDs.         |              |                  |
|             | -   This column  |              |                  |
|             |     uniquely     |              |                  |
|             |     identifies   |              |                  |
|             |     each         |              |                  |
|             |     department.  |              |                  |
|             | -   The          |              |                  |
|             |     DEPTS_AUX,   |              |                  |
|             |     JMASTER,     |              |                  |
|             |     SMASTER,     |              |                  |
|             |     SSYS, and    |              |                  |
|             |     UDEPFUN      |              |                  |
|             |     tables       |              |                  |
|             |     reference    |              |                  |
|             |     this table.  |              |                  |
+-------------+------------------+--------------+------------------+
| DEPTNAME    | -   This column  | char (20)    | None             |
|             |     contains the |              |                  |
|             |     department   |              |                  |
|             |     names.       |              |                  |
|             | -   The          |              |                  |
|             |     Enterprise   |              |                  |
|             |     Manager      |              |                  |
|             |     requires     |              |                  |
|             |     unique       |              |                  |
|             |     department   |              |                  |
|             |     names in     |              |                  |
|             |     this column. |              |                  |
+-------------+------------------+--------------+------------------+

: DEPTS Column Descriptions

  Index Code   Columns
  ------------ ---------
  PK_DEPTS     DEPTID

  : DEPTS Index Descriptions

### DEPTS_AUX

The secondary table DEPTS_AUX contains auxiliary information describing
Departments. The Department ID links the auxiliary information to the
correct record in the primary DEPTS table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| DEPTID      | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     department  |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     DEPTS       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| DAFC        | This column     | smallint (2)   | 0:              |
|             | contains        |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| DASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| DAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: DEPTS_AUX Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_DEPTSAUX | DEPTID  |
|             |         |
|             | DAFC    |
|             |         |
|             | DASEQNO |
+-------------+---------+

: DEPTS_AUX Index Descriptions

### EmbeddedScriptPrivileges {#embeddedscriptprivileges mc-conditions=""}

The primary table EmbeddedScriptPrivileges contains the mapping of user
roles to the embedded scripts to which they have access.

  Column Name        Explanation                                                                            Data Type   Additional Information
  ------------------ -------------------------------------------------------------------------------------- ----------- ------------------------
  Id                 This column contains the ID that uniquely identifies each Embedded Script Privilege.   int (4)     None
  UserRoleId         This column contains the ID of the user role being mapped.                             int (4)     None
  EmbeddedScriptId   This column contains the ID of the embedded script being mapped to.                    int (4)     None

  : EmbeddedScriptPrivileges Column Descriptions

+-----------------------------+---------+
| Index Code                  | Columns |
+=============================+=========+
| PK_EmbeddedScriptPrivileges | Id\     |
+-----------------------------+---------+

: EmbeddedScriptPrivileges Index Descriptions

### ENSACTIONS

The primary table ENSACTIONS contains base information describing Event
Notification Actions. OpCon references the Event Notification Actions by
ENS Group IDs.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| GROUPOFID   | -   This column  | int (4)       | None             |
|             |     contains ENS |               |                  |
|             |     group IDs.   |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     ENSGROUPS    |               |                  |
|             |     table.       |               |                  |
+-------------+------------------+---------------+------------------+
| STATUSCODE  | -   This column  | char (3)      | -   J1: Job      |
|             |     contains the |               |     Submitted    |
|             |     triggering   |               | -   J2: Job      |
|             |     status       |               |                  |
|             |     codes.       |               |   Initialization |
|             | -   This column  |               |     Error        |
|             |     contains the |               | -   J3: Job      |
|             |     status codes |               |     Prerun       |
|             |     that trigger |               |     Failed       |
|             |                  |               | -   J4: Job      |
|             |   notifications. |               |     Missed Start |
|             |                  |               |     Time         |
|             |                  |               | -   J5: Job      |
|             |                  |               |     Exceeded Max |
|             |                  |               |     Runtime      |
|             |                  |               | -   J6: Job      |
|             |                  |               |     Finished OK  |
|             |                  |               | -   J7: Job      |
|             |                  |               |     Failed       |
|             |                  |               | -   J8: Job      |
|             |                  |               |     Marked       |
|             |                  |               |     Finished OK  |
|             |                  |               | -   J9: Job      |
|             |                  |               |     Marked       |
|             |                  |               |     Failed       |
|             |                  |               | -   J10: Job     |
|             |                  |               |     Cancelled    |
|             |                  |               | -   J11: Job     |
|             |                  |               |     Restarted    |
|             |                  |               | -   J12: Job     |
|             |                  |               |     Skipped      |
|             |                  |               | -   J13: Job to  |
|             |                  |               |     be Killed    |
|             |                  |               | -   J14: Job     |
|             |                  |               |     Wait Machine |
|             |                  |               | -   J15: Job     |
|             |                  |               |     Late to      |
|             |                  |               |     Start        |
|             |                  |               | -   J16: Job     |
|             |                  |               |     Late to      |
|             |                  |               |     Finish       |
|             |                  |               | -   J17: Job     |
|             |                  |               |     Still        |
|             |                  |               |     Attempting   |
|             |                  |               |     Start        |
|             |                  |               | -   J18: Job     |
|             |                  |               |     Running      |
|             |                  |               | -   M1: Machine  |
|             |                  |               |     Marked Down  |
|             |                  |               | -   M2: Machine  |
|             |                  |               |     Marked Up    |
|             |                  |               | -   M3: Machine  |
|             |                  |               |     Status       |
|             |                  |               |     Changed      |
|             |                  |               | -   M4: Network  |
|             |                  |               |     Down         |
|             |                  |               | -   M5: Network  |
|             |                  |               |     Up           |
|             |                  |               | -   M6: Network  |
|             |                  |               |     Status       |
|             |                  |               |     Changed      |
|             |                  |               | -   S1: Schedule |
|             |                  |               |     Start        |
|             |                  |               | -   S2: Schedule |
|             |                  |               |     Complete     |
|             |                  |               | -   S3: Schedule |
|             |                  |               |     Placed On    |
|             |                  |               |     Hold         |
|             |                  |               | -   S4: Schedule |
|             |                  |               |     Released     |
|             |                  |               |     From Hold    |
+-------------+------------------+---------------+------------------+
| ACTIONID    | -   This column  | int (4)       | -   Identity     |
|             |     contains the |               | -   Not for      |
|             |     action IDs.  |               |     replication  |
|             | -   This column  |               |                  |
|             |     provides a   |               |                  |
|             |     unique ID    |               |                  |
|             |     for each     |               |                  |
|             |     action.      |               |                  |
+-------------+------------------+---------------+------------------+
| ACTIONINCID | This column      | char (1)      | -   Y: Yes       |
|             | contains a flag  |               | -   N: No        |
|             | determining if   |               |                  |
|             | each job's      |               |                  |
|             | unique number is |               |                  |
|             | included with    |               |                  |
|             | the              |               |                  |
|             | notification.    |               |                  |
+-------------+------------------+---------------+------------------+
| ACTIONNAME  | -   This column  | varchar (255) | None             |
|             |     contains the |               |                  |
|             |     action       |               |                  |
|             |     names.       |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     information  |               |                  |
|             |     from the     |               |                  |
|             |     Description  |               |                  |
|             |     field in the |               |                  |
|             |     ENS Manager. |               |                  |
+-------------+------------------+---------------+------------------+

: ENSACTIONS Column Descriptions

+---------------+------------+
| Index Code    | Columns    |
+===============+============+
| PK_ENSACTIONS | ACTIONID   |
|               |            |
|               |            |
+---------------+------------+
| I2ENSACTIONS  | GROUPOFID  |
|               |            |
|               | STATUSCODE |
|               |            |
|               | ACTIONID   |
+---------------+------------+

: ENSACTIONS Index Descriptions

### ENSGROUPS

The secondary table ENSGROUPS contains the Event Notification Group
information. The ENS Group ID links the information to the correct
record in the ENSACTIONS primary table.

+----------------+----------------+---------------+----------------+
| Column Name    | Explanation    | Data Type     | Additional     |
|                |                |               | Information    |
+================+================+===============+================+
| GROUPOFID      | -   This       | int (4)       | None           |
|                |     column     |               |                |
|                |     contains   |               |                |
|                |     ENS group  |               |                |
|                |     IDs.       |               |                |
|                | -   The        |               |                |
|                |     ENS        |               |                |
|                | ACTIONS,ENSHIS |               |                |
|                | TORY,ENSMESSAG |               |                |
|                | ES,ENSSELECTED |               |                |
|                |     AND NOTIFY |               |                |
|                |     tables     |               |                |
|                |     reference  |               |                |
|                |     this       |               |                |
|                |     table.     |               |                |
+----------------+----------------+---------------+----------------+
| GROUPTYPE      | This column    | char (1)      | -   Identity   |
|                | contains       |               | -   Not for    |
|                | values that    |               |                |
|                | indicate       |               |    replication |
|                | whether the    |               | -   M: Machine |
|                | group is for   |               | -   S:         |
|                | machine,       |               |     Schedule   |
|                | schedules or   |               | -   J: Job     |
|                | jobs.          |               |                |
+----------------+----------------+---------------+----------------+
| GROUPEXCLSEL   | -   This       | int (4)       | -   0: As Not  |
|                |     column     |               |     Selected   |
|                |     contains   |               | -   1: As      |
|                |     the        |               |     Selected   |
|                |     default    |               |                |
|                |     selection  |               |                |
|                |     type for   |               |                |
|                |     each ENS   |               |                |
|                |     group.     |               |                |
|                | -   This       |               |                |
|                |     column     |               |                |
|                |     determines |               |                |
|                |     for each   |               |                |
|                |     ENS Group  |               |                |
|                |     the        |               |                |
|                |     default    |               |                |
|                |     method for |               |                |
|                |     the        |               |                |
|                |     selection  |               |                |
|                |     of all     |               |                |
|                |     Machines,  |               |                |
|                |     Schedules, |               |                |
|                |     and Jobs.  |               |                |
+----------------+----------------+---------------+----------------+
| GROUPNAME      | -   This       | varchar (255) | None           |
|                |     column     |               |                |
|                |     contains   |               |                |
|                |     the group  |               |                |
|                |     names.     |               |                |
|                | -   This       |               |                |
|                |     column     |               |                |
|                |     contains   |               |                |
|                |     the        |               |                |
|                |                |               |                |
|                |   user-defined |               |                |
|                |     group      |               |                |
|                |     names for  |               |                |
|                |     Machines,  |               |                |
|                |     Schedules, |               |                |
|                |     and Jobs.  |               |                |
+----------------+----------------+---------------+----------------+
| P              | -   This       | int (4)       | -   0          |
| ARENTGROUPOFID |     column     |               | -   An         |
|                |     contains   |               |     existing   |
|                |     ENS group  |               |     ENS group  |
|                |     IDs.       |               |     ID         |
|                | -   This       |               |                |
|                |     column     |               |                |
|                |     contains   |               |                |
|                |     c          |               |                |
|                | ross-reference |               |                |
|                |                |               |                |
|                |    information |               |                |
|                |     for lookup |               |                |
|                |     back into  |               |                |
|                |     the        |               |                |
|                |     ENSGROUPS  |               |                |
|                |     table to   |               |                |
|                |     determine  |               |                |
|                |     a parent   |               |                |
|                |     group.     |               |                |
+----------------+----------------+---------------+----------------+

: ENSGROUPS Column Descriptions

  Index Code     Columns
  -------------- -----------
  PK_ENSGROUPS   GROUPOFID

  : ENSGROUPS Index Descriptions

### ENSHISTORY

The primary table ENSHISTORY contains notifications the SMA Notify
Handler has processed. When the SMA Notify Handler retrieves the record
successfully, it deletes the record.

  ----------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------
  ![White pencil/paper icon on gray circular background](../../Resources/Images/note-icon(48x48).png "Note icon")   **NOTE:** [The stored procedure 'SMA_CHECK_FOR_NOTIFICATION' should be used to insert data into the table.]
  ----------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------

+----------------+----------------+----------------+----------------+
| Column Name    | Explanation    | Data Type      | Additional     |
|                |                |                | Information    |
+================+================+================+================+
| TRIGGERNAME    | Name of the    | varchar (255)  | None           |
|                | ENS Event      |                |                |
|                | trigger.       |                |                |
+----------------+----------------+----------------+----------------+
| MACHNAME       | This column    | char (24)      | None           |
|                | contains the   |                |                |
|                | machine names  |                |                |
|                | associated     |                |                |
|                | with the       |                |                |
|                | events.        |                |                |
+----------------+----------------+----------------+----------------+
| SKDDATE        | This column    | int (4)        | -   This       |
|                | contains the   |                |     column     |
|                | date stamps of |                |     stores the |
|                | the schedules. |                |     date in    |
|                |                |                |     SQL        |
|                |                |                |     format.    |
|                |                |                | -   The        |
|                |                |                |     integer    |
|                |                |                |     represents |
|                |                |                |     the day    |
|                |                |                |     count      |
|                |                |                |     since      |
|                |                |                |     Saturday,  |
|                |                |                |     December   |
|                |                |                |     30, 1899.  |
+----------------+----------------+----------------+----------------+
| SKDNAME        | This column    | varchar (255)  | None           |
|                | contains the   |                |                |
|                | descriptive    |                |                |
|                | schedule       |                |                |
|                | names.         |                |                |
+----------------+----------------+----------------+----------------+
| INSTNO         | Contains a     | int (4)        | None           |
|                | number that    |                |                |
|                | identifies the |                |                |
|                | instance of    |                |                |
|                | the schedules. |                |                |
+----------------+----------------+----------------+----------------+
| JOBNAME        | -   This       | varchar (128)  | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the job    |                |                |
|                |     names.     |                |                |
|                | -   A value in |                |                |
|                |     this       |                |                |
|                |     column is  |                |                |
|                |     only       |                |                |
|                |     present    |                |                |
|                |     for job    |                |                |
|                |     event      |                |                |
|                |     triggers.  |                |                |
+----------------+----------------+----------------+----------------+
| GROUPOFID      | -   This       | int (4)        | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     ENS group  |                |                |
|                |     IDs.       |                |                |
|                | -   This       |                |                |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     c          |                |                |
|                | ross-reference |                |                |
|                |                |                |                |
|                |    information |                |                |
|                |     for lookup |                |                |
|                |     into the   |                |                |
|                |     ENSGROUPS  |                |                |
|                |     table.     |                |                |
+----------------+----------------+----------------+----------------+
| ACTIONID       | This column    | int (4)        | None           |
|                | consists of    |                |                |
|                | the Action IDs |                |                |
|                | from the       |                |                |
|                | ENSACTIONS     |                |                |
|                | table.         |                |                |
+----------------+----------------+----------------+----------------+
| ACTIONNAME     | -   This       | varchar (255)  | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the action |                |                |
|                |     names.     |                |                |
|                | -   This       |                |                |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the        |                |                |
|                |                |                |                |
|                |    information |                |                |
|                |     from the   |                |                |
|                |                |                |                |
|                |    Description |                |                |
|                |     field in   |                |                |
|                |     the ENS    |                |                |
|                |     Manager.   |                |                |
+----------------+----------------+----------------+----------------+
| ACTIONINCID    | This column    | char (1)       | -   Y: Yes     |
|                | contains a     |                | -   N: No      |
|                | flag           |                |                |
|                | determining if |                |                |
|                | each job's    |                |                |
|                | unique number  |                |                |
|                | is included    |                |                |
|                | with the       |                |                |
|                | notification.  |                |                |
+----------------+----------------+----------------+----------------+
| ACTIONTYPE     | This column    | int (4)        | -   1: Event   |
|                | consists of a  |                |     Log        |
|                | type of action |                | -   2: E-Mail  |
|                | required.      |                | -   3: Net     |
|                |                |                |     Send       |
|                |                |                | -   4: SNMP    |
|                |                |                | -   5: SPO     |
|                |                |                | -   6: Text    |
|                |                |                |     Message    |
|                |                |                | -   7:         |
|                |                |                |     OpCon/xps  |
|                |                |                |     Event      |
+----------------+----------------+----------------+----------------+
| ACTIONMSG      | This column    | varchar (4000) | None           |
|                | consists of    |                |                |
|                | the message    |                |                |
|                | content for    |                |                |
|                | the            |                |                |
|                | notification.  |                |                |
+----------------+----------------+----------------+----------------+
| NOTIFICATIONID | This column    | int (4)        | None           |
|                | contains the   |                |                |
|                | unique keys    |                |                |
|                | that the       |                |                |
|                | notification   |                |                |
|                | was generated  |                |                |
|                | with           |                |                |
|                | (PIPESEQKEY on |                |                |
|                | the NOTIFY     |                |                |
|                | table).        |                |                |
+----------------+----------------+----------------+----------------+

: NOTIFY Column Descriptions

  Index Code      Columns
  --------------- ----------------
  PK_ENSHISTORY   NOTIFICATIONID

  : ENSHISTORY Index Descriptions

### ENSMESSAGES

The table contains the messages associated with Event Notification
System (ENS) event triggers (ENSACTIONS).

+--------------+-----------------+---------------+-----------------+
| Column Name  | Explanation     | Data Type     | Additional      |
|              |                 |               | Information     |
+==============+=================+===============+=================+
| GROUPOFID    | -   This column | char (6)      | None            |
|              |     consists of |               |                 |
|              |     the ENS     |               |                 |
|              |     group IDs   |               |                 |
|              |     from the    |               |                 |
|              |     ENSGROUPS   |               |                 |
|              |     table.      |               |                 |
|              | -   This column |               |                 |
|              |     contains    |               |                 |
|              |                 |               |                 |
|              | cross-reference |               |                 |
|              |     information |               |                 |
|              |     for lookup  |               |                 |
|              |     into the    |               |                 |
|              |     ENSGROUPS   |               |                 |
|              |     table.      |               |                 |
+--------------+-----------------+---------------+-----------------+
| ACTIONID     | This column     | int (4)       | None            |
|              | consists of the |               |                 |
|              | Action IDs from |               |                 |
|              | the ENSACTIONS  |               |                 |
|              | table.          |               |                 |
+--------------+-----------------+---------------+-----------------+
| ACTIONTYPE   | This column     | int (4)       | -   1: Event    |
|              | consists of the |               |     Log         |
|              | notification    |               | -   2: Email    |
|              | type.           |               | -   3: Net Send |
|              |                 |               | -   4: SNMP     |
|              |                 |               | -   5: SPO      |
|              |                 |               | -   6: Text     |
|              |                 |               |     Message     |
|              |                 |               | -   7:          |
|              |                 |               |     OpCon/xps   |
|              |                 |               |     Event       |
|              |                 |               | -   10: Run     |
|              |                 |               |     Command     |
+--------------+-----------------+---------------+-----------------+
| ACTIONACTIVE | This column     | int (4)       | -   0: Inactive |
|              | consists of the |               | -   1: Active   |
|              | Active/Inactive |               |                 |
|              | status of the   |               |                 |
|              | Action type.    |               |                 |
+--------------+-----------------+---------------+-----------------+
| ACTIONMSG    | This column     | varchar (max) | None            |
|              | consists of the |               |                 |
|              | message content |               |                 |
|              | for the         |               |                 |
|              | notification.   |               |                 |
+--------------+-----------------+---------------+-----------------+

: ENSMESSAGES Column Descriptions

+----------------+------------+
| Index Code     | Columns    |
+================+============+
| PK_ENSMESSAGES | GROUPOFID  |
|                |            |
|                | ACTIONID   |
|                |            |
|                | ACTIONTYPE |
+----------------+------------+

: ENSMESSAGES Index Descriptions

### ENSSELECTED

The secondary table ENSSELECTED contains the Event Notification Selected
information. The ENS Group ID links the information to the correct
record in the ENSACTIONS primary table.

+--------------+-----------------+---------------+-----------------+
| Column Name  | Explanation     | Data Type     | Additional      |
|              |                 |               | Information     |
+==============+=================+===============+=================+
| GROUPOFID    | -   This column | int (4)       | None            |
|              |     contains    |               |                 |
|              |     ENS group   |               |                 |
|              |     IDs.        |               |                 |
|              | -   This column |               |                 |
|              |     contains    |               |                 |
|              |                 |               |                 |
|              | cross-reference |               |                 |
|              |     information |               |                 |
|              |     for lookup  |               |                 |
|              |     into the    |               |                 |
|              |     ENSGROUPS   |               |                 |
|              |     table.      |               |                 |
+--------------+-----------------+---------------+-----------------+
| SELECTID     | -   This column | int (4)       | None            |
|              |     contains    |               |                 |
|              |     the         |               |                 |
|              |     selected    |               |                 |
|              |     items IDs.  |               |                 |
|              | -   This column |               |                 |
|              |     contains a  |               |                 |
|              |     unique ID   |               |                 |
|              |     for each    |               |                 |
|              |     item.       |               |                 |
+--------------+-----------------+---------------+-----------------+
| SELECTSTRING | -   This column | varchar (255) | None            |
|              |     contains    |               |                 |
|              |     the         |               |                 |
|              |     selected    |               |                 |
|              |     item        |               |                 |
|              |                 |               |                 |
|              |    information. |               |                 |
|              | -   This column |               |                 |
|              |     contains    |               |                 |
|              |     the list of |               |                 |
|              |     machines,   |               |                 |
|              |     schedules,  |               |                 |
|              |     or jobs     |               |                 |
|              |     that are    |               |                 |
|              |     not in the  |               |                 |
|              |                 |               |                 |
|              |    GROUPEXCLSEL |               |                 |
|              |     column in   |               |                 |
|              |     the         |               |                 |
|              |     ENSGROUPS   |               |                 |
|              |     table.      |               |                 |
|              | -   For         |               |                 |
|              |     example, if |               |                 |
|              |                 |               |                 |
|              |    GROUPEXCLSEL |               |                 |
|              |     were set to |               |                 |
|              |     0 (As Not   |               |                 |
|              |     Selected),  |               |                 |
|              |     this list   |               |                 |
|              |     would       |               |                 |
|              |     contain the |               |                 |
|              |     items in    |               |                 |
|              |     the         |               |                 |
|              |     selected    |               |                 |
|              |     column in   |               |                 |
|              |     the ENS     |               |                 |
|              |     Manager.    |               |                 |
+--------------+-----------------+---------------+-----------------+

: ENSSELECTED Column Descriptions

+----------------+--------------+
| Index Code     | Columns      |
+================+==============+
| PK_ENSSELECTED | GROUPOFID    |
|                |              |
|                | SELECTID     |
|                |              |
|                | SELECTSTRING |
+----------------+--------------+

: ENSSELECTED Index Descriptions

### ENSTRIGGERS

The table is a lookup table containing descriptions of the Event
Notification System (ENS) machine, schedule, and job event triggers.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| TRIGGERCODE | This column      | char (6)      | -   J1: Job      |
|             | contains the     |               |     Submitted    |
|             | triggering       |               | -   J2: Job      |
|             | status codes.    |               |                  |
|             |                  |               |   Initialization |
|             |                  |               |     Error        |
|             |                  |               | -   J3: Job      |
|             |                  |               |     PreRun       |
|             |                  |               |     Failed       |
|             |                  |               | -   J4: Job      |
|             |                  |               |     Missed Start |
|             |                  |               |     Time         |
|             |                  |               | -   J5: Job      |
|             |                  |               |     Exceeded Max |
|             |                  |               |     Runtime      |
|             |                  |               | -   J6: Job      |
|             |                  |               |     Finished OK  |
|             |                  |               | -   J7: Job      |
|             |                  |               |     Failed       |
|             |                  |               | -   J8: Job      |
|             |                  |               |     Marked       |
|             |                  |               |     Finished OK  |
|             |                  |               | -   J9: Job      |
|             |                  |               |     Marked       |
|             |                  |               |     Failed       |
|             |                  |               | -   J10: Job     |
|             |                  |               |     Cancelled    |
|             |                  |               | -   J11: Job     |
|             |                  |               |     Restarted    |
|             |                  |               | -   J12: Job     |
|             |                  |               |     Skipped      |
|             |                  |               | -   J13: Job to  |
|             |                  |               |     be Killed    |
|             |                  |               | -   J14: Job     |
|             |                  |               |     Wait Machine |
|             |                  |               | -   J15: Job     |
|             |                  |               |     Late to      |
|             |                  |               |     Start        |
|             |                  |               | -   J16: Job     |
|             |                  |               |     Late to      |
|             |                  |               |     Finish       |
|             |                  |               | -   J17: Job     |
|             |                  |               |     Still        |
|             |                  |               |     Attempting   |
|             |                  |               |     Start        |
|             |                  |               | -   J18: Job     |
|             |                  |               |     Running      |
|             |                  |               | -   M1: Machine  |
|             |                  |               |     Marked Down  |
|             |                  |               | -   M2: Machine  |
|             |                  |               |     Marked Up    |
|             |                  |               | -   M3: Machine  |
|             |                  |               |     Status       |
|             |                  |               |     changed      |
|             |                  |               | -   M4: Network  |
|             |                  |               |     down         |
|             |                  |               | -   M5: Network  |
|             |                  |               |     Up           |
|             |                  |               | -   M6: Network  |
|             |                  |               |     Status       |
|             |                  |               |     changed      |
|             |                  |               | -   M7: Machine  |
|             |                  |               |     Marked       |
|             |                  |               |     Limited      |
|             |                  |               | -   S1: Schedule |
|             |                  |               |     Start        |
|             |                  |               | -   S2: Schedule |
|             |                  |               |     Complete     |
|             |                  |               | -   S3: Schedule |
|             |                  |               |     Placed on    |
|             |                  |               |     Hold         |
|             |                  |               | -   S4: Schedule |
|             |                  |               |     Released     |
|             |                  |               |     from Hold    |
+-------------+------------------+---------------+------------------+
| TRIGGERNAME | This column      | varchar (255) | None             |
|             | contains the     |               |                  |
|             | name of the ENS  |               |                  |
|             | Event trigger.   |               |                  |
+-------------+------------------+---------------+------------------+

: ENSTRIGGERS Column Descriptions

  Index Code       Columns
  ---------------- -------------
  PK_ENSTRIGGERS   TRIGGERCODE

  : ENSTRIGGERS Index Descriptions

### ENSTRIGINFO

The table is populated by the Event Notification System (ENS) triggers
on the MACHS, SSTATUS, and SMASTER tables. It contains details of
changes to these tables that are potential triggers for ENS
notifications.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDDATE     | This column      | int (4)       | None             |
|             | contains the     |               |                  |
|             | schedule dates.  |               |                  |
+-------------+------------------+---------------+------------------+
| OBJECTID    | -   Machine ID   | int (4)       | None             |
|             |     for changed  |               |                  |
|             |     MACHS row.   |               |                  |
|             | -   Schedule ID  |               |                  |
|             |     for a        |               |                  |
|             |     changed      |               |                  |
|             |     SSTATUS or   |               |                  |
|             |     SMASTER row. |               |                  |
+-------------+------------------+---------------+------------------+
| OBJECTNAME  | -   Machine name | varchar (255) | None             |
|             |     for a        |               |                  |
|             |     changed      |               |                  |
|             |     MACHS row.   |               |                  |
|             | -   Schedule     |               |                  |
|             |     name for a   |               |                  |
|             |     changed      |               |                  |
|             |     SSTATUS row. |               |                  |
|             | -   Job name for |               |                  |
|             |     a changed    |               |                  |
|             |     SMASTER row. |               |                  |
+-------------+------------------+---------------+------------------+
| INTJOBNO    | Internal job     | int (4)       | 0 for a changed  |
|             | number for a     |               | MACHS or SSTATUS |
|             | changed SMASTER  |               | row.             |
|             | row.             |               |                  |
+-------------+------------------+---------------+------------------+
| INSTNO      | Contains a       | int (4)       | None             |
|             | number that      |               |                  |
|             | identifies the   |               |                  |
|             | instance of the  |               |                  |
|             | schedules.       |               |                  |
+-------------+------------------+---------------+------------------+
| MACHID      | This column      | int (4)       | None             |
|             | contains the ID  |               |                  |
|             | of the machine   |               |                  |
|             | the job started  |               |                  |
|             | for a changed    |               |                  |
|             | SMASTER row.     |               |                  |
|             | NULL for a       |               |                  |
|             | changed MACHS or |               |                  |
|             | SSTATUS row.     |               |                  |
+-------------+------------------+---------------+------------------+
| ISNULLMACH  | This column      | int (4)       | None             |
|             | indicates if the |               |                  |
|             | job ran on a     |               |                  |
|             | particular       |               |                  |
|             | machine for a    |               |                  |
|             | changed SMASTER  |               |                  |
|             | row.             |               |                  |
+-------------+------------------+---------------+------------------+
| OBJECTTYPE  | This column      | char (1)      | -   M: Machs     |
|             | contains the     |               | -   S: SSTATUS   |
|             | Object Type.     |               | -   J: SMASTER   |
+-------------+------------------+---------------+------------------+
| FIELDNAME   | This column      | varchar (128) | None             |
|             | contains the     |               |                  |
|             | name of the      |               |                  |
|             | field that       |               |                  |
|             | changed on the   |               |                  |
|             | MACHS, SSTATUS,  |               |                  |
|             | or SMASTER row.  |               |                  |
+-------------+------------------+---------------+------------------+
| CHR_OLDVAL  | This column      | char (1)      | -   0: Not       |
|             | contains         |               |     Processed    |
|             | information      |               | -   1: Processed |
|             | about the old    |               |                  |
|             | value only if    |               |                  |
|             | the field was    |               |                  |
|             | OPERSTATUS or    |               |                  |
|             | NETSTATUS.       |               |                  |
+-------------+------------------+---------------+------------------+
| CHR_NEWVAL  | This column      | char (1)      | None             |
|             | contains         |               |                  |
|             | information      |               |                  |
|             | about the new    |               |                  |
|             | value only if    |               |                  |
|             | the field was    |               |                  |
|             | OPERSTATUS or    |               |                  |
|             | NETSTATUS.       |               |                  |
+-------------+------------------+---------------+------------------+
| INT_OLDVAL  | This column      | smallint (2)  | None             |
|             | contains         |               |                  |
|             | information      |               |                  |
|             | about the old    |               |                  |
|             | value only if    |               |                  |
|             | the field was    |               |                  |
|             | SKDSTATUS,       |               |                  |
|             | STSTATUS,        |               |                  |
|             | JOBSTATUS, or    |               |                  |
|             | MAXMINS.         |               |                  |
+-------------+------------------+---------------+------------------+
| INT_NEWVAL  | This column      | smallint (2)  | None             |
|             | contains the new |               |                  |
|             | information only |               |                  |
|             | if the field was |               |                  |
|             | SKDSTATUS,       |               |                  |
|             | STSTATUS,        |               |                  |
|             | JOBSTATUS, or    |               |                  |
|             | MAXMINS.         |               |                  |
+-------------+------------------+---------------+------------------+
| ENSSTATUS   | This column      | smallint (2)  | -   0: Not       |
|             | contains         |               |     Processed    |
|             | information the  |               | -   1: Processed |
|             | status           |               |                  |
|             | indicating if    |               |                  |
|             | this             |               |                  |
|             | ENSTRINGINFO row |               |                  |
|             | has been         |               |                  |
|             | processed by     |               |                  |
|             | S                |               |                  |
|             | MANotifyHandler. |               |                  |
+-------------+------------------+---------------+------------------+
| ENSTRIGKEY  | This column      | int (4)       | None             |
|             | contains the key |               |                  |
|             | value            |               |                  |
|             | incremented as   |               |                  |
|             | each new row is  |               |                  |
|             | inserted into    |               |                  |
|             | ENSTRIGINFO.     |               |                  |
+-------------+------------------+---------------+------------------+

: ENSTRIGINFO Column Descriptions

  Index Code       Columns
  ---------------- ------------
  PK_ENSTRIGINFO   ENSTRIGKEY

  : ENSTRIGINFO Index Descriptions

### Escalation

The primary table [Escalation]{.GeneralEscalatedNotificationCapitalized} contains the details and status of a notification
[escalation]{.GeneralEscalatedNotification}.
  Column Name           Explanation                                                                                                                                           Data Type       Additional Information
  --------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------- --------------- -------------------------------------------------------
  EscalationId          This column contains [escalation]{.GeneralEscalatedNotification} IDs that uniquely identify each [escalation]{.GeneralEscalatedNotification}.         int (4)         The EscalationRecipient table references this column.   EscalationRuleId      This column contains the ID of the [escalation]{.GeneralEscalatedNotification} rule that triggered the [escalation]{.GeneralEscalatedNotification}.   int (4)         None
  EscalationSequence    This column contains the ID of the current [escalation]{.GeneralEscalatedNotification} sequence (level).                                              smallint (2)    None   EscalationStatus      This column contains the status of the [escalation]{.GeneralEscalatedNotification}.                                                                   int (4)         None
  Attempts              This column contains the number of attempts that have been made to escalate the notification to the current level.                                    int (4)         None
  LastMessageSent       This column contains the time the most recent [escalation]{.GeneralEscalatedNotification} message was sent out.                                       datetime (8)    None   ActionMessage         This column holds the content from the ACTIONMSG column on the ENSMESSAGES table but with tokens resolved.                                            varchar (max)   None
  TriggerName           This column contains the name of the ENS trigger being escalated.                                                                                     varchar (255)   None
  MachineName           This column contains the machine name.                                                                                                                char (24)       None
  ScheduleDate          This column contains the schedule date where relevant.                                                                                                int (4)         None
  ScheduleName          This column contains the schedule name where relevant.                                                                                                varchar (255)   None
  InstanceNumber        This column contains the schedule instance number where relevant.                                                                                     int (4)         None
  JobName               This column contains the job name where relevant.                                                                                                     varchar (150)   None
  ActionID              This column contains the ACTIONID from the ENSMESSAGES table.                                                                                         int (4)         None
  ActionType            This column contains the ACTIONTYPE from the ENSMESSAGES table.                                                                                       int (4)         None
  GroupOfId             This column contains the GROUPOFID from the ENSMESSAGES table.                                                                                        int (4)         None
  ActionName            This column contains the ACTIONNAME from the ENSMESSAGES table.                                                                                       varchar (255)   None
  ActionIncludeId       This column contains the ACTIONINCID from the ENSMESSAGES table.                                                                                      char (1)        None
  NotifyDelimiter       This column contains the Notify delimiter from the NOTIFY table.                                                                                      char (1)        None
  AcknowledgedBy        This column contains the USERSIGNON of the user who acknowledged the [escalation]{.GeneralEscalatedNotification}.                                     char (512)      None   AcknowledgeTime       This column contains the time the [escalation]{.GeneralEscalatedNotification} was acknowledged.                                                       datetime (8)    None
  AcknowledgeHostName   This column contains the name of the host from which the acknowledgment was made.                                                                     varchar (100)   None

  : Escalation Column Descriptions

  Index Code      Columns
  --------------- --------------
  PK_Escalation   EscalationId

  : Escalation Index Descriptions

### EscalationGroup

The primary table EscalationGroup contains an ID and name for a
collection of roles that are associated together for purposes of
[escalation]{.GeneralEscalatedNotification} of notifications.
  Column Name           Explanation                                                                                                                                                 Data Type        Additional Information
  --------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------- -------------------------------------------------------------------------------------
  EscalationGroupId     This column contains [escalation]{.GeneralEscalatedNotification} group IDs that uniquely identify each [escalation]{.GeneralEscalatedNotification} group.   int (4)          The EscalationGroupRole and EscalationGroupENSMessage tables reference this column.   EscalationGroupName   This column contains [escalation]{.GeneralEscalatedNotification} group names.                                                                               nvarchar (128)   None

  : EscalationGroup Column Descriptions

  Index Code           Columns
  -------------------- -------------------
  PK_EscalationGroup   EscalationGroupId

  : EscalationGroup Index Descriptions

### EscalationGroupUser

The primary table EscalationGroupUser is a relationship table that links
OpCon users with [escalation]{.GeneralEscalatedNotification} groups for notifications.

+----------------+----------------+----------------+----------------+
| Column Name    | Explanation    | Data Type      | Additional     |
|                |                |                | Information    |
+================+================+================+================+
| Esc            | This column    | int (4)        | The            |
| alationGroupId | contains       |                | E              |
|                | [              |                | scalationGroup | |                | escalation]{.G |                | table is       |
|                | eneralEscalate |                | referenced     |
|                | dNotification} |                | from this      |
|                | group IDs that |                | table via this |
|                | identify       |                | field.         |
|                | [              |                |                | |                | escalation]{.G |                |                |
|                | eneralEscalate |                |                |
|                | dNotification} |                |                |
|                | groups         |                |                |
|                | associated     |                |                |
|                | with           |                |                |
|                | notification   |                |                |
|                | [escalati      |                |                | |                | ons]{.GeneralE |                |                |
|                | scalatedNotifi |                |                |
|                | cationPlural}. |                |                |
+----------------+----------------+----------------+----------------+
| UserSignon     | This column    | nvarchar (255) | -   The USERS  |
|                | contains OpCon |                |     table is   |
|                | user logins    |                |     referenced |
|                | that identify  |                |     from this  |
|                | users          |                |     table via  |
|                | associated     |                |     this       |
|                | with           |                |     field.     |
|                | [              |                |                | |                | escalation]{.G |                | -   However,   |
|                | eneralEscalate |                |     since      |
|                | dNotification} |                |     there is a |
|                | groups.        |                |                |
|                |                |                |    requirement |
|                |                |                |     for this   |
|                |                |                |     to be      |
|                |                |                |     tokenized, |
|                |                |                |     there is   |
|                |                |                |     no foreign |
|                |                |                |     key        |
|                |                |                |                |
|                |                |                |   relationship |
|                |                |                |                |
|                |                |                |    implemented |
|                |                |                |     in the     |
|                |                |                |     database.  |
+----------------+----------------+----------------+----------------+

: EscalationGroupUser Column Descriptions

+------------------------+-------------------+
| Index Code             | Columns           |
+========================+===================+
| PK_EscalationGroupUser | EscalationGroupId |
|                        |                   |
|                        | UserSignon        |
+------------------------+-------------------+

: EscalationGroupUser Index Descriptions

### EscalationHistory

The primary table EscalationHistory contains the details and status of a
notification [escalation]{.GeneralEscalatedNotification} retained for historical purposes.

  Column Name           Explanation                                                                                                                                           Data Type       Additional Information
  --------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------- --------------- --------------------------------------------------------------
  EscalationId          This column contains [escalation]{.GeneralEscalatedNotification} IDs that uniquely identify each [escalation]{.GeneralEscalatedNotification}.         int (4)         The EscalationHistoryRecipient table references this column.   EscalationRuleId      This column contains the ID of the [escalation]{.GeneralEscalatedNotification} rule that triggered the [escalation]{.GeneralEscalatedNotification}.   int (4)         None
  EscalationSequence    This column contains the ID of the current [escalation]{.GeneralEscalatedNotification} sequence (level).                                              smallint (2)    None   EscalationStatus      This column contains the status of the [escalation]{.GeneralEscalatedNotification}.                                                                   int (4)         None
  Attempts              This column contains the number of attempts that have been made to escalate the notification to the current level.                                    int (4)         None
  LastMessageSent       This column contains the time the most recent [escalation]{.GeneralEscalatedNotification} message was sent out.                                       datetime (8)    None   ActionMessage         This column holds the content from the ACTIONMSG column on the ENSMESSAGES table but with tokens resolved.                                            varchar (max)   None
  TriggerName           This column contains the name of the ENS trigger being escalated.                                                                                     varchar (255)   None
  MachineName           This column contains the machine name.                                                                                                                char (24)       None
  ScheduleDate          This column contains the schedule date where relevant.                                                                                                int (4)         None
  ScheduleName          This column contains the schedule name where relevant.                                                                                                varchar (255)   None
  InstanceNumber        This column contains the schedule instance number where relevant.                                                                                     int (4)         None
  JobName               This column contains the job name where relevant.                                                                                                     varchar (150)   None
  ActionID              This column contains the ACTIONID from the ENSMESSAGES table.                                                                                         int (4)         None
  ActionType            This column contains the ACTIONTYPE from the ENSMESSAGES table.                                                                                       int (4)         None
  GroupOfId             This column contains the GROUPOFID from the ENSMESSAGES table.                                                                                        int (4)         None
  ActionName            This column contains the ACTIONNAME from the ENSMESSAGES table.                                                                                       varchar (255)   None
  ActionIncludeId       This column contains the ACTIONINCID from the ENSMESSAGES table.                                                                                      char (1)        None
  NotifyDelimiter       This column contains the Notify delimiter from the NOTIFY table.                                                                                      char (1)        None
  AcknowledgedBy        This column contains the USERSIGNON of the user who acknowledged the [escalation]{.GeneralEscalatedNotification}.                                     char (512)      None   AcknowledgeTime       This column contains the time the [escalation]{.GeneralEscalatedNotification} was acknowledged.                                                       datetime (8)    None
  AcknowledgeHostName   This column contains the name of the host from which the acknowledgment was made.                                                                     varchar (100)   None

  : EscalationHistory Column Descriptions

  Index Code             Columns
  ---------------------- --------------
  PK_EscalationHistory   EscalationId

  : EscalationHistory Index Descriptions

### EscalationRecipient

The primary table EscalationRecipient contains an ID, OpCon login, and
email address for a recipient of a notification
[escalation]{.GeneralEscalatedNotification}.
  Column Name             Explanation                                                                                                                                                               Data Type        Additional Information
  ----------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------- ------------------------
  EscalationRecipientId   This column contains EscalationRecipient IDs that uniquely identify each recipient of a notification [escalation]{.GeneralEscalatedNotification}.                         int (4)          None   EscalationId            This column contains the ID of the notification [escalation]{.GeneralEscalatedNotification} that was sent to the [escalation]{.GeneralEscalatedNotification} recipient.   int (4)          None
  UserSignOn              This column contains the OpCon USERSIGNON of the [escalation]{.GeneralEscalatedNotification} recipient.                                                                   char (512)       None   Email                   This column contains the email address of the [escalation]{.GeneralEscalatedNotification} recipient.                                                                      varchar (4000)   None
  EscalationSequence      This column contains the sequence of the [escalation]{.GeneralEscalatedNotification}.                                                                                     smallint (2)     None
  : EscalationRecipient Column Descriptions

  Index Code               Columns
  ------------------------ -----------------------
  PK_EscalationRecipient   EscalationRecipientId

  : EscalationRecipient Index Descriptions

### EscalationRecipientHistory

The primary table EscalationRecipientHistory contains the history of the
mapping between notification
[escalations]{.GeneralEscalatedNotificationPlural} and their recipients, i.e., which notification
[escalations]{.GeneralEscalatedNotificationPlural} were sent to whom.
  Column Name             Explanation                                                                                                                                                               Data Type        Additional Information
  ----------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------- ------------------------
  EscalationRecipientId   This column contains EscalationRecipient IDs that uniquely identify each recipient of a notification [escalation]{.GeneralEscalatedNotification}.                         int (4)          None   EscalationId            This column contains the ID of the notification [escalation]{.GeneralEscalatedNotification} that was sent to the [escalation]{.GeneralEscalatedNotification} recipient.   int (4)          None
  UserSignOn              This column contains the OpCon USERSIGNON of the [escalation]{.GeneralEscalatedNotification} recipient.                                                                   char (512)       None   Email                   This column contains the email address of the [escalation]{.GeneralEscalatedNotification} recipient.                                                                      varchar (4000)   None
  EscalationSequence      This column contains the sequence of the [escalation]{.GeneralEscalatedNotification}.                                                                                     smallint (2)     None
  : EscalationRecipientHistory Column Descriptions

  Index Code                      Columns
  ------------------------------- -----------------------
  PK_EscalationRecipientHistory   EscalationRecipientId

  : EscalationRecipientHistory Index Descriptions

### EscalationRule

The primary table EscalationRule contains an ID and name for a
collection of rules created for purposes of
[escalation]{.GeneralEscalatedNotification} of notifications.
  Column Name             Explanation                                                                                                                                         Data Type        Additional Information
  ----------------------- --------------------------------------------------------------------------------------------------------------------------------------------------- ---------------- ------------------------------------------------------------------------------------
  EscalationRecipientId   This column contains EscalationRecipient IDs that uniquely identify each recipient of a notification [escalation]{.GeneralEscalatedNotification}.   int (4)          The EscalationRuleGroup and EscalationRuleENSMessage tables reference this column.   EscalationRuleName      This column contains [escalation]{.GeneralEscalatedNotification} rule names.                                                                        nvarchar (128)   None

  : EscalationRule Column Descriptions

  Index Code          Columns
  ------------------- ------------------
  PK_EscalationRule   EscalationRuleId

  : EscalationRule Index Descriptions

### EscalationRuleENSMessage

The primary table EscalationRuleENSMessage is a relationship table that
links [escalation]{.GeneralEscalatedNotification} rules for notifications with notification messages.

  Column Name        Explanation                                                                                                                                                                                                                  Data Type   Additional Information
  ------------------ ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------- ------------------------------------------------------------------------
  EscalationRuleId   This column contains [escalation]{.GeneralEscalatedNotification} rule IDs that identify [escalation]{.GeneralEscalatedNotification} rules associated with notification [escalations]{.GeneralEscalatedNotificationPlural}.   int (4)     The EscalationRule table is referenced from this table via this field.   GroupofId          This column contains ENS group IDs that identify groups of notifications.                                                                                                                                                    int (4)     The ENSMESSAGES table is referenced from this table via this field.
  ActionId           This column contains ENS action IDs that identify notification actions.                                                                                                                                                      int (4)     The ENSMESSAGES table is referenced from this table via this field.
  ActionType         This column contains ENS action types that identify the type of notification that will be sent.                                                                                                                              int (4)     The ENSMESSAGES table is referenced from this table via this field.

  : EscalationRuleENSMessage Column Descriptions

+-----------------------------+------------------+
| Index Code                  | Columns          |
+=============================+==================+
| PK_EscalationRuleENSMessage | EscalationRuleId |
|                             |                  |
|                             | GroupofId        |
|                             |                  |
|                             | ActionId         |
|                             |                  |
|                             | ActionType       |
+-----------------------------+------------------+

: EscalationRuleENSMessage Index Descriptions

### EscalationSequence

The primary table EscalationSequence is a relationship table that links
[escalation]{.GeneralEscalatedNotification} rules for notifications with [escalation]{.GeneralEscalatedNotification} groups. It also further
describes the rule further in terms of levels of
[escalation]{.GeneralEscalatedNotification}, [escalation]{.GeneralEscalatedNotification} intervals, and other
categories.

  Column Name            Explanation                                                                                                                                                                                                                  Data Type        Additional Information
  ---------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------- -------------------------------------------------------------------------
  EscalationSequenceId   This column contains [escalation]{.GeneralEscalatedNotification} sequence IDs that identify sequences associated with notification [escalation]{.GeneralEscalatedNotification} level rules and groups.                       int (4)          None   EscalationRuleId       This column contains [escalation]{.GeneralEscalatedNotification} rule IDs that identify [escalation]{.GeneralEscalatedNotification} rules associated with notification [escalations]{.GeneralEscalatedNotificationPlural}.   int (4)          The EscalationRule table is referenced from this table via this field.
  EscalationGroupId      This column contains [escalation]{.GeneralEscalatedNotification} group IDs that identify groups associated with notification [escalations]{.GeneralEscalatedNotificationPlural}.                                             int (4)          The EscalationGroup table is referenced from this table via this field.   Sequence               This column contains sequence numbers associated with [escalation]{.GeneralEscalatedNotification} rule and group pairs.                                                                                                      smallint (2)     None
  AttemptLimit           This column contains the maximum number of times that an [escalation]{.GeneralEscalatedNotification} message will be sent before escalating to the next level.                                                               smallint (2)     None   AttemptInterval        This column contains the interval in minutes between attempts to send an [escalation]{.GeneralEscalatedNotification} message.                                                                                                smallint (2)     None
  Name                   This column contains names for the [escalation]{.GeneralEscalatedNotification} levels.                                                                                                                                       nvarchar (128)   None
  : EscalationSequence Column Descriptions

  Index Code              Columns
  ----------------------- ----------------------
  PK_EscalationSequence   EscalationSequenceId

  : EscalationSequence Index Descriptions

### EVENTLOG

The SAM, while processing events, accesses the EVENTLOG table used for
storing Event information.

+-------------+-------------------+------------+-------------------+
| Column Name | Explanation       | Data Type  | Additional        |
|             |                   |            | Information       |
+=============+===================+============+===================+
| DATETIME    | This column       | float (8)  | -   This column   |
|             | contains the      |            |     contains the  |
|             | dates and times   |            |     date/time     |
|             | the table         |            |     stamp in SQL  |
|             | receives the      |            |     format.       |
|             | event data.       |            | -   The integer   |
|             |                   |            |     part of the   |
|             |                   |            |     SQL date      |
|             |                   |            |     represents    |
|             |                   |            |     the day count |
|             |                   |            |     since         |
|             |                   |            |     Saturday,     |
|             |                   |            |     December      |
|             |                   |            |     30, 1899.     |
|             |                   |            | -   The           |
|             |                   |            |     fractional    |
|             |                   |            |     part of the   |
|             |                   |            |     SQL date      |
|             |                   |            |     represents    |
|             |                   |            |     the time in   |
|             |                   |            |     seconds since |
|             |                   |            |     midnight.     |
+-------------+-------------------+------------+-------------------+
| EVDETS      | This column       | char (124) | The format of     |
|             | contains the      |            | external events   |
|             | event details.    |            | is identical to   |
|             |                   |            | internal events   |
|             |                   |            | found on the Job  |
|             |                   |            | Master \> Events  |
|             |                   |            | tab in the        |
|             |                   |            | Enterprise        |
|             |                   |            | Manager.          |
+-------------+-------------------+------------+-------------------+
| USERSIGNON  | This column       | char (20)  | None              |
|             | contains User     |            |                   |
|             | Login IDs and     |            |                   |
|             | external event    |            |                   |
|             | passwords.        |            |                   |
+-------------+-------------------+------------+-------------------+

: EVENTLOG Column Descriptions

+-------------+----------+
| Index Code  | Columns  |
+=============+==========+
| PK_EVENTLOG | DATETIME |
|             |          |
|             | EVDETS   |
+-------------+----------+

: EVENTLOG Index Descriptions

### FEATURES

This table is reserved for internal use by SMA Technologies.

### FUNCDESC

The primary table FUNCDESC contains base information describing Function
Privileges. This table is part of the internal security mechanism.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| FUNCID      | -   This column  | smallint (2) | None             |
|             |     contains     |              |                  |
|             |     function     |              |                  |
|             |     IDs.         |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     from the     |              |                  |
|             |     UDEPFUN      |              |                  |
|             |     table.       |              |                  |
+-------------+------------------+--------------+------------------+
| FUNCDESC    | This column      | char (40)    | None             |
|             | contains the     |              |                  |
|             | description of   |              |                  |
|             | the function     |              |                  |
|             | privileges.      |              |                  |
+-------------+------------------+--------------+------------------+
| DEPTALFUN   | This column      | smallint (2) | -   0:           |
|             | contains the     |              |                  |
|             | flag determining |              | Non-Departmental |
|             | if each function |              | -   1:           |
|             | privilege is     |              |     Departmental |
|             | Departmental or  |              |                  |
|             | N                |              |                  |
|             | on-Departmental. |              |                  |
+-------------+------------------+--------------+------------------+

: FUNCDESC Column Descriptions

  Index Code    Columns
  ------------- ---------
  PK_FUNCDESC   FUNCID

  : FUNCDESC Index Descriptions

### HISTARC

The primary table HISTARC contains History information archived from the
HISTORY table.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains     |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains job |               |                  |
|             |     names.       |               |                  |
|             | -   Job names    |               |                  |
|             |     must be      |               |                  |
|             |     unique       |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| INTJOBNO    | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     internal     |               |                  |
|             |     unique job   |               |                  |
|             |     numbers.     |               |                  |
|             | -   The SAM      |               |                  |
|             |     assigns      |               |                  |
|             |     these        |               |                  |
|             |     numbers at   |               |                  |
|             |     job run      |               |                  |
|             |     time.        |               |                  |
+-------------+------------------+---------------+------------------+
| SKDDATE     | This column      | int (4)       | -   This column  |
|             | contains the     |               |     contains the |
|             | schedule dates.  |               |     schedule     |
|             |                  |               |     date in SQL  |
|             |                  |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
+-------------+------------------+---------------+------------------+
| JSTART      | This column      | float (8)     | -   This column  |
|             | contains the     |               |     contains the |
|             | start dates and  |               |     date/time    |
|             | start times of   |               |     stamp in SQL |
|             | the jobs.        |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| JSTAT       | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     termination  |               |                  |
|             |     statuses of  |               |                  |
|             |     the jobs.    |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     job statuses |               |                  |
|             |     from the     |               |                  |
|             |     SMASTER      |               |                  |
|             |     table.       |               |                  |
|             | -   For          |               |                  |
|             |     reporting    |               |                  |
|             |     purposes,    |               |                  |
|             |     the column   |               |                  |
|             |     can be       |               |                  |
|             |                  |               |                  |
|             | cross-referenced |               |                  |
|             |     with the     |               |                  |
|             |     JSTATMAP     |               |                  |
|             |     table, where |               |                  |
|             |     the STSTATUS |               |                  |
|             |     column is    |               |                  |
|             |     set to 900   |               |                  |
|             |     and the      |               |                  |
|             |     JOBSTATUS    |               |                  |
|             |     column is    |               |                  |
|             |     equal to the |               |                  |
|             |     JSTAT        |               |                  |
|             |     column.      |               |                  |
+-------------+------------------+---------------+------------------+
| JTERM       | This column      | float (8)     | -   This column  |
|             | contains the end |               |     contains the |
|             | dates and end    |               |     date/time    |
|             | times of the     |               |     stamp in SQL |
|             | jobs.            |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| JRUN        | This column      | int (4)       | The job run time |
|             | contains the run |               | is in minutes.   |
|             | times of the     |               |                  |
|             | jobs.            |               |                  |
+-------------+------------------+---------------+------------------+
| JMACH       | -   This column  | char (24)     | None             |
|             |     contains the |               |                  |
|             |     machines for |               |                  |
|             |     the jobs.    |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     names of the |               |                  |
|             |     machines     |               |                  |
|             |     that         |               |                  |
|             |     processed    |               |                  |
|             |     the jobs.    |               |                  |
+-------------+------------------+---------------+------------------+
| JDESC       | This column      | varchar (255) | This column      |
|             | contains the     |               | contains the     |
|             | termination      |               | 20-character job |
|             | descriptions of  |               | termination      |
|             | the jobs.        |               | string received  |
|             |                  |               | from the LSAM.   |
+-------------+------------------+---------------+------------------+
| DEPTID      | This column      | int (4)       | None             |
|             | contains the     |               |                  |
|             | department IDs   |               |                  |
|             | associated with  |               |                  |
|             | the jobs.        |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | This column      | char (20)     | None             |
|             | contains the     |               |                  |
|             | frequency names  |               |                  |
|             | associated with  |               |                  |
|             | the jobs.        |               |                  |
+-------------+------------------+---------------+------------------+

: HISTARC Column Descriptions

+------------+----------+
| Index Code | Columns  |
+============+==========+
| PK_HISTARC | SKDID    |
|            |          |
|            | JOBNAME  |
|            |          |
|            | INTJOBNO |
+------------+----------+

: HISTARC Index Descriptions

### HISTARC_AUX

The secondary table HISTARC_AUX contains auxiliary information
describing archived history data. The combination of Schedule ID, Job
Name, and Internal Unique Job Number links the auxiliary information to
the correct record in the HISTARC primary table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| JOBNAME     | -   This column | varchar (128)  | None            |
|             |     contains    |                |                 |
|             |     the job     |                |                 |
|             |     names.      |                |                 |
|             | -   The job     |                |                 |
|             |     names must  |                |                 |
|             |     be unique   |                |                 |
|             |     within each |                |                 |
|             |     schedule.   |                |                 |
|             | -   The         |                |                 |
|             |     schedule ID |                |                 |
|             |     (SKDID)     |                |                 |
|             |     identifies  |                |                 |
|             |     the         |                |                 |
|             |     schedule.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| INTJOBNO    | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     internal    |                |                 |
|             |     unique job  |                |                 |
|             |     numbers.    |                |                 |
|             | -   The SAM     |                |                 |
|             |     assigns     |                |                 |
|             |     these       |                |                 |
|             |     numbers at  |                |                 |
|             |     job run     |                |                 |
|             |     time.       |                |                 |
+-------------+-----------------+----------------+-----------------+
| SKDDATE     | This column the | int (4)        | -   This column |
|             | schedule dates. |                |     contains    |
|             |                 |                |     the         |
|             |                 |                |     schedule    |
|             |                 |                |     date in SQL |
|             |                 |                |     format.     |
|             |                 |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| HAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| HASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| HAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| HATEXT      | This column is  | text (16)      | None            |
|             | reserved for    |                |                 |
|             | future use.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| HATEXTLEN   | This column is  | int (4)        | None            |
|             | reserved for    |                |                 |
|             | future use.     |                |                 |
+-------------+-----------------+----------------+-----------------+

: HISTARC_AUX Column Descriptions

+---------------+----------+
| Index Code    | Columns  |
+===============+==========+
| PK_HISTARCAUX | SKDID    |
|               |          |
|               | JOBNAME  |
|               |          |
|               | INTJOBNO |
|               |          |
|               | SKDDATE  |
|               |          |
|               | HAFC     |
|               |          |
|               | HASEQNO  |
+---------------+----------+

: HISTARC_AUX Index Descriptions

### HISTORY {#history style="margin-top: 30pt;"}

The primary HISTORY table contains History information regarding
execution of every job. The SAM inserts all job history records. The Job
Execution History screen of the Enterprise Manager and the History
Management utility display the job history. The History.exe command-line
utility is used to maintain the data.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains     |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The jobs     |               |                  |
|             |     name must be |               |                  |
|             |     unique       |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| INTJOBNO    | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     internal     |               |                  |
|             |     unique job   |               |                  |
|             |     numbers.     |               |                  |
|             | -   The SAM      |               |                  |
|             |     assigns      |               |                  |
|             |     these        |               |                  |
|             |     numbers at   |               |                  |
|             |     job run      |               |                  |
|             |     time.        |               |                  |
+-------------+------------------+---------------+------------------+
| SKDDATE     | This column the  | int (4)       | -   This column  |
|             | schedule dates.  |               |     contains the |
|             |                  |               |     schedule     |
|             |                  |               |     date in SQL  |
|             |                  |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
+-------------+------------------+---------------+------------------+
| JSTART      | This column      | float (8)     | -   This column  |
|             | contains the     |               |     contains the |
|             | start dates and  |               |     date/time    |
|             | start times of   |               |     stamp in SQL |
|             | the jobs.        |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| JSTAT       | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     termination  |               |                  |
|             |     statuses of  |               |                  |
|             |     the jobs.    |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     job statuses |               |                  |
|             |     from the     |               |                  |
|             |     SMASTER      |               |                  |
|             |     table.       |               |                  |
|             | -   For          |               |                  |
|             |     reporting    |               |                  |
|             |     purposes,    |               |                  |
|             |     the column   |               |                  |
|             |     can be       |               |                  |
|             |                  |               |                  |
|             | cross-referenced |               |                  |
|             |     with the     |               |                  |
|             |     JSTATMAP     |               |                  |
|             |     table, where |               |                  |
|             |     the STSTATUS |               |                  |
|             |     column is    |               |                  |
|             |     set to 900   |               |                  |
|             |     and the      |               |                  |
|             |     JOBSTATUS    |               |                  |
|             |     column is    |               |                  |
|             |     equal to     |               |                  |
|             |     JSTAT        |               |                  |
|             |     column.      |               |                  |
+-------------+------------------+---------------+------------------+
| JTERM       | This column      | float (8)     | -   This column  |
|             | contains the end |               |     contains the |
|             | dates and end    |               |     date/time    |
|             | times of the     |               |     stamp in SQL |
|             | jobs.            |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| JRUN        | This column      | int (4)       | The job run time |
|             | contains the job |               | is in minutes.   |
|             | run times.       |               |                  |
+-------------+------------------+---------------+------------------+
| JMACH       | -   This column  | char (24)     | None             |
|             |     contains the |               |                  |
|             |     machines for |               |                  |
|             |     the jobs.    |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     names of the |               |                  |
|             |     machines     |               |                  |
|             |     that         |               |                  |
|             |     processed    |               |                  |
|             |     the jobs.    |               |                  |
+-------------+------------------+---------------+------------------+
| JDESC       | This column      | varchar (255) | This column      |
|             | contains the     |               | contains the     |
|             | termination      |               | 20-character job |
|             | descriptions of  |               | termination      |
|             | the jobs.        |               | string received  |
|             |                  |               | from the LSAM.   |
+-------------+------------------+---------------+------------------+
| DEPTID      | This column      | int (4)       | None             |
|             | contains the     |               |                  |
|             | department IDs   |               |                  |
|             | associated with  |               |                  |
|             | the jobs.        |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | This column      | char (20)     | None             |
|             | contains the     |               |                  |
|             | frequency names  |               |                  |
|             | associated with  |               |                  |
|             | the jobs.        |               |                  |
+-------------+------------------+---------------+------------------+

: HISTORY Column Descriptions

+------------+----------+
| Index Code | Columns  |
+============+==========+
| PK_HISTORY | SKDID    |
|            |          |
|            | JOBNAME  |
|            |          |
|            | INTJOBNO |
|            |          |
|            | SKDDATE  |
+------------+----------+

: HISTORY Index Descriptions

### HISTORY_AUX

The secondary table HISTORY_AUX contains auxiliary information
describing Job History data. The combination of Schedule ID, Job Name,
and Internal Unique Job Number links the auxiliary information to the
correct record in the HISTORY primary table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| JOBNAME     | -   This column | varchar (128)  | None            |
|             |     contains    |                |                 |
|             |     the job     |                |                 |
|             |     names.      |                |                 |
|             | -   The jobs    |                |                 |
|             |     name must   |                |                 |
|             |     be unique   |                |                 |
|             |     within each |                |                 |
|             |     schedule.   |                |                 |
|             | -   The         |                |                 |
|             |     schedule ID |                |                 |
|             |     (SKDID)     |                |                 |
|             |     identifies  |                |                 |
|             |     the         |                |                 |
|             |     schedule.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| INTJOBNO    | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     internal    |                |                 |
|             |     unique job  |                |                 |
|             |     numbers.    |                |                 |
|             | -   The SAM     |                |                 |
|             |     assigns     |                |                 |
|             |     these       |                |                 |
|             |     numbers at  |                |                 |
|             |     job run     |                |                 |
|             |     time.       |                |                 |
+-------------+-----------------+----------------+-----------------+
| SKDDATE     | This column the | int (4)        | -   This column |
|             | schedule dates. |                |     contains    |
|             |                 |                |     the         |
|             |                 |                |     schedule    |
|             |                 |                |     date in SQL |
|             |                 |                |     format.     |
|             |                 |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| HAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| HASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| HAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| HATEXT      | This column is  | text           | None            |
|             | reserved for    |                |                 |
|             | future use.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| HATEXTLEN   | This column is  | int (4)        | None            |
|             | reserved for    |                |                 |
|             | future use.     |                |                 |
+-------------+-----------------+----------------+-----------------+

: HISTORY_AUX Column Descriptions

+---------------+----------+
| Index Code    | Columns  |
+===============+==========+
| PK_HISTORYAUX | SKDID    |
|               |          |
|               | JOBNAME  |
|               |          |
|               | INTJOBNO |
|               |          |
|               | SKDDATE  |
|               |          |
|               | HAFC     |
|               |          |
|               | HASEQNO  |
+---------------+----------+

: HISTORY_AUX Index Descriptions

### INSTANTMESSAGES

The table contains the messages associated with test notifications
generated via the ENS Manager utility as well as notifications generated
through the use of $NOTIFY:\<action\> OpCon events.

+---------------+----------------+----------------+----------------+
| Column Name   | Explanation    | Data Type      | Additional     |
|               |                |                | Information    |
+===============+================+================+================+
| ACTIONID      | This column    | int (4)        | None           |
|               | consists of    |                |                |
|               | the Action IDs |                |                |
|               | from the       |                |                |
|               | ENSACTIONS     |                |                |
|               | Table.         |                |                |
+---------------+----------------+----------------+----------------+
| ACTIONTYPE    | This column    | int (4)        | -   1: Event   |
|               | consists of    |                |     Log        |
|               | notification   |                | -   2: Email   |
|               | type required. |                | -   3: Net     |
|               |                |                |     Send       |
|               |                |                | -   4: SNMP    |
|               |                |                | -   5: SPO     |
|               |                |                | -   6: Text    |
|               |                |                |     Message    |
|               |                |                | -   7:         |
|               |                |                |     OpCon/xps  |
|               |                |                |     Event      |
|               |                |                | -   10: Run    |
|               |                |                |     Command    |
+---------------+----------------+----------------+----------------+
| ACTIONMSG     | This column    | varchar (4000) | None           |
|               | consists of    |                |                |
|               | the message    |                |                |
|               | content for    |                |                |
|               | the            |                |                |
|               | notification.  |                |                |
+---------------+----------------+----------------+----------------+
| ACTIONSTATUS  | This column    | smallint (2)   | -   0: Not     |
|               | consists of    |                |     Processed  |
|               | the status     |                | -   1:         |
|               | indicating if  |                |     Processed  |
|               | this           |                |                |
|               | I              |                |                |
|               | NSTANTMESSAGES |                |                |
|               | row has been   |                |                |
|               | processed by   |                |                |
|               | SMA            |                |                |
|               | NotifyHandler. |                |                |
+---------------+----------------+----------------+----------------+
| ACTIONTRIGGER | This column    | varchar (255)  | None           |
|               | indicates if   |                |                |
|               | the trigger is |                |                |
|               | a Test         |                |                |
|               | Notification   |                |                |
|               | for ENS        |                |                |
|               | Manager or an  |                |                |
|               | OpCon/xps      |                |                |
|               | Event via the  |                |                |
|               | \              |                |                |
|               | $NOTIFY:ACTION |                |                |
|               | event.         |                |                |
+---------------+----------------+----------------+----------------+

: INSTANTMESSAGES Column Descriptions

  Index Code           Columns
  -------------------- ----------
  PK_INSTANTMESSAGES   ACTIONID

  : INSTANTMESSAGES Index Descriptions

### JDEPJOB

The secondary table JDEPJOB contains the Job Dependency details for the
JMASTER primary table.

+---------------+-----------------+---------------+-----------------+
| Column Name   | Explanation     | Data Type     | Additional      |
|               |                 |               | Information     |
+===============+=================+===============+=================+
| SKDID         | -   This column | int (4)       | None            |
|               |     contains    |               |                 |
|               |     the         |               |                 |
|               |     schedule    |               |                 |
|               |     IDs.        |               |                 |
|               | -   This column |               |                 |
|               |     contains    |               |                 |
|               |                 |               |                 |
|               | cross-reference |               |                 |
|               |     information |               |                 |
|               |     for lookup  |               |                 |
|               |     into the    |               |                 |
|               |     SNAME       |               |                 |
|               |     table.      |               |                 |
+---------------+-----------------+---------------+-----------------+
| JOBNAME       | -   This column | varchar (128) | None            |
|               |     contains    |               |                 |
|               |     the job     |               |                 |
|               |     names.      |               |                 |
|               | -   The jobs    |               |                 |
|               |     name must   |               |                 |
|               |     be unique   |               |                 |
|               |     within each |               |                 |
|               |     schedule.   |               |                 |
|               | -   The         |               |                 |
|               |     schedule ID |               |                 |
|               |     (SKDID)     |               |                 |
|               |     identifies  |               |                 |
|               |     the         |               |                 |
|               |     schedule.   |               |                 |
+---------------+-----------------+---------------+-----------------+
| FREQNAME      | -   This column | char (20)     | None            |
|               |     contains    |               |                 |
|               |     the         |               |                 |
|               |     frequency   |               |                 |
|               |     names.      |               |                 |
|               | -   The         |               |                 |
|               |     frequency   |               |                 |
|               |     name must   |               |                 |
|               |     be unique   |               |                 |
|               |     within a    |               |                 |
|               |     job.        |               |                 |
|               | -   The job     |               |                 |
|               |     name        |               |                 |
|               |     (JOBNAME)   |               |                 |
|               |     identifies  |               |                 |
|               |     the job.    |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPSKDID      | -   This column | int (4)       | None            |
|               |     contains    |               |                 |
|               |     the         |               |                 |
|               |     dependency  |               |                 |
|               |     schedule    |               |                 |
|               |     IDs.        |               |                 |
|               | -   This column |               |                 |
|               |     contains    |               |                 |
|               |     the IDs of  |               |                 |
|               |     the         |               |                 |
|               |     Schedule    |               |                 |
|               |     containing  |               |                 |
|               |     the jobs in |               |                 |
|               |     job         |               |                 |
|               |                 |               |                 |
|               |    dependencies |               |                 |
|               |     (in the     |               |                 |
|               |     DEPJOBNAME  |               |                 |
|               |     column).    |               |                 |
|               | -   This column |               |                 |
|               |     contains    |               |                 |
|               |                 |               |                 |
|               | cross-reference |               |                 |
|               |     information |               |                 |
|               |     for lookup  |               |                 |
|               |     into the    |               |                 |
|               |     SNAME       |               |                 |
|               |     table.      |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPJOBNAME    | -   This column | varchar (128) | None            |
|               |     contains    |               |                 |
|               |     the names   |               |                 |
|               |     of the jobs |               |                 |
|               |     in job      |               |                 |
|               |                 |               |                 |
|               |   dependencies. |               |                 |
|               | -   This column |               |                 |
|               |     specifies   |               |                 |
|               |     the names   |               |                 |
|               |     of the job  |               |                 |
|               |     on which    |               |                 |
|               |     the jobs in |               |                 |
|               |     the JOBNAME |               |                 |
|               |     column      |               |                 |
|               |     depend.     |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPDATEOFFSET | -   This column | smallint (2)  | None            |
|               |     contains    |               |                 |
|               |     the         |               |                 |
|               |     dependency  |               |                 |
|               |     offset      |               |                 |
|               |     days.       |               |                 |
|               | -   This column |               |                 |
|               |     contains    |               |                 |
|               |     the number  |               |                 |
|               |     of days     |               |                 |
|               |     offset from |               |                 |
|               |     the         |               |                 |
|               |     schedule    |               |                 |
|               |     date.       |               |                 |
|               | -   The         |               |                 |
|               |     consequent  |               |                 |
|               |     date is     |               |                 |
|               |     checked for |               |                 |
|               |                 |               |                 |
|               |   dependencies. |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPTYPE       | This column     | smallint (2)  | -   1: Required |
|               | contains the    |               | -   2: Conflict |
|               | dependency      |               |     (Check day  |
|               | types.          |               |     for name)   |
|               |                 |               | -   3: After    |
|               |                 |               | -   4: Excludes |
|               |                 |               | -   34:         |
|               |                 |               |     Conflict    |
|               |                 |               |     (Check day  |
|               |                 |               |     for job     |
|               |                 |               |     name like)  |
|               |                 |               | -   66:         |
|               |                 |               |     Conflict    |
|               |                 |               |     (Check all  |
|               |                 |               |     days for    |
|               |                 |               |     job name)   |
|               |                 |               | -   98:         |
|               |                 |               |     Conflict    |
|               |                 |               |     (Check all  |
|               |                 |               |     days for    |
|               |                 |               |     job name    |
|               |                 |               |     like)       |
|               |                 |               | -   129:        |
|               |                 |               |     Required    |
|               |                 |               |     (ignore     |
|               |                 |               |     exit code)  |
|               |                 |               | -   131: After  |
|               |                 |               |     (ignore     |
|               |                 |               |     exit code)  |
|               |                 |               | -   257:        |
|               |                 |               |     Required    |
|               |                 |               |     (On         |
|               |                 |               |     Failure)    |
|               |                 |               | -   259: After  |
|               |                 |               |     (On         |
|               |                 |               |     Failure)    |
+---------------+-----------------+---------------+-----------------+

: JDEPJOB Column Descriptions

+------------+---------------+
| Index Code | Columns       |
+============+===============+
| PK_JDEPJOB | SKDID         |
|            |               |
|            | JOBNAME       |
|            |               |
|            | FREQNAME      |
|            |               |
|            | DEPSKDID      |
|            |               |
|            | DEPJOBNAME    |
|            |               |
|            | DEPDATEOFFSET |
+------------+---------------+

: JDEPJOB Index Descriptions

### JDEPTHR

The secondary table JDEPTHR contains Threshold Dependency details for
the JMASTER primary table.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The jobs     |               |                  |
|             |     name must be |               |                  |
|             |     unique       |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTHRID    | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     th           |               |                  |
|             | reshold/resource |               |                  |
|             |     dependency   |               |                  |
|             |     IDs.         |               |                  |
|             | -   Each number  |               |                  |
|             |     is the ID of |               |                  |
|             |     the          |               |                  |
|             |     th           |               |                  |
|             | reshold/resource |               |                  |
|             |     on which the |               |                  |
|             |     jobs in the  |               |                  |
|             |     JOBNAME      |               |                  |
|             |     column       |               |                  |
|             |     depend.      |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     THRESH       |               |                  |
|             |     table.       |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTHRVAL   | -   This column  | int (4)       | Valid values     |
|             |     contains the |               | range from 0 to  |
|             |     values for   |               | 2,147,483,647.   |
|             |     th           |               |                  |
|             | reshold/resource |               |                  |
|             |     comparisons. |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     values used  |               |                  |
|             |     to compare   |               |                  |
|             |     against the  |               |                  |
|             |     values of    |               |                  |
|             |     the          |               |                  |
|             |     thre         |               |                  |
|             | sholds/resources |               |                  |
|             |     at each      |               |                  |
|             |     job's run   |               |                  |
|             |     time.        |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTHROPER  | -   This column  | smallint (2)  | -   0: Equal (=) |
|             |     contains     |               | -   1: Greater   |
|             |     dependency   |               |     Than (\>)    |
|             |     operators    |               | -   2: Less Than |
|             |     for the      |               |     (\<)         |
|             |     thres        |               | -   3: Greater   |
|             | holds/resources. |               |     Than or      |
|             | -   This column  |               |     Equal (\>=)  |
|             |     contains the |               | -   4: Less Than |
|             |     operators    |               |     or Equal     |
|             |     used to      |               |     (\<=)        |
|             |     compare the  |               | -   5: Not Equal |
|             |     DEPTHRVAL    |               |     (\<\>)       |
|             |     value        |               |                  |
|             |     against the  |               |                  |
|             |     values of    |               |                  |
|             |     the          |               |                  |
|             |     thre         |               |                  |
|             | sholds/resources |               |                  |
|             |     at each      |               |                  |
|             |     job's run   |               |                  |
|             |     time.        |               |                  |
+-------------+------------------+---------------+------------------+
| USEALL      | This column      | char (5)      | -   Valid values |
|             | indicates if the |               |     are True and |
|             | dependency       |               |     False        |
|             | requires all     |               |     (default)    |
|             | resources for    |               | -   This value   |
|             | the defined      |               |     must be      |
|             | resource.        |               |     False if the |
|             |                  |               |     DEPTHRVAL    |
|             |                  |               |     column is    |
|             |                  |               |     any number   |
|             |                  |               |     other than   |
|             |                  |               |     zero (0).    |
+-------------+------------------+---------------+------------------+

: JDEPTHR Column Descriptions

+------------+----------+
| Index Code | Columns  |
+============+==========+
| PK_JDEPTHR | SKDID    |
|            |          |
|            | JOBNAME  |
|            |          |
|            | FREQNAME |
|            |          |
|            | DEPTHRID |
+------------+----------+

: JDEPTHR Index Descriptions

### JDOCS

The secondary table JDOCS contains the Documentation details for the
JMASTER primary table.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| DOCID       | This column is   | smallint (2)  | None             |
|             | reserved for     |               |                  |
|             | future use.      |               |                  |
+-------------+------------------+---------------+------------------+
| DOCLINE     | This column      | smallint (2)  | The              |
|             | contains the     |               | documentation    |
|             | documentation    |               | line numbers are |
|             | line numbers.    |               | positive         |
|             |                  |               | integers         |
|             |                  |               | starting at zero |
|             |                  |               | (0).             |
+-------------+------------------+---------------+------------------+
| DOCTEXT     | This column      | char (80)     | None             |
|             | contains the     |               |                  |
|             | documentation    |               |                  |
|             | text for the     |               |                  |
|             | corresponding    |               |                  |
|             | line numbers.    |               |                  |
+-------------+------------------+---------------+------------------+

: JDOCS Column Descriptions

+------------+----------+
| Index Code | Columns  |
+============+==========+
| PK_JDOCS   | SKDID    |
|            |          |
|            | JOBNAME  |
|            |          |
|            | FREQNAME |
|            |          |
|            | DOCID    |
|            |          |
|            | DOCLINE  |
+------------+----------+

: JDOCS Index Descriptions

### JEVENTS

The secondary table JEVENTS contains the Event details for the JMASTER
primary table.

+--------------+----------------+----------------+----------------+
| Column Name  | Explanation    | Data Type      | Additional     |
|              |                |                | Information    |
+==============+================+================+================+
| SKDID        | -   This       | int (4)        | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the        |                |                |
|              |     schedule   |                |                |
|              |     IDs.       |                |                |
|              | -   This       |                |                |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     c          |                |                |
|              | ross-reference |                |                |
|              |                |                |                |
|              |    information |                |                |
|              |     for lookup |                |                |
|              |     into the   |                |                |
|              |     SNAME      |                |                |
|              |     table.     |                |                |
+--------------+----------------+----------------+----------------+
| JOBNAME      | -   This       | varchar (128)  | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the job    |                |                |
|              |     names.     |                |                |
|              | -   The job    |                |                |
|              |     names must |                |                |
|              |     be unique  |                |                |
|              |     within     |                |                |
|              |     each       |                |                |
|              |     schedule.  |                |                |
|              | -   The        |                |                |
|              |     schedule   |                |                |
|              |     ID (SKDID) |                |                |
|              |     identifies |                |                |
|              |     the        |                |                |
|              |     schedule.  |                |                |
+--------------+----------------+----------------+----------------+
| FREQNAME     | -   This       | char (20)      | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the        |                |                |
|              |     frequency  |                |                |
|              |     names.     |                |                |
|              | -   The        |                |                |
|              |     frequency  |                |                |
|              |     names must |                |                |
|              |     be unique  |                |                |
|              |     within     |                |                |
|              |     each job.  |                |                |
|              | -   The job    |                |                |
|              |     name       |                |                |
|              |     (JOBNAME)  |                |                |
|              |     identifies |                |                |
|              |     the job.   |                |                |
+--------------+----------------+----------------+----------------+
| JOBSTATUS    | This column    | smallint (2)   | -   500:       |
|              | contains the   |                |     Running    |
|              | job statuses   |                |     (Time      |
|              | that trigger   |                |     Exceeded)  |
|              | the events.    |                | -   900:       |
|              |                |                |     Finished   |
|              |                |                |     OK         |
|              |                |                | -   910:       |
|              |                |                |     Failed     |
|              |                |                | -   940:       |
|              |                |                |     Skipped    |
+--------------+----------------+----------------+----------------+
| FEEDBACKFC   | -   This       | int            | -   0: The     |
|              |     column     |                |     JOBSTATUS  |
|              |     contains   |                |     value will |
|              |     the field  |                |     trigger    |
|              |     code for   |                |     the event. |
|              |     the LSAM   |                | -   922: The   |
|              |     Feedback   |                |     Exit       |
|              |     item that  |                |                |
|              |     will       |                |    Description |
|              |     trigger    |                |     will be    |
|              |     the event. |                |     used to    |
|              | -   The code   |                |     determine  |
|              |     can be     |                |     the event  |
|              |     specific   |                |     trigger.   |
|              |     to a       |                | -   All other  |
|              |                |                |     values are |
|              |    platform's |                |     plat       |
|              |     list of    |                | form-specific. |
|              |     feedback,  |                |                |
|              |     or it will |                |                |
|              |     be a       |                |                |
|              |     specific   |                |                |
|              |     value if   |                |                |
|              |     the Exit   |                |                |
|              |                |                |                |
|              |    Description |                |                |
|              |     will       |                |                |
|              |     trigger    |                |                |
|              |     the event. |                |                |
+--------------+----------------+----------------+----------------+
| LSAMFEEDBACK | This column    | varchar (4000) | When           |
|              | contains the   |                | FEEDBACKFC is: |
|              | comparison     |                |                |
|              | string for the |                | -   0: The     |
|              | value of the   |                |     value in   |
|              | feedback.      |                |     this       |
|              |                |                |     column is  |
|              |                |                |     an empty   |
|              |                |                |     string.    |
|              |                |                | -   922: The   |
|              |                |                |     value      |
|              |                |                |     contains   |
|              |                |                |     an         |
|              |                |                |     operator a |
|              |                |                |     colon (:)  |
|              |                |                |     and the    |
|              |                |                |     comparison |
|              |                |                |     string     |
|              |                |                |     (e.g.,     |
|              |                |                |     EQ:32004). |
|              |                |                | -   Any other  |
|              |                |                |     values     |
|              |                |                |     contain a  |
|              |                |                |     string for |
|              |                |                |                |
|              |                |                |    comparison. |
+--------------+----------------+----------------+----------------+
| EVDETS       | -   This       | varchar (738)  | For more       |
|              |     column     |                | information on |
|              |     contains   |                | valid OpCon    |
|              |     each       |                | events, refer  |
|              |     event's   |                | to the [OpCon  | |              |     details.   |                | Events](../    |
|              | -   This       |                | OpCon-Events |
|              |     column can |                | /Introduction.md) |
|              |     contain    |                | online help.   |
|              |     the        |                |                |
|              |     expandable |                |                |
|              |     tokens     |                |                |
|              |     that the   |                |                |
|              |     SAM        |                |                |
|              |     interprets |                |                |
|              |     at run     |                |                |
|              |     time.      |                |                |
+--------------+----------------+----------------+----------------+
| USERID       | This column is | smallint (2)   | None           |
|              | reserved for   |                |                |
|              | future use.    |                |                |
+--------------+----------------+----------------+----------------+

: JEVENTS Column Descriptions

+------------+-----------+
| Index Code | Columns   |
+============+===========+
| PK_JEVENTS | SKDID     |
|            |           |
|            | JOBNAME   |
|            |           |
|            | FREQNAME  |
|            |           |
|            | JOBSTATUS |
|            |           |
|            | EVDETS    |
+------------+-----------+

: JEVENTS Index Descriptions

### JGROUPS

The JGROUPS table is intended for job groups and is not currently used.

  Column Name   Explanation                               Data Type      Additional Information
  ------------- ----------------------------------------- -------------- ------------------------
  JOBGROUPID    This column is reserved for future use.   smallint (2)   None
  JOBGROUP      This column is reserved for future use.   char (24)      None

  : JGROUPS Column Descriptions

  Index Code   Columns
  ------------ ------------
  PK_JGROUPS   JOBGROUPID

  : JGROUPS Index Descriptions

### JMASTER

The primary table JMASTER contains Job Master information. There is no
limit, other than physical, to the number of job records within a
schedule. However, each job record must be unique.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTID      | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     department   |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     DEPTS table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBTYPE     | -   This column  | smallint (2)  | -   -1: Null     |
|             |     contains the |               | -   1: File      |
|             |     type of      |               |     Transfer     |
|             |     environment  |               | -   3: Windows   |
|             |     for each     |               | -   4: OpenVMS   |
|             |     job.         |               | -   5: IBM i     |
|             | -   The job type |               | -   6: UNIX      |
|             |     determines   |               | -   7: OS 2200   |
|             |     the machines |               | -   9: MCP       |
|             |     and machine  |               | -   11: BIS      |
|             |     groups that  |               | -   12: z/OS     |
|             |     are          |               | -   13: SAP R/3  |
|             |     available    |               |     and CRM      |
|             |     for each     |               | -   14: SAP BW   |
|             |     job.         |               | -   15:          |
|             |                  |               |     Container    |
|             |                  |               | -   16: JEE      |
|             |                  |               | -   17: Java     |
+-------------+------------------+---------------+------------------+
| ACCESSCDID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     Access Code  |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     ACCESSID     |               |                  |
|             |     table.       |               |                  |
|             | -   This         |               |                  |
|             |     column's    |               |                  |
|             |     data limits  |               |                  |
|             |     access to    |               |                  |
|             |     the job in   |               |                  |
|             |     OpCon.       |               |                  |
+-------------+------------------+---------------+------------------+
| JOBGROUPID  | This column is   | smallint (2)  | None             |
|             | reserved for     |               |                  |
|             | future use.      |               |                  |
+-------------+------------------+---------------+------------------+
| PRIMMACHID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     primary      |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   The primary  |               |                  |
|             |     machine is   |               |                  |
|             |     each job's  |               |                  |
|             |     default      |               |                  |
|             |     machine.     |               |                  |
|             | -   This column  |               |                  |
|             |     is           |               |                  |
|             |                  |               |                  |
|             | [mandatory]{.ul} |               |                  | |             |     if a machine |               |                  |
|             |     group ID is  |               |                  |
|             |     not          |               |                  |
|             |     specified;   |               |                  |
|             |     however, it  |               |                  |
|             |     is mutually  |               |                  |
|             |     exclusive    |               |                  |
|             |     with the     |               |                  |
|             |     machine      |               |                  |
|             |     group ID.    |               |                  |
|             | -   The primary  |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| ALTMACH1ID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     first        |               |                  |
|             |     alternate    |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   If the       |               |                  |
|             |     primary      |               |                  |
|             |     machine is   |               |                  |
|             |     unavailable  |               |                  |
|             |     at run time, |               |                  |
|             |     the jobs run |               |                  |
|             |     on an        |               |                  |
|             |     alternate    |               |                  |
|             |     machine.     |               |                  |
|             | -   Alternate    |               |                  |
|             |     machines are |               |                  |
|             |                  |               |                  |
|             |  [optional]{.ul} |               |                  | |             |     and should   |               |                  |
|             |     be defined   |               |                  |
|             |     in order.    |               |                  |
|             | -   The          |               |                  |
|             |     alternate    |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| ALTMACH2ID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     second       |               |                  |
|             |     alternate    |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   If the       |               |                  |
|             |     primary and  |               |                  |
|             |     first        |               |                  |
|             |     alternate    |               |                  |
|             |     machines are |               |                  |
|             |     unavailable  |               |                  |
|             |     at run time, |               |                  |
|             |     the jobs run |               |                  |
|             |     on the       |               |                  |
|             |     second       |               |                  |
|             |     alternate    |               |                  |
|             |     machine.     |               |                  |
|             | -   Alternate    |               |                  |
|             |     machines are |               |                  |
|             |                  |               |                  |
|             |  [optional]{.ul} |               |                  | |             |     and should   |               |                  |
|             |     be defined   |               |                  |
|             |     in order.    |               |                  |
|             | -   The          |               |                  |
|             |     alternate    |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| ALTMACH3ID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     third        |               |                  |
|             |     alternate    |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   If the       |               |                  |
|             |     primary,     |               |                  |
|             |     first        |               |                  |
|             |     alternate    |               |                  |
|             |     and second   |               |                  |
|             |     alternate    |               |                  |
|             |     machines are |               |                  |
|             |     unavailable  |               |                  |
|             |     at run time, |               |                  |
|             |     the jobs run |               |                  |
|             |     on an        |               |                  |
|             |     alternate    |               |                  |
|             |     machine.     |               |                  |
|             | -   Alternate    |               |                  |
|             |     machines are |               |                  |
|             |                  |               |                  |
|             |  [optional]{.ul} |               |                  | |             |     and should   |               |                  |
|             |     be defined   |               |                  |
|             |     in order.    |               |                  |
|             | -   The          |               |                  |
|             |     alternate    |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| MACHGRPID   | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     machine      |               |                  |
|             |     group IDs.   |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHGRPS     |               |                  |
|             |     table.       |               |                  |
|             | -   The machine  |               |                  |
|             |     group ID     |               |                  |
|             |     identifies a |               |                  |
|             |     group of     |               |                  |
|             |     machines     |               |                  |
|             |     compatible   |               |                  |
|             |     with the     |               |                  |
|             |     job.         |               |                  |
|             | -   The machine  |               |                  |
|             |     group ID is  |               |                  |
|             |     mutually     |               |                  |
|             |     exclusive    |               |                  |
|             |     with the     |               |                  |
|             |     primary      |               |                  |
|             |     machine ID.  |               |                  |
|             | -   The machine  |               |                  |
|             |     group type   |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| ESTRUNTIME  | -   This column  | int (4)       | The estimated    |
|             |     contains the |               | run time is in   |
|             |     estimated    |               | minutes.         |
|             |     run times    |               |                  |
|             |     for the      |               |                  |
|             |     jobs.        |               |                  |
|             | -   The OpCon    |               |                  |
|             |                  |               |                  |
|             |    administrator |               |                  |
|             |     calculates   |               |                  |
|             |     this value   |               |                  |
|             |     with the     |               |                  |
|             |     JOB_AVG      |               |                  |
|             |     script       |               |                  |
|             |     provided by  |               |                  |
|             |     [SMA         |               |                  | |             |     Tec          |               |                  |
|             | hnologies]{.Gene |               |                  |
|             | ralCompanyName}. |               |                  |
+-------------+------------------+---------------+------------------+
| SHORTNAME   | Contains a       | char (12)     | None             |
|             | generated name   |               |                  |
|             | for the job that |               |                  |
|             | is used in       |               |                  |
|             | communication    |               |                  |
|             | with the agents. |               |                  |
+-------------+------------------+---------------+------------------+

: JMASTER Column Descriptions

+------------+---------+
| Index Code | Columns |
+============+=========+
| PK_JMASTER | SKDID   |
|            |         |
|            | JOBNAME |
+------------+---------+

: JMASTER Index Descriptions

### JMASTER_AUX

The secondary table JMASTER_AUX contains auxiliary information
describing JMASTER data. The Schedule ID and Job Name link the auxiliary
information to the correct record in the JMASTER primary table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     schedule.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| JOBNAME     | -   This column | varchar (128)  | None            |
|             |     contains    |                |                 |
|             |     the job     |                |                 |
|             |     names.      |                |                 |
|             | -   The jobs    |                |                 |
|             |     name must   |                |                 |
|             |     be unique   |                |                 |
|             |     within each |                |                 |
|             |     schedule.   |                |                 |
|             | -   The         |                |                 |
|             |     schedule ID |                |                 |
|             |     (SKDID)     |                |                 |
|             |     identifies  |                |                 |
|             |     the         |                |                 |
|             |     schedule.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| JAFC        | This column     | smallint (2)   | -   1000 -      |
|             | contains the    |                |     1999: File  |
|             | auxiliary       |                |     Transfer    |
|             | information     |                | -   3000 -      |
|             | field codes.    |                |     3999:       |
|             |                 |                |     Windows     |
|             |                 |                | -   4000 -      |
|             |                 |                |     4999:       |
|             |                 |                |     OpenVMS     |
|             |                 |                | -   5000 -      |
|             |                 |                |     5999: i5/OS |
|             |                 |                | -   6000 -      |
|             |                 |                |     6999: UNIX  |
|             |                 |                | -   7000 -      |
|             |                 |                |     7999: OS    |
|             |                 |                |     2200        |
|             |                 |                | -   9000 -      |
|             |                 |                |     9999: MCP   |
|             |                 |                | -   10000 -     |
|             |                 |                |     10999: BIS  |
|             |                 |                | -   11000 -     |
|             |                 |                |     11999: z/OS |
|             |                 |                | -   12000 -     |
|             |                 |                |     12999: SAP  |
|             |                 |                |     R/3 and CRM |
|             |                 |                | -   13000 -     |
|             |                 |                |     13999: SAP  |
|             |                 |                |     BW          |
|             |                 |                | -   14000 -     |
|             |                 |                |     14999:      |
|             |                 |                |     Container   |
+-------------+-----------------+----------------+-----------------+
| JASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| JAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: JMASTER_AUX Column Descriptions

+---------------+---------+
| Index Code    | Columns |
+===============+=========+
| PK_JMASTERAUX | SKDID   |
|               |         |
|               | JOBNAME |
|               |         |
|               | JAFC    |
|               |         |
|               | JASEQNO |
+---------------+---------+

: JMASTER_AUX Index Descriptions

### JSKD

The secondary table JSKD contains Job Frequency details for jobs in the
JMASTER primary table. There is no limit for frequency definitions
within a job; however, each frequency name must be unique.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQPRI     | -   This column  | smallint (2)  | Valid frequency  |
|             |     contains the |               | priority values  |
|             |     frequency    |               | are positive     |
|             |     priorities.  |               | integers         |
|             | -   This column  |               | starting at zero |
|             |     determines   |               | (0).             |
|             |     which        |               |                  |
|             |     frequency is |               |                  |
|             |     used if two  |               |                  |
|             |     frequencies  |               |                  |
|             |     for a single |               |                  |
|             |     job qualify  |               |                  |
|             |     for the same |               |                  |
|             |     day.         |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| PRIORITY    | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     run-time     |               |                  |
|             |     priorities   |               |                  |
|             |     of the jobs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     number the   |               |                  |
|             |     SAM uses to  |               |                  |
|             |     evaluate     |               |                  |
|             |     priorities   |               |                  |
|             |     for job      |               |                  |
|             |     submissions  |               |                  |
|             |     when         |               |                  |
|             |     multiple     |               |                  |
|             |     jobs qualify |               |                  |
|             |     to run at    |               |                  |
|             |     the same     |               |                  |
|             |     time.        |               |                  |
+-------------+------------------+---------------+------------------+
| FREQCODE    | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     codes.       |               |                  |
|             | -   This column  |               |                  |
|             |     contains [an |               |                  | |             |     SMA          |               |                  |
|             |                  |               |                  |
|             |    Technologies] |               |                  |
|             | {.GeneralCompany |               |                  |
|             | NameAnLowercase} |               |                  |
|             |     proprietary  |               |                  |
|             |     value        |               |                  |
|             |     indicating   |               |                  |
|             |     the          |               |                  |
|             |     scheduling   |               |                  |
|             |     pattern of   |               |                  |
|             |     each         |               |                  |
|             |     frequency.   |               |                  |
+-------------+------------------+---------------+------------------+
| CALID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     calendar     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     CALDATA and  |               |                  |
|             |     CALDESC      |               |                  |
|             |     tables.      |               |                  |
+-------------+------------------+---------------+------------------+
| STOFFSET    | This column      | real (4)      | -   This column  |
|             | contains the     |               |     stores the   |
|             | start time       |               |     time in SQL  |
|             | offsets for the  |               |     format.      |
|             | jobs.            |               | -   The integer  |
|             |                  |               |     part of this |
|             |                  |               |     SQL date is  |
|             |                  |               |     irrelevant.  |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| STABSREL    | -   This column  | char (1)      | -   A: Absolute  |
|             |     contains the |               | -   R: Relative  |
|             |     start time   |               |                  |
|             |     offset types |               |                  |
|             |     for the      |               |                  |
|             |     jobs.        |               |                  |
|             | -   This column  |               |                  |
|             |     determines   |               |                  |
|             |     if the start |               |                  |
|             |     time is      |               |                  |
|             |     absolute or  |               |                  |
|             |     relative.    |               |                  |
+-------------+------------------+---------------+------------------+
| LTSTTIME    | This column      | real (4)      | -   This column  |
|             | contains the     |               |     stores the   |
|             | latest start     |               |     time in SQL  |
|             | time offsets for |               |     format.      |
|             | the jobs.        |               | -   The integer  |
|             |                  |               |     part of this |
|             |                  |               |     SQL date is  |
|             |                  |               |     irrelevant.  |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| LTABSREL    | -   This column  | char (1)      | -   A: Absolute  |
|             |     contains the |               | -   R: Relative  |
|             |     latest start |               |                  |
|             |     time types   |               |                  |
|             |     for the      |               |                  |
|             |     jobs.        |               |                  |
|             | -   This column  |               |                  |
|             |     determines   |               |                  |
|             |     if the       |               |                  |
|             |     latest start |               |                  |
|             |     time is      |               |                  |
|             |     absolute or  |               |                  |
|             |     relative.    |               |                  |
+-------------+------------------+---------------+------------------+
| STSTATUS    | -   This column  | smallint (2)  | -   -1: Do Not   |
|             |     contains the |               |     Schedule     |
|             |     start        |               | -   0: On Hold   |
|             |     statuses for |               | -   99: Released |
|             |     the jobs.    |               |                  |
|             | -   This column  |               |                  |
|             |     determines   |               |                  |
|             |     the starting |               |                  |
|             |     states of    |               |                  |
|             |     the jobs     |               |                  |
|             |     when         |               |                  |
|             |     scheduled.   |               |                  |
+-------------+------------------+---------------+------------------+
| AOBN        | -   This column  | smallint (2)  | -   A = 1        |
|             |     contains the |               |     (After)\     |
|             |     AOBN         |               |     Move the job |
|             |     frequency    |               |     to the next  |
|             |     settings.    |               |     working day. |
|             | -   This column  |               | -   O = 2 (On    |
|             |     determines   |               |     Date)        |
|             |     where the    |               |     Schedule the |
|             |     jobs should  |               |     job on the   |
|             |     be moved     |               |     holiday.     |
|             |     when they    |               | -   B = 4        |
|             |     are          |               |     (Before)\    |
|             |     scheduled on |               |     Move the job |
|             |     a holiday.   |               |     to the       |
|             |                  |               |     previous     |
|             |                  |               |     working day. |
|             |                  |               | -   N = 8 (Not   |
|             |                  |               |     Schedule) Do |
|             |                  |               |     not schedule |
|             |                  |               |     the job.     |
+-------------+------------------+---------------+------------------+
| MAXMINS     | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     maximum      |               |                  |
|             |     minutes for  |               |                  |
|             |     the jobs to  |               |                  |
|             |     run.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains the |               |                  |
|             |     amount of    |               |                  |
|             |     time in      |               |                  |
|             |     minutes      |               |                  |
|             |     before the   |               |                  |
|             |     respective   |               |                  |
|             |     job is       |               |                  |
|             |     marked as    |               |                  |
|             |     having       |               |                  |
|             |     exceeded     |               |                  |
|             |     their        |               |                  |
|             |     maximum      |               |                  |
|             |     allowed run  |               |                  |
|             |     times.       |               |                  |
+-------------+------------------+---------------+------------------+
| ESTRUNTIME  | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     estimated    |               |                  |
|             |     run times    |               |                  |
|             |     for the      |               |                  |
|             |     jobs.        |               |                  |
|             | -   The OpCon    |               |                  |
|             |                  |               |                  |
|             |    administrator |               |                  |
|             |     calculates   |               |                  |
|             |     this value   |               |                  |
|             |     with the     |               |                  |
|             |     JOB_AVG      |               |                  |
|             |     script       |               |                  |
|             |     provided by  |               |                  |
|             |     [SMA         |               |                  | |             |     Tec          |               |                  |
|             | hnologies]{.Gene |               |                  |
|             | ralCompanyName}. |               |                  |
+-------------+------------------+---------------+------------------+

: JSKD Column Descriptions

+------------+----------+
| Index Code | Columns  |
+============+==========+
| PK_JSKD    | SKDID    |
|            |          |
|            | JOBNAME  |
|            |          |
|            | FREQPRI  |
|            |          |
|            | FREQNAME |
+------------+----------+

: JSKD Index Descriptions

### JSKD_AUX

The secondary table JSKD_AUX contains auxiliary information describing
Job Frequency details in the JSKD table. The combination of Schedule ID,
Job Name, Frequency Priority, and Frequency Name links the auxiliary
information to the correct record in the JSKD table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| JOBNAME     | -   This column | varchar (128)  | None            |
|             |     contains    |                |                 |
|             |     the job     |                |                 |
|             |     names.      |                |                 |
|             | -   The job     |                |                 |
|             |     names must  |                |                 |
|             |     be unique   |                |                 |
|             |     within each |                |                 |
|             |     schedule.   |                |                 |
|             | -   The         |                |                 |
|             |     schedule ID |                |                 |
|             |     (SKDID)     |                |                 |
|             |     identifies  |                |                 |
|             |     the         |                |                 |
|             |     schedule.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| FREQPRI     | -   This column | smallint (2)   | Valid frequency |
|             |     contains    |                | priority values |
|             |     the         |                | are positive    |
|             |     frequency   |                | integers        |
|             |     priorities. |                | starting at     |
|             | -   This column |                | zero (0).       |
|             |     determines  |                |                 |
|             |     which       |                |                 |
|             |     frequency   |                |                 |
|             |     is used if  |                |                 |
|             |     two         |                |                 |
|             |     frequencies |                |                 |
|             |     for a       |                |                 |
|             |     single job  |                |                 |
|             |     qualify for |                |                 |
|             |     the same    |                |                 |
|             |     day.        |                |                 |
+-------------+-----------------+----------------+-----------------+
| FREQNAME    | -   This column | char (20)      | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     frequency   |                |                 |
|             |     names.      |                |                 |
|             | -   The         |                |                 |
|             |     frequency   |                |                 |
|             |     names must  |                |                 |
|             |     be unique   |                |                 |
|             |     within each |                |                 |
|             |     job.        |                |                 |
|             | -   The job     |                |                 |
|             |     name        |                |                 |
|             |     (JOBNAME)   |                |                 |
|             |     identifies  |                |                 |
|             |     the job.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| JAFC        | This column     | smallint (2)   | -   0:          |
|             | contains the    |                |     Indicates   |
|             | auxiliary       |                |     the content |
|             | information     |                |     is          |
|             | field codes.    |                |                 |
|             |                 |                |   documentation |
|             |                 |                | -   1 -- 51:    |
|             |                 |                |     Reserved    |
|             |                 |                |     for current |
|             |                 |                |     column      |
|             |                 |                |     lookup use  |
|             |                 |                | -   101:        |
|             |                 |                |     Averaged    |
|             |                 |                |     Job Run     |
|             |                 |                |     Time for    |
|             |                 |                |     this        |
|             |                 |                |     frequency   |
|             |                 |                | -   102:        |
|             |                 |                |     Expected    |
|             |                 |                |     (i.e.,      |
|             |                 |                |     Target)     |
|             |                 |                |     Start Time  |
|             |                 |                | -   103: Start  |
|             |                 |                |     Scheduling  |
|             |                 |                |     Date        |
|             |                 |                | -   104: End    |
|             |                 |                |     Scheduling  |
|             |                 |                |     Date        |
|             |                 |                | -   105:        |
|             |                 |                |     Include     |
|             |                 |                |     Regardless  |
|             |                 |                |     Dates       |
|             |                 |                | -   106:        |
|             |                 |                |     Exclude     |
|             |                 |                |     Regardless  |
|             |                 |                |     Dates       |
+-------------+-----------------+----------------+-----------------+
| JASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| JAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: JSKD_AUX Column Descriptions

+------------+----------+
| Index Code | Columns  |
+============+==========+
| PK_JSKDAUX | SKDID    |
|            |          |
|            | JOBNAME  |
|            |          |
|            | FREQPRI  |
|            |          |
|            | FREQNAME |
|            |          |
|            | JAFC     |
|            |          |
|            | JASEQNO  |
+------------+----------+

: JSKD_AUX Index Descriptions

### JSTATMAP

The JSTATMAP table maps (i.e., cross-references) Job Status and Start
Status Codes to their respective descriptions.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| STSTATUS    | This column      | smallint (2) | Values less than |
|             | contains start   |              | 900 indicate     |
|             | statuses of the  |              | that the job has |
|             | jobs.            |              | not been         |
|             |                  |              | submitted; thus, |
|             |                  |              | the job is       |
|             |                  |              | either On Hold,  |
|             |                  |              | Released, or     |
|             |                  |              | waiting for the  |
|             |                  |              | start criteria   |
|             |                  |              | to be met.       |
+-------------+------------------+--------------+------------------+
| JOBSTATUS   | -   This column  | smallint (2) | The value is     |
|             |     contains the |              | zero (0) when    |
|             |     available    |              | the STSTATUS is  |
|             |     job progress |              | less than 900.   |
|             |     statuses.    |              |                  |
|             | -   After a job  |              |                  |
|             |     has been     |              |                  |
|             |     submitted,   |              |                  |
|             |     this column  |              |                  |
|             |     reflects the |              |                  |
|             |     progress of  |              |                  |
|             |     the job and  |              |                  |
|             |     the          |              |                  |
|             |     resulting    |              |                  |
|             |     termination  |              |                  |
|             |     state.       |              |                  |
+-------------+------------------+--------------+------------------+
| JOBSTATE    | This column      | varchar (40) | Each pair of     |
|             | contains the job |              | numbers          |
|             | state            |              | (STSTATUS and    |
|             | descriptions.    |              | JOBSTATUS)       |
|             |                  |              | indicates a      |
|             |                  |              | unique job       |
|             |                  |              | state. This      |
|             |                  |              | column contains  |
|             |                  |              | the description  |
|             |                  |              | of each state.   |
+-------------+------------------+--------------+------------------+
| FILTERCAT   | This column is   | varchar (40) | None             |
|             | the filtering    |              |                  |
|             | category used to |              |                  |
|             | filter jobs      |              |                  |
|             | displayed on the |              |                  |
|             | Operations views |              |                  |
|             | (in the          |              |                  |
|             | Enterprise       |              |                  |
|             | Manager).        |              |                  |
+-------------+------------------+--------------+------------------+

: JSTATMAP Column Descriptions

+---------------+-----------+
| Index Code    | Columns   |
+===============+===========+
| PK\_ JSTATMAP | STSTATUS  |
|               |           |
|               | JOBSTATUS |
+---------------+-----------+

: JSTATMAP Index Descriptions

### JTHR

The JTHR table contains the Threshold information for a job to set the
particular threshold to a value upon termination with the associated job
status.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| JOBSTATUS   | -   This column  | smallint (2)  | -   500: Running |
|             |     contains the |               |     (Time        |
|             |     triggering   |               |     Exceeded)    |
|             |     job          |               | -   900:         |
|             |     statuses.    |               |     Finished OK  |
|             | -   This column  |               | -   910: Failed  |
|             |     contains the |               | -   940: Skipped |
|             |     job statuses |               |                  |
|             |     that cause   |               |                  |
|             |     the          |               |                  |
|             |     thre         |               |                  |
|             | sholds/resources |               |                  |
|             |     to be set.   |               |                  |
+-------------+------------------+---------------+------------------+
| THRESHID    | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     th           |               |                  |
|             | reshold/resource |               |                  |
|             |     IDs of the   |               |                  |
|             |     thre         |               |                  |
|             | sholds/resources |               |                  |
|             |     to be set.   |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     THRESH       |               |                  |
|             |     table.       |               |                  |
+-------------+------------------+---------------+------------------+
| THRESHVAL   | This column      | int (4)       | Valid values     |
|             | contains the new |               | range from 0 to  |
|             | value for the    |               | 2,147,483,647.   |
|             | thres            |               |                  |
|             | holds/resources. |               |                  |
+-------------+------------------+---------------+------------------+

: JTHR Column Descriptions

+------------+-----------+
| Index Code | Columns   |
+============+===========+
| PK\_ JTHR  | SKDID     |
|            |           |
|            | JOBNAME   |
|            |           |
|            | FREQNAME  |
|            |           |
|            | JOBSTATUS |
|            |           |
|            | THRESHID  |
+------------+-----------+

: JTHR Index Descriptions

### LSAMTYPES

The primary table LSAMTYPES contains a list of LSAMs supported by SMA Technologies.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| LSAMTYPEID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     LSAM type    |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     from the     |               |                  |
|             |                  |               |                  |
|             |    LSAMTYPES_AUX |               |                  |
|             |     table and    |               |                  |
|             |     various      |               |                  |
|             |     OpCon        |               |                  |
|             |                  |               |                  |
|             |    applications. |               |                  |
+-------------+------------------+---------------+------------------+
| LSAMTYPDESC | This column      | varchar (255) | None             |
|             | contains the     |               |                  |
|             | name associated  |               |                  |
|             | with each LSAM   |               |                  |
|             | type.            |               |                  |
+-------------+------------------+---------------+------------------+

: LSAMTYPES Column Descriptions

  Index Code     Columns
  -------------- ------------
  PK_LSAMTYPES   LSAMTYPEID

  : LSAMTYPES Index Descriptions

### LSAMTYPES_AUX

The secondary table LSAMTYPES_AUX contains auxiliary information
describing LSAM type details. The LSAM type ID links the auxiliary
information to the correct record in the LSAMTYPES primary table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | SQL Data Type  | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| LSAMTYPEID  | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the LSAM    |                |                 |
|             |     type IDs.   |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     LSAMTYPES   |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| LAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| LASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| LAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: LSAMTYPES_AUX Column Descriptions

+-----------------+------------+
| Index Code      | Columns    |
+=================+============+
| PK_LSAMTYPESAUX | LSAMTYPEID |
|                 |            |
|                 | LAFC       |
|                 |            |
|                 | LASEQNO    |
+-----------------+------------+

: LSAMTYPES_AUX Index Descriptions

### MACHGRPS

The primary table MACHGRPS contains the machine group details.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| MACHGRPID   | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     machine      |              |                  |
|             |     group IDs.   |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     JMASTER      |              |                  |
|             |     table.       |              |                  |
+-------------+------------------+--------------+------------------+
| MACHGRP     | This column      | char (20)    | None             |
|             | contains the     |              |                  |
|             | machine group    |              |                  |
|             | names.           |              |                  |
+-------------+------------------+--------------+------------------+
| MACHGRPTP   | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     operating    |              |                  |
|             |     system type  |              |                  |
|             |     assigned to  |              |                  |
|             |     each machine |              |                  |
|             |     group.       |              |                  |
|             | -   Consistent   |              |                  |
|             |     with the     |              |                  |
|             |     machine/job  |              |                  |
|             |     type, only   |              |                  |
|             |     machines of  |              |                  |
|             |     the same OS  |              |                  |
|             |     type can be  |              |                  |
|             |     listed in    |              |                  |
|             |     the group.   |              |                  |
+-------------+------------------+--------------+------------------+

: MACHGRPS Column Descriptions

  Index Code      Columns
  --------------- -----------
  PK\_ MACHGRPS   MACHGRPID

  : MACHGRPS Index Descriptions

### MACHGRPS_AUX

The secondary table MACHGRPS_AUX contains auxiliary information
describing machine group details. The machine group ID links the
auxiliary information to the correct record in the MACHGRPS primary
table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | SQL Data Type  | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| MACHGRPID   | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the machine |                |                 |
|             |     group IDs.  |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     MACHGRPS    |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| MAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| MASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| MAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: MACHGRPS_AUX Column Descriptions

+----------------+-----------+
| Index Code     | Columns   |
+================+===========+
| PK_MACHGRPSAUX | MACHGRPID |
|                |           |
|                | MAFC      |
|                |           |
|                | MASEQNO   |
+----------------+-----------+

: MACHGRPS_AUX Index Descriptions

### MACHS

The primary table MACHS contains machine details for communicating with
the Local Schedule Activity Monitors (LSAMs).

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| MACHID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     machine IDs. |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     JMASTER      |              |                  |
|             |     table.       |              |                  |
+-------------+------------------+--------------+------------------+
| MACHNAME    | -   This column  | char (24)    | None             |
|             |     contains the |              |                  |
|             |     machine      |              |                  |
|             |     names.       |              |                  |
|             | -   The A-Series |              |                  |
|             |     LSAM         |              |                  |
|             |     requires a   |              |                  |
|             |     period       |              |                  |
|             |     following    |              |                  |
|             |     the machine  |              |                  |
|             |     name.        |              |                  |
|             | -   It is        |              |                  |
|             |     essential    |              |                  |
|             |     these names  |              |                  |
|             |     exactly      |              |                  |
|             |     match the    |              |                  |
|             |     host names   |              |                  |
|             |     identified   |              |                  |
|             |     on each of   |              |                  |
|             |     the LSAM     |              |                  |
|             |     machines.    |              |                  |
+-------------+------------------+--------------+------------------+
| MACHTYPE    | This column      | smallint (2) | -   0: \<Null    |
|             | contains the     |              |     Machine\>    |
|             | operating system |              | -   1: N/A       |
|             | type assigned to |              | -   3: Windows   |
|             | each machine.    |              | -   4: OpenVMS   |
|             |                  |              | -   5: IBM i     |
|             |                  |              | -   6: UNIX      |
|             |                  |              | -   7: OS 2200   |
|             |                  |              | -   9: MCP       |
|             |                  |              | -   11: BIS      |
|             |                  |              | -   12: z/OS     |
|             |                  |              | -   13: SAP R/3  |
|             |                  |              |     and CRM      |
|             |                  |              | -   14: SAP BW   |
|             |                  |              | -   17: Java     |
+-------------+------------------+--------------+------------------+
| MACHSOCKET  | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     LSAM TCP/IP  |              |                  |
|             |     socket       |              |                  |
|             |     numbers for  |              |                  |
|             |     the          |              |                  |
|             |     machines.    |              |                  |
|             | -   This column  |              |                  |
|             |     contains the |              |                  |
|             |     TCP/IP       |              |                  |
|             |     socket       |              |                  |
|             |     numbers used |              |                  |
|             |     to           |              |                  |
|             |     communicate  |              |                  |
|             |     with the     |              |                  |
|             |     LSAM         |              |                  |
|             |     machines.    |              |                  |
|             | -   The LSAMs    |              |                  |
|             |     must be      |              |                  |
|             |     configured   |              |                  |
|             |     on the same  |              |                  |
|             |     TCP/IP       |              |                  |
|             |     sockets      |              |                  |
|             |     configured   |              |                  |
|             |     in this      |              |                  |
|             |     column.      |              |                  |
+-------------+------------------+--------------+------------------+
| MACHGWAYID  | This column      | smallint (2) | None             |
|             | contains the IDs |              |                  |
|             | of the machines  |              |                  |
|             | used as gateways |              |                  |
|             | for the machines |              |                  |
|             | in the MACHNAME  |              |                  |
|             | column.          |              |                  |
+-------------+------------------+--------------+------------------+
| MACHGRPID   | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     machine      |              |                  |
|             |     group IDs.   |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     MACHGRPS     |              |                  |
|             |     table.       |              |                  |
+-------------+------------------+--------------+------------------+
| LASTUPDATE  | -   This column  | float (8)    | -   This column  |
|             |     contains the |              |     stores the   |
|             |     dates/times  |              |     date in SQL  |
|             |     of last      |              |     format.      |
|             |     updates for  |              | -   The integer  |
|             |     the          |              |     part of the  |
|             |     machines.    |              |     SQL date     |
|             | -   To determine |              |     represents   |
|             |     machine      |              |     the day      |
|             |     inquiry      |              |     count since  |
|             |     cycles, this |              |     Saturday,    |
|             |     column       |              |     December     |
|             |     indicates    |              |     30, 1899.    |
|             |     when the     |              | -   The          |
|             |     information  |              |     fractional   |
|             |     was last     |              |     part of the  |
|             |     updated for  |              |     SQL date     |
|             |     the          |              |     represents   |
|             |     machines.    |              |     the time in  |
|             |                  |              |     seconds      |
|             |                  |              |     since        |
|             |                  |              |     midnight.    |
+-------------+------------------+--------------+------------------+
| MAXJOBS     | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     maximum      |              |                  |
|             |     number of    |              |                  |
|             |     concurrent   |              |                  |
|             |     jobs allowed |              |                  |
|             |     to process   |              |                  |
|             |     on the       |              |                  |
|             |     machines.    |              |                  |
|             | -   The          |              |                  |
|             |                  |              |                  |
|             |    configuration |              |                  |
|             |     on the LSAM  |              |                  |
|             |     machines     |              |                  |
|             |     determines   |              |                  |
|             |     the maximum  |              |                  |
|             |     number of    |              |                  |
|             |     concurrent   |              |                  |
|             |     jobs per     |              |                  |
|             |     machine.     |              |                  |
+-------------+------------------+--------------+------------------+
| CURRJOBS    | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     number of    |              |                  |
|             |     jobs         |              |                  |
|             |     currently    |              |                  |
|             |     executing on |              |                  |
|             |     the          |              |                  |
|             |     machines.    |              |                  |
|             | -   The SAM      |              |                  |
|             |     maintains    |              |                  |
|             |     these        |              |                  |
|             |     numbers      |              |                  |
|             |     during       |              |                  |
|             |     processing.  |              |                  |
+-------------+------------------+--------------+------------------+
| NETSTATUS   | This column      | char (1)     | -   U: Up        |
|             | contains the     |              | -   D: Down      |
|             | current status   |              |                  |
|             | of the network   |              |                  |
|             | connections      |              |                  |
|             | between          |              |                  |
|             | SMANetCom and    |              |                  |
|             | the LSAM         |              |                  |
|             | machines.        |              |                  |
+-------------+------------------+--------------+------------------+
| OPERSTATUS  | -   This column  | char (1)     | None             |
|             |     contains the |              |                  |
|             |     current      |              |                  |
|             |     statuses of  |              |                  |
|             |     the LSAMs as |              |                  |
|             |     set by       |              |                  |
|             |     Events or by |              |                  |
|             |     the          |              |                  |
|             |     graphical    |              |                  |
|             |     interfaces.  |              |                  |
|             | -   These        |              |                  |
|             |     statuses     |              |                  |
|             |     decide       |              |                  |
|             |     whether      |              |                  |
|             |     SMANetCom    |              |                  |
|             |     should       |              |                  |
|             |     communicate  |              |                  |
|             |     with each    |              |                  |
|             |     LSAM.        |              |                  |
+-------------+------------------+--------------+------------------+

: MACHS Column Descriptions

  Index Code   Columns
  ------------ ----------
  PK_MACHS     MACHID
  I2MACHS      MACHNAME

  : MACHS Index Descriptions

### MACHS_AUX

The secondary table MACHS_AUX contains auxiliary information describing
machine details. The machine ID links the auxiliary information to the
correct record in the MACHS primary table.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| MACHID      | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the machine |                |                 |
|             |     group IDs.  |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     MACHS       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| MAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| MASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| MAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: MACHS_AUX Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_MACHSAUX | MACHID  |
|             |         |
|             | MAFC    |
|             |         |
|             | MASEQNO |
+-------------+---------+

: MACHS_AUX Index Descriptions

### MSGS_TO_NETCOM

The table MSGS_TO_NETCOM contains details of messages the SAM sends to
SMANetCom for communication with the LSAM agents.

  Column Name      Explanation                                                                              Data Type        Additional Information
  ---------------- ---------------------------------------------------------------------------------------- ---------------- --------------------------------------------------------------------------------------------------------
  MSGNUMBER        This column contains unique sequential identification numbers.                           int (4)          The database scripts create this column with the IDENTITY property and the NOT FOR REPLICATION option.
  NETCOMNAME       This column contains the name of the SMANetCom that should process the messages.         char (128)       None
  DESTMACH         This column contains the names of the LSAM machines for SMANetCom to communicate with.   char (24)        None
  MESSAGE_LENGTH   This column contains the lengths of the messages.                                        int (4)          The length of each message is in bytes.
  MESSAGE          This column contains messages less than 7,500 characters to send to the LSAMs.           varchar (7500)   None
  LONG_MESSAGE     This column contains messages greater than 7,600 characters to send to the LSAMs.        text (16)        None

  : MSGS_TO_NETCOM Column Descriptions

  Index Code          Columns
  ------------------- -----------
  PK_MSGS_TO_NETCOM   MSGNUMBER

  : MSGS_TO_NETCOM Index Descriptions

### MSGS_TO_SAM

The table MSGS_TO_SAM contains details of messages SMANetCom returns to
the SAM from the LSAM agents.

  Column Name      Explanation                                                                    Data Type        Additional Information
  ---------------- ------------------------------------------------------------------------------ ---------------- --------------------------------------------------------------------------------------------------------
  MSGNUMBER        This column contains unique sequential identification numbers.                 int (4)          The database scripts create this column with the IDENTITY property and the NOT FOR REPLICATION option.
  NETCOMNAME       This column contains the name of the SMANetCom that inserted the messages.     char (128)       None
  MESSAGE_LENGTH   This column contains the lengths of the messages.                              int (4)          The length of the message is in bytes.
  MESSAGE          This column contains the messages less than 7,500 characters from the LSAMs.   varchar (7500)   Stores messages less than 7,500 characters.
  LONG_MESSAGE     This column contains messages greater than 7,500 characters from the LSAMs.    text (16)        Stores messages exceeding 7,500 characters.

  : MSGS_TO_SAM Column Descriptions

  Index Code       Columns
  ---------------- -----------
  PK_MSGS_TO_SAM   MSGNUMBER

  : MSGS_TO_SAM Index Descriptions

### NamedScheduleInstanceProperty

The primary table NamedScheduleInstanceProperty contains the names and
values of properties associated with named schedule instances.

  Column Name                      Explanation                                                                                                                 Data Type       Additional Information
  -------------------------------- --------------------------------------------------------------------------------------------------------------------------- --------------- ------------------------
  NamedScheduleInstancePropetyId   This column contains the NamedScheduleInstanceProperty ID that uniquely identifies each named schedule instance property.   int (4)
  ScheduleInstanceLinkId           This column contains the ID to link the property to a named instance of a schedule.                                         int (4)
  PropertyName                     This column contains the property names of the named schedule instance properties.                                          varchar (255)
  PropertyValue                    This column contains the property values of the named schedule instance properties.                                         varchar (255)

  : NamedScheduleInstanceProperty Column Descriptions

+-----------------------------------+---------------------------------+
| Index Code                        | Columns                         |
+===================================+=================================+
| IX_NamedScheduleInstanceP         | PropertyName                    |
| roperty_PropertyNamePropertyValue |                                 |
|                                   | PropertyValue                   |
+-----------------------------------+---------------------------------+
| PK_NamedScheduleInstanceProperty  | NamedScheduleInstancePropertyId |
+-----------------------------------+---------------------------------+

: NamedScheduleInstanceProperty Index Descriptions

### NOTIFY

The primary table NOTIFY contains notifications generated by Events on
Job Definitions, ENS, or external events. The SMA Notify Handler
processes all records in this table. When the SMA Notify Handler
retrieves the record successfully, it deletes the record.

  ----------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------
  ![White pencil/paper icon on gray circular background](../../Resources/Images/note-icon(48x48).png "Note icon")   **NOTE:** [The stored procedure 'SMA_CHECK_FOR_NOTIFICATION' should be used to insert data into the table.]
  ----------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| TRIGGERNAME | Name of the ENS | varchar (255)  | None            |
|             | Event trigger.  |                |                 |
+-------------+-----------------+----------------+-----------------+
| MACHNAME    | This column     | char (24)      | None            |
|             | contains the    |                |                 |
|             | machine names   |                |                 |
|             | associated with |                |                 |
|             | the events.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| SKDDATE     | This column     | int (4)        | -   This column |
|             | contains the    |                |     stores the  |
|             | date stamps of  |                |     date in SQL |
|             | the schedules.  |                |     format.     |
|             |                 |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| SKDNAME     | This column     | varchar (255)  | None            |
|             | contains the    |                |                 |
|             | descriptive     |                |                 |
|             | schedule names. |                |                 |
+-------------+-----------------+----------------+-----------------+
| INSTNO      | Contains a      | int (4)        | None            |
|             | number that     |                |                 |
|             | identifies the  |                |                 |
|             | instance of the |                |                 |
|             | schedules.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| JOBNAME     | -   This column | varchar (128)  | None            |
|             |     contains    |                |                 |
|             |     the job     |                |                 |
|             |     names.      |                |                 |
|             | -   A value in  |                |                 |
|             |     this column |                |                 |
|             |     is only     |                |                 |
|             |     present for |                |                 |
|             |     job event   |                |                 |
|             |     triggers.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| GROUPOFID   | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     ENS group   |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     ENSGROUPS   |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| ACTIONID    | This column     | int (4)        | None            |
|             | consists of the |                |                 |
|             | Action IDs from |                |                 |
|             | the ENSACTIONS  |                |                 |
|             | table.          |                |                 |
+-------------+-----------------+----------------+-----------------+
| ACTIONNAME  | This column     | varchar (255)  | None            |
|             | contains the    |                |                 |
|             | action names.   |                |                 |
|             |                 |                |                 |
|             | This column     |                |                 |
|             | contains the    |                |                 |
|             | information     |                |                 |
|             | from the        |                |                 |
|             | Description     |                |                 |
|             | field in the    |                |                 |
|             | ENS Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| ACTIONINCID | This column     | char (1)       | -   Y: Yes      |
|             | contains a flag |                | -   N: No       |
|             | determining if  |                |                 |
|             | each job's     |                |                 |
|             | unique number   |                |                 |
|             | is included     |                |                 |
|             | with the        |                |                 |
|             | notification.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| ACTIONTYPE  | This column     | int (4)        | -   1: Event    |
|             | consists of a   |                |     Log         |
|             | type of action  |                | -   2: E-Mail   |
|             | required.       |                | -   3: Net Send |
|             |                 |                | -   4: SNMP     |
|             |                 |                | -   5: SPO      |
|             |                 |                | -   6: Text     |
|             |                 |                |     Message     |
|             |                 |                | -   7:          |
|             |                 |                |     OpCon/xps   |
|             |                 |                |     Event       |
+-------------+-----------------+----------------+-----------------+
| ACTIONMSG   | This column     | varchar (4000) | None            |
|             | consists of the |                |                 |
|             | message content |                |                 |
|             | for the         |                |                 |
|             | notification.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| NOTIFYDELIM | The delimiter   | char (1)       | None            |
|             | for parsing the |                |                 |
|             | notification.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| RETRY_COUNT | This column     | int (4)        | None            |
|             | contains the    |                |                 |
|             | number of       |                |                 |
|             | attempts the    |                |                 |
|             | SMA Notify      |                |                 |
|             | Handler has     |                |                 |
|             | made to process |                |                 |
|             | each            |                |                 |
|             | notification.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| STATUS      | This column     | int (4)        | -   0: Not      |
|             | contains the    |                |     Processed   |
|             | statuses of the |                | -   1:          |
|             | notifications.  |                |     Processed   |
+-------------+-----------------+----------------+-----------------+
| PIPESEQKEY  | This column     | int (4)        | None            |
|             | contains        |                |                 |
|             | internal unique |                |                 |
|             | keys.           |                |                 |
+-------------+-----------------+----------------+-----------------+

: NOTIFY Column Descriptions

+------------+------------+
| Index Code | Columns    |
+============+============+
| PK_NOTIFY  | PIPESEQKEY |
+------------+------------+
| X_NOTIFY   | STATUS     |
|            |            |
|            | PIPESEQKEY |
+------------+------------+

: NOTIFY Index Descriptions

### OPCON_CONFIG

The OPCON_CONFIG table contains OpCon configuration information.

  Column Name    Explanation                                      Data Type        Additional Information
  -------------- ------------------------------------------------ ---------------- ------------------------
  CONFIG_KEY     This column contains the configuration keys.     varchar (16)     None
  CONFIG_VALUE   This column contains the configuration values.   varchar (4000)   None

  : OPCON_CONFIG Column Descriptions

  Index Code        Columns
  ----------------- ------------
  PK_OPCON_CONFIG   CONFIG_KEY

  : OPCON_CONFIG Index Descriptions

### OPCON_INFO

The OPCON_INFO table contains OpCon general information.

  Column Name   Explanation                                    Data Type        Additional Information
  ------------- ---------------------------------------------- ---------------- ------------------------
  INFO_KEY      This column contains the information keys.     varchar (16)     None
  INFO_VALUE    This column contains the information values.   varchar (4000)   None

  : OPCON_INFO Column Descriptions

  Index Code      Columns
  --------------- ----------
  PK_OPCON_INFO   INFO_KEY

  : OPCON_INFO Index Descriptions

### OPCONREQ

The OPCONREQ table contains requests to the SMA Request Router by
various request handlers.

  Column Name    Explanation                                                                         Data Type           Additional Information
  -------------- ----------------------------------------------------------------------------------- ------------------- -----------------------------------------------------------------
  REQTIMESTAMP   This column contains the time stamps of the requests.                               char (12)           None
  REQSRCDESC     This column contains the descriptions of the request sources.                       varchar (50)        None
  REQSRCID       This column contains the request source IDs.                                        varchar (50)        None
  REQHNDLR       This column contains the request handler names.                                     varchar (50)        None
  REQTYPE        This column contains the request types.                                             varchar (50)        None
  REQDSN         This column contains the names of the request data sources.                         varchar (50)        None
  REQEXPIRES     This column contains the expiration dates and times of the requests.                smalldatetime (4)   None
  REQPROCESSED   This column contains information determining if the requests have been processed.   smallint (2)        None
  REQLTH         Contains the length of the request.                                                 int (4)             None
  REQDETS        This column contains the details of the requests.                                   varchar (4000)      None
  REQTXTDETS     Contains text details of the request.                                               text (16)           Used only if the length of the request exceeds 4000 characters.

  : OPCONREQ Column Descriptions

  Index Code    Columns
  ------------- --------------
  PK_OPCONREQ   REQTIMESTAMP

  : OPCONREQ Index Descriptions

### OPCONRSP

The OPCONRSP table contains responses from the various request handlers.

  Column Name    Explanation                                                             Data Type           Additional Information
  -------------- ----------------------------------------------------------------------- ------------------- -----------------------------------------------------------------
  REQTIMESTAMP   This column contains the time stamps of the requests.                   char (12)           None
  REQSRCDESC     This column contains the descriptions of the request sources.           varchar (50)        None
  REQSRCID       This column contains the IDs of the request sources.                    varchar (50)        None
  RSPTYPE        This column contains the response types.                                varchar (50)        None
  RSPEXPIRES     This column contains the expiration dates and times of the responses.   smalldatetime (4)   None
  RSPLTH         This column contains the lengths of the responses.                      int (4)             None
  RSPDETS        This column contains the details of the responses.                      varchar (4000)      None
  RSPTXTDETS     This column contains the text details of the responses.                 text (16)           Used only if the length of the request exceeds 4000 characters.

  : OPCONRSP Column Descriptions

  Index Code    Columns
  ------------- --------------
  PK_OPCONRSP   REQTIMESTAMP

  : OPCONRSP Index Descriptions

### OPCONXPSEVENTS

The primary table OPCONXPSEVENTS contains a list of supported OpCon
events.

  Column Name   Explanation                                                 Data Type       Additional Information
  ------------- ----------------------------------------------------------- --------------- ------------------------
  EVENTID       This column contains the event IDs.                         smallint (2)    None
  EVENTNAME     This column contains the name associated with each event.   varchar (255)   None

  : OPCONXPSEVENTS Column Descriptions

  Index Code          Columns
  ------------------- ---------
  PK_OPCONXPSEVENTS

  : OPCONXPSEVENTS Index Descriptions

### RemoteInstances

The primary table RemoteInstances contains the details and status of a
remote instance notification.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| Id          | This column     | int            |                 |
|             | contains the ID |                |                 |
|             | that uniquely   |                |                 |
|             | identifies each |                |                 |
|             | remote          |                |                 |
|             | instance.       |                |                 |
+-------------+-----------------+----------------+-----------------+
| Name        | This column     | varchar (255)  |                 |
|             | contains the    |                |                 |
|             | name of the     |                |                 |
|             | remote          |                |                 |
|             | instances.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| Description | This column     | varchar (8000) |                 |
|             | contains the    |                |                 |
|             | description of  |                |                 |
|             | the remote      |                |                 |
|             | instance.       |                |                 |
+-------------+-----------------+----------------+-----------------+
| Value       | This column     | varchar (8000) |                 |
|             | contains value  |                |                 |
|             | of the          |                |                 |
|             | connection      |                |                 |
|             | string (or      |                |                 |
|             | URL).           |                |                 |
+-------------+-----------------+----------------+-----------------+
| Type        | This column     | varchar (10)   | C = connection  |
|             | contains the    |                | string          |
|             | type of remote  |                |                 |
|             | instance        |                | **Note**: More  |
|             | identifier      |                | options will be |
|             | (connection     |                | supported in a  |
|             | string or URL). |                | future release. |
+-------------+-----------------+----------------+-----------------+

: RemoteInstances Column Descriptions

### REPORTS

The primary table REPORTS contains the report specifications for all
reports that are recognized by OpCon. The reports are divided by user
types of public, and administrator. For interactively running reports,
OpCon only supports BIRT Reports.

+--------------+----------------+----------------+----------------+
| Column Name  | Explanation    | Data Type      | Additional     |
|              |                |                | Information    |
+==============+================+================+================+
| REPID        | -   This       | int (4)        | -   Positive   |
|              |     column     |                |     numbers    |
|              |     contains   |                |     indicate   |
|              |     the report |                |     reports    |
|              |     IDs.       |                |     are public |
|              | -   This       |                |     and        |
|              |     column     |                |     visible to |
|              |     specifies  |                |     all users. |
|              |     the user   |                | -   Negative   |
|              |     types,     |                |     numbers    |
|              |     public or  |                |     indicate   |
|              |                |                |     reports    |
|              | administrator. |                |     are only   |
|              |                |                |     visible by |
|              |                |                |     a          |
|              |                |                | dministrators. |
+--------------+----------------+----------------+----------------+
| REPDESC      | This column    | char (64)      | None           |
|              | contains the   |                |                |
|              | report titles. |                |                |
+--------------+----------------+----------------+----------------+
| REPFILE      | This column    | char (64)      | None           |
|              | contains the   |                |                |
|              | legacy Crystal |                |                |
|              | report         |                |                |
|              | filenames.     |                |                |
+--------------+----------------+----------------+----------------+
| REPPRIMTBL   | -   This       | varchar (128)  | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the name   |                |                |
|              |     of each    |                |                |
|              |     report's  |                |                |
|              |     primary    |                |                |
|              |     table.     |                |                |
|              | -   All other  |                |                |
|              |                |                |                |
|              |    information |                |                |
|              |     in the     |                |                |
|              |     report     |                |                |
|              |     originates |                |                |
|              |     from other |                |                |
|              |     tables     |                |                |
|              |     through    |                |                |
|              |     cros       |                |                |
|              | s-referencing. |                |                |
+--------------+----------------+----------------+----------------+
| REPFILTER    | This column    | int (4)        | -   This       |
|              | contains the   |                |     column     |
|              | report         |                |     contains a |
|              | selection      |                |     binary     |
|              | filters.       |                |     coded      |
|              |                |                |     number     |
|              |                |                |     indicating |
|              |                |                |     the        |
|              |                |                |                |
|              |                |                |    combination |
|              |                |                |     of Date,   |
|              |                |                |     Schedule   |
|              |                |                |     and        |
|              |                |                |     Department |
|              |                |                |     filters    |
|              |                |                |     that are   |
|              |                |                |     applicable |
|              |                |                |     to the     |
|              |                |                |     particular |
|              |                |                |     report.    |
|              |                |                | -   A filter   |
|              |                |                |     with all   |
|              |                |                |     three      |
|              |                |                |     dependents |
|              |                |                |     should     |
|              |                |                |     have a     |
|              |                |                |     value      |
|              |                |                |     of 7.      |
+--------------+----------------+----------------+----------------+
| REPSPSQL     | This column    | varchar (1000) | None           |
|              | contains a     |                |                |
|              | specially      |                |                |
|              | formatted      |                |                |
|              | field that     |                |                |
|              | contains       |                |                |
|              | information on |                |                |
|              | how to present |                |                |
|              | an additional  |                |                |
|              | record         |                |                |
|              | selection      |                |                |
|              | criterion      |                |                |
|              | through a      |                |                |
|              | drop-down list |                |                |
|              | displayed to   |                |                |
|              | you for some   |                |                |
|              | reports.       |                |                |
+--------------+----------------+----------------+----------------+
| REPLOCKED    | -   This       | char (1)       | None           |
|              |     column     |                |                |
|              |     indicates  |                |                |
|              |     if the     |                |                |
|              |     report     |                |                |
|              |     records    |                |                |
|              |     are        |                |                |
|              |     locked.    |                |                |
|              | -   Only the   |                |                |
|              |     OpCon      |                |                |
|              |                |                |                |
|              | administrative |                |                |
|              |     user       |                |                |
|              |                |                |                |
|              |   [ocadm]{.ul} |                |                | |              |     can unlock |                |                |
|              |     a report   |                |                |
|              |     for        |                |                |
|              |     editing.   |                |                |
+--------------+----------------+----------------+----------------+
| REPBIRTTMPLT | This column    | varchar (128)  | None           |
|              | contains the   |                |                |
|              | BIRT report    |                |                |
|              | template       |                |                |
|              | names.         |                |                |
+--------------+----------------+----------------+----------------+

: REPORTS Column Descriptions

  Index Code     Columns
  -------------- ---------
  PK\_ REPORTS   REPID

  : REPORTS Index Descriptions

### REQHANDLER

The REQHANDLER table contains information regarding the various request
handlers.

  Column Name   Explanation                                                  Data Type        Additional Information
  ------------- ------------------------------------------------------------ ---------------- ------------------------
  REQHNDLR      This column contains the request handler names.              varchar (50)     None
  RHFC          This column contains the request handler field codes.        int (4)          None
  RHSEQNO       This column contains the request handler sequence numbers.   smallint (2)     None
  RHVALUE       This column contains the request handler values.             varchar (4000)   None

  : REQHANDLER Column Descriptions

+---------------+----------+
| Index Code    | Columns  |
+===============+==========+
| PK_REQHANDLER | REQHNDLR |
|               |          |
|               | RHFC     |
|               |          |
|               | RHSEQNO  |
+---------------+----------+

: REQHANDLER Index Descriptions

### REQSOURCE

The REQSOURCE table contains information regarding the source of the
various request handlers.

  Column Name   Explanation                                                 Data Type        Additional Information
  ------------- ----------------------------------------------------------- ---------------- ------------------------
  REQSRCDESC    This column contains the request source descriptions.       varchar (50)     None
  RSFC          This column contains the request source field codes.        int (4)          None
  RSSEQNO       This column contains the request source sequence numbers.   smallint (2)     None
  RSVALUE       This column contains the request handler values.            varchar (4000)   None

  : REQSOURCE Column Descriptions

+--------------+------------+
| Index Code   | Columns    |
+==============+============+
| PK_REQSOURCE | REQSRCDESC |
|              |            |
|              | RSFC       |
|              |            |
|              | RSSEQNO    |
+--------------+------------+

: REQSOURCE Index Descriptions

### ROLE_SERVICE_REQUEST

The primary table ROLE_SERVICE_REQUEST is a relationship table that
links SMA Self Service requests with OpCon roles.

+-----------------+-----------------+-----------+-----------------+
| Column Name     | Explanation     | Data Type | Additional      |
|                 |                 |           | Information     |
+=================+=================+===========+=================+
| ROLEID          | -   This column | int (4)   | None            |
|                 |     contains    |           |                 |
|                 |     the role    |           |                 |
|                 |     IDs that    |           |                 |
|                 |     identify    |           |                 |
|                 |     roles       |           |                 |
|                 |     associated  |           |                 |
|                 |     with        |           |                 |
|                 |     service     |           |                 |
|                 |     requests.   |           |                 |
|                 | -   The ROLES   |           |                 |
|                 |     table is    |           |                 |
|                 |     referenced  |           |                 |
|                 |     from this   |           |                 |
|                 |     table via   |           |                 |
|                 |     this field. |           |                 |
+-----------------+-----------------+-----------+-----------------+
| SER             | This column     | int (4)   | None            |
| VICE_REQUEST_ID | contains        |           |                 |
|                 | service request |           |                 |
|                 | IDs that        |           |                 |
|                 | identify        |           |                 |
|                 | service         |           |                 |
|                 | requests        |           |                 |
|                 | associated with |           |                 |
|                 | roles.          |           |                 |
+-----------------+-----------------+-----------+-----------------+

: ROLE_SERVICE_REQUEST Column Descriptions

+-------------------------+--------------------+
| Index Code              | Columns            |
+=========================+====================+
| PK_ROLE_SERVICE_REQUEST | ROLEID             |
|                         |                    |
|                         | SERVICE_REQUEST_ID |
+-------------------------+--------------------+

: ROLE_SERVICE_REQUEST Index Descriptions

### ROLES

The primary table ROLES contains role information.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| ROLEID      | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     role IDs.    |               |                  |
|             | -   This column  |               |                  |
|             |     uniquely     |               |                  |
|             |     identifies   |               |                  |
|             |     each role.   |               |                  |
|             | -   Used for     |               |                  |
|             |     lookup from  |               |                  |
|             |     the          |               |                  |
|             |     AUDITHST,    |               |                  |
|             |     UACCESS,     |               |                  |
|             |     UDEPFUN,     |               |                  |
|             |     UMACHGRPS,   |               |                  |
|             |     UMACHS,      |               |                  |
|             |     USCHED,      |               |                  |
|             |     USERS_AUX,   |               |                  |
|             |     and USYSACC  |               |                  |
|             |     tables.      |               |                  |
+-------------+------------------+---------------+------------------+
| ROLENAME    | This column      | varchar (255) | None             |
|             | contains the     |               |                  |
|             | names of the     |               |                  |
|             | roles to which   |               |                  |
|             | users are        |               |                  |
|             | assigned.        |               |                  |
+-------------+------------------+---------------+------------------+

: ROLES Column Descriptions

  Index Code   Columns
  ------------ ----------
  PK_ROLES     ROLEID
  I2ROLES      ROLENAME

  : ROLES Index Descriptions

### ROLES_AUX

The secondary table ROLES_AUX contains auxiliary information about
Roles. The ROLEID links the auxiliary information to the primary
information.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| ROLEID      | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the role    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     ROLES       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| RAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| RASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| RAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: ROLES_AUX Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_ROLESAUX | ROLEID  |
|             |         |
|             | RAFC    |
|             |         |
|             | RASEQNO |
+-------------+---------+

: ROLES_AUX Index Descriptions

### RPTPARAMS

The RPTPARAMS table provides fields for reporting a query of the
database.

  Column Name   Explanation                               Data Type       Additional Information
  ------------- ----------------------------------------- --------------- ------------------------
  RPTPARAMID    This column is reserved for future use.   int (4)         None
  RPTFIELD1     This column is reserved for future use.   varchar (255)   None
  RPTFIELD2     This column is reserved for future use.   varchar (255)   None
  RPTFIELD3     This column is reserved for future use.   varchar (255)   None
  RPTFIELD4     This column is reserved for future use.   varchar (255)   None
  RPTFIELD5     This column is reserved for future use.   varchar (255)   None
  RPTFIELD6     This column is reserved for future use.   varchar (255)   None
  RPTFIELD7     This column is reserved for future use.   varchar (255)   None
  RPTFIELD8     This column is reserved for future use.   varchar (255)   None
  RPTFIELD9     This column is reserved for future use.   varchar (255)   None
  RPTFIELD10    This column is reserved for future use.   varchar (255)   None

  : RPTPARAMS Column Descriptions

  Index Code     Columns
  -------------- ------------
  PK_RPTPARAMS   RPTPARAMID

  : RPTPARAMS Index Descriptions

### Runner

The Runner table contains the command formats for the script types on
each platform.

+----------------+----------------+----------------+----------------+
| Column Name    | Explanation    | Data Type      | Additional     |
|                |                |                | Information    |
+================+================+================+================+
| RunnerId       | This column    | int (4)        | None           |
|                | contains the   |                |                |
|                | Runner IDs     |                |                |
|                | that uniquely  |                |                |
|                | identify each  |                |                |
|                | runner.        |                |                |
+----------------+----------------+----------------+----------------+
| ScriptTypeId   | -   This       | int (4)        | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the ID of  |                |                |
|                |     the script |                |                |
|                |     type.      |                |                |
|                | -   The column |                |                |
|                |     references |                |                |
|                |     the        |                |                |
|                |     ScriptType |                |                |
|                |     table.     |                |                |
+----------------+----------------+----------------+----------------+
| O              | -   This       | int (4)        | None           |
| pConPlatformId |     column     |                |                |
|                |     contains   |                |                |
|                |     the ID of  |                |                |
|                |     the OpCon  |                |                |
|                |     Agent      |                |                |
|                |     platform.  |                |                |
|                | -   The column |                |                |
|                |     references |                |                |
|                |     the        |                |                |
|                |     LSAMTYPES  |                |                |
|                |     table.     |                |                |
+----------------+----------------+----------------+----------------+
| Name           | This column    | nvarchar (255) | None           |
|                | contains the   |                |                |
|                | name of the    |                |                |
|                | runner.        |                |                |
+----------------+----------------+----------------+----------------+
| CommandFormat  | This column    | varchar (4000) | None           |
|                | contains the   |                |                |
|                | command        |                |                |
|                | formats for    |                |                |
|                | the script     |                |                |
|                | type and       |                |                |
|                | platform       |                |                |
|                | combination.   |                |                |
+----------------+----------------+----------------+----------------+
| CreatedDate    | This column    | datetime (8)   | None           |
|                | contains the   |                |                |
|                | date and time  |                |                |
|                | that this      |                |                |
|                | script type    |                |                |
|                | was created.   |                |                |
+----------------+----------------+----------------+----------------+
| LastUpdated    | This column    | datetime (8)   | None           |
|                | contains the   |                |                |
|                | date and time  |                |                |
|                | that the row   |                |                |
|                | was last       |                |                |
|                | updated.       |                |                |
+----------------+----------------+----------------+----------------+

: Runner Column Descriptions

  Index Code   Columns
  ------------ ----------
  PK_Runner    RunnerId

  : Runner Index Descriptions

### SAMPULSE

The SAMPULSE table indicates if the SAM is processing or not.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| SAMID       | This column is   | smallint (2) | None             |
|             | reserved for     |              |                  |
|             | future use.      |              |                  |
+-------------+------------------+--------------+------------------+
| SAMSTAMP    | This column      | float (8)    | -   This column  |
|             | contains the     |              |     stores the   |
|             | date/time stamp  |              |     date in SQL  |
|             | of the last      |              |     format.      |
|             | pulse sent from  |              | -   The integer  |
|             | the SAM.         |              |     part of the  |
|             |                  |              |     SQL date     |
|             |                  |              |     represents   |
|             |                  |              |     the day      |
|             |                  |              |     count since  |
|             |                  |              |     Saturday,    |
|             |                  |              |     December     |
|             |                  |              |     30, 1899.    |
|             |                  |              | -   The          |
|             |                  |              |     fractional   |
|             |                  |              |     part of the  |
|             |                  |              |     SQL date     |
|             |                  |              |     represents   |
|             |                  |              |     the time in  |
|             |                  |              |     seconds      |
|             |                  |              |     since        |
|             |                  |              |     midnight.    |
+-------------+------------------+--------------+------------------+

: SAMPULSE Column Descriptions

  Index Code      Columns
  --------------- ---------
  PK\_ SAMPULSE   SAMID

  : SAMPULSE Index Descriptions

### ScheduleInstance

The primary table ScheduleInstance contains the identifying details of
named schedule instances.

  Column Name              Explanation                                                                                                                                             Data Type       Additional Information
  ------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------- --------------- --------------------------------------------------------------------------
  ScheduleInstanceId       This column contains ScheduleInstance IDs that uniquely identify each named schedule instance. The ScheduleInstanceLink table references this column.   int (4)
  ScheduleInstanceName     This column contains the name of the named schedule instance.                                                                                           varchar (255)
  ScheduleInstanceNumber   This column contains the predefined instance number assigned to the named schedule instance.                                                            int (4)         Predefined instance numbers of named schedules must be negative numbers.

  : ScheduleInstance Column Descriptions

  Index Code                                 Columns
  ------------------------------------------ ----------------------
  IX_ScheduleInstance_ScheduleInstanceName   ScheduleInstanceName
  PK_ScheduleInstance                        ScheduleInstanceId

  : ScheduleInstance Index Descriptions

### ScheduleInstanceLink

The primary table ScheduleInstanceLink contains the identifying details
needed to link schedules with schedule instances names.

  Column Name              Explanation                                                                                                                                                                                            Data Type   Additional Information
  ------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ ----------- ------------------------
  ScheduleInstanceLinkId   This column contains ScheduleInstanceLink IDs that uniquely identify each link between a schedule and a schedule instance name. The ScheduleException and JobException tables reference this column.   int (4)
  ScheduleId               This column contains the IDs of schedules that are associated with schedule instance names. These IDs reference the SNAME table.                                                                       int (4)
  ScheduleInstanceId       This column contains the IDs of predefined schedule instances associated with schedules. These IDs reference the ScheduleInstance table.                                                               int (4)

  : ScheduleInstanceLink Column Descriptions

  Index Code                           Columns
  ------------------------------------ ------------------------
  IX_ScheduleInstanceLink_ScheduleId   ScheduleId
  PK_ScheduleInstanceLink              ScheduleInstanceLinkId

  : ScheduleInstanceLink Index Descriptions

### ScheduleWithJobPattern

The primary table ScheduleWithJobPattern associates named schedule
instances with job name patterns.

  Column Name                Explanation                                                                                Data Type   Additional Information
  -------------------------- ------------------------------------------------------------------------------------------ ----------- ------------------------
  ScheduleWithJobPatternId   This column contains ScheduleWithJobPattern IDs that uniquely identify each association.   int (4)
  ScheduleInstanceLinkId     This column contains the ID to link to the ScheduleInstanceLink table.                     int (4)
  JobPatternId               This column contains the ID to link to the JobPattern table.                               int (4)

  : ScheduleWithJobPattern Column Descriptions

+------------------------------------------+--------------------------+
| Index Code                               | Columns                  |
+==========================================+==========================+
| IX_ScheduleWithJobPa                     | ScheduleInstanceLinkId   |
| ttern_ScheduleInstanceLinkIdJobPatternId |                          |
|                                          | JobPatternId             |
+------------------------------------------+--------------------------+
| PK_ScheduleWithJobPattern                | ScheduleWithJobPatternId |
+------------------------------------------+--------------------------+

: ScheduleWithJobPattern Index Descriptions

### ScheduleWithJobPatternException

The primary table ScheduleWithJobPatternException associates job name
patterns in named schedule instances with exceptions.

  Column Name                         Explanation                                                                                         Data Type   Additional Information
  ----------------------------------- --------------------------------------------------------------------------------------------------- ----------- ------------------------
  ScheduleWithJobPatternExceptionId   This column contains ScheduleWithJobPatternException IDs that uniquely identify each association.   int (4)
  ScheduleWithJobPatternId            This column contains the ID to link to the ScheduleWithJobPattern table.                            int (4)
  ExceptionId                         This column contains the ID to link to the Exception table.                                         int (4)

  : ScheduleWithJobPatternException Column Descriptions

+----------------------------------+----------------------------------+
| Index Code                       | Columns                          |
+==================================+==================================+
| IX_Sch                           | ScheduleWithJobPatternId         |
| eduleWithJobPatternException_Sch |                                  |
| eduleWithJobPatternIdExceptionId | ExceptionId                      |
+----------------------------------+----------------------------------+
| PK                               | S                                |
| _ScheduleWithJobPatternException | cheduleWithJobPatternExceptionId |
+----------------------------------+----------------------------------+

: ScheduleWithJobPatternException Index Descriptions

### SCOPE

The SCOPE table contains scope definition information for WebOpCon.

  Column Name   Explanation                              Data Type      Additional Information
  ------------- ---------------------------------------- -------------- ------------------------
  USERID        This column contains the user IDs.       smallint (2)   None
  SCOPENAME     This column contains the scope names.    char (40)      None
  FIELDNAME     This column contains the field names.    char (40)      None
  FIELDVALUE    This column contains the field values.   char (40)      None

  : SCOPE Column Descriptions

+------------+------------+
| Index Code | Columns    |
+============+============+
| PK_SCOPE   | USERID     |
|            |            |
|            | SCOPENAME  |
|            |            |
|            | FIELDNAME  |
|            |            |
|            | FIELDVALUE |
+------------+------------+

: SCOPE Index Descriptions

### Script

The Script table contains the name and description of scripts in use in
the environment.

+----------------+----------------+----------------+----------------+
| Column Name    | Explanation    | Data Type      | Additional     |
|                |                |                | Information    |
+================+================+================+================+
| ScriptId       | -   This       | int (4)        | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the Script |                |                |
|                |     IDs that   |                |                |
|                |     uniquely   |                |                |
|                |     identify   |                |                |
|                |     each       |                |                |
|                |     script.    |                |                |
|                | -   The        |                |                |
|                |                |                |                |
|                |  ScriptVersion |                |                |
|                |     and        |                |                |
|                |     S          |                |                |
|                | criptingEngine |                |                |
|                |     tables     |                |                |
|                |     references |                |                |
|                |     this       |                |                |
|                |     column.    |                |                |
+----------------+----------------+----------------+----------------+
| ScriptTypeId   | -   This       | int (4)        | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the        |                |                |
|                |     ScriptType |                |                |
|                |     IDs that   |                |                |
|                |     uniquely   |                |                |
|                |     identify   |                |                |
|                |     each       |                |                |
|                |     script     |                |                |
|                |     type.      |                |                |
|                | -   The column |                |                |
|                |     is a       |                |                |
|                |     reference  |                |                |
|                |     to the     |                |                |
|                |     ScriptType |                |                |
|                |     table.     |                |                |
+----------------+----------------+----------------+----------------+
| Name           | -   This       | varchar (255)  | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the ID of  |                |                |
|                |     the script |                |                |
|                |     type.      |                |                |
|                | -   It         |                |                |
|                |     references |                |                |
|                |     the        |                |                |
|                |     associated |                |                |
|                |     script     |                |                |
|                |     type in    |                |                |
|                |     the        |                |                |
|                |     ScriptType |                |                |
|                |     table.     |                |                |
+----------------+----------------+----------------+----------------+
| Scr            | This column    | nvarchar       | None           |
| iptDescription | contains an    | (4000)         |                |
|                | optional       |                |                |
|                | description of |                |                |
|                | the script     |                |                |
|                | type.          |                |                |
+----------------+----------------+----------------+----------------+
| CreatedDate    | This column    | datetime (8)   | None           |
|                | contains the   |                |                |
|                | date and time  |                |                |
|                | that this      |                |                |
|                | script type    |                |                |
|                | was created.   |                |                |
+----------------+----------------+----------------+----------------+
| LastUpdated    | This column    | datetime (8)   | None           |
|                | contains the   |                |                |
|                | date and time  |                |                |
|                | that the row   |                |                |
|                | was last       |                |                |
|                | updated.       |                |                |
+----------------+----------------+----------------+----------------+

: Script Column Descriptions

  Index Code   Columns
  ------------ ----------
  PK_Script    ScriptId

  : Script Index Descriptions

### ScriptType

The ScriptType table contains the types of scripts in use in the
environment (e.g., PowerShell, Perl, Python, VBScript).

+----------------+----------------+----------------+----------------+
| Column Name    | Explanation    | Data Type      | Additional     |
|                |                |                | Information    |
+================+================+================+================+
| ScriptTypeId   | -   This       | int (4)        | None           |
|                |     column     |                |                |
|                |     contains   |                |                |
|                |     the        |                |                |
|                |     ScriptType |                |                |
|                |     IDs that   |                |                |
|                |     uniquely   |                |                |
|                |     identify   |                |                |
|                |     each       |                |                |
|                |     script     |                |                |
|                |     type.      |                |                |
|                | -   The Script |                |                |
|                |     table      |                |                |
|                |     references |                |                |
|                |     this       |                |                |
|                |     column.    |                |                |
+----------------+----------------+----------------+----------------+
| Name           | This column    | nvarchar (255) | None           |
|                | contains the   |                |                |
|                | name of the    |                |                |
|                | script type.   |                |                |
+----------------+----------------+----------------+----------------+
| ScriptT        | This column    | nvarchar       | None           |
| ypeDescription | contains an    | (4000)         |                |
|                | optional       |                |                |
|                | description of |                |                |
|                | the script     |                |                |
|                | type.          |                |                |
+----------------+----------------+----------------+----------------+
| FileExtension  | This column    | varchar (255)  | None           |
|                | contains the   |                |                |
|                | file extension |                |                |
|                | for script     |                |                |
|                | files of this  |                |                |
|                | type.          |                |                |
+----------------+----------------+----------------+----------------+
| CreatedDate    | This column    | datetime (8)   | None           |
|                | contains the   |                |                |
|                | date and time  |                |                |
|                | that this      |                |                |
|                | script type    |                |                |
|                | was created.   |                |                |
+----------------+----------------+----------------+----------------+
| LastUpdated    | This column    | datetime (8)   | None           |
|                | contains the   |                |                |
|                | date and time  |                |                |
|                | that the row   |                |                |
|                | was last       |                |                |
|                | updated.       |                |                |
+----------------+----------------+----------------+----------------+

: ScriptType Column Descriptions

  Index Code      Columns
  --------------- --------------
  PK_ScriptType   ScriptTypeId

  : Script Index Descriptions

### ScriptVersion

The ScriptVersion table contains the versioned script content.

  Column Name       Explanation                                                                                      Data Type         Additional Information
  ----------------- ------------------------------------------------------------------------------------------------ ----------------- ------------------------
  ScriptVersionId   This column contains ScriptVersion IDs that uniquely identify each version of each script.       int (4)           None
  ScriptId          This column references the Script table which contains the name and description of the script.   int (4)           None
  ScriptVersion     This column contains the version number for this version of the script.                          int (4)           None
  Comment           This column contains a comment describing pertinent details of this version of the script.       nvarchar (4000)   None
  Content           This column contains the script content itself.                                                  varchar (max)     None
  CreatedDate       This column contains the date and time that this version of the script was created.              datetime (8)      None
  LastUpdated       This column contains the date and time that the row was last updated.                            datetime (8)      None
  UserSignon        This column contains the user login of the user that created this version of the script.         char (512)        None
  ContentHash       This column contains the MD5 hash of the script content.                                         char (32)         None

  : ScriptVersion Column Descriptions

  Index Code         Columns
  ------------------ -----------------
  PK_ScriptVersion   ScriptVersionId

  : ScriptVersion Index Descriptions

### SDEPJOB

The SDEPJOB table contains Daily Schedule Job Dependency Details.

+---------------+-----------------+---------------+-----------------+
| Column Name   | Explanation     | Data Type     | Additional      |
|               |                 |               | Information     |
+===============+=================+===============+=================+
| SKDDATE       | This column     | int (4)       | -   This column |
|               | contains the    |               |     stores the  |
|               | date stamps of  |               |     date in SQL |
|               | the schedules.  |               |     format.     |
|               |                 |               | -   The integer |
|               |                 |               |     represents  |
|               |                 |               |     the day     |
|               |                 |               |     count since |
|               |                 |               |     Saturday,   |
|               |                 |               |     December    |
|               |                 |               |     30, 1899.   |
+---------------+-----------------+---------------+-----------------+
| SKDID         | This column     | int (4)       | None            |
|               | contains the    |               |                 |
|               | schedule IDs.   |               |                 |
|               |                 |               |                 |
|               | This column     |               |                 |
|               | contains        |               |                 |
|               | cross-reference |               |                 |
|               | information for |               |                 |
|               | lookup into the |               |                 |
|               | SNAME table.    |               |                 |
+---------------+-----------------+---------------+-----------------+
| INSTNO        | Contains a      | int (4)       | None            |
|               | number that     |               |                 |
|               | identifies the  |               |                 |
|               | instance of the |               |                 |
|               | schedules.      |               |                 |
+---------------+-----------------+---------------+-----------------+
| JOBNAME       | -   This column | varchar (128) | None            |
|               |     contains    |               |                 |
|               |     the job     |               |                 |
|               |     names.      |               |                 |
|               | -   The job     |               |                 |
|               |     names must  |               |                 |
|               |     be unique   |               |                 |
|               |     within each |               |                 |
|               |     schedule.   |               |                 |
|               | -   The         |               |                 |
|               |     schedule ID |               |                 |
|               |     (SKDID)     |               |                 |
|               |     identifies  |               |                 |
|               |     the         |               |                 |
|               |     schedule.   |               |                 |
+---------------+-----------------+---------------+-----------------+
| FREQNAME      | -   This column | char (20)     | None            |
|               |     contains    |               |                 |
|               |     the         |               |                 |
|               |     frequency   |               |                 |
|               |     names.      |               |                 |
|               | -   The         |               |                 |
|               |     frequency   |               |                 |
|               |     names must  |               |                 |
|               |     be unique   |               |                 |
|               |     within each |               |                 |
|               |     job.        |               |                 |
|               | -   The job     |               |                 |
|               |     name        |               |                 |
|               |     (JOBNAME)   |               |                 |
|               |     identifies  |               |                 |
|               |     the job.    |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPSKDID      | -   This column | int (4)       | None            |
|               |     contains    |               |                 |
|               |     the IDs of  |               |                 |
|               |     the         |               |                 |
|               |     schedules   |               |                 |
|               |     containing  |               |                 |
|               |     the jobs in |               |                 |
|               |     the         |               |                 |
|               |     DEPJOBNAME  |               |                 |
|               |     column.     |               |                 |
|               | -   This column |               |                 |
|               |     contains    |               |                 |
|               |                 |               |                 |
|               | cross-reference |               |                 |
|               |     information |               |                 |
|               |     for lookup  |               |                 |
|               |     into the    |               |                 |
|               |     SNAME       |               |                 |
|               |     table.      |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPJOBNAME    | This column     | varchar (128) | None            |
|               | contains the    |               |                 |
|               | names of the    |               |                 |
|               | jobs that the   |               |                 |
|               | jobs in the     |               |                 |
|               | JOBNAME column  |               |                 |
|               | are dependent   |               |                 |
|               | on.             |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPDATEOFFSET | -   This column | smallint (2)  | None            |
|               |     contains    |               |                 |
|               |     the number  |               |                 |
|               |     of days     |               |                 |
|               |     offset from |               |                 |
|               |     the         |               |                 |
|               |     schedule    |               |                 |
|               |     dates.      |               |                 |
|               | -   The         |               |                 |
|               |     consequent  |               |                 |
|               |     date is     |               |                 |
|               |     checked for |               |                 |
|               |                 |               |                 |
|               |   dependencies. |               |                 |
+---------------+-----------------+---------------+-----------------+
| DEPTYPE       | This column     | smallint (2)  | -   1: Required |
|               | contains the    |               | -   2: Conflict |
|               | dependency      |               |     (Check day  |
|               | types.          |               |     for name)   |
|               |                 |               | -   3: After    |
|               |                 |               | -   4: Excludes |
|               |                 |               | -   34:         |
|               |                 |               |     Conflict    |
|               |                 |               |     (Check day  |
|               |                 |               |     for job     |
|               |                 |               |     name like)  |
|               |                 |               | -   66:         |
|               |                 |               |     Conflict    |
|               |                 |               |     (Check all  |
|               |                 |               |     days for    |
|               |                 |               |     job name)   |
|               |                 |               | -   98:         |
|               |                 |               |     Conflict    |
|               |                 |               |     (Check all  |
|               |                 |               |     days for    |
|               |                 |               |     job name    |
|               |                 |               |     like)       |
|               |                 |               | -   129:        |
|               |                 |               |     Required    |
|               |                 |               |     (ignore     |
|               |                 |               |     exit code)  |
|               |                 |               | -   131: After  |
|               |                 |               |     (ignore     |
|               |                 |               |     exit code)  |
|               |                 |               | -   257:        |
|               |                 |               |     Required    |
|               |                 |               |     (On         |
|               |                 |               |     Failure)    |
|               |                 |               | -   259: After  |
|               |                 |               |     (On         |
|               |                 |               |     Failure)    |
+---------------+-----------------+---------------+-----------------+

: SDEPJOB Column Descriptions

+--------------+---------------+
| Index Code   | Columns       |
+==============+===============+
| PK\_ SDEPJOB | SKDDATE       |
|              |               |
|              | SKDID         |
|              |               |
|              | JOBNAME       |
|              |               |
|              | FREQNAME      |
|              |               |
|              | DEPSKDID      |
|              |               |
|              | DEPJOBNAME    |
|              |               |
|              | DEPDATEOFFSET |
+--------------+---------------+
| I2SDEPJOB    | DEPSKDID      |
|              |               |
|              | DEPJOBNAME    |
+--------------+---------------+

: SDEPJOB Index Descriptions

### SDEPTHR

The SDEPTHR table contains Daily Schedule Threshold Dependency details.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDDATE     | This column      | int (4)       | -   This column  |
|             | contains the     |               |     stores the   |
|             | date stamps of   |               |     date in SQL  |
|             | the schedules.   |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
+-------------+------------------+---------------+------------------+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| INSTNO      | Contains a       | int (4)       | None             |
|             | number that      |               |                  |
|             | identifies the   |               |                  |
|             | instance of the  |               |                  |
|             | schedules.       |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTHRID    | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     IDs of the   |               |                  |
|             |     thre         |               |                  |
|             | sholds/resources |               |                  |
|             |     on which the |               |                  |
|             |     jobs in the  |               |                  |
|             |     JOBNAME      |               |                  |
|             |     column       |               |                  |
|             |     depend.      |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     THRESH       |               |                  |
|             |     table.       |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTHRVAL   | This column      | int (4)       | The valid value  |
|             | contains the     |               | range is from    |
|             | values used to   |               | zero (0) to      |
|             | compare against  |               | 2,147,483,647.   |
|             | the values of    |               |                  |
|             | the              |               |                  |
|             | thre             |               |                  |
|             | sholds/resources |               |                  |
|             | at each job's   |               |                  |
|             | run time.        |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTHROPER  | This column      | smallint (2)  | -   0: Equal (=) |
|             | contains the     |               | -   1: Greater   |
|             | arithmetic       |               |     Than (\>)    |
|             | operators used   |               | -   2: Less Than |
|             | to compare the   |               |     (\<)         |
|             | DEPTHRVAL values |               | -   3: Greater   |
|             | against the      |               |     Than or      |
|             | current values   |               |     Equal (\>=)  |
|             | of the           |               | -   4: Less Than |
|             | thre             |               |     or Equal     |
|             | sholds/resources |               |     (\<=)        |
|             | at each job's   |               | -   5: Not Equal |
|             | run time.        |               |     (\<\>)       |
+-------------+------------------+---------------+------------------+
| USEALL      | This column      | char (5)      | -   Valid values |
|             | indicates if the |               |     are True and |
|             | dependency       |               |     False        |
|             | requires all     |               |     (default)    |
|             | resources for    |               | -   This value   |
|             | the defined      |               |     must be      |
|             | resource.        |               |     False if the |
|             |                  |               |     DEPTHRVAL    |
|             |                  |               |     column is    |
|             |                  |               |     any number   |
|             |                  |               |     other than   |
|             |                  |               |     zero (0).    |
+-------------+------------------+---------------+------------------+

: SDEPTHR Column Descriptions

+--------------+----------+
| Index Code   | Columns  |
+==============+==========+
| PK\_ SDEPTHR | SKDDATE  |
|              |          |
|              | SKDID    |
|              |          |
|              | JOBNAME  |
|              |          |
|              | FREQNAME |
|              |          |
|              | DEPTHRID |
+--------------+----------+

: SDEPTHR Index Descriptions

### SDOCS

The SDOCS table contains Daily job documentation details.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDDATE     | This column      | int (4)       | -   This column  |
|             | contains the     |               |     stores the   |
|             | date stamps of   |               |     date in SQL  |
|             | the schedules.   |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
+-------------+------------------+---------------+------------------+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| INSTNO      | Contains a       | int (4)       | None             |
|             | number that      |               |                  |
|             | identifies the   |               |                  |
|             | instance of the  |               |                  |
|             | schedules.       |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| DOCID       | This column is   | smallint (2)  | None             |
|             | reserved for     |               |                  |
|             | future use.      |               |                  |
+-------------+------------------+---------------+------------------+
| DOCLINE     | This column      | smallint (2)  | The              |
|             | contains the     |               | documentation    |
|             | documentation    |               | lines should     |
|             | line numbers.    |               | start with 0 and |
|             |                  |               | increment        |
|             |                  |               | consecutively.   |
+-------------+------------------+---------------+------------------+
| DOCTEXT     | This column      | char (80)     | None             |
|             | contains the     |               |                  |
|             | documentation    |               |                  |
|             | text for each    |               |                  |
|             | line number.     |               |                  |
+-------------+------------------+---------------+------------------+

: SDOCS Column Descriptions

+------------+----------+
| Index Code | Columns  |
+============+==========+
| PK\_ SDOCS | SKDDATE  |
|            |          |
|            | SKDID    |
|            |          |
|            | JOBNAME  |
|            |          |
|            | FREQNAME |
|            |          |
|            | DOCID    |
|            |          |
|            | DOCLINE  |
+------------+----------+

: SDOCS Index Descriptions

### SERVICE_REQUEST

The primary table SERVICE_REQUEST contains base information describing
requests made via the SMA Solution Manager Self Service module.

+----------------+----------------+----------------+----------------+
| Column Name    | Explanation    | Data Type      | Additional     |
|                |                |                | Information    |
+================+================+================+================+
| SERV           | -   This       | int (4)        | This column is |
| ICE_REQUEST_ID |     column     |                | auto           |
|                |     contains   |                | generated.     |
|                |     Service    |                |                |
|                |     Request    |                |                |
|                |     IDs that   |                |                |
|                |     uniquely   |                |                |
|                |     identify   |                |                |
|                |     each       |                |                |
|                |     service    |                |                |
|                |     request.   |                |                |
|                | -   The        |                |                |
|                |     ROLE_S     |                |                |
|                | ERVICE_REQUEST |                |                |
|                |     table      |                |                |
|                |     references |                |                |
|                |     this       |                |                |
|                |     table.     |                |                |
+----------------+----------------+----------------+----------------+
| NAME           | This column    | nvarchar (max) | None           |
|                | contains       |                |                |
|                | Service        |                |                |
|                | Request names. |                |                |
+----------------+----------------+----------------+----------------+
| DOCUMENTATION  | This column    | nvarchar (max) | None           |
|                | contains       |                |                |
|                | Service        |                |                |
|                | Request        |                |                |
|                | documentation. |                |                |
+----------------+----------------+----------------+----------------+
| HTML           | This column    | nvarchar (max) | None           |
|                | contains       |                |                |
|                | Service        |                |                |
|                | Request HTML.  |                |                |
+----------------+----------------+----------------+----------------+
| DETAILS        | This column    | nvarchar (max) | This column    |
|                | contains       |                | will be used   |
|                | Service        |                | to store XML.  |
|                | Request        |                |                |
|                | details.       |                |                |
+----------------+----------------+----------------+----------------+

: SERVICE_REQUEST Column Descriptions

  Index Code             Columns
  ---------------------- --------------------
  PK\_ SERVICE_REQUEST   SERVICE REQUEST_ID

  : SERVICE_REQUEST Index Descriptions

### SEVENTS

The SEVENTS table contains information on internal events that should be
triggered when the job terminates with a specified status.

+--------------+----------------+----------------+----------------+
| Column Name  | Explanation    | Data Type      | Additional     |
|              |                |                | Information    |
+==============+================+================+================+
| SKDDATE      | This column    | int (4)        | -   This       |
|              | contains the   |                |     column     |
|              | date stamps of |                |     stores the |
|              | the schedules. |                |     date in    |
|              |                |                |     SQL        |
|              |                |                |     format.    |
|              |                |                | -   The        |
|              |                |                |     integer    |
|              |                |                |     represents |
|              |                |                |     the day    |
|              |                |                |     count      |
|              |                |                |     since      |
|              |                |                |     Saturday,  |
|              |                |                |     December   |
|              |                |                |     30, 1899.  |
+--------------+----------------+----------------+----------------+
| SKDID        | -   This       | int (4)        | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the        |                |                |
|              |     schedule   |                |                |
|              |     IDs.       |                |                |
|              | -   This       |                |                |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     c          |                |                |
|              | ross-reference |                |                |
|              |                |                |                |
|              |    information |                |                |
|              |     for lookup |                |                |
|              |     into the   |                |                |
|              |     SNAME      |                |                |
|              |     table.     |                |                |
+--------------+----------------+----------------+----------------+
| INSTNO       | Contains a     | int (4)        | None           |
|              | number that    |                |                |
|              | identifies the |                |                |
|              | instance of    |                |                |
|              | the schedules. |                |                |
+--------------+----------------+----------------+----------------+
| JOBNAME      | -   This       | varchar (128)  | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the job    |                |                |
|              |     names.     |                |                |
|              | -   The job    |                |                |
|              |     names must |                |                |
|              |     be unique  |                |                |
|              |     within     |                |                |
|              |     each       |                |                |
|              |     schedule.  |                |                |
|              | -   The        |                |                |
|              |     schedule   |                |                |
|              |     ID (SKDID) |                |                |
|              |     identifies |                |                |
|              |     the        |                |                |
|              |     schedule.  |                |                |
+--------------+----------------+----------------+----------------+
| FEEDBACKFC   | -   This       | int            | -   0: The     |
|              |     column     |                |     JOBSTATUS  |
|              |     contains   |                |     value will |
|              |     the field  |                |     trigger    |
|              |     code for   |                |     the event. |
|              |     the LSAM   |                | -   922: The   |
|              |     Feedback   |                |     Exit       |
|              |     item that  |                |                |
|              |     will       |                |    Description |
|              |     trigger    |                |     will be    |
|              |     the event. |                |     used to    |
|              | -   The code   |                |     determine  |
|              |     can be     |                |     the event  |
|              |     specific   |                |     trigger.   |
|              |     to a       |                | -   All other  |
|              |                |                |     values are |
|              |    platform's |                |     plat       |
|              |     list of    |                | form-specific. |
|              |     feedback,  |                |                |
|              |     or it will |                |                |
|              |     be a       |                |                |
|              |     specific   |                |                |
|              |     value if   |                |                |
|              |     the Exit   |                |                |
|              |                |                |                |
|              |    Description |                |                |
|              |     will       |                |                |
|              |     trigger    |                |                |
|              |     the event. |                |                |
+--------------+----------------+----------------+----------------+
| LSAMFEEDBACK | This column    | varchar (4000) | When           |
|              | contains the   |                | FEEDBACKFC is: |
|              | comparison     |                |                |
|              | string for the |                | -   0: The     |
|              | value of the   |                |     value in   |
|              | feedback.      |                |     this       |
|              |                |                |     column is  |
|              |                |                |     an empty   |
|              |                |                |     string.    |
|              |                |                | -   922: The   |
|              |                |                |     value      |
|              |                |                |     contains   |
|              |                |                |     an         |
|              |                |                |     operator a |
|              |                |                |     colon (:)  |
|              |                |                |     and the    |
|              |                |                |     comparison |
|              |                |                |     string     |
|              |                |                |     (e.g.,     |
|              |                |                |     EQ:32004). |
|              |                |                | -   Any other  |
|              |                |                |     values     |
|              |                |                |     contain a  |
|              |                |                |     string for |
|              |                |                |                |
|              |                |                |    comparison. |
+--------------+----------------+----------------+----------------+
| FREQNAME     | -   This       | char (20)      | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the        |                |                |
|              |     frequency  |                |                |
|              |     names.     |                |                |
|              | -   The        |                |                |
|              |     frequency  |                |                |
|              |     names must |                |                |
|              |     be unique  |                |                |
|              |     within     |                |                |
|              |     each job.  |                |                |
|              | -   The job    |                |                |
|              |     name       |                |                |
|              |     (JOBNAME)  |                |                |
|              |     identifies |                |                |
|              |     the job.   |                |                |
+--------------+----------------+----------------+----------------+
| JOBSTATUS    | This column    | smallint (2)   | -   500:       |
|              | contains the   |                |     Running    |
|              | job statuses   |                |     (Time      |
|              | that trigger   |                |     Exceeded)  |
|              | the events.    |                | -   900:       |
|              |                |                |     Finished   |
|              |                |                |     OK         |
|              |                |                | -   910:       |
|              |                |                |     Failed     |
|              |                |                | -   940:       |
|              |                |                |     Skipped    |
+--------------+----------------+----------------+----------------+
| EVDETS       | -   This       | varchar (738)  | None           |
|              |     column     |                |                |
|              |     contains   |                |                |
|              |     the event  |                |                |
|              |     details to |                |                |
|              |     execute.   |                |                |
|              | -   This       |                |                |
|              |     column can |                |                |
|              |     contain    |                |                |
|              |     expandable |                |                |
|              |     tokens,    |                |                |
|              |     which the  |                |                |
|              |     SAM        |                |                |
|              |     interprets |                |                |
|              |     at         |                |                |
|              |     run-time.  |                |                |
|              | -   For more   |                |                |
|              |                |                |                |
|              |    information |                |                |
|              |     on valid   |                |                |
|              |     OpCon      |                |                |
|              |     events,    |                |                |
|              |     refer to   |                |                |
|              |     the [OpCon |                |                | |              |                |                |                |
|              |    Events](../ |                |                |
|              | OpCon-Events |                |                |
|              | /Introduction.md) |                |                |
|              |     online     |                |                |
|              |     help.      |                |                |
+--------------+----------------+----------------+----------------+
| USERID       | This column is | smallint (2)   | None           |
|              | reserved for   |                |                |
|              | future use.    |                |                |
+--------------+----------------+----------------+----------------+

: SEVENTS Column Descriptions

+--------------+-----------+
| Index Code   | Columns   |
+==============+===========+
| PK\_ SEVENTS | SKDDATE   |
|              |           |
|              | SKDID     |
|              |           |
|              | JOBNAME   |
|              |           |
|              | FREQNAME  |
|              |           |
|              | JOBSTATUS |
|              |           |
|              | EVDETS    |
+--------------+-----------+

: SEVENTS Index Descriptions

### SKDEVENT

The interim table SKDEVENT contains event-processing information for the
SAM.

  Column Name   Explanation                                               Data Type       Additional Information
  ------------- --------------------------------------------------------- --------------- ------------------------
  RECNO         This column contains the internal event record numbers.   int (4)         None
  ACTION        This column contains the actions to be taken.             smallint (2)    None
  FIELD1        This column contains the event to be processed.           varchar (780)   None

  : SKDEVENT Column Descriptions

  Index Code      Columns
  --------------- ---------
  PK\_ SKDEVENT   RECNO

  : SKDEVENT Index Descriptions

### SKDSTATMAP

The SKDSTATMAP table maps (i.e., cross-references) Schedule Status Codes
to their respective descriptions.

  Column Name    Explanation                                                                                        Data Type      Additional Information
  -------------- -------------------------------------------------------------------------------------------------- -------------- ------------------------
  SKDSTATUS      This column contains statuses of Schedules.                                                        smallint (2)   None
  SKDSTATE       This column contains the schedule state descriptions.                                              varchar (40)   None
  SKDFILTERCAT   This column is the filtering category used to filter schedules displayed in Schedule Operations.   varchar (40)   None

  : SKDSTATMAP Table Maps

  Index Code        Columns
  ----------------- -----------
  PK\_ SKDSTATMAP   SKDSTATUS

  : SKDSTATMAP Index Descriptions

### SMALOOKUP

The SMALOOKUP table contains auxiliary table field codes.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SMATBLNAME  | This column     | varchar (128)  | None            |
|             | contains the    |                |                 |
|             | table names to  |                |                 |
|             | which the       |                |                 |
|             | information is  |                |                 |
|             | associated.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| SMAFC       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the lookup  |                |                 |
|             |     field       |                |                 |
|             |     codes.      |                |                 |
|             | -   The field   |                |                 |
|             |     code        |                |                 |
|             |     matches the |                |                 |
|             |     field code  |                |                 |
|             |     in the      |                |                 |
|             |     associated  |                |                 |
|             |     SMATBLNAME  |                |                 |
|             |     or the      |                |                 |
|             |     auxiliary   |                |                 |
|             |     table for   |                |                 |
|             |     the         |                |                 |
|             |     SMATBLNAME. |                |                 |
+-------------+-----------------+----------------+-----------------+
| SMAFSC      | This column     | int (4)        | -   0: JDL Tag  |
|             | contains the    |                | -   1: Data     |
|             | lookup field    |                |     Type        |
|             | sub codes.      |                | -   2: Display  |
|             |                 |                |     Format      |
|             |                 |                | -   3: Low      |
|             |                 |                |     Range / Min |
|             |                 |                |     Characters  |
|             |                 |                |     (depending  |
|             |                 |                |     on data     |
|             |                 |                |     type)       |
|             |                 |                | -   4: High     |
|             |                 |                |     Range / Max |
|             |                 |                |     Characters  |
|             |                 |                | -   5: Valid    |
|             |                 |                |     Characters  |
|             |                 |                | -   6: Invalid  |
|             |                 |                |     Characters  |
|             |                 |                | -   7: Default  |
|             |                 |                |     / Global    |
|             |                 |                |     value       |
|             |                 |                | -   8: Help     |
|             |                 |                |     Context ID  |
|             |                 |                | -   9: Allow    |
|             |                 |                |     Multiple    |
|             |                 |                |                 |
|             |                 |                | Occurrences (T) |
|             |                 |                | -   10:         |
|             |                 |                |     Component   |
|             |                 |                |     (that       |
|             |                 |                |     generated   |
|             |                 |                |     an error)   |
|             |                 |                | -   11: Used to |
|             |                 |                |     Define      |
|             |                 |                |     Associated  |
|             |                 |                |     Fields      |
|             |                 |                | -   12: Display |
|             |                 |                |     Order       |
|             |                 |                | -   1004: Error |
|             |                 |                |     Message     |
|             |                 |                |     Text        |
+-------------+-----------------+----------------+-----------------+
| SMAVALUE    | This column     | varchar (4000) | None            |
|             | contains the    |                |                 |
|             | field content.  |                |                 |
+-------------+-----------------+----------------+-----------------+

: SMALOOKUP Column Descriptions

+--------------+------------+
| Index Code   | Columns    |
+==============+============+
| PK_SMALOOKUP | SMATBLNAME |
|              |            |
|              | SMAFC      |
|              |            |
|              | SMAFSC     |
+--------------+------------+

: SMALOOKUP Index Descriptions

### SMASTER

The primary table SMASTER contains the details for a job that has been
built or added into the Daily schedule.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDDATE     | This column      | int (4)       | -   This column  |
|             | contains the     |               |     stores the   |
|             | date stamps of   |               |     time in SQL  |
|             | the schedules.   |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
+-------------+------------------+---------------+------------------+
| PRIORITY    | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     run-time     |               |                  |
|             |     priorities   |               |                  |
|             |     of the jobs  |               |                  |
|             |     in the Daily |               |                  |
|             |     schedules.   |               |                  |
|             | -   The SAM      |               |                  |
|             |     evaluates    |               |                  |
|             |     the          |               |                  |
|             |     priorities   |               |                  |
|             |     in this      |               |                  |
|             |     column to    |               |                  |
|             |     determine    |               |                  |
|             |     job          |               |                  |
|             |     submission   |               |                  |
|             |     order when   |               |                  |
|             |     multiple     |               |                  |
|             |     jobs qualify |               |                  |
|             |     to run at    |               |                  |
|             |     the same     |               |                  |
|             |     time.        |               |                  |
+-------------+------------------+---------------+------------------+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| INSTNO      | Contains a       | int (4)       | None             |
|             | number that      |               |                  |
|             | identifies the   |               |                  |
|             | instance of the  |               |                  |
|             | schedules.       |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| INTJOBNO    | This column      | int (4)       | None             |
|             | contains the     |               |                  |
|             | internal job     |               |                  |
|             | numbers          |               |                  |
|             | maintained by    |               |                  |
|             | the SAM.         |               |                  |
+-------------+------------------+---------------+------------------+
| DEPTID      | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     department   |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     DEPTS table. |               |                  |
+-------------+------------------+---------------+------------------+
| JOBTYPE     | -   This column  | smallint (2)  | The job type     |
|             |     contains the |               | determines the   |
|             |     operating    |               | machines and     |
|             |     system type  |               | machine groups   |
|             |     for each     |               | that are         |
|             |     job.         |               | available for    |
|             | -   The job type |               | the job.         |
|             |     determines   |               |                  |
|             |     the machines |               |                  |
|             |     and machine  |               |                  |
|             |     groups that  |               |                  |
|             |     are          |               |                  |
|             |     available    |               |                  |
|             |     for each     |               |                  |
|             |     job.         |               |                  |
+-------------+------------------+---------------+------------------+
| ACCESSCDID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     Access Code  |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     ACCESSID     |               |                  |
|             |     table.       |               |                  |
|             | -   This         |               |                  |
|             |     column's    |               |                  |
|             |     data limits  |               |                  |
|             |     access to    |               |                  |
|             |     the job in   |               |                  |
|             |     OpCon.       |               |                  |
+-------------+------------------+---------------+------------------+
| JOBGROUPID  | This column is   | smallint (2)  | None             |
|             | reserved for     |               |                  |
|             | future use.      |               |                  |
+-------------+------------------+---------------+------------------+
| PRIMMACHID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     primary      |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   The primary  |               |                  |
|             |     machine is   |               |                  |
|             |     each job's  |               |                  |
|             |     default      |               |                  |
|             |     machine.     |               |                  |
|             | -   The field is |               |                  |
|             |                  |               |                  |
|             | [mandatory]{.ul} |               |                  | |             |     if no        |               |                  |
|             |     machine      |               |                  |
|             |     group ID is  |               |                  |
|             |     specified;   |               |                  |
|             |     however, it  |               |                  |
|             |     is mutually  |               |                  |
|             |     exclusive    |               |                  |
|             |     with the     |               |                  |
|             |     machine      |               |                  |
|             |     group ID.    |               |                  |
|             | -   The primary  |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| ALTMACH1ID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     first        |               |                  |
|             |     alternate    |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   If the       |               |                  |
|             |     primary      |               |                  |
|             |     machine is   |               |                  |
|             |     unavailable  |               |                  |
|             |     at run time, |               |                  |
|             |     the jobs run |               |                  |
|             |     on an        |               |                  |
|             |     alternate    |               |                  |
|             |     machine.     |               |                  |
|             | -   Alternate    |               |                  |
|             |     machines are |               |                  |
|             |                  |               |                  |
|             |  [optional]{.ul} |               |                  | |             |     and should   |               |                  |
|             |     be defined   |               |                  |
|             |     in order.    |               |                  |
|             | -   The          |               |                  |
|             |     alternate    |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| ALTMACH2ID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     second       |               |                  |
|             |     alternate    |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   If the       |               |                  |
|             |     primary and  |               |                  |
|             |     first        |               |                  |
|             |     alternate    |               |                  |
|             |     machines are |               |                  |
|             |     unavailable  |               |                  |
|             |     at run time, |               |                  |
|             |     the jobs run |               |                  |
|             |     on the       |               |                  |
|             |     second       |               |                  |
|             |     alternate    |               |                  |
|             |     machine.     |               |                  |
|             | -   Alternate    |               |                  |
|             |     machines are |               |                  |
|             |                  |               |                  |
|             |  [optional]{.ul} |               |                  | |             |     and should   |               |                  |
|             |     be defined   |               |                  |
|             |     in order.    |               |                  |
|             | -   The          |               |                  |
|             |     alternate    |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| ALTMACH3ID  | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     third        |               |                  |
|             |     alternate    |               |                  |
|             |     machine IDs. |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHS table. |               |                  |
|             | -   If the       |               |                  |
|             |     primary,     |               |                  |
|             |     first        |               |                  |
|             |     alternate    |               |                  |
|             |     and second   |               |                  |
|             |     alternate    |               |                  |
|             |     machines are |               |                  |
|             |     unavailable  |               |                  |
|             |     at run time, |               |                  |
|             |     the jobs run |               |                  |
|             |     on an        |               |                  |
|             |     alternate    |               |                  |
|             |     machine.     |               |                  |
|             | -   Alternate    |               |                  |
|             |     machines are |               |                  |
|             |                  |               |                  |
|             |  [optional]{.ul} |               |                  | |             |     and should   |               |                  |
|             |     be defined   |               |                  |
|             |     in order.    |               |                  |
|             | -   The          |               |                  |
|             |     alternate    |               |                  |
|             |     machine type |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| MACHGRPID   | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     machine      |               |                  |
|             |     group IDs.   |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     MACHGRPS     |               |                  |
|             |     table.       |               |                  |
|             | -   The machine  |               |                  |
|             |     group ID     |               |                  |
|             |     identifies a |               |                  |
|             |     group of     |               |                  |
|             |     machines     |               |                  |
|             |     compatible   |               |                  |
|             |     with the     |               |                  |
|             |     job.         |               |                  |
|             | -   The machine  |               |                  |
|             |     group ID is  |               |                  |
|             |     mutually     |               |                  |
|             |     exclusive    |               |                  |
|             |     with the     |               |                  |
|             |     primary      |               |                  |
|             |     machine ID.  |               |                  |
|             | -   The machine  |               |                  |
|             |     group type   |               |                  |
|             |     [must]{.ul}  |               |                  | |             |     match the    |               |                  |
|             |     job type.    |               |                  |
+-------------+------------------+---------------+------------------+
| STARTMACH   | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     machine IDs  |               |                  |
|             |     on which the |               |                  |
|             |     jobs were    |               |                  |
|             |     started.     |               |                  |
|             | -   This         |               |                  |
|             |     information  |               |                  |
|             |     is useful    |               |                  |
|             |     when there   |               |                  |
|             |     are          |               |                  |
|             |     alternate    |               |                  |
|             |     machines or  |               |                  |
|             |     a machine    |               |                  |
|             |     group        |               |                  |
|             |     assigned to  |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| STOFFSET    | This column      | real (4)      | -   This column  |
|             | contains the     |               |     stores the   |
|             | start time       |               |     date in SQL  |
|             | offsets.         |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     part of this |
|             |                  |               |     number is    |
|             |                  |               |     irrelevant.  |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| STABSREL    | This column      | char (1)      | -   A: Absolute  |
|             | contains the     |               | -   R: Relative  |
|             | start time flags |               |                  |
|             | describing       |               |                  |
|             | whether the      |               |                  |
|             | start times are  |               |                  |
|             | absolute or      |               |                  |
|             | relative.        |               |                  |
+-------------+------------------+---------------+------------------+
| LTSTTIME    | This column      | real (4)      | -   This column  |
|             | contains the     |               |     stores the   |
|             | latest start     |               |     date in SQL  |
|             | time offsets.    |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     part of this |
|             |                  |               |     number is    |
|             |                  |               |     irrelevant.  |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| LTABSREL    | -   This column  | char (1)      | -   A: Absolute  |
|             |     contains the |               | -   R: Relative  |
|             |     latest start |               |                  |
|             |     time flags.  |               |                  |
|             | -   This column  |               |                  |
|             |     states       |               |                  |
|             |     whether the  |               |                  |
|             |     latest start |               |                  |
|             |     time is      |               |                  |
|             |     absolute or  |               |                  |
|             |     relative.    |               |                  |
+-------------+------------------+---------------+------------------+
| STSTATUS    | This column      | smallint (2)  | -   Values less  |
|             | contains start   |               |     than 900     |
|             | statuses of the  |               |     indicate     |
|             | jobs.            |               |     that the     |
|             |                  |               |     jobs have    |
|             |                  |               |     not been     |
|             |                  |               |     submitted    |
|             |                  |               |     for          |
|             |                  |               |     starting.    |
|             |                  |               | -   When jobs    |
|             |                  |               |     are          |
|             |                  |               |     submitted    |
|             |                  |               |     for          |
|             |                  |               |     starting,    |
|             |                  |               |     the value of |
|             |                  |               |     this field   |
|             |                  |               |     is set to    |
|             |                  |               |     900 and the  |
|             |                  |               |     JOBSTATUS    |
|             |                  |               |     column       |
|             |                  |               |     indicates    |
|             |                  |               |     the job      |
|             |                  |               |     progress.    |
+-------------+------------------+---------------+------------------+
| JOBSTATUS   | This column      | smallint (2)  | The value is     |
|             | contains the     |               | zero (0) when    |
|             | progress         |               | the start status |
|             | statuses of the  |               | column STSTATUS  |
|             | jobs.            |               | is less than     |
|             |                  |               | 900.             |
|             | This column      |               |                  |
|             | reflects the     |               |                  |
|             | progress of the  |               |                  |
|             | jobs after       |               |                  |
|             | submission and   |               |                  |
|             | reflects the     |               |                  |
|             | final            |               |                  |
|             | termination      |               |                  |
|             | states of the    |               |                  |
|             | jobs.            |               |                  |
+-------------+------------------+---------------+------------------+
| STARTSTAMP  | This column      | float (8)     | -   This column  |
|             | contains the     |               |     stores the   |
|             | start dates and  |               |     date in SQL  |
|             | start times of   |               |     format.      |
|             | the jobs.        |               | -   The integer  |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| TERMSTAMP   | This column      | float (8)     | -   This column  |
|             | contains the end |               |     stores the   |
|             | dates and end    |               |     date in SQL  |
|             | times of the     |               |     format.      |
|             | jobs.            |               | -   The integer  |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| LASTUPDATE  | -   This column  | float (8)     | -   This column  |
|             |     contains the |               |     Stores the   |
|             |     dates and    |               |     date in SQL  |
|             |     times of the |               |     format.      |
|             |     last         |               | -   The integer  |
|             |     messages     |               |     part of the  |
|             |     from the     |               |     SQL date     |
|             |     LSAMs        |               |     represents   |
|             |     regarding    |               |     the day      |
|             |     the jobs.    |               |     count since  |
|             | -   This         |               |     Saturday,    |
|             |     information  |               |     December     |
|             |     is useful in |               |     30, 1899.    |
|             |     keeping      |               | -   The          |
|             |     track of     |               |     fractional   |
|             |     jobs that    |               |     part of the  |
|             |     are          |               |     SQL date     |
|             |     considered   |               |     represents   |
|             |     to be lost.  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| TERMDESC    | This column      | varchar (255) | This column      |
|             | contains         |               | contains the     |
|             | termination      |               | 20-character job |
|             | descriptions of  |               | termination      |
|             | the job.         |               | information      |
|             |                  |               | received from    |
|             |                  |               | the LSAMs.       |
+-------------+------------------+---------------+------------------+
| MAXMINS     | This column      | smallint (2)  | None             |
|             | contains the     |               |                  |
|             | amount of time   |               |                  |
|             | in minutes       |               |                  |
|             | before each job  |               |                  |
|             | is marked as     |               |                  |
|             | having exceeded  |               |                  |
|             | the maximum      |               |                  |
|             | allowed          |               |                  |
|             | run-time.        |               |                  |
+-------------+------------------+---------------+------------------+
| ESTRUNTIME  | -   This column  | int (4)       | The estimated    |
|             |     contains the |               | run time is in   |
|             |     estimated    |               | minutes.         |
|             |     run times    |               |                  |
|             |     for the      |               |                  |
|             |     jobs.        |               |                  |
|             | -   The OpCon    |               |                  |
|             |                  |               |                  |
|             |    administrator |               |                  |
|             |     calculates   |               |                  |
|             |     this value   |               |                  |
|             |     with the     |               |                  |
|             |     JOB_AVG      |               |                  |
|             |     script       |               |                  |
|             |     provided by  |               |                  |
|             |     [SMA         |               |                  | |             |     Tec          |               |                  |
|             | hnologies]{.Gene |               |                  |
|             | ralCompanyName}. |               |                  |
+-------------+------------------+---------------+------------------+
| SHORTNAME   | Contains a       | char (12)     | None             |
|             | generated name   |               |                  |
|             | for the job that |               |                  |
|             | is used in       |               |                  |
|             | communication    |               |                  |
|             | with the agents. |               |                  |
+-------------+------------------+---------------+------------------+

: SMASTER Column Descriptions

+---------------+----------+
| Index Code    | Columns  |
+===============+==========+
| PK_SMASTER    | SKDDATE  |
|               |          |
|               | PRIORITY |
|               |          |
|               | SKDID    |
|               |          |
|               | JOBNAME  |
+---------------+----------+
| I2SMASTR      | SKDDATE  |
|               |          |
|               | SKDID    |
|               |          |
|               | JOBNAME  |
+---------------+----------+
| I3SMASTR      | SKDDATE  |
|               |          |
|               | INTJOBNO |
+---------------+----------+
| X_SMASTERSTAT | STSTATUS |
+---------------+----------+

: SMASTER Index Descriptions

### SMASTER_AUX

The secondary table SMASTER_AUX contains auxiliary information for a job
that has been built or added into the Daily schedule. The combination of
Schedule Date, Schedule ID, and Job Name links the auxiliary information
to the primary information.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDDATE     | This column     | int (4)        | -   This column |
|             | contains the    |                |     stores the  |
|             | date stamps of  |                |     date in SQL |
|             | the schedules.  |                |     format.     |
|             |                 |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| INSTNO      | Contains a      | int (4)        | None            |
|             | number that     |                |                 |
|             | identifies the  |                |                 |
|             | instance of the |                |                 |
|             | schedules.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| JOBNAME     | -   This column | varchar (128)  | None            |
|             |     contains    |                |                 |
|             |     the job     |                |                 |
|             |     names.      |                |                 |
|             | -   The job     |                |                 |
|             |     names must  |                |                 |
|             |     be unique   |                |                 |
|             |     within each |                |                 |
|             |     schedule.   |                |                 |
|             | -   The         |                |                 |
|             |     schedule ID |                |                 |
|             |     (SKDID)     |                |                 |
|             |     identifies  |                |                 |
|             |     the         |                |                 |
|             |     schedule.   |                |                 |
+-------------+-----------------+----------------+-----------------+
| SAFC        | This column     | int (4)        | -   0: Reason   |
|             | contains the    |                |     for last    |
|             | auxiliary       |                |     manually    |
|             | information     |                |     changed job |
|             | field codes.    |                |     status      |
|             |                 |                | -   51: The     |
|             |                 |                |                 |
|             |                 |                |    concatenated |
|             |                 |                |     Estimated   |
|             |                 |                |     Run Time,   |
|             |                 |                |     Target      |
|             |                 |                |     Start Time, |
|             |                 |                |     Estimated   |
|             |                 |                |     Start Time, |
|             |                 |                |     and Job     |
|             |                 |                |                 |
|             |                 |                |   dependencies. |
|             |                 |                |                 |
|             |                 |                |   -   Estimated |
|             |                 |                |         Start   |
|             |                 |                |         Time -- |
|             |                 |                |                 |
|             |                 |                |      calculated |
|             |                 |                |                 |
|             |                 |                |   -   Estimated |
|             |                 |                |         Run     |
|             |                 |                |         Time -- |
|             |                 |                |         this is |
|             |                 |                |                 |
|             |                 |                |       retrieved |
|             |                 |                |         the     |
|             |                 |                |         first   |
|             |                 |                |         time    |
|             |                 |                |         the     |
|             |                 |                |                 |
|             |                 |                |       estimated |
|             |                 |                |         start   |
|             |                 |                |         time is |
|             |                 |                |                 |
|             |                 |                |     calculated. |
|             |                 |                |         From    |
|             |                 |                |                 |
|             |                 |                |        JSKD_AUX |
|             |                 |                |         FC=101  |
|             |                 |                |         if it   |
|             |                 |                |         exists, |
|             |                 |                |         else    |
|             |                 |                |         from    |
|             |                 |                |                 |
|             |                 |                |        JMASTER. |
|             |                 |                |     -   Target  |
|             |                 |                |         Start   |
|             |                 |                |         Time -  |
|             |                 |                |         From    |
|             |                 |                |                 |
|             |                 |                |        JSKD_AUX |
|             |                 |                |         FC=102  |
|             |                 |                |         if it   |
|             |                 |                |         exists, |
|             |                 |                |         else 0  |
|             |                 |                |     -   Job     |
|             |                 |                |                 |
|             |                 |                |      Dependency |
|             |                 |                |         Flags   |
|             |                 |                |         --      |
|             |                 |                |         Missing |
|             |                 |                |                 |
|             |                 |                |     dependency, |
|             |                 |                |                 |
|             |                 |                |        circular |
|             |                 |                |                 |
|             |                 |                |     dependency, |
|             |                 |                |         etc.    |
|             |                 |                | -   999: Job    |
|             |                 |                |     Details     |
|             |                 |                | -   os000: Job  |
|             |                 |                |     Name (used  |
|             |                 |                |     to define   |
|             |                 |                |                 |
|             |                 |                |    restrictions |
|             |                 |                |     of job      |
|             |                 |                |     names per   |
|             |                 |                |     LSAM)       |
|             |                 |                | -   os001 -     |
|             |                 |                |     os999: Each |
|             |                 |                |     field       |
|             |                 |                |     required by |
|             |                 |                |     the LSAM to |
|             |                 |                |     define a    |
|             |                 |                |     job         |
|             |                 |                | -   The os is   |
|             |                 |                |     the value   |
|             |                 |                |     of the      |
|             |                 |                |     current     |
|             |                 |                |     JobType.    |
+-------------+-----------------+----------------+-----------------+
| SASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| SAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: SMASTER_AUX Column Descriptions

+---------------+---------+
| Index Code    | Columns |
+===============+=========+
| PK_SMASTERAUX | SKDDATE |
|               |         |
|               | SKDID   |
|               |         |
|               | JOBNAME |
|               |         |
|               | SAFC    |
|               |         |
|               | SASEQNO |
+---------------+---------+

: SMASTER_AUX Index Descriptions

### SMASTER_INSERTIONS

The primary table SMASTER_INSERTIONS contains identifying details for a
job that has been built or added into the Daily schedule.

+-------------+-------------------+------------+-------------------+
| Column Name | Explanation       | Data Type  | Additional        |
|             |                   |            | Information       |
+=============+===================+============+===================+
| SKDDATE     | -   This column   | int (4)    | The integer       |
|             |     contains the  |            | represents the    |
|             |     date stamps   |            | day count since   |
|             |     of the        |            | Saturday,         |
|             |     schedules.    |            | December 30,      |
|             | -   This column   |            | 1899.             |
|             |     stores the    |            |                   |
|             |     time in SQL   |            |                   |
|             |     format.       |            |                   |
+-------------+-------------------+------------+-------------------+
| SKDID       | -   This column   | int (4)    | None              |
|             |     contains the  |            |                   |
|             |     schedule IDs. |            |                   |
|             | -   This column   |            |                   |
|             |     contains      |            |                   |
|             |                   |            |                   |
|             |   cross-reference |            |                   |
|             |     information   |            |                   |
|             |     for lookup    |            |                   |
|             |     into the      |            |                   |
|             |     SNAME table.  |            |                   |
+-------------+-------------------+------------+-------------------+
| INSTNO      | This column       | int (4)    | None              |
|             | contains the      |            |                   |
|             | instance number   |            |                   |
|             | of the schedule.  |            |                   |
+-------------+-------------------+------------+-------------------+
| JOBNAME     | This column       | char (128) | None              |
|             | contains the job  |            |                   |
|             | names.            |            |                   |
|             |                   |            |                   |
|             | The job names     |            |                   |
|             | must be unique    |            |                   |
|             | within each       |            |                   |
|             | schedule.         |            |                   |
+-------------+-------------------+------------+-------------------+
| INSERTTIME  | This column       | float (8)  | None              |
|             | contains the time |            |                   |
|             | the record was    |            |                   |
|             | added to the      |            |                   |
|             | SMASTER table.    |            |                   |
+-------------+-------------------+------------+-------------------+

: SMASTER_INSERTIONS Column Descriptions

+-----------------------+------------+
| Index Code            | Columns    |
+=======================+============+
| PK_SMASTER_INSERTIONS | SKDID      |
|                       |            |
|                       | SKDDATE    |
|                       |            |
|                       | INSTNO     |
|                       |            |
|                       | JOBNAME    |
|                       |            |
|                       | INSERTTIME |
+-----------------------+------------+

: SMASTER_INSERTIONS Index Descriptions

### SNAME

The SNAME table contains schedule information.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     uniquely     |               |                  |
|             |     identifies   |               |                  |
|             |     each         |               |                  |
|             |     schedule.    |               |                  |
|             | -   This table   |               |                  |
|             |     is used for  |               |                  |
|             |     lookup from  |               |                  |
|             |     most tables  |               |                  |
|             |     in the       |               |                  |
|             |     database.    |               |                  |
+-------------+------------------+---------------+------------------+
| SKDNAME     | This column      | varchar (255) | None             |
|             | contains the     |               |                  |
|             | descriptive      |               |                  |
|             | schedule names.  |               |                  |
+-------------+------------------+---------------+------------------+
| SKDSAM      | This column is   | smallint (2)  | None             |
|             | reserved for     |               |                  |
|             | future use.      |               |                  |
+-------------+------------------+---------------+------------------+
| SKDSTART    | This column      | real (4)      | -   This column  |
|             | contains the     |               |     stores the   |
|             | intended start   |               |     date in SQL  |
|             | times of the     |               |     format.      |
|             | schedules.       |               | -   The integer  |
|             |                  |               |     part of this |
|             |                  |               |     SQL date is  |
|             |                  |               |     irrelevant.  |
|             |                  |               | -   The          |
|             |                  |               |     fractional   |
|             |                  |               |     part of the  |
|             |                  |               |     SQL date     |
|             |                  |               |     represents   |
|             |                  |               |     the time in  |
|             |                  |               |     seconds      |
|             |                  |               |     since        |
|             |                  |               |     midnight.    |
+-------------+------------------+---------------+------------------+
| SKDWKDAYS   | -   This column  | smallint (2)  | Valid values are |
|             |     contains the |               | 1, 2, 3, 4, 5,   |
|             |     workdays per |               | 6, and 7.        |
|             |     week for     |               |                  |
|             |     each         |               |                  |
|             |     schedule.    |               |                  |
|             | -   This         |               |                  |
|             |     information  |               |                  |
|             |     determines   |               |                  |
|             |     what         |               |                  |
|             |     constitutes  |               |                  |
|             |     a working    |               |                  |
|             |     day and how  |               |                  |
|             |     the holidays |               |                  |
|             |     are being    |               |                  |
|             |     assigned.    |               |                  |
+-------------+------------------+---------------+------------------+

: SNAME Column Descriptions

  Index Code   Columns
  ------------ ---------
  PK\_ SNAME   SKDID

  : SNAME Index Descriptions

### SNAME_AUX

The secondary table SNAME_AUX contains auxiliary information for
schedules. The Schedule ID links the auxiliary information to the
primary information.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| SAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| SASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| SAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: SNAME_AUX Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_SNAMEAUX | SKDID   |
|             |         |
|             | SAFC    |
|             |         |
|             | SASEQNO |
+-------------+---------+

: SNAME_AUX Index Descriptions

### SSTATUS

The SSTATUS table contains information on the Daily schedule status.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| SKDDATE     | This column     | int (4)        | -   This column |
|             | contains the    |                |     stores the  |
|             | intended start  |                |     date in SQL |
|             | dates for the   |                |     format.     |
|             | schedules.      |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| INSTNO      | Contains a      | int (4)        | None            |
|             | number that     |                |                 |
|             | identifies the  |                |                 |
|             | instance of the |                |                 |
|             | schedules.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| SKDSAM      | This column is  | smallint (2)   | None            |
|             | reserved for    |                |                 |
|             | future use.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| SKDSTTIME   | This column     | real (4)       | -   This column |
|             | contains the    |                |     stores the  |
|             | intended start  |                |     date in SQL |
|             | times for the   |                |     format.     |
|             | schedules.      |                | -   The integer |
|             |                 |                |     part of     |
|             |                 |                |     this SQL    |
|             |                 |                |     date is     |
|             |                 |                |     irrelevant. |
|             |                 |                | -   The         |
|             |                 |                |     fractional  |
|             |                 |                |     part of the |
|             |                 |                |     SQL date    |
|             |                 |                |     represents  |
|             |                 |                |     the time in |
|             |                 |                |     seconds     |
|             |                 |                |     since       |
|             |                 |                |     midnight.   |
+-------------+-----------------+----------------+-----------------+
| SKDACTDATE  | This column     | int (4)        | -   This column |
|             | contains the    |                |     stores the  |
|             | actual start    |                |     date in SQL |
|             | dates of the    |                |     format.     |
|             | schedules.      |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| SKDACTTIM   | This column     | real (4)       | -   This column |
|             | contains the    |                |     stores the  |
|             | actual start    |                |     date in SQL |
|             | times of the    |                |     format.     |
|             | schedules.      |                | -   The integer |
|             |                 |                |     part of     |
|             |                 |                |     this SQL    |
|             |                 |                |     date is     |
|             |                 |                |     irrelevant. |
|             |                 |                | -   The         |
|             |                 |                |     fractional  |
|             |                 |                |     part of the |
|             |                 |                |     SQL date    |
|             |                 |                |     represents  |
|             |                 |                |     the time in |
|             |                 |                |     seconds     |
|             |                 |                |     since       |
|             |                 |                |     midnight.   |
+-------------+-----------------+----------------+-----------------+
| SKDSTATUS   | This column     | smallint (2)   | -   0: Wait to  |
|             | contains the    |                |     Start       |
|             | statuses of the |                | -   10: On Hold |
|             | schedules.      |                | -   50: In      |
|             |                 |                |     Process     |
|             |                 |                | -   100:        |
|             |                 |                |     Completed   |
+-------------+-----------------+----------------+-----------------+
| SKDENDDATE  | This column     | int (4)        | -   This column |
|             | contains the    |                |     stores the  |
|             | actual end      |                |     date in SQL |
|             | dates of the    |                |     format.     |
|             | schedules.      |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| SKDENDTIME  | This column     | real (4)       | -   This column |
|             | contains the    |                |     stores the  |
|             | actual end      |                |     date in SQL |
|             | times of the    |                |     format.     |
|             | schedules.      |                | -   The integer |
|             |                 |                |     part of     |
|             |                 |                |     this SQL    |
|             |                 |                |     date is     |
|             |                 |                |     irrelevant. |
|             |                 |                | -   The         |
|             |                 |                |     fractional  |
|             |                 |                |     part of the |
|             |                 |                |     SQL date    |
|             |                 |                |     represents  |
|             |                 |                |     the time in |
|             |                 |                |     seconds     |
|             |                 |                |     since       |
|             |                 |                |     midnight.   |
+-------------+-----------------+----------------+-----------------+
| SKDPATH     | This column     | varchar (8000) | None            |
|             | contains the    |                |                 |
|             | path from the   |                |                 |
|             | root schedule,  |                |                 |
|             | through a       |                |                 |
|             | multi-level     |                |                 |
|             | hierarchy of    |                |                 |
|             | container jobs, |                |                 |
|             | to the current  |                |                 |
|             | schedule.       |                |                 |
+-------------+-----------------+----------------+-----------------+

: SSTATUS Column Descriptions

+------------+---------+
| Index Code | Columns |
+============+=========+
| PK_SSTATUS | SKDID   |
|            |         |
|            | SKDDATE |
+------------+---------+
| I2SSTATS   | SKDDATE |
+------------+---------+

: SSTATUS Index Descriptions

### SSTATUS_AUX

The secondary table SSTATUS_AUX contains auxiliary information for the
daily schedule status. The combination of Schedule ID and Schedule Date
links the auxiliary information to the primary information.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| SKDID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     schedule    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     SNAME       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| SKDDATE     | This column     | int (4)        | -   This column |
|             | contains the    |                |     stores the  |
|             | intended start  |                |     date in SQL |
|             | dates for the   |                |     format.     |
|             | schedules.      |                | -   The integer |
|             |                 |                |     represents  |
|             |                 |                |     the day     |
|             |                 |                |     count since |
|             |                 |                |     Saturday,   |
|             |                 |                |     December    |
|             |                 |                |     30, 1899.   |
+-------------+-----------------+----------------+-----------------+
| INSTNO      | Contains a      | int (4)        | None            |
|             | number that     |                |                 |
|             | identifies the  |                |                 |
|             | instance of the |                |                 |
|             | schedules.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| SAFC        | This column     | smallint (2)   | -   0:          |
|             | contains the    |                |     Indicates   |
|             | auxiliary       |                |     the content |
|             | information     |                |     is          |
|             | field codes.    |                |                 |
|             |                 |                |   documentation |
|             |                 |                | -   1 -- 50:    |
|             |                 |                |     Reserved    |
|             |                 |                |     for current |
|             |                 |                |     column      |
|             |                 |                |     lookup use  |
|             |                 |                | -   51: Last    |
|             |                 |                |     Manual      |
|             |                 |                |     Status      |
|             |                 |                |     Change      |
|             |                 |                |     Reason      |
|             |                 |                | -   52:         |
|             |                 |                |     Schedule's |
|             |                 |                |     Estimated   |
|             |                 |                |     Start and   |
|             |                 |                |     End Times   |
|             |                 |                | -   53: Job     |
|             |                 |                |     counts      |
|             |                 |                |     within      |
|             |                 |                |     status      |
|             |                 |                | -   54: Last    |
|             |                 |                |     calculated  |
|             |                 |                |     date/time   |
+-------------+-----------------+----------------+-----------------+
| SASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| SAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: STATUS_AUX Column Descriptions

+---------------+---------+
| Index Code    | Columns |
+===============+=========+
| PK_SSTATUSAUX | SKDID   |
|               |         |
|               | SKDDATE |
|               |         |
|               | SAFC    |
|               |         |
|               | SASEQNO |
+---------------+---------+

: SSTATUS_AUX Index Descriptions

### SSYS

The SSYS table contains system summary information. The table contains a
single record, which is maintained by the Administration and Security
sections of the Enterprise Manager and SAM. All keys are by default base
one and increment of one.

  --------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ![White "X" icon on red circular background](../../Resources/Images/warning-icon(48x48).png "Warning icon")   **WARNING:** [Invalid changes in this table result in database referential integrity problems, and subsequent failure of the user to insert, delete or modify information in the database.]
  --------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| DEPTKEY     | This column      | smallint (2) | None             |
|             | contains the     |              |                  |
|             | next DEPTID for  |              |                  |
|             | the DEPTS table. |              |                  |
+-------------+------------------+--------------+------------------+
| SCHEDKEY    | This column      | int (4)      | None             |
|             | contains the     |              |                  |
|             | next SKDID for   |              |                  |
|             | the SNAME table. |              |                  |
+-------------+------------------+--------------+------------------+
| SYSTEM      | This column      | int (4)      | None             |
|             | contains the     |              |                  |
|             | OpCon database   |              |                  |
|             | schema version.  |              |                  |
+-------------+------------------+--------------+------------------+
| INTJOBNO    | -   This column  | int (4)      | None             |
|             |     contains the |              |                  |
|             |     next         |              |                  |
|             |     available    |              |                  |
|             |     internal job |              |                  |
|             |     number.      |              |                  |
|             | -   This field   |              |                  |
|             |     is           |              |                  |
|             |     maintained   |              |                  |
|             |     strictly by  |              |                  |
|             |     the SAM.     |              |                  |
+-------------+------------------+--------------+------------------+
| CALKEY      | This column      | int (4)      | None             |
|             | contains the     |              |                  |
|             | next CALID for   |              |                  |
|             | the CALDESC      |              |                  |
|             | table.           |              |                  |
+-------------+------------------+--------------+------------------+
| EVENTKEY    | This column is   | smallint (2) | None             |
|             | reserved for     |              |                  |
|             | future use.      |              |                  |
+-------------+------------------+--------------+------------------+
| ACCESSKEY   | This column      | smallint (2) | None             |
|             | contains the     |              |                  |
|             | next ACCESSCDID  |              |                  |
|             | for the ACCESSCD |              |                  |
|             | table.           |              |                  |
+-------------+------------------+--------------+------------------+
| MACHKEY     | This column      | smallint (2) | None             |
|             | contains the     |              |                  |
|             | next MACHID for  |              |                  |
|             | the MACHS table. |              |                  |
+-------------+------------------+--------------+------------------+
| MACHGRPKEY  | This column      | smallint (2) | None             |
|             | contains the     |              |                  |
|             | next MACHGRPID   |              |                  |
|             | for the MACHGRPS |              |                  |
|             | table.           |              |                  |
+-------------+------------------+--------------+------------------+
| USERKEY     | This column      | smallint (2) | None             |
|             | contains the     |              |                  |
|             | next USERID for  |              |                  |
|             | the USERS table. |              |                  |
+-------------+------------------+--------------+------------------+
| THRESHKEY   | This column      | int (4)      | None             |
|             | contains the     |              |                  |
|             | next THRESHID    |              |                  |
|             | for the THRESH   |              |                  |
|             | table.           |              |                  |
+-------------+------------------+--------------+------------------+
| TOKENKEY    | This column      | int (4)      | None             |
|             | contains the     |              |                  |
|             | next TKNID for   |              |                  |
|             | the TOKEN table. |              |                  |
+-------------+------------------+--------------+------------------+
| AUDITKEY    | This column      | smallint (2) | -   0: Indicates |
|             | contains the     |              |     auditing is  |
|             | Flag reflecting  |              |     disabled.    |
|             | the auditing     |              | -   -1:          |
|             | status.          |              |     Indicates    |
|             |                  |              |     auditing is  |
|             |                  |              |     enabled.     |
+-------------+------------------+--------------+------------------+
| NUMTRANREC  | -   This column  | smallint (2) | The default is   |
|             |     contains the |              | 20.              |
|             |     transaction  |              |                  |
|             |     batch size.  |              |                  |
|             | -   This column  |              |                  |
|             |     contains the |              |                  |
|             |     number of    |              |                  |
|             |     records      |              |                  |
|             |     processed    |              |                  |
|             |     within a     |              |                  |
|             |     transaction  |              |                  |
|             |     during       |              |                  |
|             |     schedule     |              |                  |
|             |     building.    |              |                  |
+-------------+------------------+--------------+------------------+

: SSYS Column Descriptions

  Index Code   Columns
  ------------ ---------
  PK\_ SSYS    DEPTKEY

  : SSYS Index Descriptions

### STHR

The STHR table contains information on how jobs affect threshold values,
depending on their termination state in the Daily schedule.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| SKDDATE     | This column      | int (4)       | -   This column  |
|             | contains the     |               |     stores the   |
|             | date stamps of   |               |     date in SQL  |
|             | the schedules.   |               |     format.      |
|             |                  |               | -   The integer  |
|             |                  |               |     represents   |
|             |                  |               |     the day      |
|             |                  |               |     count since  |
|             |                  |               |     Saturday,    |
|             |                  |               |     December     |
|             |                  |               |     30, 1899.    |
+-------------+------------------+---------------+------------------+
| SKDID       | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     schedule     |               |                  |
|             |     IDs.         |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     SNAME table. |               |                  |
+-------------+------------------+---------------+------------------+
| INSTNO      | Contains a       | int (4)       | None             |
|             | number that      |               |                  |
|             | identifies the   |               |                  |
|             | instance of the  |               |                  |
|             | schedules.       |               |                  |
+-------------+------------------+---------------+------------------+
| JOBNAME     | -   This column  | varchar (128) | None             |
|             |     contains the |               |                  |
|             |     job names.   |               |                  |
|             | -   The job      |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     schedule.    |               |                  |
|             | -   The schedule |               |                  |
|             |     ID (SKDID)   |               |                  |
|             |     identifies   |               |                  |
|             |     the          |               |                  |
|             |     schedule.    |               |                  |
+-------------+------------------+---------------+------------------+
| FREQNAME    | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     frequency    |               |                  |
|             |     names.       |               |                  |
|             | -   The          |               |                  |
|             |     frequency    |               |                  |
|             |     names must   |               |                  |
|             |     be unique    |               |                  |
|             |     within each  |               |                  |
|             |     job.         |               |                  |
|             | -   The job name |               |                  |
|             |     (JOBNAME)    |               |                  |
|             |     identifies   |               |                  |
|             |     the job.     |               |                  |
+-------------+------------------+---------------+------------------+
| JOBSTATUS   | This column      | smallint (2)  | -   500: Running |
|             | contains the job |               |     (Time        |
|             | statuses that    |               |     Exceeded)    |
|             | cause the        |               | -   900:         |
|             | thre             |               |     Finished OK  |
|             | sholds/resources |               | -   910: Failed  |
|             | to be set.       |               | -   940: Skipped |
+-------------+------------------+---------------+------------------+
| THRESHID    | -   This column  | int (4)       | None             |
|             |     contains the |               |                  |
|             |     IDs of the   |               |                  |
|             |     thre         |               |                  |
|             | sholds/resources |               |                  |
|             |     to be set.   |               |                  |
|             | -   This column  |               |                  |
|             |     contains     |               |                  |
|             |                  |               |                  |
|             |  cross-reference |               |                  |
|             |     information  |               |                  |
|             |     for lookup   |               |                  |
|             |     into the     |               |                  |
|             |     THRESH       |               |                  |
|             |     table.       |               |                  |
+-------------+------------------+---------------+------------------+
| THRESHVAL   | This column      | int (4)       | Valid values     |
|             | contains the     |               | range from 0 to  |
|             | values to set    |               | 2,147,483,647.   |
|             | the              |               |                  |
|             | thre             |               |                  |
|             | sholds/resources |               |                  |
|             | to.              |               |                  |
+-------------+------------------+---------------+------------------+

: STHR Column Descriptions

+------------+-------------------+
| Index Code | Columns           |
+============+===================+
| PK\_ STHR  | SKDDATESKDID      |
|            |                   |
|            | JOBNAME           |
|            |                   |
|            | FREQNAMEJOBSTATUS |
|            |                   |
|            | THRESHID          |
+------------+-------------------+

: STHR Index Descriptions

### THRESH

The THRESH table contains Threshold and Resource names and values.

+---------------+-----------------+---------------+-----------------+
| Column Name   | Explanation     | Data Type     | Additional      |
|               |                 |               | Information     |
+===============+=================+===============+=================+
| THRESHID      | This column     | int (4)       | None            |
|               | contains the    |               |                 |
|               | thr             |               |                 |
|               | eshold/resource |               |                 |
|               | IDs.            |               |                 |
+---------------+-----------------+---------------+-----------------+
| THRESHDES     | This column     | char (20)     | None            |
|               | contains the    |               |                 |
|               | descriptive     |               |                 |
|               | names of the    |               |                 |
|               | thresh          |               |                 |
|               | olds/resources. |               |                 |
+---------------+-----------------+---------------+-----------------+
| THRESHVAL     | This column     | int (4)       | Valid values    |
|               | contains the    |               | range from 0 to |
|               | current values  |               | 2,147,483,647.  |
|               | of the          |               |                 |
|               | thresholds or   |               |                 |
|               | contains the    |               |                 |
|               | maximum number  |               |                 |
|               | for the         |               |                 |
|               | resources.      |               |                 |
+---------------+-----------------+---------------+-----------------+
| THRESHUSED    | -   For each    | int (4)       | None            |
|               |     resource,   |               |                 |
|               |     this column |               |                 |
|               |     contains    |               |                 |
|               |     the current |               |                 |
|               |     number of   |               |                 |
|               |     resources   |               |                 |
|               |     in use.     |               |                 |
|               | -   This column |               |                 |
|               |     is in use   |               |                 |
|               |     if the      |               |                 |
|               |     THRESHID    |               |                 |
|               |     represents  |               |                 |
|               |     a resource. |               |                 |
|               | -   This column |               |                 |
|               |     is          |               |                 |
|               |     [not]{.ul}  |               |                 | |               |     in use if   |               |                 |
|               |     the         |               |                 |
|               |     THRESHID    |               |                 |
|               |     represents  |               |                 |
|               |     a           |               |                 |
|               |     threshold.  |               |                 |
+---------------+-----------------+---------------+-----------------+
| THRESHSTYLE   | This column     | smallint (2)  | None            |
|               | determines      |               |                 |
|               | whether each    |               |                 |
|               | THRESHID        |               |                 |
|               | represents a    |               |                 |
|               | threshold or a  |               |                 |
|               | resource.       |               |                 |
+---------------+-----------------+---------------+-----------------+
| THRESHOLOCKED | This column     | varchar (256) | -   Valid       |
|               | indicates if    |               |     values are  |
|               | one or more     |               |     an empty    |
|               | jobs in         |               |     string, or  |
|               | Operations      |               |     a string a  |
|               | require "All" |               |     values      |
|               | of the defined  |               |     stored by   |
|               | resource to     |               |     the SAM for |
|               | meet a          |               |     maintaining |
|               | dependency for  |               |     the state   |
|               | running.        |               |     of the      |
|               |                 |               |     lock.       |
|               |                 |               | -   This column |
|               |                 |               |     is updated  |
|               |                 |               |     only by SAM |
|               |                 |               |     to maintain |
|               |                 |               |     the state   |
|               |                 |               |     of the      |
|               |                 |               |     resource.   |
+---------------+-----------------+---------------+-----------------+

: THRESH Column Descriptions

  Index Code   Columns
  ------------ ----------
  PK_THRESH    THRESHID

  : THRESH Index Descriptions

### THRESH_AUX

The secondary table THRESH_AUX contains auxiliary information about
Thresholds and Resources. The Threshold ID links the auxiliary
information to the primary information.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| THRESHID    | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     thr         |                |                 |
|             | eshold/resource |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     THRESH      |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| TAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| TASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| TAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: THRESH_AUX Column Descriptions

+--------------+----------+
| Index Code   | Columns  |
+==============+==========+
| PK_THRESHAUX | THRESHID |
|              |          |
|              | TAFC     |
|              |          |
|              | TASEQNO  |
+--------------+----------+

: THRESH_AUX Index Descriptions

### TOKEN

The TOKEN table contains Token names and values.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| TKNID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the token   |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     uniquely    |                |                 |
|             |     identifies  |                |                 |
|             |     each token. |                |                 |
+-------------+-----------------+----------------+-----------------+
| TKNDESC     | -   This column | varchar (64)   |                 |
|             |     contains    |                |                 |
|             |     the names   |                |                 |
|             |     of the      |                |                 |
|             |     tokens.     |                |                 |
|             | -   The token   |                |                 |
|             |     names can   |                |                 |
|             |     be user     |                |                 |
|             |     defined or  |                |                 |
|             |     can be one  |                |                 |
|             |     of the      |                |                 |
|             |     system's   |                |                 |
|             |     predefined  |                |                 |
|             |     tokens that |                |                 |
|             |     begin with  |                |                 |
|             |     a dollar    |                |                 |
|             |     sign        |                |                 |
|             |     (**$**).   |                |                 |
|             | -   The SAM     |                |                 |
|             |     expands     |                |                 |
|             |                 |                |                 |
|             |    user-defined |                |                 |
|             |     tokens to   |                |                 |
|             |     the actual  |                |                 |
|             |     TKNVAL.     |                |                 |
|             | -   The SAM     |                |                 |
|             |     expands     |                |                 |
|             |     system      |                |                 |
|             |     tokens in a |                |                 |
|             |                 |                |                 |
|             |   predetermined |                |                 |
|             |     manner,     |                |                 |
|             |     using the   |                |                 |
|             |     TKNVAL for  |                |                 |
|             |     formatting  |                |                 |
|             |     only.       |                |                 |
+-------------+-----------------+----------------+-----------------+
| TKNVAL      | This column     | varchar (4000) | -   The         |
|             | contains the    |                |     contents of |
|             | values of the   |                |     the token   |
|             | tokens.         |                |     can be      |
|             |                 |                |     either a    |
|             |                 |                |     value,      |
|             |                 |                |     directly    |
|             |                 |                |     substituted |
|             |                 |                |     by the SAM, |
|             |                 |                |     or          |
|             |                 |                |     formatting  |
|             |                 |                |     information |
|             |                 |                |     for System  |
|             |                 |                |     Tokens.     |
|             |                 |                | -   For         |
|             |                 |                |     example,    |
|             |                 |                |     the         |
|             |                 |                |     contents of |
|             |                 |                |     tokens      |
|             |                 |                |     $DATE and  |
|             |                 |                |     $NOW is    |
|             |                 |                |     Short Date, |
|             |                 |                |     which is    |
|             |                 |                |     interpreted |
|             |                 |                |     by the SAM  |
|             |                 |                |     to whatever |
|             |                 |                |     short date  |
|             |                 |                |     format was  |
|             |                 |                |     specified   |
|             |                 |                |     in the      |
|             |                 |                |     Regional    |
|             |                 |                |     Settings of |
|             |                 |                |     the Control |
|             |                 |                |     Panel.      |
+-------------+-----------------+----------------+-----------------+
| TKNLENGTH   | This column     | smallint (2)   | Valid values    |
|             | contains the    |                | range from 1 to |
|             | lengths for the |                | 77.             |
|             | values in the   |                |                 |
|             | TKNVAL column   |                |                 |
+-------------+-----------------+----------------+-----------------+

: TOKEN Column Descriptions

  Index Code   Columns
  ------------ ---------
  PK_TOKEN     TKNID

  : TOKEN Index Descriptions

### TOKEN_AUX

The TOKEN_AUX table contains auxiliary information about Tokens. The
Token ID links the auxiliary information to the primary information.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| TKNID       | -   This column | int (4)        | None            |
|             |     contains    |                |                 |
|             |     the token   |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     TOKEN       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| TAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| TASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| TAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: TOKEN_AUX Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_TOKENAUX | TKNID   |
|             |         |
|             | TAFC    |
|             |         |
|             | TASEQNO |
+-------------+---------+

: TOKEN_AUX Index Descriptions

### UACCESS

The UACCESS table contains Access Code privilege information. Access
Codes allow you to lock or hide specific job records from other users,
even on a schedule those users have access to.

  ----------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------
  ![White pencil/paper icon on gray circular background](../../Resources/Images/note-icon(48x48).png "Note icon")   **NOTE:** [You cannot see records that have an Access Code to which you do not have permission.]
  ----------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| USERID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     ROLEIDs with |              |                  |
|             |     privileges   |              |                  |
|             |     to the       |              |                  |
|             |     access       |              |                  |
|             |     codes.       |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     ROLES table. |              |                  |
+-------------+------------------+--------------+------------------+
| ACCESSCDID  | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     Access Code  |              |                  |
|             |     IDs granted  |              |                  |
|             |     to the       |              |                  |
|             |     users.       |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     ACCESSCD     |              |                  |
|             |     table.       |              |                  |
+-------------+------------------+--------------+------------------+
| CANUPDATE   | This column      | smallint (2) | -   0: Indicates |
|             | contains the     |              |     that you can |
|             | flag to          |              |     only view    |
|             | determine each   |              |     records with |
|             | user's rights.  |              |     this Access  |
|             |                  |              |     Code.        |
|             |                  |              | -   1: Indicates |
|             |                  |              |     that you can |
|             |                  |              |     update       |
|             |                  |              |     records with |
|             |                  |              |     this Access  |
|             |                  |              |     Code.        |
+-------------+------------------+--------------+------------------+

: UACCESS Column Descriptions

+------------+------------+
| Index Code | Columns    |
+============+============+
| PK_UACCESS | USERID     |
|            |            |
|            | ACCESSCDID |
+------------+------------+

: UACCESS Index Descriptions

### UDEPFUN

The UDEPFUN table contains information on what Departmental and
Non-Departmental privileges each user has. One record per function is
entered for each user.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| USERID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     role IDs     |              |                  |
|             |     with         |              |                  |
|             |     privileges   |              |                  |
|             |     to the       |              |                  |
|             |     functions.   |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     ROLES table. |              |                  |
+-------------+------------------+--------------+------------------+
| DEPTID      | -   This column  | smallint (2) | -   A valid      |
|             |     contains the |              |     non-zero     |
|             |     department   |              |     department   |
|             |     IDs.         |              |     ID           |
|             | -   This column  |              |     associates   |
|             |     contains     |              |     the granted  |
|             |                  |              |     function to  |
|             |  cross-reference |              |     the specific |
|             |     information  |              |     department.  |
|             |     for lookup   |              | -   A zero value |
|             |     into the     |              |     indicates    |
|             |     DEPTS table. |              |     ALL          |
|             |                  |              |     departments  |
|             |                  |              |     or a         |
|             |                  |              |                  |
|             |                  |              | non-departmental |
|             |                  |              |     privilege.   |
+-------------+------------------+--------------+------------------+
| FUNCID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     function     |              |                  |
|             |     IDs.         |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     FUNCDESC     |              |                  |
|             |     table.       |              |                  |
+-------------+------------------+--------------+------------------+

: UDEPFUN Column Descriptions

+------------+---------+
| Index Code | Columns |
+============+=========+
| PK_UDEPFUN | USERID  |
|            |         |
|            | DEPTID  |
|            |         |
|            | FUNCID  |
+------------+---------+

: UDEPFUN Index Descriptions

### UMACHGRP

The UMACHGRP table is currently not in use.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| USERID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     ROLEIDs with |              |                  |
|             |     privileges   |              |                  |
|             |     to the       |              |                  |
|             |     machine      |              |                  |
|             |     groups.      |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     ROLES table. |              |                  |
+-------------+------------------+--------------+------------------+
| MACHGRPID   | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     Machine      |              |                  |
|             |     Group IDs    |              |                  |
|             |     granted to   |              |                  |
|             |     the users.   |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     MACHGRPS     |              |                  |
|             |     table.       |              |                  |
+-------------+------------------+--------------+------------------+
| CANUPDATE   | This column      | smallint (2) | -   0: Indicates |
|             | contains the     |              |     that you can |
|             | flag to          |              |     only view    |
|             | determine each   |              |     records with |
|             | user's rights.  |              |     this Machine |
|             |                  |              |     Group.       |
|             |                  |              | -   1: Indicates |
|             |                  |              |     that you can |
|             |                  |              |     update       |
|             |                  |              |     records with |
|             |                  |              |     this Machine |
|             |                  |              |     Group.       |
+-------------+------------------+--------------+------------------+

: UMACHGRP Column Descriptions

+-------------+-----------+
| Index Code  | Columns   |
+=============+===========+
| PK_UMACHGRP | USERID    |
|             |           |
|             | MACHGRPID |
+-------------+-----------+

: UMACHGRP Index Descriptions

### UMACHS

The UMACHS table is currently not in use.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| USERID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     ROLEIDs with |              |                  |
|             |     privileges   |              |                  |
|             |     to the       |              |                  |
|             |     machines.    |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     ROLES table. |              |                  |
+-------------+------------------+--------------+------------------+
| MACHID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     Machine IDs  |              |                  |
|             |     granted to   |              |                  |
|             |     the users.   |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     MACHS table. |              |                  |
+-------------+------------------+--------------+------------------+
| CANUPDATE   | This column      | smallint (2) | -   0: Indicates |
|             | contains the     |              |     that you can |
|             | flag to          |              |     only view    |
|             | determine each   |              |     records with |
|             | user's rights.  |              |     this Machine |
|             |                  |              | -   1: Indicates |
|             |                  |              |     that you can |
|             |                  |              |     update       |
|             |                  |              |     records with |
|             |                  |              |     this         |
|             |                  |              |     Machine.     |
+-------------+------------------+--------------+------------------+

: UMACHS Column Descriptions

+------------+---------+
| Index Code | Columns |
+============+=========+
| PK_UMACHS  | USERID  |
|            |         |
|            | MACHID  |
+------------+---------+

: UMACHS Index Descriptions

### USCHED

The USCHED table describes which schedules each user is allowed to
access.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| USERID      | -   This column  | smallint (2) | None             |
|             |     contains the |              |                  |
|             |     role IDs     |              |                  |
|             |     with         |              |                  |
|             |     privileges   |              |                  |
|             |     to the       |              |                  |
|             |     schedule(s). |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     ROLES table. |              |                  |
+-------------+------------------+--------------+------------------+
| SKDID       | -   This column  | int (4)      | None             |
|             |     contains the |              |                  |
|             |     schedule IDs |              |                  |
|             |     granted to   |              |                  |
|             |     the          |              |                  |
|             |     associated   |              |                  |
|             |     users.       |              |                  |
|             | -   This column  |              |                  |
|             |     contains     |              |                  |
|             |                  |              |                  |
|             |  cross-reference |              |                  |
|             |     information  |              |                  |
|             |     for lookup   |              |                  |
|             |     into the     |              |                  |
|             |     SNAME table. |              |                  |
+-------------+------------------+--------------+------------------+

: USCHED Column Descriptions

+------------+---------+
| Index Code | Columns |
+============+=========+
| PK_USCHED  | USERID  |
|            |         |
|            | SKDID   |
+------------+---------+

: USCHED Index Descriptions

### USERS

The primary table USERS contains user information.

+-------------+------------------+---------------+------------------+
| Column Name | Explanation      | Data Type     | Additional       |
|             |                  |               | Information      |
+=============+==================+===============+==================+
| USERID      | -   This column  | smallint (2)  | None             |
|             |     contains the |               |                  |
|             |     user IDs.    |               |                  |
|             | -   This column  |               |                  |
|             |     uniquely     |               |                  |
|             |     identifies   |               |                  |
|             |     each user.   |               |                  |
|             | -   Used for     |               |                  |
|             |     lookup from  |               |                  |
|             |     the          |               |                  |
|             |     AUDITHST,    |               |                  |
|             |     ROLES_AUX,   |               |                  |
|             |     and          |               |                  |
|             |     USERS_AUX    |               |                  |
|             |     tables.      |               |                  |
+-------------+------------------+---------------+------------------+
| USERSIGNON  | -   This column  | char (20)     | None             |
|             |     contains the |               |                  |
|             |     names used   |               |                  |
|             |     for signing  |               |                  |
|             |     into the     |               |                  |
|             |     database.    |               |                  |
|             | -   The user     |               |                  |
|             |     sign-on name |               |                  |
|             |     is used to   |               |                  |
|             |     validate the |               |                  |
|             |     user when in |               |                  |
|             |     to OpCon.    |               |                  |
|             | -   This name    |               |                  |
|             |     should not   |               |                  |
|             |     be defined   |               |                  |
|             |     as a SQL     |               |                  |
|             |     database     |               |                  |
|             |     user.        |               |                  |
|             | -   OpCon uses a |               |                  |
|             |     separate     |               |                  |
|             |     login to SQL |               |                  |
|             |     server.      |               |                  |
+-------------+------------------+---------------+------------------+
| USERNAME    | This column      | char (60)     | None             |
|             | contains the     |               |                  |
|             | descriptive user |               |                  |
|             | names.           |               |                  |
+-------------+------------------+---------------+------------------+
| USERDETS1   | This column      | char (60)     | None             |
|             | contains the     |               |                  |
|             | details for the  |               |                  |
|             | users.           |               |                  |
+-------------+------------------+---------------+------------------+
| USERDETS2   | This column      | char (60)     | None             |
|             | contains the     |               |                  |
|             | additional       |               |                  |
|             | details for the  |               |                  |
|             | users.           |               |                  |
+-------------+------------------+---------------+------------------+
| USERPWD     | This column      | varchar (255) | -   The value is |
|             | contains the     |               |     encrypted    |
|             | login passwords  |               |     when entered |
|             | for the users    |               |     and used to  |
|             |                  |               |     validate     |
|             |                  |               |     user login.  |
|             |                  |               | -   Maximum      |
|             |                  |               |     length for   |
|             |                  |               |     the password |
|             |                  |               |     is 12        |
|             |                  |               |     characters.  |
|             |                  |               | -   The          |
|             |                  |               |     encrypted    |
|             |                  |               |     string is    |
|             |                  |               |     longer than  |
|             |                  |               |     12           |
|             |                  |               |     characters.  |
+-------------+------------------+---------------+------------------+
| USEREXPW    | -   This column  | char (20)     | The password is  |
|             |     contains the |               | not encrypted.   |
|             |     external     |               |                  |
|             |     passwords    |               | The default      |
|             |     (i.e., event |               | value is 20      |
|             |     passwords)   |               | asterisks        |
|             |     for the      |               | (**\***).        |
|             |     users.       |               |                  |
|             | -   These        |               |                  |
|             |     passwords    |               |                  |
|             |     allow the    |               |                  |
|             |     SAM to       |               |                  |
|             |     validate     |               |                  |
|             |     external     |               |                  |
|             |     events that  |               |                  |
|             |     come into    |               |                  |
|             |     the system   |               |                  |
|             |     on behalf of |               |                  |
|             |     these users. |               |                  |
+-------------+------------------+---------------+------------------+

: USERS Column Descriptions

  Index Code   Columns
  ------------ ------------
  PK_USERS     USERID
  I2USERS      USERSIGNON

  : USERS Index Descriptions

### USERS_AUX

The secondary table USERS_AUX contains auxiliary information about
Users. The User ID links the auxiliary information to the primary
information.

+-------------+-----------------+----------------+-----------------+
| Column Name | Explanation     | Data Type      | Additional      |
|             |                 |                | Information     |
+=============+=================+================+=================+
| USERID      | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the user    |                |                 |
|             |     IDs.        |                |                 |
|             | -   This column |                |                 |
|             |     contains    |                |                 |
|             |                 |                |                 |
|             | cross-reference |                |                 |
|             |     information |                |                 |
|             |     for lookup  |                |                 |
|             |     into the    |                |                 |
|             |     USERS       |                |                 |
|             |     table.      |                |                 |
+-------------+-----------------+----------------+-----------------+
| UAFC        | This column     | smallint (2)   | 0:              |
|             | contains the    |                | Documentation   |
|             | auxiliary       |                | field           |
|             | information     |                |                 |
|             | field codes.    |                |                 |
+-------------+-----------------+----------------+-----------------+
| UASEQNO     | -   This column | smallint (2)   | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     sequence    |                |                 |
|             |     numbers.    |                |                 |
|             | -   This column |                |                 |
|             |     provides    |                |                 |
|             |     unique      |                |                 |
|             |                 |                |                 |
|             |  identification |                |                 |
|             |     numbers     |                |                 |
|             |     allowing    |                |                 |
|             |     multiple    |                |                 |
|             |     fields of   |                |                 |
|             |     the same    |                |                 |
|             |     name to be  |                |                 |
|             |     presented   |                |                 |
|             |     on a single |                |                 |
|             |     screen.     |                |                 |
+-------------+-----------------+----------------+-----------------+
| UAVALUE     | -   This column | varchar (4000) | None            |
|             |     contains    |                |                 |
|             |     the         |                |                 |
|             |     auxiliary   |                |                 |
|             |     information |                |                 |
|             |     content.    |                |                 |
|             | -   This column |                |                 |
|             |     stores the  |                |                 |
|             |     data from   |                |                 |
|             |     the         |                |                 |
|             |     associated  |                |                 |
|             |     field in    |                |                 |
|             |     the         |                |                 |
|             |     Enterprise  |                |                 |
|             |     Manager.    |                |                 |
+-------------+-----------------+----------------+-----------------+

: USERS_AUX Column Descriptions

+-------------+---------+
| Index Code  | Columns |
+=============+=========+
| PK_USERSAUX | USERID  |
|             |         |
|             | UAFC    |
|             |         |
|             | UASEQNO |
+-------------+---------+

: USERS_AUX Index Descriptions

### USRSECUR

The USRSECUR table contains information on User IDs for jobs to run
under on each applicable operating system.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| SECURID     | This column      | smallint (2) | None             |
|             | contains the IDs |              |                  |
|             | of the security  |              |                  |
|             | tokens.          |              |                  |
+-------------+------------------+--------------+------------------+
| OSTYPE      | This column      | smallint (2) | -   3: Windows   |
|             | contains the     |              | -   4: OpenVMS   |
|             | operating system |              | -   5: i5/OS     |
|             | type for each    |              | -   6: UNIX      |
|             | security token.  |              | -   9: MCP       |
+-------------+------------------+--------------+------------------+
| USERSPEC    | -   This column  | char (61)    | None             |
|             |     contains the |              |                  |
|             |     Batch user   |              |                  |
|             |     names or IDs |              |                  |
|             |     to verify    |              |                  |
|             |     before       |              |                  |
|             |     submitting   |              |                  |
|             |     jobs.        |              |                  |
|             | -   Also known   |              |                  |
|             |     as the Batch |              |                  |
|             |     User ID, the |              |                  |
|             |     user name or |              |                  |
|             |     ID must be   |              |                  |
|             |     valid for    |              |                  |
|             |     the defined  |              |                  |
|             |     operating    |              |                  |
|             |     system.      |              |                  |
|             | -   For example, |              |                  |
|             |     the NT       |              |                  |
|             |                  |              |                  |
|             |    specification |              |                  |
|             |     is           |              |                  |
|             |                  |              |                  |
|             |  domain\\userid; |              |                  |
|             |     whereas, the |              |                  |
|             |     UNIX         |              |                  |
|             |                  |              |                  |
|             |    specification |              |                  |
|             |     is           |              |                  |
|             |                  |              |                  |
|             |   groupid/userid |              |                  |
|             |     expressed in |              |                  |
|             |     numeric      |              |                  |
|             |     format.      |              |                  |
|             |                  |              |                  |
|             | **Caution:**     |              |                  |
|             | When an invalid  |              |                  |
|             | user name or ID  |              |                  |
|             | is used on a     |              |                  |
|             | job, the job     |              |                  |
|             | does not         |              |                  |
|             | process.         |              |                  |
+-------------+------------------+--------------+------------------+
| USERPWD     | This column      | char (64)    | The value is     |
|             | contains the     |              | encrypted.       |
|             | User passwords   |              |                  |
|             | for each         |              |                  |
|             | Microsoft        |              |                  |
|             | Windows user.    |              |                  |
+-------------+------------------+--------------+------------------+

: USRSECUR Column Descriptions

  Index Code    Columns
  ------------- ---------
  PK_USRSECUR   SECURID

  : USRSECUR Index Descriptions

### USYSACC

The USYSACC table links the users with the security IDs they have
privileges to for each operating system.

+-------------+------------------+--------------+------------------+
| Column Name | Explanation      | Data Type    | Additional       |
|             |                  |              | Information      |
+=============+==================+==============+==================+
| USERID      | This column      | smallint (2) | None             |
|             | contains the     |              |                  |
|             | role IDs with    |              |                  |
|             | privileges to    |              |                  |
|             | the Batch User   |              |                  |
|             | IDs.             |              |                  |
+-------------+------------------+--------------+------------------+
| OSTYPE      | This column      | smallint (2) | -   3: Windows   |
|             | contains the     |              | -   4: OpenVMS   |
|             | operating system |              | -   5: i5/OS     |
|             | type of the      |              | -   6: UNIX      |
|             | security token   |              | -   9: A Series  |
|             | granted to the   |              |                  |
|             | user.            |              |                  |
+-------------+------------------+--------------+------------------+
| SECURID     | This column      | smallint (2) | None             |
|             | contains the     |              |                  |
|             | Batch User IDs,  |              |                  |
|             | granted to the   |              |                  |
|             | users, from the  |              |                  |
|             | USRSECUR table.  |              |                  |
+-------------+------------------+--------------+------------------+

: USYSACC Column Descriptions

+------------+---------+
| Index Code | Columns |
+============+=========+
| PK_USYSACC | USERID  |
|            |         |
|            | OSTYPE  |
|            |         |
|            | SECURID |
+------------+---------+

: USYSACC Index Descriptions

### XMLFREQDATA

This table is reserved for internal use by SMA Technologies.
:::
