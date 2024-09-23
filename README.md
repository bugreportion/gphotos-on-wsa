# Unlimited Photo Backup to the Google Photo on WSA

## Before you start
1. Photos and videos must be copied to the internal memory of the subsystem (userdata.vhdx); otherwise, the process won’t proceed. This can only be done directly within WSA itself.
2. If the amount of media being uploaded is too large, it is strongly recommended to move the subsystem to another partition (preferably if it belongs to an SSD) to avoid overfilling the space on the main system partition where the WSA disk is located by default.
3. **The [Google Photos Unlimited Zygisk](https://gitlab.com/cuynu/gphotos-unlimited-zygisk) module on WSA works incorrectly!** Follow the instructions to set up a properly functioning unlimited backup.

## Manual
1. [Download the desired build type](https://github.com/MustardChef/WSABuilds/releases/) (I recommend using the KernelSU + MindTheGapps + RemovedAmazon version; other versions have had issues).
2. If you want to:
   - Install the subsystem on the main system partition, everything is as usual: unzip the folder from the archive to any convenient location, do **not delete** afterwards, rename it to WSA, and launch Run.bat.
   - Install the subsystem on a different partition:
     - Unzip the folder from the archive to any convenient location on the required drive, do **not delete** afterwards, rename it to WSA, and launch Run.bat.
     - After the first launch, go to the "Windows Subsystem for Android" app and terminate the subsystem using the **Turn off** button or `WsaClient /shutdown` command.
     - Open "Run" window (Win + R), navigate to `%LOCALAPPDATA%/Packages/MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe/LocalCache`
     - Cut out the metadata.vhdx and userdata.vhdx files and move them to the desired partition (for ex. to the folder from where WSA was initially installed). The files may have slightly different names, such as userdata.**2**.vhdx.
     - Download and install [Link Shell Extension](https://schinagl.priv.at/nt/hardlinkshellext/linkshellextension.html#download), or run in Terminal:
       - `winget install HermannSchinagl.LinkShellExtension`
       - `choco install linkshellextension`
       - You also can use [mklink command.](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/mklink)
     - Go to the moved files in the new directories. Right-click on the userdata.vhdx file → (Windows 11) Show more options → Remember link source.
     - Go back to `%LOCALAPPDATA%/Packages/MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe/LocalCache` → Right-click → Create as... → Symbolic link. Do the same with the metadata.vhdx file.

Now WSA has been moved to a different drive.

3. Log into your Google account. Download the Google Photos app. Navigate to the Windows Subsystem for Android application → Advanced settings → Experimental features → enable Share user folders → select the path to the folder with the media you want to upload.
4. Download and install the [KernelSU Manager](https://github.com/tiann/KernelSU/releases), then the [Zygisk Next](https://github.com/Dr-TSNG/ZygiskNext/releases) and [LSPosed](https://github.com/begoniacommunity/list/blob/files/lsposed_no-logs.zip) modules. Restart the subsystem.
> How to install an app via adb [(Platform-tools package must be installed)](https://github.com/SunsetTechuila/Platform-Tools-Installer): navigate to the Windows Subsystem for Android application → Advanced settings → Developer mode. Open the Terminal and connect via the specified address, for instance:
adb connect 127.0.0.1:73924 (ignore the failed to authenticate error). Confirm the connection in the Android popup window by clicking Allow. Now execute the installation command, e.g., adb install KernelSU.apk.
6. Open the LSPosed Manager through the notification or download launcher from [Google Play](https://play.google.com/store/apps/details?id=org.lsposed.manager&hl=en), then install the [Pixelify Google Photos](https://github.com/BaltiApps/Pixelify-Google-Photos/releases) module and activate it in LSPosed.
7. Launch the Pixelify GPhotos app, select Device to spoof → Pixel XL. Check the Customize feature flags menu, only the *Pixel 2016* should be checked. Restart the subsystem.
8. Open the Google Photos app and go to the account menu – if successful, you will see the message *Copy photos and videos from this Pixel device to the cloud for free and in unlimited amounts.*
9. Download and install any file explorer for Android (ex. [Material Files](https://github.com/zhanghai/MaterialFiles/releases)). Your files are stored in the Windows folder. Transfer them to the internal memory of WSA. The subsystem's space limitation is 130 GB. If the volume of media exceeds the available space, simply split your files in several parts.
10. Return to Google Photos and enable photo copying to the cloud. The upload process will start automatically. You can track it in the account menu.

## Confirmation
![proof](https://github.com/user-attachments/assets/42c0abb6-9044-42cd-aead-f154b86322e4)

## Additional Information
* What's wrong with the [Google Photos Unlimited Zygisk](https://gitlab.com/cuynu/gphotos-unlimited-zygisk) module?
The module apparently incorrectly patches the device's feature flags on the emulator, resulting in it being recognized as a Pixel XL, but when uploading to the cloud, the photos still occupy space in the free storage.
* Why is a build with KernelSU recommended rather than Magisk Canary?
At the time of writing, installing the latest current build with Magisk Canary on a partition other than the system one results in unknown errors, after which neither Magisk nor Google Play Services is installed.
