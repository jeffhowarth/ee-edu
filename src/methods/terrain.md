# __terrain__  

These methods derive topographic attributes of terrain from raster elevation data. 

Many terrain methods compare vertical elevation to horizontal distance. For these operations to work correctly, the vertical units (often called __z-units__) need to be the same as the horizontal units (__xy units__). Because horizontal units in Earth Engine are always meters, this means that the general pattern is to first check the z-units of your elevation data and see if you need to scale the values before you call a terrain method. 

<center>

``` mermaid
graph LR

  step01>"If z-units are meters"] ;
  step02("Apply a terrain method") ;
  step03>"If z-units are not meters"] ;
  step04("Apply scalar operation") ;

  step01 --> step02
  step03 --> step04
  step04 --> step02

  classDef task fill:#DDE6C3,stroke-width:0px,color:#000000;
  
  class step01 task; 
  class step02 task;
  class step03 task; 
  class step04 task;

```

</center>

## __derive slope__

__Derive slope of a surface in degrees from elevation in meters.__  

Call the ```ee.Terrain.slope``` method with the elevation data (with z-units meters) as the argument.  

<center>

``` mermaid
graph LR
  step02("SLOPE") ;
  step03[/"OUTPUT_SLOPE"/]  ;
  arg01["elevation in meters"] ;

  step02 --> step03
  arg01 --- step02


  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class step01 in-out; 
  class step02 op;
  class step03 in-out;
  class arg01 arg; 
```

</center>

  

```js
var output_slope = ee.Terrain.slope(input_elevation);

```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>