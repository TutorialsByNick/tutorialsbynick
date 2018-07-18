---
layout: post
title: "Android Studio FTC Tools: Making common tasks easier and faster"
comments: true
author: Nicholas Day
email: true
category: "FTC Basics"
---

In Android Studio, there is a feature called _External Tools_. This adds links under the `Tools->External Tools` header that runs command line programs. Why is this useful for FTC? We can add commands that let us easily connect to the robot over wireless, upload code wirelessly and update the Driver Station's app quickly.

# Table of Contents

- TOC
{:toc}

Go to `File->Settings` and search for `external tools` in the search box in the top left. A screen like below should show up.

![Android Studio External Tools]

I have already made my tools, but to add a tool click the green `+`.

# Restarting ADB Tool

This is the tool that will restart ADB to use over the network. Enter in information like I did below:

![Restart ADB Tool]

So there are a lot of fields here, but the most important ones are

- `Name`
  - This is the name of your tool
- `Program`
  - This is the program being called
  - We are calling `adb` which stands for Android Debug Bridge. Internally Android Studio uses this to upload your app apk install files over usb
- `Parameters`
  - These are the things passed to the program
  - Here we are telling `adb` what port to restart on and what port it will use to connect to the phone
- `Working directory`
  - This is where the directory where the program is called from

There are also some weird `$`'s inside of the program:

- `$ModuleSdkPath$`
  - This means where the Android SDK is (which is where `adb` is located)
- `$ProjectFileDir$`
  - This is the current project's directory

# Connecting over Wifi Tool

This tool will actually connect over wifi from your computer to the phone.

![Wifi Connect Tool]

Inside the `Parameters`, you tell `adb` to connect to a certain IP address and port. The port is the one we specified earlier, and the IP address is the identifier used to find the Robot Controller on the network. You'll need to change this to whatever IP address is listed under the Robot Controller's About page which is under the menu button in the top right.

# Actually Connecting over Wifi

To connect to the phone wirelessly and update code, you need to connect to the phone's wifi network first. On one of the phones click the menu icon in the top right corner and click _About_. The phone's wireless network name and password should be displayed. The IP address of the Robot Controller should also be displayed. If it isn't on that phone try either the other Driver Station or Robot Controller in the pair. Then once you've done that, connect the Robot Controller to the computer. Now you'd use the `Tools->External Tools->Restart ADB` tool and a small window at the bottom of Android Studio should pop up. Once that has finished working, unplug the phone from your computer. Then run the `Tools->External Tools->Connect over Wifi` tool and it should show your phone as connected! :)

# Install Driver Station Tool

Sometimes when the FTC SDK updates, bugfixes are released or helpful updates are added. When this happens, we need to update the Robot Controllers code, and the Driver Station app. Helpfully, FTC keeps the Driver Station app apk installer file inside of `YourProjectNameFolder/doc/apk/FtcDriverStation-release.apk`. We can also use `adb` to install programs! Let's make the tool to do this:

![Install Driver Station Tool]

# Actually installing the Driver Station

Now to update the Driver Station, all you have to do is

- Uninstall the current version of the Driver Station app from the phone
- Connect the Driver Station phone to the computer
- Check allow this computer always on the phone so that we are allowed to install it
- Click on `Tools->External Tools->Install Driver Station`
- It should be updating now!

# The End

These features may take a bit to set up, but they pay off in the long run with the time they save. You'll save lots of time not having to download the Driver Station from the app store, and plugging and unplugging your Robot Controller constantly from the computer. You'll also save your usb port some stress and make it last longer.

[Android Studio External Tools]: {{ site.url }}/images/android-studio-tools-ftc/external-tools.png
[Restart ADB Tool]: {{ site.url }}/images/android-studio-tools-ftc/restart-adb.png
[Wifi Connect Tool]: {{ site.url }}/images/android-studio-tools-ftc/connect.png
[Install Driver Station Tool]: {{ site.url }}/images/android-studio-tools-ftc/install-ds.png
