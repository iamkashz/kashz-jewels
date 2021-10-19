# SSH Tunnel

NOTE: needs valid SSH creds on box to pivot from.

## Tunnel configuration

```bash
ssh user@IP -D 6900
# this sets up a tunnel between localhost:TUNNEL-PORT and target
# any requests to localhost:TUNNEL-PORT is routed via target
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

