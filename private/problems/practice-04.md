__PRACTICE 4__ 

# _**Forest blocks and habitat connectors**_  

## __goal__  

This problem continues working on our map of forest habitat blocks for the town of Middlebury, Vt.  

Your practical goal is to:

1. include rare natural communities in your forest habitat block layer; 
2. incorporate lidar-informed flood inundation data to map habitat connectors;
3. distinguish habitat blocks and connectors as separate classes in a single raster layer.


Your workflow should reproduce all the layers shown in the app below.  

---    

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/practice-04"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/practice-04){target=_blank}

---  

## __data sources__

This problem uses several datasets from the [tutorial problem](../problems/tutorial-04.md). In addition, we will use two new datasets described in the table below.  

<center>

| ASSET NAME                                | DESCRIPTION                                   | FORMAT    | RESOLUTION| 
| :---                                      | :--                                           | :--       | :--       | 
| LakeChamplainBasin  | [Lake Champlain Basin Lidar-Informed Flood Inundation Layer][vcgi-flood]{target=_blank}                | Image     | 70 cm     | 
| SignificantNaturalCommunities | [VT Significant Natural Communities][vcgi-rare]{target=_blank} | FC | |

</center>

[vcgi-flood]: https://vcgi.vermont.gov/data-release/lake-champlain-basin-lidar-informed-flood-inundation-layer-now-available

[vcgi-rare]: https://geodata.vermont.gov/datasets/VTANR::vt-significant-natural-communities-public-version/about

---  

## __starter script__  

### __00 Getting started__  

Begin with a header and importing the module. The address variables will give you access to all the data that you need for this problem.  

```js
/*     
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:     
    TITLE:  

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

```

---  

### __01 Define study region__  

This section is pretty similar to the tutorial, so you should be able to recycle that code here.  

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  1. Define study region.
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  1.1 Define study town (Middlebury)
// -------------------------------------------------------------


// -------------------------------------------------------------
//  1.2 Convert study town into boolean (to use as mask later)
// -------------------------------------------------------------


// -------------------------------------------------------------
//  1.3 Define aoi as study town and towns that overlap (share boundary) with study town.
// -------------------------------------------------------------


// -------------------------------------------------------------
//  1.4 Convert aoi into a boolean (to use as mask later).
// -------------------------------------------------------------


// -------------------------------------------------------------
//  1.5 Center map on study town and set basemap to hybrid. 
// -------------------------------------------------------------



```

---  

### __02 Include rarity in blocks__  

Often, rare elements on the landscape are small in size. So by selecting habitat blocks that are greater than 100 acres, we may show bias and under-represent rare elements of the landscape in our conservation plan, essentially making poverty traps for rare but significant natural communities. 

To try to right this wrong, this chunk of the problem gathers data on Significant Natural Communities collected through Vermont's Natural Heritage program and includes these locations in our habitat blocks layer, even if they are relatively small.  

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  2. Make blocks inclusive of rare communities.  
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  2.1 Gather habitat blocks cloud asset that overlap aoi. 
// -------------------------------------------------------------



// -------------------------------------------------------------
//  2.2 Convert 2.1 to a boolean image.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  2.3 Gather rare natural communities that overlap aoi.
// -------------------------------------------------------------


// -------------------------------------------------------------
//  2.4 Make boolean image of rare natural communities that overlap aoi.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  2.5 Make a boolean image of locations that are either blocks or rare natural communities.
// -------------------------------------------------------------




```

---

### __03 Classify habitat blocks versus habitat connectors__   

If you look at the habitat block layers we have mapped thus far, you will notice that many blocks have both _low connectivity_ and _low circuitry_. In this step, we aim to improve both conditions by modeling __habitat connectors__.  

Your goal in this set of tasks is to use the Lidar-Informed Flood Inundation layer to represent valley bottoms. Your final layer should bring in valley bottom locations so that any valley bottom that does not overlap a habitat block is classed with the value 2. This will make a layer with three classes as shown in the table below.  

| VALUE     | CLASS NAME                                |
| :--:      | :--                                       |
| 0         | Neither a block or valley bottom.         |  
| 1         | Habitat blocks.                           |  
| 2         | Habitat connectors (valley bottoms that are not habitat blocks or not impervious surfaces).   |  

When you have made this layer, it is a good time to export the image as a cloud asset to use in the final steps of the problem.  


```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  3. Classify habitat blocks versus habitat connectors.  
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  3.1 Gather valley bottom, make it boolean (anything not 0 is true), and mask for aoi.
// -------------------------------------------------------------


// -------------------------------------------------------------
//  3.2 Erase all impervious land from valley bottoms.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  3.3 Distinguish valley bottoms without impervious that do not intersect habitat blocks as a new habitat class.
// Your goal here is to make a single layer where the value 1 represents habitat blocks and 2 represents connectors that are not also blocks nor are they an impervious surface. 
// -------------------------------------------------------------


// -------------------------------------------------------------
//  3.4 Export 3.3 image to asset and display asset as Map layer.   
// -------------------------------------------------------------




```

---  

### __04 Cartography__  

Finish your workflow with a little cartography to provide support to a map reader.  

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  4. A little cartography 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  4.1 Add a legend for the habitat block/connector layer.  
// -------------------------------------------------------------



// -------------------------------------------------------------
//  4.2 Add layer of outlines for study town.  
// -------------------------------------------------------------



```

---  


### __05 Checks__  

```js
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
//  PRACTICE CHECKS
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

print("CHECKS:");

//  Import check module for practice problem 4.

var check = require("users/jhowarth/eePatterns:checks/p04.js");

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

//  PLEASE DO THE FOLLOWING: 

// 1. Uncomment all of the check statements below.
// 2. Replace 'result_#p#' with the name of the data object that you used to map as a layer in each section.
// 3. Run the script.
// 4. Use the results printed to Console in the Check Up that is due Friday 5pm. 

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>

// check.checkCollection("Check 1.1", result_1p1);
// check.checkCollection("Check 1.3", result_1p3);
// check.checkCollection("Check 2.1", result_2p1);
// check.checkCollection("Check 2.3", result_2p3);

// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  Check 3.4. What percent of Middlebury are habitat blocks and connectors?  
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// Please calculate percent area based on your result from 3.4.
// When calculating area, please use 5 for scale and study_town (Middlebury) for extent.
// The last two checks in Canvas will ask you to report area for habitat blocks and habitat connectors separately. 



```


---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>