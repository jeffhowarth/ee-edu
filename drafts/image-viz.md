## make histogram of image values 

```js
// Make a viz dictionary.

var input_viz = {
  min: [0,0,0],                       // List of min in same order as band list.
  max: [255,255,255],                 // List of max in same order as band list.
  bands: ['R', 'G', 'B']              // In this example, R is index 0, G is index 1, and B is index 2.
};

// Make a histogram to see data distribution.  

var b = 0;                            // This targets a band number by the list index. 0 will target R.
var i = INPUT;                        // This targets an image. Replace IMAGE with image variable.
var v = input_viz;                    // This targets the viz parameters for the image.

var histogram = t.makeHistogram(
  i,                                  // Must be an image (not an image collection).
  v.bands[b],                         // Select one band at a time.
  3,                                  // Pixel resolution of image.
  v.min[b],                           // Minimum value of x-axis
  v.max[b]                            // Maximum value of x-axis.
  )
;

// Print, print, print...

print(
  "HISTOGRAM", 
  histogram
  )
;

// -------------------------------------------------------------

```

## Print min and max of an image 

```js
// -------------------------------------------------------------
//  PRINT MIN AND MAX OF AN IMAGE 

//  IMAGE must be, well, an image... 
//  REGION must be a feature collection or feature that define study region.
//  SCALE is pixel scale of request; the function will run faster if request a lower resolution.
//  LABEL to print as a header in Console (must be a string). 

// -------------------------------------------------------------
```

```js
t.printImageRange(image, region, scale, label);

```

Please note: you do not need to store the output of this function as a variable. You just need to run the function with your desired arguments and a dictionary with the min/max values will be printed to the Console.  

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}.   

---

## Viz with gamma to influence midtones  

```js
// -------------------------------------------------------------
//  VIZ WITH GAMMA TO INFLUENCE MIDTONES
//
//  A gamma > 1 will lighten midtones.
//  A gamma < 1 will darken midtones. 
// -------------------------------------------------------------

var viz = {
  
  min: 0, 
  max: 255,
  gamma: 1.5
  
  }
;

```

---

## Blend two images  

```js
// -------------------------------------------------------------
//  BLEND TWO IMAGES

//  Thanks to Jesse Anderson's gee-blend module. 
//  https://github.com/jessjaco/gee-blend

//  These are similar to Photoshop overlay techniques.  
//  It is often more effective to blend two images than try 
//  to visually combine them by lowering the opacity of one layer.  
// -------------------------------------------------------------
```

```js
var blend = require('users/jja/public:blend.js');

var output = blend.multiply(rgb1, rgb2);          // See gee-blend docs for other blend options besides multiply.  

Map.addLayer(output, {}, "RGB1 and RGB2 blend");

// -------------------------------------------------------------

```

Read the [gee-blend docs][gee-blend-docs]{target=_blank} to learn more about this useful module for cartography with ee.  


[make-histogram]: ../methods/image-viz.md#make-histogram-of-image-values 
[print-min-max]: ../methods/image-viz.md#print-min-and-max-of-an-image   
[viz-gamma]: ../methods/image-viz.md#viz-with-gamma-to-influence-midtones  
[viz-blend]: ../methods/image-viz.md#blend-two-images  


[tasks-module]: https://code.earthengine.google.com/?accept_repo=users/jhowarth/public  
[gee-blend-docs]: https://github.com/jessjaco/gee-blend  