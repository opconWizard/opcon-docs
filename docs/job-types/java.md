# Java Job Details

The information in this section applies to defining a Java job. The Java
job type supports three operations than can be executed by the Java
Agent: Class, Command, and JAR.

## Class Operation Fields

The Class operation is used to execute a Java class. The following
information applies to defining Class operations:

- **Jar File Name** (Required): Defines the name of the jar file that
    contains the class or method to be executed.
  - Required Extension: .jar
  - Maximum Characters: 4000
  - Valid Characters: alphanumeric, underscore, period, and hyphen

- **Class Name** (Required): Defines the name of the Java class to be
    executed by the Java Agent.
  - Maximum Characters: 4000
  - Valid Characters: alphanumeric, underscore, period, and hyphen

- **Method Name** (Optional): Defines the name of the method in the
    Java class to execute.
  - Default Value: main
  - Maximum Characters: 4000
  - Valid Characters: alphanumeric, underscore, period, and hyphen

- **Alternate JVM** (Optional): Defines the path to an alternate JVM
    to be executed by the Java Agent.
  - Maximum characters: 4000
  - Valid characters: all

- **Parameters** (Optional): Defines the parameters that will be
    passed to the method of the Java class that will be executed by the
    Java Agent. The parameters are passed in the order in which they are
    defined in the Name Value table.
  - Valid Characters: alphanumeric, underscore, period, and hyphen
  - Valid Values: STRING, INTEGER, LONG, or BOOLEAN
    - The *STRING*, *INTEGER*, *LONG* or *BOOLEAN* parameter type
            must be specified in the Name field with the value specified
            in the Value field.
    - The type of parameter should match the definitions on the
            method call.

- **JVM Arguments** (Optional): Defines the arguments that will be
    passed as JVM-specific (Java Virtual Machine) arguments, also known
    as Java VM Options. It is possible to specify jvmargs that will be
    included on the command line when the Java process is called. For
    more information on Java HotSpot VM Options, refer to
    <http://www.oracle.com/technetwork/articles/java/vmoptions-jsp-140102.mdl>.

    A special argument definition, JAVA_JVM_ARGS, can be used to point
    to a global property that contains a list of arguments described in
    arg=value pairs separated by a comma (e.g.,
    JAVA_JVM_ARGS=\[\[GLOBAL_PROPERTY\]\], where     \[\[GLOBAL_PROPERTY\]\]=\[\[arg1=value1,arg2=value2\]\]). When
    defining these values in global properties, property names should
    not be used.

  - Maximum Characters: 4000
  - Valid Characters: alphanumeric, asterisk, slash, backslash,
        percent, colon, underscore, period, and hyphen

    +----------------------------------+----------------------------------+
    | ![White pencil icon on green     | **EXAMPLE:** [When setting the   |     | circular                         | JVM memory requirements for the  |
    | background](../../Reso           | job:]{.statement2}               |
    | urces/Images/example-icon(48x48) |                                  |
    | .png "Example icon") |                                  |
    |                                  |                                  |
    |                                  | [Insert the memory requirement   |     |                                  | in the JVM Argument Name         |
    |                                  | field:]{.statement2}             |
    |                                  |                                  |
    |                                  | -Xmx256m                         |
    +----------------------------------+----------------------------------+

    +----------------------------------+----------------------------------+
    | ![White pencil icon on green     | **EXAMPLE:** [When using the -D  |     | circular                         | option to set logging            |
    | background](../../Reso           | information:]{.statement2}       |
    | urces/Images/example-icon(48x48) |                                  |
    | .png "Example icon") |                                  |
    |                                  |                                  |
    |                                  | [Insert the option in the JVM    |     |                                  | Argument Name                    |
    |                                  | field:]{.statement2}             |
    |                                  |                                  |
    |                                  | -Dlog4j.configuration            |
    |                                  |                                  |
    |                                  |                                  |
    |                                  |                                  |
    |                                  | [Insert the definition in the    |     |                                  | JVM Argument Value               |
    |                                  | field:]{.statement2}             |
    |                                  |                                  |
    |                                  | file:c:\                         |
    |                                  | \test\\logging\\log4j.properties |
    +----------------------------------+----------------------------------+

- **Environment Variables** (Optional): Defines the variables that
    allow users to specify Operating System Environment Variables. The
    variables will be set as environment variables when the Java process
    is called. These environment variables can be referenced by the Java
    program using the *System.getenv()* function.

    A special argument definition, JAVA_ENV_VARS, can be used to point
    to a global property that contains a list of environment variables
    described in env=value pairs separated by a comma (e.g.,
    JAVA_ENV_VARS=\[\[GLOBAL_PROPERTY\]\], where     \[\[GLOBAL_PROPERTY\]\]=\[\[name1=value1,name2=value2\]\]). When
    defining these values in global properties, property names should
    not be used.

  - Maximum Characters: 4000
  - Valid Characters: alphanumeric, asterisk, slash, backslash,
        percent, colon, underscore, period, and hyphen

    +----------------------------------+----------------------------------+
    | ![White pencil icon on green     | **EXAMPLE:** [When setting a     |     | circular                         | directory                        |
    | background](../../Reso           | definition:]{.statement2}        |
    | urces/Images/example-icon(48x48) |                                  |
    | .png "Example icon") |                                  |
    |                                  |                                  |
    |                                  | [Insert the option in the Env    |     |                                  | Variable Name                    |
    |                                  | field:]{.statement2}             |
    |                                  |                                  |
    |                                  | TEST_HOME                        |
    |                                  |                                  |
    |                                  |                                  |
    |                                  |                                  |
    |                                  | [Insert the definition in the    |     |                                  | Env Variable Value               |
    |                                  | field:]{.statement2}             |
    |                                  |                                  |
    |                                  | c:\\test                         |
    +----------------------------------+----------------------------------+

- **Failure Criteria**: Provides fields to define criteria that
    OpCon uses to determine the final status
    of the job.
  - **Exit Codes**: If any one of the criteria is TRUE at the end of
        a job, OpCon reports the job as
        Failed. Up to five different failure criteria may be defined. A
        failure criterion contains two parts: *Operator* and *Exit Code
        integer*:
    - **Operator**: An exit code criterion may use one of the
            following operators to compare the exit code with a
            user-defined value:
      - **EQ** (equal to)
      - **NE** (not equal to)
      - **LT** (less than)
      - **GT** (greater than)
      - **GE** (greater than or equal to)
      - **LE** (less than or equal to)
    - **Exit Code Integer**: Any integer (-2,147,483,648 through
            2,147,483,647) to compare with the job's exit code.

## Command Operation Fields

The Command operation is used to execute a script. The following
information applies to defining Command operations:

- **Directory Path** (Required): Defines the full directory path of
    the exe or script to execute.
  - Maximum Characters: 4000

- **Executable** (Required): Defines the name of the executable or
    script to execute. The definition must end with an exe, a .cmd, a
    .bat, or a .sh extension.
  - Maximum Characters: 4000

- **Parameters** (Optional): Defines the parameters that will be
    passed to the script. The parameters are passed in the order in
    which they are defined in the Name Value table.
  - Valid Characters: alphanumeric, underscore, period, and hyphen.
  - Valid Values: STRING, INTEGER, LONG, BOOLEAN, or an indicator,
        such as --p, etc.
    - The *STRING* parameter type can be used to specify a single
            parameter to be passed to the script as an argument.
    - If the script arguments include switches, then enter the
            switch in the Name field and the value in the Value field.

- **Environment Variables** (Optional): Defines the variables that
    allow users to specify Operating System Environment Variables. The
    variables will be set as environment variables when the Java process
    is called. These environment variables can be referenced by the Java
    program using the *System.getenv()* function.

    A special argument definition, JAVA_ENV_VARS, can be used to point
    to a global property that contains a list of environment variables
    described in env=value pairs separated by a comma (e.g.,
    JAVA_ENV_VARS=\[\[GLOBAL_PROPERTY\]\], where     \[\[GLOBAL_PROPERTY\]\]=\[\[name1=value1,name2=value2\]\]). When
    defining these values in global properties, property names should
    not be used.

  - Maximum Characters: 4000
  - Valid Characters: alphanumeric, asterisk, slash, backslash,
        percent, colon, underscore, period, and hyphen

    +----------------------------------+----------------------------------+
    | ![White pencil icon on green     | **EXAMPLE:** [When setting a     |     | circular                         | directory                        |
    | background](../../Reso           | definition:]{.statement2}        |
    | urces/Images/example-icon(48x48) |                                  |
    | .png "Example icon") |                                  |
    |                                  |                                  |
    |                                  | [Insert the option in the Env    |     |                                  | Variable Name                    |
    |                                  | field:]{.statement2}             |
    |                                  |                                  |
    |                                  | TEST_HOME                        |
    |                                  |                                  |
    |                                  |                                  |
    |                                  |                                  |
    |                                  | [Insert the definition in the    |     |                                  | Env Variable Value               |
    |                                  | field:]{.statement2}             |
    |                                  |                                  |
    |                                  | c:\\test                         |
    +----------------------------------+----------------------------------+

- **Failure Criteria**: Provides fields to define criteria that
    OpCon uses to determine the final status
    of the job.
  - **Exit Codes**: If any one of the criteria is TRUE at the end of
        a job, OpCon reports the job as
        Failed. Up to five different failure criteria may be defined. A
        failure criterion contains two parts: *Operator* and *Exit Code
        integer*:
    - **Operator**: An exit code criterion may use one of the
            following operators to compare the exit code with a
            user-defined value:
      - **EQ** (equal to)
      - **NE** (not equal to)
      - **LT** (less than)
      - **GT** (greater than)
      - **GE** (greater than or equal to)
      - **LE** (less than or equal to)
    - **Exit Code Integer**: Any integer (-2,147,483,648 through
            2,147,483,647) to compare with the job's exit code.

## JAR Operation Fields

The JAR operation is used to define the execution of a JAR file in a
separate jvm. The following information applies to defining JAR
operations:

**Directory Path** (Required): Defines the full directory path of the
exe or script to execute.

- Maximum Characters: 4000

**Jar File Name** (Required): Defines the name of the jar file that
contains the class or method to be executed.

- Required Extension: .jar
- Maximum Characters: 4000
- Valid Characters: alphanumeric, underscore, period, and hyphen

**Alternate JVM** (Optional): Defines the path to an alternate JVM to be
executed by the Java Agent.

- Maximum characters: 4000
- Valid characters: all

**JVM Arguments** (Optional): Defines the arguments that will be passed
as JVM-specific (Java Virtual Machine) arguments, also known as Java VM
Options. It is possible to specify jvmargs that will be included on the
command line when the Java process is called. For more information on
Java HotSpot VM Options, refer to
<http://www.oracle.com/technetwork/articles/java/vmoptions-jsp-140102.mdl>.

A special argument definition, JAVA_JVM_ARGS, can be used to point to a
global property that contains a list of arguments described in arg=value
pairs separated by a comma (e.g., JAVA_JVM_ARGS=\[\[GLOBAL_PROPERTY\]\], where \[\[GLOBAL_PROPERTY\]\]=\[\[arg1=value1,arg2=value2\]\]). When
defining these values in global properties, property names should not be
used.

- Maximum Characters: 4000
- Valid Characters: alphanumeric, asterisk, slash, backslash, percent,
    colon, underscore, period, and hyphen

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** [When setting the   | | circular                         | JVM memory requirements for the  |
| background](../../Reso           | job:]{.statement2}               |
| urces/Images/example-icon(48x48) |                                  |
| .png "Example icon") |                                  |
|                                  |                                  |
|                                  | [Insert the memory requirement   | |                                  | in the JVM Argument Name         |
|                                  | field:]{.statement2}             |
|                                  |                                  |
|                                  | -Xmx256m                         |
+----------------------------------+----------------------------------+

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** [When using the -D  | | circular                         | option to set logging            |
| background](../../Reso           | information:]{.statement2}       |
| urces/Images/example-icon(48x48) |                                  |
| .png "Example icon") |                                  |
|                                  |                                  |
|                                  | [Insert the option in the JVM    | |                                  | Argument Name                    |
|                                  | field:]{.statement2}             |
|                                  |                                  |
|                                  | -Dlog4j.configuration            |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | [Insert the definition in the    | |                                  | JVM Argument Value               |
|                                  | field:]{.statement2}             |
|                                  |                                  |
|                                  | file:c:\                         |
|                                  | \test\\logging\\log4j.properties |
+----------------------------------+----------------------------------+

**Environment Variables** (Optional): Defines the variables that allow
users to specify Operating System Environment Variables. The variables
will be set as environment variables when the Java process is called.
These environment variables can be referenced by the Java program using
the *System.getenv()* function.

A special argument definition, JAVA_ENV_VARS, can be used to point to a
global property that contains a list of environment variables described
in env=value pairs separated by a comma (e.g.,
JAVA_ENV_VARS=\[\[GLOBAL_PROPERTY\]\], where \[\[GLOBAL_PROPERTY\]\]=\[\[name1=value1,name2=value2\]\]). When
defining these values in global properties, property names should not be
used.

- Maximum Characters: 4000
- Valid Characters: alphanumeric, asterisk, slash, backslash, percent,
    colon, underscore, period, and hyphen

+----------------------------------+----------------------------------+
| ![White pencil icon on green     | **EXAMPLE:** [When setting a     | | circular                         | directory                        |
| background](../../Reso           | definition:]{.statement2}        |
| urces/Images/example-icon(48x48) |                                  |
| .png "Example icon") |                                  |
|                                  |                                  |
|                                  | [Insert the option in the Env    | |                                  | Variable Name                    |
|                                  | field:]{.statement2}             |
|                                  |                                  |
|                                  | TEST_HOME                        |
|                                  |                                  |
|                                  |                                  |
|                                  |                                  |
|                                  | [Insert the definition in the    | |                                  | Env Variable Value               |
|                                  | field:]{.statement2}             |
|                                  |                                  |
|                                  | c:\\test                         |
+----------------------------------+----------------------------------+

**Failure Criteria**: Provides fields to define criteria that
OpCon uses to determine the final status of
the job.

- **Exit Codes**: If any one of the criteria is TRUE at the end of a
    job, OpCon reports the job as Failed. Up
    to five different failure criteria may be defined. A failure
    criterion contains two parts: *Operator* and *Exit Code integer*:
  - **Operator**: An exit code criterion may use one of the
        following operators to compare the exit code with a user-defined
        value:
    - **EQ** (equal to)
    - **NE** (not equal to)
    - **LT** (less than)
    - **GT** (greater than)
    - **GE** (greater than or equal to)
    - **LE** (less than or equal to)
  - **Exit Code Integer**: Any integer (-2,147,483,648 through
        2,147,483,647) to compare with the job's exit code.
:::
