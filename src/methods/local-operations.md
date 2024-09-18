# __local operations__  

These methods compare values at corresponding pixels in two or more rasters. 

_more forthcoming_  

---  

### __mask pixels__  

Masks act like masking tape when you paint. Any pixel with the value 0 in the mask acts like tape and prevents numbers in the output raster from being painted at that location. Masked values will not be displayed with colors when you place the raster layer on a Map. Masked values in an input raster will also be ignored in any subsequent method.    

---  

![mask](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/mask.png)

---  

<center>

``` mermaid
graph LR
  input[image]
  method(".updateMask()") ;
  output[/"image_with_mask"/]  ;
  arg01["masking_image"] ;

  input --> method
  method --> output
  arg01 --o method


  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class input in-out; 
  class method op;
  class output in-out;
  class arg01 arg; 
```

</center>

---  

```js

var image_with_mask = image.updateMask(masking_image);

```

---  

### __self mask pixels__  

If you want to ignore pixels that store the value 0 in an image, you can self-mask.  

---  

![self mask](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/self-mask.png)

---  

<center>

``` mermaid
graph LR
  input[image]
  method(".selfMask()") ;
  output[/"image_with_mask"/]  ;

  input --> method
  method --> output


  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class input in-out; 
  class method op;
  class output in-out;
```

</center>

---  

```js

var image_with_mask = image.selfMask();

```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>