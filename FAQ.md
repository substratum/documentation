# Frequently Asked Questions

### 1. What is Substratum?

Substratum is an application that takes advantages of Sony's Overlay Manager
Service.

### 2. How does it work?

In a nutshell, we have added Sony's Overlay Manager Service to Android's framework,
which allows us to apply overlays (a changing of resources) to applications, which will
change their looks. To accomplish this, we have Theme Interfacer, which is compiled
inline with the ROM and placed into system with higher privileges, which acts as
the bridge between Substratum (the UI) and the framework by sending specialized
commands to OMS.

### 3. Is root required?

As of March 6th, 2017, root is no longer required for the vast majority of operations (application of overlays, sounds, fonts, and wallpapers). The major exception to this is the application of boot animations on encrypted data partitions.

### 4. How do I support Substratum?

By following our [adding Substratum support to your ROM](AddingSupport.md) guide!

### 5. Can Substratum be used without OMS changes?

Yes (henceforth referred to as legacy) but most functions will be unavailable aside
from overlays. The app will also require root to move the overlays into place
and some themes will not work with legacy.

### 6. How do I apply a theme?

1. Download the theme.
2. Open the Substratum app and click on the theme. You will see a notice that the resource cache is building and a notification to alert you of its progress. You can leave the app during this process if you would like.
3. Once the cache is built, click the theme again.
4. Navigate to the overlays tab.
5. Select the apps you want themed. If there are options for the overlay, select the ones that you want.
6. Click on the floating action button in the lower right-hand corner and select the "Build & enable" option.

Once the theme is done compiling, SystemUI will restart and the theme will be applied!

### 7. My theme looks weird or incomplete or my overlays did not apply.

1. Make sure that all of the theme applied (including framework). Rebuild the overlays if needed.
2. Do a full reboot. Occasionally, certain aspects will need a full reboot to be properly themed. One of the more common instances of this are notifications.
3. Make sure you are on an OMS-compatible ROM with all of the necessary exposures and Theme Interfacer. Stock ROMs do not theme will on Nougat. Ask your ROM developer to check [our SubstratumResources organization](https://github.com/SubstratumResources) and make sure their commits line up with ours.
4. Contact the themer to make sure that they have themed the aspect properly.
5. If all else fails, post in the [Substratum Google+ community](https://plus.google.com/communities/102261717366580091389) using the info below.

### 8. What do I include in a bug report?

1. A detailed description of the issue
2. A screenshot of Substratum settings
3. Theme being used
4. A logcat ([guide here](https://raw.githubusercontent.com/nathanchance/Android-Tools/master/Guides/Proper_Bug_Reporting.txt))

### 9. How can I contribute to translating the app in my native language?

Please go to our [Crowdin](http://translate.projektsubstratum.com) and start translating our strings!
