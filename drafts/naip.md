
## tag NAIP collection with date and number of bands

```js
// -------------------------------------------------------------
//  Tag filtered collection with date and number of bands. 

//  Collection must be a NAIP image collection.
// -------------------------------------------------------------
```

```js

output = t.tagDateAndBands(collection)
;

// -------------------------------------------------------------

```

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 

---  

### make mosaic image from image collection    

```js
// -------------------------------------------------------------
//  Make mosaic image from image collection
// -------------------------------------------------------------
```

```js

var output = t.makeMosaic(collection, year, region);

// -------------------------------------------------------------

```

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 

---


[naip-tag]: ../methods/naip.md#tag-naip-collection-with-date-and-number-of-bands  
[naip-mosaic]: ../methods/naip.md#make-mosaic-image-from-image-collection  

[tasks-module]: https://code.earthengine.google.com/?accept_repo=users/jhowarth/public  