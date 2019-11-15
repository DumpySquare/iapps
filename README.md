# iapps
All about F5 TCL iApps

Ya know, I have a ton to say about iapps...  
For now, let's just stick with documenting what I've learned, what's been written, and maybe it will help someone at some point.

Basically, at it's core, if you can issue tmsh commands, you can write an iapp.


iApps are based on TCL, TMOS is based in TCL, iRules are TCL.  ALL OF IT'S TCL!!!

##############################################
How do I currently write iapps?  A little about my setup

VScode is the core of all my coding.  It's a great tool with tons of really great plugins.  It does way more than I thought I needed it to do.  Mayby I should write something about it sometime...

With VSCode, there are plug-ins to help with F5 stuff, like TCL and iApps, get them, syntax highlighting, auto complete, good stuff.
*** idea: write a vscode plugin to manage irules like the irules editor - would need to be able to connect to F5s, grab config options and save them back to the F5 when done - I know there is a TCL extension, let's see what it can do and/or if it can be extended ***

https://marketplace.visualstudio.com/items?itemName=bitwisecook.iapp
https://marketplace.visualstudio.com/items?itemName=bitwisecook.irule
https://marketplace.visualstudio.com/items?itemName=bitwisecook.tcl

The best VSCode plugins:  Microsoft Remote Development pack
 - This pack allows you to connect to linux machines over SSH (including F5s), docker containers or WSL
 https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack
 
 So, get VSCode connected to your DEV F5, do not connect it to a production F5.  Remote VSCode installs itself on the f5, including any modules needed for development, like python linters and the stuff needed for the remote connection.  For now, it all gets installed in the user directory, which can fill up quickly and cause things to start gettin goofy...
 
 **** add link to document on getting VScode connect to an F5 - make bash script in future ***
 
 Once connected to F5, I suggest setting your directory to /config, then you can see all the main config files.  Create a folder to work in.  I typically call it /config/iapps/  or /config/deving/.  Then I can copy and paste in an iapp to start to modify or, create a new blank iapp in the gui, copy/paste the object from the /config/bigip_script.conf
 
 tmsh create sys application template <name> - drops you right into an editor to create a new iapp
  - it's vim'ish so, just ESC, :x to save and quit, then "Y" to save the changes to the config.
 tmsh list sys application template <new_iapp_name>
 
shortcut:  $ tmsh list sys application template new_test_iapp >> /config/iapps/new_test_iapp.tmpl

Open the new file in VSCode, edit away, save.

Then merge it back into the running config:  tmsh load sys config file /config/iapps/new_test_iapp.tmpl

If it loads, you're halfway there!
