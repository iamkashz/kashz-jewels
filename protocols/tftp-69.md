# tftp :69/udp

### Filename containing spaces fix:

1. kali-tftp fails when `filename` contains spaces.
2. Install `sudo apt install -y tftp-hpa`

### Commands

```bash
tftp [-v] -m binary IP -c get '\Windows\system.ini' system.ini
# \Windows\System32\Drivers\etc\hosts
```