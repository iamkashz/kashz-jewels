# kashz-kali

On top of the base kali install, following are the custom commands I have setup for quick easy access to git-repos,
tools I would need to use.

### Kali Mount Shared Directory

```bash
kali-tweaks
Select Virtualization > Install additional packages and scripts for VMware.
# should be setup to mount
sudo mount-shared-folders
```

### Sublime Text

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -;
sudo apt-get install apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt update; sudo apt install -y sublime-text sublime-merge; cd ~;
```

### View hidden files in subl directory-view

Sublime Text > Preferences > Settings

```bash
{
  "folder_exclude_patterns": [],
  "file_exclude_patterns": ["*.pyc","*.pyo","*.exe","*.dll","*.obj","*.o","*.a","*.lib","*.so","*.dylib","*.ncb","*.sdf","*.suo","*.pdb","*.idb",".DS_Store","*.class","*.psd","*.sublime-workspace"]
}
```

### Brave Browser

```bash
sudo apt install apt-transport-https curl
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
sudo apt update
sudo apt install -y brave-browser
```

### Browser Customization

#### Firefox Addons

* [foxyproxy](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/)
* [ublock origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/)
* [wappalyzer](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/)
* [cookie manager](https://addons.mozilla.org/en-US/firefox/addon/a-cookie-manager/)
* [cookie-editor](https://addons.mozilla.org/en-US/firefox/addon/cookie-editor/)
* [2FA Authenticator](https://addons.mozilla.org/en-US/firefox/addon/auth-helper/)

#### Chrome Addons

* [ModHeader](https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj?hl=en)

### Repos (cd /opt/)

```bash
cd /opt/
sudo git clone https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite.git
sudo git clone https://github.com/rebootuser/LinEnum
sudo git clone https://github.com/dievus/threader3000.git
sudo git clone https://github.com/AonCyberLabs/Windows-Exploit-Suggester.git
sudo git clone https://github.com/ivan-sincek/php-reverse-shell
sudo git clone https://github.com/Cryilllic/Active-Directory-Wordlists
sudo git clone https://github.com/dyne/file-extension-list
sudo git clone https://github.com/stealthcopter/deepce.git
sudo git clone https://github.com/samratashok/nishang.git
sudo git clone https://github.com/Anon-Exploiter/SUID3NUM.git
sudo git clone https://github.com/cddmp/enum4linux-ng.git
sudo git clone https://github.com/bitsadmin/wesng.git
sudo git clone https://github.com/WhiteWinterWolf/wwwolf-php-webshell.git
sudo git clone https://github.com/mzet-/linux-exploit-suggester.git
sudo git clone https://github.com/jondonas/linux-exploit-suggester-2.git
sudo git clone https://github.com/sleventyeleven/linuxprivchecker
sudo git clone https://github.com/diego-treitos/linux-smart-enumeration
sudo git clone https://github.com/rasta-mouse/Sherlock.git
sudo git clone https://github.com/WazeHell/PE-Linux.git
sudo git clone https://github.com/borjmz/aspx-reverse-shell
sudo git clone https://github.com/enjoiz/Privesc.git
sudo git clone https://github.com/r3motecontrol/Ghostpack-CompiledBinaries.git
sudo git clone https://github.com/dirkjanm/krbrelayx
sudo git clone https://github.com/antonioCoco/ConPtyShell
sudo git clone https://github.com/brightio/penelope.git
sudo git clone https://github.com/ohpe/juicy-potato.git
sudo git clone https://github.com/SpiderLabs/ikeforce.git
sudo git clone https://github.com/mchoji/winrm-brute.git
sudo git clone https://github.com/iamkashz/ctf-scripts.git
sudo git clone https://github.com/411Hall/JAWS.git
sudo git clone https://github.com/PowerShellMafia/PowerSploit.git
sudo git clone https://github.com/fox-it/BloodHound.py.git
sudo git clone https://github.com/BloodHoundAD/BloodHound.git

# nmapAutomator
cd /opt; sudo git clone https://github.com/21y4d/nmapAutomator.git
sudo ln -s $(pwd)/nmapAutomator/nmapAutomator.sh /usr/local/bin/; cd ~;

# Autorecon
cd /opt; sudo git clone https://github.com/Tib3rius/AutoRecon.git
cd /opt/AutoRecon;sudo python3 -m pip install -r requirements.txt; sudo python3 -m pip install .;cd ~;

# impacket
sudo apt install python3-pip
cd /opt; sudo git clone https://github.com/SecureAuthCorp/impacket.git
cd impacket; python3 -m pip install .;sudo python3 -m pip install . cd ~;

# arsenal
cd /opt; sudo git clone https://github.com/Orange-Cyberdefense/arsenal.git
cd arsenal; python3 -m pip install -r requirements.txt; cd ~;
echo "\n\n# arsenal alias\nalias a=/opt/arsenal/run -t -e" >> ~/.zshrc; cd ~;

# gittools
cd /opt; sudo git clone https://github.com/internetwache/GitTools.git
sudo ln -s /opt/GitTools/Finder/gitfinder.py /usr/local/bin
sudo ln -s /opt/GitTools/Dumper/gitdumper.sh /usr/local/bin
sudo ln -s /opt/GitTools/Extractor/extractor.sh /usr/local/bin/gitextractor.sh
cd ~;

# mitm6
cd /opt; sudo git clone https://github.com/dirkjanm/mitm6.git
cd mitm6; sudo pip3 install .;cd ~;
```

### Install additional tools via APT

```bash
sudo apt install -y rlwrap feroxbuster remmina docker.io xclip redis-tools tree php-curl python3-git-repo-updater odat golang terminator libimage-exiftool-perl html2text jq gcc-multilib g++-multilib flameshot
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev libguestfs-tools gccgo-go
sudo apt install -y bloodhound neo4j
sudo gem install -y evil-winrm
sudo gitup --add /opt

# fix wfuzz; Pycurl is not compiled against Openssl
sudo apt --purge remove python3-pycurl;sudo apt install -y libcurl4-openssl-dev libssl-dev;sudo python3 -m pip install pycurl wfuzz
```

### windows-stuff

```bash
# printspoofer-exe
sudo mkdir /opt/printspoofer-exe; cd /opt/printspoofer-exe/; sudo wget https://github.com/itm4n/PrintSpoofer/releases/download/v1.0/PrintSpoofer32.exe; sudo wget https://github.com/itm4n/PrintSpoofer/releases/download/v1.0/PrintSpoofer64.exe; cd ~;

# juicypotato-exe
sudo mkdir /opt/juicypotato-exe; cd /opt/juicypotato-exe; sudo wget https://github.com/ohpe/juicy-potato/releases/download/v0.1/JuicyPotato.exe -O JuicyPotato64.exe; sudo wget https://github.com/ivanitlearning/Juicy-Potato-x86/releases/download/1.2/Juicy.Potato.x86.exe -O JuicyPotato.exe; cd ~;

# roguepotato-exe
sudo mkdir /opt/roguepotato-exe; cd /opt/roguepotato-exe; sudo wget https://github.com/antonioCoco/RoguePotato/releases/download/1.0/RoguePotato.zip; sudo unzip RoguePotato.zip; sudo rm RoguePotato.zip; cd ~;

# psexec
sudo mkdir /opt/psexec/; cd /opt/psexec/; sudo wget https://download.sysinternals.com/files/PSTools.zip; sudo unzip PSTools.zip; sudo rm PSTools.zip; cd ~;

# nc
mkdir /tmp/files; cd /tmp; wget https://eternallybored.org/misc/netcat/netcat-win32-1.12.zip; unzip netcat-win32-1.12.zip -d /tmp/files/; sudo mkdir /opt/nc; sudo cp /tmp/files/nc* /opt/nc/; sudo cp /usr/bin/nc /opt/nc/nc; cd ~;

# accesschk
sudo mkdir /opt/accesschk; cd /opt/accesschk; sudo wget https://download.sysinternals.com/files/AccessChk.zip; sudo unzip AccessChk.zip; sudo rm AccessChk.zip; cd ~;
cd /opt; sudo mkdir /opt/socat;

# socat
sudo mkdir --parents /opt/socat/linux; cd /opt/socat/linux; sudo wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx86.bin -O socat; sudo wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx64.bin -O socat64; sudo chmod +x *; sudo mkdir /opt/socat/windows; cd /opt/socat/windows; sudo wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx86.exe -O socat.exe; sudo wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx64.exe -O socat64.exe; cd ~;

# sysinternals (sigcheck.exe | strings.exe | tcpview.exe)
sudo mkdir -p /opt/sysinternals/sigcheck-exe; cd /opt/sysinternals/sigcheck-exe/; sudo wget https://download.sysinternals.com/files/Sigcheck.zip; sudo unzip Sigcheck.zip; sudo rm Sigcheck.zip; cd ~;
sudo mkdir /opt/sysinternals/strings-exe; cd /opt/sysinternals/strings-exe/; sudo wget https://download.sysinternals.com/files/Strings.zip; sudo unzip Strings.zip; sudo rm Strings.zip; cd ~;
sudo mkdir /opt/sysinternals/tcpview-exe; cd /opt/sysinternals/tcpview-exe/; sudo wget https://download.sysinternals.com/files/TCPView.zip; sudo unzip TCPView.zip; sudo rm TCPView.zip; cd ~;

# powershell encoded revshell
# https://gist.github.com/tothi/ab288fb523a4b32b51a53e542d40fe58
sudo mkdir /opt/powershell_encoded_revshell/; cd /opt/powershell_encoded_revshell/; sudo wget https://gist.githubusercontent.com/tothi/ab288fb523a4b32b51a53e542d40fe58/raw/40ade3fb5e3665b82310c08d36597123c2e75ab4/mkpsrevshell.py -O powershell_encoded_revshell.py; python3 powershell_encoded_revshell.py; cd ~;
```

### Install Custom tools

```bash
# chisel
cd ~; curl https://i.jpillora.com/chisel! | sudo bash
sudo mkdir --parents /opt/chisel/linux; cd /opt/chisel/linux; sudo wget https://github.com/jpillora/chisel/releases/download/v1.7.6/chisel_1.7.6_linux_amd64.gz; sudo wget https://github.com/jpillora/chisel/releases/download/v1.7.6/chisel_1.7.6_linux_386.gz; sudo gzip -d *; sudo mv chisel_1.7.6_linux_386 chisel; sudo mv chisel_1.7.6_linux_amd64 chisel64;
sudo mkdir /opt/chisel/windows; cd /opt/chisel/windows; sudo wget https://github.com/jpillora/chisel/releases/download/v1.7.6/chisel_1.7.6_windows_386.gz; sudo wget https://github.com/jpillora/chisel/releases/download/v1.7.6/chisel_1.7.6_windows_amd64.gz; sudo gzip -d *; sudo mv chisel_1.7.6_windows_386 chisel.exe; sudo mv chisel_1.7.6_windows_amd64 chisel64.exe; cd ~;

# pspy
sudo mkdir /opt/pspy; cd /opt/pspy; sudo wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy32; sudo wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64; sudo wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy32s; sudo wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64s;cd ~;

# mongosh client setup
cd ~; wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -; echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/5.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list; sudo apt update; sudo apt install -y mongodb-mongosh mongodb-org-shell; mongosh --version; cd ~;

# oracle sqlPlus
sudo apt install oracle-instantclient-sqlplus

# oracle tns (odat)
python3 -m pip install cx_Oracle --upgrade; sudo mkdir /opt/oracle-tns; cd /opt/oracle-tns/; sudo wget 'https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-L_2uGJGU7AVNRcqRvEi%2F-LcreDSG0Hi8mv8n8DIw%2F-LcrnYv40ILvFrpjKRkb%2Fsids-oracle.txt?alt=media&token=8206a9f6-af86-4a49-ac71-179ca973d836' -O sids-oracle.txt; sudo wget 'https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-L_2uGJGU7AVNRcqRvEi%2F-LcreDSG0Hi8mv8n8DIw%2F-Lcrmdr8nRaj1Ea6JQqm%2Fusers-oracle.txt?alt=media&token=e1dc7604-86d8-4fe6-8dcc-f8cb5167c83d' -O users-oracle.txt; sudo wget 'https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-L_2uGJGU7AVNRcqRvEi%2F-LcreDSG0Hi8mv8n8DIw%2F-LcrmhoNYnuxhr1Sy7A1%2Fpass-oracle.txt?alt=media&token=0879b74c-07eb-40a7-8038-e5f4b42621f3' -O pass-oracle.txt;cd ~;

# postman
cd ~;wget https://dl.pstmn.io/download/latest/linux64 -O /tmp/postman.tar.gz;
cd /opt; sudo tar -xvf /tmp/postman.tar.gz; rm /tmp/postman.tar.gz;
sudo ln -s /opt/Postman/app/postman /usr/local/bin/;cd ~;

# joplin
cd ~; wget -O - https://raw.githubusercontent.com/laurent22/joplin/dev/Joplin_install_and_update.sh | bash

# pyenv
cd ~; curl https://pyenv.run | bash

# namemash.py
sudo mkdir /opt/namemash; cd /opt/namemash; sudo wget https://gist.githubusercontent.com/superkojiman/11076951/raw/053152dba6c5cc3107ff0374ce7246306958d72c/namemash.py; sudo chmod +x namemash.py
cd ~;
```

### tmux

```bash
cd /opt; sudo git clone https://github.com/iamkashz/tmux-config.git
./tmux-config/install.sh
# use terminator shell
```

### Update PATH (subl ~/.zshrc)

```bash
# golang vars
export GOROOT=/usr/lib/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH

# sudo updatedb; locate libsqlplus.so
# set ORACLE_HOME=path without filename
# sqlplus vars
export ORACLE_HOME=/usr/lib/oracle/19.6/client64/lib/
export LD_LIBRARY_PATH="$ORACLE_HOME"
export PATH="$ORACLE_HOME:$PATH"

# pyenv vars
export PATH="/home/kashz/.pyenv/bin:/home/kashz/.pyenv/shims:/home/kashz/.local/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)" 
```

### python2 pyenv

```bash
pyenv install -v 2.7.18
# to set global python2
pyenv global 2.7.18

# setup pip for py2
cd ~; wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
sudo python2 get-pip.py
python2 -m pip install setuptools
rm get-pip.py
python3 -m pip install --upgrade pip
python3 -m pip install --upgrade pip

# windows-exploit-suggester.py
python2 -m pip install xlrd==1.2.0
pip install impacket
pip install requests
pip install --upgrade pip
pip install droopescan
```

### Custom tasks

```bash
# rockyou extract
cd /usr/share/wordlists; sudo gzip -d /usr/share/wordlists/rockyou.txt.gz;cd ~

# enum4linux update
sudo wget https://raw.githubusercontent.com/CiscoCXSecurity/enum4linux/master/enum4linux.pl -O /usr/share/enum4linux/enum4linux.pl

# smb /etc/samba/smb.conf
[global]
	client min protocol = NT1
	# client min protocol = LANMAN1
```

### Bloodhound

```bash
python2 -m pip install dnspython ldap3 impacket
cd /opt/BloodHound.py; pip install .; cd ~;
```

### evil-winrm fix readline

```bash
sudo apt install libreadline-dev
$RUBY_VERSION = $(ruby --version | cut -d 'p' -f 1 | cut -d ' ' -f 2)
cd /tmp;
wget "https://ftp.ruby-lang.org/pub/ruby/2.7/ruby-$RUBY_VERSION.tar.gz"
tar -xf ruby-$RUBY_VERSION.tar.gz
cd /tmp/$RUBY_VERSION/ext/readline; ruby ./extconf.rb; make
sudo cp /usr/lib/x86_64-linux-gnu/ruby/$RUBY_VERSION/readline.so /usr/lib/x86_64-linux-gnu/ruby/$RUBY_VERSION/readline.so.bk
sudo cp -f readline.so /usr/lib/x86_64-linux-gnu/ruby/$RUBY_VERSION/readline.so
```

## References

* [kali.org/using-eol-python-versions/](https://www.kali.org/docs/general-use/using-eol-python-versions/)
* [docs.mongodb.com/tutorial/install-mongodb-on-debian/](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-debian/)