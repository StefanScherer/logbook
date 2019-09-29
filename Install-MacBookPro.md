# Installationlogbuch Stefans MacBook Pro

## 2014-03-01

* Rechner eingeschaltet
* Benutzer Stefan angelegt
* Kinderkonten angelegt, Kinderschutz aktiviert
* Benutzer Doris angelegt
* Ins WLAN eingetragen
* App Store -> Updates eingespielt, Mavericks bootet nochmal, weitere Updates eingespielt
* Homebrew installiert

```
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

* Xcode 5.0.2 installiert

```
sudo xcodebuild -license
brew doctor
```

* Dann mal brew install anything ausprobiert

```
Stefans-MacBook-Pro:~ stefan$ brew doctor
Your system is ready to brew.
Stefans-MacBook-Pro:~ stefan$ brew install virtualbox
Error: No available formula for virtualbox
Searching taps...
Stefans-MacBook-Pro:~ stefan$ VBoxManage --version
4.3.8r92456
Stefans-MacBook-Pro:~ stefan$ brew install vagrant
Error: No available formula for vagrant
Searching taps...
homebrew/completions/vagrant-completion
Stefans-MacBook-Pro:~ stefan$ brew install packer
Error: No available formula for packer
Searching taps...
homebrew/binary/packer
```

hm, da fehlen wohl einige brew Pakete... also dann manuell

* VirtualBox 4.3.8 von https://www.virtualbox.org/wiki/Downloads heruntergeladen und installiert
* Vagrant 1.4.3 von http://www.vagrantup.com/downloads.html heruntergeladen und installiert
* Packer 0.5.2 von http://www.packer.io/downloads.html heruntergeladen und installiert

```
cd Downloads/
cd 0
sudo mkdir /Applications/Packer
sudo cp pa* /Applications/Packer/
sudo ln -s /Applications/Packer/packer /usr/bin/packer
```

Da müssen aber noch mehr Symlinks erstellt werden. Vielleicht doch eher PATH erweitern

```
brew install vim --override-system-vi
sudo mv /usr/bin/vim /usr/bin/vim-off
sudo mv /usr/bin/vi /usr/bin/vi-off
brew install macvim
```

Meine Unix dotfiles eingespielt. Mal sehen, die habe ich bisher immer nur auf Ubuntu verwendet.

```
cd
mkdir code
cd code
git clone https://github.com/StefanScherer/dotfiles && cd dotfiles && ./sync.sh
```

* Systemeinstellungen -> Sicherheit -> Firewall eingeschaltet
* meanstack-ide frisch erstmalig gebaut. Fertig in 690 Sekunden, komplett aus dem Internet.
* Microsoft Remote Desktop App aus dem Mac App Store installiert
* Vagrant Plugins installiert

```
vagrant plugin install vagrant-cachier
vagrant plugin install vagrant-pristine
vagrant plugin install vagrant-vbox-snapshot
vagrant plugin install vagrant-windows
```

SSH Key eingespielt

## 2014-03-02

* Virtual Box Extension Pack (PUEL license) installiert von https://www.virtualbox.org/wiki/Downloads

## 2014-03-08

* Wireshark 1.10.6 heruntergeladen von http://www.wireshark.org/download.html und installiert
* XQuartz 2.7.5 X11 heruntergeladen von http://xquartz.macosforge.org/landing/ und installiert
* Node 0.10.26 heruntergeladen von http://nodejs.org/download/ und installiert

```
git clone https://github.com/dpree/jenkins-box
cd jenkins-box
sudo ./bootstrap.sh  oder doch ohne sudo?
```

Mit sudo hat er unter meinem User das .berkshelf Verzeichnis falsch erzeugt: sudo chown -R stefan .berkshelf

* grip installiert, Markdown to HTML

```
sudo easy_install pip
sudo pip install grip
```

## 2014-03-11

* Mavericks in einer VirtualBox
* Siehe hier http://www.robertsetiadi.net/install-os-x-virtualbox/

```
sudo gem install iesd
iesd -i InstallESD.dmg -o Mavericks.dmg -t BaseSystem
```

* Vagrant 1.5.0 von http://www.vagrantup.com/downloads.html heruntergeladen und installiert

```
$ vagrant up
Vagrant experienced a version conflict with some installed plugins!
This usually happens if you recently upgraded Vagrant. As part of the
upgrade process, some existing plugins are no longer compatible with
this version of Vagrant. The recommended way to fix this is to remove
your existing plugins and reinstall them one-by-one. To remove all
plugins:

    rm -r ~/.vagrant.d/plugins.json ~/.vagrant.d/gems

The error message is shown below:

Bundler could not find compatible versions for gem "celluloid":
  In Gemfile:
    vagrant-berkshelf (>= 0) ruby depends on
      celluloid (~> 0.14.0) ruby

    vagrant (= 1.5.0) ruby depends on
      celluloid (0.15.2)
```

Also nochmal schnell die Liste der Plugins ermittelt:

```
cat plugins.json | python -mjson.tool
sudo rm -rf .vagrant.d/gems .vagrant.d/plugins.json

vagrant plugin install vagrant-berkshelf
vagrant plugin install vagrant-cachier
vagrant plugin install vagrant-pristine
vagrant plugin install vagrant-vbox-snapshot
vagrant plugin install vagrant-windows
```

* vagrant-berkshelf lässt sich dennoch nicht installieren. Siehe auch https://sethvargo.com/the-future-of-vagrant-berkshelf/

## 2014-03-12

* Beim nächsten Packer Update versuche ich mal Homebrew aus. Das steht bei Mitch http://www.packer.io/intro/getting-started/setup.html

```
$ brew tap homebrew/binary
$ brew install packer
```

* VirtualBox 4.3.6 ausprobiert, ob damit Mavericks geht. Hängt aber auch beim Booten. Also wieder auf 4.3.8 hoch.
* Vagrant 1.5.0 meldet Warnungen wegen shared libs:

```
$ vagrant status
WARNING: Could not load IOV methods. Check your GSSAPI C library for an update
WARNING: Could not load AEAD methods. Check your GSSAPI C library for an update
WARNING: Nokogiri was built against LibXML version 2.8.0, but has dynamically loaded 2.9.1
```

## 2014-03-16

* Updates aus dem Mac App Store
* Command Line Dev Tool of OS X Version 5.1.0.0
* Xcode Version 5.1
* Microsoft Remote Desktop Version 8.0.5

## 2014-03-17

* Update Vagrant 1.5.0 -> 1.5.1 via Download

## 2014-03-19

* Node.js 0.10.26 installiert per Download von http://nodejs.org

## 2014-03-20

* `sudo npm install -g nodemon` -> nodemon 1.0.16
* Chrome Browser installiert
* Node und npm nochmal manuell entfernt
* Link: http://flummox-engineering.blogspot.de/2013/11/how-to-uninstall-package-pkg-in-mac-os-x.html

```bash
pkgutil --pkgs | grep -i node
cd /usr/local/
pkgutil --only-files --files org.nodejs.pkg | xargs sudo rm
pkgutil --only-files --files org.nodejs.node.npm.pkg | xargs sudo rm
curl -L https://raw.github.com/creationix/nvm/master/install.sh | sh
```

* Neues Terminal öffnen
* globale npm Module können nun ohne sudo installiert werden

```bash
nvm install v0.10.26
nvm alias default 0.10.26
npm install -g node-inspector
npm install -g jshint
npm install -g nodemon
```

* `nvm use 0.10.26`
* `npm install -g jsontool`
* `npm install -g js-beautify`
*

## 2014-03-27

* Meine Verzeichnisse geschützt

```
cd
chmod 700 code iso tmp bin
```

## 2014-04-06

* `brew install wakeonlan`

## 2014-04-13

* Installation Sublime Text 3 von http://www.sublimetext.com/3 bzw. [Sublime Text 3 Build 3059](http://c758482.r82.cf2.rackcdn.com/Sublime%20Text%20Build%203059.dmg)
* Link erzeugt, um `subl` aus der Kommandozeile aufrufen zu können. Siehe http://www.sublimetext.com/docs/2/osx_command_line.html

```
ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl ~/bin/subl
```

* User Preferences sind hier: `Library/Application\ Support/Sublime\ Text\ 3/Packages/User/Preferences.sublime-settings`

* Package Control installiert, nach Anleitung unter [https://sublime.wbond.net/installation](https://sublime.wbond.net/installation)
* Install Sublime Package Control (if you haven't done so already) from [here](http://wbond.net/sublime_packages/package_control) . Be sure to restart ST2 to complete the installation.

* Bring up the command palette (default `ctrl+shift+p` or `cmd+shift+p`) and start typing `Package Control: Install Package` then press return or click on that option to activate it. You will be presented with a new Quick Panel with the list of available packages. Type `GoSublime` and press return or on its entry to install GoSublime. If there is no entry for GoSublime, you most likely already have it installed.

## 2014-04-14

* [Installation Go 1.2.1](http://golang.org/doc/install#osx)
* Download [go1.2.1.darwin-amd64-osx10.8.pkg](https://code.google.com/p/go/downloads/detail?name=go1.2.1.darwin-amd64-osx10.8.pkg&can=2&q=OpSys-OSX+Type-Installer) und den Anweisungen folgen.
* In den dotfiles ist in .exports bereits `export GOPATH=$HOME/go` eingetragen.
* Nun nur noch ein `mkdir $HOME/go` auf dem Mac.
* `mkdir -p $GOPATH/src/github.com/StefanScherer`

## 2014-04-16

* [Install Mercurial 2.9.1](http://mercurial.selenic.com/downloads)

## 2014-04-20

* Developing packer

```
cd
cd go/src/github.com
mkdir mitchellh
cd mitchellh/
git clone git@github.com:StefanScherer/packer.git
cd packer/
git checkout packer-vcloud
git remote add upstream https://github.com/mitchellh/packer.git
```

* Install Bazaar with `brew install bzr`

## 2014-04-22

* Update VirtualBox auf 4.3.10
* Update Vagrant auf 1.5.4

## 2014-05-07

* Download [CUDA Driver 6.0.37](http://www.nvidia.de/object/macosx-cuda-6.0.37-driver-de.html)
* Download [Vagrant 1.6.0](https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.0.dmg)

```
$ vagrant --version
Vagrant 1.6.0

$ vagrant plugin list
vagrant-cachier (0.7.0)
vagrant-login (1.0.1, system)
vagrant-pristine (0.3.0)
vagrant-share (1.0.1, system)
vagrant-vbox-snapshot (0.0.4)
vagrant-windows (1.6.0)

$ vagrant plugin
Usage: vagrant plugin <command> [<args>]

Available subcommands:
     install
     license
     list
     uninstall
     update

For help on any individual command run `vagrant plugin COMMAND -h`

$ vagrant plugin update
Updating installed plugins...
Updated 'vagrant-cachier' to version '0.7.1'!

$ vagrant plugin uninstall vagrant-windows
Uninstalling the 'vagrant-windows' plugin...
```

## 2014-05-16

* Vagrant 1.6.2 installed

## 2014-05-22

* Installed HTTpie

If you want to do it from scratch, then:

```bash
install Homebrew on Mac
# http://brew.sh
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
brew doctor

# Install HTTPie on Mac
# https://gist.github.com/BlakeGardner/5586954
brew install python
pip install httpie
http
```

## 2014-05-24

* Syncthing: `go get github.com/calmh/syncthing/cmd/syncthing`
* jsonpp: `go get github.com/jmhodges/jsonpp`
  \*\* Then you can pretty print json responses: `curl -s http://localhost:8080/rest/config | jsonpp`

## 2014-05-29

* Update VirtualBox auf 4.3.12

## 2014-06-23

* `brew install htop`

## 2014-07-06

* Kid3 Tag Editor download from http://downloads.sourceforge.net/project/kid3/kid3/3.1/kid3-3.1.0-Darwin.dmg?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fkid3%2Ffiles%2F%3Fsource%3Dnavbar&ts=1404634152&use_mirror=cznic
* `sudo pip install buster`
* `brew install wget`

# 2014-07-15

* Licensed and installed vagrant-vmware-fusion plugin. Now it's time for a box in a box (in a box) ...

```
vagrant plugin install vagrant-vmware-fusion
vagrant plugin license vagrant-vmware-fusion license.lic
```

# 2014-07-16

* Changed vagrant snapshot plugin to support more providers

```
vagrant plugin uninstall vagrant-vbox-snapshot
vagrant plugin install vagrant-multiprovider-snap
```

# 2014-07-20

* Install Adobe Photoshop Lightroom 3.6 as my license is for both Win + Mac
* Interactive Download from http://www.adobe.com/support/downloads/detail.jsp?ftpID=5307

```
curl -O http://download.adobe.com/pub/adobe/lightroom/mac/3.x/Lightroom_3_LS11_mac_3_6.dmg
```

* Nice tip to update brew + cask: `brew update && brew upgrade brew-cask && brew cleanup && brew cask cleanup`

# 2014-07-23

* Use multiple SSH keys for Git access. See https://gist.github.com/jexchan/2351996
* `cat ~/.ssh/config`

```
Host github.com-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa-work
```

* Then you add the second private key and clone repos with different host name

```
ssh-add ~/.ssh/id_rsa-work
git clone git@github.com-work:org/repo
```

* List keys with `ssh-add -l`, delete all entries with `ssh-add -D`

# 2014-07-26

* Update VirtualBox by download from http://download.virtualbox.org/virtualbox/4.3.14/VirtualBox-4.3.14-95030-OSX.dmg

# 2014-08-11

* Update Vagrant Plugins

```
$ vagrant plugin list
vagrant-cachier (0.8.0)
vagrant-login (1.0.1, system)
vagrant-multiprovider-snap (0.0.11.my20140805)
  - Version Constraint: 0.0.11.my20140805
vagrant-omnibus (1.4.1)
vagrant-pristine (0.3.0)
vagrant-serverspec (0.1.0)
vagrant-share (1.1.0, system)
vagrant-vmware-fusion (2.4.1)
~
$ vagrant plugin update
Updating installed plugins...
Updated 'vagrant-cachier' to version '0.9.0'!
Updated 'vagrant-vmware-fusion' to version '2.5.2'!
$ vagrant plugin uninstall vagrant-multiprovider-snap
Uninstalling the 'vagrant-multiprovider-snap' plugin...
~/code/logbook on master*
$ vagrant plugin install vagrant-multiprovider-snap
Installing the 'vagrant-multiprovider-snap' plugin. This can take a few minutes...
Installed the plugin 'vagrant-multiprovider-snap (0.0.12)'!
```

# 2014-08-17

* Install Tiger VNC viewer

```bash
sudo chown stefan /usr/local/include
sudo chown stefan /usr/local/lib
sudo chown stefan /usr/local/share/man/man3
sudo chown stefan /usr/local/share/man/man5

brew link xz
brew install tiger-vnc
```

* Installs command `vncviewer`

# 2014-09-14

```
$ vagrant plugin update
Updating installed plugins...
Updated 'vagrant-share' to version '1.1.1'!
Updated 'vagrant-vmware-fusion' to version '3.0.1'!
```

* VirtualBox 4.3.16 installed from .dmg download
* Vagrant 1.6.5 installed from .dmg download

# 2014-09-21

* Update Packer 0.6.1 -> 0.7.1

```
brew uninstall packer
brew update
brew install packer
```

# 2014-09-25

* XCode 6.0.1 per Mac App Store installiert

# 2014-09-26

```
sudo xcodebuild -license
$ git --version
git version 1.9.3 (Apple Git-50)
```

* Git update as described in http://kj-prince.com/code/install-git-mac-osx-homebrew/

* Update XQuartz 2.7.7 via http://xquartz.macosforge.org/downloads/SL/XQuartz-2.7.7.dmg
* Update GitHub for Mac which has installed `/usr/local/bin/git` version 1.8.4
* removed links from /usr/local/bin/git

```
brew install git
brew link git
sudo rm /usr/local/bin/git*
sudo rm -r /usr/local/share/git-core/
rm -r /usr/local/share/man/man1/git*
rm -r /usr/local/share/man/man3/git*
rm -r /usr/local/share/man/man5/git*
rm -r /usr/local/share/man/man7/git*
sudo chown -R stefan /usr/local/lib/perl5/site_perl
rm -r /usr/local/lib/perl5/site_perl/Git
rm -r /usr/local/lib/perl5/site_perl/Git.pm
brew link git
$ git --version
git version 2.1.1
```

# 2014-09-26

* Enter [panamax.io](http://panamax.io)

```
brew install http://download.panamax.io/installer/brew/panamax.rb
panamax init
panamax
```

* List of [panamax commands](https://github.com/CenturyLinkLabs/panamax-ui/wiki/Panamax-Installer-Commands)

# 2014-09-30

* Update XQuartz 2.7.7 from dmg
* Installed `BashUpdateMavericks.dmg` to fix shellshock bash bug
* Install Atom with Homebrew

```
brew doctor
brew update
brew prune
brew install caskroom/cask/brew-cask
brew cask install atom
```

# 2014-10-01

```
$ vagrant plugin update
Updating installed plugins...
Updated 'vagrant-cachier' to version '1.0.0'!
Updated 'vagrant-multiprovider-snap' to version '0.0.13'!
Updated 'vagrant-share' to version '1.1.2'!
```

# 2014-10-03

```
brew install jq
```

# 2014-10-04

* Installed Atom syntax highlighter for Vagrant development

```
apm install language-powershell
apm install language-batch
```

# 2014-10-12

* Update Panamax to 0.3.0

```
brew upgrade http://download.panamax.io/installer/brew/panamax.rb && panamax reinstall
```

# 2014-10-17

* Update to OS X Yosemite
* Update VMware Fusion 6.0.5
* many other updates for Yosemite (iMove, Pages, Command Line Developer Tools, Numbers, GarageBand ...)

# 2014-10-21

* Update Xcode 6.1

# 2014-10-25

* Quartz 2.7.7 installed from dmg
* Wireshark 1.12.1 installed from dmg
* Checked that symlink exists `sudo ln -s /opt/X11 /usr/X11`
* To enabled Quartz X11 Retina display mode, see http://osxdaily.com/2012/01/12/enable-hidpi-mode-in-mac-os-x-lion/ but I haven't done it yet.

# 2014-11-01

* Update Microsoft Remote Desktop 8.0.10 (and catched download)
* `brew install exiftool`
* Say good bye to so funny words like `Sockelserver` instead of `Socketserver` and turned off the auto correction
* `Einstellungen -> Tastatur -> Text`, then uncheck the `Automatische Korrektur`
* Works on iPhone as well, same names there

# 2014-11-20

* VirtualBox 4.3.18 installed from .dmg download

# 2014-12-03

* VirtualBox 4.3.20 installed from .dmg download

# 2014-12-07

* Installed Disk Inventory X to clean up disk

```bash
brew update
brew cask install disk-inventory-x
```

# 2014-12-13

* Update homebrew-cask from 0.43 to 0.50

```bash
brew update
brew unlink brew-cask
brew install caskroom/cask/brew-cask
```

* Update packer 0.7.2 to 0.7.5

```bash
brew cask install packer
```

# 2014-12-20

* Update Vagrant 1.6.5 -> 1.7.1 by downloading dmg

```
$ vagrant plugin list
vagrant-multiprovider-snap (0.0.14)
vagrant-cucumber (0.0.8)
vagrant-login (1.0.1, system)
vagrant-omnibus (1.4.1)
vagrant-pristine (0.3.0)
vagrant-serverspec (0.1.0)
  - Version Constraint: 0.1.0
vagrant-share (1.1.2, system)
vagrant-vcloud (0.4.3)
vagrant-vmware-fusion (3.1.2)
```

# 2015-01-04

* Install `github-release` via [GitHub repo aktau/github-release](https://github.com/aktau/github-release)

```bash
go get github.com/aktau/github-release
```

# 2015-01-08

* Update Python and pip to install virtualenv

```bash
brew install python
pip install virtualenv
```

```bash
$ python --version
Python 2.7.9
$ pip --version
pip 1.5.6 from /usr/local/Cellar/python/2.7.9/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages/pip-1.5.6-py2.7.egg (python 2.7)
```

# 2015-01-09

* Installed `hub` the command line tool for GitHub via `brew install --HEAD hub`
* See [https://hub.github.com](https://hub.github.com)

# 2015-01-11

* Installed vagrant-triggers Plugin

```bash
vagrant plugin install vagrant-triggers
```

# 2015-01-12

* Installed VLC Player with `brew cask install vlc`, is in `~/Applications/VLC.app/Contents/MacOS/VLC`
* Installed Kodi (XMBC) to test IPTV

# 2015-01-13

* Installed `tree` with `brew install tree`

# 2015-01-15

* Installed SizeUp with `brew cask install sizeup`

# 2015-01-21

* Install Vagrant plugin `vagrant-hostmanager`

```bash
$ vagrant plugin list
vagrant-multiprovider-snap (0.0.14)
vagrant-cucumber (0.0.8)
vagrant-hostmanager (1.5.0)
vagrant-omnibus (1.4.1)
vagrant-pristine (0.3.0)
vagrant-reload (0.0.1)
vagrant-serverspec (0.5.0)
  - Version Constraint: 0.5.0
vagrant-share (1.1.4, system)
vagrant-triggers (0.5.0)
vagrant-vmware-fusion (3.2.0)
```

# 2015-01-28

* Update 10.10.2
* 1Password 5.1

# 2015-01-29

* `brew install ssh-copy-id` - then you can `ssh-copy-id user@remote && ssh user@remote`
* `brew install p7zip` to use `7za`
*

# 2015-02-07

* `brew install pv`
* `brew install pigz`
* `brew cask install macpass`

# 2015-02-18

* Update to VirtualBox 4.3.22

# 2015-02-23

* Installed Keybase.io

```bash
npm install -g keybase-installer
keybase-installer
```

# 2015-02-27

* installed `drone` command line tool
* `brew tap drone/drone`
* `brew install drone`

# 2015-03-06

* Update VirtualBox 4.3.24

# 2015-03-07

* `brew cask install fritzing`
* Downloaded Wireshark 1.99.3 - now without X11!

# 2015-03-11

* `brew install meld`

# 2015-03-13

* Install `docker-machine` from https://docs.docker.com/machine/
* `docker-machine create --driver virtualbox dev`
* `brew install docker` to install the Docker 1.5.0 client
* To point your Docker client at it, run this `$(docker-machine env dev)`
* See also http://flurdy.com/docs/docker/docker_compose_machine_swarm_cloud.html

# 2015-04-04

* Install Fritzing 0.9.2, now with Pi 2 Parts
* `brew cask install nosleep`

# 2015-04-10

* Download and update VirtualBox 4.3.26

# 2015-05-07

* Installed new Docker binaries:
* `brew install docker`
* `brew install docker-machine`
* `brew install docker-compose`

# 2015-05-09

* Update to VMware Fusion 7.1.1
* Next `vagrant up` shows this:

```
$ vagrant up esxi60 --provider vmware_fusion
Bringing machine 'esxi60' up with 'vmware_fusion' provider...
You're using a license that doesn't allow you to use the installed
version of Fusion. This error message occurs if you upgraded Fusion
without also upgrading your license. Please upgrade your license to
unlock features and support for the latest version of VMware Fusion,
or revert your version of Fusion back to the supported version.
You can upgrade your license by going to the following URL:

http://license.hashicorp.com/upgrade/vmware2014
```

* Purchased new Vagrant license
* `vagrant plugin license vagrant-vmware-fusion ~/Downloads/license.lic`

# 2015-05-13

* `go get github.com/vmware/govmomi/govc`

# 2015-05-16

* `brew install jingweno/ccat/ccat`
* `brew install pass`

# 2015-06-07

* Storing some secret tokens with `pass`
* `pass init scherer_stefan@icloud.com`
* `pass git init`
* `pass insert digital_ocean_token`
* `pass show digital_ocean_token`

# 2015-06-25

* Record Mac audio output with Soundflower
* `brew cask install soundflower`

# 2015-06-25

* Upgrade VMware Fusion 7.1.2

# 2015-07-03

* Upgrade packer 0.8.1 with `brew cask install packer`

# 2015-07-11

* Preparing update of Vagrant, still running 1.7.1 with these plugins

```
$ vagrant plugin list
vagrant-azure (1.1.1)
vagrant-multiprovider-snap (0.0.14)
vagrant-cucumber (0.0.10)
vagrant-digitalocean (0.7.4)
vagrant-esxi (0.0.1)
vagrant-hostmanager (1.5.0)
vagrant-omnibus (1.4.1)
vagrant-pristine (0.3.0)
vagrant-reload (0.0.1)
vagrant-serverspec (1.0.1)
vagrant-share (1.1.4, system)
vagrant-triggers (0.5.0)
vagrant-vmware-fusion (3.2.8)
vagrant-vsphere (1.0.1)
```

* Installed Vagrant 1.7.3 by downloading dmg
* Installed VirtualBox 5.0.0 by downloading dmg

# 2015-07-17

* Update Atom to version 1.0.2
* `go get -u github.com/golang/lint/golint`
* `go get -v code.google.com/p/rog-go/exp/cmd/godef`
* `go get golang.org/x/tools/cmd/goimports`
* `apm install go-plus`

# 2015-07-18

* `brew cask install vagrant` update to Version 1.7.4
* `brew cask install packer` update to Version 0.8.2

# 2015-08-05

* Update to IO.js 3.0.0 and nvm 0.25.4
* `brew install nvm`
* Updated dotfiles `.bash_profile`
* `nvm install iojs`
* `nvm alias default iojs`
* Update docker-compose to 1.3.3, docker client to 1.7.1
* `brew unlink fig && brew uninstall fig`
* `brew install docker-compose`

# 2015-08-06

* The Homebrew version of `docker-compose` shows SSL warnings. So I use the upstream release.
* `brew uninstall docker-compose`
* `curl -L https://github.com/docker/compose/releases/download/1.4.0rc3/docker-compose-`uname -s`-`uname -m`> /usr/local/bin/docker-compose`
* `chmod +x /usr/local/bin/docker-compose`

# 2015-08-14

* Installed new docker 1.8.1 and docker-machine 0.4.0 binaries:
* `brew update`
* `brew install docker`
* `brew install docker-machine`

# 2015-08-17

* Installed VirtualBox 5.0.2 by downloading dmg

# 2015-08-23

* Installed ImageMagick to add shadows to windows screenshots
* `brew install imagemagick`
* script `add-shadow`:

```bash
#!/bin/bash
convert $1 \( +clone -background black -shadow 120x30+0+20 \) +swap -background transparent -layers merge +repage "$1-shadow.png"
```

# 2015-09-09

* Update to Node.js 4.0.0

```
nvm install 4.0
nvm alias default node
nvm reinstall-packages iojs
npm install -g forany
```

# 2015-09-18

* Update docker 1.8.2, docker-machine 1.4.1 with Homebrew

# 2015-09-20

* Xcode 7.0, iTunes 12.3

# 2015-09-22

```
$ sudo gem install compass
Password:
Sorry, try again.
Password:
Fetching: sass-3.4.18.gem (100%)
Successfully installed sass-3.4.18
Fetching: compass-core-1.0.3.gem (100%)
Successfully installed compass-core-1.0.3
Fetching: compass-import-once-1.0.5.gem (100%)
Successfully installed compass-import-once-1.0.5
Fetching: chunky_png-1.3.4.gem (100%)
Successfully installed chunky_png-1.3.4
Fetching: rb-fsevent-0.9.6.gem (100%)
Successfully installed rb-fsevent-0.9.6
Fetching: rb-inotify-0.9.5.gem (100%)
Successfully installed rb-inotify-0.9.5
Fetching: compass-1.0.3.gem (100%)
Compass is charityware. If you love it, please donate on our behalf at http://umdf.org/compass Thanks!
Successfully installed compass-1.0.3
Parsing documentation for sass-3.4.18
Installing ri documentation for sass-3.4.18
Parsing documentation for compass-core-1.0.3
Installing ri documentation for compass-core-1.0.3
Parsing documentation for compass-import-once-1.0.5
Installing ri documentation for compass-import-once-1.0.5
Parsing documentation for chunky_png-1.3.4
Installing ri documentation for chunky_png-1.3.4
Parsing documentation for rb-fsevent-0.9.6
Installing ri documentation for rb-fsevent-0.9.6
Parsing documentation for rb-inotify-0.9.5
Installing ri documentation for rb-inotify-0.9.5
Parsing documentation for compass-1.0.3
Installing ri documentation for compass-1.0.3
7 gems installed
```

# 2015-09-28

* `brew install socat` ( http://kartoza.com/how-to-run-a-linux-gui-application-on-osx-using-docker/ )
* `socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"`

# 2015-10-03

* `brew install scw` - scaleway cli

# 2015-10-12

* `brew unlink hugo`
* `brew install hugo`

# 2015-10-13

* `brew install docker-compose`
* `brew link --overwrite docker-compose`

# 2015-10-16

* Download and update VirtualBox 5.0.6

# 2015-10-19

* Install Packer 0.8.6 `brew install packer`, removed old links from Caskroom

# 2015-10-23

* Update to OSX El Capitan
* Update GPG Keychain

# 2015-11-08

* Update docker 1.9.0, docker-machine 0.5.0, docker-compose 1.5.0 with brew

# 2015-11-12

* Compile docker-machine from source as new plugins could not be used with brew docker-machine 0.5.0

# 2015-11-14

* Update Atom 1.2.0
* Update VMware Fusion 7.1.3
* Update VirtualBox 5.0.10

# 2015-11-27

* `brew cask install docker-compose`
* `brew update && brew upgrade brew-cask && brew cleanup && brew cask cleanup`

# 2015-12-08

* Update to docker 1.9.1, docker-compose 1.5.2
* `brew cask update`
* `brew cask install docker-compose`

# 2015-12-21

* Update Vagrant 1.8.0

```
$ vagrant plugin list
```

* Plugins of Vagrant 1.7.4:

```
winrm (1.3.6)
winrm-fs (0.2.3)
vagrant-hostmanager (1.6.1)
vagrant-multiprovider-snap (0.0.14)
vagrant-pristine (0.3.0)
vagrant-share (1.1.4, system)
vagrant-triggers (0.5.2)
vagrant-vmware-fusion (4.0.2
```

* `mv .vagrant.d vagrant-d-174`
* download latest Vagrant 1.8.0 dmg
* `vagrant --version`
* `cp vagrant-d-174/licens* .vagrant.d`
* `cp vagrant-d-174/Vagrantfile .vagrant.d`
* Add workaround for VMware Fusion 7.1.3 (only Professional has linked clones)
* `vi .vagrant.d/Vagrantfile`

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "vmware_fusion" do |v|
    v.linked_clone = false
  end
...
end
```

```
$ vagrant plugin list
vagrant-share (1.1.5, system)
vagrant-vmware-fusion (4.0.5)
```

# 2016-01-03

* Update docker-machine
* `brew update; brew cleanup; brew cask cleanup`
* `brew uninstall --force brew-cask; brew update`
* `brew cask uninstall docker-machine`
* `brew cask install docker-machine`
* Update go 1.5.1 -> 1.5.2
* `brew unlink go`
* `brew install go`

# 2016-01-04

* Downgraded Vagrant back to 1.7.4 due to a problem with the OSX Vagrant box, see https://github.com/mitchellh/vagrant/issues/6792

# 2016-01-07

* `sudo gem install travis`

# 2016-01-22

* Update VirtualBox 5.0.14

# 2016-01-31

* `brew install azure-cli`

# 2016-02-04

* `brew install watch`

# 2016-02-06

* Update docker 1.10, docker-compose 1.6, docker-machine 0.6

# 2016-02-11

* Install `shellcheck` and Atom linter
* `apm install linter`
* `apm install linter-shellcheck`
* `brew install shellcheck`

# 2016-02-19

* Update Vagrant 1.7.4 to 1.8.1

```
$ vagrant plugin list
vagrant-share (1.1.5, system)
vagrant-vmware-fusion (4.0.8)
```

* Update packer to 0.9.0-rc2

# 2016-02-22

* Update packer to 0.9.0

# 2016-03-03

* Update VMware Fusion Pro 8.1.0

# 2016-04-15

* `brew cask install wireshark`

# 2016-04-27

* Update VMware Fusion Pro 8.1.1

# 2016-05-06

* Fix scaleway-cli. A brew install scw didn't work, json parse error, the same for go get ...
* brew uninstall scw

```
# prepare for first install and upgrade
mkdir -p /usr/local/bin
mv /usr/local/bin/scw /tmp/scw.old

# get latest release
wget "https://github.com/scaleway/scaleway-cli/releases/download/v1.9.0/scw_1.9.0_darwin_amd64.zip" -O /tmp/scw.zip
unzip /tmp/scw.zip \*/scw -d /tmp
mv /tmp/scw_*/scw /usr/local/bin
rm -rf /tmp/scw.zip /tmp/scw_*_darwin_amd64

# test
scw version
```

# 2016-05-15

* Update packer 0.10.1

```
wget https://releases.hashicorp.com/packer/0.10.1/packer_0.10.1_darwin_amd64.zip
unzip packer_0.10.1_darwin_amd64.zip
mv packer /usr/local/bin/
```

# 2016-06-01

* Update some vagrant plugins

```
$ vagrant plugin list
vagrant-azure (1.3.0)
vagrant-digitalocean (0.8.0)
vagrant-multiprovider-snap (0.0.14)
vagrant-pristine (0.3.0)
vagrant-reload (0.0.1)
vagrant-share (1.1.5, system)
vagrant-vmware-fusion (4.0.8)
~
$ vagrant plugin update
Updating installed plugins...
Updated 'vagrant-digitalocean' to version '0.9.0'!
Updated 'vagrant-vmware-fusion' to version '4.0.9'!
```

# 2016-06-09

* Install ODROID UART KIT driver
* From http://www.silabs.com/Support%20Documents/Software/Mac_OSX_VCP_Driver.zip
* http://forum.odroid.com/viewtopic.php?f=53&t=841
* ODROID: `screen /dev/tty.SLAB_USBtoUART 115200`
* Adafruit RPi: `screen /dev/cu.usbserial 115200`

# 2016-06-19, DockerCon

* `brew install mosh`
* `brew install httping`

# 2016-07-09

* After serveral tests with Vagrant 1.8.4 + winrm-fs 0.4.3 I gave up and installed Vagrant 1.8.1, but this also wasn't so easy as Win10/TP5 VM's abort provisioning.
* Install Vagrant 1.8.1 with standard winrm-fs 0.2.3
* Trick in provision script of Chocolatey is to `rm $PROFILE` to remove Chocolatey module

# 2016-07-29

* Removed my last docker-machine: `docker-machine rm -f dev`
* `brew upgrade`
* `brew uninstall docker`
* `brew uninstall docker-machine`
* `brew uninstall docker-compose`
* Installed Docker for Mac 1.12 from https://www.docker.com/products/docker#/mac

# 2016-08-30

* Update Node.js 6.5.0 with `nvm`

# 2016-08-31

* Install Azure CLI again
* `npm install -g azure-cli`

# 2016-09-14

* Update VMware Fusion Pro 8.5

# 2016-09-21

* Update Homebrew 1.0.0

```
$ brew update
$ sudo chown root:wheel /usr/local
$ brew --version
```

* Update to macOS Sierra 10.12

# 2016-09-25

* `brew upgrade`
* Update packer 0.10.2 for Sierra with
* `brew install packer`

# 2016-09-26

* Update VirtualBox 5.0.26

# 2016-10-07

* Update Vagrant 1.8.6
* Before: Vagrant 1.8.1:

```
$ vagrant plugin list
winrm (1.3.6)
vagrant-cucumber (0.1.1)
vagrant-multiprovider-snap (0.0.14)
vagrant-reload (0.0.1)
vagrant-serverspec (1.1.1)
vagrant-share (1.1.5, system)
vagrant-vmware-fusion (4.0.11)
```

* After: Vagrant 1.8.6

```
$ vagrant plugin list
vagrant-cucumber (0.1.1)
vagrant-multiprovider-snap (0.0.14)
vagrant-reload (0.0.1)
vagrant-serverspec (1.1.1)
vagrant-share (1.1.5, system)
vagrant-vmware-fusion (4.0.13)
```

# 2016-10-31

* Update VMware Fusion Pro 8.5.1
* Update VirtualBox 5.1.8

# 2016-11-05

* Update Scaleway cli 1.11

```
brew install scw
brew link --overwrite scw
```

* Install XQuartz 2.7.11

```
brew cask install xquartz
```

Using X11 from a VM: https://learning-continuous-deployment.github.io/docker/images/dockerfile/2015/04/22/docker-gui-osx/

```
socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
```

# 2016-11-10

* Update Vagrant 1.8.7

```
sudo mv /opt/homebrew-cask/Caskroom/ /usr/local/Caskroom
brew cask uninstall --force vagrant && brew cask install vagrant
$ vagrant plugin list
vagrant-cucumber (0.1.1)
vagrant-multiprovider-snap (0.0.14)
vagrant-reload (0.0.1)
vagrant-serverspec (1.1.1)
vagrant-share (1.1.5, system)
vagrant-vmware-fusion (4.0.14)
```

* Update Wireshark 2.2.1

```
brew cask uninstall --force wireshark && brew cask install wireshark
```

# 2016-11-14

* Update `travis`: `gem install travis`
* Update VMware Fusion 8.5.2

# 2016-11-15

* Fix problem with Vagrant 1.8.7

```
sudo rm /opt/vagrant/embedded/bin/curl
```

# 2016-11-30

* Update VMware Fusion Pro 8.5.3

# 2016-12-08

* Update Vagrant 1.8.7 -> 1.9.1

```
$ vagrant plugin list
vagrant-cucumber (0.1.1)
vagrant-multiprovider-snap (0.0.14)
vagrant-reload (0.0.1)
vagrant-serverspec (1.1.1)
vagrant-share (1.1.5, system)
vagrant-vmware-fusion (4.0.14)
```

* `brew cask reinstall vagrant`

```
$ vagrant version
Installed Version: 1.9.1
Latest Version: 1.9.1

 You're running an up-to-date version of Vagrant!
 ~
 $ vagrant plugin list
 vagrant-multiprovider-snap (0.0.14)
 vagrant-reload (0.0.1)
 vagrant-serverspec (1.1.1)
 vagrant-share (1.1.6, system)
 vagrant-vmware-fusion (4.0.15)
```

# 2016-12-12

* `brew install terraform` Version 0.7.13

# 2016-12-14

* `brew upgrade packer` to Packer 0.12.0

# 2016-12-21

* Update VirtualBox 5.1.12 (download dmg)
* `brew upgrade packer` to Packer 0.12.1
* `brew upgrade terraform` to Terraform 0.8.1

# 2016-12-23

* Install Visual Studio Code
* `brew cask install visual-studio-code`

# 2016-12-31

* Install VirtualBox Extension Pack 5.1.12
* Downgrade Packer 0.12.1 -> 0.12.0

```
$ brew list --versions packer
packer 0.10.2 0.12.0 0.12.1
$ brew switch packer 0.12.0
```

# 2017-01-17

* Disk Inventory X was lost, reinstall it

```bash
brew cask install disk-inventory-x
```

* Open Finder, right click Disk Inventory X edit settings to Open in Low Resolution

# 2017-01-19

* Update Docker for Mac 1.13.0

# 2017-01-22

* Update Terraform 0.8.4
* `brew upgrade terraform`

# 2017-02-18

* Install UNetbootin

```
brew install Caskroom/cask/unetbootin
```

# 2017-03-01

* Update Vagrant 1.9.2

```
$ vagrant plugin list
vagrant-multiprovider-snap (0.0.14)
vagrant-reload (0.0.1)
vagrant-serverspec (1.1.1)
vagrant-share (1.1.6, system)
vagrant-vmware-fusion (4.0.15)
$ mv .vagrant.d/ vagrant-d-191
$ brew update
$ brew cask reinstall vagrant
$ rmdir .vagrant.d/boxes/
$ mv vagrant-191/boxes/ .vagrant.d/
$ vagrant plugin install vagrant-vmware-fusion
$ vagrant plugin install vagrant-reload
$ vagrant plugin install vagrant-mulitprovider-snap
$ vagrant plugin list
vagrant-multiprovider-snap (0.0.14)
vagrant-reload (0.0.1)
vagrant-share (1.1.7, system)
vagrant-vmware-fusion (4.0.17)
$ mv vagrant-191/license-vagrant-vmware-fusion.lic .vagrant.d/
$ mv vagrant-191/Vagrantfile .vagrant.d/
```

# 2017-03-02

* Update Packer 0.12.3

```
$ brew unlink packer
$ brew install packer
```

* Update Docker for Mac 17.03.0-ce

# 2017-03-11

* Update VMware Fusion Pro 8.5.4

# 2017-03-14

* Update VMware Fusion Pro 8.5.5
* Install Ink2Go

# 2017-03-29

* Update terraform 0.9.2
* Update VMware Fusion Pro 8.5.6

# 2017-04-26

* Install Codeship jet CLI

```
brew cask install jet
```

# 2017-05-02

* Update VirtualBox 5.1.22

# 2017-05-03

* Update Packer 1.0.0, Vagrant 1.9.4

```
brew upgrade packer
brew cask reinstall vagrant
```

* Update vagrant-vmware-fusion plugin 4.0.19

```
vagrant plugin update
```

# 2017-05-19

* Update VMware Fusion Pro 8.5.7

# 2017-06-05

* Update Scaleway cli to 1.13

```
brew upgrade scw
```

# 2017-06-07

* Install new Azure CLI

```
curl -L https://aka.ms/InstallAzureCli | bash
```

* Update Terraform 0.9.6

```
brew install terraform
brew link --overwrite terraform
```

# 2017-06-27

* Update VMware Fusion 8.5.8

# 2017-07-05

* Update docker-machine manually to 0.12.1 to fix nasty version check bug

```
rm /usr/local/bin/docker-machine
curl -L https://github.com/docker/machine/releases/download/v0.12.1/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine &&   chmod +x /usr/local/bin/docker-machine
```

# 2017-07-08

* Update Vagrant 1.9.7

```
brew cask reinstall vagrant
vagrant plugin install vagrant-mware-fusion
vagrant plugin install vagrant-reload
```

* Update packer 1.0.2

```
brew upgrade packer
```

# 2017-08-27

* Update 1Password 6.8.1
* Update Docker for Mac 17.06.1
* Update Packer 1.0.4, Vagrant 1.9.8, vagrant-vmware-fusion 4.0.24

```
brew upgrade packer
brew cask reinstall vagrant
vagrant plugin update
```

* Update Atom 1.19.3
* Update VirtualBox 5.1.26

# 2017-09-07

* OMG, docker-machine 0.12.0 again, this was Docker for Mac 17.06.1 :-(
* Update Docker for Mac 17.06.2, now with fix docker-machine 0.12.2

# 2017-09-09

* Install screen recorder Kap

```
brew update
brew cask install kap
```

# 2017-09-11

* Install gifsicle to scale down Retina GIF for Twitter and blog posts. (`gifsicle --scale 0.5x0.5 retina.gif -o rdy2tweet.gif`)

```
brew install gifsicle
```

# 2017-09-18

* Update Packer 1.1.0, Vagrant 2.0.0, vagrant-vmware-fusion 4.0.24

```
brew upgrade packer
brew cask reinstall vagrant
vagrant plugin update
```

# 2017-10-03

* Update Docker for Mac 17.09.0-ce with docker-machine 0.12.2
* Update MacOS High Sierra

# 2017-10-05

* Update hub 2.2.9

```
brew unlink hub
brew install hub
```

# 2017-10-06

* Cleanup VMware NAT -> empty `[incomingtcp]` in

```
sudo vi /Library/Preferences/VMware Fusion/vmnet8/nat.conf
```

# 2017-10-13

* Install telnet for port checks

```
brew install telnet
```

# 2017-10-18

* Update VMware Fusion 10.0.1
* Update Vagrant VMware Fusion Plugin 5.0.0
* Update Packer 1.1.1

# 2017-10-24

* Install SizeUp (again)

```
brew cask install sizeup
```

# 2017-11-08

* Update Vagrant 2.0.1

```
$ brew update
$ brew cask reinstall vagrant
$ mv .vagrant.d/ vagrant-d-200
$ vagrant version
$ rmdir .vagrant.d/boxes/
$ mv vagrant-d-200/boxes/ .vagrant.d/
$ cp vagrant-d-200/license-vagrant-vmware-fusion.lic .vagrant.d/
$ vagrant plugin install vagrant-vmware-fusion
$ vagrant plugin install vagrant-reload
$ vagrant plugin list
vagrant-reload (0.0.1)
vagrant-share (1.1.9, system)
vagrant-vmware-fusion (5.0.3)
```

# 2017-11-28

* Set password for root user

# 2017-12-01

* Update Packer 1.1.2

```
brew upgrade packer
```

# 2017-12-03

* Upgrade Golang 1.9.2

```
brew upgrade golang
```

* Install docker registry v2 command line client

```
go get github.com/jessfraz/reg
```

# 2017-12-10

* Update VMware Fusion Plugin 5.0.4

```
$ vagrant plugin update
Updating installed plugins...
Fetching: vagrant-vmware-fusion-5.0.4.gem (100%)
Building native extensions.  This could take a while...

Vagrant is installing the VMware plugin which requires
root access. You may be prompted for your password to
complete setup.

Password:
Successfully uninstalled vagrant-vmware-fusion-5.0.3
Updated 'vagrant-share' to version '1.1.9'!
Updated 'vagrant-vmware-fusion' to version '5.0.4'!
```

# 2017-12-15

* Update Packer 1.1.3

```
brew upgrade packer
```

# 2017-12-16

* Update VirtualBox 5.2.2 (download)

# 2017-12-23

* Install Node 8.9.3

```
nvm install 8.9.3
nvm alias default 8.9.3
```

* Install Yarn

```
brew install yarn --without-node
```

* Update bundler

```
sudo gem install bundler
```

# 2017-12-26

* Update VMware Fusion Pro 10.1.0
* Update VirtualBox 5.2.4

# 2018-01-07

* Update Azure CLI, Python 3, ...

```
brew install azure-cli
```

# 2018-01-10

* Update Docker Compose 1.18.0

```
rm /usr/local/bin/docker-compose
brew install docker-compose
docker-compose version
```

# 2018-01-11

* Update VMware Fusion Pro 10.1.1
* Update Docker for Mac 17.12.0-ce-mac46

# 2018-01-31

* Install Keycastr to record/show keystrokes in kap screen recordings

```
brew cask install keycastr
```

# 2018-02-01

* Update Kap to version 2.0.0

# 2018-02-08

* Install UniFi 5.6.29 Controller from https://downloads.ubnt.com/unifi

# 2018-02-11

* Update Packer 1.2.0

```
brew upgrade packer
```

* Update Vagrant 2.0.2

```
$ brew cask reinstall vagrant
$ mv .vagrant.d/ vagrant-d-202
$ vagrant version
$ mv vagrant-d-202/boxes/ .vagrant.d/
$ cp vagrant-d-202/license-vagrant-vmware-fusion.lic .vagrant.d/
$ vagrant plugin install vagrant-vmware-fusion
$ vagrant plugin install vagrant-reload
$ vagrant plugin list
vagrant-reload (0.0.1)
vagrant-vmware-fusion (5.0.4)
```

# 2018-02-13

* Install Ghostscript, gv, mupdf

```
brew install gs
brew install gv
brew install mupdf
```

* Downgrade Packer to 1.1.3, as version 1.2.0 has HIGH CPU load

```
brew switch packer 1.1.3
```

# 2018-02-14

* Update ImageMagick

```
brew upgrade imagemagick
```

# 2018-02-15

* Update Git to 2.16.0

```
brew upgrade git
```

# 2018-02-16

* Soundflower updated from https://www.fluxforge.com/blog/soundflower-os-x-10.11-10.12-macOS-sierra/

# 2018-02-17

* Repair Vagrant VMware plugin 5.0.4

```
vagrant plugin uninstall vagrant-vmware-fusion
vagrant plugin install vagrant-vmware-fusion
```

# 2018-03-07

* Update Packer 1.2.1

```
brew upgrade packer
```

# 2018-03-08

* Update VirtualBox 5.2.8
* Revert to Packer 1.1.3

```
brew switch packer 1.1.3
```

# 2018-03-12

* Update docker-machine 0.14.0 as 0.13.0 creates wrong certs

```
rm /usr/local/bin/docker-machine
brew install docker-machine
```

* Update WireShark

```
$ rm -rf /Applications/Wireshark.app /usr/local/Caskroom/wireshark
$ sudo /usr/sbin/dseditgroup -o delete access_bpf
# Now brew thinks it's been uninstalled due to missing .app & cask dir
$ brew cask uninstall wireshark
Error: Cask 'wireshark' is not installed.
Error: Uninstall incomplete.
# Install & re-install now work!
$ brew cask install wireshark
```

# 2018-03-16

* Install OpenShift CLI

```
brew install openshift-cli
```

# 2018-03-17

* Allow VMware Fusion Promiscuous Mode on macOS.
  Needed for enabling Docker Swarm mode in headless Windows Docker machines.

```
sudo touch "/Library/Preferences/VMware Fusion/promiscAuthorized"
```

# 2018-03-21

* Update Azure CLI 2.0.29

```
brew upgrade azure-cli
```

# 2018-03-28

* Update Vagrant 2.0.3

```
brew cask reinstall vagrant
```

* Cleaning Vagrant plugins

```
$ mv .vagrant.d/ vagrant202
$ vagrant plugin list
$ rmdir .vagrant.d/boxes/
$ mv vagrant202/boxes/ .vagrant.d/
```

* Install Vagrant VMware Utility
  * Download from https://www.vagrantup.com/vmware/downloads.html
* Install Vagrant VMware Desktop plugin

```
vagrant plugin install vagrant-vmware-desktop
```

* Installing other Vagrant plugins

```
vagrant plugin install vagrant-reload
```

* License the plugin

```
vagrant plugin license vagrant-vmware-desktop ~/Desktop/license.lic
```

# 2018-04-27
* Update Vagrant 2.0.4
```
$ brew cask reinstall vagrant
$ vagrant plugin repair
$ vagrant plugin list
vagrant-reload (0.0.1)
vagrant-vmware-desktop (1.0.3)
```
* Update Packer 1.2.3
```
$ brew upgrade packer
```

# 2018-05-02
* Update Docker for Mac Version 18.03.1-ce

# 2018-05-26
* Update Royal TSX 3.3

# 2018-06-02
* Document how to use the Trackpad without noisy clicking it.

* Trackpad -> Klick durch Tippen
![Trackpad](images/trackpad1.png)

* Bedienungshilfen -> Maus & Trackpad -> Trackpad-Optionen -> Bewegungen aktivieren
![Bedienungshilfen](images/trackpad2.png)

# 2018-06-10
* Install Duet Display from duetdisplay.com

# 2018-06-17
* Update 1Password 7

# 2018-06-22
* Intall 1Password command-line tool `op` from https://app-updates.agilebits.com/product_history/CLI

# 2018-07-07
* Update VMware Fusion Pro 10.1.2

# 2018-07-17
* Update Azure CLI 2.0.29 to 2.0.41
```
brew upgrade azure-cli
```

# 2018-07-18
* Update Vagrant 2.1.2, VMware plugin 1.0.4
```
$ vagrant plugin list
vagrant-reload (0.0.1)
vagrant-vmware-desktop (1.0.3)

$ vagrant --version
Vagrant 2.0.4

$ brew cask reinstall vagrant

$ vagrant plugin update
Updating installed plugins...
Fetching: vagrant-vmware-desktop-1.0.4.gem (100%)
Successfully uninstalled vagrant-vmware-desktop-1.0.3
Updated 'vagrant-vmware-desktop' to version '1.0.4'!
```

# 2018-07-21
* Update VIM to 8.1
```
brew upgrade vim
mv .vim .vim-old
mv .vimrc .vimrc-old
mv .viminfo .viminfo-old
```

# 2018-07-30
* Update Docker CE 18.06.0-ce

# 2018-08-04
* Cleanup brew cask
```
brew cask list
cd /usr/local/Caskroom/
rm -r docker-compose
rm -r docker-machine
rm -r packer
rm -r vault
brew cask ls
```

* brew cask ls
```
$ brew cask ls
atom
disk-inventory-x
docker
handbrake
jet
kap
keybase
keycastr
macpass
nosleep
real-vnc
sizeup
soundflower
tunnelblick
unetbootin
vagrant
vagrant-manager
visual-studio-code
vlc
wireshark
xquartz
```

* brew ls -full-name
```
$ brew ls --full-name
asciinema
atk
autoenv
awscli
azure-cli
bats
bazaar
bdw-gc
bison
boot2docker
cairo
cask
cmake
cscope
docker
docker-compose
docker-machine
dockviz
dosbox
emacs
exiftool
fltk
fontconfig
freetype
gd
gdbm
gdk-pixbuf
gettext
ghostscript
gifsicle
git
glib
gmp
gnu-getopt
gnupg
gnutls
go
gobject-introspection
graphviz
gsettings-desktop-schemas
gtk+
gtk+3
gtk-mac-integration
gtksourceview
gv
harfbuzz
hicolor-icon-theme
htop
httping
hub
hugo
icu4c
imagemagick
intltool
jpeg
jpeg-turbo
jq
libcroco
libepoxy
libffi
libogg
libpng
librsvg
libtasn1
libtiff
libtool
libunistring
libvorbis
libyaml
little-cms2
lynx
macvim
mercurial
minicom
mitmproxy
mosh
mupdf
nasm
nettle
nmap
nvm
oniguruma
openshift-cli
openssl
p11-kit
p7zip
packer
pango
pass
pcre
perl
pigz
pixman
pkg-config
protobuf
pv
pwgen
py2cairo
pygobject
pygtk
pygtksourceview
python
python@2
qrencode
rarian
readline
ruby
scw
sdl
sdl_net
sdl_sound
shellcheck
socat
sphinx-doc
sqlite
ssh-copy-id
telnet
terraform
tiger-vnc
tree
unrar
urlview
vim
w3m
wakeonlan
watch
wdiff
webp
wget
xz
yarn
drone/drone/drone
```

# 2018-08-05
* Install Vagrant VMware Utility 1.0.3
```
brew cask install vagrant-vmware-utility
```

# 2018-08-15
* Update VMware Fusion Pro 10.1.3
* Update Microsoft Office
* Update Packer 1.2.5
```
brew upgrade packer
```

# 2018-09-10
* Update Docker 18.06.1-ce
* Update jet 2.6.1, keycastr 0.9.6, unetbootin 661, vagrant 2.1.4, vagrant-vmware-utility 1.0.4, wireshark 2.6.3
```
brew cask upgrade
```
* Update gtksourceview 2.10.5_1 -> 2.10.5_3, mosh 1.2.6_2 -> 1.3.2_3, minicom 2.7 -> 2.7.1, openshift-cli 3.7.1 -> 3.10.0, gtk+ 2.24.31 -> 2.24.32_2, vim 8.1.0200 -> 8.1.0350, terraform 0.11.7 -> 0.11.8, libtiff 4.0.9_1 -> 4.0.9_4, pv 1.6.0 -> 1.6.6, gmp 6.1.2_1 -> 6.1.2_2, wget 1.18 -> 1.19.5, autoenv 0.2.0 -> 0.2.1, w3m 0.5.3 -> 0.5.3_5, pigz 2.3.3 -> 2.4, docker 17.12.0 -> 18.06.1, exiftool 10.20 -> 11.01, python@2 2.7.14_3 -> 2.7.15_1, lynx 2.8.8rel.2_1 -> 2.8.9rel.1, go 1.9.2 -> 1.11, azure-cli 2.0.41 -> 2.0.45, libpng 1.6.34 -> 1.6.35, hugo 0.18 -> 0.48, ghostscript 9.22 -> 9.24, gtk+3 3.20.9 -> 3.22.30, pixman 0.34.0 -> 0.34.0_1, gdbm 1.16 -> 1.18, mitmproxy 3.0.4 -> 4.0.4, cmake 3.6.2 -> 3.12.2, freetype 2.9 -> 2.9.1, p7zip 16.02 -> 16.02_1, pass 1.7.1 -> 1.7.2, libvorbis 1.3.5_1 -> 1.3.6, libunistring 0.9.8 -> 0.9.10, pango 1.40.3 -> 1.42.4, pygtk 2.24.0_1 -> 2.24.0_2, gdk-pixbuf 2.34.0 -> 2.38.0, bdw-gc 7.6.0 -> 7.6.8, icu4c 57.1 -> 62.1, atk 2.20.0 -> 2.30.0, harfbuzz 1.3.0 -> 1.8.8, glib 2.48.2 -> 2.58.0_1, nasm 2.12.02 -> 2.13.03, awscli 1.10.66 -> 1.16.10, urlview 0.9 -> 0.9-20, cairo 1.14.6_1 -> 1.14.12, webp 0.6.0 -> 1.0.0, gobject-introspection 1.48.0 -> 1.58.0, dosbox 0.74_1 -> 0.74-2, yarn 1.3.2 -> 1.9.4, nvm 0.33.0 -> 0.33.11, emacs 25.1 -> 26.1_1, fontconfig 2.12.1_2 -> 2.13.1, htop 0.8.2.8 -> 2.2.0, gtk-mac-integration 2.0.8 -> 2.1.2, macvim 8.0-110 -> 8.1-151, dockviz 0.5.0 -> 0.6.3, libcroco 0.6.11 -> 0.6.12, pygtksourceview 2.10.1_1 -> 2.10.1_3, gifsicle 1.90 -> 1.91, librsvg 2.40.16_1 -> 2.42.2_2, mercurial 3.9.1 -> 4.7.1, pwgen 2.07 -> 2.08, sphinx-doc 1.7.6 -> 1.7.9, tiger-vnc 1.8.0 -> 1.9.0, unrar 5.4.5 -> 5.6.6, asciinema 1.3.0 -> 2.0.1_1, mupdf 1.12.0 -> 1.13.0, hicolor-icon-theme 0.15 -> 0.17, watch 3.3.12 -> 3.3.15, oniguruma 6.4.0 -> 6.9.0, gd 2.2.4_1 -> 2.2.5, qrencode 4.0.0 -> 4.0.2, py2cairo 1.10.0_1 -> 1.17.1, cask 0.8.0 -> 0.8.4, pcre 8.39 -> 8.42, libepoxy 1.3.1 -> 1.5.2, scw 1.14 -> 1.17, bazaar 2.7.0 -> 2.7.0_1, docker-compose 1.18.0 -> 1.22.0_1, jpeg 9b -> 9c, nmap 7.12 -> 7.70, ssh-copy-id 7.3p1 -> 7.8p1, jq 1.5_2 -> 1.5_3, openssl 1.0.2o_2 -> 1.0.2p, imagemagick 7.0.7-22 -> 7.0.8-11_1, gnupg 1.4.21 -> 2.2.10, bison 3.0.4 -> 3.1, p11-kit 0.23.9 -> 0.23.14, pygobject 2.28.6_1 -> 2.28.7_1, protobuf 3.5.1_1 -> 3.6.0, git 2.17.1 -> 2.18.0, telnet 54.50.1 -> 60, jpeg-turbo 1.5.3 -> 2.0.0, gnutls 3.5.18 -> 3.5.19, gsettings-desktop-schemas 3.20.0 -> 3.28.1
```
brew upgrade
```

# 2018-10-09
* Update Vagrant 2.1.5, vagrant-vmware-desktop 2.0.0
```
brew cask reinstall vagrant
vagrant plugin update
brew cask reinstall vagrant-vmware-utility
```
* Update Packer 1.3.1
```
brew upgrade packer
```

# 2018-10-23
* Update macOS Mojave

# 2018-11-01
* Update Vagrant 2.2.0, Vagrant VMware Utility 1.0.5, WireShark
```
brew cask upgrade
```
* Update VMware Fusion Pro 11.0
* Update Vagrant plugins
```
vagrant plugin update
```
* Fix VMware Utility 1.0.5
```
sudo chmod 755 /opt/vagrant-vmware-desktop/
```
* Updated Vagrant VMware plugin license
```
vagrant plugin license vagrant-vmware-desktop ~/Downloads/license.lic
```
* Update Docker Community Edition 18.06.1-ce-mac73 from stable channel

# 2018-11-11
* Update VMware Fusion Pro 11.0.1

# 2018-11-12
* Update VirtualBox 5.2.20
```
brew cask reinstall virtualbox
```

# 2018-11-18
* Update macOS 10.14.1

# 2018-11-19
* Update Docker 2.0.0.0

# 2018-11-25
* Update VMware Fusion Pro 11.0.2
* Installed `dive` - A tool for exploring each layer in a docker image
```
brew tap wagoodman/dive
brew install dive
```

# 2018-12-09
* Update Vagrant 2.2.2
```
brew update
brew cask reinstall vagrant
```
* Update Vagrant VMware Desktop Plugin 2.0.2
```
vagrant plugin update
```
* Update Vagrant Vmware Utility 1.0.6
```
brew cask reinstall vagrant-vmware-utility
```
* Update Packer 1.3.3
```
brew upgrade packer
```

# 2019-01-13
* Remove nvm
```
brew uninstall --force nvm
rm -rf ~/.nvm
```

# 2019-01-15
* Update Docker Desktop 2.0.0.2

# 2019-01-24
* Update Vagrant VMware Desktop plugin 2.0.3
```
$ vagrant plugin update
Updating installed plugins...
Fetching: vagrant-vmware-desktop-2.0.3.gem (100%)
Successfully uninstalled vagrant-vmware-desktop-2.0.2
Updated 'vagrant-vmware-desktop' to version '2.0.3'!
```
* Update Vagrant 2.2.3
```
brew cask reinstall vagrant
```

# 2019-03-03
* Install Inspec
```
brew cask install chef/chef/inspec
```
* Install Packer 1.3.5
```
rm /usr/local/bin/packer 
wget https://releases.hashicorp.com/packer/1.3.5/packer_1.3.5_darwin_amd64.zip
unzip packer_1.3.5_darwin_amd64.zip 
mv packer /usr/local/bin/
rm packer_1.3.5_darwin_amd64.zip 
```

# 2019-03-05
* Update Vagrant 2.2.4
```
brew cask reinstall vagrant
```

# 2019-04-14
* Update VMware Fusion Pro 11.0.3

# 2019-05-13
* Update VMware Fusion Pro 11.1.0

# 2019-05-22
* Update Terraform 0.11.14
```
brew upgrade terraform
```

# 2019-06-10
* Update Packer 1.4.1
```
brew upgrade packer
```

# 2019-07-13
* Update Vagrant 2.2.5
```
vagrant plugin expunge --reinstall
```

# 2019-09-20
* Update VMware Fusion Pro 11.5.0

# 2019-09-29
* Update Azure CLI
```
sudo xcodebuild -license accept
xcode-select --install
brew upgrade azure-cli
brew cleanup
```
