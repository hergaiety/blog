---
title: The Great App Store Trials
description: Becoming a Published Play Store Developer
date: 2017/08/13
tags:
  - App
  - Retrospective
---

[Today marks my first day as a published app store developer](https://play.google.com/store/apps/details?id=io.cordova.myspells). It's been a dream of mine to release work I've done not just on the web, but as something native you can put in your pocket without needing a browser. Some stories are of great heroes who overcome dangerous challenges through incredible feats of might; this one is of the problems and solutions of releasing a web app to the Play Store.

## Act I: Building the App

I chose the [Quasar Framework](http://quasar-framework.org/) powered by [Vue.js](https://vuejs.org/) with [Cordova](https://cordova.apache.org/) mobile conversion built in. **Choosing tools that played well together** assured me that if I _read the documentation_ and put in the effort **I'd eventually succeed**.

**Release often**. Advice I give to anyone and even easier to follow for a hobbyist project. Hit your **minimum viable product then release** the app to the public.

### Problem: Releasing a Web App Cheaply and Easily

I'm no server admin. I've built my app and just wish to see it online for public consumption.

#### Solution: Netlify

Open Source projects can be automatically deployed and built directly from a Github repo for free to the [Netlify](https://www.netlify.com/) servers. Once hosted you get a simple URL to include in your project.

### Problem: Bugs

They happen, bugs are a natural part of application development. Keeping a todo list on your computer seems counter to the connected open source world we live in.

#### Solution: Github Issues

Being transparent in logging bugs has a number of benefits. [Github Issues](https://guides.github.com/features/issues/) is a great tool for this.

* As easy as a todo list.
* Great practice, especially if you _follow [SemVer](http://semver.org/)_ and write _clean commits_.
* Users know what's busted and have a window into helping to _fix the bugs themselves_.
* **Forms a public history for the project** while _encouraging a changelog_ as the app evolves.

## Act II: Building for Android

Generally [Quasar makes compiling for Android easy](http://quasar-framework.org/guide/quasar-play-app.html) and enjoyable. Running their mobile dev tools unveiled several mobile specific bugs, which I logged then fixed.

Quasar's easy tools are great for quick feedback but are nothing compared to a real debugging APK running on your phone. Luckily there are docs for [wrapping your Quasar app in Cordova](http://quasar-framework.org/guide/cordova-wrapper.html).

### Problem: Running Cordova Built APK

The documentation drops off quickly after Cordova has done its job.

> You find yourself in a wolf's den of opinions and tools in a world of assumed knowledge.

Emulation through [Android Studio](https://developer.android.com/studio/index.html) is possible, but I could never get it to work with my non-Android-Studio app.

#### Solution: Cordova compile to device.

After some digging, the most successful way to compile to my Android device was:

1. `quasar build` from my **root**.
2. `quasar run --device` from the **cordova directory** while my **phone was plugged** in with **USB Debugging** turned on.

This automatically compiles and opens the app on your connected Android device.

_P.S. Android Studio may still be required here._

##### Also... Overcoming USB Debugging

Enabling USB Debugging on modern Android phones is the opposite of obvious. Luckily, [this guide to Android USB debugging](https://www.kingoapp.com/root-tutorials/how-to-enable-usb-debugging-mode-on-android.htm) explains the process.

##### Also... Overcoming USB Cable Differences

I encountered times where USB debugging refused to work. Turns out _some usb cables only transfer power and not data_. Use the correct USB cable type to avoid wasted time for silly reasons.

#### Problem: Local Ajax Calls Don't Work

JSON cannot be fetched locally as we could on Netlify. I did not wish to bake in all of my data on the web app to slow down initial load.

#### Solution: Bake in data for the app build only.

For my web app, the only concern with baking in data was app size for first load. On mobile that's not a problem. In fact, baking in the data means an even easier offline solution.

I wrote a [data processor](https://github.com/sharpshark28/my_spells/blob/master/build/process_spells.js) node script that could either compile my data to a JSON file or to a JS importable module (with `export default ...`) along with some [package.json build scripts](https://github.com/sharpshark28/my_spells/blob/master/package.json) to simplify the process during development and releases. In the app, I always import the JS module and if there is `data.length > 0` I use it, else I attempt to fetch the JSON file.

It took effort, but assured that my both the web and android app were quick to launch.

## ACT III: Publishing

Congratulations! You have an app that runs on Android. Next, you must fumble through the _app publishing process_. I've done my best to list the steps, problems and solutions below.

### Step: You Want Money and My Soul?

First step is registering for a Publisher Account with your Google User. This involves agreeing to many terms of services and paying a **fee of $25** that separates you from the potential onslaught of crapware and spam that may otherwise reach the Play Store. Relatively straightforward and _a necessary evil_ to progress.

### Problem: Releasable APK file

Up until now _we've been using a debugging APK_ file. That's not good enough for release.

#### Solution: Cordova Build

`cordova build` will create an android-release-unsigned.apk that is, as the filename implies, an **unsigned but otherwise ready to release APK**. 

### Problem: Signing the APK file

One of the least documented parts of the process is signing the APK outside of a completely Android Studio made app.

#### Solution: Android App Studio, Keystore, jarsigner

1. Install [Android Studio](https://developer.android.com/studio/index.html) and launch it
2. Open an Existing Project... choose the cordova created project directory for the app
3. Build -> Generate Signed APK
4. Key Store Path: Create New (follow onscreen prompts)
  - Note the place you've saved it, and what the key alias is (key0 is fine)
5. Close Android Studio, we'll instead use jarsigner to sign our apk:
  ``` bash
  jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore <~/path/to/keystore.jks> <~/path/to/android-release-unsigned.apk> <KEY ALIAS>
  ```

### Problem: Installing onto Android Device

Let's get it running on our Android once again, signed and ready to release.

`adb install ~/path/to/android-release-signed.apk`

#### Solution: Installing `adb`

`adb` can be installed from the Android Studio Preferences screen:

1. Appearance & Behavior > System Settings > Android SDK > SDK Tools
2. Check Android SDK Build-Tools, Android SDK Platform-Tools, Android SDK Tools
3. If `adb` still isn't available, correct your path like so: https://stackoverflow.com/questions/10303639/adb-command-not-found 

Now running `adb install` on your apk will install directly to your device.

### Problem: zipalign

While uploading to the Play Store you may see a notice that the apk is not zipaligned.

#### Solution: zipalign it

Unfortunately this is not a tool we can install by itself, but it does come with Android Studio.

The command we desire to run is something like:

`zipalign -v 4 ~/path/to/file.apk ~/path/to/newfile.apk`

Replace `zipalign` with the path to it on your machine, likely under your android studio sdk directory. 

---

Finally we have a **signed, zipaligned, releasable APK file ready for the Play Store**. Follow the prompts on the site and your app will hopefully be published within a day.

I encourage others to write about their experiences building apps for the Play Store. I'm sure there are simpler ways to achieve the same result with fewer headaches. Ultimately, having a published app on the Play Store is a very satisfying experience and this document will serve as a reminder of the trials I've been through in an attempt to inform others of the problems that may be encountered along the way with some solutions that worked for me.

Stuck with a similar project? Reach out to me on Twitter @SharpShark28
