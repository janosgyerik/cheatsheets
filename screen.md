Basics
------

    C-a c          create
    C-a k          destroy
    C-a n          next
    C-a p          previous
    C-a space      next
    C-a backspace  previous
 
    C-a w          show a list of windows
    C-a "          present a list of all windows for selection
    C-a 0          select 0
    C-a 9          select 9
    C-a A          enter a name for the current window
    C-a h          write a hardcopy of the current window (named hardcopy.n)
    C-a x          lock screen
 
    C-a d          detach
    C-a D D        detach and logout
    C-a C-\        quit
 
    C-a t          show system information
 
    C-a ?          show key bindings

Reattach
--------

    screen -d -r
    screen -d -R
    screen -d -RR
    screen -D -r
    screen -D -R
    screen -D -RR

More advanced features
----------------------

    C-a [          enter copy mode, mark copy positions with SPACE
    C-a ]          paste copied text at current cursor position
    C-a _          monitor window for 30 seconds of silence
    C-a M          monitor window for all activity
    C-a S          split window
    C-a TAB        move between split windows
    C-a X          remove window

Practical use cases
-------------------

* In general, whenever you ssh to a remote server to do any work, 
  the first thing you should do is `screen -R mytask` where `mytask` is something to with 
  the task you are about to perform. It will be the name of the screen session, 
  you can suspend and return to it any time.

    * If something you are doing takes a long time (for example, copying or tar-ing a large folder), 
      you don't need to start another ssh session, simply create a new screen window with `C-a c`.

    * If you need to leave your computer, you can just close the ssh window, 
      and later you will be able to continue exactly where you left off, 
      just ssh to the server again and resume the screen session with `screen -R mytask`. 
      If you did not exit the previous screen session cleanly then it might think you are
      still attached to it, and not let you reattach.
      (What will happen in this case is, a completely new screen session will start with name `mytask`.)
      You can fix this by `screen -R mytask -D` which will detach the broken session before trying to re-attach.

    * To suspend (= detach from) the current screen session use `C-a d`

* Suppose you want to start some long process on a remote server,
  put it in the background and close your ssh session to step out somewhere.
  Putting ssh sessions in the background this way can be tricky, what's worse,
  checking later if the long process finish can also be tricky.
  Not anymore. Fire up a new screen session for such tasks,
  then either detach from the screen session cleanly with `C-a d`
  or just close the ssh window altogether, you will still be able to reattach later.

* Creating `~/.screenrc-task` files can be convenient to automatically create windows upon startup.
  Run with `screen -c .screenrc-task`. Example screenrc file:

    sessionname gs
    screen -t manager 0 bash
    screen -t broker 1 bash
    screen -t bash 2 bash
    screen -t bash 3 bash
    screen -t bash 4 bash
    screen -t engine 5 bash
    screen -t bash 6 bash

How to use screen within sudo
-----------------------------

When you are in a sudo shell (for example by sudo su - someuser) you get an error like:

    Cannot open your terminal '/dev/pts/1' - please check.

The workaround:

    script /dev/null
    screen

Resources
---------
1. `man screen`
2. [TIPs Using screen - Gentoo Linux Wiki](http://gentoo-wiki.com/TIP_Using_screen)
