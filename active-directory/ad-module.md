# ad module

* [samratashok/ADModule](https://github.com/samratashok/ADModule)

```bash
Import-Module Import-Module Microsoft.ActiveDirectory.Management.dll -Verbose
Import-Module ActiveDirectory.psd1
Get-Command -Module ActiveDirectory

[OR] . .\Import-ActiveDirectory.ps1
```

## Domain information

```bash
Get-Domain [-Domain DOMAIN]
Get-DomainController [-Domain DOMAIN] 
Get-DomainSID
Get-DomainPolicy
(Get-DomainPolicy)."to-enumerate-further"
```

## Domain Users & Computers

```bash
Get-DomainUser | Out-File -FilePath .\DomainUsers.txt
Get-DomainUser | select samaccountname,userprincipalname, memberof
Get-DomainUser * -Domain DOMAIN | Select-Object -Property name,samaccountname,description,memberof,admincount,userprincipalname, serviceprincipalname, useraccountcontrol
Get-UserProperty [-Properties FIELD]

Get-DomainComputer -Properties OperatingSystem, Name, DnsHostName | Sort-Object -Property DnsHostName
# live hosts
Get-DomainComputer -Ping -Properties OperatingSystem, Name, DnsHostName | Sort-Object -Property DnsHostName
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
Invoke-ShareFinder [-CheckShareAccess]
```

## GPO

```bash
Get-NetGPO [| select displayname]
Get-DomainGPOLocalGroup | Select-Object GPODisplayName, GroupName
```

## ACLs

```bash
# Returns the ACLs associated with the specified account
Get-DomaiObjectAcl -Identity <AccountName> -ResolveGUIDs

#Search for interesting ACEs
Find-InterestingDomainAcl -ResolveGUIDs

#Check the ACLs associated with a specified path (e.g smb share)
Get-PathAcl -Path "\\Path\Of\A\Share"
```

## Domain Trusts

```bash
Get-DomainTrust
Get-DomainTrust -Domain <DomainName>

#Enumerate all trusts for the current domain and then enumerates all trusts for each domain it finds
Get-DomainTrustMapping
```

## User Hunting

```bash
#Finds all machines on the current domain where the current user has local admin access
Find-LocalAdminAccess -Verbose

#Find local admins on all machines of the domain
Find-DomainLocalGroupMember -Verbose

#Find computers were a Domain Admin OR a spesified user has a session
Find-DomainUserLocation | Select-Object UserName, SessionFromName

#Confirming admin access
Test-AdminAccess
```

## References

* [https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands](https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands)
* [https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)