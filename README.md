# My Mac Setup

Yeah, I forget stuff.

So I made this list of stuff I need to do in a new Mac OS build.

## Basic Stuff 🤙

Some basic installations and updates that are the **NOT** optional.

#### Update System Preferences

- ** > System Preferences > Software Update**
- General > Sidebar icon size > Large
- Dock > Automatically hide the dock
- Trackpad > Tap to click
- Accessibilty > Mouse & Trackpad > Increase Double-click speed to full
- Siri > **Disable** it

#### Install [Homebrew](https://brew.sh/)

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### Brew [Node](https://nodejs.org/en/) and other stuff

```sh
brew install node
brew install hugo
brew install mysql
brew install youtube-dl libav ffmpeg
```

#### Install [Cask](https://caskroom.github.io/) Stuff

```sh
brew tap homebrew/cask-cask
brew tap homebrew/cask-fonts
```

## Prezto for Zsh 😈

#### Main Prezto Installation

```sh
zsh
```

```sh
git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"
```

```sh
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

```sh
chsh -s /bin/zsh
```

Open a new Zsh terminal window or tab.

#### Configure theme and modules

Go to,

```sh
subl ~/.zpreztorc
```

And add,

```sh
zstyle ':prezto:module:prompt' theme 'minimal'
```

```sh
zstyle ':prezto:load' pmodule \
  'environment' \
  'terminal' \
  'editor' \
  'history' \
  'directory' \
  'autosuggestions' \
  'spectrum' \
  'utility' \
  'completion' \
  'syntax-highlighting' \
  'history-substring-search' \
  'prompt'
```

## Git love ❤️

#### Setup Git

```sh
git config --global user.name "praveenjuge"
git config --global user.email "praveen@skcript.com"
git config --global color.ui true
```

Then connect [GitHub with SSH](https://help.github.com/articles/connecting-to-github-with-ssh/) and make sure you can [Sign commits with GPG](https://help.github.com/articles/signing-commits-with-gpg/).

#### Folder for Git Version Control

```sh
mkdir ~/Projects
```

## Apps and Fonts ⚡️

```sh
# Apps
brew cask install android-file-transfer android-platform-tools
brew cask install figma
brew cask install google-chrome
brew cask install image2icon
brew cask install imageoptim
brew cask install transmission
brew cask install visual-studio-code

# Quicklook Plugins
brew cask install qlcolorcode
brew cask install qlimagesize
brew cask install qlmarkdown
brew cask install qlstephen
brew cask install qlvideo
brew cask install quicklook-json
brew cask install quicklookase
brew cask install webpquicklook

# Fonts
brew cask install font-anonymous-pro
brew cask install font-comic-neue
brew cask install font-cutive
brew cask install font-cutive-mono
brew cask install font-dejavu-sans
brew cask install font-inconsolata
brew cask install font-inter
brew cask install font-karla
brew cask install font-lato
brew cask install font-lobster
brew cask install font-noto-sans
brew cask install font-noto-sans-tamil
brew cask install font-nunito
brew cask install font-open-sans
brew cask install font-oxygen
brew cask install font-oxygen-mono
brew cask install font-playfair-display
brew cask install font-poppins
brew cask install font-quicksand
brew cask install font-raleway
brew cask install font-roboto
brew cask install font-roboto-condensed
brew cask install font-roboto-mono
brew cask install font-roboto-slab
brew cask install font-source-code-pro
brew cask install font-ubuntu
brew cask install font-work-sans
```

## OS Changes 💿

Sometimes mac doesn't get it right.

```sh
# Disable the sound effects on boot
sudo nvram SystemAudioVolume=" "

# Disable the “Are you sure you want to open this application?” dialog
defaults write com.apple.LaunchServices LSQuarantine -bool false

# Enable character repeat on keydown
defaults write -g ApplePressAndHoldEnabled -bool false

# text selection in quick look
defaults write com.apple.finder QLEnableTextSelection -bool true

# Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

# Finder: show all filename extensions
defaults write NSGlobalDomain AppleShowAllExtensions -bool true

# Show Path bar in Finder
defaults write com.apple.finder ShowPathbar -bool true

# Show Status bar in Finder
defaults write com.apple.finder ShowStatusBar -bool true

# Show absolute path in finder's title bar.
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES

# Enable AirDrop over Ethernet and on unsupported Macs
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

# Avoid creating .DS_Store files on network volumes
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

# Quit finder using cmd-q
defaults write com.apple.finder QuitMenuItem -bool true

# Enable the Develop menu and the Web Inspector in Safari
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true && \
defaults write com.apple.Safari IncludeDevelopMenu -bool true && \
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true && \
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled -bool true && \
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true
```

## VS Code Settings 📑

#### Install Plugins

```
Better TOML
```

#### Save Preferences

Go to **Code > Preferences > Settings - User**

```
{
  "editor.fontSize": 17,
  "editor.formatOnPaste": true,
  "prettier.disableLanguages": ["vue", "md", "markdown"],
  "window.zoomLevel": 1,
  "editor.wordWrap": "on",
  "editor.formatOnSave": true,
  "javascript.updateImportsOnFileMove.enabled": "always"
}
```

## Aliases 🙆‍♂️

In terminal do, `subl ~/.zprofile` and add,

```sh
# Lazy git
gitpush() {
    echo -e "\e[0;32m YOUR GIT STATUS: \e[0m"
    git status -s -u -v
    echo -n "\e[0;32m Press ENTER to continue: \e[0m"
    read var_name
    echo -e "\e[0;32m ADDING ALL... \e[0m"
    git add . -v
    echo -e "\e[0;32m COMMITING... \e[0m"
    git commit -a -s -v -m "$*"
    echo -e "\e[0;32m PUSHING... \e[0m"
    git push -v
}
alias lg=gitpush

# Lazy youtube-dl
youtubedownload() {
  youtube-dl \
    -f '(bestvideo[ext=mp4]/bestvideo)+(bestaudio[ext=m4a]/bestaudio)/best' \
    --max-filesize 500m \
    --console-title \
    -o "~/Downloads/%(title)s.%(ext)s" \
    $*
}
youtubedownloadlist() {
  youtube-dl \
    -f '(bestvideo[ext=mp4]/bestvideo)+(bestaudio[ext=m4a]/bestaudio)/best' \
    --max-filesize 500m \
    --console-title \
    -o "~/Downloads/%(playlist_title)s/%(playlist_index)s - %(title)s.%(ext)s" \
    $*
}
alias yd=youtubedownload
alias ydl=youtubedownloadlist

# To Convert Video Files to GIF for Dribbble
# Usage: vtg videofilename.mov
videotogif() {
  ffmpeg -y -i "${1}" -vf fps=${3:-10},scale=${2:-320}:-1:flags=lanczos,palettegen "${1}.png"
  ffmpeg -i "${1}" -i "${1}.png" -filter_complex "fps=${3:-10},scale=800:600:-1:flags=lanczos[x];[x][1:v]paletteuse" "${1}".gif
  rm "${1}.png"
}
alias vtg=videotogif

# Find and delete .DS_Store Files
alias cleanup="find . -type f -name '*.DS_Store' -ls -delete"

# Empty Trash and Other Caches
alias emptytrash="sudo rm -rfv ~/Library/Caches/; sudo rm -rfv /Volumes/*/.Trashes; sudo rm -rfv ~/.Trash; sudo rm -rfv /private/var/log/asl/*.asl; sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'delete from LSQuarantineEvent'"

# To Open VS Code easily
alias s='code .'

# Update everything at once
alias brewup='brew update && brew upgrade && brew cu -a -f --cleanup -y && brew cleanup; brew doctor'

# MAMP DB
export DATABASE_USERNAME="root"
export DATABASE_PASSWORD="root"
export DATABASE_SOCKET="/Applications/MAMP/tmp/mysql/mysql.sock"
export DATABASE_DEV_NAME=""
export DATABASE_DEV_USERNAME="root"
export DATABASE_DEV_PASSWORD="root"
export DATABASE_DEV_PORT=""
export DATABASE_DEV_SOCKET="/Applications/MAMP/tmp/mysql/mysql.sock"
```

## That's it! 👏

Enjoy your fully configured mac os, future me.
