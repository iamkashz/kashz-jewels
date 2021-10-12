# openemr

## Default Creds

```
admin:pass
```

## Interesting Paths

```bash
# version check
/admin.php

# db information
/gacl/setup.php

# register page
/portal/account/register.php

# db creds
/sql/defaults.sql
/sites/default/sqlconf.php
```

## Enable patient portal

Note: most exploit db require this

Logged in > Administration > Globals > Portal > Enable Version 2 Onsite Patient Portal

## RCE (authenticated)

v5.0.1.x

```
https://www.exploit-db.com/exploits/45161
```

## multiple SQLi

v5.0.1.3

```
https://www.open-emr.org/wiki/images/1/11/Openemr_insecurity.pdf
```
