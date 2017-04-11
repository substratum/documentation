# Adding Substratum support to your ROM

In order to add Substratum support to your ROM, you will need to add our changes
to your appropriate repos and inline Theme Interfacer. We prefer that the Substratum
app be downloaded from the Play Store by the users who want it but if you want
to inline it, it must be included as a prebuilt (which I will go over below).

If you are based on LineageOS, you may consider checking out [this thread](https://forum.xda-developers.com/apps/substratum/reference-lineageos-substratum-support-t3580276), as it will be tailored specifically to that ROM. Anything AOSP based should follow this guide.

# Step 1: Add our framework changes

We keep all of our framework changes in the [SubstratumResources organization](https://github.com/SubstratumResources).

Currently, there are changes in the following repos (between OMS7 and our
exposures that we have tried to label).

+ [frameworks/base](https://github.com/SubstratumResources/platform_frameworks_base/commits/n-mr2)
+ [frameworks/native](https://github.com/SubstratumResources/platform_frameworks_native/commits/n-mr2)
+ [packages/apps/Contacts](https://github.com/SubstratumResources/platform_packages_apps_contacts/commits/n-mr2)
+ [packages/apps/ContactsCommon](https://github.com/SubstratumResources/platform_packages_apps_ContactsCommon/commits/n-mr2)
+ [packages/apps/Dialer](https://github.com/SubstratumResources/platform_packages_apps_Dialer/commits/n-mr2)
+ [packages/apps/ExactCalculator](https://github.com/SubstratumResources/platform_packages_apps_ExactCalculator/commits/n-mr2)
+ [packages/apps/PackageInstaller](https://github.com/SubstratumResources/platform_packages_apps_PackageInstaller/commits/n-mr2)
+ [packages/apps/PhoneCommon](https://github.com/SubstratumResources/platform_packages_apps_PhoneCommon/commits/n-mr2)
+ [packages/apps/Settings](https://github.com/SubstratumResources/platform_packages_apps_settings/commits/n-mr2)
+ [system/core](https://github.com/SubstratumResources/platform_system_core/commits/n-mr2)
+ [system/sepolicy](https://github.com/SubstratumResources/platform_system_sepolicy/commits/n-mr2)

For the projekt_*.xml files, you can add those changes to your own ROM's xml
files without any issues. If you get merge conflicts on any of the framework
changes, look back on the history for the file and see why it was altered (most
CAF ROMs will run into this issue due to changes to AssetManager).

I hope that everyone running a ROM knows how to run git but if not, here is a
brief breakdown on how to fetch our changes.

```bash
git fetch URL BRANCH
git cherry-pick SHA1
```

Example:
```bash
git fetch https://github.com/SubstratumResources/platform_frameworks_base n-mr2
git cherry-pick 7b1db662f29429470ae603f070aedbdb5851f155
```

You can also cherry pick the changes all together by typing:
```bash
git cherry-pick FIRSTSHA1^..SECONDSHA1
```

Example:
```bash
git cherry-pick 7b1db662f29429470ae603f070aedbdb5851f155^..9500b19884081a9d09521a96bf4a057f1d3e5ec7
```

# Step 2: Compile Theme Interfacer

First, you will need to track our Theme Interfacer package by adding the following to
your manifest (leave out the remote if you already have one for Github):

```xml
<remote name="github"
        fetch="https://github.com/" />

<project path="packages/apps/ThemeInterfacer" name="substratum/interfacer" remote="github" revision="n-rootless" />
```

You may also fork it and add our changes as we push them (you will need to pay
close attention to our repos as Theme Interfacer changes will occasionally need to line
up with a new Substratum release.)

After that, you will need to add Theme Interfacer to the list of packages to build in
your vendor:

```makefile
PRODUCT_PACKAGES += \
    ...\
    ...\
    ...\
    ThemeInterfacer
```

After that, you are done! You can build your ROM and download the app from the
Play Store!

Let us promote you if you do decide to add support. Fill out the ROM submission
form in our [supported ROMs list](SupportedROMs.md) so we can add you!

# Compiling Substratum as a prebuilt

Should you want to inline Substratum into your ROM directly, you must do it using
this procedure so that users can properly update from the Play Store.

The latest Substratum APK can be retrieved from [APK Mirror](http://www.apkmirror.com/apk/projekt/substratum-theme-engine/).

Add this bit to your Android.mk file for your prebuilt apps (assuming the Substratum
APK in that same folder, otherwise change the LOCAL_SRC_FILES line):

```makefile
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)
LOCAL_MODULE := Substratum
LOCAL_MODULE_TAGS := optional
LOCAL_MODULE_CLASS := APPS
LOCAL_BUILT_MODULE_STEM := package.apk
# Make sure the build system doesn't try to resign the APK
LOCAL_CERTIFICATE := PRESIGNED
LOCAL_DEX_PREOPT := false
LOCAL_SRC_FILES := Substratum.apk
include $(BUILD_PREBUILT)
```

This will keep the certificate of the APK intact so that the Play Store can
install updates successfully. If you include debug APKs, we will not support
your users.
