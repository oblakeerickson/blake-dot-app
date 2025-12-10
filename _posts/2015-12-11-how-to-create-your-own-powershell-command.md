---
layout: post
title:  "How To Create Your Own PowerShell Command"
date:   2015-12-11 01:00:00 -0600
---

I did it again. I created another subdomain for an application I'm working on and I can't get to it!

Now I have to start the very annoying process of opening up Notepad.exe in Administrator mode and try to remember where my hosts file is then change the file extension picker to "all files" so that I can actually see my hosts file. Once I finally have the file open I then I have to type in the full ip address and subdomain. Once I save the file I'm still not done by the way because I still have to open up IIS Manager and find where I need to add a new binding to my local website and add it there. Ohh by the way now I'm really annoyed and totally forgot what I was working on.

Ever find yourself in a similar situation? To end my frustration I made a simple PowerShell command (my very first one) to do all that manual work for me.

For a real quick summary of what you need to do to create a new PowerShell command you can follow these steps which I'll walk you through:

1. Open PowerShell ISE
2. Save file as command.psm1
3. Create Function
4. Export-ModuleMember
5. Add Import-Module to profile
6. Profit

## Create a PowerShell Module

Normal PowerShell Scripts live in `.ps1` files, but PowerShell modules live in `.psm1` files, so we need to make one of those. Go ahead and open up PowerShell ISE. I'll be honest, I didn't know this existed, but it is a very handy editor for writing PowerShell scripts. Once it opens it will have a new unsaved file open for you so the first thing you should do is go to 'File -> Save As' and save it with a cool name and a `.psm1` extension.

## Write a function

Now we need to create a new function and give it a "Verb-Noun" name. I also added the $SubDomain parameter that we can pass in. Inside of the function I added the PowerShell commands that I want to be executed. At the end of our file add a line for exporting our new function as a module.

```
function New-Binding($SubDomain) {

    ## Add Binding to IIS
    [string]$FullSubDomain = $SubDomain + ".yourdomain.local"
    New-WebBinding -Name "YourSite.Name" -IPAddress "*" -Port 80 -HostHeader $FullSubDomain

    ## Add to hosts file
    [string]$HostsEntry = "127.0.0.1    " + $FullSubDomain
    Add-Content C:\Windows\System32\drivers\etc\hosts $HostsEntry

    Write-Host "Created Binding for: " $FullSubDomain
}

Export-ModuleMember -Function 'New-Binding'
```

Now that we have our function written we can save and close PowerShell ISE.

## Import the Module

Before we can use the module we need to import it so that PowerShell can access our new command. To import our module we need to open up our PowerShell profile. You can find out where your PowerShell profile is by typing `$profile` inside of PowerShell. You can easily open up your profile by typing `notepad $profile`

Once your have your profile open add this line to it:

```
Import-Module "C:\code\powershell\NewBinding.psm1" -force
```

## Run the command

Now if you re-open PowerShell as Administrator your new module will be imported and we can type our new command!

What else can you automate?
