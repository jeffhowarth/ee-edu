__STARTERS__  

# __*NAIP*__  

Earth Engine provides images collected from the National Agricultural Imagery Program [(NAIP)][naip]{target=_blank} as cloud assets.

The starter script below will help you quickly filter and mosaic this collection for an area of interest.  

[naip]: https://developers.google.com/earth-engine/datasets/catalog/USDA_NAIP_DOQQ

## __:earth_americas: NAIP__  

```js
/*    
// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><

    AUTHOR:     
    DATE:       
    TITLE:  NAIP starter 

// ><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><
*/

var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 


// -------------------------------------------------------------
//  Define AOI from point with 10km buffer.
// -------------------------------------------------------------

var geometry = ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-73.16875, 44.01336]),
            {
              "system:index": "0"
            })]);

var aoi = geo.fcProximity.bufferByDistance(geometry, 10000);

Map.centerObject(geometry, 15);

// -------------------------------------------------------------
//  Get year of interest.
// -------------------------------------------------------------

var year_list = geo.icNAIP.yearList(
    aoi,        
    4       // Change to 3 if you would like to include earliest images that lack NIR band.  
);

var yoi = year_list.get(0);   // This gets the first year in the year list.

// var yoi = year_list.get(year_list.length().subtract(1));  // This gets the last year.

// print("Year of interest", yoi);

// -------------------------------------------------------------
//  Filter NAIP image collection by aoi, year, and number of bands.
// -------------------------------------------------------------

var ic = ee.ImageCollection("USDA/NAIP/DOQQ")
  .filterBounds(aoi)
  .filter(ee.Filter.calendarRange(yoi, yoi, "year"))
  .map(geo.icNAIP.setNumberOfBands)
  .filter(ee.Filter.eq("number_of_bands", 4))
  ;

// geo.icGather.inspectCollection("NAIP Collection", ic);

// -------------------------------------------------------------
//  Mosaic image collection.
// -------------------------------------------------------------
  
var ic_mosaic = geo.icFlatten.mosaicToImage(ic);

// print("Mosaic", ic_mosaic);

// -------------------------------------------------------------
//  Define viz dictionaries.
// -------------------------------------------------------------

var rgb_viz_natural = 
    {
        bands:  ['R', 'G', 'B'],      
        min:    [0, 0, 0],        
        max: [255, 255, 255],
        gamma: [1,1,1]    
    }
;

var rgb_viz_false = 
    {
        bands:  ['N', 'R', 'G'],      
        min:    [0, 0, 0],        
        max: [255, 255, 255],
        gamma: [1,1,1]    
    }
;

// -------------------------------------------------------------
//  Refine viz dictionaries with histogram.
// -------------------------------------------------------------

// To refine natural image.
var histogram = geo.iCart.iHistogramRGB(ic_mosaic, rgb_viz_natural);

// // To refine false image.
// var histogram = geo.iCart.iHistogramRGB(ic_mosaic, rgb_viz_false);

print(histogram);

// -------------------------------------------------------------
//  Display as Map layers. 
// -------------------------------------------------------------

Map.addLayer(ic_mosaic,rgb_viz_false,"Earliest False Color",true);
Map.addLayer(ic_mosaic,rgb_viz_natural,"Earliest Natural Color ",true);


```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>