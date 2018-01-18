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

```git clone https://github.com/praveenjuge/bitbar-plugins.git```


## OS Changes

Sometimes mac doesn't get it right.

```
#Set a blazingly fast keyboard repeat rate
defaults write NSGlobalDomain KeyRepeat -int 1

#Set a shorter Delay until key repeat
defaults write NSGlobalDomain InitialKeyRepeat -int 10

#Add a context menu item for showing the Web Inspector in web views
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

#Show the ~/Library folder
chflags nohidden ~/Library

#Store screenshots in subfolder on desktop
mkdir ~/Desktop/Screenshots
defaults write com.apple.screencapture location ~/Desktop/Screenshots
```

## Sublime Text Settings

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

In terminal do, `subl ~/.zprofile`

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