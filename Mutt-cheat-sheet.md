Quick tips
----------

* Mark all messages read

    * Step 1: tag all messages matching regex: `T.`

    * Step 2: clear new flag on tagged messages: `;WN`


Automatically move read mails out of Inbox
------------------------------------------
* Note: you want to move read mails out of Inbox for very practical reasons

    * To not get the message about new email every time you start a new shell.

    * If your Inbox grows big, you will experience a delay when logging in to the server.
      With a huge Inbox, the delay can be extremely long.

* By default, all mails are appended to `~/Mail/root`

* To automatically move read mails to `~/Mail/read_inbox` when exiting mutt, at this to `.muttrc`

        set move=yes
        set mbox=+read_inbox

* This works even when new emails are not in a flat file but in a folder like `~/Maildir/new`
