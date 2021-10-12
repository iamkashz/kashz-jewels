# ftp

## ProFTPd 1.3.5

```
# file copy
https://www.exploit-db.com/exploits/36742
```

## vsftpd 2.3.4

```
https://gitlab.com/0xdf/ctfscripts/-/tree/master/vsftpd2.3.4-backdoor
# launches a php intereactive shell
# run phpinfo() and search for disable_functions - to check for commands that will not run on system via php shell
getcwd();
get_current_user();
scandir("/")
ls # List local, instance or class variables, methods and constants.
show $variable
echo file_get_contents("FILE_TO_READ")
readfile("FILE_TO_READ")
fwrite(fopen("FILE_TO_WRITE_TO","w+"),"DATA");
```
