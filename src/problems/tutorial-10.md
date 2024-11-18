__TUTORIAL 10__ 

# __*Drought mapping*__  

## __goal__

This tutorial aims to introduce you to mapping __temporal anomalies__, where __anomaly__ means the percent difference of a part to a whole and __temporal__ means the parts and whole represent a short duration record versus a long duration record.  

In this example, we will look at temporal anomalies in the NDVI index of MODIS 8 day composites. Since NDVI represents the "greenness" or health of vegetation, it is often used as a proxy for drought.  

We will develop the model using the case of drought in Santa Barbara, California. But the script should be written such that you can easily run the analysis for almost any region in the world.  

---    

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/tutorial-10"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/tutorial-10){target=_blank}

---  

## __workflow__  

Here are the main steps to the solution. Whenever possible, please print your results to console so that you can self-check your workflow.   


### __00 start a script__  

```js

/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:       
    DATE:         
    TITLE:        tutorial-10.js

    Mapping drought - temporal anomaly with MODIS 8 day composites.  

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

Map.setOptions('hybrid');

```

---

### __01 combine MODIS collections__  

```js

// ----------------------------------------------------------------------
//  Step 1. Combine Terra and Aqua daily collections. 
// ----------------------------------------------------------------------

// Print metadata for spectral bands. 



// Gather collections of terra and aqua 8 day averages. 


// Combine daily collections. 

```

---

### __02 filter ldr and sdr__ 

```js

// ----------------------------------------------------------------------
//  Step 2. Filter collection for long- and short- duration records.
// ----------------------------------------------------------------------

// Mask cloudy and water pixels and rename bands --> long duration record.

var output_ldr = combineMODIS
  .map(geo.icMODIS.maskClouds_8day)                   // Mask cloudy pixels
  .map(geo.icMODIS.maskWater_8day)                    // Mask water pixels.
  .map(geo.icMODIS.renameSpectralBands)               // Rename bands because they have weird names.
;

// Define year of interest as 2015.

var yoi = 2015;

// Filter long duration record by year of interest --> short term record.


```

---

### __03 map sdr median__ 

The script below assumes that you named your short duration record: output_sdr  

```js

// ----------------------------------------------------------------------
//  Step 3. Display median short duration image as Map layer.  
// ----------------------------------------------------------------------

var viz = {

  bands: ['R', 'G', 'B'],
  min: [0.01, 0.02, 0.0],
  max: [0.25, 0.25, 0.175],
  gamma: 1.2,

};

// Define display image from short duration collection. 

var display_image = output_sdr    // short duration collection
  .median()                       // flatten image (median)
  .multiply(0.0001)               // apply scalar for reflectance values (* 0.0001)  
;          

Map.addLayer(display_image, viz, 'STEP 3. MODIS imagery', false);

```

---

### __04 chart histogram__  

In the script above, I already did some stretch enhancement for you. This step is here if you would like to further adjust, or to have this step in workflow for future applications.  

```js

// // ------------------------------------------------------------------------
// //  Step 4. Chart histogram for a selected Image band.  
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

// print("Step 4. HISTOGRAM OF SELECTED BAND", histogram);

```

---

### __05 Map spectral index function__ 

```js

// ----------------------------------------------------------------------
//  Step 5. Calculate spectral index for each image in each collection.  
// ----------------------------------------------------------------------

// Write computation as a function.  



// Map function over long duration record.  



// Map function over short duration record. 


```

---

### __06 Display median NDVI of sdr__ 

```js

// ----------------------------------------------------------------------
//  Step 6. Display median NDVI of sdr as a Map layer.  
// ----------------------------------------------------------------------

// Flatten sdr with spatial index as median image and select 'NDVI' band.


// Define viz parameters.

var viz_ndvi =  {min:-0.8, max:0.8, palette: geo.iPalettes.iDrought};

// Display image as map layer. 

```

---

### __07 Define roi__ 

```js

// ------------------------------------------------------------------------
//  Step 7. Define regions of interest.  
// ------------------------------------------------------------------------

// Gather regions as feature collection from "FAO/GAUL/2015/level2".  



// Define a point of interest (update with geometry tools to change roi).

var geometry = ee.Geometry.Point([-119.72687261495858, 34.42223412451513]);

// Select region of interest with poi.


// Center Map on roi at zoom 9.

```

---

### __08 Make monthly summaries__ 

The script below assumes that you named short duration record with spectral index from Step 5: output_sdr_with_si.

---  

```js

// ----------------------------------------------------------------------
//  Step 8. Make monthly summaries of short and long duration records. 
// ----------------------------------------------------------------------

// Make monthly summary of short duration record. 

var monthly_summaries_sdr = geo.icIntervals.reduceToMonthlySeries(
    output_sdr_with_si,             // Collection
    "month",                        // Time unit to reduce.
    ee.Reducer.mean()               // Reducer
);

// Make monthly summary of long duration record (use same time unit and reducer as above).


print("STEP 8. MONTHLY SUMMARIES", monthly_summaries_sdr);


```

---

### __09 Make two band image__ 

The script below assumes that you named your results from Step 8: monthly_summaries_sdr and monthly_summaries_ldr.

---  

```js 

// ----------------------------------------------------------------------
//  Step 9. Make two band image of short- and long-duration records.  
// ----------------------------------------------------------------------

var monthly_summaries_stack = geo.icIntervals.stackShortLongRecords(
  "NDVI",                         // Band in each image to chart.
  monthly_summaries_sdr,          // Short duration monthly summaries.
  monthly_summaries_ldr           // Long duration monthly summaries.
  )
;

print("STEP 9. TWO BAND TIME SERIES", monthly_summaries_stack);

```

---

### __10 Chart monthly summaries__ 

The script below assumes that you named your results from Step 8: monthly_summaries_sdr and monthly_summaries_ldr.

---  

```js 

// -------------------------------------------------------------
//  Step 10. Chart monthly summaries.  
// -------------------------------------------------------------

var panel_chart = geo.icIntervals.initializePanelForChart('bottom-left');

Map.add(panel_chart);

// Define parameters for time series chart.

var parameters = {
  collection: monthly_summaries_stack,  // Name of two band image (Step 9).
  reducer: ee.Reducer.mean(),
  image_scale: 500,
  interval_unit: "month",          
  panel: panel_chart,
  roi: regions_select                   // Name of your selected region of interest (Step 7).
};

// Chart time series with parameters. 

geo.icIntervals.chartMonthlyStacks(parameters);

``` 

---

### __11 percent difference__ 

The script below assumes that you named your results from Step 9: monthly_summaries_stack.

---  

```js 

// --------------------------------------------------------------------------
//  STEP 11. Compute percent difference of short- and long-duration monthly summaries.   
// --------------------------------------------------------------------------  

var percent_difference = monthly_summaries_stack    // Two band image. 
    .map(geo.icIntervals.percentDifference(
        'NDVI_SDR',                                 // Band name for spectral index of SDR
        'NDVI_LDR'                                  // Band name for spectral index of LDR
        )
    )
;

print("STEP 11. PERCENT DIFFERENCE", percent_difference);

``` 

---

### __12 map percent difference layer__ 

---  

```js 

// --------------------------------------------------------------------------
//  STEP 12. Display percent difference for a target month as a Map layer.   
// --------------------------------------------------------------------------  

// Define month of interest to display.

var moi = 8;

var display_month = percent_difference.filter(ee.Filter.eq("month", moi));

// Define viz paramters. 

var viz_percent_difference = {
  min:-30, max:30, palette: geo.iPalettes.iDrought
};

// Add layer to map.

Map.addLayer(display_month, viz_percent_difference, "STEP 12. NDVI Anomaly");

``` 

---

### __13 Display regions__ 

---  

```js 

// ------------------------------------------------------------------------
//  STEP 13. Display regions of interest as map layers.
// ------------------------------------------------------------------------

var strokes = geo.fcCart.paintStrokes(regions, "white", 0.5);

Map.addLayer(strokes, {}, "STEP 13A. Region outlines");

var strokes_select = geo.fcCart.paintStrokes(regions_select, "yellow", 2);

Map.addLayer(strokes_select, {}, "STEP 13B. Selected region outlines");

```  










---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>