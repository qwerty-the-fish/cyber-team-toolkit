# Guide: Android Debug Bridge (`adb`)
!!! note "Topic: Android Debugging Bridge (adb)"
    CLI tool used to **communicate with Android devices** - install apps, remotely reboot the device, transfer files between the computer and device, etc.

    Included in the `Android SDK Platform Tools` package - can be downloaded using the [SDK manager](https://developer.android.com/studio/intro/update?_gl=1*1mc64i8*_up*MQ..*_ga*MTE2MjI5OTI4Ny4xNzM3NDEzNzk1*_ga_6HH9YJMN9M*MTczNzQxMzc5NS4xLjAuMTczNzQxMzc5NS4wLjAuMTY3NDkzNjE4Mw..#sdk-manager).

    [Android developer documentation](https://developer.android.com/tools/adb)


---

### Enabling `adb` debugging

- enable `Developer Options` first

    - `System Settings` > find the `Build number` > tap on it seven times until the popup appears

- enable USB debugging in the device system settings (under `Developer Options`)
- once enabled, connect the phone to your computer via USB

---

### Starting adb client

- `adb start` - checks to see if the server is already running

    - **server not running**: client starts the server process
    - **server running**: client binds to local TCP port 5037, starts listening for commands sent from client

---

## Useful Commands

| Command | Description |
|-|-|
| adb devices -l | List devices currently connected and accessible via adb |
| adb kill-server | Kill any existing adb server |
| adb install [APK-PATH] | Install an APK on your connected Android device |
| adb pull [REMOTE-PATH] [LOCAL-PATH] | Copy a file/directory from the device to your computer |
| adb push [LOCAL-PATH] [REMOTE-PATH] | Copy a file/directory to the device from your computer |

---

## Logcat

!!! note "Topic: Logcat"
    A command-line tool that dumps a log of system messages.

    Includes messages written from the app using the Log class.

    [Android developer documentation - logcat](https://developer.android.com/tools/logcat)

You can call logcat using: `adb logcat` or `adb shell logcat`.

!!! definition "Define: Tag"
    A short string defining the origin of the message.

!!! definition "Define: Priority"
    The priority of the log message.

    | priority | symbol | name |
    |-|-|-|
    | lowest | V | Verbose |
    | | D | Debug |
    | | I | Info |
    | | W | Warning |
    | | E | Error |
    | | F | Fatal |
    | highest | S | Silent |

    Log messages at priority level 'Silent' are not displayed.

We can use the tag and the priority to filter log messages.

- use the format `TAG:PRIORITY`
- e.g. `adb logcat ActivityManager:I MyApp:D *:S`

    - `*:S` - only show log messages for the previously defined sources
