__TUTORIAL 4__

# _**Forest blocks**_  

## __goal__  

This tutorial aims to introduce concepts and techniques for working with __local overlay operations__ and __geographic objects__ in Earth Engine.  

Our practical goal is to identify all habitat blocks (contiguous regions of tree canopy and shrublands without impervious surfaces) that are greater than 100 acres in area. You will experiment with two different approaches to model these geographic objects and then export one layer as a cloud asset. In the end, your workflow should produce the set of layers shown in the app below. 

---    

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/tutorial-04"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/tutorial-04){target=_blank}

---  

## Starter scripts  

Please complete the workflow outlined below. For most tasks, you will produce a layer that you can compare to the layers in the app.

### __00 Start your workflow.__    

Start a new script and then add your header, import the geo module, and your cloud data addresses. 

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

// -------------------------------------------------------------  

// Feature collections  

var town_address = "projects/conservation-atlas/assets/cadastre/Boundary_TWNBNDS_poly"; 

// Images

var canopy_address = "projects/vt-conservation/assets/landcover/STATEWIDE_2022_50cm_LANDCOVER_TreeCanopy" ;
var shrub_address = "projects/vt-conservation/assets/landcover/STATEWIDE_2022_50cm_LANDCOVER_Shrublands";
var imp_address = "projects/vt-conservation/assets/landcover/STATEWIDE_2022_50cm_LANDCOVER_Impervious";
```  

---  

### __01 Define study region.__ 

Your goals here are to first define a __study town__. We will use Middlebury in this tutorial, but ideally you will write your script so that you will be able to easily switch your study to any other town in Vermont.

After you select the study town, please define your __study region__ as the study town plus all adjacent towns (or any town that overlaps a boundary of the study town). 

Next make __boolean images__ for both the study town and the study region. We will need these to mask layers later in the workflow.  

Finally, __center the Map__ on your study town. I used a zoom level of 12, but just pick one that works for your monitor. Then __change the base map__ to 'hybrid' so that you can compare the land cover layers in the next step to an image of ground conditions.    

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  1. Define study region.
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  1.1 Make a layer that shows the study town (Middlebury).
// -------------------------------------------------------------


// -------------------------------------------------------------
//  1.2 Convert study town into boolean (to use as mask later).
// -------------------------------------------------------------


// -------------------------------------------------------------
//  1.3 Define aoi as study town and surrounding towns. 
// -------------------------------------------------------------



// -------------------------------------------------------------
//  1.4 Convert aoi into a boolean (to use as mask later).
// -------------------------------------------------------------


// -------------------------------------------------------------
//  1.5 Center map on study town.
// -------------------------------------------------------------


```

---  

### __02 Gather land cover data.__  

The next set of tasks involve gathering the land cover data that we will use to model habitat blocks. These datasets are all available [through VCGI][vcgi-landcover]{target=_blank}. I have imported them as assets in the cloud so that we can all share them. The table below provides more details about each dataset used in this tutorial. 

---  

<center>

| ASSET NAME                                | DESCRIPTION                                   | FORMAT    | RESOLUTION| 
| :---                                      | :--                                           | :--       | :--       | 
| STATEWIDE_2022_50cm_LANDCOVER_TreeCanopy  | [Vermont Tree Canopy Land Cover 2022][vcgi-canopy]{target=_blank}                | Image     | 50 cm     | 
| STATEWIDE_2022_50cm_LANDCOVER_Shrublands  | [Vermont Shrublands Land Cover 2022][vcgi-shrublands]{target=_blank}             | Image     | 50 cm     |
| STATEWIDE_2022_50cm_LANDCOVER_Impervious  | [Vermont Impervious Surfaces Land Cover 2022][vcgi-impervious]{target=_blank}    | Image     | 50 cm     |

</center>

---  

After you __construct images__ from these address, you will likely need to __inspect the data properties__ of these objects in order to display them effectively. The table below lists the palettes that I used in the tutorial. 

---  


```js
var canopy_palette = ["#238b45", "#74c476"];
var shrubs_palette = ["#c0e673"];
var imp_palette = ["#4e4e4e", "#ffffff", "#a2a2a2", "#C47774"];
```

---  

The layers that you draw on your Map should:  

* use the colors from these palettes  
* only show data for our aoi  

---   

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  2. Gather land cover data. 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  2.1 Gather and display tree canopy masked by aoi.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  2.2 Gather and display shrub masked by aoi.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  2.3 Gather and display impervious masked by aoi.
// -------------------------------------------------------------



```

___  

### __03 Model habitat as a boolean image.__  

In this set of tasks, your goal is to use __local operations__ with the land cover data to make a layer that shows locations that are either tree canopy __or__ shrubland but __not__ impervious and then report both the total area and the area as a percent of the study town.  

Part of the puzzle here involves working with masks. Remember, that any location that is masked will not be included in the analysis. In this case, you want to __exclude__ all locations outside of your AOI, but __include__ all locations within your AOI.   

You might find it helpful to use the __inspector__ tool to click on locations and see their data values. For each layer, you want to make sure that values are masked outside the AOI and not masked inside the aoi.  

Also pay close attention that you should report the area and percent area of tree or shrub without impervious in the __study town__, not the entire AOI. 

---  

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  3. Model habitat as boolean image. 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  3.1 Make boolean image that shows locations that are either tree canopy or shrub.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  3.2 Make image of tree or shrub locations that are not impervious.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  3.3. Calculate area of tree or shrub without impervious in study town.
// -------------------------------------------------------------



// -------------------------------------------------------------
//  3.3. Calculate area of tree or shrub without impervious as percent of study town. 
// -------------------------------------------------------------



```

---  

### __04 Model habitat blocks as object image with focal methods.__  

In this set of tasks, your goal is to experiment with __focal methods__ to identify objects and calculate their areas.  

I would like you to pay attention to two things here:  

1. How would you describe the habitat that is omitted from the resulting layer? Why do you think this habitat was excluded from the results? 
2. How does your result change when you zoom in or out of the layer? What does this tell you about how focal methods work in Earth Engine?  

---  

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  4. Model habitat blocks as object image with focal methods. 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  4.1 Make object layer from clusters with 3.2 boolean image.
// -------------------------------------------------------------


// -------------------------------------------------------------
//  4.2 Make object area layer from clusters with 3.2 boolean image.
// -------------------------------------------------------------


```

---  

### __05 Model habitat blocks as object image with vector methods.__    

Your goal here is to experiment with __vector methods__ to identify objects. You will find that this approach is computationally expensive and Earth Engine may throw errors at you that complain about how much work you are asking it to do. To help resolve this, you will __filter the collection by attribute__ and select only the habitat blocks that are at least 100 acres in area. You should be able to display this result as a map layer.  

Finally, because the vector method is computationally expensive, your last task in this set is to __export the feature collection as an asset__. We will use this layer in the practice problem later this week.  

---

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  5. Model habitat blocks as object image with vector methods. 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  5.1 Make objects from 3.2 boolean image using convert to vector method.
// -------------------------------------------------------------


// DO NOT ADD AS LAYER - EE WILL LIKELY PROTEST! 
// Just inspect with print to console methods. 


// -------------------------------------------------------------
//  5.2 Filter for blocks greater than 100 acres and display as map layer. 
// -------------------------------------------------------------


// Again, this is a big computational ask for Earth Engine, so do not show layer by default.


// -------------------------------------------------------------
//  5.3 Export 5.2 feature collection to asset and display as layer.
// -------------------------------------------------------------





```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>

---  

[vcgi-landcover]: https://geodata.vermont.gov/pages/land-cover
[vcgi-shrublands]: https://maps.vcgi.vermont.gov/gisdata/metadata/LandLandcov_Shrubland2022TIF.htm 
[vcgi-canopy]: https://maps.vcgi.vermont.gov/gisdata/metadata/LandLandcov_TreeCanopy2022TIF.htm 
[vcgi-impervious]: https://maps.vcgi.vermont.gov/gisdata/metadata/LandLandcov_ImpervSrfcs2022TIF.htm  
