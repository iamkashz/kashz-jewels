# bloodhound

## Collectors

* [SharpHound.exe](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.exe)
* [SharpHound.ps1](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1)

## Usage

### SharpHound.ps1 | SharpHound.exe

```bash
# run powershell -ep bypass;
. .\SharpHound.ps1
Invoke-Bloodhound -CollectionMethod All -Domain DOMAIN -ZipFileName DOMAIN.zip -LDAPUser USER -LDAPPass PASS [-CollectAllProperties]

.\SharpHound.exe -c All -d DOMAIN --zipfilename DOMAIN.zip --ldapusername USER --ldappassword PASS [--collectallproperties]
```

### bloodhound-python

```bash
bloodhound-python -c all --zip -u USER -p PASS -d DOMAIN -ns IP [-dc DOMAIN_CONTROLLER] [-gc GLOBAL_CATALOG_IP]
```