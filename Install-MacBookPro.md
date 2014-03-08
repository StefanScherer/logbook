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

