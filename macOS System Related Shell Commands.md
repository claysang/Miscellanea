# macOS System Related Shell Commands

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

## Clear Icon Services Cache:
sudo rm -rf /Library/Caches/com.apple.iconservices.store

/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -r -domain local -domain user

sudo find /private/var/folders/ \   -name com.apple.dock.iconcache -exec rm {} \

sudo find /private/var/folders/ \   -name com.apple.iconservices -exec rm -rf {} \

## Restore Missing Share Menu Options:
/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -seed

## Restore Launchpad:
defaults write com.apple.dock ResetLaunchPad -bool true && killall Dock

## Launchd Agent:
sudo chmod 644 /Library/LaunchAgents/com.clay.ConfigProxy.plist

sudo chown root:wheel /Library/LaunchAgents/com.clay.ConfigProxy.plist

sudo launchctl load /Library/LaunchAgents/com.clay.ConfigProxy.plist

## System Info:
system_profiler SPHardwareDataType

sysctl -n machdep.cpu.brand_string

kextstat | grep -v com.apple

pmset -g log | grep -e "Display is turned on"

## Local Backup:
sudo tmutil disablelocal
sudo tmutil enablelocal

## Delete Xcode:
sudo /Developer/Library/uninstall-devtools --mode=all

## Reload Audio Kext:
sudo kextunload /System/Library/Extensions/AppleHDA.kext
sudo kextload /System/Library/Extensions/AppleHDA.kext

## Misc.:
defaults write com.apple.PowerChime ChimeOnAllHardware -bool true; open /System/Library/CoreServices/PowerChime.app &

/usr/libexec/java_home -V

sudo /Applications/Parallels\ Desktop.app/Contents/MacOS/Parallels\ Service.app/Contents/MacOS/prl_disp_service -e

sudo mdutil -E /

## PKG:
pkgutil --pkg-info the-package-name.pkg

pkgutil --only-files --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -i

pkgutil --only-dirs --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -ir

sudo pkgutil --forget the-package-name.pkg

cd/

## Show All Files:
defaults write com.apple.finder AppleShowAllFiles Yes && killall Finder

defaults write com.apple.finder AppleShowAllFiles No && killall Finder

## .DS_Store:
sudo find / -name .DS_Store -delete; killall Finder

rm ~/Library/Preferences/com.apple.finder.plist; killall Finder

## Clear Font Cache:
sudo atsutil databases -remove
(/System/Library/Frameworks/ApplicationServices.framework/Frameworks/CoreText.framework/Resources/)

## Dock Icon:
sudo find /private/var/folders/ -name com.apple.dock.iconcache -exec rm {} \;

killall Dock

## Mac App Store:
defaults write com.apple.appstore ShowDebugMenu -bool true

defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1

## com.apple.kerberos.kdc: <http://automatica.com.au/2012/01/how-to-give-a-mac-os-x-machine-a-new-kerberos-identity/>

sudo rm -fr /var/db/krb5kdc

sudo /usr/libexec/configureLocalKDC

## Optimization:
sudo mdutil -E /

sudo defaults write /System/Library/LaunchDaemons/com.apple.coreservices.appleevents ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchDaemons/com.apple.securityd ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchDaemons/com.apple.diskarbitrationd ExitTimeOut -int 1

sudo defaults write /System/Library/LaunchAgents/com.apple.coreservices.appleid.authentication ExitTimeOut -int 1