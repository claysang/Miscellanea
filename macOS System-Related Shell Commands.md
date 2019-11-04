# macOS System-Related Shell Commands

## Network
sudo killall -HUP mDNSResponder

sudo lsof -n -P| grep :55555

lsof -i4

### Network First-Aid
sudo killall -9 networkd

sudo launchctl kickstart -k

system/com.apple.networking.discoveryd

sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist

sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist

## Disk Utility
diskutil apfs setPassphraseHint [diskXsX] -user disk -clear

### Mount EFI
sudo mkdir /Volumes/EFI

sudo mount -t msdos /dev/diskXsX /Volumes/EFI

## Clear Icon Services Cache
sudo rm -rf /Library/Caches/com.apple.iconservices.store

/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -r -domain local -domain user

sudo find /private/var/folders/ \   -name com.apple.dock.iconcache -exec rm {} \

sudo find /private/var/folders/ \   -name com.apple.iconservices -exec rm -rf {} \

## Restore Missing Share Menu Options
/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -seed

## Restore Launchpad
defaults write com.apple.dock ResetLaunchPad -bool true && killall Dock

## Launchd Agent
sudo chmod 644 /Library/LaunchAgents/com.clay.ConfigProxy.plist

sudo chown root:wheel /Library/LaunchAgents/com.clay.ConfigProxy.plist

sudo launchctl load /Library/LaunchAgents/com.clay.ConfigProxy.plist

## Bluetooth audio
sudo defaults read bluetoothaudiod

sudo defaults write bluetoothaudiod "Enable AptX codec" -bool true

sudo defaults write bluetoothaudiod "Enable AAC codec" -bool true

sudo defaults write bluetoothaudiod "AAC Bitrate" -int 320

sudo defaults write bluetoothaudiod "AAC CBR" -bool false

sudo defaults write bluetoothaudiod "AAC max packet size" -int 644

sudo defaults write bluetoothaudiod "Apple Bitpool Max" -int 80

sudo defaults write bluetoothaudiod "Apple Bitpool Min" -int 80

sudo defaults write bluetoothaudiod "Apple Initial Bitpool" -int 80

sudo defaults write bluetoothaudiod "Negotiated Bitpool" -int 80

sudo defaults write bluetoothaudiod "Negotiated Bitpool Max" -int 80

sudo defaults write bluetoothaudiod "Negotiated Bitpool Min" -int 80

## Update Bash
chsh -s /usr/local/bin/bash

echo $BASH && echo $BASH_VERSION

etc/shells

## Uninstall all brew packages
brew list -1 | xargs brew rm

## System Info
system_profiler SPHardwareDataType

sysctl -n machdep.cpu.brand_string

pmset -g log | grep -e "Display is turned on"

## Code Signing
codesign --verify --verbose

codesign -dv --verbose=4

codesign --display --entitlements -

codesign --verify --verbose --no-strict

## Local Backup
sudo tmutil disablelocal

sudo tmutil enablelocal

## Delete Xcode
sudo /Developer/Library/uninstall-devtools --mode=all

## Kext
sudo kextunload /System/Library/Extensions/AppleHDA.kext

sudo kextload /System/Library/Extensions/AppleHDA.kext

kextstat | grep -v com.apple

kextfind -b

## Misc.
defaults write com.apple.PowerChime ChimeOnAllHardware -bool true; open /System/Library/CoreServices/PowerChime.app &

/usr/libexec/java_home -V

sudo /Applications/Parallels\ Desktop.app/Contents/MacOS/Parallels\ Service.app/Contents/MacOS/prl_disp_service -e

sudo mdutil -E /

strings yourPDFfilepath.pdf | grep FontName

## PKG
pkgutil --pkg-info the-package-name.pkg

pkgutil --only-files --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -i

pkgutil --only-dirs --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -ir

sudo pkgutil --forget the-package-name.pkg

cd/

## Show All Files
defaults write com.apple.finder AppleShowAllFiles Yes && killall Finder

defaults write com.apple.finder AppleShowAllFiles No && killall Finder

## .DS_Store
sudo find / -name .DS_Store -delete; killall Finder

rm ~/Library/Preferences/com.apple.finder.plist; killall Finder

## Clear Font Cache
sudo atsutil databases -remove
(/System/Library/Frameworks/ApplicationServices.framework/Frameworks/CoreText.framework/Resources/)

## Dock Icon
sudo find /private/var/folders/ -name com.apple.dock.iconcache -exec rm {} \;

killall Dock

## Mac App Store
defaults write com.apple.appstore ShowDebugMenu -bool true

defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1

defaults delete com.apple.appstore.commerce

## [com.apple.kerberos.kdc](http://automatica.com.au/2012/01/how-to-give-a-mac-os-x-machine-a-new-kerberos-identity/)

sudo rm -fr /var/db/krb5kdc

sudo /usr/libexec/configureLocalKDC

## Optimization
sudo mdutil -E /

sudo defaults write /System/Library/LaunchDaemons/com.apple.coreservices.appleevents ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchDaemons/com.apple.securityd ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchDaemons/com.apple.diskarbitrationd ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchAgents/com.apple.coreservices.appleid.authentication ExitTimeOut -int 1
