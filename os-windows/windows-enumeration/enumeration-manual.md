# enumeration manual

## Basic checks

```bash
# users enum
> net user | net user <USER>
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
> wmic service 'name like "%KEYWORD%"' get name
```

## Firewall

```bash
# open a PORT
netsh advfirewall firewall add rule name="NAME" dir=in action=allow protocol=tcp localport=PORT

> sc query windefend
> netsh firewall show state
> netsh firewall show config
> netsh advfirewall firewall dump
> netsh advfirewall show [currentprofile | allprofiles]
> netsh advfirewall show rule [all | name=all]

# turn off firewall
> netsh firewall set opmode disable
> netsh advfirewall set allprofiles state off

# using PS (run all in one go)
Set-MpPreference -DisableRealtimeMonitoring $true
Set-MpPreference -DisableRemovableDriveScanning $true
Set-MpPreference -DisableArchiveScanning $true
Set-MpPreference -DisableAutoExclusions $true
Set-MpPreference -DisableBehaviorMonitoring $true
Set-MpPreference -DisableBlockAtFirstSeen $true
Set-MpPreference -DisableCatchupFullScan $true
Set-MpPreference -DisableCatchupQuickScan $true
Set-MpPreference -DisableEmailScanning $true
Set-MpPreference -DisableIntrusionPreventionSystem $true
Set-MpPreference -DisableIOAVProtection $true
Set-MpPreference -DisablePrivacyMode $true
Set-MpPreference -DisableRealtimeMonitoring $true
Set-MpPreference -DisableRemovableDriveScanning $true
Set-MpPreference -DisableRestorePoint $true
Set-MpPreference -DisableScanningMappedNetworkDrivesForFullScan $true
Set-MpPreference -DisableScanningNetworkFiles $true
Set-MpPreference -DisableScriptScanning $true

# enable ICMP
netsh advfirewall firewall add rule name="ICMP Allow incoming V4 echo request" protocol=icmpv4:8,any dir=in action=allow
netsh advfirewall firewall add rule name="ICMP Allow incoming V6 echo request" protocol=icmpv6:8,any dir=in action=allow

# disable across AD
Set-NetFirewallProfile -Profile Domain, Public, Private -Enabled False
```

## Installed Applications

* [jaapbrasser/SharedScripts/Get-RemoteProgram.ps1](https://github.com/jaapbrasser/SharedScripts/blob/master/Get-RemoteProgram/Get-RemoteProgram.ps1)

```bash
> powershell.exe -exec bypass -Command "& {Import-Module .\Get-RemoteProgram.ps1; Get-RemoteProgram}"
# [OR]
> wmic product get name,version
```

## Scheduled Tasks

* [jaapbrasser/SharedScripts/Get-ScheduledTask.ps1](https://github.com/jaapbrasser/SharedScripts/blob/master/Get-ScheduledTask/Get-ScheduledTask.ps1)

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
