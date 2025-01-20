# Android Debug Bridge (`adb`)

[Android developer documentation](https://developer.android.com/tools/adb)

- CLI tool used to communicate with Android devices - performing actions such as installing apps, remotely rebooting the device, transferring files between a computer and the device, etc.
- included in the Android SDK Platform Tools package which can be downloaded using the [SDK manager](https://developer.android.com/studio/intro/update?_gl=1*1mc64i8*_up*MQ..*_ga*MTE2MjI5OTI4Ny4xNzM3NDEzNzk1*_ga_6HH9YJMN9M*MTczNzQxMzc5NS4xLjAuMTczNzQxMzc5NS4wLjAuMTY3NDkzNjE4Mw..#sdk-manager)
- when an `adb` client starts, it checks to see if an `adb` server is already running
  - if the server isn't running, the client starts the server process
  - if the server is running, the client binds to local TCP port 5037 and listens for commands sent from the client
 
### Enabling `adb` debugging

- will need to enable developer options first: go to system settings > find the `Build number` > tap on it seven times until the popup appears
- enable USB debugging in the device system settings (under `Developer options`)
- once enabled, connect the phone to your computer via USB

## Useful Commands

- `adb devices -l` - list the devices currently connected and accessible via `adb`
- `adb kill-server` - kill any existing `adb` server
- `adb install [APK-PATH]` - install an apk on your connected Android device
- `adb pull [REMOTE-PATH] [LOCAL-PATH]` - copy a file/directory from the device
- `adb push [LOCAL-PATH] [REMOTE-PATH]` - copy a file/directory to the device
