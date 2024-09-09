# __cartography layout__  

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

