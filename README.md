# My Mac Setup

Yeah, I forget stuff.

So I made this list of configurations I need to do in a new Mac OS build.

## Basic Stuff 🤙

Some basic installations and updates that are the **NOT** optional.

### Update System Preferences

- ** > System Preferences > Software Update**
- General > Sidebar icon size > Large
- Dock > Automatically hide the dock
- Trackpad > Tap to click
- Accessibility > Pointer Control > Increase Double-click speed to full

#### Install [Homebrew](https://brew.sh/)

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

#### Brew [Node](https://nodejs.org/en/) and other binaries

```sh
brew install node
brew install hugo
brew install mysql
brew install youtube-dl libav ffmpeg
```

## Prezto for Zsh 😈

### Main Prezto Installation

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
open ~/.zpreztorc
```

And replace theme and modules,

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

### Setup Git

```sh
git config --global user.name "praveenjuge"
git config --global user.email "praveen@skcript.com"
git config --global color.ui true
```

Then connect [GitHub with SSH](https://help.github.com/articles/connecting-to-github-with-ssh/) and make sure you can [Sign commits with GPG](https://help.github.com/articles/signing-commits-with-gpg/).

### Folder for Git Version Control

```sh
mkdir ~/Projects
```

## Apps and Fonts ⚡️

```sh
# Apps
brew install android-file-transfer android-platform-tools
brew install figma
brew install iina
brew install image2icon
brew install google-chrome
brew install visual-studio-code
brew install zoom

# Fonts
brew tap homebrew/cask-fonts

brew install font-inter
brew install font-jetbrains-mono
brew install font-lato
brew install font-lobster
brew install font-noto-sans
brew install font-noto-sans-tamil
brew install font-nunito
brew install font-open-sans
brew install font-playfair-display
brew install font-poppins
brew install font-quicksand
brew install font-raleway
brew install font-roboto
brew install font-roboto-condensed
brew install font-roboto-mono
brew install font-roboto-slab
brew install font-source-code-pro
brew install font-ubuntu
brew install font-work-sans
```

## OS Changes 💿

Sometimes mac doesn't get it right.

```sh
# Disable the “Are you sure you want to open this application?” dialog
defaults write com.apple.LaunchServices LSQuarantine -bool false

# Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

# Show path bar in Finder
defaults write com.apple.finder ShowPathbar -bool true

# Show status bar in Finder
defaults write com.apple.finder ShowStatusBar -bool true

# Show absolute path in finder's title bar.
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES

# Quit finder using cmd-q
defaults write com.apple.finder QuitMenuItem -bool true

# Avoid creating .DS_Store files on network volumes
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
```

## Aliases 🙆‍♂️

In terminal do, `code ~/.zprofile` and add,

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

# Youtube Downloader
youtubedownload() {
  youtube-dl \
    -f '(bestvideo[ext=mp4]/bestvideo)+(bestaudio[ext=m4a]/bestaudio)/best' \
    --max-filesize 9999m \
    --console-title \
    -o "~/Downloads/%(title)s.%(ext)s" \
    $*
}
youtubedownloadlist() {
  youtube-dl \
    -f '(bestvideo[ext=mp4]/bestvideo)+(bestaudio[ext=m4a]/bestaudio)/best' \
    --max-filesize 9999m \
    --console-title \
    -o "~/Downloads/%(playlist_title)s/%(playlist_index)s - %(title)s.%(ext)s" \
    $*
}
alias yd=youtubedownload
alias ydl=youtubedownloadlist

# To Convert Video Files to GIF for Dribbble
# Usage: vtg videofilename.mov
video2gif() {
  ffmpeg -y -i "${1}" -vf fps=${3:-10},scale=${2:-320}:-1:flags=lanczos,palettegen "${1}.png"
  ffmpeg -i "${1}" -i "${1}.png" -filter_complex "fps=${3:-10},scale=1600:1200:-1:flags=lanczos[x];[x][1:v]paletteuse" "${1}".gif
  rm "${1}.png"
}
alias vtg=videotogif

# Torrent Downloader (https://github.com/webtorrent/webtorrent-cli)
tplay() {
  webtorrent download $* --iina --out "Downloads/" --no-quit
}
tdown() {
  webtorrent download $* --out "Downloads/"
}

# Image Compressor (https://github.com/funbox/optimizt)
ic() {
  optimizt --verbose $*
}

# Find and delete .DS_Store Files
alias cleanup="find . -type f -name '*.DS_Store' -ls -delete"

# Empty Trash and Other Caches
alias emptytrash="sudo rm -rfv ~/Library/Caches/; sudo rm -rfv /Volumes/*/.Trashes; sudo rm -rfv ~/.Trash; sudo rm -rfv /private/var/log/asl/*.asl; sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'delete from LSQuarantineEvent'"

# To Open VS Code
alias c='code .'

# Update everything at once
alias brewup='brew update && brew upgrade && brew cu -a -f --cleanup -y && brew cleanup; brew doctor'

# mysql DB
export DATABASE_USERNAME="root"
export DATABASE_PASSWORD=""
export DATABASE_DEV_USERNAME="root"
export DATABASE_DEV_PASSWORD=""
export DATABASE_SOCKET="/tmp/mysql.sock"
export DATABASE_DEV_SOCKET="/tmp/mysql.sock"

# Notes
pushnotes() {
  cd && cd projects/orison
  now=$(date '+%A %d %m %Y %X')
  git add . -v
  git commit -a -s -v -m $now
  git push -v
}
alias notes='cd && cd projects/orison && code .'
```

## That's it! 👏

Enjoy your fully configured mac os, future me.
