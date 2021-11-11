# AD enumeration

* [Kerbrute](https://github.com/ropnop/kerbrute/releases)
* [Rubeus](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/Rubeus.exe)
* [kekeo](https://github.com/gentilkiwi/kekeo)
* [Bloodhound](https://github.com/BloodHoundAD/BloodHound/releases)
* [SharpHound.exe](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.exe)
* [SharpHound.ps1](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1)
* [Invoke-Kerberoast.ps1](https://github.com/EmpireProject/Empire/blob/master/data/module\_source/credentials/Invoke-Kerberoast.ps1)

```powershell
Invoke-Bloodhound -CollectionMethod All -Domain DOMAIN -ZipFileName DOMAIN.zip
```

## Cached Group Policy Preferences Creds

Use `PowerUp.ps1`.

1. File path: `C:\ProgramData\Microsoft\Group Policy\History\{UUID-DIRECTORY}}\Machine\Preferences\Groups\Groups.xml`
2. in kali `gpp-decrypt HASH`

* [hackingarticles.in/credential-dumping-group-policy-preferences-gpp/](https://www.hackingarticles.in/credential-dumping-group-policy-preferences-gpp/)