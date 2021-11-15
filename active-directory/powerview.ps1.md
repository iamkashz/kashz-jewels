# powerview.ps1

* [PowerView.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1)

```bash
powershell.exe -exec bypass; Import-Module PowerView.ps1
[OR] . .\PowerView.ps1
```

## Domain information

```bash
Get-NetDomain
Get-NetDomainController [-Domain DOMAIN]
Get-DomainSID
Get-DomainPolicy
  (Get-DomainPolicy)."to-enumerate-further"
```

## Domain Users & Computers

```bash
Get-NetUser | select samaccountname,userprincipalname, memberof
Get-NetUser * -Domain DOMAIN | Select-Object -Property name,samaccountname,description,memberof,admincount,userprincipalname, serviceprincipalname, useraccountcontrol
Get-UserProperty [-Properties FIELD]

Get-NetComputer [-FullData] [| select ]
```

### Kerberoastable Users

```bash
Get-NetUser -SPN | select serviceprincipalname
Get-DomainUser * -SPN | Get-DomainSPNTicket -OutputFormat Hashcat
```

## Domain Groups

```bash
# can use *admin*
Get-NetGroup [-GroupName "GROUPNAME"]
Get-NetGroupMember [-GroupName "GROUPNAME"]
```

## SMB Shares

```bash
Invoke-ShareFinder
```

## GPO
```bash
Get-NetGPO [| select displayname]
```

## References

* [https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands](https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands)
* [https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)