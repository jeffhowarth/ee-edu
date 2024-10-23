__PATTERNS__  

# __*RGB composites*__  

## __additive color system__ 

RGB composites use additive color to display raster data values in three bands at once. 

_More soon._

---  

<!-- Before we get into the code, we should step back and think about why an image will often contain more than one band, why we would want to display the data in more than one band at once, and how additive color works as a system for comparing three data values.  

## __display multiple conditions at locations__ 

Let's say that you wanted to map the population of four zones at three different moments in time.

In a vector model, you could do this with multiple __columns__ in a table.

![vector-model][]  

In a raster model you could do this with multiple __bands__ in an image.

![raster-model][]  

The main idea is that _bands in an image function like columns in a table_; they allow you to describe multiple attributes for locations. 

Now let's say that you want to visualize change in these three conditions. If you made charts for each zone, it would look something like this: 

![three-band-charts][]  

Displaying these charts as a single map layer is tricky if you get stuck thinking about a map layer as something that displays data values with a single palette.  

When you think in additive color, the problem becomes quite simple.  

![as-additive-color][] 

Here is how additive color works:

* there are three color channels: Red, Green, and Blue 
* the values of a single band are displayed in one color channel  
* the three color channels combine to create a color displayed on the monitor.  

---   -->

Use the RGB mixer below to create the colors by adding values in Red, Green, and Blue channels.  

<iframe
  src="https://jhowarth.users.earthengine.app/view/ee-edu-rgb"
  style="width:910px; height:576px;"
></iframe>

[_Open app in new browser window_](https://jhowarth.users.earthengine.app/view/ee-edu-rgb){target=_blank}  

---  

Here is the key for primary and secondary additive colors.  

![Additive color](https://geography.middlebury.edu/howarth/ee_edu/RGB_alt3.png)  




## __RGB viz__  

The basic pattern to visualize __multi-band images__ as a combination of red, green, and blue channels:

```js
var rgb_viz = 
    {
        bands:  ['red', 'green', 'blue'],      
        min:    [0, 0, 0],        
        max: [255, 255, 255]    
    }
;
```


---

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivs 4.0 International License</a>.
