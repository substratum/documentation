# Building Substratum

In order to contribute any changes to Substratum, you will need to know how to
build the APK. This can be done in two ways: Android Studio or the command line.

A note about these APKs: these should only be used for testing purposes since
they are debug APKs (i.e. not signed with the official keys, meaning that they
cannot be installed over a Play Store version). They should not be included in
ROMs unless you are willing to build every time there is a new commit. We will
also not provide support for debug APKs.

# Android Studio

### 1. Grab the latest copy of Android Studio

<https://developer.android.com/studio/index.html>

Make sure you install the latest SDK and build tools.

### 2. Checkout the Substratum project

1. Open Android Studio
2. Click "Checkout project from Version Control"
3. Set up your Github credentials if you have not done so already
4. Put <https://github.com/nicholaschum/substratum> into the URL field and select where you want it cloned.
5. Hit Clone.
6. Hit Yes to opening the gradle file.
7. Hit OK on the next window to select the default values.

### 3. Build the APK

Click on the Build menu and select "Build APK". There will be a message with an
APK file once that is done.

# Command line

This is perfect for people with build servers or those who just prefer to work
from the command line.

NOTE: For the SDK and gradlew binary commands, macOS/Linux users may need to add `./` or `bash` before the command.

### 1. Grab the latest Android build tools

1. Download the command line tools via wget or curl: <https://developer.android.com/studio/index.html>
2. Unzip the file

   ```bash
   unzip -d <desired_folder_name> <zip_name>
   ```

3. Run the SDK manager to download the proper packages

   ```bash
   cd <desired_folder_name>
   tools/android update sdk --no-ui
   tools/android update sdk -u -a -t #
   ```

   Where as # is the number of the package you want to install. You will need the
   latest build tools (currently 25.0.3) and SDK (currently 25). You should be
   able to agree to the terms and conditions now, otherwise it will throw an error
   when attempting to build. If you need to download multiple packages, separate the
   numbers with a comma (1,2,3).

### 2. Specify where the SDK location is

```bash
export ANDROID_HOME=<full_sdk_path>
```

### 3. Clone the Substratum repo

```bash
git clone https://github.com/nicholaschum/substratum substratum
cd substratum
```

### 4. Build the APK

```bash
gradlew assembleDebug
```

The finalized APK will be in the app/build/outputs/apk folder within the Substratum repo folder.
