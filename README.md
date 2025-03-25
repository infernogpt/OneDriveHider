# Onedrive Hider

This batch script hides the OneDrive folder in File Explorer on Windows and makes this change permanent by creating a scheduled task to run the script at every user logon.
-The File Runs On Loadup. You Are Not Ratted Or Have A Virus! This Script Is Open Sourced (On The Page You Are On) So You Can See What You Are Installing

## How to Use

1. Save the script as `hide_onedrive_and_create_task.bat`.
2. Right-click the file and select "Run as administrator".

## Script Details

The script performs the following actions:
1. Displays "Onedrive Hider" in big letters.
2. Hides the OneDrive folder in File Explorer by modifying the registry.
3. Restarts the explorer process to apply the changes.
4. Creates a scheduled task to run the script at every user logon, ensuring the OneDrive folder remains hidden.

## Script

```batch
@echo off
REM Big letters "Onedrive Hider"
echo  ___           _           _               _   _     _      _           
echo / _ \ _ __ ___| |__   __ _| |  _ __   ___ | |_| |__ (_)_ __| | _____ _ __ 
echo| | | | '__/ __| '_ \ / _` | | | '_ \ / _ \| __| '_ \| | '__| |/ / _ \ '__|
echo| |_| | | | (__| | | | (_| | | | | | | (_) | |_| | | | | |  |   <  __/ |   
echo \___/|_|  \___|_| |_|\__,_|_| |_| |_|\___/ \__|_| |_|_|_|  |_|\_\___|_|   

REM Hide OneDrive folder in File Explorer
REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Desktop\NameSpace\{018D5C66-4533-4307-9B53-224DE2ED1FE6}" /v "Attributes" /t REG_DWORD /d 0x00000001 /f
taskkill /f /im explorer.exe
start explorer.exe
echo OneDrive folder is now hidden in File Explorer.

REM Create a scheduled task to run the script at every user logon
schtasks /create /tn "Hide OneDrive Folder" /tr "%~dp0hide_onedrive_and_create_task.bat" /sc onlogon /rl highest /f
echo Scheduled task created to hide OneDrive folder at every logon.
pause
```

## Notes

- Make sure to run the script as an administrator to allow it to make the necessary changes.
- The scheduled task ensures that the OneDrive folder remains hidden even after a system restart or user logon.
