# osclass

## Interesting Paths

```bash
# login page
/osclass/oc-admin
/osclass/oc-admin/index.php

# update mysql pass
# if bcrypt: https://bcrypt-generator.com/
update oc_t_admin set s_password=PWDHASH where s_username='admin';
```

## v3.4.1 LFI

```
https://www.exploit-db.com/exploits/34763
```
