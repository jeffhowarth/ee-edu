## buffer features in collection by feet  

```js
// -------------------------------------------------------------
//  BUFFER FEATURES IN COLLECTION BY FEET.

//  INPUT is a feature collection. 
//  DISTANCE is a number in units feet.
//  OUTPUT is a single part feature collection of polygons. 
// -------------------------------------------------------------

```

```js  

var OUTPUT = INPUT.map(t.bufferFeet(DISTANCE));

// -------------------------------------------------------------

```

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 

---  

## euclidean distance image    

```js

// -----------------------------------------------------------------------------
//  EUCLIDEAN DISTANCE
//
//  euc_distance output represents the euclidean distance to the nearest non-zero pixel of input.
//  Input must be image with 0 as background value.
// -----------------------------------------------------------------------------

```
```js

var crs = "EPSG:32145";
var kr = 100;                   // Diameter of kernel, or zone to compute distance over. 

var euc_distance = input
  .distance(ee.Kernel.euclidean({radius: kr, units: 'meters'}))
  .reproject({crs: crs})       // This can slow down analysis, especially over large extents.                                   
  .rename('distance')
  ;

// Fun palette for distance images. 

var inferno = ["#000004", "#320A5A", "#781B6C", "#BB3654", "#EC6824", "#FBB41A", "#FCFFA4"].reverse();

// Add layer to map with fun palette. 

Map.addLayer(euc_distance,  {min:0, max: 100, palette: inferno}, "Euclidean distance image", false);

// -------------------------------------------------------------

```
### practical tip for crs  

The ``` .reproject({crs: crs}) ``` line allows you to force earth engine to calculate distance in a specified coordinate system. Without this, ee will compute distance with web mercator and the distance measurement will not be accurate. With this, it can slow down the computation because ee essentially has to make a new image and then make the calculation on it.  

One strategy then is to comment out the crs line when you are drafting your script to speed up visualizing and checking your work. If you do this, you will need to remember to uncomment the line when you are producing final results.  

---  

[buffer-feet]: ../methods/distance.md#buffer-features-in-collection-by-feet  
[distance-euc]: ../methods/distance.md#euclidean-distance-image  

[tasks-module]: https://code.earthengine.google.com/?accept_repo=users/jhowarth/public  