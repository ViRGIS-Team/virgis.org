---
layout: virgis
title: 3D Geospatial Systems
nav_order: 3
parent: Design Philosophy
description: "Discussion of the structure of GIS in 3D and VR"
---

# ​Purpose

The purpose of this section is to provide some background and discussion into the complications of 3D Geospatial Systems and the design decisions being made.

Read this section to get a deeper understanding of the reasoning behind some of the design decisions made in the ViRGIS App.


# ​Sources

The following are some of the sources for this discussion

Tet-Khuan, C., Rahman, A.A. & Zlatanova, S. (2007) 3D spatial operations in geo DBMS environment for 3D GIS. In: _ResearchGate_. 26 August 2007 pp. 151–163.

Laksono, D. & Aditya, T. (2019) Utilizing A Game Engine for Interactive 3D Topographic Data Visualization. _ISPRS International Journal of Geo-Information_. 8 (8), 361.

De Roo, B., Bourgeois, J. & De Maeyer, P. (2017) Usability Assessment of a Virtual Globe-Based 4D Archaeological GIS. In: Alias Abdul-Rahman (ed.). _Advances in 3D Geoinformation_. Cham, Springer International Publishing. pp. 323–335.

De Roo, B. (2016) A GEODATA INFRASTRUCTURE FOR ARCHAEOLOGY: FLEXIBILITY IN MANAGEMENT AND ANALYSIS. In: _ResearchGate_. [Online]. 28 June 2016 Available from: doi:10.5593/SGEM2016/B21/S08.071 [Accessed: 22 March 2020].

van Oosterom, P., Martinez-Rubi, O., Tijssen, T. & Gonçalves, R. (2017) Realistic Benchmarks for Point Cloud Data Management Systems. In: Alias Abdul-Rahman (ed.). _Advances in 3D Geoinformation_. Cham, Springer International Publishing. pp. 1–30.

Rahman, A.A., Karim, H., Jamali, A., Buyuksalih, G., et al. (2018) Conceptual Framework Towards Unified 3D Topological Modelling and Visualization Based on CityGML. In: _ResearchGate_. [Online]. 1 May 2018 Available from: [https://www.researchgate.net/publication/323382865_Conceptual_Framework_Towards_Unified_3D_Topological_Modelling_and_Visualization_Based_on_CityGML](https://www.researchgate.net/publication/323382865_Conceptual_Framework_Towards_Unified_3D_Topological_Modelling_and_Visualization_Based_on_CityGML) [Accessed: 22 March 2020].

Nicholas Duggan FRGS Cgeog (GIS) (2015) “Why 3D GIS is the Future”: [https://www.xyht.com/spatial-itgis/3d-gis-future/](https://www.xyht.com/spatial-itgis/3d-gis-future/)

Martin Dobias (2019) New QGIS 3D capabilities and future plans reviewed in [https://hub.packtpub.com/new-qgis-3d-capabilities-and-future-plans-presented-by-martin-dobias-a-core-qgis-developer/](https://hub.packtpub.com/new-qgis-3d-capabilities-and-future-plans-presented-by-martin-dobias-a-core-qgis-developer/)

De Roo, B., Bourgeois, J. & De Maeyer, P. (2017) Usability Assessment of a Virtual Globe-Based 4D Archaeological GIS. In: Alias Abdul-Rahman (ed.). _Advances in 3D Geoinformation_. Cham, Springer International Publishing. pp. 323–335.

Zou, M. (2013) An Algorithm for Triangulating 3D Polygons. All Theses and Dissertations (ETDs). 1212.

Roth, G. & Wibowoo, E. (1997) An Efficient Volumetric Method for Building Closed Triangular Meshes from 3-D Image and Point Data. In: ResearchGate. [Online]. 1 January 1997 Available from: https://www.researchgate.net/publication/221474907_An_Efficient_Volumetric_Method_for_Building_Closed_Triangular_Meshes_from_3-D_Image_and_Point_Data [Accessed: 16 July 2020].

Maur, Pavel Delaunay Triangulation in 3D. [Online] Available from: https://www.kiv.zcu.cz/site/documents/verejne/vyzkum/publikace/technicke-zpravy/2002/tr-2002-02.pdf.

Kenneth Rose, Alla Sheffer, Jamie Wither, Marie-Paule Cani, Boris Thibert (2007) Developable Surfaces from Arbitrary Sketched
Boundaries. Available from https://hal.inria.fr/inria-00337445/document [accessed June 2020]


# ​Some Terminology and Realms

**Real-World Space** - space defined by geographic coordinates and by real-world units (e.g. metres). This space is always projected and z-up.

**VR--Space** - space defined in the virtual world in the coordinate system of the VR world. This is an unprojected coordinate system and y-up.

**GIS World** - refers to the paradigm space of Geospatial Information and the tools and processes used there.

**VR World** - refers to the paradigm space of the VR and gaming systems and the tools and processes used there.

**World Space Coordinates** - refers to the Unity World Space Coordinate System. The Map Space Coordinates are transformed into the World Space Coordinates by the zoom of the model.

**Map Space Coordinates** - refers to the Coordinate System of the GIS Model. The Map Space Coordinate System is a Transverse Mercator projection with units of 1m (i.e. 1m is mapped to one Unity unit) with the center of the projection placed at the origin of the model as defined in the Project.JSON file and the axis transposed to be y-up.

**Data Coordinates** Each RecordSet has a Coordinate Reference System (CRS). This is usually a well-known CRS such as EPSG:4326. 


# ​Geometry

ViRGIS creates a limited extent geodetically projected coordinate system in the VR Space, where the ellipsoid is represented as a planar datum. This tool is intended for limited extent GIS or Spatial analysis problems where the planar projection is not a problem. If an ellipsoid representation of the datum is required, this is not the tool.

This space can be zoomed - this changes the base relationship between VR Space units and Real World Space units (which is a nominal 1m per unit).

Real-world Points, Lines and Polygons etc are projected into this VR Space using standard projection techniques.


# ​Basics - moving from 2D to 3D

## Coordinate systems don’t change. 

We continue to use the same Coordinate Reference Systems and datums. With all of the same tools needed and problems associated.

## Altitudes are not Always Altitudes

Z, or more traditionally Altitude, has always been used in GIS but has not been a core coordinate and as such the handling is less well defined. Z can be:
    1. Relative to the Ellipsoid,
    2. Relative to the Geoid,
    3. Relative to local ground level or a dedicated local datum,
    4. Relative to a regional datum such as MSL.
    
In 2D GIS, in most cases Z is just a DEM (i.e. an attribute), so this did not matter and since Z is a data attribute and not actually a coordinate, if the data is wrong or missing it does not change the geometry. This is not true in true 3D space. 

In the VR World, all Z values from the Real-World Space are projected into Y values in the VR Space coordinate system relative to the ellipsoid. Thus, the Z values must be ellipsoid-height figures.

## Points are Points

A point (with Z value) is a simple 3D entity. No difference there.

2D points - i.e. LatLngs - have to be dealt with since they are valid data points in the GIS formats used. The current assumption will be to place these points on the ellipsoid. The preferred approach is to deal with these points in the data acquisition phase and in the GIS - basically to give all points valid Z values before they get to the VR Space. 

There are some additional types of symbology. Using the experience quoted by QGIS 3D, a good starting point is:

- Basic shape and colour. The basic shapes in Unity are sphere (actually ellipsoid since it can be scaled in each dimension), cube (actually right cuboid since it can be scaled in each dimension) & right elliptical cylinder and the colours are defined by a standard RGBA color space. So - we shall start with that.
- Using 3D models (i.e. meshes) as 3D icons. This capability is practically OOTB with Unity, but providing the library of Icons and semantics to define them in the Project.json will take some time.
- Billboards. I.e. 2D sprites that always face the viewer. Creating Text based Billboards is simple in Unity and will be used in ViRGIS V1 for labelling. Adding texture should not be complicated but has the same problem of library and semantics as b).

## Lines remain Lines

A line is a set of points or vertices and, provided all vertices have a Z value, is a simple 3D entity although it should be noted for completeness that the length of the line measured in 3D may not be the same as the length of the line measured in 2D.

The symbology questions are primarily:

- “Simple” or “Buffered” - i.e. whether the width is defined in VR-World units or in Real-World Units and projected to VR-World units. In Virgis, for V1 and V2, only simple lines will provided since buffered lines have the ability to break the VR illusion.

- Shape. In the VR-World (more so than the 3D GIS World) every entity needs solid structure for the brain to process it correctly. Lines with zero depth don’t work. Therefore, all lines will be represented by cuboids or right elliptical cylinders. 

As a note, the line segment is created by elongating the mesh along the z-axis in VR Space. That means the characteristics of the line symbology (i.e. cross section) are set by the X and Y values of the scale vector in VR Space. To keep consistency, the scaling is still written as a 3D transform in z-up format. This means that in the project.json file, the x and z values set the width and depth of the line. The y value should always be 1, since the y-value is created when drawing the line.

## Polygons are difficult

As discussed in Tet-Khuan et al and elsewhere, Polygons are not actually 3D shapes and a number of assumptions have to be made:

The assumption in 2D GIS is that a polygon is planar and orthogonal to the view (i.e. that all vertices have the same Z value). It is possible create this polygon in the VR Space either :
- As a 2D Mesh, or
- As a prism whose cross section is the polygon.

For ViRGIS, we have not used either of these methods. We have assumed that solid bodies, such as might be represented by approach ii) will come into the App as either a group of polygons or as a mesh. These two statements are functional the same as described below but have different meanings in term of the formats used. A group of polygons might be represented by a GeoJSON file while a mesh is more likely to be presented as a .OBJ file etc.

It is possible to construct a polygon with 3D points. This is sometimes called a polygonZ and is assumed to be planar. Due to projection, the shape of this polygon might not the same as the shape seen in 2D GIS.

If it is not planar, it is a polyhedral.

For features presenting as polygons, we have chosen the following method

*   A Polygon is represented by a set of linear rings as defined in GeoJSON, 
*   There are no constraints on the Z values of the vertices and no assumptions that the Polygon is actually planar although there is an assumption tha the surface is developable (i.e.  surfaces that can be unfolded into the plane with no distortion),
*   This polygonZ is turned into a triangulated mesh by identifying the plane closest to the set of points made by the verteces of the outer linear ring using a least-square method, projecting all of the linear rings onto that plane and getting the Delaunay Triangulation for the polygon made up of the projected linear rings. A mesh is then made from that triangulation and the original 3D verteces in world space coordinates. Note that for a planar polygon, the polygon will at this point still be planar but represented by a triangulated mesh rather than a polygon. Also note that because of the projection, it is possible for a valid hole in the origingal GIS representation (i.e. the xy plane in real world space) to be invalid in the projected polygon because it is not contained by the outer linear ring. In this case, the innner linear ring is ignored.
*   The polyhedral can now be manipulated by moving any of vertices.
*   The polyhedral is returned back to the GIS world by returning the linear rings. This will then be projected into the 2D GIS world automatically, since that world will ignore the z values as coordinates and just use the x and y values.

This means that all polygons become internally just a special case of a mesh.  

For symbology, the mesh needs to be constructed from a material that is covered with a texture. This texture can be computed, e.g. flat or cross-checked, where the color and possible other parameters have to be configured, or it can be a link to an image in .PNG or .JPEG format.

One characteristic of a polygon over a mesh is the linear ring - which can take symbology as well. This allows the edges in a polygon mesh to be high-lighted. This is not simply possible in a standard Unity mesh.

## Meshes are New

In the VR World, meshes become a very important feature type. Meshes are 2.xD surfaces made up of small planar polygons joined at the edges with a large number of vertices.

[ToDO - more research on the use of mesh in GIS] 

In Unity, meshes can have triangular or quad faces, but for performance and greater consistency with the GIS TIN formats, we will only be using triangulated meshes. 

ViRGIS V1 will include arbitrary meshes as georeferenced objects in the model and allow the position, scale and rotation of the mesh to be manipulated.

ViRGIS v1 assumes that, for meshes coming from “non-polygon” formats (e.g..OBJ), all data about the material, texture and colour of the mesh is included in the mesh data and no additional symbology is provided.

Each mesh definition file (which may contain one or more individual meshes) is created in the model as its own `RecordSet` object or GIS layer.

## Point Clouds are New

A point cloud is a large set of 3D points each of which has attributes (e.g. colour) and together make up some structure. The key point here is the size of the dataset. 

Point Clouds are important for LiDAR analysis and for Photogrammetry.

ViRGIS V1 loads Point Cloud data into a Unity Particle system to provide a performant way of presenting very large numbers of points in the VR World.
