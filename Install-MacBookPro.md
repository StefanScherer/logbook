# Installationlogbuch Stefans MacBook Pro

## 2014-03-01
* Rechner eingeschaltet
* Benutzer Stefan angelegt
* Benutzer Carina und Katja angelegt, Kinderschutz aktiviert
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
* Node 0.10.26 heruntergeladen von http://nodejs.org/download/  und installiert

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
** Then you can pretty print json responses: `curl -s http://localhost:8080/rest/config | jsonpp`


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
* `curl -L https://github.com/docker/compose/releases/download/1.4.0rc3/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose`
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
````
$ vagrant plugin list
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

