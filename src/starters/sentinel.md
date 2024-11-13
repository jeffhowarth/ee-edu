__STARTERS__  

# __*Sentinel*__

Earth Engine provides a number of different [Sentinel products][ee-sentinel]{target=_blank} as cloud assets.


[ee-sentinel]: https://developers.google.com/earth-engine/datasets/catalog/sentinel  


---  

## __Sentinel-2 MSI__    

The starter below will help you quickly find and process Level 1-C Harmonized Surface Reflectance data from the Sentinel 2 Multispectral Instrument (MSI). 

### __prereqs__  

To thoughtfully use the starter script below, you should be able to answer these questions:

* what is _surface reflectance_ and how does this differ from other Sentinel products available through Earth Engine catalog?
* why is _harmonized_ data helpful for time series analysis?  
* what is the _mission duration_ (start and end of image collection)?
* what is the _recurrence time_ of each scene (how may days between images)?
* how does the satellite _orbit_ affect the time difference between neighboring scenes?
* what _time of day_ is the scene captured as an image?
* what _portion of the EM spectrum_ does each band measure?
* what is the _spatial resolution_ of each band?

You can glean much of this info from these resources:  

* [Earth Engine data catalog](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED){target=_blank}   
* [ESA Copernicus page](https://www.esa.int/Applications/Observing_the_Earth/Copernicus/Sentinel-2){target=_blank} 
* [Sentinel 2 on SentiWiki](https://sentiwiki.copernicus.eu/web/sentinel-2){target=_blank}    


### __spectral bands__  

The chart below shows how the MSI sensor on Sentinel compares to the sensors onboard the Landsat missions.  

---  

![s2-v-landsat](https://landsat.gsfc.nasa.gov/wp-content/uploads/2015/06/Landsat.v.Sentinel-2.png)

---  

### __starter__  

```js
  
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Title:        starter_S2.js
//  Author:       Jeff Howarth
//  Last edited:  11/12/2023
//
//  Starter for harmonized Sentinel 2 collection. 
//  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// ----------------------------------------------------------------------
//  Define your point or area of interest with geometry tools. 
// ----------------------------------------------------------------------

var geometry = 
    ee.Geometry.Point([37.34715255366928, -3.0521293499524087]);

Map.centerObject(geometry, 9);

// ----------------------------------------------------------------------
//  Filter and flatten image collection.
// ----------------------------------------------------------------------

var output = ee.ImageCollection("COPERNICUS/S2_SR_HARMONIZED")
  .filterBounds(geometry)
  // .filter(ee.Filter.calendarRange(2020, 2020, 'year'))
  .filter(ee.Filter.calendarRange(1, 3, 'month')) 
  // .filter(ee.Filter.calendarRange(1, 30, 'day')) 
  .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE',20))
  .map(geo.icSentinel.cloudMask_S2)
  .map(geo.icSentinel.scale_S2)
  .median()
;

print(output);

// ----------------------------------------------------------------------
//  Display layer on Map. 
// ----------------------------------------------------------------------

// Print list of band names for S2.

print(
  "S2 BAND LIST",
  geo.icSentinel.bands_S2
);

// Define viz parameters. 

var viz = {
  bands: ['B4', 'B3', 'B2'],
  min: [0, 0, 0],
  max: [0.2, 0.15, 0.1]
};

// Add layer to Map. 

Map.addLayer(output, viz, 'From Sentinel 2 Collection');

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

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>