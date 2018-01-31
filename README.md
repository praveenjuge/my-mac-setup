# My Mac Setup

Yeah, I forget stuff.

So I made this list of stuff I need to do in a new Mac OS build.

## Basic Stuff 🤙

Some basic installations and updates that are the **NOT** optional. 

#### Update System

Go to ** > App Store > Updates**

#### My System Preferences

- General > Use dark menu bar
- General > Sidebar icon size > Large
- Trackpad > Tap to click
- Dock > Automatically hide the dock
- Accessibilty > Mouse & Trackpad > Increase Double-click speed to full
- Accessibilty > Display > Reduce transparency
- Siri > **Disable** it

#### Install [Homebrew](https://brew.sh/)

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### Install [Cask](https://caskroom.github.io/) Stuff

```sh
brew tap caskroom/cask && brew tap buo/cask-upgrade && brew tap caskroom/fonts
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
  'ssh' \
  'completion' \
  'homebrew' \
  'osx' \
  'ruby' \
  'rails' \
  'git' \
  'syntax-highlighting' \
  'history-substring-search' \
  'prompt'
```

## Git love ❤️

#### Setup Git

```sh
git config --global user.name "praveenjuge"
git config --global user.email "praveen@skcript.com"

git config --global alias.co checkout
git config --global alias.st status
git config --global color.ui true
```

#### Folder for Git Version Control

```sh
mkdir ~/projects
```

## Apps and Fonts ⚡️

#### All the apps, plugins and fonts that i have on my system right now.

```sh 
brew cask install android-file-transfer appcleaner bitbar font-anonymous-pro font-bebas-neue font-comic-neue font-cutive font-cutive-mono font-dejavu-sans font-fira-sans font-inconsolata font-inter-ui font-karla font-lato font-lobster font-noto-sans font-noto-sans-tamil font-nunito font-open-sans font-oxygen font-oxygen-mono font-playfair-display font-poppins font-quicksand font-raleway font-roboto font-roboto-condensed font-roboto-mono font-roboto-slab font-source-code-pro font-ubuntu font-work-sans franz google-backup-and-sync google-chrome handshaker iina image2icon imageoptim qlcolorcode qlimagesize qlmarkdown qlstephen qlvideo quicklook-json quicklookase sketch sublime-text transmission webpquicklook
```

#### or do it one-by-one

```sh
# Apps
brew cask install android-file-transfer
brew cask install appcleaner
brew cask install bitbar
brew cask install franz
brew cask install google-backup-and-sync
brew cask install google-chrome
brew cask install handshaker
brew cask install iina
brew cask install image2icon
brew cask install imageoptim
brew cask install sketch
brew cask install sublime-text
brew cask install transmission

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
brew cask install font-bebas-neue
brew cask install font-comic-neue
brew cask install font-cutive
brew cask install font-cutive-mono
brew cask install font-dejavu-sans
brew cask install font-fira-sans
brew cask install font-inconsolata
brew cask install font-inter-ui
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

## Bitbar Plugins 🤓

Assuming you installed Bitbar from the previous step.

```sh
cd ~/projects
git clone https://github.com/praveenjuge/bitbar-plugins.git
```

Go to bitbar and point the plugin folder to this.

## OS Changes 💿 

Sometimes mac doesn't get it right.

```sh
# Disable the sound effects on boot
sudo nvram SystemAudioVolume=" "

# Enable character repeat on keydown
defaults write -g ApplePressAndHoldEnabled -bool false

# Set a blazingly fast keyboard repeat rate
defaults write NSGlobalDomain KeyRepeat -int 1

# text selection in quick look
defaults write com.apple.finder QLEnableTextSelection -bool true

# Set a shorter Delay until key repeat
defaults write NSGlobalDomain InitialKeyRepeat -int 10

# Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

# Disable the “Are you sure you want to open this application?” dialog
defaults write com.apple.LaunchServices LSQuarantine -bool false

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

# Enable the Develop menu and the Web Inspector in Safari
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true && \
defaults write com.apple.Safari IncludeDevelopMenu -bool true && \
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true && \
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled -bool true && \
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

# finder cmd-q
defaults write com.apple.finder QuitMenuItem -bool true
```

## Safari Extensions 💎

[Adblock Plus](https://safari-extensions.apple.com/details/?id=org.adblockplus.adblockplussafari-GRYYZR985A)

[PiPer](https://safari-extensions.apple.com/details/?id=com.amarcus.safari.piper-BQ6Q24MF9X)

## Sublime Text Settings 📑

#### Install Package Control

Go to **View > Show Console**

```sh
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

For more information, [Installation - Package Control](https://packagecontrol.io/installation).

#### Install Plugins and Themes

```
A File Icon

Emmet

HTML-CSS-JS Prettify

Material Theme

GitGutter

Sidebar Enhancements

SCSS
```

#### Save Preferences

Go to **Sublime Text > Preferences > Settings - User**

```
{
  "color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
  "font_size": 16,
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "detect_indentation": true,
  "use_tab_stops": true,
  "word_wrap": true,
  "ignored_packages":
  [
    "Vintage"
  ],
  "material_theme_accent_acid-lime": true,
  "material_theme_accent_scrollbars": true,
  "material_theme_accent_titlebar": true,
  "material_theme_compact_panel": true,
  "material_theme_contrast_mode": true,
  "material_theme_panel_separator": true,
  "material_theme_small_statusbar": true,
  "material_theme_small_tab": true,
  "material_theme_tabs_autowidth": true,
  "material_theme_titlebar": true,
  "theme": "Material-Theme.sublime-theme"
}

```

## Lazy git 👾

In terminal do, `subl ~/.zprofile` and add,

```sh
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
```

## Lazy youtube-dl 🔻

```sh
brew install youtube-dl libav ffmpeg
```

In terminal do, `subl ~/.zprofile` and add,

```sh
youtubedownload() { 
  youtube-dl \
    -f '(bestvideo[ext=mp4]/bestvideo)+(bestaudio[ext=m4a]/bestaudio)/best' \
    --max-filesize 500m \
    --console-title \
    -o "~/Downloads/%(title)s.%(ext)s" \
    $*
}
alias yd=youtubedownload
```

## Update everything at once ♻️

```sh
alias brewup='brew update && brew upgrade && brew cu -a -f --cleanup -y && brew cleanup; brew doctor'
```

## That's it! 👏 

Enjoy your fully configured mac os, future me.