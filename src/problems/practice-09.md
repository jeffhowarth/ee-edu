__PRACTICE 09__  

# __*CZU Lightning Complex Burn Severity*__  

### __goal__  

This tutorial introduces a general workflow to map the burn severity of wildfire with Sentinel-2 MSI data.

We will use the [CZU Lightning Complex fires][czu-wiki]{target=_blank} on California’s Slow Coast as a case study. This practice problem complements a research article on the impacts to the old growth forests in Big Basin Redwoods State Park [(Potter 2023)][potter]{target=_blank}.  

[czu-wiki]: https://en.wikipedia.org/wiki/CZU_Lightning_Complex_fires

[potter]: https://journal.wildlife.ca.gov/2023/04/12/impacts-of-the-czu-lightning-complex-fire-of-august-2020-on-the-forests-of-big-basin-redwoods-state-park/

Your script should reproduce the map layers shown in the app below.  

---    

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/practice-09"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/practice-09){target=_blank}

---  

## __deliverables__    

Please take the checkup on Canvas <mark>by 5pm Friday 11/15</mark>. This checkup will ask you to report checkpoint answers and will be automatically graded, so you will be able to retake the checkup as many times as you would like until 5pm on Monday 11/18. Your final score for the checkup will be your maximum score.   

---

## __workflow__  

Please work through the steps outlined below.  

---  

### __00 Start a script__  

Start a new script with the code block below. I have define an area of interest for you by buffering a point near Bonny Doon, California. For the checks to work, please use this aoi. 

```js

/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:      
    TITLE:    09 Practice - CZU burn severity

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  

var geometry = 
 
    ee.Geometry.Point([-122.2241722048408, 37.148316599201095]);

var aoi = geometry.buffer(20 * 1000);

```

---  

### __01 Set up map__    

```js

// -------------------------------------------------------------
//  1. SET UP MAP.
// -------------------------------------------------------------

// Center map on AOI at zoom 10.



// Set base map to terrain.



```

---  

### __02 Make post-burn image__

```js
// -------------------------------------------------------------
//  2. MAKE POST-BURN IMAGE.
// -------------------------------------------------------------

```

Please adapt the [S2 starter script](../starters/sentinel.md){target=_blank} for this step. Your post-burn image should: 

1. Filter by aoi location.
2. Filter for September 2020.  
3. Filter for images with less that 20% cloud cover. 
4. Apply the scale and cloud mask methods for S2. 
5. Flatten to median image. 
6. Clip image by aoi (see pattern below). 
7. Display RGB as SWIR2, NIR, Red
8. Stretch enhance the RGB composite.  

To clip the image, please use this method : 

```js
 var clipped_image = image.clip(aoi)

```

---  

### __03 Make pre-burn image__  

```js
// -------------------------------------------------------------
//  3. MAKE PRE-BURN IMAGE.
// -------------------------------------------------------------

```

Your pre-burn image should replicate the criteria of Step 2 with one exception: you now want to filter for 2019. This image should show conditions in the same place and season for the year before the burn.  

---

### __04 Map post-burn NBR__  

```js
// -------------------------------------------------------------
//  4. MAP NORMALIZED BURN RATIO FOR POST-BURN SNAPSHOT
// -------------------------------------------------------------

```

For this step, you will need to: 

1. Load spectral indices module. 
2. Define parameters for Sentinel 2 Surface Reflectance. 
3. Compute NBR index. 
4. Isolate NBR band as a new single-band image. 
5. Display result as map layer using the viz parameters defined below.

```js
var nbr_viz = {bands: ["NBR"], min:-1, max:1, palette: ['purple', 'white', 'green']};
```

---  

### __05 Map pre-burn NBR__  

```js
// -------------------------------------------------------------
//  5. MAP NORMALIZED BURN RATIO FOR PRE-BURN SNAPSHOT
// -------------------------------------------------------------

```

You do not need to reload the spectral indices module, since you already did that above. You will need to do the three other steps described above (2-5) using the pre-burn image as the input. 

---  

### __06 Map burn severity__  


From the [readings this week][un-nbr]{target=_blank}, you saw that burn severity is the change in NBR caused by a fire scar.    

![burn-severity](https://un-spider.org/sites/default/files/dNBR_formula.jpg)  

[un-nbr]: https://un-spider.org/advisory-support/recommended-practices/recommended-practice-burn-severity/in-detail/normalized-burn-ratio

Please calculate and map the burn severity based on your two NBR images.

```js
// ------------------------------------------------------------------------
//  6. MAP BURN SEVERITY INDEX.
// ------------------------------------------------------------------------

```

---  

### __07 Reclassify burn severity__  

Please use the thresholds shown below to reclassify the burn severity image.  

![usu-thresholds](https://un-spider.org/sites/default/files/table+legend.PNG)  

```js
// ------------------------------------------------------------------------
//  7. RECLASSIFY BURN SEVERITY BASED ON USGS THRESHOLDS. 
// ------------------------------------------------------------------------

// Viz parameters for classified layer.

var burn_severity_viz = {
  min: 0,
  max: 6,
  palette: [
    '#778735', 
    '#a7c04f', 
    '#07e444', 
    '#f6fc0d', 
    '#f7b140', 
    '#f86819', 
    '#a601d4'
  ]
};

```

---  

### __08 Add legend__  

```js
// ------------------------------------------------------------------------
//  8. ADD BURN SEVERITY CLASS LEGEND TO MAP. 
// ------------------------------------------------------------------------

var burn_severity_labels = [
  'High post-fire regrowth',
  'Low post-fire regrowth',
  'Unburned',
  'Low Severity',
  'Moderate-low Severity',
  'Moderate-high Severity',
  'High Severity'
  ]
;

// Make legend from image with nominal data.

var legend_nominal = geo.iCart.legendNominal(
  "Burn Severity Classes", 
  burn_severity_viz, 
  burn_severity_labels, 
  "bottom-left"
  )
;

// Add legend to Map.  

Map.add(legend_nominal);
```

---  

### __09 Make ocean mask__ 

```js
// ------------------------------------------------------------------------
//  9. MAKE OCEAN MASK. 
// ------------------------------------------------------------------------

```

1. Gather an image from this cloud address: "NASA/NASADEM_HGT/001".
2. Select "elevation" band.
3. Make a boolean image where land is 1 and ocean is 0. 
4. Display mask as a Map layer.  


---  

### __10 Display burn severity with mask__  

```js
// ------------------------------------------------------------------------
//  10. DISPLAY BURN SEVERITY WITH OCEAN MASK. 
// ------------------------------------------------------------------------

// Display the burn severity class image with the ocean mask with opacity of 0.6.
// All other layers should not be displayed by default. 

```

---  

### __CHECKS__  

```js
// ----------------------------------------------------------------------
//  CHECKS
//
//  Please update the "result_step#" variable as needed for each step.  
// ----------------------------------------------------------------------

var check = require('users/jhowarth/eePatterns:checks/p09.js');

check.checkPoint("CHECK STEP 2:", result_step2.select("B8"));
check.checkPoint("CHECK STEP 3:", result_step3.select("B8"));
check.checkPoint("CHECK STEP 4:", result_step4);
check.checkPoint("CHECK STEP 5:", result_step5);
check.checkPoint("CHECK STEP 6:", result_step6);
check.checkPoint("CHECK STEP 7:", result_step7);
check.checkPoint("CHECK STEP 9:", result_step9);

```


---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>