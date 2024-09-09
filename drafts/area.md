## acres of each feature in collection 

```js

// -------------------------------------------------------------
//  CALCULATE AREA (ACRES) OF FEATURES IN COLLECTION. 
// -------------------------------------------------------------

//  This CRS is good for Vermont. Replace if you work elsewhere.

var crs = "EPSG:32145";

//  Input must be a feature collection.
//  Output is a feature collection.
//  Each output feature has new property 'acres' that holds the area of feature.
//  Replace 'acres' with something else to define an alternative property name. 
//  Remember to following naming rules for properties. 
// -------------------------------------------------------------

```

```js  

var output = input
  .map(t.howManyAcres(crs, 'acres'))
;

// -------------------------------------------------------------

```

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 

---  

## sq km of each features in collection 

```js

// -------------------------------------------------------------
//  CALCULATE AREA (SQUARE KM) OF FEATURES IN COLLECTION. 
// -------------------------------------------------------------

//  This CRS is good for Vermont. Replace if you work elsewhere.

var crs = "EPSG:32145";

//  Input must be a feature collection.
//  Output is a feature collection.
//  Each output feature has new property 'sq_km' that holds the area of feature.
//  Replace 'sq_km' with something else to define an alternative property name.  
//  Remember to following naming rules for properties (no spaces).
// -------------------------------------------------------------

```

```js 

var output = input
  .map(t.howManySqKm(crs, 'sq_km'))
;

// -------------------------------------------------------------

```

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 

---  

## make pixel area image  

```js

// -------------------------------------------------------------
//  MAKE PIXEL AREA IMAGE.

//  Returns an image with values that represent pixel area in acres. 
//  Modify second line to alter units. 
// -------------------------------------------------------------


```

```js  

var output = ee.Image.pixelArea()
  .divide(4046.86)                  // converts to acres

// -------------------------------------------------------------
```

---  

[area-fc-acres]: ../methods/area.md#acres-of-each-feature-in-collection  
[area-fc-sq-km]: ../methods/area.md#sq-km-of-each-feature-in-collection      

[pixel-area]: ../methods/area.md#make-pixel-area-image   

[tasks-module]: https://code.earthengine.google.com/?accept_repo=users/jhowarth/public  