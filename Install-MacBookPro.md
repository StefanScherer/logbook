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

hm, da fehlen wohl einige brew Pakete… also dann manuell

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
curl https://raw.github.com/creationix/nvm/master/install.sh | sh
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
