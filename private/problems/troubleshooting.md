__PROBLEMS__  

# __*Troubleshooting errors*__  

This activity aims to help you practice troubleshooting your scripts in Earth Engine. Each script below contains several errors. Your task is to fix the errors and articulate a rule of thumb for handing each type of error in your workflows.

Please do the following: 

1. Make a "troubleshooting" folder in your Earth Engine repository. 
2. Start a new script for each of the workflows below. 
3. Fix the errors and document how you fixed the errors in this [worksheet](http://geography.middlebury.edu/howarth/ee_edu/eePatterns/troubleshooting/troubleshooting.pdf){target=_blank}. 

Please note, you will receive a copy of this worksheet in lab. 

At the end of lab, please fill out [__this form__](https://docs.google.com/forms/d/e/1FAIpQLScqqeMHvZEcMsjW8ScJ3syq1DPZlsCfWEzHb87plA5hHNbBWQ/viewform?usp=sf_link){target=_blank} where you will submit links to your scripts. Please ask an instructor if you need help getting links to your scripts.

_Thank you._

---  

## __practice 01__

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:     Oct 14, 2024
    TITLE:    Troubleshooting Practice 1

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/



// -------------------------------------------------------------
//  Access image from this cloud address:
//  "projects/ee-patterns/assets/p01/chipmanHill_2023_35cm_DEMHF"
// -------------------------------------------------------------

var image = ee.ImageCollection("projects/ee-patterns/assets/p01/chipmanHill_2023_35cm_DEMHF");

print("FIRST IMAGE", image);

// -------------------------------------------------------------
//  Customize Map. 
// -------------------------------------------------------------

// Set map center and zoom level.

Map.centerObject(image, 15);

//  Set basemap style to hybrid.

Map.setOptions('HYBRID');

// -------------------------------------------------------------
//  Display image as a map layer;
//  Stretch layer display values over image data range.
// -------------------------------------------------------------

// Print min and max values of image. 

print("Min & max value of image", geo.iCart.iMinMax(image));

// Chart histogram of actual data values.

print("Image histogram", geo.iCart.iHistogram(image));

// Define viz dictionary. 

var single_viz = 
    {
        min: [86],        
        max: [246],        
    }
;

// Add map layer. 

Map.addLayer(image,single_viz,"Digital Elevation Model (meters)");


var i_min_max = geo.iCart.iMinMax(image);

print("Min & max value of image", i_min_max);

Map.addLayer(image, {min: 96, max: 247}, "Image displayed by min and max", false);

// -------------------------------------------------------------
//  Calculate the PERCENT slope of each location in image. 
// -------------------------------------------------------------

var image_slope = ee.Terrain.slope(image);

var image_slope_percent = image_slope.divide(180).multiply(Math.PI).tan().multiply(100);

// -------------------------------------------------------------
//  Display slope image as a map layer;
//  Stretch layer display values over image data range.
// -------------------------------------------------------------

print("slope min max", geo.iCart.iMinMax(image_slope_percent));

var output_histogram = geo.iCart.iHistogram(image_slope_percent);

print("slope histogram", output_histogram);

Map.addLayer(image_slope_percent, {min:0, max: 87}, "Image slope - steeper is darker");

// -------------------------------------------------------------
//  Calculate the hillshade of each location in image. 
// -------------------------------------------------------------

var image_hs = ee.Terrain.hillshade(image.multiply(2), 45, 315);

print("hs min max", geo.iCart.iMinMax(image_hs));

var output_histogram = geo.iCart.iHistogram(image_hs);

print("hs histogram", output_histogram);

Map.addLayer(image_hs, {}, "Image hillshade");

// -------------------------------------------------------------
//  Calculate the deviation from mean elevation;
//  Use 10 as the distance argument.
//  Try to display the layer with this palette: ['blue', 'white', 'red']
// -------------------------------------------------------------

var image_dme = geo.iTerrain.devFromMeanElev(image, 10);

print("dme min max", geo.iCart.iMinMax(image_dme, 3));  

var output_histogram = geo.iCart.iHistogram(image_dme);

print("dme histogram", output_histogram);

Map.addLayer(image_dme, {min: -1, max:1, palette: ['blue', 'white', 'red']}, "Image DME");


```

---

## __practice 02__  

```js

 /*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:     Oct 14, 2024
    TITLE:    Troubleshooting Practice 02

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/


var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// -------------------------------------------------------------------------------
//  Gather image from "projects/ee-patterns/assets/p02/NOAA-CoNED-SOCAL".
//  Print a histogram - do you see land vs ocean floor in the histogram?
// -------------------------------------------------------------------------------

// var bathy = ee.Image("projects/sat-io/open-datasets/gebco/gebco_grid/gebco_2023_n900_s00_w-1800_e-900");

var image = ee.Image("projects/ee-patterns/assets/p02/NOAA-CoNED-SOCAL");

print("Image", image);

// Chart histogram of data values.

print("Image histogram", geo.iCart.iHistogram(image, 30));

// -------------------------------------------------------------------------------
//  Area of interest for practice problem.
// -------------------------------------------------------------------------------

var aoi = image;


// Center map on aoi at zoom level 9 and set base layer to hybrid.

Map.centerObject(aoi, 9);
Map.setOptions('hybrid');


// -------------------------------------------------------------------------------
//  Apply a vertical exageration (z-factor) of 2 to elevation data for hillshade. 
//  Make a hillshade from this image and display the hillshade image as layer on Map.
// -------------------------------------------------------------------------------

var image_ve = image.multiply(2);

var image_hs = ee.Terrain.hillshade(imagee_ve, 315, 35);

Map.addLayer(image_hs, {min:255, max:0}, "Hillshade");

// -------------------------------------------------------------------------------
//  Separate the original elevation image (without vertical exageration) into two different images:

//  (1) land elevations
//  (2) ocean floor elevations (bathymetry)

//  Each image should only store land or bathymetry elevation values, respectively.
//  All other values should be masked.
// -------------------------------------------------------------------------------

var image_land = image.selfMask(image.gt(0));

print("image land", image_land);

var image_bathy = image.updateMask(image.lte(0)) ;

// -------------------------------------------------------------------------------
//  Reclassify the bathymetry image at equal 100 meter intervals. 
//  Display the reclassified image as layer on Map with 0.5 opacity.
//  To improve contrast, set max of viz dictionary such that all locations less than -2000 m (or class 20) are the darkest blue in palette.
//  Use this palette: geo.iPalettes.iBathy.eleven
// -------------------------------------------------------------------------------

// Equal intervals

var image_bathy_reclass = geo.iReclass.equalInterval(aoi, -100);

// Print min and max values of image. 

print("Min & max value of bathy reclass", geo.iCart.iMinMax(image_bathy_reclass, 30, aoi));

// Chart histogram of actual data values.

print("Bathy histogram", geo.iCart.iHistogram(image_bathy_reclass, 30, aoi));

// // Define viz dictionary. 

var viz_bathy = 
    {
        max: [20],        
        min: [0], 
        palette: geo.iPalettes.iBathy.eleven
    }
;

// Add map layer. 

Map.addLayer(image_bathy_reclass,viz_bathy,"Bathymetry", 1, 0.5);

// -------------------------------------------------------------------------------
//  Define the Pleistocene shoreline as 130 meters lower than today's shoreline.
//  Make a boolean image that shows all land above ocean in Pleistocene.
//  Display boolean image as layer on Map with all non-land masked.
// -------------------------------------------------------------------------------

var image_pleistocene = image_bathy.add(130);

var image_pleistocene_boolean = image_pleistocene.gt(0);

var image_pleistocene_boolean_simple = image_bathy.gte(-130).updateMask();

Map.addLayer(image_pleistocene_boolean.selfMask(), {min:0, max:1, palette: "#ffffff"}, "Pleistocene Land", 1, 0.5);

// -------------------------------------------------------------------------------
//  Reclassify the land image at equal 100 meter intervals. 
//  Display the reclassified image as layer on Map with 0.5 opacity.
//  Use this palette: geo.iPalettes.iHypso.bartholomew
// -------------------------------------------------------------------------------

var image_land_reclass = geo.iReclass.equalInterval(image_land, 100);

print("image land reclass", image_land_reclass);

// Print min and max values of image. 

print("Min & max value of land_image_reclass", geo.iCart.iMinMax(image_land_reclass, 30, aoi));

var viz_land = 

    {
        min: [0],        
        max: [30], 
        palette: geo.iPalettes.iHypso.bartholome
    }
;

Map.addLayer(image_land_reclass,viz_land,"Image land", 1, 0.5);




```

---  

## __practice 03__  

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:     October 14, 2024
    TITLE:    Troubleshooting Practice 03

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/


var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 


// -------------------------------------------------------------
//  DATA SOURCES 
// ------------------------------------------------------------- 

var fc_address_county = "TIGER/2018/Counties";
var fc_address_town = "projects/conservation-atlas/assets/cadastre/Boundary_TWNBNDS_poly";
var fc_address_parcel = "projects/vt-conservation/assets/state/FS_VCGI_OPENDATA_Cadastral_VTPARCELS_poly_standardized_parcels_SP_v1";
var fc_address_soils = "projects/conservation-atlas/assets/soils/VT_Data_NRCS_Soil_Survey_Units";
var ic_address_dem = "USGS/3DEP/1m"; 

var palette_soils = geo.iPalettes.iSoils.parent_materials_addison_county;
var class_labels_soils = geo.iPalettes.iSoils.parent_materials_addison_county_labels;

print("SOILS Palette and Class labels", palette_soils, class_labels_soils);

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  1. GATHER HUMAN GEOGRAPHY
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  1.1 Make Addison County layer
// -------------------------------------------------------------

var fc_county = ee.FeatureCollection(fc_address_county)
  .filter(ee.Filter.eq("NAME", "ADDISON"))
;

print(
  "COUNTY first row",
  fc_county.first()
);


Map.addLayer(fc_county, {color: 'yellow'}, "1.1: Addison County", false);

var result_1p1 = fc_county; 

// -------------------------------------------------------------
//  1.2 Make study town (Middlebury) layer
// -------------------------------------------------------------

var town_name = "Middlebury";

var fc_town = ee.FeatureCollection(fc_address_town)
  .filter(ee.Filter.eq("TOWNNAME",  town_name.toUpperCase()))
;

Map.addLayer(fc_town, {color: 'green'}, "1.2: Study town: ".concat(town_name), false);

var result_1p2 = fc_town; 

// -------------------------------------------------------------
//  1.3 Center map on study town
// -------------------------------------------------------------

Map.centerObject(fc_town, 13);
Map.setOptions('hybrid');

// -------------------------------------------------------------
//  1.4 Make parcels in study town layer
// -------------------------------------------------------------

var fc_parcels = ee.FeatureCollection(fc_address_parcel);

print(
  "PARCEL first row",
  fc_parcels.first()
);


// Filter by attribute  

var fc_filtered_parcels = fc_parcels.filter(
  ee.Filter.eq('TOWN', town_name.toUpperCase()))
;

// Check filtered result.  

print(
  "Parcels Townname",
  fc_parcels.size(),
  fc_filtered_parcels.size()
);

// Add filtered data to map.  

Map.addLayer(fc_filtered_parcels, {color: 'cyan'}, "1.4: Parcels in Study Town", false);

var result_1p4 = fc_filtered_parcels;

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  2. GATHER SOILS DATA AND FILTER FOR ADDISON COUNTY 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  2.1 Gather soils data
// -------------------------------------------------------------

// Gather fc data from address.

var fc_soils = ee.FeatureCollection(fc_address_soils);

// Inspect the table.  

// print(
//   "SOILS",
//   "number of rows",
//   fc_soils.size(),
//   "names of columns",
//   fc_soils.first().propertyNames(),
//   "first row of table",
//   fc_soils.first(),
//   "unique values for target column",
//   fc_soils.aggregate_array('PARENT').distinct().sort()
// );

// Display as map layer. 

Map.addLayer(fc_soils, {color: 'white'}, "2.1: Vermont Soils", false);

var result_2p1 = fc_soils;

// -------------------------------------------------------------
//  2.2 Filter for soils that overlap Addison County
// -------------------------------------------------------------

// Filter feature collection by bounds of another vector dataset. 

var fc_filter_bounds_soils = fc_soils.filter(
    ee.Filter.bounds(fc_county)
);

// Check filtered result.  

// print(
//   "FC SIZE BEFORE VS AFTER FILTER",
//   fc_soils.size(),
//   fc_filter_bounds_soils.size()
// );

// Add filtered data to map.

Map.addLayer(fc_filter_bounds_soils, {color: 'magenta'}, "2.2 Soils that overlap Addison County", false);  

var result_2p2 = fc_filter_bounds_soils; 

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  3. MAKE PARENT MATERIAL IMAGE FOR STUDY TOWN. 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  3.1 Make nominal image of soil parent material. 
// -------------------------------------------------------------

var image_nominal_soils = geo.fcConvert.toNumericImage(fc_filter_bounds_soils, "PARENT")
;

// -------------------------------------------------------------
//  3.2 Mask by Addison County.
// -------------------------------------------------------------

var image_boolean_county = geo.fcConvert.toBooleanImage(fc_county);

var image_with_mask_soils = image_nominal_soils.updateMask(fc_county);

// -------------------------------------------------------------
//  3.3 Display masked soils image as layer. 
// -------------------------------------------------------------

var viz_soils = {
  
  min: 0,
  max: 10,
  palette: palette_soils
  
};

Map.addLayer(image_with_mask_soils, viz_soils, "3.3 Parent Materials of Addison County");

var result_3p3 = image_with_mask_soils;

// -------------------------------------------------------------
//  3.4 Add legend to botom-left of Map. 
// -------------------------------------------------------------

var legend_nominal_soils = geo.iCart.legendNominal(
  "PARENT MATERIAL", 
  viz_soils, 
  class_labels_soils, 
  "bottom-left"
  )
;

// Add legend to Map.  

Map.add(legend_nominal_soils);


// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  4. GATHER DEM 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  4.1 Construct image collection. 
// -------------------------------------------------------------

var ic_dem = ee.ImageCollection(ic_address_dem);

// print(
//   "IC DEM", 
//   ic_dem.size(),
//   ic_dem.first() 
// );

// -------------------------------------------------------------
//  4.2 Filter for images that overlap Addison County.
// -------------------------------------------------------------

var ic_filtered_dem_county = ic_dem.filter(ee.Filter.bounds(image_boolean_county));

// print("IC DEM Addison", ic_filtered_dem_county.first(), ic_filtered_dem_county.size());

// -------------------------------------------------------------
//  4.3 Mosaic filtered image collection to image. 
// -------------------------------------------------------------

var ic_dem_mosaic = geo.icFlatten.mosaicToImage(ic_filtered_dem_county);

// print("Mosaic", ic_dem_mosaic);

// -------------------------------------------------------------
//  4.4 Mask mosaic image by Addison County. 
// -------------------------------------------------------------

var image_with_mask_dem = ic_dem_mosaic.updateMask(image_boolean_county);

// -------------------------------------------------------------
//  4.5 Make hillshade from masked image and display as layer with 0.5 opacity.
// -------------------------------------------------------------

var hs = ee.Terrain.hillshade(image_with_mask_dem, 315, 35);

Map.addLayer(hs, {min:0, max: 255}, "4.5 Hillshade", true, 0.5);

var result_4p5 = hs;

// -------------------------------------------------------------
//  4.6 Make hillshade from masked image and display as layer with 0.5 opacity.
// -------------------------------------------------------------

var slope = ee.Terrain.slope(image_with_mask_dem);

Map.addLayer(slope, {min:45, max:0}, "4.6 Slope", false, 0.5);

var result_4p6 = slope;

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  5. PAINT STROKES
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  5.1 Make strokes for parcels ("white" and 0.5 weight) and add as layer.
// -------------------------------------------------------------

var strokes_parcels = geo.fcCart.paintStrokes(fc_filtered_parcels, "white", 0.5);

Map.addLayer(strokes_parcels, {}, "5.1 Parcel Outlines");

// -------------------------------------------------------------
//  5.2 Make strokes for town ("white" and 4 weight) and add as layer.
// -------------------------------------------------------------

var strokes_town = geo.fcCart.paintStrokes(fc_town, "white", 4);

Map.addLayer(strokes_town, {}, "5.2 Town Outlines");



```

---  

## __practice 4__  

```js
/*     
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:   10/2/2024       
    TITLE:  Troubleshooting Practice 4   

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// Feature collections

var vt_town_address = "projects/conservation-atlas/assets/cadastre/Boundary_TWNBNDS_poly";
var rare_address = "projects/conservation-atlas/assets/rarity/Significant_Natural_Communities";
var large_blocks_middlebury = "projects/ee-patterns/assets/vt-conservation/t04_habitat_blocks";

// Images

var valley_bottom_address = "projects/vt-conservation/assets/champlain_basin/LakeChamplainBasin";
var imp_address = "projects/vt-conservation/assets/landcover/STATEWIDE_2022_50cm_LANDCOVER_Impervious";


// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  1. Define study region.
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  1.1 Define study town (Middlebury)
// -------------------------------------------------------------

var town = ee.FeatureCollection(vt_town_address);

var study_town = town
  .filter(ee.Filter.eq("TOWNNAME", "MIDDLEBURY"));
  
Map.addLayer(study_town, {color: "black"}, "1.1 Study Town", false);

// print(study_town, study_town.first().getNumber("SHAPE_area").divide(4046.86));

var result_1p1 = study_town;

// -------------------------------------------------------------
//  1.2 Convert study town into boolean (to use as mask later)
// -------------------------------------------------------------

var town_mask = geo.fcConvert.toBooleanImage(study_town);

Map.addLayer(town_mask, {min:0, max:1}, "1.2 town mask", false);

// -------------------------------------------------------------
//  1.3 Define aoi as study town and towns that overlap (share boundary) with study town.
// -------------------------------------------------------------

var aoi = town.filterBounds(study_town);

Map.addLayer(aoi, {color: "white"}, "1.3 Area of interest (aoi)", false);


var result_1p3 = aoi;

// -------------------------------------------------------------
//  1.4 Convert aoi into a boolean (to use as mask later).
// -------------------------------------------------------------

var aoi_mask = geo.fcConvert.toBooleanImage(aoi);

Map.addLayer(aoi_mask, {min:0, max:1}, "1.4 aoi mask", false);

// -------------------------------------------------------------
//  1.5 Center map on study town and set basemap to hybrid. 
// -------------------------------------------------------------

Map.centerObject(study_town, 12);
Map.setOptions('hybrid');

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  2. Make blocks inclusive of rare communities.  
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  2.1 Gather habitat blocks cloud asset that overlap aoi. 
// -------------------------------------------------------------

var blocks_asset = ee.FeatureCollection(large_blocks_middlebury)
  .filterBounds(aoi)
;

Map.addLayer(blocks_asset, {color: 'GreenYellow'}, "2.1 Blocks overlap aoi", false);

var result_2p1 = blocks_asset;

// -------------------------------------------------------------
//  2.2 Convert 2.1 to a boolean image.
// -------------------------------------------------------------

var image_boolean_blocks = geo.fcConvert.toBooleanImage(blocks_asset)
  .updateMask(aoi_mask)
;

// var classes_areas = geo.iZonal.areaClasses(image_boolean_blocks.unmask(), 5, study_town, "max");

// print(
//     "Area (square meters) blocks",
//     classes_areas
// );

// var class_percent_of_region = geo.iZonal.classPercentRegion(classes_areas);

// print(
//   "Area (percent of region)",
//   class_percent_of_region
//   )
// ;

print("image_boolean_blocks", image_boolean_blocks);

Map.addLayer(image_boolean_blocks, {min:0, max:1}, "2.2 Blocks boolean", false);

// -------------------------------------------------------------
//  2.3 Gather rare natural communities that overlap aoi.
// -------------------------------------------------------------

var rare_nc = ee.FeatureCollection(rare_address)
  .filterBounds(aoi)
;

Map.addLayer(rare_nc, {color:'cyan'}, "2.3 Rare Natural Communities overlap aoi", false);

var result_2p3 = rare_nc;

// -------------------------------------------------------------
//  2.4 Make boolean image of rare natural communities that overlap aoi.
// -------------------------------------------------------------

var image_boolean_rare = geo.fcConvert.toBooleanImage(rare_nc)
  .updateMask(aoi_mask)
;

Map.addLayer(image_boolean_rare, {min:0, max:1}, "2.4 Image rare", false);

// -------------------------------------------------------------
//  2.5 Find locations that are either blocks or rare natural communities.
// -------------------------------------------------------------

var blocks_or_rare = image_boolean_blocks.or(image_boolean_rare);

Map.addLayer(blocks_or_rare, {color: "Yellow"}, "2.5 Blocks or Rare", false);

var classes_areas = geo.iZonal.areaClasses(blocks_or_rare, 5, study_town, "max");

// print(
//     "Area (square meters) + rarity",
//     classes_areas
// );

// var class_percent_of_region = geo.iZonal.classPercentRegion(classes_areas);

// print(
//   "Area (percent of region)",
//   class_percent_of_region
//   )
// ;

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  3. Classify habitat blocks versus habitat connectors.  
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  3.1 Gather valley bottom, make it boolean (anything not 0 is true), and mask for aoi.
// -------------------------------------------------------------

var valley_bottoms = ee.Image(valley_bottom_address)
  // .neq(0)
  .updateMask(aoi_mask)
;

var output_min_max = geo.iCart.iMinMax(valley_bottoms, 10, study_town);

print("Min & max value of valley bottom image", output_min_max);

Map.addLayer(valley_bottoms, {min:0, max:1}, "3.1 Valley bottoms", false, 1);

// -------------------------------------------------------------
//  3.2 Erase all impervious land from valley bottoms.
// -------------------------------------------------------------

var imp = ee.Image(imp_address)
  .unmask()
  .updateMask(aoi_mask)
;

var valley_bottoms_not_impervious = valley_bottoms.multiply(imp.eq(0));

// print(valley_bottoms_not_impervious);

var output_min_max = geo.iCart.iMinMax(valley_bottoms_not_impervious, 10, study_town);

print("Min & max value of image", output_min_max);


Map.addLayer(valley_bottoms_not_impervious, {min:0, max:1}, "3.2 Valley bottoms without Impervious", false);

// -------------------------------------------------------------
//  3.3 Distinguish valley bottoms without impervious that do not intersect habitat blocks as a new habitat class.
//  Your goal here is to make a single layer where the value 1 represents habitat blocks and 2 represents corridors. 
// -------------------------------------------------------------

//  Note to TAs: there are a lot of different ways to solve this step, so do not feel like you need to force
//  students to use my solution. There are alternatives. 

// One way

var habitat_classes = blocks_or_rare
  .eq(0)
  .multiply(valley_bottoms_not_impervious)
  .multiply(2)
  .add(blocks_or_rare)
  ;

// Another way

// var habitat_classes = blocks_or_rare
//   .eq(0)
//   .multiply(valley_bottoms_not_impervious)
//   .remap(
//     [0,1],
//     [0,2])
//   .add(blocks_or_rare)
//   ;
  

print("habitat classes", habitat_classes);

Map.addLayer(habitat_classes.selfMask(), {min:0, max:2, palette: ["black", "#9370DB", "#DBD570"]}, "3.3b Habitat blocks and connectors", false);

// -------------------------------------------------------------
//  3.4 Export image to asset and display as map layer.  
// -------------------------------------------------------------

//  I started getting some "tile" errors here that tells me EE is getting sweating the task. 
//  So that is why I exported the result from 3.3 as an asset and continued working with it. 

// geo.iExport.toCloudAsset(
//   habitat_classes, 
//   "p04_habitat_blocks_and_connectors",
//   aoi, 
//   "mode"
// );

var image_asset = ee.Image("projects/ee-patterns/assets/vt-conservation/p04_habitat_blocks_and_connectors");


var viz_habitat = {
  min:1,
  max:2, 
  palette: ["#9370DB", "#DBD570"]
};

Map.addLayer(image_asset.selfMask(), viz_habitat, "3.3 Habitat blocks and connectors", true);

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  4. A little cartography 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  4.1 Add a legend.  
// -------------------------------------------------------------

// Make legend from image with nominal data.

var legend_nominal = geo.iCart.legendNominal(
  "Act 171 Habitat Elements", 
  viz_habitat, 
  ["Blocks", "Connectors"], 
  "position-on-map"
  )
;

// Add legend to Map.  

Map.add(legend_nominal);

// -------------------------------------------------------------
//  4.2 Add outlines of study town.  
// -------------------------------------------------------------

var strokes = geo.fcCart.paintStrokes(study_town, "white", 4);

Map.addLayer(strokes, {}, "Study town outlines");

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
//  PRACTICE CHECKS
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

// Please calculate percent area based on your result from 3.4.
// When calculating area, please use 5 for scale and study_town (Middlebury) for extent.
// The last two checks in Canvas will ask you to report area for habitat blocks and habitat connectors separately. 

var habitat_classes_areas = geo.iZonal.areaClasses(habitat_classes, 5, study_town, "max");
var class_percent_of_region = geo.iZonal.classPercentRegion(habitat_classes_areas);

print(
  "Check 3.4: Area (percent of region) habitat",
  class_percent_of_region
  )
;





```