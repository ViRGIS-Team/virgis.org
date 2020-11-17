---
layout: virgis
title: Installation
nav_order: 2
description: "ViRGiS Installation Instructions"
permalink: /installation
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

# Basics
{: .no_toc}

Virgis is build in Unity.

There are two seperate code bases for ViRGIS:

- Version 1 - simple version all in c# with limited functionality
- Version 2 - complete version with external C++ plugins that only work currently on Windows.

---

# Version 1

Version 1 is intended primarily to be a technology demontsrator and an experiemental rig. It is built entirely in c# and has no external dependencies.

This has less functionality than V2 and can only load a limited set of files in EPSG:4326 CRS but works across all of the platforms : MacOS, Windows Desktop, Quest VR and Rift VR.

By default, the player expects to be next to a folder called `test-data` that contains a file called `gisproject.json`. This should be a complete and valid project.json file and will define the model that the player will load.

The repository is complete Unity project that will build a basic player that has all of the ViRGIS functionality but is fairly basic in terms of the user experience in starting the project.

You can change the user experience and the player experience in your own applications by normal Unity development but it is not part of the core ViRGIS project to provide this user experience.

## Download
{: .no_toc}

You can either :

1. clone the repository to your local machine and use Unity to build your own version of the player, or

1. download one of the pre-built players from the [releases page](https://github.com/ViRGIS-Team/ViRGIS/releases).

---

# Version 2

Version 2 is the current production version. It has much more functionality and can access a wide range of file types but currently is only supported on Windows-x64 platforms - Rift VR and Windows Desktop.

Version 2 is released as a Unity Package Manager (UPM) package available from  [the Virgis_V2 repo](https://github.com/ViRGIS-Team/ViRGiS_v2).

Verions 2 is also available as a Unity Project that consumes the Virgis_V2 package. This project is intended primarily for development, testing and as a example for other developers and not as an end product. The development project is available [in the Virgis_dev repo](https://github.com/ViRGIS-Team/ViRGiS_Dev).


---

# Installation

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
