__PRACTICE 6__  

# __*Changes in the night*__  

## __goal__    

This problem aims to introduce you to making and interpreting __RGB composites__ with __additive color__.  

Your practiceal goal is to make a map that shows changes in the brightness of nighttime lights between 1993, 2003, and 2013. You will then interpret the additive colors in the image to describe different patterns of change.  

Your solution should make a map like that shown in the app below. 

---

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/practice-06"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/practice-06){target=_blank}

---

## __conceptual workflow__  

The diagram below sketches how we will use additive color to show changes in a nighttime lights dataset with Earth Engine.  

![Workflow](https://geography.middlebury.edu/howarth/ee_edu/rgb_lights_workflow.png)

---

## __starter workflow__  

### __00 start a new script__

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:     
    TITLE:    P6: Changes in the night

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module.

```

---  

### __01 set up map and AOI__  

```js

// -------------------------------------------------------------
//  Set up Map.
// -------------------------------------------------------------

Map.setCenter(126.8, 33.485, 5);
Map.setOptions('HYBRID');

// Get AOI from Map extent

```

---  

### __02 gather image collection__  

Please use this dataset and band: 

```js
var ic_address = 'NOAA/DMSP-OLS/NIGHTTIME_LIGHTS';
var band = "stable_lights";
```

---  

```js

// -------------------------------------------------------------
//  Gather image collection 
// -------------------------------------------------------------



// -------------------------------------------------------------
//  Select "stable lights" band from image.
// -------------------------------------------------------------

```

---  

### __03 filter by time__  

Please filter the collection for images captured in the years 2013.

```js

// -------------------------------------------------------------
//  Filter image collection by calendar unit.
// -------------------------------------------------------------

```

### __04 select image, rename band__

```js  

// -------------------------------------------------------------
//  Select first image of collection. 
// -------------------------------------------------------------


// -------------------------------------------------------------
//  Rename band "2013".
// -------------------------------------------------------------


```

### __05 display image as Map layer__  

```js  
// -------------------------------------------------------------
//  Display image as Map layer.
// -------------------------------------------------------------

```

---  

### __06 make mean image for 2003__  

Please recycle the steps above to make an image that represents the mean brightness of nighttime lights in the year 2003.  

_Why do you think we need to make a __composite image__ here, rather than just selecting the first image in the filtered collection?_  

```js

// -------------------------------------------------------------
//  Filter collection for year 2003
// -------------------------------------------------------------


// -------------------------------------------------------------
//  Composite collection by mean 
// -------------------------------------------------------------


// -------------------------------------------------------------
//  Rename image band.
// -------------------------------------------------------------



// -----------------------------------------------------------------------
//  Display image as layer on the map.
// -----------------------------------------------------------------------

```

---  

### __07 make mean image for 2013__  

Now try to chain the workflow, rather than saving each step as a separate variable.  

```js

// -----------------------------------------------------------------------
//  Chain the workflow to make the third band.
// -----------------------------------------------------------------------

var select_by_time_3 = select_by_band.filter(
  ee.Filter.calendarRange(1993, 1993, "year")
  )
  .mean()
  .rename(["1993"])
;

// print("Year 3", select_by_time_3);

Map.addLayer(select_by_time_3, viz, "1993", false);


// -----------------------------------------------------------------------
//  Construct a three band image from the three images.  
// -----------------------------------------------------------------------



// -----------------------------------------------------------------------
//  Add RGB composite as a layer to the map.
// -----------------------------------------------------------------------

```

---  

### __08 explore the RGB image__ 

Please copy and paste this code to the end of your script. You will need to replace "change_image" with the name of your three band image that represents nighttime lights in 2013, 2003, and 1993.  

Then run your script, explore the five patterns, and click locations to make charts of data values. 
What do the different visual patterns (Flame, Aurora, Holiday Lights, Red Giant, Political lines) show you about the temporal characteristics of spatial change?

When you have finished exploring the image, please complete the [practice-06 checkup] _link coming soon_ on Canvas <mark> by Friday 10/25 @ 5pm </mark>.  

```js

// -----------------------------------------------------------------------
//  Widgets
// -----------------------------------------------------------------------

//  Please uncomment the line below and run the script. 

geo.uiWidgets.p6(change_image);






```





---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>

