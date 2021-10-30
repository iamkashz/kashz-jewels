# rconfig management

## Default Creds

```
admin:admin
```

## Interesting Paths

```
[/home]/rconfig/config/config.inc.php
```

## Change Admin Pass (Auth Bypass)

v 3.9.3 | 3.9.4 | 3.9.5

```
# update vars in file
https://www.exploit-db.com/exploits/48878
# option 2 changes admin password admin:Testing1@
```

## Manual Reverse Shell

* https://gist.github.com/farid007/9f6ad063645d5b1550298c8b9ae953ff

1. Login > `/vendors.php` > Add Vendor > .php as Vendor Logo
2. Burp the `Content-Type` to `image/gif`
3. File is uploaded at /images/vendor/shell.php?cmd=whoami
4. revshell will auto invoke on page refresh

## Authenticated RCE

v3.9.4 | 3.9.3

* https://www.exploit-db.com/exploits/48207

## RCE to root <=3.9.4

* https://github.com/v1k1ngfr/exploits-rconfig

Performs chained execution to root

1. CVE-2019-19509 : authenticated RCE
2. CVE-2019-19585 : Local Privilege Escalation (root)
3. CVE-2020-10220 : unauthenticated SQLi



