# phpmyadmin

## Interesting Stuff

```
/etc/phpmyadmin/config-db.php
```

## LFI + phpinfo() exploit race-condition

```bash
REQUIREMENT: file_uploads: ON

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/File%20Inclusion/phpinfolfi.py

# modify code
1. update payload
2. add cookie, session ID in request (LFI and payload)
3. update LFIREQ 
4. => to =&gt

python phpinfolfi.py IP PORT THREADS
```
