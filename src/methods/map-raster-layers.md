# __map raster layers__  

Any geographic information system will provide methods for displaying data as a map layer. The patterns below deal with mapping raster data as layers.  

## __display data as map layer__       

__Use the ``` Map.addLayer() ``` method to display data as a map layer.__   

```js
Map.addLayer(data,viz,"Layer Name",show,opacity);
```

The ```Map.addLayer()``` method takes the following arguments: 

| ARGUMENT      | DESCRIPTION   |
| --:           | :--           |
| data          | The name of the variable that contains the data that you wish to display.  |
| viz           | The viz dictionary that defines how to visualize (display) the data.   | 
| layer name    | A string that provides a label for the data in the list of layers.    |
| show          | A boolean argument to control whether or not the layer is displayed when first loaded. |
| opacity       | A decimal number between 0 and 1 to adjust the opacity of the layer.                  |


## __raster viz dictionary__  

__For raster data, store the viz dictionary as a variable and then call this variable when you add the map layer.__   

Here is a common pattern to visualize single-band grayscale images:

```js
var single_viz = 
    {
        min: [],        
        max: [],        
    }
;
```

Here is a common pattern to visualize single-band images:

```js
var single_viz = 
    {
        min: [],        
        max: [],        
        palette: [],    
    }
;
```

This is a common pattern to visualize multi-band images:

```js
var multi_viz = 
    {
        bands: [],      
        min:  [].      
        max: [],        
        gamma: [],      
    }
;
```

---   
 
## __:earth_americas: set viz range to data range__  

__Print the min and max data value of a raster image and then use as min and max values in viz dictionary.__ 

```js
var output_min_max = geo.iCart.iMinMax(input_image);

print("Min & max value of image", output_min_max);

```

---

## __:earth_americas: chart histogram of data values__  

__See how your data are distributed between the minimum and maximum data value by charting a histogram.__

```js
var output_histogram = geo.iCart.iHistogram(image);

print("Image histogram", output_histogram);
```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>