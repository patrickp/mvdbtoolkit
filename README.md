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
  "filedelim": "\ or /",
  "platform": "WINDOWS or LINUX"
}
</pre>

### MVDBTOOLKIT.WEXECUTE

This is for handing calling O/S commands.  It is passed a object and returns a object

<pre>
{ "COMMAND":"COMMAND TO USE",
    "DIRECTORY":"OPTIONAL DIRECTORY TO RUN IN",
    "DEBUG":"YES OR NO",
    "DOCAPTURE":"YES OR NO, DEFAULT YES",
    "RETURNING":"YES OR NO, DEFAULT YES",
    "RTNDATA":"YES OR NO, DEFAULT NO",
    "PASSLIST":"ACTUAL PASSLIST"
    "DATA": ["ARRAY OF DATA STATEMENTS"],
    "RESULT: {
                "RESULT":"RESULT IF CAPTURED",
                "RTNDATA":"RESULT OF RTNDATA",
                "RETURNING":"RESULT OF RETURNING",
                "DEBUG":"DEBUG INFORMATION IF TURNED ON"
    }
    }
</pre>

CALL MVDBTOOLKIT.EXECUTE(OBJ)

There are actually seperate routines for the different platforms.  

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
*        { "name":"field name","value":"field value"}
*    ],
*    "insecure":"Yes,Y,YES - Sets the -k on curl",
*    "timeout": ## (default is 45)
*    "response": {
*        "data":"RESULT",
*        "status":"STATUS",
*        "curl_cmnd":"Actual curl command created"
*    }
*  }
</pre>


