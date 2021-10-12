# RDP tools

## Connect

```bash
$ xfreerdp /dynamic-resolution +clipboard /cert:ignore /v:IP /u:USER /p:PASS

$ rdesktop IP
```

## Run shell as elevated user without UAC prompt

### [Advanced Run](https://www.nirsoft.net/utils/advanced_run.html)

```bash
> AdvancedRun.exe /EXEFilename "kashz.exe" /RunAs 4 /Run
# 3: Administrator
# 4: SYSTEM
```

### [nircmd](https://www.nirsoft.net/utils/nircmd.html)

```bash
> nircmd.exe elevatecmd runassystem kashz.exe
```

{% embed url="https://www.winhelponline.com/blog/run-program-as-system-localsystem-account-windows" %}
