# office document analysis and exploitation

Any file with extension `.docm, .xlsm` etc is a macro embedded file

* [zeltser.com/analyzing-malicious-documents/](https://zeltser.com/analyzing-malicious-documents/)

## .xlsm

Using oletools, we can extract macro.

```bash
python3 -m pip3 install oletools
olevba FILE.xlsm
```

## .doc

Using Nishang Out-Word.ps1

**REQUIREMENT:**

* Needs payload
* Needs a Windows system to generate .doc
* [/samratashok/nishang/Out-Word.ps1](https://github.com/samratashok/nishang/blob/master/Client/Out-Word.ps1)

* NOTE: Need local MS Word installation. Need to disable Defender.

```bash
PS> . .\Out-Word.ps1
PS> Out-HTA -Payload "PS_ENCODED_PAYLOAD" -Outputfile FILLE.doc
# file will be saved in Documents
```

## Microsoft Exchange Email

* [dafthack/MailSniper](https://github.com/dafthack/MailSniper)

## MFA check

* [dafthack/MFASweep](https://github.com/dafthack/MFASweep)

## office365

* [blacklanternsecurity/TREVORspray](https://github.com/blacklanternsecurity/TREVORspray)

## OWA office webApp

* search on metasploit