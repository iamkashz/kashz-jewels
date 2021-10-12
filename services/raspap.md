# raspAP

[https://checkmarx.com/blog/chained-raspap-vulnerabilities-grant-root-level-access/](https://checkmarx.com/blog/chained-raspap-vulnerabilities-grant-root-level-access/)

## Default Creds

```
admin:secret
```

## Version check (Authenticated)

```
# version check > About RaspAP
http://IP:PORT/index.php?page=about
```

## Interesting Paths

```
/includes/config.php
```

## webconsole

```bash
# Dashboard > System > Console
/includes/webconsole.php
```
