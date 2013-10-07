# Create bootable Mac OS from MAS file

* Show contents of Install.app.
* Copy 'InstallESD.dmg' from '/Contents/SharedSupport/ to an USB drive.


# Boot

* PRAM Reset: Press holding Command-Alt-P-R while booting until you hear the start sound for the second time.
* Safe Mode: Press holding Shift while booting until you see the apple *(disables login items and non-essential kernel extensions from starting up)*.
* Hardware Test: Press D while booting.
* Single-User Mode: Press Command-S while booting *(to repair complex hard drive issues)*.
* Startup Manager: Press Alt while booting *(to select boot source)*. 
* Target Mode: Press T while booting *(to boot from a FireWire device)*.
* OS X Boot: Press X while booting *(will force the Mac to boot from OS X, no matter which disk is specified as the startup disk)*.
* CD/DVD Boot: Press C while booting.
* Network Boot: Press N while booting.
* Verbose Mode: Press Command-V while booting *(to show boot information)*.


# Mac OS

* [General hints](https://pinboard.in/u:michaelx/t:hints/t:osx/)
* [Dotfiles with a bunch of initial tweaks](https://github.com/michaelx/dotfiles)

## Show the Library folder

```
chflags nohidden ~/Library
```

## Disable opening and closing window animations

```
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false
```

## Disable send and reply animations in Mail.app

```
defaults write com.apple.mail DisableReplyAnimations -bool true
defaults write com.apple.mail DisableSendAnimations -bool true
```

## Disable internal Laptop Display when external Display is attached (pre-10.7 behavior)

```
sudo nvram boot-args="iog=0x0"
```

### Undo

```
sudo nvram -d boot-args
```

## Enable “natural” (Lion-style) scrolling

```
defaults write NSGlobalDomain com.apple.swipescrolldirection -bool true
```

## Disable local Time Machine backups

```
hash tmutil &> /dev/null && sudo tmutil disablelocal
```

## Force Time Machine backup

```
/System/Library/CoreServices/backupd.bundle/Contents/Resources/backupd-helper
```

## Force Google Contacts sync

```
/System/Library/PrivateFrameworks/GoogleContactSync.framework/Versions/A/Resources/gconsync --sync com.google.ContactSync
```

## Disable Sudden Motion Sensor in a portable Mac with a SSD (re-enable with '1')

```
sudo pmset -a sms 0
```

## Change Hibernation Mode (0:RAM, 1:HDD, 3:RAM+HDD) and delete last image (Standard: 3)

```
sudo pmset -a hibernatemode 0; sudo rm /var/vm/sleepimage
```

## Rebuild Launch Services to remove duplicates from "Open With" menu

```
/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -kill -r -domain local -domain system -domain user
```

Or delete `/Home/Library/Preferences/com.apple.~LaunchServices`

## Rebuild Spotlight index

```
killall mds
sudo mdutil -i on /
sudo mdutil -E /
```

## Add Dock spaces

```
defaults write com.apple.dock persistent-apps -array-add '{ "tile-type" = "spacer-tile"; }'
killall Dock
```

## Speed up sleep mode

```
sudo pmset -a hibernationmode <#>
```

### Options <#>

* 0: Sleep with RAM *(fast - save everything to the RAM, but your data isn't secure if your battery is low.)*
* 1: Sleep with Hard Drive *(slow - save everything to the HDD, your data is secure.)*
* 3: Sleep with RAM and Hard Drive *(slow and the standard mode - save everything to the RAM and additional to the HDD, your data is secure.)*


# Finder

## Show hidden files

```
defaults write com.apple.finder AppleShowAllFiles -boolean true;killall Finder
```

## Hide hidden files

```
defaults write com.apple.finder AppleShowAllFiles -boolean false;killall Finder
```

## Tinker column view

Double-click on the Resize handle at the bottom of the window. The column will expand to the width of the longest name in the column.

### Save column size

Option-drag on a column handle, the Finder will use the column size settings for every Finder window you open.

### Advanced resize options

Control (right) click on a column handle and you’ll see three options:

1. Right Size This Column *(makes that column the width of the longest name in the column)*
2. Right Size All Columns Individually *(each column will be a different size based on the length of names within each column)*
3. Right Size All Columns Equally *(imposes the widest column length on all the columns)*

[Source](http://www.macworld.com/article/155221/2010/10/tinker_column_view.html)

## Save temporary flash files

* Search for files named *FlashTmp.xyz* in `/private/var/folders/`.
* Copy and rename to xyz.avi.


# Screenshots

## Change default location

``
defaults write com.apple.screencapture location -string "$HOME/xyz"
``

## Change format 

Options: PNG, BMP, GIF, JPG, PDF, TIFF

```
defaults write com.apple.screencapture type -string "png"
```

## Disable shadow

```
defaults write com.apple.screencapture disable-shadow -bool true
```