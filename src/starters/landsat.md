__STARTERS__  

# __*Landsat*__  

Earth Engine provides a number of different [Landsat products][ee-landsat]{target=_blank} as cloud assets.

The starter scripts on this page will help you quickly find and process collection 2, tier 1, level 2, surface reflectance data for a place and time of interest.  

Since that was a mouthful, let's define some key terms first.

## __key terms__  

### __collections__   

There have been two major reprocessing efforts by USGS to improve data quality. [Collection 2](https://www.usgs.gov/landsat-missions/landsat-collection-2){target=_blank} is the most recent and has the best geolocation accuracy which improves time series analyses.    

### __tiers__  

Within a collection, Tier 1 data have the highest radiometric and positional quality. USGS recommends using Tier 1 data for all time-series analysis.  

### __levels__  

The level of data processing applied to products.    

- [__Level-1__](https://www.usgs.gov/landsat-missions/landsat-level-1-processing-details){target=_blank} includes processing to improve locational accuracy of data.  

- [__Level-2__](https://www.usgs.gov/landsat-missions/landsat-collection-2-level-2-science-products){target=_blank} products are built from Level 1, but also provide atmospheric correction to create surface reflectance and surface temperature products. Level-2 science products also include spectral indices derived from surface reflectance products.  

- [__Level-3__](https://www.usgs.gov/landsat-missions/landsat-science-products){target=_blank} products are built from Level-2 products and include Analysis Ready Data (ARD), including Fractional Snow Covered Area and Burned Area, and Scene-based Inputs, including Provisional Actual Evapotranspiration.   

### __orbit__  

This video visualizes the path of Landsat 8 around the globe. Please note that some details about satellite orbits differ between Landsat missions.

<iframe width="720" height="405" src="https://www.youtube.com/embed/P-lbujsVa2M?si=1fIN_s06noaM8YkH" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---  

### __spectral bands__  

The chart below compares the bands of each mission with respect to spectral and spatial resolution.

![landsat-comparison](https://d9-wret.s3.us-west-2.amazonaws.com/assets/palladium/production/s3fs-public/media/images/LandsatSpectralBands_20240319.png)  

### __mother of landsat__  

![MSS image of Half Dome](https://landsat.gsfc.nasa.gov/wp-content/uploads/2014/05/HalfDome_May1972_MSSem321_crop_4web.png)

Please read [Virginia Tower Norwood's biography](https://www.technologyreview.com/2021/06/29/1025732/the-woman-who-brought-us-the-world/){target=_blank}.   

## __prereqs__  

To thoughtfully use the starter scripts below, you should be able to answer these questions:  

* what is _surface reflectance_ and how does this differ from other Landsat products available through Earth Engine catalog? 
* what is the mission _duration_ (start and end of image collection)?  
* what is the _recurrence time_ of each scene (how may days between images)?  
* how does the satellite orbit affect the time difference between _neighboring scenes_?   
* what _time of day_ is the scene captured as an image?  
* what _portion of the EM spectrum_ does each band measure?  
* what is the _spatial resolution_ of each band?  

[ee-landsat]: https://developers.google.com/earth-engine/datasets/catalog/landsat



---

## __:earth_americas: Landsat 5__  

```js

//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_L5.js
//  Author:       Jeff Howarth
//  Last edited:  11/4/2024
//
//  Starter for Landsat 5 collection. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// ------------------------------------------------------------------------
//  Define your point or area of interest with geometry tools. 
// ------------------------------------------------------------------------

var geometry = 
    ee.Geometry.Point([37.34715255366928, -3.0521293499524087]);

Map.centerObject(geometry, 8);

// ------------------------------------------------------------------------
//  Filter and flatten image collection.   
// ------------------------------------------------------------------------

var output = ee.ImageCollection('LANDSAT/LT05/C02/T1_L2')
  .filterBounds(geometry)
  // .filter(ee.Filter.calendarRange(1995, 1995, 'year'))
  .filter(ee.Filter.calendarRange(1, 3, 'month'))
  // .filter(ee.Filter.calendarRange(1, 1, 'day_of_year'))
  .filter(ee.Filter.lt('CLOUD_COVER', 20))
  .map(geo.icLandsat.scale_L5)
  .map(geo.icLandsat.cloudMask_L5)
  .median()
;

print("Landsat 5 image", output);

// ------------------------------------------------------------------------
//  Display layer on Map.
// ------------------------------------------------------------------------

var viz = {
  bands: ['SR_B3', 'SR_B2', 'SR_B1'],
  min: [0.0, 0.0, 0.0],
  max: [0.3, 0.3, 0.3],
};

Map.addLayer(output, viz, 'Landsat 5 image');

// ------------------------------------------------------------------------
//  Chart histogram for a selected Image band.  
// ------------------------------------------------------------------------

// Select a band in viz dictinary to chart. 

var select_band = output.select(viz.bands[0]);

// Get AOI from map extent.

var aoi = geo.uiMap.getAOIfromMapExtent();

// Make and print histogram.

var histogram = geo.iCart.iHistogram(select_band, 30, aoi);

print("Histogram of selected band", histogram);

```

---

## __:earth_americas: Landsat 7__

```js

//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_L7.js
//  Author:       Jeff Howarth
//  Last edited:  11/4/2024
//
//  Starter for Landsat 7 collection. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// ------------------------------------------------------------------------
//  Define your point or area of interest with geometry tools. 
// ------------------------------------------------------------------------

var geometry = 
    ee.Geometry.Point([37.34715255366928, -3.0521293499524087]);

Map.centerObject(geometry, 8);

// ------------------------------------------------------------------------
//  Filter and flatten image collection.   
// ------------------------------------------------------------------------

var output = ee.ImageCollection('LANDSAT/LE07/C02/T1_L2')
  .filterBounds(geometry)
  // .filter(ee.Filter.calendarRange(2000, 2000, 'year'))     // January 1999–April 2022
  .filter(ee.Filter.calendarRange(1, 3, 'month'))
  // .filter(ee.Filter.calendarRange(1, 1, 'day_of_year'))
  // .filter(ee.Filter.lt('CLOUD_COVER', 20))
  .map(geo.icLandsat.scale_L7)
  .map(geo.icLandsat.cloudMask_L7)
  .median()
;

print("Landsat 7 image", output);

// ------------------------------------------------------------------------
//  Display as layer on Map.
// ------------------------------------------------------------------------

var viz = {
  bands: ['SR_B3', 'SR_B2', 'SR_B1'],
  min: [0.0, 0.0, 0.0],
  max: [0.3, 0.3, 0.3]
};

Map.addLayer(output, viz, 'Landsat 7 image');


// ------------------------------------------------------------------------
//  Chart histogram for a selected Image band.  
// ------------------------------------------------------------------------

// Select a band in viz dictinary to chart. 

var select_band = output.select(viz.bands[0]);

// Get AOI from map extent.

var aoi = geo.uiMap.getAOIfromMapExtent();

// Make and print histogram.

var histogram = geo.iCart.iHistogram(select_band, 30, aoi);

print("Histogram of selected band", histogram);


```

---  

## __:earth_americas: Landsat 8__  

```js

//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_L8.js
//  Author:       Jeff Howarth
//  Last edited:  11/4/2024
//
//  Starter for Landsat 8 collection. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// ------------------------------------------------------------------------
//  Define your point or area of interest with geometry tools. 
// ------------------------------------------------------------------------

var geometry = 
    ee.Geometry.Point([37.34715255366928, -3.0521293499524087]);

Map.centerObject(geometry, 8);

// ----------------------------------------------------------------------
//  Filter and flatten image collection. 
// ----------------------------------------------------------------------

var output = ee.ImageCollection("LANDSAT/LC08/C02/T1_L2")
  .filterBounds(geometry)
  // .filter(ee.Filter.calendarRange(2015, 2015, 'year'))
  .filter(ee.Filter.calendarRange(1, 3, 'month')) 
  // .filter(ee.Filter.calendarRange(1, 1, 'day_of_year')) 
  // .filter(ee.Filter.lt('CLOUD_COVER',20))
  .map(geo.icLandsat.scale_L8)
  .map(geo.icLandsat.cloudMask_L8)
  .median()
;

print("Landsat 8 image", output);

// ----------------------------------------------------------------------
//  Display as layer on Map.
// ----------------------------------------------------------------------

var viz = {
  bands: ['SR_B4', 'SR_B3', 'SR_B2'],
  min: [0.0, 0.0, 0.0],
  max: [0.25, 0.25, 0.25],
};

Map.addLayer(output, viz, 'Landsat 8 image');


// ------------------------------------------------------------------------
//  Chart histogram for a selected Image band.  
// ------------------------------------------------------------------------

// Select a band in viz dictinary to chart. 

var select_band = output.select(viz.bands[0]);

// Get AOI from map extent.

var aoi = geo.uiMap.getAOIfromMapExtent();

// Make and print histogram.

var histogram = geo.iCart.iHistogram(select_band, 30, aoi);

print("Histogram of selected band", histogram);


```

---  

## __:earth_americas: Landsat 9__   

```js
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_L9.js
//  Author:       Jeff Howarth
//  Last edited:  11/4/2024
//
//  Starter for Landsat 9 collection. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// ------------------------------------------------------------------------
//  Define your point or area of interest with geometry tools. 
// ------------------------------------------------------------------------

var geometry = 
    ee.Geometry.Point([37.34715255366928, -3.0521293499524087]);

Map.centerObject(geometry, 8);


// ----------------------------------------------------------------------
//  Filter and flatten image collection.
// ----------------------------------------------------------------------

var output = ee.ImageCollection("LANDSAT/LC09/C02/T1_L2")
  .filterBounds(geometry)
  // .filter(ee.Filter.calendarRange(2022, 2022, 'year'))
  .filter(ee.Filter.calendarRange(1, 3, 'month')) 
  // .filter(ee.Filter.calendarRange(1, 1, 'day_of_year')) 
  // .filter(ee.Filter.lt('CLOUD_COVER',20))
  .map(geo.icLandsat.scale_L9)
  .map(geo.icLandsat.cloudMask_L9)
  .median()
;

print("Landsat 9 image", output);

// ----------------------------------------------------------------------
//  Display image as layer on Map.
// ----------------------------------------------------------------------

var viz = {
  bands: ['SR_B4', 'SR_B3', 'SR_B2'],
  min: [0.0, 0.0, 0.0],
  max: [0.25, 0.25, 0.25],
};

Map.addLayer(output, viz, 'Landsat 9 image');


// ------------------------------------------------------------------------
//  Chart histogram for a selected Image band.  
// ------------------------------------------------------------------------

// Select a band in viz dictinary to chart. 

var select_band = output.select(viz.bands[0]);

// Get AOI from map extent.

var aoi = geo.uiMap.getAOIfromMapExtent();

// Make and print histogram.

var histogram = geo.iCart.iHistogram(select_band, 30, aoi);

print("Histogram of selected band", histogram);


```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>