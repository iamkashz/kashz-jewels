# group policy management

## Disable Windows Defender

1. Start > (right-click) Group Policy Management > Run as Administrator
2. Under Forest, Domains > (right-click) DOMAIN >  Create GPO in this domain and link it here.
3. set NAME: `Disable Windows Defender`
4. Under Forest, Domains > DOMAIN > (right-click) Disable Windows Defender > Edit
5. Computer Configuration > Policies > Administrative Templates > Windows Components > Windows Defender Antivirus
6. Select `Turn off Windows Defender Antivirus` > Enabled > Apply > OK

Check `Windows Defender SmartScreen` & `Windows Defender ExploitGuard`.

### Enforce Policy

1. Under Forest, Domains > DOMAIN > Select the Policy
2. (right-click) Enforced column > Enable it.

## Cached Group Policy Preferences Creds (ms14-025)

### Check using msf

* `use auxiliary/scanner/smb/smb_enum_gpp`
* `use post/windows/gather/credentials/gpp`

### Manual

Use `PowerUp.ps1`.

1. File path
   1. `C:\ProgramData\Microsoft\Group Policy\History\{UUID-DIRECTORY}\Machine\Preferences\Groups\Groups.xml`
   2. `\Policies\{UUID-DIRECTORY}\MACHINE\Preferences\Groups\Groups.xml`
2. in kali `gpp-decrypt HASH`

* [rapid7.com/blog/pentesting-in-the-real-world-group-policy-pwnage/](https://www.rapid7.com/blog/post/2016/07/27/pentesting-in-the-real-world-group-policy-pwnage/)
* [hackingarticles.in/credential-dumping-group-policy-preferences-gpp/](https://www.hackingarticles.in/credential-dumping-group-policy-preferences-gpp/)

## Fix

* Disable LLMNR
  | [blackhillsinfosec.com/how-to-disable-llmnr-why-you-want-to/](https://www.blackhillsinfosec.com/how-to-disable-llmnr-why-you-want-to/)
* if cannot
    * Require Network Access Control
    * Require strong user passwords1