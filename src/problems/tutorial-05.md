__TUTORIAL 5__

# __*scale in web mercator*__

##  

This tutorial aims to introduce concepts and methods for working with __proximity__ and __zonal statistics__ in Earth Engine.  

Our practical goal is to make a map of Tissot's Indicatrix and then compute the area and number of pixels contained by each circle through a zonal overlay method. By the end, your script should reproduce the layers shown in the app below. 

In addition, you should be able to interpret your results by using the Inspector tool to compare how pixel scale changes with respect to the area and pixel count of Tissot's indicatrix.   

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/tutorial-05"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/tutorial-05){target=_blank}



## __workflow__  

---  

### __00 start script__

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   
    DATE:     10/7/2024
    TITLE:    Scale in web mercator

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 


```

---  

### __01 set up map__  


```js
// -------------------------------------------------------------
//  1. Set up map
// -------------------------------------------------------------

// 1.1. Center map on prime meridian and equator at zoom level 2.  

Map.setCenter(0,0,2);

// 1.2. Set base map to hybrid.



// 1.3. Compute Map scale at Map zoom 

var scale = Map.getScale();

print("Map scale", scale);

```

---

### __02 visualize pixel area__  

```js
// -------------------------------------------------------------
//  2. Visualize change in pixel area across Map.
// -------------------------------------------------------------

// 2.1. Make a layer that stores area of each pixel in square kilometers.

var pixel_area = ee.Image.pixelArea().divide(1e6);

// 2.2. Draw a rectangle from equator to pole.

var test_extent = ee.Geometry.Polygon(
        [[[-139.54012012783244, 16.927790310290327],
          [-139.54012012783244, -85.91090722591649],
          [52.41300487216755, -85.91090722591649],
          [52.41300487216755, 16.927790310290327]]]);

// 2.3. Calculate min and max of area image with test_extent rectangle at scale of zoom level. 


 
 // 2.4. Define viz parameters with palette: geo.iPalettes.iDistance.inferno
 


// 2.5. Display pixel_area as layer on Map.



// 2.6. Make legend of pixel area layer. 



// 2.7. Add legend to Map.  

```

---  

### __03 create Tissot's indicatrix__  

```js
// -------------------------------------------------------------
//  3. Create Tissot's Indicatrix. 
// -------------------------------------------------------------

// 3.1. Gather tissot grid.

var grid = geo.projections.tissot_grid;

print("3.1. grid", grid);

// 3.2. Display grid as Map layer.



// 3.3 Buffer each point in grid by 600,000 meters. 



// 3.4 Add buffered points (Tissot's Indicatrix) as Map Layer. 

Map.addLayer(indicatrix, {color: 'gold'}, "3.4. Tissot's Indicatrix");


```

---  

### __04 visualize area of indicatrix__    

```js
// -------------------------------------------------------------
//  4. Visualize area of Tissot's indicatrix
// -------------------------------------------------------------

// 4.1 Zonal statistic for sum of pixel area at scale 5000.




// 4.2 Convert 4.1 output to image



// 4.3 Define viz parameters.



// 4.4 Display as Map layer.



// 4.5. Make legend of tissot area layer. 



// 4.6. Add legend to Map.  



```

---  

### __05 visualize count of indicatrix__    

```js
// -------------------------------------------------------------
//  5. Visualize count of indicatrix
// -------------------------------------------------------------

// 5.1 Zonal statistic for count of pixel area at scale 5000.



// 5.2 Convert to image. 



// 5.3 Define viz parameters. 




// 5.4 Display as Map layer.  




// 5.5. Make legend of tissot area layer. 


// 5.6. Add legend to Map.  



```

---  

### __06 inspect your results__    

Click on the __Inspector tab__ on the right panel of the Code Editor. Moving from the equator towards the poles, clock on the Tissot Indicatrix and note the __Scale (approx. m/px)__ that GEE reports. This number should report the distance on the ground represented by the length of one pixel side.  

_HINT: You may need to click on the __Point__ header in order to see the scale reports._  

Try to answer these questions:  

1. How does scale change with latitude?  
2. How does this jive with the area and count statistics that you calculated for each circle?  
3. How do you explain these results?  

---  


<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>