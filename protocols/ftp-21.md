# ftp :21

## download all via FTP

```
wget -m ftp://anonymous:anonymous@IP
wget -m --user="" --password="" ftp://IP
```

## Interesting Path for different FTP Config files

```
# vsftpd
/etc/vsftpd.conf
# look for
write_enable=YES
anon_root=<PATH-WHERE-FILES-ARE-WRITTEN-TO>
```

## Default upload dir
```bash
/var/ftp
```