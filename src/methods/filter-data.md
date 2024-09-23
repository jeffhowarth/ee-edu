# __filter data__  

_more forthcoming_  

## __filter FC by attribute__  

---  

### filter by attribute 

```js
var fc_filtered = fc.filter(
  ee.Filter.eq('column_name', 'attribute'))
;
```

---  

### check filter results

```js
print(
  "FC SIZE BEFORE VS AFTER FILTER",
  fc.size(),
  fc_filtered.size()
);

```

---  

### full pattern  

```js
// Filter by attribute  

var fc_filtered = fc.filter(
  ee.Filter.eq('column_name', 'attribute_value'))
;

// Check filtered result.  

print(
  "FC SIZE BEFORE VS AFTER FILTER",
  fc.size(),
  fc_filtered.size()
);

// Add filtered data to map.  

Map.addLayer(fc_filtered, {color: 'cyan'}, "FC filtered by attribute");

```

---

## __filter FC by location__  

---

### make geometry object for POI

Use the geometry tools in the upper-left of Map to create a point of interest (POI).  

---  

###  filter by intersection with POI.

```js
var fc_intersect_poi = fc.filter(
    ee.Filter.bounds(geometry)
);

```

---  

### check filter results  

```js
print(
  "FC SIZE BEFORE VS AFTER FILTER",
  fc.size(),
  fc_intersect_poi.size()
);
```

---  

### full pattern  

```js
// Filter by location (intersection with poi).

var fc_intersect_poi = fc.filter(
    ee.Filter.bounds(geometry)
);

// Check filtered result.  

print(
  "FC SIZE BEFORE VS AFTER FILTER",
  fc.size(),
  fc_intersect_poi.size()
);

// Add filtered data to map.

Map.addLayer(fc_intersect_poi, {color: 'magenta'}, "FC filtered by location");  

```

---  

## __filter FC by multiple criteria__    

---  

### AND filter  

```js
var fc_filter_and = fc.filter(
  ee.Filter.and(
    ee.Filter.eq("column_name", "attribute_value"),
    ee.Filter.eq("column_name2", "attribute_value")
  )
);
```

---

### check filter results  

```js
print(
  "FC SIZE BEFORE VS AFTER 'AND' FILTER",
  fc.size(),
  fc_filter_and.size()
);
```

---  

### full pattern  

```js

// Filter for attributes in two or more columns.  

var fc_filter_and = fc.filter(
  ee.Filter.and(
    ee.Filter.eq("column_name", "attribute_value"),
    ee.Filter.eq("column_name2", "attribute_value")
  )
);

// Check results of the filter.  

print(
  "FC SIZE BEFORE VS AFTER 'AND' FILTER",
  fc.size(),
  fc_filter_and.size()
);

// Add result as layer to Map

Map.addLayer(fc_filter_and, {color: 'OrangeRed'}, "FC filtered with AND");
```

---   

## __filter FC by spatial relationships__    

### :earth_americas: spatial filters  

This is a custom method that allows you to filter features in one collection (figure) based on their spatial relationship to features in another collection (ground).     

```js

var fc_in_ground = geo.fcFilter.spatial('spatialRelationship', figure, ground);

```

You may choose one of three spatial relationships.  

| SPATIAL RELATIONSHIP  | DESCRIPTION                                                                   |
| --:                   | :--                                                                           |
| "containedIn"         | Returns features in figure collection that are contained by features in the ground collection.    |
| "disjoint"            | Returns features in figure collection that do not touch any features in ground collection.        |  
| "intersects"          | Returns features in figure collection that touch a feature in ground collection.


---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>