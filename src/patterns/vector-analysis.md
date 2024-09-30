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

