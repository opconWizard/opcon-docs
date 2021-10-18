---
lang: en-us
title: URL Shortcuts
viewport: width=device-width, initial-scale=1.0
---

# URL Shortcuts

## Self Service Shortcut

To bypass the Home page and go directly to Self Service, you can enter
its dedicated URL. Use the following URL syntax:
[https://server:port/selfservice]{style="color: #6b8e23;"} 
 

When you type the URL in the web browser, you will first be prompted to
log into SMA Solution Manager (if not already logged in). After login,
you will automatically be redirected to the Self Service page.

## Service Request Shortcut

To bypass Self Service and go directly to a Service Request, you can
enter a unique URL. Use the following URL syntax:
[https://server:port/selfservice/servicerequest/execution/servicerequestname]{style="color: #6b8e23;"} 
 

Example:

[https://server:port/selfservice/servicerequest/execution/run backup]{style="color: #6b8e23;"}

 

Modern web browsers don't need you to use URL encoding even if it\'s
good practice to replace special characters with percent-encoding (e.g.,
- for space). For example, in the example above, \"run backup\" may
automatically be transformed into the following:

 

Example:

[https://server:port/selfservice/servicerequest/execution/run-backup]{style="color: #6b8e23;"} 
 

When you type the URL in the web browser, you will first be prompted to
log into SMA Solution Manager (if not already logged in). After login,
you will automatically be redirected to the Service Request form.

 

+----------------------------------+----------------------------------+
| ![White pencil/paper icon on     | **NOTE:** [ Service Request      | | gray circular                    | access via the URL shortcut may  |
| background](../../.              | be impacted by any Hide/Disable  |
| ./Resources/Images/note-icon(48x | rules applied to the Service     |
| 48).png "Note icon") | Request. For this reason, bear   |
|                                  | the following in                 |
|                                  | mind:]               |
|                                  |                                  |
|                                  | -   [If a Service Request is     | |                                  |                                  |
|                                  |  [Disabled](Disabling_Hiding-S |
|                                  | ervice-Requests.md#Disablin), |
|                                  |     the URL shortcut will not be |
|                                  |     honored because the request  |
|                                  |     is disabled.]    |
|                                  | -   [If a Service Request is     | |                                  |     [Hidden](Disabling_Hiding%2  |
|                                  | 0Service-Requests.md#Hiding), |
|                                  |     but not Disabled, then the   |
|                                  |     URL shortcut will be         |
|                                  |     honored. Only users who are  |
|                                  |     provided the shortcut will   |
|                                  |     be able to access the hidden |
|                                  |     Service                      |
|                                  |     Request.]        |
+----------------------------------+----------------------------------+
:::

 

