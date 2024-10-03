# __local overlay operations__  

These methods compare values at corresponding pixels in two or more rasters. 

![local-overlay-operations](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/local-operations-basics.png)

---  

## __masks__

Masks act like masking tape when you paint. When you mask pixels in a raster before displaying the raster as a map layer, all the pixels with the mask will remain transparent (they will not be displayed with a color). Similarly, when you mask pixels of an input raster in an operation, the masked pixels will be excluded from the computation.  

Typically, workflows with masks involve three steps.    

<center>

``` mermaid
graph LR
  step01("Make mask")
  step02("Apply mask") ;
  step03("Paint (display as layer)") ;
  step04("Transform (input in operation)") ;
 

  step01 --> step02
  step02 --> step03
  step02 --> step04


  classDef steps fill:#C9C3E6,stroke-width:1px,stroke: #00000000, color:#000000; 

  

  class step01 steps; 
  class step02 steps;
  class step03 steps;
  class step04 steps; 
```

</center>

### __mask pixels__  

This pattern uses another raster, typically a [Boolean raster](../reclassify/#boolean-raster) as a mask on another raster. 

Any pixel with the value 0 in the mask acts like masking tape and prevents numbers in the output raster from being painted at that location. Masked values will not be displayed with colors when you place the raster layer on a Map. Masked values in an input raster will also be ignored in any subsequent operation.    

![mask](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/mask.png)

---  

<center>

``` mermaid
graph LR
  input[image]
  method(".updateMask()") ;
  output[/"image_with_mask"/]  ;
  arg01["mask<br>boolean_raster"] ;

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

If you want to ignore pixels that store the value 0 in an raster, you can self-mask.  

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

### __unmask__  

If you are working with a masked image, you can remove the mask and populate all the masked locations with a constant. 

![self mask](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/unmask.png)

---  

---  

<center>

``` mermaid
graph LR
  input["image_with_mask"]
  method(".unmask()") ;
  output[/"image_without_mask"/]  ;
  arg["constant"]

  input --> method
  method --> output
  arg --o method  

  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  
  class input in-out; 
  class method op;
  class output in-out;
  class arg arg
```

</center>

---  

```js

var image_without_mask = image_with_mask.unmask();

```

---  

In Earth Engine, ```unmask()``` will replace masked values with 0 by default (This makes the method the inverse of ```selfMask()```. You can include an argument (a number in the parantheses) to specify a different constant.   

---  

## __logical comparisons__  

The diagram below illustrates three common logical comparisons between two regions: A, B. Going from left to right, the first picture shows the two regions. The second picture shows where either region A __or__ region B are present (or true), called the __union__ of the two. The third picture shows where both region A __and__ region B are present, called the __intersection__ of the two. The fourth and final picture shows where region A is present but __not__ region B. In this last case, region B acts like an eraser or __knife__ that cuts out the portion of region A that it touches.  

![Logical comparisons](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/logical-comparisons.png)

---  

The patterns below describe how each logical comparison shown above can be implemented with raster data models.  

---  

### __or (union)__  


The ```.or()``` method takes two rasters as inputs and kicks out a boolean raster that represents their union: pixels that are true (not 0) in raster A or pixels that are true (not 0) in raster B.  

![OR union](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/or-union.png)

---  

The inputs are commonly __boolean rasters__, as illustrated in the above diagram, but the method will work with nominal (class) data, returning a boolean raster.  

![OR union nominal case](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/or-nominal-case.png)

---  

The order of the inputs (which raster is image_A versus image_B) does not really matter. The main thing to remember here is that any masked pixels will be excluded from this operation. So it is good practice to triple-check your inputs to see if you are using a mask on pixels that should be zeros so that you do not inadvertently erase locations that are true in one layer but masked in another.  

```js

var image_union = image_A.or(image_B);

```

### __and (intersection)__


The ```and()``` method takes two rasters as inputs and kicks out a boolean raster that represents their intersection: locations that are true (not 0) in raster A and true (not 0) in raster B.  

![AND intersection](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/and-intersection.png)

--- 

Like the ```or``` operation, the inputs are commonly __boolean rasters__, but the method will work with nominal (class) data, returning a boolean raster as shown below.  

![AND nominal case](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/and-nominal-case.png)

---  

The order of inputs again does not really matter here. And because this operation is like a __knife__ that cuts and alters the shapes of inputs, this method is less sensitive to masks, unlike the ```or()``` method.

```js

var image_intersection = image_A.and(image_B);

```

---  

### __not__  

In Earth Engine, finding locations in raster A that are true but not true in raster B is a little tricky. The workflow involves inverting the binary of raster_B and then multiplying it against raster_A.   

![NOT](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/not.png)

---  

```js

var image_A_not_B = image_A.multiply(image_B_inverted_binary);

```

## __map arithmetic__  

As the diagram at the top of this page illustrates, a common type of local overlay operation performs arithmetic operations (addition, subtraction, multiplication, and division) with two rasters.  

---

### __addition__  

The ```.add()``` method performs addition between values in corresponding pixels of two rasters. The order (which raster is A versus B) does not matter. The main thing to remember is that any pixel that is masked will be excluded from the operation (so that output pixel will remain masked).  

![local-overlay-operations](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/add.png)

---   

```js
var image_A_add_B = image_A.add(image_B);

```

---

### __subtraction__  

The ```.subtract()``` method performs subtraction between values in corresponding pixels of two rasters. The order matters here: you subtract image_B from image_A. Masked pixels in either raster will remain masked in the output.  

![local-overlay-operations](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/subtract.png)

```js

var image_A_subtract_B = image_A.subtract(image_B);

```

---

### __multiplication__

The ```.multiply()``` method performs multiplication between values in corresponding pixels of two rasters. The order does not matter here. Masked pixels do matter and will remain masked. 

Multiplication is often used with a boolean raster as a method to __erase__ values in another image, because 0 will convert to 0 and 1 will retain the original value.   

![local-overlay-operations](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/multiply.png)


```js

var image_A_subtract_B = image_A.multiply(image_B);

```

--- 

### __division__  

The ```.divide()``` method performs division between values in corresponding pixels of the two rasters. The order does matter here because you divide the values in image_A by the values in image_B. Masked pixels in either image again remain masked in the output.  

![local-overlay-operations](https://geography.middlebury.edu/howarth/ee_edu/eePatterns/localOperations/divide.png)


```js
var image_A_divide_B = image_A.divide(image_B);

```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>