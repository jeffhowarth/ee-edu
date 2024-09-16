# __scalar operations__

Uniformly change the values of all data in a raster object by adding, subtracting, multiplying, or dividing the raster with a constant.   

### __change value units__ 

A common example is when you need to change the units of your data. For example, to change elevation data from centimeters to meters you divide all elevation values by 100. 

```js
var output = input.divide(constant);
```

### __vertical exaggeration__ 

Another common example is when you want to apply vertical exaggeration to a terrain operation by multiplying the elevation values by a constant, usually called the __z-factor__. For example, by multiplying elevation by 2, you will exaggerate the terrain, making every location appear twice as high as it 'really' is. It is often helpful to exaggerate terrain when visualizing micro-topography at large scales or macro-topography at small scales.  

```js
var output = input.multiply(constant);
```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>