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

