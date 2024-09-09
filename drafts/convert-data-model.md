## feature collection to binary image  

```js
// -------------------------------------------------------------
//  CONVERT FEATURE COLLECTION TO BINARY IMAGE. 

//  INPUT must be a feature collection.
//  OUTPUT will be a binary raster.  
// -------------------------------------------------------------
```

```js

var output = t.fc2Binary(input);

// -------------------------------------------------------------



```

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 

---  

## heat map (density image) from points  

I often use heat maps to visualize a gps breadcrumb track (set of points). It generally requires converting a .gpx file into a shapefile (in QGIS) and then uploading the shapefile as an EE asset.  

You will need to [load the task module][load-task-module] in order to call this tool. You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 
 

```js
// -------------------------------------------------------------
//  MAKE HEAT MAP. 

//  INPUT (feature collection) should be a set of point locations.
//  RADIUS (integer) defines the circle size used to compute density.  
// -------------------------------------------------------------
```

```js

var OUTPUT = t.makeHeatmap(INPUT,RADIUS);

// -------------------------------------------------------------


```


```js
// -------------------------------------------------------------
//  CONVERT FEATURE COLLECTION TO BINARY IMAGE. 

//  INPUT must be a feature collection.
//  OUTPUT will be a binary raster.  
// -------------------------------------------------------------
```

```js

var output = t.fc2Binary(input);

// -------------------------------------------------------------



## mosaic image collection to image    

```js
// -------------------------------------------------------------
//  MOSAIC IMAGE COLLECTION   

//  INPUT must be an image collection with a 'quilt patch' structure.
//  OUTPUT will be a image with a 'quilted' structure.  
// -------------------------------------------------------------
```

```js

var output = input.mosaic();

// -------------------------------------------------------------
```

---  

## image to rgb   

```js
// -------------------------------------------------------------------------
//  IMAGE TO RGB  

//  INPUT is an image.
//  min, max, gamma, etc are should call viz parameters
//  OUTPUT is three band (RGB) image. 
// -------------------------------------------------------------------------
```

```js

var output_rgb = input.visualize({
  min: viz.min, 
  max: viz.max, 
  gamma: viz.gamma,
  forceRgbOutput: true
});

```

---   

[load-task-module]: ../methods/load-modules.md#tasks-module  


[convert-fc-binary]: ../methods/convert-data-model.md#feature-collection-to-binary-image  

[mosaic-ic]: ../methods/convert-data-model.md#mosaic-image-collection-to-image   
[convert-image-rgb]: ../methods/convert-data-model.md#image-to-rgb  


[tasks-module]: https://code.earthengine.google.com/?accept_repo=users/jhowarth/public  