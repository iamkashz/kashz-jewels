# c2 frameworks

## Powershell-Empire

### Install

```bash
sudo apt install powershell-empire starkiller
```

### Running

```
# config file
/usr/share/powershell-empire/empire/client/config.yaml

# start server
sudo powershell-empire server

# start client
powershell-empire client
connect HOSTNAME --username=USER --password=PASS

# gui version
starkiller
```

## Covenant

### Install

Install `dotnet` using `kali-tweaks` > `metapackages` > `windows-resources`.

```bash
cd /tmp
wget https://packages.microsoft.com/config/ubuntu/21.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get install -y dotnet-sdk-3.1
```

```bash
cd /opt; sudo git clone --recurse-submodules https://github.com/ZeroPointSecurity/Covenant.git
```

### startup-script

* Save this to `/usr/bin/start-covenant`

```bash
#!/bin/sh
set -e
cd /opt/Covenant/Covenant && sudo /usr/bin/dotnet run
```

* `sudo chmod 755 /usr/bin/start-covenant`

## References

* [GoogleDoc: C2Matrix](https://docs.google.com/spreadsheets/d/1b4mUxa6cDQuTV2BPC6aA-GR4zGZi0ooPYtBe4IgPsSc/edit#gid=0)
* Install Guide: [howto.thec2matrix.com/](https://howto.thec2matrix.com/)