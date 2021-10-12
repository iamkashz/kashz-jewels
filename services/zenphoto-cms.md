# zenphoto cms

## version check

```
# view source on homepage
<!-- zenphoto version 1.4.1.4 [8157] (Official Build)
```

## Interesting Paths

```bash
# admin login page
/admin
/zp-core/admin.php

# config file
/zp-data/zp-config.php
/zp-core/zp-config.php
config.php
```

## 'ajax_create_folder.php' RCE

v1.4.1.4

```
https://www.exploit-db.com/exploits/18083
$ php 18083.php IP PATH
# msfvenom to stable shell
```
