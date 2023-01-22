# SAMMI livesplit extension

This is an extension for SAMMI that adds the ability to control livesplit, as well as get data or receive events using the LiveSplitWebsocket extension here: https://github.com/Xenira/LiveSplit-Websocket The livesplit Websocket there must be installed for this to work at all, so do that first!

# Install:
  1) Follow the instructions to download and install livesplit websocket from here: https://github.com/Xenira/LiveSplit-Websocket
  2) Download the release version of SAMMI livesplit extenension and install using SAMMI's built in extension installer
  3) Install the test deck from the TestDeck.txt file. This is optional, but recommended if you need examples of how it works with SAMMI.

# Usage:

This extension adds three new commands and several triggers to SAMMI under Extension Commands > Transmitter.

   Livesplit Connect:
      - You must run this command before you can do anything else. This will connect SAMMI to the websocket in livesplit and allow the two programs to communicate. Input the ip and port that you are using in livesplit (default is 127.0.0.1 and 16835).
      
  * Livesplit Command:
      - This will send an instruction to Livesplit. Can be used to reset, start the timer, etc. using hotkeys or buttons from within SAMMI.
      
  * Livesplit Request:
      - This sends a request for data from Livesplit and puts it into a variable of your choice. Fields are listed below.
      
          `request`     - A dropdown menu for which request you are sending to the websocket.
      
          `modifier`    - This field is for modifying specific commands. I have not extensively tested this, so unless you know what you are doing leave it blank.
          
          `variable`    - This will be the variable name that SAMMI will put your data into.
          
          `buttonID`    - This is so that you can choose a button for the variable to belong to so that it doesn't have to be global.
       
  * Extension Triggers
      - In addition to commands SAMMI will also listen in for events from Livesplit that can trigger buttons. If you wish to create a button to listen for events, just create a button and give it an extension trigger with the	Message `livesplit *`. You can then pull the event as a wildcard. You could also just replace the * with whatever event it is you want to trigger the button, for example `livesplit pause` or `livesplit gold`.
  
      - Supported events are listed below.
            
            `pause`
            `reset`
            `resume`
            `skipSplit`
            `split`
            `start`
            `switchComparison`
            `undoAllPauses`
            `undoSplit`
            `pb`
            `gold`
            
      - In addition to the trigger, an object will also be packaged with the trigger. You can use the `Trigger Pull Data` command to get the data in the sent object.

          `Game`                - object with info on game, category, how many (completed) runs so far
          `splits`              - array of all splits with info, an object for each
          `splitindex`          - split number-1 for array usage (so you can do splits[splitindex])
          `bestpossibletime`    - best possible time from this point (in ms)
          `comparison`          - current active comparison (e.g. Personal Best, Average Segments)
          `delta`               - current amount ahead/behind (in ms)
          
      - These additional data points will be packaged with the object while a run is ongoing (after at least one split).

          `ahead`               - returns 1 if you're ahead of the comparison, 0 if behind
          `gained`              - returns 1 if you gained time in that split, 0 if you lost time
          `gold`                - returns 1 if the segment was your best ever, 0 if not
          
 # Troubleshooting:

  * Websocket won't connect.
    - The websocket server in livesplit may not be on. This must be done manually each time you start livesplit or change layouts. Start the server by rightclicking on livesplit > control > Start Server (WS). After you do this make sure SAMMI attempts to connect again with the `Livesplit Connect` command

