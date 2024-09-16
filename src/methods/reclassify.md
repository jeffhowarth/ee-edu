# __reclassify images__  

These methods purposefully reclassify the values in an image.   

### __Make a boolean (true/false) image__   

```js
var image_boolean = image.neq(0);  
```

### __:earth_americas: Reclassify by equal intervals__  

```js
var image_reclassified = geo.iReclass.equalInterval(image, interval);
```

### __Remap old values to new values__

```js
var image_remapped = image.remap(
    [1,2,3,4,5,6,7,8,9,10],            // Original values
    [1,1,2,2,3,3,4,4,5, 5]             // New values
    )
  ;

```