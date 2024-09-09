# __export to drive__  

The following three code blocks together provide a template for exporting objects from Earth Engine scripts to your personal google drive so that you can use these data in whitebox or other gis platforms.  

---  

```js
var x = {
  data: image_dme,
  label: "DFM_Chipman",
  folder: "_eex",
};

print(x.data);


var projection = x.data.projection();

projection.evaluate(function(proj_obj) {
  Export.image.toDrive({
    image: x.data,
    description: x.label,
    folder: "_eex",
    fileFormat: "GeoTiff",
    maxPixels: 1e13,
    crs: proj_obj.crs,
    crsTransform: proj_obj.transform,
    region: x.data.geometry() });
});


```


## Load data    

To get started, we need some data to export. In the code block below, we first instantiate a polygon geometry object that represents a test study region that I use in many of the whitebox tutorials. We then load the high-resolution land cover dataset that represent an image with nominal data. 

```js
// ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
//  Exporting template  

//  Last modified: 3/22/2024 
// ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

// -------------------------------------------------------------
//  LOAD DATA MODULE. 
// -------------------------------------------------------------

var data = require('users/jhowarth/public:modules/data.js');       
print('DATA', data);

// -------------------------------------------------------------
//  DEFINE KEY TERMS
// -------------------------------------------------------------

var crs = "EPSG:32145";
var xfolder = 'x0352';

var scale = 1.5;
var transform = [scale, 0, 0, 0, scale, 0];

// -------------------------------------------------------------
//  DEFINE GEOMETRY OBJECT
//
//  I used the drawing tools to make this polygon and then pasted
//  the coordinates here so that we could all have the same object.
// -------------------------------------------------------------

var geometry = 
    ee.Geometry.Polygon(
        [[[-73.22494136517258, 44.03630018203328],
          [-73.22494136517258, 44.001612587825356],
          [-73.13190089886399, 44.001612587825356],
          [-73.13190089886399, 44.03630018203328]]], null, false);

Map.centerObject(geometry, 13);
Map.setOptions('hybrid');

Map.addLayer(geometry, {color: 'red'}, "Geometry object", false);

// -------------------------------------------------------------
//  DEFINE A NOMINAL IMAGE 
// -------------------------------------------------------------

//  Reproject nominal image into desired scale and coordinate system.

var image = ee.Image(data.lc.base.i)
;

//  View as a layer. 

Map.addLayer(image, data.lc.base.viz, "Base land cover", false);

```

---  

## Export geometry object to drive  

The code block below exports the geometry object defined above to a folder in your google drive called 'x0352'. If this folder does not exist, earth engine will make it at the root level.  

```js
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
//  EXPORT GEOMETRY OBJECT 
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

//  Reproject geometry object into desired coordinate system.

var geo_projected = geometry.transform(crs, 1);

//  Cast geometry as a feature collection. 

var geo_fc = ee.FeatureCollection(geo_projected);

//  Define name for export object and task

var geo_name = 'geo_object_example';

//  Export to drive

Export.table.toDrive(
  {
    collection: geo_fc, 
    description: geo_name, 
    folder: xfolder, 
    fileNamePrefix: geo_name, 
    fileFormat: 'SHP', 
    // selectors, maxVertices, priority
  }
);
```

---  

## Export nominal raster 

The code block below exports the nominal image from above to your google drive. Please note that the export dictionary requires a region that will clip the exported image. In this example, we use the test region polygon for this purpose.  

```js
// -------------------------------------------------------------
//  EXPORT A NOMINAL IMAGE 
// -------------------------------------------------------------

//  Reproject nominal image into desired scale and coordinate system.

var image_projected = ee.Image(data.lc.base.i)
  .reproject(crs, [scale, 0, 0, 0, scale , 0])
  .byte()
;

//  Define name for task and image. 

var task = 'base_land_cover';       // 03/29/24

//  Export image to drive.

Export.image.toDrive(
  {
    image: image_projected, 
    description: task, 
    folder: xfolder, 
    fileNamePrefix: task, 
    // dimensions, 
    region: geo_projected, 
    // scale, 
    crs: crs, 
    crsTransform: transform, 
    maxPixels: 1e12, 
    // shardSize, 
    // fileDimensions, 
    // skipEmptyTiles, 
    fileFormat: 'GeoTIFF', 
    // formatOptions, 
    // priority
    
  }
);

```
