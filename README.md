# My Mac Setup

I forget stuff, so I made this list of configurations I need to do in a new Mac OS build.

## Update System Preferences 

- ** > System Preferences > Software Update**
- General > Sidebar icon size > Large
- Dock > Automatically hide the dock
- Trackpad > Tap to click

## Install [Homebrew](https://brew.sh/) 🏠

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## Brew [Node](https://nodejs.org/en/) and other binaries 🥤

```sh
brew install node
brew install yt-dlp libav ffmpeg

npm install webtorrent-cli -g
```

## Prezto for Zsh 😈

### Prezto Installation

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
git config --global user.email ""
git config --global color.ui true
```

Then connect [GitHub with SSH](https://help.github.com/articles/connecting-to-github-with-ssh/) and make sure you can [Sign commits with GPG](https://help.github.com/articles/signing-commits-with-gpg/).

### Folder for Git Version Control

```sh
mkdir ~/Projects
```

## Install Apps⚡️

```sh
brew install cursor
brew install figma
brew install google-chrome
brew install iina
brew install image2icon
brew install raycast
brew install slack
```

## OS Changes 💿

Sometimes mac doesn't get it right.

```sh
# Disable the “Are you sure you want to open this application?” dialog
defaults write com.apple.LaunchServices LSQuarantine -bool false

# Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

# Quit finder using cmd-q
defaults write com.apple.finder QuitMenuItem -bool true
```

## Aliases 🙆‍♂️

In terminal do, `code ~/.zprofile` and add,

```sh
# Lazy git
lg() {
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

# Youtube Downloader
yd() {
  yt-dlp \
    -f '(bestvideo[ext=mp4]/bestvideo)+(bestaudio[ext=m4a]/bestaudio)/best' \
    --max-filesize 9999m \
    --console-title \
    -o "~/Downloads/%(title)s.%(ext)s" \
    $*
}
ydl() {
  yt-dlp \
    -f '(bestvideo[ext=mp4]/bestvideo)+(bestaudio[ext=m4a]/bestaudio)/best' \
    --max-filesize 9999m \
    --console-title \
    -o "~/Downloads/%(playlist_title)s/%(playlist_index)s - %(title)s.%(ext)s" \
    $*
}

# To Convert Video Files to GIF for Dribbble
# Usage: vtg videofilename.mov
vtg() {
  ffmpeg -y -i "${1}" -vf fps=${3:-10},scale=${2:-320}:-1:flags=lanczos,palettegen "${1}.png"
  ffmpeg -i "${1}" -i "${1}.png" -filter_complex "fps=${3:-10},scale=1600:1200:-1:flags=lanczos[x];[x][1:v]paletteuse" "${1}".gif
  rm "${1}.png"
}

# Torrent Downloader (https://github.com/webtorrent/webtorrent-cli)
tp() {
  webtorrent download $* --iina --out "Downloads/" --no-quit
}
td() {
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

# To Open Cursor
alias c='cursor .'

# Update everything at once
brewup() {
  # Update Homebrew
  echo "Updating Homebrew..."
  brew update

  # Upgrade outdated formulae
  echo "Upgrading outdated formulae..."
  brew upgrade

  # Upgrade outdated casks
  echo "Upgrading outdated casks..."
  brew upgrade --cask

  # BREW CU - Install here: https://github.com/buo/homebrew-cask-upgrade
  echo "brew-cask-upgrade"
  brew cu -a -f --cleanup -y -i --include-mas

  # Cleanup old versions of formulae and casks
  echo "Cleaning up old versions..."
  brew cleanup

  # Check for potential issues
  echo "Checking for potential issues..."
  brew doctor
  brew missing

  # List outdated formulae and casks after upgrade
  echo "Listing outdated formulae and casks after upgrade..."
  brew outdated

  # Remove orphaned dependencies
  echo "Removing orphaned dependencies..."
  brew autoremove

  # Upgrade Node.js and npm packages
  echo "Upgrading npm packages..."
  npm update -g

  # Upgrade Bun
  echo "Upgrading bun..."
  bun upgrade

  # Clear system caches
  echo "Clearing system caches..."
  sudo rm -rf ~/Library/Caches/*
  sudo rm -rf /Library/Caches/*

  # Clear DNS cache
  echo "Clearing DNS cache..."
  sudo dscacheutil -flushcache
  sudo killall -HUP mDNSResponder

  # Free up inactive memory
  echo "Freeing up inactive memory..."
  sudo purge
  
  # Check for disk usage
  echo "Checking disk usage..."
  df -h

  # Check system load and performance
  echo "Checking system load and performance..."
  top -l 1 | head -n 10

  echo "All updates and upgrades complete!"
}
```

## That's it! 👏

Enjoy your fully configured macOS, future me.
