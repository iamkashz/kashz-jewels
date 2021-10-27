# port forwarding

## Using ssh:

### Outgoing

```bash
# for connecting to remote port via localhost (-L) (outgoing)
ssh -L KALI-IP:KALI-PORT:localhost:TARGET-PORT TARGET-USER@TARGET-IP
```

### Incoming

#### authorized_keys file

```bash
from="IP",command="echo 'This account can only be used for Port Forwarding'",no-agent-forwarding,no-X11-forwarding,no-pty <SSH-PUBLIC-key>
```

#### Command

```bash
# for allowing a connecting to your port from outside (incoming)
ssh -N -f -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no"-R KALI-IP:KALI-PORT:localhost:TARGET-PORT -i <id_rsa> KALI-USER@KALI-IP

# -N: not running commands
# -f: go to background
# UserKnownHostsFile=/dev/null & StrictHostKeyChecking=no will not ask kali password; not safe to enter password on target.
```

## [chisel](https://github.com/jpillora/chisel/releases/tag/v1.7.6)

```bash
# server
chisel server -p 8000 --reverse

# client
chisel client <kali-ip>:8000 R:<listen-on-port>:<target-ip><target-ip-port-forward>
ex. chisel.exe client -v 10.10.16.161:9000 R:8989:127.0.0.1:8888
# chisel server is 10.10.16.161:9000
# any requests to kali:8989 ==> target:8888
```

## plink.exe

```bash
# /usr/share/windows-binaries/plink.exe
plink.exe kashz@<IP> -R <remote-port>:localhost:<local-port>
```

## socat re-route inside kali

```bash
# listen on 3306 from tun0 IP and route to localhost:3306
$ socat TCP-LISTEN:3306,fork,bind=10.10.16.161 TCP:127.0.0.1:3306
```

## Socket Check:

```bash
ss <flag>
```

| flag | description              |
| ---- | ------------------------ |
| -t   | TCP sockets              |
| -u   | UDP sockets              |
| -l   | Listening sockets only   |
| -p   | Process using the socket |
| -n   | No DNS resolution        |
