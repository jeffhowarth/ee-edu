# __map vector layers__  

Earth Engine is primarily a tool for visualizing raster data. This means two things:  

* you can choose a color to display vector data, but not much else;
* if you want to control more than just the color, you will need to convert your vector data into an image. 

---  

## __simple viz with color__  

Similar to raster data, you use the ```Map.addLayer()``` method to display a feature collection as a map layer. This method takes the same five data objects [described previously](map-raster-layers.md#add-map-layer), but the viz dictionary here is much simpler: it can only contain a ```color``` key. Because of this, I usually write the dictionary directly into the statement.    

```js  
Map.addLayer(fc, {color: 'white'}, "Layer Name");

```

---  

## __:earth_americas: paint strokes without fill__  

Sometimes it is helpful to draw just the outlines (strokes) of features on a map, leaving the fills (interiors) completely transparent. This is particularly helpful with cadastre (property) lines and other boundaries of human geography.  

The method below allows you to paint the strokes of features in a collection with a color and weight (thickness) of your choice and store the output as an RGB image. (An RGB image has three bands that combine to make colors).  

You can then add the rgb image to the map as a layer, using empty curly brackets ```{}``` as a placeholder for the viz dictionary. You do not need to define the viz parameters because the data type is a byte (0-255) and Earth Engine will display the three bands (red, green, blue) correctly by default.  

```js
var strokes = geo.fcCart.paintStrokes(fc, "white", 0.5);

Map.addLayer(strokes, {}, "Feature outlines");
```

If you then add the ```strokes``` layer on top of the other layers on the Map, you will be able to see the underlying layer through the transparent interiors of the features in the collection.  

---   

## __paint nominal values with colors__  

If you have a feature collection with nominal data (classes, categories) and you would like to display each class with a unique color, then this pattern should work:

<center>

``` mermaid
graph LR

  step01("Convert fc to nominal image") ;
  step02("Display image as layer") ;

  step01 --> step02


  classDef task fill:#C9C3E6,stroke-width:0px,color:#000000 ;
  
  class step01 task; 
  class step02 task;

```

</center>


---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>