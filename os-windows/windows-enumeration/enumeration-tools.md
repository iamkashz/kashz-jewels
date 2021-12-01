# enumeration tools

## Accesschk.exe

```bash
> accesschk.exe /accepteula -flag [FLAG]
# -u: suppress errors | -q: quiet; no banner | -v: verbose

# -w: write access objects only
# -c: windows service <>
# -d: directory <>
# -k: registry key <>
```

## icacls

```bash
> icacls [FILE|DIR] [FLAG]
# /T - traverse all dir and files within the folder
# /grant USER:PERM
# /setowner USER
```

## wmic

Enumeration Script for
wmic: [fuzzysecurity.com/tutorials/wmic_info.rar](http://www.fuzzysecurity.com/tutorials/files/wmic_info.rar)

## Service Cmds

```bash
# configuration of service
> sc.exe qc SERVICE

# status of service
> sc.exe query SERVICE

# modify config
> sc.exe config SERVICE <key>= <value>

# start / stop / restart
> net [start/stop] SERVICE
> sc [start/stop] SERVICE
PS> Restart-Service -Name SERVICE

# is exe running with admin?
> tasklist /V | findstr FILE.exe
```
