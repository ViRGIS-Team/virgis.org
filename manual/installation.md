# Installation 

# Basics

Virgis is build in Unity.

The repository is complete Unity project that will build a basic player that has all of the ViRGIS functionality but is fairly basic in terms of the user experience in starting the project.

By default, the player expects to be next to a folder called `test-data` that contains a file called `gisproject.json`. This should be a complete and valid project.json file and will define the model that the player will load.

You can change the user experience and the player experience in your own applications by normal Unity development but it is not part of the core ViRGIS project to provide this user experience.

## Versions

There are two seperate code bases for ViRGIS

- ***Version 1*** has more limited functionality and can only load a limited set of files in EPSG:4326 CRS but works across all of the platforms : MacOS, Windows Desktop, Quest VR and Rift VR, and

- ***Version 2*** has much more functionality and can access a wide range of file types but currently is only supported on Windows-x64 platforms - Rift VR and Windows Desktop.

## Download

You can either :

1. clone the repository to your local machine and use Unity to build your own version of the player, or

1. download one of the pre-built players from the [releases page](https://github.com/ViRGIS-Team/ViRGIS/releases).

In the future, ViRGIS will also be available as a Unity Package.

For the rest of this document, it will assumed that you want to use the player download option.

Select the latest version of the file you want and downloaded it.

## Installation - Windows, Mac & Oculus Rift 

The file will be a zip file. Expand the zip and there will an application (.app or .exe), some additional files in Windows and a directory called `test-data` with some test data and test models.

The player is now ready to go. Open the .app or .exe and the player will load.

Note that the installation instructions for Windows Desktop and Windows Rift VR are exactly the same - just using different downloads. The VR version assumes that you have a Rift or Quest in Rift Link mode and that the Oculus software is loaded and running.

## Installation - Oculus Quest

The download is a zip of an APK file and the `test_data` directory.

These have to be loaded seperately onto the Quest.

- The test data needs to be loaded into the following directory on the Quest :

```
/sdcard/virgis
```

- This can be done by placing the Quest into a file-transfer connection with the PC (like any other Android device) and doing the transfer.
- The APK must be sideloaded onto the Quest. The easiest way of doing this is to use SideQuest. Follow the [instructions](https://sidequestvr.com/setup-howto) for setting up SideQuest and then use SideQuest on the PC to upload the APK. 
