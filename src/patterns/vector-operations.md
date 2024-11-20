__PATTERNS__  

# __*vector operations*__  

Vector operations work with tables of geometries and often attributes. 

---   

## __transform geometries__  

These methods create new geometries based on the input geometries of feature collections.    

_More to come._

### __:earth_americas: bounding box__ 

---  

```js
var fc_bounds = geo.fcGeometry.boundingBox(fc);

Map.addLayer(fc_bounds, {color: 'cyan'}, "Bounding box", false);

```

---  

### __:earth_americas: centroid__  

---  

```js
var fc_centroid = geo.fcGeometry.centroidPoint(fc);

Map.addLayer(fc_centroid, {color: 'yellow'}, "Centroid point", false);

```

---  

### __:earth_americas: convex hull__   

--- 

```js
var fc_convex_hull = geo.fcGeometry.convexHullPolygon(fc);

Map.addLayer(fc_convex_hull, {color: 'magenta'}, "Convex hull", false);

```

---  

## __multipart vs. single part geometries__  

These methods change the form of the geometries liked to rows in a table. The picture below illustrates several concepts. The leftmost frame (__A__) shows a table with a __singlepart__ geometry; a single polygon linked to each row in the table. The center frame (__B__) shows a table linked to __multipart__ geometry (multipart geometry can link two or more polygons to a single row of attributes). The rightmost frame (__C__) shows another table with multipart geometries; four polygons associated with one row.   

![aggregation-levels](http://geography.middlebury.edu/howarth/ee_edu/eePatterns/vector-operations/aggregation-levels.png)

Operations are shown laterally. Moving from A to B is a __dissolve__ operation (singlepart --> multipart), while moving from B to A is an __explode__ operation (multipart --> singlepart). Note the asymmetry between moves on the right side. From B to C is another dissolve, but from C to B is not possible.  

### __:earth_americas: dissolve by attribute__ 

This will dissolve a feature collection into multipart features that share a common attribute. 

```js
// -------------------------------------------------------------
//  Dissolve by attribute
// -------------------------------------------------------------

var output_dissolve = geo.fcGeometry.dissolveByAttribute(fc, "property");

print("DISSOLVE", fc.first(), output_dissolve.first());

```

Using the illustration at the top of this section, the snippet below will transform A into B. 

```js
var B = geo.fcGeometry.dissolveByAttribute(A, "CITY");
```

_Please note that the property name is case sensitive, so when working with HOLC data you would need to specify "city" or "holc_grade"._   

## __vector overlay__  

Vector overlay operations compare locations between two vector layers. In Earth Engine, the vector layers are generally features in a feature collection.  

_more soon_  

### __:earth_americas: clip by region__

```geo.fcOverlay.clipByRegion()``` is a __knife__ method that takes two arguments. 

| ARGUMENT          | DESCRIPTION       |
| :--:              | :--               |
| __fc_dough__      | A vector dataset (feature collection) with features that you want to cut. |  
| __fc_cutter__     | A vector dataset (feature collection) with features that you want to use as the knife to cut the dough. |   

The output is a feature collection that retains that attributes but alters the geometry of the dough.  

```js

var fc_clip = geo.fcOverlay.clipByRegion(fc_dough, fc_cutter);

```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>