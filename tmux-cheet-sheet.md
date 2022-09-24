Attach and detach to sessions
-----------------------------

    tmux new -s name
    tmux attach -t name
    tmux list-sessions

Basics
------

    prefix ?          show key bindings; search with `/`, it's case insensitive
    
    prefix c          create
    prefix n          next
    prefix p          previous
    prefix 0          select 0
    prefix 9          select 9
    prefix d          detach
    prefix &          kill current window
    prefix : kill-session  kill current session
 
    prefix w          show a list of sessions and windows; and switch to any other window in any session
    prefix ,          rename current window
    prefix $          rename current session

Splitting windows
-----------------

    prefix "          split window vertically
    prefix %          split window horizontally
    prefix o          switch to another pane
    prefix x          kill pane

Copy-paste
----------

Enter copy mode with `prefix [` or `prefix PgUp`.

Move the cursor to the top of the text to copy and press `space`.

Move the cursor to the end of the text to copy and press `enter`.

Paste the last copied buffer with `prefix ]`, or select a previous buffer with `prefix =`.

Misc
----

    prefix t          show a clock :-)

Migrating from `screen` to `tmux`
---------------------------------

To change the prefix from `C-b` to `C-a`, add in `~/.tmux.conf`:

    set-option -g prefix C-a
    unbind-key C-b
    bind-key C-a send-prefix

It seems that to apply changes, you must restart tmux, stopping all sessions.

To jump to the beginning of the line in Bash, instead of `C-a a` it's `C-a C-a`.

Resources
---------

1. `man tmux`
