# ArcGIS Pro workshop for LA 5020 (Cerra), focusing on Athens, NY

Workshop 2025-02-26 by Keith Jenkins, GIS Librarian at Mann Library, Cornell University.\
This document is online at: <https://kgjenkins.github.io/la-5020-athens-ny/>

For help after this workshop, contact me at kgj2@cornell.edu  
Or set up a Zoom or in-person appointment at <https://guides.library.cornell.edu/gis/help>

All the data and documentation for this workshop can be downloaded from:\
<https://github.com/kgjenkins/la-5020-athens-ny/archive/main.zip>

After downloading the zip file, be sure to UNZIP it!  (Right-click > Extract All)

### Getting Started

* Open ArcGIS Pro
    * Login required -- see https://guides.library.cornell.edu/gis/arcgis
    * Use the "Map" template to create a new project
* Create your project in the `la-5020-athens-ny-main` folder that was extracted from the zip file

### Add town and village boundaries

* From the "boundaries" folder, drag the .shp files onto the ArcGIS map
* Adjust the symbology (in the Contents panel, double-click the color swatch under the layer name)
    * Symbology panel > Properties
    * Set Color = No color
    * Outline Color = something bright
    * Outline Width = 2pt
* Click the polygon to view attributes
 
### Add streets for Greene County

* Greene County streets were extracted from a statewide dataset, and saved as a GeoPackage .gpkg file
* GeoPackage files cannot be dragged-and-dropped onto the map
* Map menu > Add Data > Browse to file, double-click and add the "main.streets" layer
* Adjust symbology as needed
* Compare lines to the basemap -- are there any differences?
* Right-click the layer name > Attribute table

### Add parcels from web service

* Go to <https://gis.ny.gov/parcels>
* Open the "Web Services" link
* Copy the link to "NYS_Tax_Parcels_Public" (Feature Server)
* In ArcGIS, Map menu > Add Data From Path
    * <https://gisservices.its.ny.gov/arcgis/rest/services/NYS_Tax_Parcels_Public/FeatureServer>
* There is a "PROP_CLASS" attribute which contains a 3-digit code
* These property type classification codes are documented at:
    * <https://www.tax.ny.gov/research/property/assess/manuals/prclas.htm>

### Add buildings from web service

* Use the link to "BuildingFootprints" (Feature Server)

### Change the basemap

* Map menu > Basemap > Imagery Hybrid
* Notice that some building outlines are for structures that no longer exist
* Click one of those polygons to see the Source Date (2013)

### Add 2013 imagery to verify former structures
* Go to <https://gis.ny.gov/orthoimagery>
* Copy the link to "Web services"
* In ArcGIS, we'll need to add a server connection:
    * Insert menu > Connections > Server > New ArcGIS Server
    * Paste the copied URL: <https://orthos.its.ny.gov/arcgis/rest/services/wms>
    * Click OK
* Now we connect to the server and add an image layer
    * View menu > Catalog Pane
    * In the catalog pane, expand Servers > wms on orthos.its.ny.gov.ags > wms
    * Drag the "2013" layer onto the map (you may need to zoom in/out to see it)
* Note that some of the other available years don't cover Athens

### Add 10m elevation raster

* From the elevation folder, drag and drop the v48elu.dem file onto the map
* When prompted to "Build pyramids", click "No" (more useful with larger files)
* Under the layer name, double-click the gradient to open the Symbology Panel
* Change the Primary Symbology from "Stretch" to "Shaded Relief"
* Notice that this 10m raster is not very detailed for the study site

### Add 1m elevation raster

* From the elevation folder, drag the .img file onto the map
* When prompted to "Build pyramids", click "No"
* Under the layer name, double-click the gradient to open the Symbology Panel
* Change the Primary Symbology from "Stretch" to "Shaded Relief"
* Click the map to get the pixel value -- but unfortunately, ArcGIS rounds the value when using shaded relief!
* To avoid that, change the style from "Shaded Relief" to "Stretch" -- then clicking the map will give 0.01m precision

### Create contour lines

* Analysis menu > Tools
* Search for "Contour" and open the "Contour" tool
* Input raster = the .img file
* Contour interval = 1 (1m is possible with this high-resolution raster)
* Run

### Export to CAD

* Analysis tab > Tools > search for "Export to CAD"
* Input features = select all the layers you want to export
* Click the "Environments" tab at the top of the tool dialog
* Set "Output Coordinate System" to a meters-based system (not latitude/longitude)
    * Select a layer until you see something like "NAD_1983_UTM_Zone_18N"
    * Do NOT use a latitude/longitude system that begins with "GCS" (Geographic Coordinate System)
* Zoom/pan your map to frame your study area
* Under "Extent", click the first icon "Current Display Extent"
    * If you don't do this, you'll get the entire layer! (for example, all the streets in the county)


## Data sources

* Boundaries: <https://gis.ny.gov/civil-boundaries>
* Elevation: <https://www.orthos.dhses.ny.gov/>
* Imagery: <https://gis.ny.gov/orthoimagery> (web services link)
* Parcels and buildings: <https://gis.ny.gov/parcels> (web services link)
* Streets: <https://gis.ny.gov/streets-addresses> (Greene County extracted from statewide dataset)

More data is available in the Box folder for the class.  Many (but not all) data formats can be added by drag-and-drop onto the ArcGIS map.  If you get an error, try using the "Add Data" button on the Map menu.

Other sources:
* Historical Sanborn fire insurance maps <https://www.loc.gov/collections/sanborn-maps/about-this-collection/>
* Some of these are being georeferenced at <https://oldinsurancemaps.net/>
* CUGIR (Cornell University Geospatial Information Repository) <https://cugir.library.cornell.edu/>
* Geolode, a catalog of open geodata websites: <https://geolode.org/>