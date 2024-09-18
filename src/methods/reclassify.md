# __reclassify images__  

These methods purposefully reclassify the values in an image. 

_more forthcoming_  

### __Make a boolean (true/false) raster__   

![boolean](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/reclassify/boolean.png)

<center>

``` mermaid
graph LR
  input[image]
  method(".gt()") ;
  output[/"image_boolean"/]  ;
  arg1["20"]  ;

  input --> method
  method --> output
  arg1 --o method


  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class input in-out; 
  class method op;
  class output in-out;
  class arg1 arg;
```

</center>

```js
var image_boolean = image.gt(20);  
```

The table below lists some of the common methods to ask true or false questions about a raster. Each takes a number as an argument. 

<center>

| METHOD                        | DESCRIPTION                                             |
| --:                           | :--                                                     |
|```.eq()```, ```.neq()```      | Equal to, not equal to                                  |    
|```.gt()``` ```.gte()```       | Greater than, greater than or equal to                 |   
|```.lt()``` ```.lte()```       | Less than, less than or equal to                 |   

</center>

---  

### __:earth_americas: Reclassify by equal intervals__  

![equal intervals](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/reclassify/equal-interval.png)

<center>

``` mermaid
graph LR
  method("geo.iReclass.equalInterval()") ;
  output[/"image_reclassified"/]  ;
  arg1["image"]  ;
  arg2["interval"]  ;

  method --> output
  arg1 --o method
  arg2 --o method

  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class method op;
  class output in-out;
  class arg1 arg;
  class arg2 arg;
```

</center>


```js
var image_reclassified = geo.iReclass.equalInterval(image, interval);
```

---   

### __Remap old values to new values__

![remap](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/reclassify/remap.png)

<center>

``` mermaid
graph LR
  input["image"] ;
  method(".remap()") ;
  output[/"image_remapped"/]  ;
  arg1["[original values]"]  ;
  arg2["[new values]"]  ;

  input --> method  
  method --> output
  arg1 --o method
  arg2 --o method

  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  
  class input in-out;
  class method op;
  class output in-out;
  class arg1 arg;
  class arg2 arg;
```

</center>

```js
var image_remapped = image.remap(
    [1,2,3,4,5,6,7,8,9,10],            // Original values
    [1,1,2,2,3,3,4,4,5, 5]             // New values
    )
  ;

```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>