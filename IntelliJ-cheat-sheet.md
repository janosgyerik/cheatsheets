IntelliJ cheat sheet
====================

My cheat sheet of IntelliJ (and PyCharm) shortcuts.


Initial setup
-------------

- Open settings:
  <kbd>Control</kbd> + <kbd>Alt</kbd> + <kbd>s</kbd> or <kbd>cmd</kbd> + <kbd>,</kbd>

- Disable spell checking:
  - Filter by *"spell"*, and then: **Inspections / Spelling / Typo**

- Ensure line feed at file end:
  - Filter by *"end of line"*, and then: **Editor / Ensure line feed at file end on Save**

- Jump to high priority errors first:
  - Filter by *"next error"*, and then: **Editor / 'Next Error' action goes to high priority problems only**

- Show line numbers:
  - Filter by: *"line num"*, and then: **Editor / Appearance / Show line numbers**


Windows
-------

    alt enter           intention actions
    control alt s       open settings
    control n           open class
    control shift n     open file / resource
    control shift a     find action by name
    F2                  jump to next error
    control b           jump to declaration
    control tab         switch between open files (keep control down!)
    alt /               complete word
    esc esc             switch to editor
    alt 1               switch to / toggle project tool window
    alt insert          new file / package / constructor / ...
    control shift up    move up statement / method / class / ...
    control F4          close window
    shift delete        cut current line
    control x           cut current line
    control y           delete current line
    control g           jump to line
    run unit test       control shift F10
    run last            shift F10


Linux
-----

    alt enter           intention actions
    control alt s       open settings
    control shift t     open class
    control shift r     open file / resource
    control shift a     find action by name
    F2                  jump to next error
    F3                  jump to declaration
    control tab         switch between open files (keep control down!)
    alt /               complete word
    esc esc             switch to editor
    alt 1               switch to / toggle project tool window
    alt insert          new file / package / constructor / ...
    alt up              move line up
    control F4          close window
    shift delete        cut current line
    control l           jump to line


Mac OS X
--------

    option enter        intention actions
    cmd ,               open settings
    cmd o               open class
    cmd shift o         open file (resource)
    cmd shift a         find action by name
    F2                  jump to next error
    cmd b               jump to declaration
    control tab         switch between open files (keep control down!)
    option /            complete word
    esc esc             switch to editor
    cmd 1               switch to project tool window
    control n           new file / package / constructor / ...
    cmd shift up        move up statement / method / class / ...
    option shift up     move up line
    cmd w               close window
    cmd x               cut current line
    cmd y               delete current line
    cmd g               jump to line
    run unit test       control shift F10
    run last            shift F10
    cmd option l        reindent, reformat, organize
