# __customize Map__  

It is often helpful to customize the Map so that it centers and zooms on your area of interest and uses a base map that supports your purpose.  

The diagram below shows a general pattern.

<center>

``` mermaid
graph LR

  step01("Set map center and zoom") ;
  step02("Set base map style") ;

  step01 --> step02

  classDef task fill:#C3C8E6,stroke-width:0px,color:#000000;
  
  class step01 task; 
  class step02 task;

```

</center>

It is good practice to set the map center and zoom level before setting the base map so that the base map does not need to redraw.

## __set map center and zoom__  

__Use a data object to center the map and to suggest an appropriate zoom level.__  

```js
Map.centerObject(
    image,              // data object
    16                  // zoom level
);
```

## __set basemap style__  

__Select a basemap that provides the most helpful reference information from your data.__  

```js
Map.setOptions("HYBRID");
```

Choose from the following options: 

```js
"ROADMAP" 
```
```js   
"SATELLITE" 
```
```js
"HYBRID"
```
```js 
"TERRAIN" 
```

