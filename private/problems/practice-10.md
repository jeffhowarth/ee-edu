__PRACTICE 10__ 

# __*Memories of urban environments*__  

## __goal__  

This problem aims to introduce methods for mapping differences between conditions of sub-regions from whole regions. The general framework will help you explore __distributive environmental (in)justice__ in built environments and the central question: are the costs and benefits of the built environment distributed unevenly among groups or classes of society?  

This problem also introduces:

* a workflow to compute [land surface temperature (LST)][lst]{target=_blank} from Landsat collections using [a module by Sofia Ermida][sofia-lst]{target=_blank};  

* [a community module of color palettes][ee-palettes] to help display raster images, but generates a noticeable delay in the execution of any script that calls it; 

* methods for [changing aggregation levels](../patterns/vector-operations.md#multipart-vs-single-part-geometries){target=_blank} of regions with attributes of feature collections.   

By the end of the tutorial, you should have a script that reproduces the layers shown in the app below. You should also be able to rerun your analysis for any city in the USA with HOLC maps simply by changing one variable of your script.  

[lst]: https://earthobservatory.nasa.gov/global-maps/MOD_LSTD_M
[sofia-lst]: https://github.com/sofiaermida/Landsat_SMW_LST  
[ee-palettes]: https://github.com/gee-community/ee-palettes


---  

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/practice-10"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/practice-10){target=_blank}

## __context__  

This case study concerns the environmental legacies of redlining that are embedded in many (most) American cities. Your practical goal is to run the analysis by [Hoffman et al (2020)][hoffman]{target=_blank} with more recent LST data and create visuals inspired by the work of Nadja Popovich and Brian Palmer in [the second reading][nyt]{target=_blank} for this week.  

For more background on redlining and the history of the Home Owners' Loan Corporation (HOLC), please review the resources at [Mapping Inequality][urichmond]{target=_blank} from the University of Richmond.

[hoffman]: https://www.mdpi.com/2225-1154/8/1/12?type=check_update&version=1  
[nyt]: https://www.nytimes.com/interactive/2020/08/24/climate/racism-redlining-cities-global-warming.html
[urichmond]: https://dsl.richmond.edu/panorama/redlining  

---  

## __deliverables__  

Please complete the checkup on Canvas <mark>by 5pm on Friday 11/22</mark>. Because of the holiday next week, this will be a hard deadline. If your travel plans make this deadline impossible, please contact me for an extension before the deadline.  

---  

## __workflow__  

Please work through the steps of the workflow outlined below. Many steps draw on patterns introduced earlier in the course and I keep the scaffolding for these steps quite light. This aims to help you practice for the upcoming IP.  

---

### __00 Start a script__  

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:       11/20/2024
    TITLE:      practice-10.js
    
    Investigate environmental legacies of HOLC with LST.

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/


var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// Module for EE community palettes. 

var palettes = require('users/gena/packages:palettes');

print("Community palettes", palettes);
```

---  

### __01 Make and display Layer 1__  

```js

// ------------------------------------------------------------------------
//  1. Make and display Layer 1.
// ------------------------------------------------------------------------

 var holc_address = "projects/ee-primer/assets/holc_numeric_grades"

```

---  

### __02 Make and display Layer 2__  

```js

// ------------------------------------------------------------------------
//  2. Make and display Layer 2.
// ------------------------------------------------------------------------

```

---  

### __03 Define & display levels of aggregation__

```js

// ---------------------------------------------------------------------
//  3. Define levels of aggregation for HOLC data.
// ---------------------------------------------------------------------

// Define and display all holc zones of a city as a single, multipart feature. 


// Define each holc grade as a single, multipart features. 


// Print aggregation levels. 

```

---  

### __04 Create LST datasets from Landsat__  

Here is [a starter script](../starters/landsat.md#land-surface-temperature){target=_blank} to help get started with Sofia's module.  

```js

// ------------------------------------------------------------------------
//  4. Create LST datasets from Landsat.
// ------------------------------------------------------------------------

// Module to compute LST from Landsat.

var LandsatLST = require('users/sofiaermida/landsat_smw_lst:modules/Landsat_LST.js');

// Define arguments for LST module. 

var date_start = '2020-07-01';            // Filter by time start.
var date_end = '2024-09-01';              // Filter by time end.
var region = holc;                        // Filter by location.
var use_ndvi = true;                      // Use NDVI in computation (true or false).

// Compute LST from L9 collection.  


// Compute LST from L8 collection.  


// Print to inspect your work!



```

---  

### __05 Merge image collections__  

```js
// ------------------------------------------------------------------------
//  5. Merge image collections.
// ------------------------------------------------------------------------




```

---  

### __06 Filter merged collection__  

Filter the dataset for images collected in summer months (June - August) with cloud cover less that 10 percent. Also select only the 'LST' band from the images.

```js

// ------------------------------------------------------------------------
//  6. Filter merged collection.
// ------------------------------------------------------------------------

```

---  

### __07 Flatten, convert, rename, clip__  

Please do the following:  

1. calculate the average (mean) temperature of summer months collection (result of step 6) for each pixel; 
2. convert units of reduced image from Kelvin (units that result from LST module) to Fahrenheit;
3. rename the band "AVG_LST_F" in the output image;
4. clip to the holc_extent.

To convert from K to F: 

1. Subtract 273.15 from Kelvin temperature
2. Multiply by 1.8 
3. Add 32

```js
// ------------------------------------------------------------------------
//  7. Flatten, convert, rename, clip.
// ------------------------------------------------------------------------

```

---   

### __08 Display Layer 5__  

I include a viz dictionary below to help you use the community palettes module. For more help on this, please refer to [the module's docs](https://github.com/gee-community/ee-palettes?tab=readme-ov-file#ee-palettes){target=_blank}.   

```js
// ------------------------------------------------------------------------
//  8. Display as Layer 5.
// ------------------------------------------------------------------------

var output_viz = {
  bands: ["AVG_LST_F"],
  min: 85,
  max: 115,
  palette: palettes.colorbrewer.YlOrRd[9]
};


```

---  

### __09 Make and display Layer 6__  

```js

// ------------------------------------------------------------------------
//  9. Make and display Layer 6.
// ------------------------------------------------------------------------


```

---  

### __10 Compute difference__  

```js
// ------------------------------------------------------------------------
//  10. Compute difference: mean of parts - mean of whole.
// ------------------------------------------------------------------------

//  Use zonal statistics to calculate mean lst in each aggregation level. 


//  Convert each of above to image.



//  Compute difference: mean_parts - mean_whole 


```

---  

### __11 Display Layer 7__  

```js
// ------------------------------------------------------------------------
//  11. Display Layer 7.
// ------------------------------------------------------------------------
```

---  

### __12 Chart difference__  

```js
// ---------------------------------------------------------------------
//  12. Chart difference for each part. 
// ---------------------------------------------------------------------

// Define chart arguments. 

var chart_arguments = {
  data_image: difference,                           // Image used for Layer 7.
  class_image: image_nominal,                       // Image used for Layer 2.
  aoi: aoi_dissolve_whole,                          // Feature collection for Layer 3. 
  reducer: ee.Reducer.mean(),
  scale: 30,
  class_labels: geo.iPalettes.iHOLC.labels,
  title: 'Difference of grade from average LST',
  palette: geo.iPalettes.iHOLC.palette,
  ha_label: "degrees (F)"
  
  
};
 
var myChart = geo.uiChart.makeBarChartByClass(chart_arguments);

Map.add(myChart);


```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>