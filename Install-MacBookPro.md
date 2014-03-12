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
