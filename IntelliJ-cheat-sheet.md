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
    control shift a     find action by name
    control alt s       open settings
    control n           open class
    control shift n     open file / resource
    control h           open type hierarchy : control Enter to open selected
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
    control shift F10   run unit test for current scope; creates run configuration if doesn't exist
    shift F10           run last configuration
    control pageup      jump to top
    alt j               macro trigger key (see Macros section below)
    control q           quick documentation
    control home        jump to top
    control end         jump to bottom
    shift shift         search everywhere (might nothing happen at first, may need to build some index, give it a few seconds)

Linux
-----

    alt enter               intention actions
    control shift a         find action by name
    control alt s           open settings
    control shift t         open class
    control shift r         open file / resource
    control h               open type hierarchy : control Enter to open selected
    F2                      jump to next error
    F3                      jump to declaration
    control tab             switch between open files (keep control down!)
    alt /                   complete word
    esc esc                 switch to editor
    alt 1                   switch to / toggle project tool window
    alt insert              new file / package / constructor / ...
    alt up                  move line up
    control F4              close window
    shift delete            cut current line
    ?control x		    	cut current line
    ?control y    			delete current line
    ?control l              jump to line
    control pageup          jump to top
    ?control q              quick documentation
    control home            jump to top
    control end             jump to bottom
    control alt shift n     open any symbol or field
    alt shift c             quickly review recent changes
    control alt t           surround code with... (if, for, ...)
    F12                     move focus to the last focused tool window
    shift escape            close current tool window and switch to editor window
    control `               quickly switch color theme (and others)
    control shift i         View | Quick Definition; quickly review definition or content of the symbol at caret, without the need to open it in a new editor tab
    alt home                jump to navigation bar; use the arrow keys to locate the necessary files or folders
    control shift F7        on implements keyword shows the list of overridden methods

Mac OS X
--------

    option enter        intention actions
    cmd shift a         find action by name
    cmd ,               open settings
    cmd o               open class
    cmd shift o         open file (resource)
    ?cmd h              open type hierarchy : control Enter to open selected
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
    cmd j               macro trigger key (see Macros section below)
    ?control q          quick documentation
    cmd fn left         jump to top
    cmd fn right        jump to bottom
    cmd shift F7        Edit | Find | Highlight Usages in File
    option F7           Find Usages
    command F7          Find Usages in File
    control shift q     View | Context Info: see the declaration of the current method without the need to scroll to it
    control up          move quickly between methods in the editor

Misc
----

- Click on `implements` keyword to highlight overridden methods
- Click on a `return` or `throw` keyword to highlight all exit points from a method

Macros
------

Macros are useful to insert code templates.

To run macros, just type the letters where you want to insert it in the code,
and press the trigger key (see shortcuts above).

    sout        insert System.out.println()
    iter        insert for-each iterator to iterate over an iterable in the current scope

Live templates
--------------

http://stackoverflow.com/documentation/intellij-idea/2703/live-templates
