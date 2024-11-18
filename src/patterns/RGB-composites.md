__PATTERNS__  

# __*RGB composites*__  

## __additive color system__ 

RGB composites use additive color to display raster data values in three bands at once. 

_More soon._

---  

<!-- Before we get into the code, we should step back and think about why an image will often contain more than one band, why we would want to display the data in more than one band at once, and how additive color works as a system for comparing three data values.  

## __display multiple conditions at locations__ 

Let's say that you wanted to map the population of four zones at three different moments in time.

In a vector model, you could do this with multiple __columns__ in a table.

![vector-model][]  

In a raster model you could do this with multiple __bands__ in an image.

![raster-model][]  

The main idea is that _bands in an image function like columns in a table_; they allow you to describe multiple attributes for locations. 

Now let's say that you want to visualize change in these three conditions. If you made charts for each zone, it would look something like this: 

![three-band-charts][]  

Displaying these charts as a single map layer is tricky if you get stuck thinking about a map layer as something that displays data values with a single palette.  

When you think in additive color, the problem becomes quite simple.  

![as-additive-color][] 

Here is how additive color works:

* there are three color channels: Red, Green, and Blue 
* the values of a single band are displayed in one color channel  
* the three color channels combine to create a color displayed on the monitor.  

---   -->

Use the RGB mixer below to create the colors by adding values in Red, Green, and Blue channels.  

<iframe
  src="https://jhowarth.users.earthengine.app/view/ee-edu-rgb"
  style="width:910px; height:576px;"
></iframe>

[_Open app in new browser window_](https://jhowarth.users.earthengine.app/view/ee-edu-rgb){target=_blank}  

---  

Here is the key for primary and secondary additive colors.  

![Additive color](https://geography.middlebury.edu/howarth/ee_edu/RGB_alt3.png)  

---  


## __RGB viz__  

This is a basic pattern to visualize __multi-band images__ as a combination of red, green, and blue channels.  

```js
var rgb_viz = 
    {
        bands:  ['red', 'green', 'blue'],      
        min:    [0, 0, 0],        
        max: [255, 255, 255],
        gamma: [1,1,1]    
    }
;
```

The _gamma_ property bends the function that maps display values to data values in order to lighten or darken the midtones of the image. Lowering the gamma value (towards 0) darkens the image, while raising the gamma value (towards 2) lightens the image.  

The min, max, and gamma values can be adjusted separately for each band. 

## __natural and false color__  

A __natural color__ image displays reflectance in the Red, Green, and Blue bands of the EM spectrum using the Red, Green, and Blue color channels, respectively. The result looks roughly similar to what we see when we have a window seat and the shade up. 

A __false color__ image breaks this like-to-like mapping of the EM spectrum to additive color. For example, the near infrared (NIR) false color image displays reflectance in NIR, Red, and Green bands of the EM spectrum to the Red, Green, and Blue color channels. respectively. The result looks different from our experience, but is often helpful for distinguishing different types of vegetation and surfaces that otherwise look 'green' in natural color composites.  

Importantly, a NIR false color image is just one example of a false color image. Many other false color images display reflectance in shortwave infrared (SWIR), sometimes called mid-range infrared, that are useful in wide range of applications. 

To better understand how false color images work, please read:

* [Why is that Forest Red and that Cloud Blue? How to Interpret a False-Color Satellite Image](https://earthobservatory.nasa.gov/features/FalseColor){target=_blank}  

This is an old but still helpful reference for exploring different band combinations for false color:  

* [Landsat band combinations](https://web.pdx.edu/~nauna/resources/10_BandCombinations.htm){target=_blank}  

---  

## __chart spectral signatures__ 

To interpret and explain why false color images look the way they do, it can be helpful to chart the spectral signature of locations in an image.  

If you add the appropriate pattern below to the end of a script that produces an image from a Landsat collection, you should be able to click on locations on the Map and chart the spectral signature of each location.    

---  

### __:earth_americas: Landsat 5__  

```js

// -------------------------------------------------------------
//  Click to chart spectral signatures from L5 image.
// -------------------------------------------------------------

var config = {};
var panel_chart = ui.Panel({style: {position: 'bottom-left'}});
var samples = [];

Map.onClick(function(coords) {          // To embed in app, change "Map" to "left_Map" or "right_Map".
  
  config.poi = ee.Geometry.Point(coords.lon, coords.lat);
  samples.push(ee.Feature(config.poi, {'sample': samples.length}));
  
  panel_chart.clear();
  panel_chart.add(geo.icLandsat.chartSpectralSignatureL5(
    output,                             // Name of L5 image ('output' assumes you are using starter script).
    samples
    ));
  }
);

Map.add(panel_chart);                   // To embed in app, change "Map" to "side_bar".

```

---  

### __:earth_americas: Landsat 7__  

```js

// -------------------------------------------------------------
//  Click to chart spectral signatures from L7 image.
// -------------------------------------------------------------

var config = {};
var panel_chart = ui.Panel({style: {position: 'bottom-left'}});
var samples = [];

Map.onClick(function(coords) {          // To embed in app, change "Map" to "left_Map" or "right_Map".
  
  config.poi = ee.Geometry.Point(coords.lon, coords.lat);
  samples.push(ee.Feature(config.poi, {'sample': samples.length}));
  
  panel_chart.clear();
  panel_chart.add(geo.icLandsat.chartSpectralSignatureL7(
    output,                             // Name of L7 image ('output' assumes you are using starter script).
    samples
    ));
  }
);

Map.add(panel_chart);                   // To embed in app, change "Map" to "side_bar".


```

---

### __:earth_americas: Landsat 8__  

```js

// -------------------------------------------------------------
//  Click to chart spectral signatures from L8 image.
// -------------------------------------------------------------

var config = {};
var panel_chart = ui.Panel({style: {position: 'bottom-left'}});
var samples = [];

Map.onClick(function(coords) {          // To embed in app, change "Map" to "left_Map" or "right_Map".
  
  config.poi = ee.Geometry.Point(coords.lon, coords.lat);
  samples.push(ee.Feature(config.poi, {'sample': samples.length}));
  
  panel_chart.clear();
  panel_chart.add(geo.icLandsat.chartSpectralSignatureL8(
    output,                             // Name of L8 image ('output' assumes you are using starter script).
    samples
    ));
  }
);

Map.add(panel_chart);                   // To embed in app, change "Map" to "side_bar".


```

---  

### __:earth_americas: Landsat 9__  

```js

// -------------------------------------------------------------
//  Click to chart spectral signatures from L9 image.
// -------------------------------------------------------------

var config = {};
var panel_chart = ui.Panel({style: {position: 'bottom-left'}});
var samples = [];

Map.onClick(function(coords) {          // To embed in app, change "Map" to "left_Map" or "right_Map".
  
  config.poi = ee.Geometry.Point(coords.lon, coords.lat);
  samples.push(ee.Feature(config.poi, {'sample': samples.length}));
  
  panel_chart.clear();
  panel_chart.add(geo.icLandsat.chartSpectralSignatureL9(
    output,                             // Name of the L9 image ('output' assumes you are using starter script).
    samples
    ));
  }
);

Map.add(panel_chart);                   // To embed in app, change "Map" to "side_bar".

```

---  

### __:earth_americas: MODIS__   

```js
// -------------------------------------------------------------
//  Click to chart spectral signatures from MODIS image.
// -------------------------------------------------------------

var config = {};
var panel_chart = ui.Panel({style: {position: 'bottom-left'}});
var samples = [];

Map.onClick(function(coords) {          // To embed in app, change "Map" to "left_Map" or "right_Map".

  config.poi = ee.Geometry.Point(coords.lon, coords.lat);
  samples.push(ee.Feature(config.poi, {'sample': samples.length}));

  panel_chart.clear();
  panel_chart.add(geo.icMODIS.chartSpectralSignatureMODIS(
    output,                             // Name of the MODIS image ('output' assumes you are using starter script).
    samples
    ));
  }
);

Map.add(panel_chart);                   // To embed in app, change "Map" to "side_bar".


```


---  

### __:earth_americas: Sentinel 2__    

```js
// -------------------------------------------------------------
//  Click to chart spectral signatures from S2 image.
// -------------------------------------------------------------

var config = {};
var panel_chart = ui.Panel({style: {position: 'bottom-left'}});
var samples = [];

Map.onClick(function(coords) {          // To embed in app, change "Map" to "left_Map" or "right_Map".

  config.poi = ee.Geometry.Point(coords.lon, coords.lat);
  samples.push(ee.Feature(config.poi, {'sample': samples.length}));

  panel_chart.clear();
  panel_chart.add(geo.icSentinel.chartSpectralSignatureS2(
    output,                             // Name of the S2 image ('output' assumes you are using starter script).
    samples
    ));
  }
);

Map.add(panel_chart);                   // To embed in app, change "Map" to "side_bar".






```


---

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivs 4.0 International License</a>.
