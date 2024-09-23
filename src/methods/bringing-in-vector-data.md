# __bringing in vector data__  

_more forthcoming_  

## __gather & inspect data__ 

---  

### construct feature collection from address  

```js

var fc = ee.FeatureCollection("address/of/cloud/data");

```

---  

### how many rows in table?  

```js  
print(
  "FC SIZE",
  fc.size()
);
```

---  

### what are names of columns?

```js
print(
  "FC COLUMN NAMES",
  fc.first().propertyNames()
);
```

---  

### what is first row of table?

```js
print(
  "FC FIRST ROW",
  fc.first()
);
```

---  

### what are all unique attributes of a column?

```js  
print(
  "FC ATTRIBUTES FOR COLUMN: ",
  fc.aggregate_array('property_name').distinct().sort()
);
```

---  

### display as map layer  

```js  
Map.addLayer(fc, {color: 'white'}, "Layer Name");

```

---  

### full pattern  

```js
// Gather fc data from address.

var fc = ee.FeatureCollection("address/of/cloud/data");

// Inspect the table.  

print(
  "FC SIZE",
  fc.size(),
  "FC COLUMN NAMES",
  fc.first().propertyNames(),
  "FC FIRST ROW",
  fc.first(),
  "FC ATTRIBUTES FOR COLUMN: ",
  fc.aggregate_array('property_name').distinct().sort()
);

// Display as map layer. 

Map.addLayer(fc, {color: 'white'}, "Layer Name");

```

---  

## __make new geometries__  

---   

### :earth_americas: bounding box  

---  

```js
var fc_bounds = geo.fcGeometry.boundingBox(fc)
```

---  

### :earth_americas: centroid  

---  

```js
var fc_centroid = geo.fcGeometry.centroidPoint(fc)
```

---  

### :earth_americas: convex hull 

--- 

```js
var fc_convex_hull = geo.fcGeometry.convexHullPolygon(fc)
```


---  

## __convert vector to raster__  

--- 

### :earth_americas: FC to boolean image  

This method converts a feature collection into a boolean image.

```js
var image_boolean = geo.fcConvert.toBooleanImage(fc);
```

---  

### :earth_americas: FC to nominal image  

This method converts a feature collection with nominal attributes to a single-band image and prints a dictionary that reports the integer code for each unique attribute specified by column name.   

```js
var image_nominal = geo.fcConvert.toNominalImage(fc, "column_name");

```



---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>