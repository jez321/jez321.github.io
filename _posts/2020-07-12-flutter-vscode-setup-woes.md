---
layout: post
title: 'Flutter VSCode setup woes'
date: 2020-07-12 11:49:30 +0900
categories: flutter vscode
---

While attempting to [set up flutter](https://flutter.dev/docs/get-started/install){:target="\_blank"} for development, I came across a few issues which I'll briefly run through below, along with their solutions.

## Setting the Android SDK path

Running `flutter doctor` (the command that checks everything is set up as it should be), I came across an error claiming that the Android SDK could not be found.
The solution was to specify the path to the Android SDK explicitly with the following command:
`flutter config --android-sdk <path-to-your-android-sdk-path>`

## Detecing Android Virtual devices

The next issue I came across was that flutter on VSCode could not detect my Android Virtual Devices (AVDs). In this case I was attempting to use an older x86 image running an older version of Android which I don't believe should be an issue (I was even able to launch the app on the same emulator using Android Studio), but after some googling around for a solution, I was eventually able to get it working by creating a new x86_64 image using the latest Android build. x86_64 architecture and the latest build of Android should not be required to connect to an AVD however, it was more likely due to the image being created a long time ago with an old version of the Android SDK, so simply recreating the AVD with the same settings would probably have worked as well.

## Connecting to an Android Virtual Device

After getting my target AVD to show up in VSCode, I then found that I was not able to actually connect to it. On attempting to run the sample app, it would get stuck forever on the 'Waiting for application to connect' message.
The problem appeared to be an issue with my launch configuration, adding back the default launch configuration and running it finally allowed me to connect to the AVD from within VSCode and view the default counter app in all it's glory!
If you need to restore the default launch configuration, just copy the folloing code into `.vscode/launch.json`.

```json
{
  "name": "Flutter",
  "request": "launch",
  "type": "dart"
}
```

If you don't have a `.vscode/launch.json` you shouldn't have to worry as you should already have the default launch configuration. If you'd like to create a `launch.json` to be sure, you can do so by clicking the cog icon in the 'Run' tab of VSCode.

![Add launch configuration](/assets/2020-07-12-flutter-vscode-setup-woes/add-launch-configuration.png)

{% include share-buttons.html %}
