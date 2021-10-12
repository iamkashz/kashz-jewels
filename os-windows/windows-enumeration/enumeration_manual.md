# enumeration_manual

## Basic checks

```bash
# users enum
> net user [OR] net user <USER>
> net localgroup adminstrators
PS> $env:UserName | $env:UserDomain | $env:ComputerName
PS> [System.Security.Principal.WindowsIdentity]::GetCurrent().Name

# network information
> arp -A
> netstat -ano
> route print

# find keyword in files
> findstr /si "password" *.xml *.ini *.txt
# find file
> dir /b /s "FILE"

# schedule shutdown
> shutdown /r -t <seconds>
# abort shutdown
> shutdown -a
```

## Running services

```bash
> netstat -anop tcp | find "PROCESS-NAME"
> tasklist / SVC
> tasklist | find "PID"
> wmic service get name,displayname,pathname,startmode | findstr /i /v "C:\Windows\\" |findstr /i /v """
> wmic product get name,version
```

## Firewall

```bash
> sc query windefend
> netsh firewall show state
> netsh firewall show config
> netsh advfirewall firewall dump
> netsh advfirewall show [currentprofile | allprofiles]
> netsh advfirewall show rule [all | name=all]

# turn off firewall
> netsh firewall set opmode disable
> netsh advfirewall set allprofiles state off
```

## Installed Applications

* [Get-RemoteProgram.ps1](https://github.com/jaapbrasser/SharedScripts/blob/master/Get-RemoteProgram/Get-RemoteProgram.ps1)

```bash
> powershell.exe -exec bypass -Command "& {Import-Module .\Get-RemoteProgram.ps1; Get-RemoteProgram}"
# [OR]
> wmic product get name,version
```

## Scheduled Tasks

* [Get-ScheduledTask.ps1](https://github.com/jaapbrasser/SharedScripts/blob/master/Get-ScheduledTask/Get-ScheduledTask.ps1)

```bash
> powershell.exe -exec bypass -Command ".\Get-ScheduledTask.ps1"
# [OR]
> schtasks /query /fo LIST /v
PS> Get-ScheduledTask | where {$_.TaskPath -notlike "\Microsoft*"} | ft TaskName,TaskPath,State
```

## Installed Patches

```bash
> wmic qfe list
```
