__PRACTICE 05__  

# __*land use in watershed riparian zones*__  

## __goal__  

This problem aims to help you practice working with __proximity__ and __zonal statistics__ in Earth Engine. 

Your practical goal is to make a map that reports the percent of riparian zones that are either developed or used for agriculture in each watershed that overlaps a study town.  

We will define key terms as follows: 

* __study town__: Middlebury, Vermont  
* __aoi__: all level 12 watersheds that overlap the study town  
* __surface waters__: all streams, rivers, ponds, and lakes    
* __riparian__: all land within 50 feet of surface waters  
* __developed__: all impervious surfaces (buildings, roads, pavement, and railroads)  
* __agriculture__: all agricultural land uses (hayfields, crop fields, and pasture)  

Your solution should produce a map with the layers shown in the app below.  

---  

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/practice-05"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/practice-05){target=_blank}


---  

## __data sources__  

In this problem, we will use the [National Hydrology Dataset (NHD)][usgs-nhd]{target=_blank} that is available as a cloud asset through the [Awesome Earth Engine Community Catalog][aeecc]{target=_blank}.

In addition, we will use town and land cover data that we have worked with in previous problems.  

## __workflow__    

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR: 
    DATE:   
    TITLE:  Land use in watershed riparian zones

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// -------------------------------------------------------------
//  datasets
// -------------------------------------------------------------

// Towns

var vt_towns = ee.FeatureCollection("projects/conservation-atlas/assets/cadastre/Boundary_TWNBNDS_poly"); 

// Land cover

var vt_ag = ee.Image("projects/vt-conservation/assets/landcover/STATEWIDE_2022_50cm_LANDCOVER_Agriculture");
var vt_imp = ee.Image("projects/vt-conservation/assets/landcover/STATEWIDE_2022_50cm_LANDCOVER_Impervious");

// National Hydrology Dataset

var nhd_wbdhu12 = ee.FeatureCollection("projects/sat-io/open-datasets/NHD/NHD_VT/WBDHU12");
var nhd_flowline = ee.FeatureCollection("projects/sat-io/open-datasets/NHD/NHD_VT/NHDFlowline");
var nhd_area = ee.FeatureCollection("projects/sat-io/open-datasets/NHD/NHD_VT/NHDArea");
var nhd_waterbody = ee.FeatureCollection("projects/sat-io/open-datasets/NHD/NHD_VT/NHDWaterbody");

// Viz helpers

var viz_bool = {min:0, max:1};
var red_palette = geo.iPalettes.yellowOrangeRed[6];

// General parameters.

var scale = 30;  // To help model run a little faster, please set scale at 30 in Part 9. 

// -------------------------------------------------------------
//  1. Define study town and set up map.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  2. Select Level 12 watersheds that overlap study town. 
// -------------------------------------------------------------  



// -------------------------------------------------------------
//  3. Select NHD features that overlap selected watersheds. 
// -------------------------------------------------------------  


// -------------------------------------------------------------
//  4. Clip selected area features to selected watersheds. 
// ------------------------------------------------------------- 



// -------------------------------------------------------------
//  5. Define riparian as buffer of selected hydrology features by 50 feet.  
// ------------------------------------------------------------- 



// -------------------------------------------------------------
//  6. Make union of buffered hydrology features.    
// ------------------------------------------------------------- 



// -------------------------------------------------------------
//  7. Define developed land as union of impervious and ag lands.    
// ------------------------------------------------------------- 



// -------------------------------------------------------------
//  8. Define developed land in riparian.     
// ------------------------------------------------------------- 



// -------------------------------------------------------------
//  9. Compute percent of developed land in riparian. (Set scale = 30 to help model run faster.)       
// ------------------------------------------------------------- 



// -------------------------------------------------------------
//  10. Classify percent into equal 10% intervals.  
// ------------------------------------------------------------- 



// -------------------------------------------------------------
//  11. Add watershed reference lines and legend.     
// ------------------------------------------------------------- 





```

## __checks__

Please add this code to the end of your script and edit the names to match those of your layers. You will need this answers to complete the checkup on Canvas that is due Monday by 5pm.

```js
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
//  PRACTICE CHECKS
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

print("CHECKS:");

//  Import check module for practice problem 4.

var check = require("users/jhowarth/eePatterns:checks/p05.js");

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

//  PLEASE DO THE FOLLOWING: 

// 1. Uncomment all of the check statements below.
// 2. Replace 'result_part_#' with the name of the data object that you used to map as a layer in each section.
// 3. Run the script.
// 4. Use the results printed to Console in the Check Up that is due Monday 5pm. 

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>


check.checkFeature("Check Part 1:", result_part_1);
check.checkFeature("Check Part 2:", result_part_2);
check.checkArea("Check Part 6:", result_part_6);
check.checkArea("Check Part 7:", result_part_7);
check.checkArea("Check Part 8:", result_part_8);
check.checkPoint("Check Part 9:", result_part_9);
check.checkPoint("Check Part 10:", result_part_10);


```


---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>



[towns]: https://geodata.vermont.gov/datasets/VCGI::vt-data-town-boundaries-1/about  

[aeecc]: https://gee-community-catalog.org/
[aeecc-nhd]: https://gee-community-catalog.org/projects/nhd/
[usgs-nhd]: https://www.usgs.gov/national-hydrography/national-hydrography-dataset

[vcgi-landcover]: https://geodata.vermont.gov/pages/land-cover