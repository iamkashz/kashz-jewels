# enumeration tools

## Accesschk.exe

```bash
> accesschk.exe /accepteula -flag <name>
# -u: suppress errors | -q: quiet; no banner | -v: verbose

# -w: write access objects only
# -c: windows service <>
# -d: directory <>
# -k: registry key <>
```

## icacls

```bash
> icacls <FILE/DIR> [<flags>]
# /T - traverse all dir and files within the folder
# /grant <USER>:<PERM>
```

## wmic

Enumeration Script for wmic: [fuzzysecurity.com/tutorials/wmic_info.rar](http://www.fuzzysecurity.com/tutorials/files/wmic_info.rar)

## Service Cmds

```bash
# configuration of service
> sc.exe qc <service>

# status of service
> sc.exe query <service>

# modify config
> sc.exe config <service> <key>= <value>

# start / stop / restart
> net [start/stop] <service>
> sc [start/stop] <service>
PS> Restart-Service -Name <service>

# is exe running with admin?
> tasklist /V | findstr <.exe>
```
