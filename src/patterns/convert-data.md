__PATTERNS__

# _**convert data**_  

These methods change the models used to represent geographic data and include:

* vector to raster
* raster to vector

## __vector to raster__  

These methods typically convert feature collections to images. 

_more soon_  

### :earth_americas: any FC to boolean raster  

This method converts a feature collection into a boolean raster. 

```js
var image_boolean = geo.fcConvert.toBooleanImage(fc);
```

---  

### :earth_americas: nominal FC to integer raster  

This method converts a feature collection with text attributes to a single-band image. It essentially creates a list of unique text attributes from a table column (defined by "column_name") and matches each unique text attribute to a unique integer. The result is an image with integer pixel values. The method also prints a dictionary to the Console that reports the integer code for each unique attribute.   

```js
var image_nominal = geo.fcConvert.toNominalImage(fc, "column_name");

```

---  

### :earth_americas: numeric FC to numeric raster

This method uses numeric attribute data in a feature collection to create a raster. 

```js
var image_numeric = geo.fcConvert.toNumericImage(fc, "column_name", "reducer");

```

The method takes three arguments that are defined in the table below.  

| ARGUMENTS | DESCRIPTION       |
|:--:       | :--               | 
| fc        | The feature collection to convert.    |
| "column_name" | The name of the column with the numeric data to populate the pixel values of the output raster. | 
| "reducer"     | How you would like to handle cases where two of more features overlap. Essentially, what value do you want to populate a pixel with when there is more than one number? This must be a string and one of the following: "mean", "first", "max", "min". |


---  

## __raster to vector__

These methods typically convert images to feature collections.  

_more soon_  


### __:earth_americas: make objects with vectors__ 

This method identifies objects from rasters based on two conditions: 

(1) Pixels share the same value.  
(2) Pixels form contiguous regions that can be represented with a polygon.  

It returns a feature collection of distinct regions and includes the area as an attribute of each feature.  

```js
var objects_with_vectors = geo.iConvert.makeObjectsWithVectors(image, "property", scale, extent, "unit");

```

| ARGUMENTS | DESCRIPTION   | 
| :--       | :--           |
| __image__ | Input image with a band that represent boolean or nominal (class) raster to clump.    |  
| __"property"__    | A description (as a string) of the boolean or class data used to clump. Flr example, "class".       |  
| __scale__ | Scale of analysis to help troubleshoot TIME OUT errors. Often good practice to start relatively coarse and then increase resolution in later runs.        |  
| extent    | The area of interest or study region to constrain analysis.         |
| "unit"    | Choose between "acres", "sq_m", and "sq_km"               |  

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>