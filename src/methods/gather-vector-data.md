# __gather vector data__  

Points, polylines, and polygons, oh my.  

_more forthcoming_  

## __accessing data from cloud__ 

The general pattern for acquiring vector data from the cloud is quite similar to the one for raster data.   

<center>

``` mermaid
graph LR

  step01("Construct from address") ;
  step02("Inspect data object") ;

  step01 --> step02

  classDef task fill:#C9C3E6,stroke-width:0px,color:#000000;
  
  class step01 task; 
  class step02 task;

```

</center>


### __construct fc from address__    

```js

var fc = ee.FeatureCollection("address/of/cloud/data");

```

---  

### __inspect data__  

Working with vector data in Earth Engine can be a little challenging because you never really get to see the data as a table. You can, however, try to piece together the basic structure of the table by asking a set of questions about the data with the ```print()``` method.   

#### how many rows in table?  

This method will print the number of features in the collection to the Console, which is the same as the number of rows in a table. 

```js  
print(
  "fc size",
  fc.size()
);
```

It is often helpful to know how many features the collection contains at the start as a way to monitor the results of your filters in subsequent steps.  

---  

#### what is first row of table?

This method will print the first row of the table as a dictionary to the Console.  

```js
print(
  "fc first row",
  fc.first()
);
```

The keys of the dictionary are the column names of the table. The values in the dictionary are the values for the first row of the table. Often, the first row is arbitrary and you may not even know where this feature is in the world. But your goal here is to understand the __data schema__:  

* what are the column names that define the categories of attributes stored in the table?  
* what is the format of the column names and attribute values? Are they text or numbers? If text, are they all caps, title case, all lower?  

This information is usually quite helpful when you need to filter the collection in subsequent steps.  

---  

#### what are all unique values of a target column?

This method will print all the unique values for a target column that you specify with the "property_name" argument. You usually find the column name use the ```fc.first()``` method shown above.  

```js  
print(
  "FC unique values for target category",
  fc.aggregate_array('property_name').distinct().sort()
);
```

This information usually facilitates filter by attribute methods. (I often copy and paste attributes from this list to avoid typos).     

---  

### __full pattern__ 

Here is the full pattern for constructing and inspecting feature collections.  

```js
// Gather fc data from address.

var fc = ee.FeatureCollection("address/of/cloud/data");

// Inspect the table.  

print(
  "FC NAME",
  "number of rows:",
  fc.size(),
  "first row of table:",
  fc.first(),
  "unique values for target column:",
  fc.aggregate_array('column_name').distinct().sort()
);

```

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>