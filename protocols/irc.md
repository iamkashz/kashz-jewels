# irc

## Info

```bash
# sudo apt install pidgin

There are 2 kinds of IRC users:
1. Operators => need user:pass to connect to IRC
2. Users => only need nickname to connect to IRC
```

## Connect

1. launch pidgin
2. create a profile
3. to connect as user, any username (no password is needed) > connect
    1. view chats > join.
4. to connect as operator, username:password is needed.

## Recon

```bash
nmap --script irc-unrealircd-backdoor.nse -p PORT IP
```
