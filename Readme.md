#Remote Debugging iOS Apps with LLDB

Install Xcode.app

### New device setup
```
# copy debug server to device
scp 7.0/debugserver root@rPad.local:~/

# connect to device
ssh root@rPad.local

```

## on device commands
```
# get a list of installed apps
~/debugserver --applist

# start the debugserver (on port 1234)
 ~/debugserver *:1234 /var/mobile/Applications/*/*.app/Twitter
 ```

## host commands (lldb)
```
lldb

platform select remote-ios
process connect connect://rPad.local:1234

```

## source
[https://github.com/llvm-mirror/lldb/tree/master/tools/debugserver](https://github.com/llvm-mirror/lldb/tree/master/tools/debugserver)

# Work required for new iOS versions
``` 
# mount the developer diskimage
hdiutil attach /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport/7.0/DeveloperDiskImage.dmg

# overwrite debugserver entitlements
cp /Volumes/DeveloperDiskImage/usr/bin/debugserver ./7.0/

codesign -s - --entitlements entitlements.plist -f 7.0/debugserver
```
