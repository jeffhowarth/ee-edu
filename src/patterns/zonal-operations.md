__PATTERNS__

# _**zonal operations**_  

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
  class_percent_of_region
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

---  

## __:earth_americas: zonal statistics__    

This method calculates a statistic of image values within a zone of analysis defined by one or more features in a feature collection. The output of the method is a feature collection with a new column that contains the statistic.  

![zonal-stat]

```js
var fc_zonal_stat = geo.iZonal.zonalStats(dough, cutter, "statistic", scale);

```

The method takes four arguments that are defined in the table below.  

| ARGUMENTS   | DESCRIPTION                                   |
| :--:        | :--                                           |
| dough       | The image with pixel values to be analyzed.   |  
| cutter      | The feature collection with one or more features that define the zones of analysis. |
| "statistic" | The statistic to calculate within each zone of analysis. Must be a string from these options: "sum", "max", "min", "mean", "count", "variety" ("count" reports the number of pixels, while "variety" reports the number of unique pixel values). |  
| scale       | The scale of analysis. Should be set to raster scale (pixel size) of dough. If you encounter time out errors that prevent you from displaying output layer, you can try to resolve by changing the scale of analysis, though this will introduce rounding errors. |  


[zonal-stat]: http://geography.middlebury.edu/howarth/ee_edu/eePatterns/zonal-overlay/zonal-statistic.png

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>