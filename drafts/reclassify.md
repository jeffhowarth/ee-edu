## reclassify nominal values  

```js
// -------------------------------------------------------------
//  RECLASSIFY VALUES AT LOCATIONS.

//  INPUT is an image with values to reclassify;
//  from key holds list of values in input image,
//  to key holds a list of new values, where the list index
//  determines the from --> to reclassification.
//  'BAND_NAME' is name of band to reclassify (default is first band).
//  OUTPUT is name for new reclassified image. 
// -------------------------------------------------------------
```

```js

var output = input.remap(
  {
    from: [0,1,2,3,4],
    to:   [0,0,1,0,1],
    bandName: 'band_name'
  }

); 

// -------------------------------------------------------------

```

---

## classify image by equal interval  

```js
// -------------------------------------------------------------
//  CLASSIFY AN IMAGE BY AN EQUAL INTERVAL

//  INPUT is an image with continuous values (like a DEM).
//  INTERVAL is an integer that defines equal interval of scheme. 

//  OUTPUT is an image, where values represent quotient as integer;
//    input = dividend, 
//    interval = divisor,  
//    remainder is ignored.
// -------------------------------------------------------------
```

```js

var output = input.divide(interval).ceil();

// -------------------------------------------------------------

```

---

## threshold an image

```js
// -------------------------------------------------------------
//  THRESHOLD AN IMAGE

//  INPUT is an image with values to convert to binary.
//  THRESHOLD is placeholder for criterion operator:

//    .eq() --> equals
//    .lt() --> less than 
//    .gt() --> greater than
//    etc. 
//
//  OUTPUT is binary, where all pixels that satisfy criterion are 1
//  and all other pixels are 0. 
// -------------------------------------------------------------
```

```js

var output = input.THRESHOLD(VALUE); 

// -------------------------------------------------------------

```

---   
