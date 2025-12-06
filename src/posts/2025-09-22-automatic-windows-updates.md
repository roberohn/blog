---
title: Automatic Windows Update via PowerShell &amp; GPO
description: Simple and rudimentary script to update Windows on a set schedule.
date: '2025-09-22'
categories:
  - windows
published: true
---

### Windows Updates

Windows has a habit of constantly telling you it requires updates to be installed. It'll even say it'll do it during quiet hours but often it just doesn't do it. Same problem I find with macOS. I'm told it'll install updates overnight, fine go ahead and do that I leave my device on all the time. However, when I come to use my laptop the next morning I find it hasn't performed the update. Is it because when I finish using my device I close the lid? Maybe, but the OS isn't a doing a good job of telling me exactly how I should leave my device if it's pending an update.<br><br>

Anyway I'm ranting a little and I'm talking about Windows today. I wanted to automate Windows updates for my team without spending a penny or subscribing to services such as InTune. I decided that PowerShell should be able to achieve this.<br><br>

I created a script which needs to be sensibly stored on the network somewhere. You can call it whatever you want, I went with `installWindowsUpdateModule.ps1`.

<br><br>

```powershell
Write-Host "Windows Update process started. Your device may require an immediate restart shortly"
Write-Host "Please stand by..."

# Checks if the NuGet package exists on the deivce, if it doesn't it'll force install the minimum version
if (Get-PackageProvider -ListAvailable -Name NuGet) {
    Write-Host "NuGet package provider exists, moving on to next step"
}
else {
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Write-Host "NuGet package provider has now been installed"
}

# Installs the PSWindowsUpdate module if it doesn't exist
if (Get-Module -ListAvailable -Name PSWindowsUpdate) {
    Write-Host "PSWindowsUpdate module exists, moving on to next step"
}
else {
    Install-Module PSWindowsUpdate -Force
    Add-WUServiceManager -MicrosoftUpdate -Force
    Write-Host "PSWindowsUpdate module has now been installed"
}

# Creates a folder on the local C:\ drive if it does not exist
$folderName = "C:\UpdateLogs\"
if (Test-Path $folderName) {
    Write-Host "C:\UpdateLogs\ folder exists, moving on to next step"
}
else {
    New-Item $folderName -ItemType Directory
    Write-Host "Folder created"
}

Write-Host "Checking for and installing any available Windows updates"
Install-WindowsUpdate -MicrosoftUpdate -AcceptAll -AutoReboot | Out-File "C:\UpdateLogs\$env:computername-$(Get-Date -f yyyy-MM-dd)-MSUpdates.log" -Force
```
<br><br>

Let me explain what this script is doing. It'll first show a message to the user if they happen to be using the PC when the script kicks in.<br><br>

It'll then check if NuGet is installed, this is a package that's required to have PowerShell check for new available updates, if it already exists it'll skip past it otherwise it'll get installed once.<br><br>

Another package called PSWindowsUpdate is checked and installed.<br><br>

Next the script will create a folder on the C:\ drive called `UpdateLogs`, once the script has run I want a simple notepad doc to create a log of any updates it's downloading and installing.<br><br>

With all the packages and directories checked or created the final part of the script will install any outstanding Windows updates, write those updates to a log for checking later and then reboot the computer.<br><br>

Nice and simple, just remember to save any work before you finish for the day because this script doesn't check for that.

## Schedule

To automate this I wanted to have it run on a scheduled task on a group policy for my team. Head to the Group Policy Management Editor and go to User Configuration > Preferences > Control Panel Settings > Scheduled Tasks. Right-click that and click on New > Scheduled Task.<br><br>

<img src="/powershell-windows-updates/SCR-20250307-jmyp-optimized.png" alt=""><br><br>

I set this as an Update action and to run using the `NT AUTHORITY\System` user. Select "Run whether user is logged on or not".<br><br>

<img src="/powershell-windows-updates/SCR-20250307-jmkh-optimized.png" alt=""><br><br>

On the Triggers tab you can create the sort of schedule you want this to run. I run ours well after the office has closed as the PCs are usually left on anyway.<br><br>

<img src="/powershell-windows-updates/SCR-20250307-jmlr-optimized.png" alt=""><br><br>

<img src="/powershell-windows-updates/SCR-20250307-jmnd-optimized.png" alt=""><br><br>

Under the Actions tab you'll want to select "Start a program". This next bit is important, you need to have it execute PowerShell and put in an argument so it'll execute your script.<br><br>

<img src="/powershell-windows-updates/SCR-20250307-jmhq-optimized.png" alt=""><br><br>

For most Windows setups you'll set this is the program path.<br><br>

`C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`

Then in the "Add arguments" box input:<br><br>

```powershell
-ExecutionPolicy Bypass -command "&amp; C:\PowerShellScripts\installWindowsUpdateModule.ps1"
```

<br><br>

The remaining tabs I've left blank. Once you've set this it's good to go. When the script has run a few times depending on your own set schedule you can check to see if it's created a logs folder with a log file within to read.<br><br>

A log will be crested each time the script runs and they only create a couple of KB so storage won't be an issue here.<br><br>

<img src="/powershell-windows-updates/SCR-20250307-jnrv-optimized.png" alt=""><br><br>

If there's no update a script is still generated but there will be nothing within it. Perhaps it could be improved to not generate at all but that's for another day.
