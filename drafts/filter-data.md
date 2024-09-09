## by attribute  

```js

// -------------------------------------------------------------
//  FILTER COLLECTION BY ATTRIBUTE. 

//  Input must be a collection.
//  Output is a collection, where each object in collection satisfies criterion.

//  Set CRITERION (see options in ee.Filter docs).
//  Set "property_name".
//  Set "value".
// -------------------------------------------------------------

```

```js

var output = input
    .filter(ee.Filter.CRITERION("property_name", "value"))
;

// -------------------------------------------------------------

```

---  

## by bounds  

```js

// -------------------------------------------------------------
//  FILTER COLLECTION BY REGION. 

//  Input must be a feature collection.
//  BOUNDS may be a point, line, or polygon geometry, feature, or feature collection.
//  Output is a collection, where each object intersects.
// -------------------------------------------------------------

```  

```js

var output = input
    .filterBounds(BOUNDS)
;

// -------------------------------------------------------------

```

---

## select image band  

```js

// -------------------------------------------------------------
//  SELECT IMAGE BAND. 

//  Input must be an image or image collection.
//  'Band_name' is name of band as a string or list of bands (list of strings).
//  Output is same data type as input. 
// -------------------------------------------------------------

```  

```js

var output = input
    .select('band_name')
;

// -------------------------------------------------------------

```

---   

[filter-collection]: ../methods/filter-data.md#by-attribute  
[filter-bounds]: ../methods/filter-data.md#by-bounds  