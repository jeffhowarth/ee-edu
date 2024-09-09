# __construct data object__  

One of the first things you will usually do with Earth Engine is load some data from the cloud. This involves calling an ee method that constructs a data object. As an argument, these methods take an address that describes where the data are stored in the cloud.  

## __image from address__    

__Use ```ee.Image()``` method to construct an image object.__ 

In the snippet below, replace ADDRESS with a data address (as a string);

```js
var output = ee.Image("address/of/cloud/data");
```

[construct-image]: ../methods/construct-data-object.md#image-from-address

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>