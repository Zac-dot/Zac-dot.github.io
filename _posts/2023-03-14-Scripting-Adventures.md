---
tags: PowerShell AutoHotkey Coding
layout: post
title: Scripting Adventures
date created: March 14th 2023
date modified: March 14th 2023
---

> Yeah to note, this does have some experiences tied in with each thing

# Scripting Adventures

So recently when I haven't be preoccupied with classes, part of what I have been doing has been trying to find ways to automate different tasks plus finding ways to get to applications or started quicker. What this led me down was a rabbit hole that involved looking at various ways to script functions, eventually leading me to make a few scripts that help with things I don't normally want to deal with.

## Finding How to Script

The first step of scripting came down to exactly what did I want to use to automate things, and if it involved typing out code or simply dragging and dropping things. There are a couple different things that could be used that I came across, these being…

### 1. [Windows Power Automate](https://powerautomate.microsoft.com/en-us/)

An interesting solution, and is mostly oriented towards automating different websites and apps that aren't local. There are two versions, however, with one being oriented for local devices that is [downloadable through the Microsoft Store](https://apps.microsoft.com/store/detail/power-automate/9NFTCH6J7FHV) and the other being more focused on cloud automations such as connecting Gmail with Forms.

The local, installable version is the one I would focus on, however I quickly did not come to like Windows Power Automate. The main problem is that I am not big on drag and drop interfaces, and that paired with some clunkiness of the Metro / Fluent design that Microsoft is attempting here, it comes across as being sluggish and difficult to use. Another issue was also the fact that attempting to automate a basic task, such as launching a website on a keypress, would constantly push Microsoft applications like Edge to display the site, despite Firefox being what is setup with the action. Lastly, the interface does allow the use of running Python scripts or other scripts on keypress, but with added memory and battery usage of Power Automate, it is much better to use something else that will simply start the script on keypress. 

### 2. [IFTTT](https://ifttt.com/explore)

This was another option that was suggested, however, there is little to zero support for automating tasks for PCs with this--its mostly oriented towards automating connections between websites and mobile devices. The closest I got to being able to automate some tasks was through the use of [AssistantComputerControl](https://assistantcomputercontrol.com/), but due to recent infrastructure changes, it would not work using the IFTTT recipes and software installed.

### 3. [AutoHotkey](https://www.autohotkey.com/)

This was something I also explored alongside Power Automate, but the main catch it was typed out in a dedicated file (ending with a .ahk) and you could use either a text editor with plugin, or simply notepad. The documentation has some QuickStart guides that proved useful, and as I have some previous coding experience, were easy to follow as the syntax mimics a mix between Python and C++. 

Interestingly, you can simply have the file run at startup and it will listen for specific keypresses, or key combos, and it would do tasks based on that. While that does come with the potential issue of effectively a keylogger watching your every move, if you aren't handling sensitive data or the AutoHotkey file your using isn't logging keypresses then you should be alright. But the main idea of the paragraph is that you would not need to code any extra lines into the file, or to add a specific case to the file in order for it to run, just would need to be in the background.

### 4. A Dedicated Scripting Language

An example of a dedicated scripting language would be something like Python, PowerShell, JavaScript, and so forth. Each of these languages can be used to write or do tasks on your behalf in the background, albeit with the correct coding experience or documentation available. This also opens the potential to making a lot more complex automated scripts, as each language can use packages or imported libraires to help expand on things. For example, you could setup Python to display a prompt to send to ChatGPT to create dialog from, and simply paste the generated dialog into a document that is being worked on. There is a lot of different things possible depending on what you want to automate using these languages. 

AutoHotkey *would* be considered a script language, but given what defines a script language specifically it does not match up with what an actual scripting language is.

## Automating and Scripting

While at first I explored using Microsoft Power Automate and IFTTT, I ultimately went with **AutoHotkey** and **PowerShell**. AutoHotkey was used for tasks that I wanted to happened based on a specific key combo being pressed, and Powershell being used for  tasks done in the background.

The sections below give more information on the scripts made and functions they serve. This also serves as a backup personally in case something happens to them over time.

## Powershell

One of the very first things I ended up automating was updating installed applications weekly through the use of Chocolatey. If you don't know what that is, Chocolatey acts as a package manager that can pull from a community repository and install them in the background--In essence it mimics what App repos on Linux do on Windows.

### Powershell -- Auto-updater

There are two parts to setting up these scripts: The script itself, plus an entry added into  Task Scheduler

#### chocoauto.ps1

```PowerShell

# This script automatically updates all installed packages using Chocolatey package manager

# Check if Chocolatey is installed, else installs if not
if (!(Test-Path -Path "C:\ProgramData\chocolatey\bin\choco.exe")) {
  Write-Host "Chocolatey is not installed. Installing Chocolatey..."
  Set-ExecutionPolicy Bypass -Scope Process -Force
  iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
}

# Update all installed packages
Write-Host "Updating all installed packages..."
choco upgrade all -y

# Display update summary
$updates = choco outdated
if ($updates) {
  Write-Host "The following packages are outdated and have not been updated:"
  Write-Host $updates
} else {
  Write-Host "All packages are up to date."
}
```

**Note**: while running the script in the console would display the information to console, running it in the background will not have the information displayed anywhere. 

#### Task Scheduler Entry for chocoauto.ps1

The script can be ran standalone from a Powershell window, but using Task Scheduler I was able to have it run silently in the background every Monday at 10am.

Using the 'Create task…' button, in each tab I did:
- General:
	- 'Run whether user is logged on'
	- 'Do not store password'
	- 'Run with highest privileges' - **IMPORTANT, will not be able to update packages elsewise**
- Triggers:
	- On a schedule, Weekly, Starting on (todays date), recuring every 1 week(s)
	- 'Delay task for up to (random delay)' of 1 minute
- Actions:
	- Start a Program
	- In 'Program/script' point it at a specific PowerShell installation or to use the built in one just put 'powershell.exe'
	- In arguments put:
		- If you don't want a PowerShell window to briefly appear:
			- ```-windowstyle hidden -File "location\to\file"```
		- Else:
		- ```"Location\to\file"```
- Conditions:
	- Idle - 'Start the task only if computer is idle for: 5 minutes'
	- Power - 'Start the task only if the computer is on AC power' and 'Stop if the computer switches to battery power'

### Powershell -- Autosorter

Another script that I ended up writing was an Autosorter. In essence, I could throw files into a single folder and every hour it will check and automatically sort the files into specific folders according to what file extension they are (IE: .doc goes into Documents)

The script is as follows, with an entry placed into Task Scheduler as well for the file

#### autosorter.ps1

```PowerShell
# Set the source and destination folders
# Change 'user' to match your Windows username, and change the directory between the "" to where you want specific files to go
$sourceFolder = "C:\Users\user\Desktop\Autosorter"
$imageDestination = "C:\Users\user\Pictures"
$docDestination = "C:\Users\user\Documents"
$pdfDestination = "C:\Users\user\Documents\PDFs"
$vidDestination = "C:\Users\user\Videos"
$otherDestination = "C:\Users\user\Unsorted"

# Get all the files in the source folder
$files = Get-ChildItem $sourceFolder -File

# Loop through each file and move it to the appropriate destination folder based on its file type
foreach ($file in $files) {
    if ($file.Extension -match "\.(jpg|png|gif)$") {
        Move-Item $file.FullName $imageDestination
    } elseif ($file.Extension -match "\.(doc|docx|txt)$") {
        Move-Item $file.FullName $docDestination
    } elseif ($file.Extension -match "\.(pdf)$"){
        Move-Item $file.FullName $pdfDestination
    } elseif ($file.Extension -match "\.(mov|mp4|webm|srt)$"){
        Move-Item $file.FullName $vidDestination
    } else {
        Move-Item $file.FullName $otherDestination
    }
}
```

#### Task Scheduler Entry for autosorter.ps1

Again, you can manually run the script but that defeats the purpose, so I have it run hourly so it will auto sort things on the go

Using the 'Create task…' button, in each tab I did:
- General:
	- 'Run whether user is logged on or not'
	- 'Do not store password'
- Trigger:
	- On a schedule, Daily, recuring every 1 day(s)
	- 'Repeat task every:' 1 hour ' for a duration of:' 1 day
- Actions:
	- 'Start a program'
	-  In 'Program/script' point it at a specific PowerShell installation or to use the built in one just put 'powershell.exe'
	- In arguments put:
		- If you don't want a PowerShell window to briefly appear:
			- ```-windowstyle hidden -File "location\to\file"```
		- Else:
		- ```"Location\to\file"```

## AutoHotkey

So AutoHotkey programs are a bit differently done than say using PowerShell and Task Scheduler to do this. Firstly you will need to install AutoHotkey from the site, or through chocolatey, etc. and then you will need to right click and create a file ending with '.ahk'

From here you can either open the file in an IDE or file editor with the ability to format AutoHotkey files, or simply use Notepad (Of which I used to quickly make these). The code for these can either be done in separate files or done as one singular, depending on your taste.

**Note:** once your file is done, you will need to place the file in the 'Startup' folder if you want to be able to run tasks from computer startup, else you will need to run the file by clicking on it.

### AutoHotkey -- Application Starter

A simple code that I used to start an application via keypress, and if it ran just to maximize it. Change '^!f' to match the key-combo you would like

This example will open Firefox

```AutoHotkey
;Launches firefox
^!f::
;Ctrl + alt + f, mainly since no program uses this key combo normally
if WinExist("ahk_exe firefox.exe"){
	WinActivate ;
} else {
	Run, C:\Program Files\Mozilla Firefox\firefox.exe
}
return
```

The other I use is to open up Obsidian (Markdown editor)

```AutoHotkey
^!o:: ;Ctrl + alt + O will open Obsidian
if WinExist("ahk_exe Obsidian.exe"){
	WinActivate ;
} else {
	Run, C:\Users\User\AppData\Local\Obsidian\Obsidian.exe
}
return
```

### AutoHotkey - Specific Use (RA Magic Sentence)

One interesting use of AutoHotkey was the ability to write a magic sentence for use as an RA while I am going to school. The idea is that when I want to get started, instead of copy / pasting the template, I can press the keycombo and it will paste in the sentence with some information filled out. There are two versions of this, one of which uses a GUI in order to have anyone fill out information as needed.

The first just uses the keypress of ```Ctrl + m``` to copy and paste it, with todays date and current time

```AutoHotkey
^m::   ;Ctrl + ' will paste the magic sentence pre-filled out
;Gets the time
FormatTime, TodaysDate
;Formats to match sentence needs
FormatTime, ThisDate, TodaysDate, dddd MMMM dd, yyyy
FormatTime, ThisTime, TodaysDate, h:mm tt
SendRaw, On %ThisDate% at approximately %ThisTime%, 
Send, {Space}
SendRaw, Resident Assistant (Full Name) was doing (what occurred to make staff member confront) in (Hall name) hall when (building & room where it occurred)
return
```

The other example uses a GUI that will ask Date, Time, Who was on duty, the hall, and if you want PoV to be in first. This is more useful than the other if writing about problems or incidents that happened in the past. Given the UI, and the fact there is data to be saved, the code is a bit more complex.

The way to activate this one is built off the keypress of the last but includes ```Alt``` making the full key combo ```Ctrl + Alt + M```.

```AutoHotkey
^!m::  ;;More control over the sentence
;; ctrl + alt + m
;;This all controls the window that will show upon pressing
Gui, New,,Magic Sentence
Gui, Add, Text,, Select the date:
Gui, Add, DateTime, vLongDateVariable w250, LongDate

Gui, Add, Text,, Select the time:
Gui, Add, DateTime, vTheActualTime w250, Time

Gui, Add, Text,, Who was on duty (Full Name)?:
Gui, Add, Edit, r1 vDutyVar w250, Xander Thompson

Gui, Add, Text,, Which hall?:
Gui, Add, Edit, r1 vHall w250, Barto

Gui, Add, Text,, Point of View (Default: 3rd)
Gui, Add, CheckBox, v1stPerson, 1st Person View

Gui, Add, Button, Default w250, OK
Gui, Show
return


ButtonOK:
GuiControlGet, TheActualTime
GuiControlGet, LongDateVariable
Gui, Submit

FormatTime, ThisDate, %LongDateVariable%, dddd MMMM dd, yyyy
FormatTime, ThisTime, %TheActualTime%, h:mm tt

SendRaw, On %ThisDate% at approximately %ThisTime%
Send, {Space}
SendRaw, Resident Assistant %DutyVar% was doing (what occurred to make you confront) in %Hall% hall when (area it occurred and so forth)

if (1stPerson > 0){
Send, {Enter}{Enter}{Space}
SendRaw, This is RA %DutyVar%'s first person account of what happened:
}
Gui, Destroy
return

GuiClose:
Gui, Destroy
return
```

## Concluding

There are a multitude of ways to help speed up automating things in the background and through different keyboard shortcuts. While for some its better to use a scripting language or specifically type out things, such as I did with AutoHotkey and PowerShell, for others there are drag and drop options depending on what you are wanting to do. On the page are some examples of different automations that I personally use, and from here you can then use these to help with your workflow or to build off of and create an even more efficient way of doing things for yourself.
