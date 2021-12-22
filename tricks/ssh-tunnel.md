# SSH Tunnel

NOTE: needs valid SSH creds on box to pivot from.

## meterpreter tunnel

```bash
# to print existing routes 
autoroute -p

run autoroute [-s IP/CIDR]
[OR]
use post/multi/manage/autoroute
# use auxiliary/server/socks_proxy
```

## ssh tunnel:

### Forward tunnel (outgoing)

```bash
ssh user@IP -D PORT
# this sets up a tunnel between localhost:TUNNEL-PORT and target
# any requests to localhost:TUNNEL-PORT is routed via target
```

### Reverse tunnel (incoming)

#### authorized_keys file

```bash
from="IP",command="echo 'This account can only be used for Port Forwarding'",no-agent-forwarding,no-X11-forwarding,no-pty <SSH-PUBLIC-key>
```

#### Command

```bash
# for allowing a connecting to your port from outside (incoming)
ssh -fN -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" -R PORT -i <id_rsa> KALI-USER@KALI-IP

# -N: not running commands
# -f: go to background
# UserKnownHostsFile=/dev/null & StrictHostKeyChecking=no will not ask kali password; not safe to enter password on target.
```

## Proxychains

### /etc/proxychains4.conf

```bash
# add line for socks4/5 proxy 
[socks4|socks5] 127.0.0.1 6900

# comment out proxy_dns to avoid nmap hanging
```

Now, run any command using `$ proxychains4 [command]`

### proxychains4 for browser

Set up a foxyproxy configuration for browser:

1. Title: proxychains
2. Proxy Type: SOCKS4
3. Proxy IP: localhost
4. Port: 6900

## chisel tunnel

### Reverse socks proxy

NOTE: configure proxychains using `socks5 IP PORT`.

```bash
# server on kali
chisel server -p 8000 --reverse

# on target
# tunnel using chisel on kali:1080
chisel client KALI_IP:8000 R:socks
```

### Forward socks proxy

```bash
# server on target
chisel server -p 8000 --socks5

# on kali
chisel client TARGET_IP:8000 TUNNEL_PORT:socks
```

## sshuttle tunnel

* **REQUIREMENTS:**
    * Works only on linux targets
    * SSH access to target
    * Python on target (static binary works)

```bash
sshuttle -r USER@TARGET_IP [SUBNET/CIDR | -N] [--ssh-cmd "ssh -i KEY"] -x TARGET_IP
# -N: auto identify based on targers routing table
# -x: used to exclude current box from forward all subnet traffic
```