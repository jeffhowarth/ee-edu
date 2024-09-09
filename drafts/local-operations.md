## maximum at locations       

```js
// -------------------------------------------------------------
//  MAXIMUM AT LOCATIONS

//  This operation does pairwise comparisons of pixel values between
//  two images (i1, i2); the output stores the maximum of each pair. 
// -------------------------------------------------------------

```

```js

var output = i1.max(i2);

// -------------------------------------------------------------

```

---

## minimum at locations       

```js
// -------------------------------------------------------------
//  MINIMUM AT LOCATIONS

//  This operation does pairwise comparisons of pixel values between
//  two images (i1, i2); the output stores the minimum of each pair. 
// -------------------------------------------------------------

```

```js

var output = i1.min(i2);

// -------------------------------------------------------------

```

---  

## intersect two binaries    

```js
// -------------------------------------------------------------
//  INTERSECT TWO BINARIES.

//  i1 and i2 are both binary images {0,1}.
//  output is a binary image {0,1}.
// -------------------------------------------------------------
```

```js

var output = i1.and(i2);

// -------------------------------------------------------------

```

---  

## erase values at locations with binary   

```js
// -------------------------------------------------------------
//  ERASE VALUES AT LOCATIONS WITH BINARY.

//  INPUT is an image with values to erase.
//  BINARY is a binary image {0,1}.
//  OE (output erased) is an image. 
// -------------------------------------------------------------
```

```js

var oe = input
  .multiply(binary)
;

print(
  "ERASED",
  oe
  )
;

// -------------------------------------------------------------

```

---  

## mask values at locations    

```js
// -------------------------------------------------------------
//  MASK VALUES AT LOCATIONS .

//  INPUT is an image with values to mask.
//  MASK is an image with zero and non-zero values.
//  OUTPUT is same as input except all zero values in MASK are masked
// -------------------------------------------------------------
```

```js

var output = input.updateMask(mask)
;

// -------------------------------------------------------------

---

[local-erase]: ../methods/local-two-layers.md#erase-values-at-locations-with-binary 
[local-intersection]: ../methods/local-two-layers.md#intersect-two-binaries  
[local-max]: ../methods/local-two-layers.md#maximum-at-locations
[local-min]: ../methods/local-two-layers.md#minimum-at-locations
[local-mask]: ../methods/local-two-layers.md#mask-values-at-locations


[local-reclass]: ../methods/local-one-layer.md#reclassify-nominal-values  
[local-multiply-constant]: ../methods/local-one-layer.md#multiply-image-by-constant
[local-classify-intervals]: ../methods/local-one-layer.md#classify-image-by-equal-interval  