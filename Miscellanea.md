# SSH
## Show server public key info
ssh-keygen -l -f /etc/ssh/ssh\_host\_ecdsa\_key.pub

## [Show server certificate info](https://security.stackexchange.com/a/46255)
openssl x509 -in x.crt -noout -fingerprint

openssl x509 -in x.crt -noout -md5 -fingerprint

openssl x509 -in x.crt -noout -sha256 -fingerprint

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

# Using JetBrains IDE as Git External Tool
## Edit `.bash_profile`
export PATH="/Applications/WebStorm.app/Contents/MacOS:$PATH"

## Edit `.gitconfig`
  [merge]
    tool = JetBrains
  [diff]
    tool = JetBrains
  [difftool]
    prompt = false
  [difftool "JetBrains"]
    cmd = webstorm diff $(cd $(dirname "$LOCAL") && pwd)/$(basename "$LOCAL") $(cd $(dirname "$REMOTE") && pwd)/$(basename "$REMOTE")
    trustExitCode = true
  [mergetool "JetBrains"]
    cmd = webstorm merge $(cd $(dirname "$LOCAL") && pwd)/$(basename "$LOCAL") $(cd $(dirname "$REMOTE") && pwd)/$(basename "$REMOTE") $(cd $(dirname "$BASE") && pwd)/$(basename "$BASE") $(cd $(dirname "$MERGED") && pwd)/$(basename "$MERGED")
    trustExitCode = true

# Android
  adb devices

  adb reboot bootloader

  adb sideload \*.zip


  fastboot oem unlock

  fastboot flash boot boot.img

  fastboot flash recovery recovery.img

# Linux
## Check memory usage
ps -e -o 'pid,comm,args,pcpu,rsz,vsz,stime,user,uid'

ps -e -o 'pid,comm,args,pcpu,rsz,vsz,stime,user,uid' | grep xxx | sort -nrk5

# macOS Path
## Icons
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources

## System Sounds
/System/Library/Components/CoreAudio.component/Contents/SharedSupport/SystemSounds/

## SF Mono
/Applications/Xcode.app/Contents/SharedFrameworks/DVTKit.framework/Versions/Current/Resources/Fonts/




# Other Stuff
/etc/sudoers