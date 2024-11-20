__STARTERS__  

# __*MODIS*__  

Earth Engine provides a somewhat staggering number of different [MODIS products][ee-modis]{target=_blank} as cloud assets. The sheer number of products available can make it a little confusing to navigate. This page aims to help by introducing some key concepts for working with MODIS.   

## __key terms__ 

### __sensor and satellites__    

The __Moderate Resolution Imaging Spectrometer__, or [MODIS][nasa-modis]{target=_blank}, is a sensor onboard two satellites:  

* __Terra__: originally called as EOS AM-1  
* __Aqua__: originally called EOS PM-1 

### __orbits__  

These two satellites image Earth's entire surface once every 1-2 days. The video below shows the orbit of the Aqua satellite.   

<iframe width="720" height="405" src="https://www.youtube.com/embed/d4QLDlAumOc?si=Sy2r8U1OilAYG2f6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### __bands__  

Compared to Landsat and Sentinel, MODIS bucks convention for band names. It also differs from other sensors by having a second NIR band (between NIR and SWIR1).     

| BAND NUMBER   | BAND NAME     | BAND WIDTH (nm)       |
|:--:           | :--:          | :--:                  |        
| B1            | Red           | 620 - 670             |  
| B2            | NIR           | 841 - 876             |  
| B3            | Blue          | 459 - 479             |  
| B4            | Green         | 545 - 565             |  
| B5            | NIR2          | 1230 - 1250           |  
| B6            | SWIR1         | 1628 - 1652           |  
| B&            | SWIR2         | 2105 - 2155           |  

---  

## __SR snapshots__  

These scripts will help you get started making snapshots with two different MODIS surface reflectance (SR) products. The eight day composites help speed up processing times.  

---  

### __daily images__  

```js
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_MODIS_daily.js
//  Author:       Jeff Howarth
//  Last edited:  11/17/2024
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// // Map.centerObject(geometry, 6);

Map.setOptions('hybrid');

// ----------------------------------------------------------------------
//  Combine Terra and Aqua daily collections. 
// ----------------------------------------------------------------------

// Print metadata for spectral bands. 

print("MODIS spectra", geo.icMODIS.spectral_bands);

// Gather collections of terra and aqua daily images. 

var terra_1day = ee.ImageCollection("MODIS/061/MOD09GA");
var aqua_1day = ee.ImageCollection("MODIS/061/MYD09GA");

print(
  "MODIS",
  terra_1day.first(),
  terra_1day.size(),
  aqua_1day.first(),
  aqua_1day.size()
  )
;

// Combine daily collections. 

var combineMODIS = terra_1day
  .merge(aqua_1day)
;

print(
  "TERRA, AQUA COMBINED",
  combineMODIS.size()
  )
;

// ----------------------------------------------------------------------
//  Filter 
// ----------------------------------------------------------------------

// Define year and month of interest. 

var yoi = 2021;
var moi = 8;

// Filter collections by time and cloudy pixels.

var output = combineMODIS
  .filter(ee.Filter.calendarRange(yoi, yoi, "year"))
  .filter(ee.Filter.calendarRange(moi, moi, "month"))
  .map(geo.icMODIS.maskClouds_1day)                   // Mask cloudy pixels
  .map(geo.icMODIS.renameSpectralBands)               // Rename bands because they have weird names.
  .median()
  .multiply(0.0001)                                   // Apply scalar after flattening collection.
;

print("OUTPUTS", output);


// ----------------------------------------------------------------------
// Display
// ----------------------------------------------------------------------

var viz = {
  
  bands: ['R', 'G', 'B'],
  min: [0.01, 0.02, 0.0],
  max: [0.25, 0.25, 0.175],
  gamma: 1.2,
  
};

Map.addLayer(output, viz, 'MODIS imagery');


// ------------------------------------------------------------------------
//  Chart histogram for a selected Image band.  
// ------------------------------------------------------------------------

// Select a band in viz dictionary to chart. 

var select_band = output.select(viz.bands[0]);

// Get AOI from map extent.

var aoi = geo.uiMap.getAOIfromMapExtent();

// Get scale from map extent.

var scale =  Map.getScale();

// Make and print histogram.

var histogram = geo.iCart.iHistogram(
    select_band, 
    scale,
    aoi                 
);

print("Histogram of selected band", histogram);

```

---  

### __8 day composites__  

```js
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_MODIS_8day_composites.js
//  Author:       Jeff Howarth
//  Last edited:  10/18/2023
//
//  Starter for MODIS collection. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

Map.setOptions('hybrid');


// ----------------------------------------------------------------------
//  Combine Terra and Aqua daily collections. 
// ----------------------------------------------------------------------

// Print metadata for spectral bands. 

print("MODIS spectra", geo.icMODIS.spectral_bands);

// Gather collections of terra and aqua 8 day averages. 

var terra_8day = ee.ImageCollection("MODIS/061/MOD09A1");
var aqua_8day = ee.ImageCollection("MODIS/061/MYD09A1");

print(
  "MODIS",
  terra_8day.first(),
  terra_8day.size(),
  aqua_8day.first(),
  aqua_8day.size()
  )
;

// Combine daily collections. 

var combineMODIS = terra_8day
  .merge(aqua_8day)
;

print(
  "TERRA, AQUA COMBINED",
  combineMODIS.size()
  )
;

// ----------------------------------------------------------------------
//  Filter collection
// ----------------------------------------------------------------------

// Define year and month of interest. 

var yoi = 2021;
var moi = 8;

// Filter collections by time and cloudy pixels.

var output = combineMODIS
  .filter(ee.Filter.calendarRange(yoi, yoi, "year"))
  .filter(ee.Filter.calendarRange(moi, moi, "month"))
  .map(geo.icMODIS.maskClouds_8day)                   // Mask cloudy pixels
  .map(geo.icMODIS.renameSpectralBands)               // Rename bands because they have weird names.
  .median()
  .multiply(0.0001)                                   // Apply scalar after flattening collection.
;

print("OUTPUTS", output);


// ----------------------------------------------------------------------
// Display
// ----------------------------------------------------------------------

var viz = {

  bands: ['R', 'G', 'B'],
  min: [0.01, 0.02, 0.0],
  max: [0.25, 0.25, 0.175],
  gamma: 1.2,

};

Map.addLayer(output, viz, 'MODIS imagery');


// ------------------------------------------------------------------------
//  Chart histogram for a selected Image band.  
// ------------------------------------------------------------------------

// Select a band in viz dictionary to chart. 

var select_band = output.select(viz.bands[0]);

// Get AOI from map extent.

var aoi = geo.uiMap.getAOIfromMapExtent();

// Get scale from map extent.

var scale =  Map.getScale();

// Make and print histogram.

var histogram = geo.iCart.iHistogram(
    select_band, 
    scale,
    aoi                 
);

print("Histogram of selected band", histogram);

```

---  

## __SR time series__    

These scripts will help you get started with time series analysis. We use the eight-day composites to help speed up processing times.   

### __basic time series__ 

The script below compiles a collection (rather than a flat image) and then charts all spectral bands over the duration of the collection. 

```js

//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_MODIS_8day_time_series.js
//  Author:       Jeff Howarth
//  Last edited:  10/18/2023
//
//  Starter for MODIS time series. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

Map.setOptions('hybrid');

// ----------------------------------------------------------------------
//  Combine Terra and Aqua daily collections. 
// ----------------------------------------------------------------------

// Print metadata for spectral bands. 

print("MODIS spectra", geo.icMODIS.spectral_bands);

// Gather collections of terra and aqua 8 day averages. 

var terra_8day = ee.ImageCollection("MODIS/061/MOD09A1");
var aqua_8day = ee.ImageCollection("MODIS/061/MYD09A1");

print(
  "MODIS",
  terra_8day.first(),
  terra_8day.size(),
  aqua_8day.first(),
  aqua_8day.size()
  )
;

// Combine daily collections. 

var combineMODIS = terra_8day
  .merge(aqua_8day)
;

print(
  "TERRA, AQUA COMBINED",
  combineMODIS.size()
  )
;

// ----------------------------------------------------------------------
//  Filter collection
// ----------------------------------------------------------------------

// Define year and month of interest. 

var yoi = 2023;

// Filter collections by time and cloudy pixels.

var output = combineMODIS
  .filter(ee.Filter.calendarRange(yoi, yoi, "year"))
  .map(geo.icMODIS.maskClouds_8day)                   // Mask cloudy pixels
  .map(geo.icMODIS.renameSpectralBands)               // Rename bands because they have weird names.
;

print("OUTPUT COLLECTION", output);


// ----------------------------------------------------------------------
//  Display image from collection as Map layer.  
// ----------------------------------------------------------------------

var viz = {

  bands: ['R', 'G', 'B'],
  min: [0.01, 0.02, 0.0],
  max: [0.25, 0.25, 0.175],
  gamma: 1.2,

};

// Define display image 

var display_image = output    // time series collection
  .median()                   // flatten image
  .multiply(0.0001)           // apply scalar for reflectance values  
;          

Map.addLayer(display_image, viz, 'MODIS imagery');


// // ------------------------------------------------------------------------
// //  Chart histogram for a selected Image band.  
// // ------------------------------------------------------------------------

// // Select a band in viz dictionary to chart. 

// var select_band = display_image.select(viz.bands[0]);

// // Get AOI from map extent.

// var aoi = geo.uiMap.getAOIfromMapExtent();

// // Get scale from map extent.

// var scale =  Map.getScale();

// // Make and print histogram.

// var histogram = geo.iCart.iHistogram(
//     select_band, 
//     scale,
//     aoi                 
// );

// print("Histogram of selected band", histogram);

// ------------------------------------------------------------------------
//  Define regions of interest.  
// ------------------------------------------------------------------------

// Gather regions from a feature collection.  

var regions = ee.FeatureCollection("FAO/GAUL/2015/level2");

// Define a point of interest with geometry tools.

var geometry = ee.Geometry.Point([-119.72687261495858, 34.42223412451513]);

// Select region of interest with poi.

var regions_select = regions.filterBounds(geometry);

// ------------------------------------------------------------------------
//  Display regions of interest as map layers.
// ------------------------------------------------------------------------

var strokes = geo.fcCart.paintStrokes(regions, "white", 0.5);

Map.addLayer(strokes, {}, "Region outlines");

var strokes_select = geo.fcCart.paintStrokes(regions_select, "yellow", 2);

Map.addLayer(strokes_select, {}, "Selected region outlines");

// -------------------------------------------------------------
//  Initialize panel for time series chart. 
// -------------------------------------------------------------

var panel_chart = geo.icIntervals.initializePanelForChart('bottom-left');

Map.add(panel_chart);

// Define parameters for time series chart.

var parameters = {
  collection: output,
  reducer: ee.Reducer.mean(),
  image_scale: 500,
  // interval_unit: "month",          // Comment out to chart by default "system:time_start"
  panel: panel_chart,
  roi: regions_select
};

// Chart time series with parameters. 

geo.icIntervals.chartTimeSeries(parameters);

```

---  

### __time series of spectral index__  

The script below will compute a spectral index (NDVI) for each image in the time series and then chart the index over duration of the collection.    

```js
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_MODIS_8day_time_series_with_ndvi.js
//  Author:       Jeff Howarth
//  Last edited:  10/18/2023
//
//  Starter for MODIS time series. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

Map.setOptions('hybrid');

// ----------------------------------------------------------------------
//  Combine Terra and Aqua daily collections. 
// ----------------------------------------------------------------------

// Print metadata for spectral bands. 

print("MODIS spectra", geo.icMODIS.spectral_bands);

// Gather collections of terra and aqua 8 day averages. 

var terra_8day = ee.ImageCollection("MODIS/061/MOD09A1");
var aqua_8day = ee.ImageCollection("MODIS/061/MYD09A1");

print(
  "MODIS",
  terra_8day.first(),
  terra_8day.size(),
  aqua_8day.first(),
  aqua_8day.size()
  )
;

// Combine daily collections. 

var combineMODIS = terra_8day
  .merge(aqua_8day)
;

print(
  "TERRA, AQUA COMBINED",
  combineMODIS.size()
  )
;

// ----------------------------------------------------------------------
//  Filter collection
// ----------------------------------------------------------------------


// Filter collections by cloudy pixels.

var output = combineMODIS
  // .filter(ee.Filter.calendarRange(yoi, yoi, "year"))
  .map(geo.icMODIS.maskClouds_8day)                   // Mask cloudy pixels
//   .map(geo.icMODIS.maskWater_8day)                    // Mask water pixels. 
  .map(geo.icMODIS.renameSpectralBands)               // Rename bands because they have weird names.
;

print("OUTPUT COLLECTION", output);


// ----------------------------------------------------------------------
//  Display image from collection as Map layer.  
// ----------------------------------------------------------------------

var viz = {

  bands: ['R', 'G', 'B'],
  min: [0.01, 0.02, 0.0],
  max: [0.25, 0.25, 0.175],
  gamma: 1.2,

};

// Define display image 

var display_image = output    // time series collection
  .median()                   // flatten image
  .multiply(0.0001)           // apply scalar for reflectance values  
;          

Map.addLayer(display_image, viz, 'MODIS imagery', false);


// // ------------------------------------------------------------------------
// //  Chart histogram for a selected Image band.  
// // ------------------------------------------------------------------------

// // Select a band in viz dictionary to chart. 

// var select_band = display_image.select(viz.bands[0]);

// // Get AOI from map extent.

// var aoi = geo.uiMap.getAOIfromMapExtent();

// // Get scale from map extent.

// var scale =  Map.getScale();

// // Make and print histogram.

// var histogram = geo.iCart.iHistogram(
//     select_band, 
//     scale,
//     aoi                 
// );

// print("Histogram of selected band", histogram);


// ----------------------------------------------------------------------
//  Calculate spectral index for each image in the collection.  
// ----------------------------------------------------------------------

// Write computation as a function.  

var computeND = function(image) {
    
    var si = image.normalizedDifference(['N', 'R']).rename('NDVI');
    
    return image.addBands(si);
    
  };

// Map function over the collection.  

var output_with_si = output.map(computeND);

print("MAP NDVI", output.first(), output_with_si.first());

// Display spectral index image from collection as layer on Map.

var display_image_si = output_with_si     // time series collection
  .median()                               // flatten image
  .select("NDVI")
; 

Map.addLayer(display_image_si, {min:-0.8, max:0.8, palette: geo.iPalettes.iDrought}, "Image with spectral index");

// ------------------------------------------------------------------------
//  Define regions of interest.  
// ------------------------------------------------------------------------

// Gather regions from a feature collection.  

var regions = ee.FeatureCollection("FAO/GAUL/2015/level2");

// Define a point of interest with geometry tools.

var geometry = ee.Geometry.Point([-119.72687261495858, 34.42223412451513]);

// Select region of interest with poi.

var regions_select = regions.filterBounds(geometry);

// ------------------------------------------------------------------------
//  Display regions of interest as map layers.
// ------------------------------------------------------------------------

var strokes = geo.fcCart.paintStrokes(regions, "white", 0.5);

Map.addLayer(strokes, {}, "Region outlines");

var strokes_select = geo.fcCart.paintStrokes(regions_select, "yellow", 2);

Map.addLayer(strokes_select, {}, "Selected region outlines");

// -------------------------------------------------------------
//  Initialize panel for time series chart. 
// -------------------------------------------------------------

var panel_chart = geo.icIntervals.initializePanelForChart('bottom-left');

Map.add(panel_chart);

// Define parameters for time series chart.

var parameters = {
  collection: output_with_si.select('NDVI'),
  reducer: ee.Reducer.mean(),
  image_scale: 500,
  // interval_unit: "month",          // Comment out to chart by default "system:time_start"
  panel: panel_chart,
  roi: regions_select
};

// Chart time series with parameters. 

geo.icIntervals.chartTimeSeries(parameters);


```


[ee-modis]: https://developers.google.com/earth-engine/datasets/catalog/modis 
[nasa-modis]: https://modis.gsfc.nasa.gov/about/ 

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>