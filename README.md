# mvdbtoolkit
Toolkit to hold cross platform utilities for common actions that are different between platforms.


The idea of this library is for it to be cross platform, handling both mv types and O/S differences

## Version 2.0 - 5/22/2019

### MVDBTOOLKIT.WPLATFORM

This function gets the platform information.  Instead of guessing this routine pulls a json config item from the MD/Voc.
This was faster/easier than detecting.  This could be improved in the future to do auto detection.

DICT MVDBTOOLKIT.BP MVDBTOOLKIT.PLATFORM.JSON

<pre>
{ "mvtype": "D3,JBASE",
  "platform": "WINDOWS or LINUX"
}
</pre>

### MVDBTOOLKIT.WEXECUTE

This is for handing calling O/S commands.  It is passed a object and returns a object

<pre>
{ "command":"COMMAND TO USE",
    "directory":"OPTIONAL DIRECTORY TO RUN IN",
    "debug":"YES OR NO",
    "docapture":"YES OR NO, DEFAULT YES",
    "returning":"YES OR NO, DEFAULT YES",
    "rtndata":"YES OR NO, DEFAULT NO",
    "passlist":"ACTUAL PASSLIST"
    "data": ["ARRAY OF DATA STATEMENTS"],
    "result: {
                "result":"RESULT IF CAPTURED",
                "rtndata":"RESULT OF RTNDATA",
                "returning":"RESULT OF RETURNING",
                "debug":"DEBUG INFORMATION IF TURNED ON"
    }
    }
</pre>

CALL MVDBTOOLKIT.EXECUTE(OBJ)

There are actually seperate routines for the different platforms.  

#### MV Platform Implementations

A unique routine exists for each platform

|  Feature   | jBase    |  D3   |   Universe   |  Unidata  |   OpenQM       |
| ---------- | -------- | ----- | ------------ | --------- | -------------- |
| Built      |   Yes    |  No   |     No       |    No     |     No         |
| returning  |   No     |  No   |     No       |    No     |     No         |
| rtndata    |   No     |  No   |     No       |    No     |     No         |
| passlist   |   No     |  No   |     No       |    No     |     No         |
| data       |   Yes    |  No   |     No       |    No     |     No         |
| debug      |   Yes    |  No   |     No       |    No     |     No         |


### WFILEIO

This function handles doing O/S file io in a consitent manner across platforms. It takes a object as it's only param.

<pre>
* INOBJ
*
* { "ACTION":"READ,WRTE,DELETE",
*   "PATH":"PATH TO THE FILE",
*   "DATA":"DATA FOR A WRITE",
*   "dosletter":"OPTIONAL DOS LETTER TO ADD TO PATH",
*   "NEWLINE":"CR,LF,CRLF,DOS,UNIX",
*   "PERMISSIONS":"TBD"
*   "response": {
*       "data":"responsedata",
*       "status":1-ok, else no,
*       "statusmsg":"statusmsg" 
*   }
* }
</pre>


### MVDBTOOLKIT.WCALL - Front end to curl

This is a front end to curl.  It is passed a object for options

<pre>
* MVDBTOOLKIT.WOBJ
* { "method":"GET,PUT,POST,ETC",
*    "url":"URL TO CALL",
*    "headers": { "HEADERNAME":"VALUE", "HEADERNAME":"VALUE" },
*    "body":"BODY",
*    "formfields": [
*        { "name":"field name","value":"field value", "fieldtype":"Optional=file if this should be a file, value is the path" }
*    ],
*    "datafields": [
*        { "name":"field name","value":field value"}
*    ],
*    "insecure":"Yes,Y,YES - Sets the -k on curl",
*    "options":"curl options to add to curl command",
*    "timeout": ## (default is 45)
*    "response": {
*        "data":"RESULT",
*        "status":"STATUS",
*        "curl_cmnd":"Actual curl command created",
*        "status": status code,
*        "statusmsg": "status msg",
*        "http_type": "http type",
*        "headers": { "header1name":"header1value, "header2name":"header2value" },
*        "log": [ "log line1", "log line2" ]
*    }
*  }
</pre>


#### Deployment

| Platform         | Status | 
| ---------------- | ------ | 
| jBase/Windows    |        | 
| jBASE/Linux      |        | 
| d3/Windows       | Pass   | 
| d3/Linux         |        |
| Unidata/Windows  |        |
| Unidata/Linux    |        |
| Universe/Windows |        |
| Universe/Linux   |        |
| Qm/Windows       |        |
| Qm/Linux         |        |

* Need to auto-populate the platform config item

#### d3/Linux
System: 10.10.17.205
Account: MVDB
Path: /home/d3packages/mvdbtoolkit/D3

### d3/Windows
System: 10.10.17.41
Account: dm
Path: c:\d3packages\mvdbtoolkit

Currently using git from remote desktop!!

Still needed to auto create platform json, should add this to mvmake!

1/17/2020  10:56: Fixed WFILEIO write.  Needed to add create temp option
1/17/2020  10:57: Failing at WCALL.RESPONSE.  - Should fix wobj variable not assigned issue also!!
1/19/2020  2:31pm Update wobj to check for unassigned passedobj and action.  Had to update tmp dor d3/windows to be c:\tmp with auto create
1/19/2020  2:31pm Need to re-test all platforms!!!



