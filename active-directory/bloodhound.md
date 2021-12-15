# bloodhound

## Collectors

* [SharpHound.exe](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.exe)
* [SharpHound.ps1](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1)
* [bloodhound-python](https://github.com/fox-it/BloodHound.py)

## Usage

### using bloodhound-python

```bash
bloodhound-python -c all --zip -u USER -p PASS -d DOMAIN -ns IP
```

### using SharpHound.ps1

```bash
# run powershell -ep bypass;
. .\SharpHound.ps1
Invoke-Bloodhound -CollectionMethod All -Domain DOMAIN -ZipFileName DOMAIN.zip -LDAPUser USER -LDAPPass PASS [-CollectAllProperties]
```

### using SharpHound.exe

```bash
.\SharpHound.exe -c All -d DOMAIN [--domaincontroller DOMAIN_IP] --zipfilename DOMAIN.zip --ldapusername USER --ldappassword PASS [--collectallproperties]
--OutputDirectory PATH
```