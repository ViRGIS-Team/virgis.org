---
layout: virgis
title: Creating a Project / Application from ViRGiS v2
nav_order: 1
parent: ViRGiS Version 2
description: "ViRGiS Version Packaging Structure"
permalink: /packaging
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# Packaging Stucture

**ViRGiS** v2 is made up a set of [Unity Package Manager](https://docs.unity3d.com/Packages/com.unity.package-manager-ui@2.0/manual/index.html) (UPM) packages that can loaded into Unity projects to create applications.

## Structure

```
+
|
+-- ViRGiS_V2
|   |
|   +-- GDAL
|   |
|   +-- PDAL
|   |
|   +-- MDAL
|   |
|   +-- GeoJSON.Net
|   |
|   +-- Geometry3Sharp
|   |
|   |-- Newtonsoft.JSON for Unity
|   |
|   +-- Delaunator-sharp
|
+-- Project Namespace
```

All of the UPM dependencies are included as package dependencies in **ViRGiS** v2 _except the Project Namespace_. **ViRGiS** has a dependency on the existance of a `Project` namespace but does _NOT_ include this as a package dependency. This allows the Application developer to create their own version of the namespace; which in turn allows the developer to add layers and config options to **ViRGiS** without needing to change the core code.

**ViRGiS** uses [Reactive](https://github.com/dotnet/reactive) for event management. This needs to be loaded as aNuget package, and there is no mechanism for setting up a UPM dependency on a Nuget package. See below for details of installation.

## Installation

To add ViRGiS v2 to you Project, add the following lines to the `manifest.json` file:

```
    "com.virgis.project_ns": "https://github.com/ViRGIS-Team/Project-Namespace.git",
    "com.virgis.virgis_v2": "https://github.com/ViRGIS-Team/ViRGiS_v2.git",
```

# Creating a new Unity Project

## Using the default Developement Project

There is a development and testing project for **ViRGiS** V2. This includes the core package, the Mapbox SDK, the Oculus Integration package and a basic UI and movement interface.

The simplest way of creating a new Application would be to clone this project and develope from there.

This Project can be found in the [ViRGiS_Dev](https://github.com/ViRGIS-Team/ViRGiS_Dev) repo.

## Creating a new Project

It is of course possible to create a new project from scratch. This would be required, for instance, if you do not want to use MapBox or to work on Oculus or want to provide a different UI.

We do not provide a detailed recipe for creating a completely new project. We have listed below, approximately, the steps required to recreate the default Developement project and it is up to you to work out how to change the steps!

1. Create a new Unity URP project
> _the package shaders are only designed for URP_,
2. Install [Nuget for Unity](https://github.com/GlitchEnzo/NuGetForUnity) from the Github package, as in the documentation,
3. Use Nuget for Unity to install the System.Reactive package,
> _System.Reactive is a Nuget dependency for ViRGiS_
4. Add the Scoped Registries to `manifest.json` 
> _There is a deficiency in UPM that means that the scoped registries must be defined in the Project and not in the `package.json`_
```
"scopedRegistries": [
    {
      "name": "package.openupm.com",
      "url": "https://package.openupm.com",
      "scopes": [
        "com.openupm",
        "com.virgis.gdal",
        "com.virgis.geojson.net",
        "com.virgis.geometry3sharp",
        "com.virgis.mdal",
        "com.virgis.pdal",
        "jillejr.newtonsoft.json-for-unity",
        "com.nol1fe.delaunator"
      ]
    },
    {
      "name": "npmjs",
      "url": "https://registry.npmjs.org/",
      "scopes": [
        "io.extendreality"
      ]
    }
  ]
```
5. Install platform dependent packages for the platform you want to run on. For instance, for the Oculus platform used in the dev project install the Oculus Unity Integration package from the Unity Asset store.
6. If you want to include MapBox in the app, install the MapBox Unity SDK unitypackage as per the [MapBox documentation](https://www.mapbox.com/install/unity/). The will need to create an account and an SDK token if you do not have one already.
> _Note that if you do NOT include MapBox in the project, you will need to create yor own version of the Project namespace excluding MapBox dependencies_
7. There is a clash between MapBox and GDAL because they both contain a copy of sqlllite.dll. Delete the SQL native plugin in the MapBox folder.
8. A fix needs to be applied to MapBox to make it work with URP. See [this article](http://barankahyaoglu.com/dev/mapbox-unity-sdk-with-urp/).
9. For Mapbox to work, there needs to be a custom layer defined for MapBox and a prefab GameObject. See the dev project for examples.
10. The abstract Map object in the prefab must have the `Use Relative Height` flag set.
11. You will need to create a map container to contain the GIS artfacts. This should be an empty GO with a component attached that is an extension of the `Virgis.MapInitialise` class with the logic added to allocate layer objects to RecordSet entities. See the dev project for an example.
12. You will need to create the UI. **ViRGiS** provides some prefabs and methods to help with this, including:

- Menus
- Head Up Display
- Pointer
- Feature Add Tool

See the dev project for examples about how to use them.

**ViRGiS** can work sucessfully with both the Input Manager and the InputSystem.

