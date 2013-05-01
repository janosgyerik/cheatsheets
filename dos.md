== DOS and UNIX ==

Similar (not necessarily equivalent!) programs in DOS and UNIX.

{| border="1" cellspacing="0" cellpadding="5" 
! DOS
! UNIX
|- 
| rmdir /s/q
| rm -fr
|-
| dir /s
| ls -R
|-
| dir /a
| ls -a
|-
| doskey /history
| history
|-
| echo %cd%
| echo $PWD
|-
| findstr 
| grep
|-
| type nul > emptyfile
| > emptyfile
|-
| cmd > nul 2>&1
| cmd > /dev/null 2>&1
|-
| fc
| diff
|-
| net statistics server
| uptime
|-
| cd %0\..
| cd $(dirname "$0")
|}

If you want to use UNIX commands in DOS, get coreutils!

http://sourceforge.net/projects/gnuwin32/files/coreutils/

== Useful DOS commands ==

* title - set the title of a cmd window
* color - set the colors of a cmd window
* tasklist /FI "IMAGENAME eq yourprocname*"

== Enable filename completion in Windows 2000 ==

# Run <code>regedit</code>.
# Navigate to <code>HKEY_CURRENT_USER\Software\Microsoft\Command Processor</code>.
# Make a DWORD value ''EnableExtensions'', equal to 1.
# Make a DWORD value ''CompletionChar'', equal to 9.

== Other tips ==

1. You can drag files and directories from an explorer window to a DOS terminal window to insert the path (correctly escaped).

2. To delete a hidden file:
 attrib -h the_file
 del the_file

* Note: luckily, tab completion works with hidden files too.

3. Various net statistics
 net statistics server
 net statistics workstation

4. Compare two files
 fc f1 f2 >nul
 if errorlevel 1 echo Different

5. Map network drive
 net use Z: \\server\folder

== Shell script template (sample) ==

 @echo off
 rem
 rem File: sqlcmd.cmd
 rem Purpose: a convenient wrapper for sqlcmd.exe
 rem
 
 SETLOCAL
 
 if not exist config.cmd (
     echo The file config.cmd must exist in the current directory.
     echo Create config.cmd from config.cmd.sample and run again.
     pause
     exit /b 1
 )
 call config.cmd
 
 rem Validate configuration
 rem
 if not defined sqlcmd_exe call:undefinedvar sqlcmd_exe & goto:eof
 if not exist %sqlcmd_exe% call:missingexe %sqlcmd_exe% & goto:eof
 if not defined dbserver call:undefinedvar dbserver & goto:eof
 if not defined dbuser call:undefinedvar dbuser & goto:eof
 if not defined dbpass call:undefinedvar dbpass & goto:eof
 if not defined dbname call:undefinedvar dbname & goto:eof
 
 set cmd=%sqlcmd_exe% -S%dbserver% -U%dbuser% -P%dbpass% -d%dbname% %sqlcmd_exe_args% %*
 
 set start_datetime=%date% %time%
 echo.
 echo *** %0: %start_datetime%
 echo *** Command: %cmd%
 echo.
 %cmd%
 set exitcode=%errorlevel%
 echo.
 echo *** Command exit code = %exitcode%
 echo *** Command started on %start_datetime%
 echo *** Command completed on %date% %time%
 echo.
 
 if defined sqlcmd_pause pause
 
 exit /b %exitcode%
 
 goto:eof
 
 :missingexe
 
 echo Error: executable does not exist: %1
 exit /b 1
 
 :undefinedvar
 
 echo Error: variable is not defined: %1
 exit /b 1
 
 goto:eof
 
 rem eof
 

== Function template ==

 :myDosFunc         -- function description here
 ::                 -- %~1: argument description here
 SETLOCAL
 REM.--function body here
 set LocalVar1=...
 set LocalVar2=...
 (ENDLOCAL & REM -- RETURN VALUES
     IF "%~1" NEQ "" SET %~1=%LocalVar1%
     IF "%~2" NEQ "" SET %~2=%LocalVar2%
 )
 GOTO:EOF

Call it with：
 call:myDosFunc %var1% %var2%

== Weirdness ==

=== Setting variables in a FOR loop ===

The code below does NOT work!
 FOR %%A IN (c:\test\*) do (
   set value=something
   echo %value%
 )

This works!
 SETLOCAL ENABLEDELAYEDEXPANSION
 FOR %%A IN (c:\test\*) do (
   set value=something
   echo !value!
 )

== DOS links ==

# [[Windows cheat sheet]]
# [http://www.ss64.com/nt/ An A-Z Index of the Windows XP command line]
# http://www.vbsedit.com/
# http://www.emeditor.com/
# http://sourceforge.net/projects/gnuwin32/files/coreutils/
