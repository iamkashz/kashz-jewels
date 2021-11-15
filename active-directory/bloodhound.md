# bloodhound

## Collectors

* [SharpHound.exe](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.exe)
* [SharpHound.ps1](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1)

## Usage

```bash
# run powershell -ep bypass;. .\SharpHound.ps1
Invoke-Bloodhound -CollectionMethod All -Domain DOMAIN -ZipFileName DOMAIN.zip
```