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

# 2021-02-10

- Update macOS 11.2.1
- Install Xcode command line tools again
```
xcode-select --install
```
