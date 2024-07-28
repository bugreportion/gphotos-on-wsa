# Unlimited Photo Copying to the GPhoto on WSA

> 
> [!NOTE]
> Repository in the process of finalization. Current version is a machine translation and may contain inaccuracies.

## Preliminary Information
1. Photos and videos must be copied to the internal memory of the subsystem (userdata.vhdx); otherwise, the process won’t proceed. This can only be done directly within WSA itself.
2. If the volume of media being uploaded is too large, it is recommended to move the subsystem to another drive (preferably an SSD) to avoid overfilling the space on the main system partition where the WSA disk is located by default.
3. **The [Google Photos Unlimited Zygisk](https://gitlab.com/cuynu/gphotos-unlimited-zygisk) module on WSA works incorrectly!** Follow the instructions to set up a properly functioning unlimited backup.

## Installation
1. [Download the desired build type](https://github.com/MustardChef/WSABuilds/releases/) (I recommend using the KernelSU + MindTheGapps + RemovedAmazon version; other versions have had issues).
2. If you want to:
   - Install the subsystem on the main system partition, everything is as usual: unzip the folder from the archive to any convenient location, do **not delete** afterwards, rename it to WSA, and launch Run.bat.
   - Install the subsystem on a different partition:
     - Unzip the folder from the archive to any convenient location on the required drive, do **not delete** afterwards, rename it to WSA, and launch Run.bat.
     - After the first launch, go to the "Windows Subsystem for Android" application and terminate the subsystem using the **Disconnect** button.
     - Open the "Run" window (Win + R), navigate to %LOCALAPPDATA%/Packages/MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe/LocalCache
     - Cut out the metadata.vhdx and userdata.vhdx files and move them to the desired disk (possibly to the folder from where WSA was initially installed). The files may have slightly different names, such as userdata.**2**.vhdx.
     - Download and install [Link Shell Extension](https://schinagl.priv.at/nt/hardlinkshellext/linkshellextension.html#download), or:
       - choco install linkshellextension
       - winget install HermannSchinagl.LinkShellExtension
     - Go to the moved files in the new directories. Right-click on the userdata.vhdx file → (Windows 11) Show more options → Remember link source.  
Go back to %LOCALAPPDATA%/Packages/MicrosoftCorporationII.WindowsSubsystemForAndroid_8wekyb3d8bbwe/LocalCache → Right-click → Create as... → Symbolic link.
Do the same with the metadata.vhdx file.
WSA has been moved to a different drive.
3. Log in to your Google account. Download the Google Photos app. Navigate to the Windows Subsystem for Android application → Advanced settings → Experimental features → Allow access to user folders (enable this setting) → select the path to the folder with the content you want to upload.
4. Download and install the [KernelSU manager](https://github.com/tiann/KernelSU/releases), then the [Zygisk Next](https://github.com/Dr-TSNG/ZygiskNext/releases) and [LSPosed](https://github.com/begoniacommunity/list/blob/files/lsposed_no-logs.zip) modules. Restart the subsystem.
> How to install an app via adb [(Platform-tools package must be installed)](https://github.com/SunsetTechuila/Platform-Tools-Installer): navigate to the Windows Subsystem for Android application → Advanced settings → Developer mode. Open the Terminal and connect via the specified address, for instance:
adb connect 127.0.0.1:73924 (ignore the failed to authenticate error). Confirm the connection in the Android popup window by clicking Allow. Now execute the installation command, e.g., adb install KernelSU.apk.
6. Open the LSPosed manager through the notification or download it from [Google Play](https://play.google.com/store/apps/details?id=org.lsposed.manager&hl=en), then install the [Pixelify Google Photos](https://github.com/BaltiApps/Pixelify-Google-Photos/releases) module and activate it in LSPosed.
7. Launch the Pixelify GPhotos app, select Device to spoof → Pixel XL. Check the Customize feature flags menu, only the Pixel 2016 item should be checked. Restart the subsystem.
8. Open the Google Photos app and go to the account menu – if successful, you will see the message *Copy photos and videos from this Pixel device to the cloud for free and in unlimited amounts.*
9. Download and install [Material Files](https://github.com/zhanghai/MaterialFiles/releases). Your files are in the Windows folder. Transfer them to the internal memory of WSA (for example, in DCIM). The subsystem's space limitation is 130 GB. If the volume of media exceeds the available space, simply split your upload into several parts.
10. Return to Google Photos and enable photo copying to the cloud. The upload process will start automatically, and you can track it in the account menu.

## Confirmation
![proof](https://github.com/user-attachments/assets/42c0abb6-9044-42cd-aead-f154b86322e4)

## Additional Information
* What's wrong with the [Google Photos Unlimited Zygisk](https://gitlab.com/cuynu/gphotos-unlimited-zygisk) module?
The module apparently incorrectly patches the device's feature flags on the emulator, resulting in it being recognized as a Pixel XL, but when uploading to the cloud, the photos still occupy space in the free storage.
* Why is a build with KernelSU recommended rather than Magisk Canary?
At the time of writing, installing the latest current build with Magisk Canary on a partition other than the system one results in unknown errors, after which neither Magisk nor Google Play Services is installed.
