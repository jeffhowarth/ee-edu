# __explain layer symbology__  

Methods for defining what colors in palettes _mean_ on your map.  

_more forthcoming_ 

## __define colors with legend__  

These methods take some or all of the following arguments.

| ARGUMENT          | DESCRIPTION   |
| --:               | :--           |
| __"title"__           | Label for the legend. Must be a string. Often a short description of image will do.  |
| __viz__               | The viz dictionary that defines how to visualize (display) the data.   | 
| __class_labels__      | A list of names for each color in the palette that define the classes or categories of the data. |
| __"position-on-map"__ | Where to place the legend. Must be a string. Composed as "row - column", where rows are "bottom", "middle", or "top" and columns are "left", "center", "right". For example, "bottom-right". There is no "middle-center". |  

### __:earth_americas: image with continuous data__  

If the image contains continuous or cyclical data, place a snapshot of the color gradient on the Map with labels that identify the minimum, maximum, and midpoint data value mapped to the gradient. 

```js
// Make legend from image with continuous data. 

var legend_continuous = geo.iCart.legendContinuous(
  "title", 
  viz, 
  "position-on-map"
  )
;

// Add legend to Map.  

Map.add(legend_continuous);

```

---

### __:earth_americas: from image with nominal data__

If the image contains nominal (discrete) data, place a symbol dictionary that defines each swatch of the palette with a label, or name for the class.     

```js

// Make legend from image with nominal data.

var legend_nominal = geo.iCart.legendNominal(
  "title", 
  viz, 
  class_labels, 
  "position-on-map"
  )
;

// Add legend to Map.  

Map.add(legend_remapped);
```



---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>