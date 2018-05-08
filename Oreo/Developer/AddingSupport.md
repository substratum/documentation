# Adding Substratum support to your ROM

In order to add Substratum support to your ROM, you will need to add our changes
to your appropriate repos. We prefer that the Substratum
app be downloaded from the Play Store by the users who want it but if you want
to inline it, it must be included as a prebuilt (which I will go over below).

# Step 1: Add our framework changes

We keep all of our framework changes in the [SubstratumResources organization](https://github.com/SubstratumResources).

Currently, there are changes in the following repos (between OMS7 and our
exposures that we have tried to label).

+ [build/make](https://github.com/SubstratumResources/platform_build/commits/o)
+ [frameworks/base](https://github.com/SubstratumResources/platform_frameworks_base/commits/o)
+ [packages/apps/Settings](https://github.com/SubstratumResources/platform_packages_apps_settings/commits/o)
+ [system/sepolicy](https://github.com/SubstratumResources/platform_system_sepolicy/commits/o)

For the projekt_*.xml files, you can add those changes to your own ROM's xml
files without any issues.

```bash
git fetch URL BRANCH
git cherry-pick SHA1
```

Example:
```bash
git fetch https://github.com/SubstratumResources/platform_frameworks_base o
git cherry-pick 7fd7a11e7c933dfa2e23a8a1ca3577bc8da19f0a
```

You can also cherry pick the changes all together by typing:
```bash
git cherry-pick FIRSTSHA1^..SECONDSHA1
```

Example:
```bash
git cherry-pick f18f319d6b262c13dae2469183be1d0dd863c72f^..7fd7a11e7c933dfa2e23a8a1ca3577bc8da19f0a
```

You are done! You can build your ROM and download the app from the
Play Store!

Let us promote you if you do decide to add support. Send a PR to
our [supported ROMs list](SupportedROMs.md) so we can add you!

# Compiling Substratum as a prebuilt

Should you want to inline Substratum into your ROM directly, you must do it using
this procedure so that users can properly update from the Play Store.

The latest Substratum APK can be retrieved from [GitHub releases)(https://github.com/substratum/substratum/releases/latest)

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