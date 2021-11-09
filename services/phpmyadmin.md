# phpmyadmin

## Interesting Stuff

```
/etc/phpmyadmin/config-db.php
```

## LFI + phpinfo() exploit race-condition

REQUIREMENT: file_uploads: ON

* [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/File%20Inclusion/phpinfolfi.py](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/File%20Inclusion/phpinfolfi.py)

```bash
# modify code
1. update payload
2. add cookie, session ID in request (LFI and payload)
3. update LFIREQ 
4. change `=>` to `=&gt`

python phpinfolfi.py IP PORT THREADS
```
