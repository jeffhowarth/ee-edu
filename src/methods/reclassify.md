# __reclassify images__  

These methods purposefully reclassify the values in an image. 

_more forthcoming_  

### __Make a boolean (true/false) image__   

```js
var image_boolean = image.neq(0);  
```

### __:earth_americas: Reclassify by equal intervals__  

```js
var image_reclassified = geo.iReclass.equalInterval(image, interval);
```

### __Remap old values to new values__

```js
var image_remapped = image.remap(
    [1,2,3,4,5,6,7,8,9,10],            // Original values
    [1,1,2,2,3,3,4,4,5, 5]             // New values
    )
  ;

```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>