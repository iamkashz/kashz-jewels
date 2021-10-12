# drupal

## Droopescan

```bash
droopescan scan drupal -u <URL>
```

## Interesting Paths

```bash
# version
/core/CHANGELOG.txt

# rest API endpoint
/rest

# contains version of drupal
view-source of home page
/CHANGELOG.txt
/core/install.php

# contains db creds
/sites/default/settings.php
```

## manual enumeration

```bash
# user enumeration via register page
admin

# number of users enumeration
/user/<number> until error

# hidden post enumeration 
/node/<number> for 1-100
wfuzz -c -z range,1-100 -u IP/node/FUZZ
[--hh ignore-errors-chars]

# php plugin installation check
# 403 = good, 404 = not installed
/modules/php
```
