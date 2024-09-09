## sum the values in a table column    

```js
// -------------------------------------------------------------
//  SUM THE VALUES IN A TABLE COLUMN (FC PROPERTY) 

//  Input must be a feature collection.
//  Replace 'PROPERTY' with the property name (STRING) to sum.  
//  Output is a number object.
// -------------------------------------------------------------

```

```js

var answer = input.aggregate_sum('PROPERTY');

// Print results to console.  

print(
  'ANSWER',
  answer,                 //  This will report the answer with eleven decimal places.
  answer.round()          //  This will round to nearest integer.
);

// -------------------------------------------------------------

```

---  

## dissolve features in collection by property  

```js

// -------------------------------------------------------------
//  DISSOLVE FEATURES IN COLLECTION BY PROPERTY. 

//  Input must be a feature collection.
//  Replace 'PROPERTY' with the property name to dissolve features.  
//  Output is a feature collection (with singlepart and multipart features),
//  where each feature represents the region of a unique property value. 
// -------------------------------------------------------------

```

```js
var output = t.dissolveByProperty(input, 'PROPERTY');

// -------------------------------------------------------------

```

You can access the underlying code for this function in the [tasks module][tasks-module]{target=_blank}. 

### practical tip  

If you would like to dissolve all features in a collection (produce one multipart feature from a collection) without distinguishing subclasses based on a property in the function, then first run this snippet to add a property to all features that holds the same value.

```js
//  Give all features in collection a new property with the same value. 

var prep = input.map(function(f){return f.set('tag', 1)});  

```  

Then use ```prep``` as input and ```'tag'``` as property.    

---

[sum-table]: ../methods/aggregate-table.md#sum-the-values-in-a-table-column  
[dissolve-by-prop]: ../methods/aggregate-table.md#dissolve-features-in-collection-by-property  

[tasks-module]: https://code.earthengine.google.com/?accept_repo=users/jhowarth/public  