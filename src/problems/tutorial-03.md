__TUTORIAL 3__

# _**Introduction to feature collections**_  

## __goal__  

This tutorial aims to introduce you to gathering, filtering, and displaying large __vector__ datasets in Earth Engine. Your goal is to work through the starter script and try to reproduce the layers that are shown in the app below.

---    

<iframe
  src="https://ee-patterns.projects.earthengine.app/view/tutorial-03"
  style="width:854px; height:854px"
></iframe>  

[_open app in new tab_](https://ee-patterns.projects.earthengine.app/view/tutorial-03){target=_blank}

---  

## __starter script__

```js
var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 

// ---------------------------------------------------------------------------
//  I. A SIMPLE FEATURE COLLECTION PATTERN
//
//  (1) Gather feature collection from "TIGER/2018/Counties".
//  (2) Note the number of rows in the table, the column names, and the first row of data.
//  (3) Also find all the unique county names in the county. How many are there?
//  (4) Display all the rows in the collection as a Map layer. Use {color: 'white'} 
// ---------------------------------------------------------------------------




// ---------------------------------------------------------------------------
//  II. FILTER BY ATTRIBUTE
//
//  (1) How may counties in the USA are named "Addison"?
//  (2) Display all counties named Addison in the USA on the Map with {color: 'gray'}.
// ---------------------------------------------------------------------------



// ---------------------------------------------------------------------------
//  III. FILTER BY LOCATION
//
//  (1) Use the geometry tool (upper left of Map) to create a point somewhere inside Addison County, Vermont.
//  (2) Filter the original feature collection by location using this poi. 
//  (3) Display the result (Addison county filtered by poi) on the Map with {color: 'black'}.
// ---------------------------------------------------------------------------




// ---------------------------------------------------------------------------
//  IV. FILTER BY MULTIPLE ATTRIBUTES.
//  
//  (1) Filter the original collection for "Orange" county.
//  (2) How many Orange counties are in the USA?
//  (3) Display the result (All counties named 'Orange') on map as layer with {color: 'orange'}.

//  (4) Use AND filter to filter the original collection of counties for "Orange" county IN VERMONT.
//  HINT: the STATEFP column stores strings (even through they look like numbers).
//  (5) Display the result as a layer on the Map with {color: 'OrangeRed'}.
// ---------------------------------------------------------------------------




// ---------------------------------------------------------------------------
//  V. FILTER BY ATTRIBUTE AND LOCATION
//
//  (1) Construct a new feature collection from "TIGER/2018/States".
//  (2) Filter collection for Vermont.
//  (3) Center Map on Vermont. 
//  (4) Add Vermont layer to Map with {color: 'green'}
//  (5) Filter original county collection by name "Orange" and use a FILTER BY LOCATION to filter in bounds of Vermont state.
//  (6) Display result on map with {color: "LightGreen"}
// ---------------------------------------------------------------------------




// ---------------------------------------------------------------------------
//  VI. FILTER BY ATTRIBUTE AND LOCATION: TRICKY CASE
//  
//  (1) Try to reproduce last workflow (FILTER BY ATTRIBUTE AND FILTER BY LOCATION) to map "Essex" county in Vermont.
//  (2) How did it work? What do you think happened?
//  (3) Can you fix it with a workflow that does not use AND but still links together
//    (A) a FILTER BY ATTRIBUTE with 
//    (B) a SPATIAL FILTER  
//  (4) Display the fixed result as a layer to the map with {color: 'magenta'}.
// ---------------------------------------------------------------------------



// ---------------------------------------------------------------------------
//  VII. FIRST CHALLENGE 
//
//  (1) How could you select all the counties in Vermont using a FILTER BY ATTRIBUTE workflow?
//  (2) After you filter the data, add the result  {color: "PowderBlue"}
// ---------------------------------------------------------------------------



// ---------------------------------------------------------------------------
//  VIII. SECOND CHALLENGE
//
//  (1) How could you select all the counties in Vermont using a FILTER BY LOCATION workflow?
//  (2) After you filter the data, add the result  {color: "DeepSkyBlue"}
// ---------------------------------------------------------------------------



// ---------------------------------------------------------------------------
//  IX. FINAL TASK
//  
//  (1) Convert one of the counties in Vermont dataset (VII or VIII) to nominal image 
//  (2) Display each county in a unique color.
// ---------------------------------------------------------------------------



```

## __checks in starter__ 

Here are some checks that you can print to Console for sections I - V.  

| SECTION | DESCRIPTION                 | CHECKS            |
| :--:    | :--                         | :--               |
| I-2     | Number of rows in table.    | 3233              |  
| I-2     | Column names                | 18 of them, beginning with GEOID and ending with METDIVFP   |
| I-2     | First row of table          | id: 00000000000000000011; geometry: Polygon, 656 vertices; properties: 17  |  
| I-3     | Unique county names         | 1922 of them      |  
| II-1    | Number of rows in table     | 1                 |
| III-2   | Number of rows in table     | 1                 |  
| IV-2    | Number of rows in table     | 8                 |  
| V       | Number of rows in table (states)    | 56          |  

For sections VI - IX, you should be able to check your work by visually comparing your map layers to the ones shown in the app above.  

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>