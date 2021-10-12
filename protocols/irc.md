# irc

## Info

```bash
# sudo apt install pidgin

There are 2 kinds of IRC users:
1. Operators => need user:pass to connect to IRC
2. Users => only need nickname to connect to IRC
```

## Connect

```
# launch pidgin
# create a profile
# to connect as user, any username (no password is needed) > connect
# view chats > join.

# to connect as operator, username:password is needed.
```

## Recon

```
nmap --script irc-unrealircd-backdoor.nse -p PORT IP
```
