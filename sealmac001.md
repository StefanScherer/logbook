# 2018-08-10

Unboxing new MacBook Pro

- Turn on
- Create Apple ID with company email
- User stefan
- Change hostname to sealmac001
- Installed macOS updates

Installed all further software with https://github.com/StefanScherer/dotfiles#setup-a-new-mac-box

```
curl https://raw.githubusercontent.com/StefanScherer/dotfiles/master/setup-mac | bash
```

- Uninstall 1Password 7
- Install 1Password 6 from 1password.com
- Connected Dropbox
- Log out / Log in for new terminal and trackpad settings
- Adjust `.gitconfig`
- Create SSH key with passphrase
```
ssh-keygen
```
- Create GPG Key with passphrase
```
gpg --full-generate-key
gpg --list-secret-keys --keyid-format LONG
gpg --armor --export xxxxxxxx
```
- Login to GitHub, remove old SSH key, insert new SSH and GPG key
- https://github.com/settings/keys
- Open VMware Fusion, start 30 day trial for Fusion Professional
- Install Vagrant plugins
```
vagrant plugin install vagrant-vmware-desktop
vagrant plugin install vagrant-reload
vagrant plugin license vagrant-vmware-desktop license.lic
```
- Open Outlook, connect to Exchange server
- Initialize pass store
```
pass init stefan.scherer@sealsystems.de
pass git init
pass insert test
pass test
```
- Open Chrome, Disable saving passwords
- No Vagrant license til Monday, switch to VirtualBox 5.2.16
```
brew cask install virtualbox
vagrant plugin uninstall vagrant-vmware-desktop
```
- Windows containers
```
cd ~/code
git clone https://github.com/StefanScherer/windows-docker-machine
cd
dm start 2016-box
```
- Configure `hub` for first time use, asks for GitHub user + password once to create token
```
hub browse
```
- Install GotoMeeting 
- Install Node.js 10.8.0
```
nvm install 10
npm install -g roboter-cli
```
- Trust my other GPG key got `pass`
```
gpg --import stefan-pub
gpg --list-keys
gpg --edit-key MYOTHERPUBID trust quit
```

# 2018-08-12
- Create Packer cache folder
```
cd
mkdir -p mkdir packer_cache/insider
ln -s .packer_cache packer_cache
```
- Disable guest account

# 2018-08-13
- Install Vagrant VMware license
```
vagrant plugin install vagrant-vmware-desktop
vagrant plugin license vagrant-vmware-desktop ~/Documents/license.lic
```
- Uninstall VirtualBox
```
brew cask uninstall virtualbox
```
- Install Timing app (test)
- Install Sophos Endpoint

# 2018-08-15
- Microsoft AutoUpdate Office 16.16.0 (18081201)
- Update VMware Fusion Pro 10.1.3

# 2018-08-16
- Mounting smb://sealsystems.local does not work through VPN, 
- add `10.100.20.2 f﹕` to `/etc/hosts` and use `smb://f﹕/files` to connect :-)
- Install pinentry-mac
```
brew install pinentry-mac
```
- Adjust ~/.gnupg/gpg-agent.conf, add `pinentry-program /usr/local/bin/pinentry-mac`
- Logout / Login
- Update Node.js 10.9.0
```
nvm install 10
nvm alias default node
nvm reinstall-packages 10.8.0
nvm uninstall 10.8.0
```

# 2018-09-10
- Update Docker 18.06.1
- Update macOS, reboot
- Update vagrant 2.1.4, vagrant-vmware-utility 1.0.4, wireshark 2.6.3
```
brew cask upgrade
```
- Update vim 8.1.0250 -> 8.1.0350, terraform 0.11.7 -> 0.11.8, ghostscript 9.23 -> 9.24, gdbm 1.17 -> 1.18, oniguruma 6.8.2 -> 6.9.0, ssh-copy-id 7.7p1 -> 7.8p1, openssl 1.0.2o_2 -> 1.0.2p, hub 2.5.0 -> 2.5.1, gnupg 2.2.9 -> 2.2.10, p11-kit 0.23.12 -> 0.23.14
```
brew upgrade
```

# 2018-09-14
- Enable TouchID for sudo
```
sudo vi /etc/pam.d/sudo
```
insert following line
```
auth       sufficient     pam_tid.so
```

# 2018-09-28
- Update to macOS Mojave 10.14
- Remove Microsoft Remote Desktop
- Install Microsoft Remote Desktop Beta with Retina support

# 2018-10-15
- Install ADR tools
```
xcode-select --install
brew install adr-tools
```

# 2018-10-19
- Update Vagrant 2.2.0
```
brew update
brew cask reinstall vagrant
```
- Update Packer 1.3.1
```
brew upgrade packer
```
- Update Vagrant VMware Desktop plugin 2.0.0
```
vagrant plugin update
```

# 2018-11-18
- Update VMware Vagrant Utility 1.0.5
```
brew cask reinstall vagrant-vmware-utility
```

# 2018-11-22
- Update Docker Desktop 2.0.0.0

# 2018-11-27
- Installation VirtualBox 5.2.22
```
brew cask install virtualbox
```
- Update VMware Fusion Pro 10.1.5

# 2018-12-14
- Update Docker Desktop 2.0.0.0 mac81

# 2019-01-02
- Install Azure CLI
```
curl -L https://aka.ms/InstallAzureCli | bash
```

# 2019-01-03
- Update VMware Fusion Pro 11 and license
- Update Vagrant 2.2.2 from vagrantup.com
- Update Vagrant VMware Desktop and license
- Uninstall VirtualBox due to problems with vmrun

