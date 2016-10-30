Initial setup
-------------

Download RCP version.

Edit `eclipse.ini`, add these flags:

    -showLocation
    -Xms512m
    -Xmx966m

UI setup
--------

- Add **Package Explorer** view
    - Window | Show View | Other... | type "Package"
    - Drag it to the left panel, drop the useless Project Explorer view
- Setup **Package Explorer** view to use **Working Sets**
    - Click on the small triangle near the top-right corner
    - Select Top Level Elements | Working Sets
- Add **Problems** view
    - Window | Show View | Other... | type "Problems"
    - Drag it to the leftmost tab in the bottom panel
- Turn on line numbers
    - Preferences | search: line
    - General | Editors | Text Editors | Show line numbers
- Make Maven show XML tab in POM editor by default
    - Maven | User Interface
- Always rerun last run/debug configuration by default
    - Window | Preferences | search for "launch" | Launching
    - Select **Always launch the previously launched application**
- To make `control .` jump to next error only and skip warnings,
  find the **Next Annotation** icon in the toolbar, and in the dropdown menu next to it,
  you can select the type of annotations to consider, and leave only **Errors** enabled

Keyboard shortcuts
------------------

    control 1           quick fix
    control .           jump to next annotation (errors, warnings, ...)
    contorl ,           jump to previous annotation
    F12                 focus to editor
    alt /               complete text
    control k           find next match of last search or highlighted text
    F3                  open implementation / jump to declaration
    control alt h       open call hierarchy
    F11                 debug last run-configuration
    control F11         run last run-configuration
    control shift i     inspect value
    control t           quick type hierarchy
    F4                  open type hierarchy view
    alt shift r         rename symbol

See also: https://www.shortcutworld.com/en/win/Eclipse.html
