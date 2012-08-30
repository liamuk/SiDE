SiDE - The Simple Desktop Environment
=====================================
SiDE is a very minimal desktop environment. The only things it does, for now,
are management of window managers and management of halt / reboot / suspend / 
hibernate / logoff

Dependencies
------------
+ ConsoleKit
+ UPower for suspend / hibernate
+ slock for screen locking

Installation
------------

just run `sudo ./INSTALL`

Configuration
-------------

for each user that wants to use side, 4 things must be done

+ Edit .siderc
+ Create a .${WM}initrc file for each window manager
+ Add `. side-dm` to your .bashrc (or your shell's equivalent)
+ Add `exec side-session $2` to your .xinitrc

### .siderc

This is a simple shell script that is sourced from side-dm
the following options are supported-

+ `SIDE_LOGGING` if set logs X output to ~/.xlog
+ `SIDE_WMS` is an array which sets which window managers are available on logon
+ `SIDE_PREFERRED_WM` sets which window manager to use automatically on logon to
  a tty in $SIDE_PREFERRED_TTYS
+ `SIDE_TTYS` is an array which sets what ttys SiDE is active on
+ `SIDE_PREFERRED_TTYS` is an array which sets what ttys use $SIDE_PREFERRED_WM
  automatically instead of prompting for one

### .${WM}initrc

This is another simple shell script which lists commands to execute on login to ${WM}. e.g. .compizinitrc is run if the user selects compiz at the prompt

All commands in this file should fork or be backgrounded in order to return control of the session back to SiDE (This is important for logoff)

#### Sample .compizinitrc -

```shell
compiz ccp &
tint2 &
pidgin &
nm-applet &
blueman-applet &
gmixer -d &
kupfer &
```
