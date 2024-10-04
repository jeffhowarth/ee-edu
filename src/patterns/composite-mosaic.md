__PATTERNS__

# _**flatten image collections**_

Many workflows for image collections will include a step that transforms an image collection into a single image (and __flattens__ the collection).  

## __composite image__  

If the collection represents a time series of satellite scenes, the workflow will often include a step that makes a __composite image__.

_We will get to composite images in the second half of the semester._  

---  

## __:earth_americas: mosaic image__ 

If the collection contains a set of small tiles, then a workflow will often include a step that makes a __mosaic image__. This is a common step in workflows with lidar products.  

![mosaic-collection](http://geography.middlebury.edu/howarth/ee_edu/eePatterns/flattenCollection/mosaic.png)


<center>

``` mermaid
graph LR

  method("geo.icFlatten.mosaicToImage()") ;
  output[/"ic_mosaic"/]  ;

  method --> output
  
  arg["ic"] ;
  
  arg --o method

  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class input in-out; 
  class method op;
  class output in-out;
  class arg arg; 
```

</center>

```js
var ic_mosaic = geo.icFlatten.mosaicToImage(ic);

print("Mosaic", ic_mosaic);

```

This method mosaics the tiles into a single image and gives the new image the same coordinate reference system as the first image in the collection. The crs defines the xy units of the image and this enables you to use the mosaic image as an input in terrain operations.  

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>