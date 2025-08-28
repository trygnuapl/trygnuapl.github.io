
The trygnuapl service <https://trygnuapl.github.io> is an online, interactive
web browser-based interface to the GNU APL interpreter, in the spirit of
Dyalog's Try APL service <https://tryapl.com>.

## Release Notes for trygnuapl version 1.2 August 2025

### Summary:

  - No User Interface (UI) changes.
  - Changes to the back-end infrastructure.
  - Updated the GNU APL interpreter to version 1.9 SVN 1882 of Aug 26 2025.

### Details:

   - Some very modest hardening of the <https://trygnuapl.github.io>
     service to thwart DoS and monopolization attacks.

   - The back-end HTTP server now implements graceful shutdown upon receipt
     of a signal(7) from the Google Cloud Run apparatus.  This signal comes
     when the trygnuapl service has been idle for (observed) 10-15 minutes.

## Release Notes for trygnuapl version 1.1 July 2025

### Summary:

  - New "SaveAs" button and status indicators.
  - `⎕PW, ⎕PS, ⎕TZ, )wsid` and `]boxing` now maintain state.
  - The key combination Shift+Enter will submit the code buffer.
  - Updated the GNU APL interpreter to version 1.9 SVN 1879 of July 3 2025.

### Details:

#### New user interface features:

  - New "SaveAs" buttons to save the contents of the APL session
    or the coding buffer as a text file to the browser's local filesystem.

  - New status indicator that displays the percent of the trygnuapl
    workspace capacity that is in use.  This quota is specific to
    trygnuapl, not GNU APL.  The trygnuapl service limits workspace
    capacity for memory and network reasons; GNU APL has no such
    limitation.

  - New status indicator of how long it took to package, transmit,
    evaluate, respond, and display each typed expression.  This elapsed duration
    includes the considerable browser, network, and HTTP server overhead.
    It is not indicative of GNU APL performance.

  - Shift+Enter keystroke combination is a new shortcut to submit
    the entire code buffer for evaluation just like the button.

#### Implement features of the APL interpreter:

  - `⎕PW` Printing Width and `⎕TZ` Time Zone system variables are now
    preserved across expression evaluation (i.e state is now retained).

  - `⎕PS` Print Style and `]boxing` settings are now preserved across
    expression evaluation (i.e. state is now retained).

  - `)wsid` setting is now preserved across expression evaluation
    (i.e. state is now retained).

#### Infrastructure:

  - Employ the tini pseudo-init package to oversee the trygnuapl HTTP
    web server.  This is to reap child processes GNU APL may leave behind
    when a `)host` command runs longer than the HTTP timeout.

##### Source code:

To inspect the source code of trygnuapl, run the GNU APL command
   
  `)host cat index.html main.go`

The trygnuapl service consists of a 509-line Go HTTP server coupled to a
318-line HTML+javascript front end.

##### Previous versions:

Version 1.1 July 2025 <https://webserver02-670833050359.us-central1.run.app/>
Version 1.0 June 2025 <https://webserver01-431643316.us-central1.run.app/>
