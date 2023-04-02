https://jurajtomori.wordpress.com/2018/01/15/houdini-tip-taking-advantage-of-environment-variables/

# HOUDINI TIP | TAKING ADVANTAGE OF ENVIRONMENT VARIABLES

Like many other applications, Houdini’s configuration can be modified by using environment variables. It is a very useful way of creating different Houdini setups for different purposes – let it be different projects, different plugin versions, sandboxes for testing assets, personal configurations, etc. While this post is written for Houdini and have examples for windows and linux, it is applicable for any other application and operating system.

## A COUPLE OF WORDS ABOUT ENVIRONMENT VARIABLES.
At first I will try to explain basic concepts of env vars and later on I will show examples for Houdini (linux and windows).

Environment variables might be a bit hidden to many users, but they can be very helpful. Actually a lot of operating system behavior is controlled by them. Apart from configuring Houdini, env vars can be used to modify a search path for binaries, libraries, can set up proxy settings, get current user’s name, path to home, temp directory, hostname, shell and much more.

An useful thing is that they can be applied globally to the whole system, and locally to the current environment in a shell (a terminal session or environment set up and executed from batch/bash script). For example one might specify global settings which are available to the whole system (path to system cache dir, username, path to root directory of all projects…) and local settings for each configured environments (houdini version, project name, project root, path to textures directory, license information about a plugin…). All child environments (set up through batch/bash script) will inherit global settings (available to the whole operating system or an user) and can have specific local settings needed for their purpose.

Here are couple of situations which env vars can efficiently address:

-[x] having a multiple versions of Houdini using different renderer plugin versions and different assets libraries
-[x] using different configurations for different projects / sequences / shots / tasks
-[x] sharing the same settings (home dir, temp dir, cache dir, footage path, rv path) for various applications (Houdini, Nuke, Katana, Maya)
 
## USING ENVIRONMENT VARIABLES ON WINDOWS
Here I will show an example of one of my Houdini startup script which sets an environment for a project and executes Houdini: houdini.bat.
Note that Houdini understands a lot of useful env vars, documentation can be found here.

```sh
@echo off
rem houdini launcher

rem source global vars
call \\network_drive\current_project\00_pipeline\globals.bat

rem set Houdini paths
rem variables PIPELINE, ROOT were set in globals.bat
set "HOUDINI_VERSION=Houdini 15.5.632"
set "HOUDINI_PATH=&;%PIPELINE%/houdini"
set "HOUDINI_OTLSCAN_PATH=&;%ROOT%/20_assets/otls"
set "HOUDINI_SPLASH_FILE=%PIPELINE%/houdini/splash.jpg"
set "HOUDINI_SPLASH_MESSAGE= | JELLY FISH | %HOUDINI_VERSION% | %USERNAME% |"
set "JOB=%ROOT%"
set "HOUDINI_BACKUP_FILENAME=$BASENAME_bak_$N"
set "HOUDINI_BACKUP_DIR=bak"
set "HOUDINI_NO_START_PAGE_SPLASH=1"
set "HOUDINI_ANONYMOUS_STATISTICS=0"
set "HOME=%ROOT%/05_user/%USERNAME%"
set "HOUDINI_DESK_PATH=&;C:/Users/%USERNAME%/Documents/houdini15.5/desktop"
set "HOUDINI_TEMP_DIR=%HOME%/tmp"
set "HOUDINI_BUFFEREDSAVE=1"
set "HOUDINI_IMAGE_DISPLAY_GAMMA=1"
set "HOUDINI_IMAGE_DISPLAY_LUT=%PIPELINE%/houdini/linear-to-srgb_14bit.lut"
set "HOUDINI_IMAGE_DISPLAY_OVERRIDE=1"
set "MEGASCANS=%JOB%/20_assets/megascans/Megascans/"
set "MEGASCANS3D=%MEGASCANS%3d/"
rem convert to forward slashes
set "MEGASCANS=%MEGASCANS:\=/%"
set "MEGASCANS3D=%MEGASCANS3D:\=/%"

rem create temp dir for houdini user if it does not exist, also convert to forwardslashes
set "TMP=%HOUDINI_TEMP_DIR%"
set "TMP=%TMP:/=\%"
IF not exist %TMP% (mkdir %TMP%)

rem run Houdini
set "HOUDINI_DIR=C:\Program Files\Side Effects Software\%HOUDINI_VERSION%\bin"
set "PATH=%HOUDINI_DIR%;%PATH%"
cd ../../
start houdinifx
```

Here I will explain some of batch syntax:
@echo off – hides printing of commands into the console, it makes output more readable
rem foo – lines starting with rem are comments
call foo.bat – executes foo.bat batch script and inherits all env vars specified in it
%MYVAR% – value of MYVAR variable
set “MYVAR=FOO” – sets MYVAR variable to FOO – those variables are specific to softwares, which are expecting them
set “PATH=%PATH%;FOO” – appends FOO to the PATH variable which is used for locating binaries to be executed (houdinifx command is not known to the whole windows system, only when houdini bin directory (containing houdinifx.exe) is appended to the PATH var)
start foo – executes foo.exe (which must be found in one of the paths in the PATH env var) while passing on all existing variables to this child environment

This script can be used for setting up local environment variables, to define a variable for the whole system environment on windows, follow this video.


USING ENVIRONMENT VARIABLES ON LINUX
(Linux version should be directly transferable to mac OS.)

In linux env vars can be set up on multiple locations (~/.profile, ~/.bashrc, ~/.bash_profile, ~/.bash_login, /etc/environment …)
System env vars can be specified in /etc/environment. User env vars can be specified in ~/.profile (~ symbol points to the user home directory).
~/.profile, ~/.bashrc, ~/.bash_profile, and ~/.bash_login have similar usage, but I recommend using ~/.profile, which is the only one executed when running applications from graphical environment in a desktop session..

In a Bash terminal the quickest way of executing an application inheriting env vars is to use this syntax: