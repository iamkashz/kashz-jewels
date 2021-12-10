# port forwarding

## meterpreter port forwarding:

```bash
portfwd list
portfwd [add | delete] -l LOCAL_PORT -p TARGET_PORT -r TARGET_IP
portfwd flush # to remove all port-forwarding
```

## ssh port forwarding:

* `-f`: background shell, to give shell back
* `-N`: only setup connect, no commands are to be run

### Forward connections (outgoing)

```bash
# for connecting to remote port via localhost (-L) (outgoing)
ssh -L KALI-IP:KALI-PORT:localhost:TARGET-PORT TARGET-USER@TARGET-IP
```

### Reverse connections (incoming)

#### authorized_keys file

```bash
from="IP",command="echo 'This account can only be used for Port Forwarding'",no-agent-forwarding,no-X11-forwarding,no-pty <SSH-PUBLIC-key>
```

#### Command

```bash
# for allowing a connecting to your port from outside (incoming)
ssh -fN -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" -R KALI-IP:KALI-PORT:localhost:TARGET-PORT -i <id_rsa> KALI-USER@KALI-IP

# -N: not running commands
# -f: go to background
# UserKnownHostsFile=/dev/null & StrictHostKeyChecking=no will not ask kali password; not safe to enter password on target.
```

## chisel port forwarding

### Remote Port Forward

```bash
# server on kali
chisel server -p 8000 --reverse

# client on target
chisel client KALI_IP:8000 R:KALI_LISTENING_PORT:TARGET_IP:TARGET_PORT_FORWARD [-v]
ex. chisel.exe client 10.10.16.161:9000 R:8989:127.0.0.1:8888
# chisel server is 10.10.16.161:9000
# any requests to kali:8989 ==> target:8888
```

### Local Port Forward

```bash
# server on target
chisel server -p 8000

# client on kali
chisel client TARGET_IP:8000 KALI_PORT:TARGET_IP:TARGET_PORT [-v]
```

* [0xdf's guide to using chisel](https://0xdf.gitlab.io/2020/08/10/tunneling-with-chisel-and-ssf-update.html)

## plink.exe

```bash
# /usr/share/windows-binaries/plink.exe
plink.exe kashz@IP -R <remote-port>:localhost:<local-port>
```

## socat port forwarding

```bash
# listen on PORT1,bind to IP1 and route to IP2:PORT2
socat tcp-l:PORT1,fork,reuseaddr,bind=IP1 tcp:IP2:PORT2
```

## Socket Check:

```bash
ss FLAG
```

| flag | description              |
| ---- | ------------------------ |
| -t   | TCP sockets              |
| -u   | UDP sockets              |
| -l   | Listening sockets only   |
| -p   | Process using the socket |
| -n   | No DNS resolution        |
