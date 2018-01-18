# My Mac Setup

Yeah, I forget stuff.

So I made this list of stuff I need to do in a new Mac OS build.

## Basic Stuff 🤙

Some basic installations and updates that are the **NOT** optional. 

#### Update System
Go to **App Store > Updates**

#### My System Preferences 
- General > Use dark menu bar
- General > Sidebar icon size > Large
- Trackpad > Tap to click
- Dock > Automatically hide the dock
- Accessibilty > Mouse & Trackpad > Increase Double-click speed to full
- Accessibilty > Display > Reduce transparency
- Siri > **Disable** it

#### Install [Homebrew](https://brew.sh/) and [Cask](https://caskroom.github.io/)

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" && brew tap caskroom/cask
```

## Install Prezto for Zsh 😈

```
zsh
```
```
git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"
```
```
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```
```
chsh -s /bin/zsh
``` 

**Open a new Zsh terminal window or tab.**

## Git love ❤️

#### Setup Git
```
git config --global user.name "praveenjuge"
git config --global user.email "praveen@skcript.com"

git config --global alias.co checkout
git config --global alias.st status
git config --global color.ui true
```

#### Folder for Git Version Control
```
mkdir ~/projects
```

## Apps ⚡️

#### All the apps that i have on my system right now.

```
brew cask install appcleaner bitbar franz google-backup-and-sync google-chrome handshaker iina image2icon imageoptim sketch sublime-text transmission
```

#### or do it one-by-one

```
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
```

## Bitbar Plugins 🤓

Assuming you installed Bitbar from the previous step.

```
cd ~/projects
git clone https://github.com/praveenjuge/bitbar-plugins.git
```

Go to bitbar and point the plugin folder to this.

## OS Changes 💿 

Sometimes mac doesn't get it right.

```
# Enable character repeat on keydown
defaults write -g ApplePressAndHoldEnabled -bool false

#Set a blazingly fast keyboard repeat rate
defaults write NSGlobalDomain KeyRepeat -int 1

# text selection in quick look
defaults write com.apple.finder QLEnableTextSelection -bool true

#Set a shorter Delay until key repeat
defaults write NSGlobalDomain InitialKeyRepeat -int 10

# Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

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

## Sublime Text Settings 📑

#### Install Package Control

Go to **View > Show Console**

```
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

For more information, [Installation - Package Control](https://packagecontrol.io/installation)

#### Install Plugins and Themes

```
Emmet

HTML-CSS-JS Prettify

Material Theme

GitGutter

Sidebar Enhancements
```

#### Save Preferences

Go to **Sublime Text > Preferences > Settings - User**

```
{
	"color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
	"font_size": 16,
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

```
gitpush() {
    echo -e "\e[0;32m YOUR GIT STATUS: \e[0m"
    git status
    echo -e "\e[0;32m ADDING ALL... \e[0m"
    git add .
    echo -e "\e[0;32m COMMITING... \e[0m"
    git commit -a -m "$*"
    echo -e "\e[0;32m PUSHING... \e[0m"
    git push
}
alias lg=gitpush
```