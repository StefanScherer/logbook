# 2021-02-09

- Turned on Mac Mini M1 16GB 
- Updated to macOS 11.2
- Install Dropbox, install 1Password 7
- Create SSH key
- put SSH pub key to GitHub
- System Preferences -> Trackpad -> Tap to click
- System Preferences -> Accessibility -> Pointer Control -> Mouse & Trackpad -> Trackpad Options... -> Enable dragging without drag lock
- Install Homebrew 3
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
echo 'eval $(/opt/homebrew/bin/brew shellenv)' >> /Users/stefanscherer/.zprofile
```
- Install jq
```
brew install jq
```
- Install Xcode 12.4
- Back to bash
```
chsh -s /bin/bash
```
- Install dotfiles
```
git clone https://github.com/StefanScherer/dotfiles && cd dotfiles && ./sync.sh
```
- Install Visual Studio Code Insiders

# 2021-02-10

- Update macOS 11.2.1
- Install Xcode command line tools again
```
xcode-select --install
```

# 2021-02-11

- Install Microsoft Remote Desktop
- Install Parallels beta for Apple Silicon
- Install Docker Desktop 3.1.0 (60984)
- Install Slack

# 2021-02-12

- Install Rectangle (SizeUp, Spectacle replacement)
```
brew install --cask rectangle
```
- Install Go 1.16rc1
```
brew install go
```

# 2021-02-22
- Remove Go 1.16rc1
```
brew uninstall go
```
- Install Go 1.16 from https://golang.org/doc/install?download=go1.16.darwin-arm64.pkg
- Fix using Xcode
```
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```
- Fix using Xcode
```
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```
- Create GPG Key with passphrase
```
gpg --full-generate-key
gpg --list-secret-keys --keyid-format LONG
gpg --armor --export xxxxxxxx
```

# 2021-02-26
- Install Ansible
```
brew install ansible ansible-lint
brew install hudochenkov/sshpass/sshpass
```
