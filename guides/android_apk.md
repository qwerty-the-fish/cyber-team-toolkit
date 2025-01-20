# Reverse Engineering an Android APK

**Android Package Kit (APK)** - a file format used to install and distribute Android apps.
- compressed archives (use tools such as `unzip` and `apktool` to decompress the file)
- specifically a JAR (Java Archive)
- contains everything needed to install the app: code, assets, and resources

## Structure

[appdome - Structure of an APK File](https://www.appdome.com/how-to/devsecops-automation-mobile-cicd/appdome-basics/structure-of-an-android-app-binary-apk/)

- `META-INF`
  - generated when signing the application - contains verification information
  - prevents modifications - any change means the app needs resigning otherwise the OS will reject the installation
  - contains two files:
    - `CERT.SF` - list of files and their associated SHA-1 hashes
    - `CERT.RSA` - contains the signed content of the `CERT.RF` - used to verify app integrity with the public key
    - `MANIFEST.MF`
      - contains the SHA-256-Digest of all the APK files
      - prevents modification - used to verify file validity - any changes causes the signature to be revoked

- `classes.dex`
  - contains the compiled Java bytecode of the application
  - optimised for the Dalvik Virtual Machine (DVM) or the Android Runtime (ART) 

- `res/`
  - holds resource files used by the application
  - uses a pre-defined folder hierarchy:
    - `drawable/` - images and icons
    - `layout/` - XML files - define the layout of the UI
    - `values/` - XML files - contain strings, colours, dimensions, etc.
  - allow the developer to provide alternatives for different screen orientations, languages, OS versions, etc. 
  
- `AndroidManifest.xml`
  - [Android developer guide](https://developer.android.com/guide/topics/manifest/manifest-intro)
  - contains key information about the application such as:
    - package name and ID
    - applications components such as activities and resources
    - required permissions
    - supported Android versions

- `lib/` - optional
  -  contains native libraries/ machine code (`.so` files) for specific device architectures
  -  Android is cross-platform - contains a subfolder for each supported processor (e.g. `arm64-v8a`, `x86`, `mips`, etc.)

- `assets/` - optional
  - additional assets the app needs - e.g. game data, sound files, configuration files, etc. 

- `resources.arsc`
  - compiled resources in a binary format - e.g. strings and styles

For example:
```
APK (ZIP archive)
├── META-INF/
│   ├── MANIFEST.MF
│   ├── CERT.SF
│   └── CERT.RSA
├── classes.dex
├── res/
│   ├── drawable/
│   ├── layout/
│   └── values/
├── AndroidManifest.xml
├── lib/ 
│   ├── armeabi/ 
│   │   └── libnative.so
│   ├── armeabi-v7a/
│   │   └── libnative.so
│   └── ...
├── assets/
│   ├── game_data.txt
│   └── sounds/
└── resources.arsc
```

## Actions

### Install the APK on your Android device
- connect to the device via `adb` (make sure `USB debugging` is enabled)
- `adb install [PATH-TO-APK]` - e.g. `adb install file.apk`

### Decode the `.apk` file using `apktool`
- decode the `.apk` file and store the extracted files in the specified directory
- `apktool d [PATH-TO-APK] -o [PATH-TO-OUTPUT-DIRECTORY]` - e.g. `apktool d file.apk -o decoded_files`

### Convert the `.apk` file to `.jar` format
- the advantage of converting to the `.jar` format is that we can then use `jd-gui` to view the Java code
