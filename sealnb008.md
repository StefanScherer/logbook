# sealnb008

## 2017-11-21

### 1Password
* `choco install -y 1password`
* `choco install -y dropbox`
* In 1Password open Help -> Advanced -> Use Native Messaging protocol

### Docker
* Docker CLI, Docker Machine and VMware machine driver preinstalled
* `docker-machine create -d vmwareworkstation --vmwareworkstation-memory-size 2048 default`
* TODO: error: Error creating machine: Error in driver during machine creation: Machine didn't return an IP after 120 seconds, aborting

### Vagrant
* Vagrant 2.0.1 preinstalled
* `vagrant plugin install vagrant-vmware-workstation`
* Add license to VMware Workstation 14 Pro
* `vagrant plugin license vagrant-vmware-workstation C:\Users\stefan.scherer\Downloads\license.lic`
* Install my Vagrantfile in  C:\Users\stefan.scherer\.vagrant.d\Vagrantfile
* Check Firmware virutalization settings

### Editors
* `choco install -y atom`
* `choco install -y visualstudiocode`
* TODO: atom fails at the moment, have to install it manually

### Tools
* `choco install -y sudo`
* Change User PATH: `C:\Program Files\git\usr\bin` added to have ssh in PATH:
* Generate new SSH key with passphrase
* `ssh-keygen`
* `notepad .ssh\id_rsa.pub` and insert public key to your GitHub account
* Send public key to your Gitolite admin

### Dotfiles
* Open PowerShell terminal
```powershell
install-module posh-git -Scope CurrentUser
install-module z -Scope CurrentUser -AllowClobber
cd $env:USERPROFILE
mkdir code
cd code
git clone https://github.com/StefanScherer/dotfiles-windows
cd dotfiles-windows
.\sync.ps1
```
* Open new PowerShell terminal
* This starts an SSH agent

### Usability 
* Google Chrome -> Swipe Gesture installed for two finger swipe right to go back to previous page.

## 2017-11-22

### Chrome
* Installed AdBlock Plus

### Screen To Gif
* `choco install -y screentogif`
* `choco install -y gifsicle` to scale down HiDPI gif for blog posts or Twitter (`gifsicle --scale 0.5x0.5 hidpi.gif -o rdy2tweet.gif`)

### WSL
* Install Ubuntu from Microsoft Store to use `bash.exe`
* Move home directory to `/Users` to have similar paths for WSL and Windows for Docker volumes etc.
```
cd ..
sudo mkdir /Users
sudo cp -r stefan /Users/stefan.scherer
sudo chown stefan:stefan /Users/stefan.scherer
sudo sed -i 's,/home/stefan,/Users/stefan.scherer,' /etc/passwd
exit
```
* Create code directory on Windows side
* Open PowerShell
```
mkdir code
exit
```
* Open Ubuntu shell again
* Create symlink `code` and docker-machine folder for Docker TLS certs
```
ln -s /mnt/c/Users/stefan.scherer/code code
mkdir .docker
ln -s /mnt/c/Users/stefan.scherer/.docker/machine .docker/machine
ln -s /mnt/c/Users/stefan.scherer/Downloads/ Downloads
ln -s /mnt/c/Users/stefan.scherer/Desktop/ Desktop
```
* Install tools
```
sudo apt-get install -y jq pass
curl https://get.docker.com | sh
```
* Copy SSH Keys into Linux session
```
umask 022
mkdir .ssh
chmod 700 .ssh
cp /mnt/c/Users/stefan.scherer/.ssh/* .ssh/
chmod 600 .ssh/*
```
* Install Unix dotfiles
```
cd code
git clone git@github.com:StefanScherer/dotfiles
cd dotfiles
./sync.sh
```
* Use VMware Docker Machine from WSL with volumes
```
docker-machine.exe start
eval $(docker-machine.exe env --shell bash | sed 's/C://g' | sed 's/\\/\//g')
docker version
cd ~/code
docker run -v $(pwd):/code alpine ls /code
```

### Vagrant + vCloud

* Install vagrant-vcloud plugin 0.4.7
```
C:\> vagrant plugin install vagrant-vcloud
Installing the 'vagrant-vcloud' plugin. This can take a few minutes...
Fetching: ruby-progressbar-1.9.0.gem (100%)
Fetching: netaddr-1.5.1.gem (100%)
Fetching: awesome_print-1.8.0.gem (100%)
Fetching: unicode-display_width-1.3.0.gem (100%)
Fetching: terminal-table-1.8.0.gem (100%)
Fetching: vagrant-vcloud-0.4.7.gem (100%)
Installed the plugin 'vagrant-vcloud (0.4.7)'!
```
* Install missing dependency nokogiri
```
C:\> vagrant plugin install nokogiri
Installing the 'nokogiri' plugin. This can take a few minutes...
Fetching: mini_portile2-2.3.0.gem (100%)
Fetching: nokogiri-1.8.1-x64-mingw32.gem (100%)
Nokogiri is built with the packaged libraries: libxml2-2.9.5, libxslt-1.1.30, zlib-1.2.11, libiconv-1.15.
Installed the plugin 'nokogiri (1.8.1)'!
Post install message from the 'nokogiri' plugin:

Nokogiri is built with the packaged libraries: libxml2-2.9.5, libxslt-1.1.30, zlib-1.2.11, libiconv-1.15.
```
* Patch vagrant-vcloud for newer API versions
```powershell
Invoke-WebRequest -UseBasicParsing `
  https://raw.githubusercontent.com/plossys/vagrant-vcloud/949f791e3598547bdca870715a3a116c7812ef83/lib/vagrant-vcloud/driver/meta.rb `
  -OutFile $env:USERPROFILE\.vagrant.d\gems\2.4.2\gems\vagrant-vcloud-0.4.7\lib\vagrant-vcloud\driver\meta.rb
```

## 2017-11-24

### Windows Docker Machine

```
cd code
git clone git@github.com:StefanScherer/windows-docker-machine
cd windows-docker-machine
vagrant up 2016
```
* Patch docker-machine.exe to talk to Windows dockerd.exe
```
sudo sed -b -i s/v1.15/v1.24/ C:\ProgramData\chocolatey\lib\docker-machine\bin\docker-machine.exe
```

```
C:\Users\stefan.scherer> docker-machine ls
NAME      ACTIVE   DRIVER              STATE     URL                          SWARM   DOCKER                  ERRORS
2016      -        generic             Running   tcp://192.168.209.132:2376           v17.10.0-ee-preview-3
default   -        vmwareworkstation   Running   tcp://192.168.209.128:2376           v17.11.0-ce
```

* Linux and Windows Containers and volumes

```
C:\Users\stefan.scherer\code> docker-machine ls
NAME      ACTIVE   DRIVER              STATE     URL                          SWARM   DOCKER                  ERRORS
2016      *        generic             Running   tcp://192.168.209.133:2376           v17.10.0-ee-preview-3
default   -        vmwareworkstation   Running   tcp://192.168.209.128:2376           v17.11.0-ce
C:\Users\stefan.scherer\code> docker-machine env | iex
C:\Users\stefan.scherer\code> docker run -v "$((pwd).path.replace('C:','').replace('\','/')):/code" -w /code alpine ls -l
total 32
drwxrwxrwx    1 root     root          4096 Nov 24 10:35 dotfiles-windows
drwxrwxrwx    1 root     root         24576 Nov 24 22:16 packer-windows
drwxrwxrwx    1 root     root             0 Nov 24 10:56 plossys
drwxrwxrwx    1 root     root          4096 Nov 24 22:30 windows-docker-machine
C:\Users\stefan.scherer\code> docker-machine env 2016 | iex
C:\Users\stefan.scherer\code> docker run -v "$(pwd):C:\code" -w /code microsoft/nanoserver cmd /c dir
 Volume in drive C has no label.
 Volume Serial Number is A87A-B4A6

 Directory of C:\code

11/24/2017  02:19 PM    <DIR>          .
11/24/2017  02:19 PM    <DIR>          ..
11/24/2017  02:35 AM    <DIR>          dotfiles-windows
11/24/2017  02:16 PM    <DIR>          packer-windows
11/24/2017  02:56 AM    <DIR>          plossys
11/24/2017  02:30 PM    <DIR>          windows-docker-machine
               0 File(s)              0 bytes
               6 Dir(s)  895,754,330,112 bytes free
C:\Users\stefan.scherer\code>
```

# 2017-12-03
* Install `hub`
```
choco install -y hub
```

# 2017-12-15
* Update Packer 1.1.3 due to restart problem in VMware boxes
```
choco upgrade -y packer
```

# 2017-12-21
* Link Vagrant folder with global Vagrantfile for vCloud from Windows to WSL to make `vcloud` shell wrapper work
```
ln -s /mnt/c/Users/stefan.scherer/.vagrant.d/ .vagrant.d
```

# 2018-03-28
* Update to Vagrant VMware Desktop plugin
* Remove vagrant-vmware-workstation plugin version 5.0.4
```
vagrant plugin uninstall vagrant-vmware-workstation
```
* Remove scheduled task "vagrant*"
* Update Vagrant 2.0.3
```
choco upgrade vagrant
```
* Install Vagrant VMware Utility
```
choco install vagrant-vmware-utility -pre -version 1.0.0
```
* Install Vagrant VMware Desktop plugin
```
vagrant plugin install vagrant-vmware-desktop
```
Woah, nokogiri again
```
$ vagrant plugin install vagrant-vmware-desktop
Installing the 'vagrant-vmware-desktop' plugin. This can take a few minutes...
Fetching: mini_portile2-2.3.0.gem (100%)
Fetching: nokogiri-1.8.2-x64-mingw32.gem (100%)
Nokogiri is built with the packaged libraries: libxml2-2.9.7, libxslt-1.1.32, zlib-1.2.11, libiconv-1.15.
Fetching: vagrant-reload-0.0.1.gem (100%)
Fetching: vagrant-share-1.1.9.gem (100%)
Fetching: ruby-progressbar-1.9.0.gem (100%)
Fetching: netaddr-1.5.1.gem (100%)
Fetching: awesome_print-1.8.0.gem (100%)
Fetching: unicode-display_width-1.3.0.gem (100%)
Fetching: terminal-table-1.8.0.gem (100%)
Fetching: vagrant-vcloud-0.4.7.gem (100%)
Fetching: vagrant-vmware-desktop-1.0.0.gem (100%)
Bundler, the underlying system Vagrant uses to install plugins,
reported an error. The error is shown below. These errors are usually
caused by misconfigured plugin installations or transient network
issues. The error from Bundler is:

Unable to resolve dependency: user requested 'nokogiri (= 1.8.1)'
C:\Users\stefan.scherer
```
* Removing all plugins and starting again, keeping boxes and Vagrantfile from previous installation
```
$ mv .\.vagrant.d\ vagrant-201
$ vagrant plugin list
$ rmdir .\.vagrant.d\boxes\
$ mv .\vagrant-201\boxes\ .\.vagrant.d\
$ cp .\vagrant-201\Vagrantfile .\.vagrant.d\
```
* Install Vagrant VMware Desktop plugin
```
vagrant plugin install vagrant-vmware-desktop
```
* Install other Vagrant plugins
```
vagrant plugin install vagrant-reload
vagrant plugin install vagrant-vcloud
```

* Patch vagrant-vcloud for newer API versions
```powershell
Invoke-WebRequest -UseBasicParsing `
  https://raw.githubusercontent.com/plossys/vagrant-vcloud/949f791e3598547bdca870715a3a116c7812ef83/lib/vagrant-vcloud/driver/meta.rb `
  -OutFile $env:USERPROFILE\.vagrant.d\gems\2.4.3\gems\vagrant-vcloud-0.4.7\lib\vagrant-vcloud\driver\meta.rb
```
* Vagrant plugins installed
```
$ vagrant plugin list
vagrant-reload (0.0.1)
vagrant-vcloud (0.4.7)
vagrant-vmware-desktop (1.0.0)
```
* License the plugin
```
vagrant plugin license vagrant-vmware-desktop $env:USERPROFILE\Desktop\license.lic
```

# 2018-04-03
* Fix vagrant-vcloud plugin
```
$ vagrant plugin install nokogiri
$ vagrant plugin list
nokogiri (1.8.2)
vagrant-reload (0.0.1)
  - Version Constraint: > 0
vagrant-vcloud (0.4.7)
  - Version Constraint: > 0
vagrant-vmware-desktop (1.0.1)
  - Version Constraint: > 0
```

# 2018-05-02
* Uninstall Windows version of Vagrant
* Update Vagrant VMware Utility 1.0.1
```
choco install -y vagrant-vmware-utility
```
* Add symlink for Vagrant VMware workaround
```
mkdir \mnt\c\Users
cmd /c mklink /D \mnt\c\Users\stefan.scherer C:\Users\stefan.scherer
```

* Removed Ubuntu
* Installed fresh Ubuntu
* User `stefan`
* Repeat steps above for WSL (home dir, SSH keys, dotfiles)
* Link existing global Vagrant folder into WSL, update plugins
```
ln -s /mnt/c/Users/$(cmd.exe /c echo %USERNAME% | tr -d '\r')/.vagrant.d/ ~/.vagrant.d
sudo apt-get install -y build-essential
vagrant plugin repair

$ vagrant plugin list
nokogiri (1.8.2)
vagrant-reload (0.0.1)
  - Version Constraint: > 0
vagrant-vcloud (0.5.0)
  - Version Constraint: > 0
vagrant-vmware-desktop (1.0.3)
  - Version Constraint: > 0
```
* Link Vagrant VMware Utility certs 
```
sudo ln -s /mnt/c/ProgramData/HashiCorp/vagrant-vmware-desktop /opt/vagrant-vmware-desktop
```
* Copy vmrun.exe helper
* Must be copied into WSL file system as my cloned GitHub repos are lying in the Windows filesystem and cannot have backslashes in file names.
```
sudo cp bin/vmrun.exe-helper "/usr/bin/C:\Program Files (x86)\VMware\VMware Workstation\vmrun.exe"
```

* Generate new SSH Key
```
ssh-keygen
cat ~/.ssh/id_rsa.pub
```
* Insert SSH pub key at https://github.com/settings/keys

* Generate new GPG key
* See also https://help.github.com/articles/generating-a-new-gpg-key/
```
gpg --gen-key
gpg --list-secret-keys --keyid-format LONG
gpg --armor --export YOURGPGID
```
* https://help.github.com/articles/telling-git-about-your-gpg-key/
```
vi ~/.gitconfig
git config --global user.signingkey YOURGPGID
```
* Insert GPG pub key at https://github.com/settings/keys

* Update Ubuntu 18.04
```
$ sudo apt update 
$ sudo apt upgrade
$ sudo apt dist-upgrade
$ sudo apt dist-upgrade
$ sudo apt install update-manager-core
$ sudo do-release-upgrade
$ sudo do-release-upgrade -d
```
