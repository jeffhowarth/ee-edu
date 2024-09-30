# __zonal operations__  

Zonal operations analyze pixel values in one layer based zones (regions) defined by another layer. In Earth Engine, the zones are generally defined by features in a feature collection.  

_more soon_  

--- 

## __zonal area__    

These methods use the zones defined by the geometry of a feature collection to compute the area of each class in a nominal or boolean layer.  

### __:earth_americas: area of classes__ 

This method returns a dictionary that reports the total area (in square meters) of each class (integer value) in the input raster.  

```js

var area_of_classes = geo.iZonal.areaClasses(image, scale, region, "band_name");

print(
    "Area (square meters)",
    area_of_classes
);

```

---  

The table below describes the arguments.  

| ARGUMENT      | DESCRIPTION               |  
| :--           | :--                       |  
| __image__     | The boolean or nominal (class) image to compute the area for each unique pixel value. |
| __scale__     | The pixel scale for analysis to troubleshoot TIME OUT errors. It can be helpful to first run at a coarse resolution and then increase resolution (make number smaller) as appropriate.    |              
| __region__        | Feature collection with one or more features that define the area of analysis or study region.         |  
| __"band_name"__   | The band name in the image with the integer values that identify the classes to compute the area of.  |  


### __:earth_americas: area of classes as percent of region__

This method returns a dictionary that reports the total area of each class (integer value) in the input raster as a percent of the region. It takes the output from ```.areaClasses()``` (above) as the input and returns a dictionary. 

```js

var class_percent_of_region = geo.iZonal.classPercentRegion(area_of_classes);

print(
  "Area (percent of region)",
  area_of_classes
  )
;

```

### __complete pattern__ 

Here is the complete pattern for calculating the area of raster classes and their percent area of a region.  


```js

var area_of_classes = geo.iZonal.areaClasses(image, scale, region, "band_name");

print(
    "Area (square meters)",
    area_of_classes
);

var class_percent_of_region = geo.iZonal.classPercentRegion(area_of_classes);

print(
  "Area (percent of region)",
  class_percent_of_region
  )
;

```

