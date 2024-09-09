## zonal summary of dough within cutters  

```js
// -------------------------------------------------------------
//  ZONAL SUMMARY OF DOUGH WITHIN CUTTERS.

//  Adjust CRS for your study region.  
//  DOUGH must be an image with values to summarize. 
//  CUTTERS must be a feature collection.  
//  Adjust REDUCER for desired summary statistic.
//  Adjust SCALE to tune processing time vs acceptable accuracy.  
//  ZS will be a feature collection.
//  The name of ZS property will reflect the REDUCER.   
//  In below example, ZS property is 'sum'.  
// -------------------------------------------------------------
```

```js  

var crs = "EPSG:32145";             // Good for Vermont.

var zs = dough
  .reduceRegions(
    {
      collection: cutters, 
      reducer: ee.Reducer.sum(), 
      scale: 3, 
      crs: crs
    }
  )
;

// -------------------------------------------------------------

```

---

[zonal-sum]: ../methods/zonal-operations.md#zonal-summary-of-dough-within-cutters  