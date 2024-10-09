__PATTERNS__

# __*proximity operations*__

Proximity operations concern questions of distance, how near (or far) places are from each other.  

_more soon_  

---  

## __a short illustration__    

I find the proximity methods in earth engine to be a little confusing, so I made the app below to illustrate how some important concepts. The text below walks you through how to build the map layers in the app. 

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/on-distance"
  style="width:854px; height:480px"
></iframe>

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/on-distance){target=_blank}

---  

### __00 start a script__  

This workflow draws on methods in the geo module, so you will need to load that module after you write a script header. 

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:   Jeff Howarth   
    DATE:     10/7/2024  
    TITLE:    On distance with web mercator

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

```

---  

### __01 proximity with vector__    

The first part of the script demonstrates proximity methods with vector. We start by constructing and drawing a test point in the center of Youngman's Field. 

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  1. Proximity with vector. 
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
//  1.1 Gather Test point
// -------------------------------------------------------------

var test_point = ee.FeatureCollection("projects/ee-patterns/assets/t05/youngman_center");

// -------------------------------------------------------------
//  1.2 Set Map center, zoom, and base layer. 
// -------------------------------------------------------------

Map.centerObject(test_point, 19);
Map.setOptions('HYBRID');

// -------------------------------------------------------------
//  1.3 Add test point layer. 
// -------------------------------------------------------------

Map.addLayer(test_point, {color: 'yellow'}, "1.3 Test Point", false);

```

We then use the vector tool ```geo.fcProximity.bufferByDistance()``` to buffer the point by 50 yards and add the result as a layer to the Map.  

```js
// -------------------------------------------------------------
//  1.4 Buffer the point by 50 yards (45.72 meters)
// -------------------------------------------------------------

var d = 45.72;

var test_buffer = geo.fcProximity.bufferByDistance(test_point, d);

// -------------------------------------------------------------
//  1.5 Add layer to Map.
// -------------------------------------------------------------

Map.addLayer(test_buffer, {color: "red"}, "1.3 Test vector buffer 50 yards", false);

```

Notice how the buffer lines up pretty well with the goal lines that are 50 yards from center field.   

---  

### __02 proximity with raster__  

Now we can try to reproduce this simple buffer using raster methods. The first step involves converting the test point feature collection to a boolean image and displaying the result as a Map layer.  

```js
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
//  2. Proximity with raster.
// -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-

// -------------------------------------------------------------
// 2.1 Convert test point to a Boolean image.
// -------------------------------------------------------------

var image_boolean_test = geo.fcConvert.toBooleanImage(test_point);

// -------------------------------------------------------------
// 2.2 Display test point image. 
// -------------------------------------------------------------

Map.addLayer(image_boolean_test, {min:0, max:1}, "2.2 Test point Image", false);
```

The next step is to use ```geo.iFocal.iDistance()``` to calculate the euclidean distance from all non-zero pixels in the test point image. At this point, we will use the coordinate reference system for web mercator. 

```js

// -------------------------------------------------------------
//  2.3. Calculate euclidean distance from test point.
// -------------------------------------------------------------

var crs = "EPSG: 3857";  // web mercator

var distance_image_test = geo.iFocal.iDistance(image_boolean_test, d, crs, "euclidean", "pixels");

// -------------------------------------------------------------
//  2.4. Define viz parameters
// -------------------------------------------------------------

var viz_euc = {min:0, max: d, palette: geo.iPalettes.iDistance.inferno.reverse()};

// -------------------------------------------------------------
//  2.5. Display euclidean distance as layer on Map.
// -------------------------------------------------------------

Map.addLayer(distance_image_test,  viz_euc, "2.5 Euc distance", false);

```

In a last step, we can create a raster version of a __buffer__ by applying a threshold of 50 yards to the distance image that results in a Boolean image. And then add this result to the Map as a layer.   

```js
// -------------------------------------------------------------
// 2.6 Threshold euclidean distance image at 50 yards. 
// -------------------------------------------------------------

var distance_image_test_threshold = distance_image_test.lte(d).selfMask();

// -------------------------------------------------------------
// 2.7 Add threshold image as layer to Map. 
// -------------------------------------------------------------

Map.addLayer(distance_image_test_threshold, {min:0, max:1}, '2.7 Threshold Distance at 50 Yards', false);

```

---  

### __reflection__  

You just made a 50 yard buffer around a point in the center of Youngman Field with vector and raster methods. How do they differ? What do you think causes their difference?  

---  

### __03 crs matters__  

Go back to section 2.3 and replace the crs variable with this:

```js
var crs = "EPSG: 32145";    // VT State Plane (NAD83)
```

Then run your script and compare the results to the vector method. Why do you think crs matters for raster proximity methods? Do they also matter for vector methods?  

---   

## __vector methods__  

---  

### __:earth_americas: buffer by distance__ 

This method takes a feature collection and distance (in meters) as arguments. The result is a buffer around each feature in the collection; the buffer defines the zone that is within the specified distance to each feature in the collection.  

```js
var fc_buffer = geo.fcProximity.bufferByDistance(fc, distance);

```

---  

## __raster methods__  

---  

### __:earth_americas: make distance raster__ 

This method makes an image that represents the distance of each pixel from all non-zero (and unmasked) pixels in the input image. 

```js

var crs = "EPSG: 32145";    // VT State Plane (NAD83)

var image_distance = geo.iFocal.iDistance(image_input, radius, crs, "model", "units");
```

The method takes four arguments:  

| ARGUMENT      | DESCRIPTION         |
|:--:            | :--                 |  
| image_input   | Input image to calculate distance to all non-zero but unmasked cells. Often a boolean or an object image. |  
| radius        | The radius of the distance kernel. This defines the size of the moving window used to calculate distance. It can not be greater than 255. |  
| crs           | A coordinate reference system as a string that provides the EPSG definition. |  
| "model"       | Defines the model of distance employed. Must be a string and one of the following: "euclidean", "manhattan", "chebyshev".                         |  
| "units"       | Defines the system of measurement for the distance kernel, either "pixels" or "meters". Must be a string. |


![raster-distance-models](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/proximity/distance-models.png)


---

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivs 4.0 International License</a>.
