__PATTERNS__  

# __*vector overlay operations*__  

Vector overlay operations compare locations between two vector layers. In Earth Engine, the vector layers are generally features in a feature collection.  

_more soon_  

## __:earth_americas: clip by region__

```geo.fcOverlay.clipByRegion()``` is a __knife__ method that takes two arguments. 

| ARGUMENT          | DESCRIPTION       |
| :--:              | :--               |
| __fc_dough__      | A vector dataset (feature collection) with features that you want to cut. |  
| __fc_cutter__     | A vector dataset (feature collection) with features that you want to use as the knife to cut the dough. |   

The output is a feature collection that retains that attributes but alters the geometry of the dough.  

```js

var fc_clip = geo.fcOverlay.clipByRegion(fc_dough, fc_cutter);

```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>