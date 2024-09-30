# __focal operations__  

Focal operations use a __moving window__ to carry out a computation based on values in the __neighborhood of a focal cell__. The window moves systematically across the raster, performing calculations for each pixel.    

![moving window](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/focalOperations/moving-window-animation.gif)

The result of each neighborhood calculation is stored in the output raster pixel that corresponds with the location of the focal pixel in the input raster. The shape and size of the moving window is defined by a __kernel__.  The example below uses a square, 3 x 3 pixel kernel to compute the average neighborhood value for a focal pixel.  
  
![neighborhood operation example](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/focalOperations/neighborhood-operation-example.png)  

## __scale of analysis__  

![scale of analysis](https://developers.google.com/static/earth-engine/images/Pyramids.png);

[_source_](https://developers.google.com/earth-engine/guides/scale){target=_blank}

---  

## __Object rasters from clusters__  

_more soon_ 

---  

### __:earth_americas: make objects from clusters__  

This method uses uses either a 'plus' or 'square' moving window to clump pixels that:

1. have the same value and
2. touch on adjacent sides ('plus' window) and/or corners ('square' window).  

It returns an image with the original band(s) and a new band called 'labels' that identifies contiguous regions with unique integer values. It is usually helpful to select the 'labels' band and visualize it with ```.randomVisualizer()```. 

The method works relatively quickly, but has two important quirks that result from Earth Engine's architecture:  

1. It cannot identify objects that are larger than 1024 pixels.  
2. The scale of analysis is determined by zoom level. Because of this, the results will change as you zoom in and out of the output layer.  

Here is the basic pattern.  

```js

var objects_from_clusters = geo.iFocal.makeObjectsFromClusters(image, 'kernel');  

Map.addLayer(objects_from_clusters.select("labels").randomVisualizer(), {}, "4.1. Objects from clusters";

```

| ARGUMENT      | DESCRIPTION   |
| :--           |               |
| __image__     | Input image with a band that contains a boolean or nominal (class) raster. If image contains more than one band, select the band that identifies the classes that you want to cluster.     |  
| __'kernel'__  | Either 'plus' or 'square'. A 'square' will clump pixels that touch at corners, while a 'plus' will only clump pixels that share a side. |  

---  

### __:earth_americas: object area from clusters__ 

This method calculates the area of distinct objects with a square (3x3 pixel) moving window. It is similar to the method described above, but differs in two ways:  

1. It can only use a 'square' window (so pixels will be clustered if they touch on corners).
2. It returns an image with only one band, named 'area', that stores the area (square meters) of the object in each pixel of the object.  

It suffers from the same two quirks described above (limited size and changes with zoom level).

Here is the basic pattern:

```js
var object_area_clusters = geo.iFocal.objectAreaFromClusters(image, "band");

```

The table below describes the arguments.  

| ARGUMENTS     | DESCRIPTION                                               |
| :--           | :--                                                       |
| __image__     | An input image.                                           |
| __"band"__    | The band name with boolean or class values to cluster.    |


