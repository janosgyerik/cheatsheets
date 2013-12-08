## Auto correct / abreviation

- `sf` -- completes to `SELECT * FROM `

You can view the list and create your own in **Session | Syntax | Configure auto correct / abreviations**.

## Gotchas

This kind of queries won't if the `sqlparam` plugin is enabled (the default):

```
CREATE OR REPLACE TRIGGER MYTABLE_TRG
BEFORE INSERT ON MYTABLE
FOR EACH ROW
BEGIN
  SELECT MYTABLE_SEQ.NEXTVAL INTO :NEW.MYID FROM DUAL;
END;
/
```

The problem is that `sqlparam` handles `:NEW` as interactive input, so it pops up a window to let you enter the value, when in fact in this case I needed to run the script verbatim. After unloading the plugin, all should be well. You can do this in **Plugins | Summary**.
