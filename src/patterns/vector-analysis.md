# __vector analysis__  

_forthcoming_

---   

## __transform geometries__  

These methods create new geometries based on the input geometries of feature collections.  

_More to come._

### __:earth_americas: bounding box__ 

---  

```js
var fc_bounds = geo.fcGeometry.boundingBox(fc);

Map.addLayer(fc_bounds, {color: 'cyan'}, "Bounding box", false);

```

---  

### __:earth_americas: centroid__  

---  

```js
var fc_centroid = geo.fcGeometry.centroidPoint(fc);

Map.addLayer(fc_centroid, {color: 'yellow'}, "Centroid point", false);

```

---  

### __:earth_americas: convex hull__   

--- 

```js
var fc_convex_hull = geo.fcGeometry.convexHullPolygon(fc);

Map.addLayer(fc_convex_hull, {color: 'magenta'}, "Convex hull", false);

```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>