# SSH
## Show server public key info
ssh-keygen -l -f /etc/ssh/ssh_host_ecdsa_key.pub

## Configure for highest security available
Ciphers chacha20-poly1305@openssh.com,aes256-ctr

KexAlgorithms curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp521

PermitRootLogin without-password

PasswordAuthentication no

## Useful Shell scripts
sudo service sshd restart

ssh -Q cipher

## Use SSH through a proxy
ProxyCommand /usr/bin/nc -X 5 -x localhost:6153 %h %p

# Android
  adb devices

  adb reboot bootloader

  adb sideload *.zip


  fastboot oem unlock

  fastboot flash boot boot.img
  
  fastboot flash recovery recovery.img

# macOS Path
## Icons
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources

## System Sounds
/System/Library/Components/CoreAudio.component/Contents/SharedSupport/SystemSounds/

## SF Mono
/Applications/Xcode.app/Contents/SharedFrameworks/DVTKit.framework/Versions/Current/Resources/Fonts/




# Other Stuff
/etc/sudoers
