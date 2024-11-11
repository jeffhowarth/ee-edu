__TUTORIAL 09__  

# __*spectral indices*__ 

## __goal__  

This tutorial introduces spectral indices, or calculations made with local operations that compare two or more spectral bands. Additionally, this tutorial introduces a method to reclassify spectral indices with user-defined breaks to make nominal images of landcover.    

Your practical goal is to solve the two problems described below. The first we will walk through in lecture. The second you will do either alone or with a buddy or two during lab.  

## __deliverables__  

By <mark>5pm on November 11</mark>, please complete the __Tutorial 09 checkup__ on Canvas. To receive credit for this tutorial, you must submit links to your scripts (and accomplish all prompts listed below). You must also thoughtfully respond to the check-up prompts to briefly critique your results for both problems. Please note that this check-up will be manually graded, so you will only be able to submit it once.  

## __NDVI problem__  

Please use Landsat 9 to make a map of New York City that accomplishes the following: 

1. Filters the image collection for:
    1. a poi in New York City,
    2. the years 2022 - 2024,
    3. the months of July and August,
    4. with less than 20% cloud cover,
    5. with cloudy pixels masked.
2. Flattens the collection to the median image. 
3. Displays the median image with two different false color composites:
    1. A NIR, Red, Green composite.
    2. A SWIR2, NIR, Green composite.  
4. Calculates the NDVI of the median image. 
5. Displays the NDVI band with the divergent color scheme ```palette_ndvi``` defined below.
6. Reclassifies the NDVI band with user-defined thresholds to distinguish five classes:  
    1. Water
    2. Impervious or bare
    3. Sparse and/or stressed vegetation
    4. Moderately healthy vegetation  
    5. Dense and/or healthy vegetation  
7. Adds the reclassified layer to the Map and displays with nominal palette scheme ```palette_reclass``` defined below.
8. Adds legends to the map for both NDVI layer and reclassified NDVI layer.  

```js

// Palette helpers. 

var palette_ndvi = ['purple', 'white', 'green'])
var palette_reclass = ["PaleTurquoise", "White", "Gold", "YellowGreen", "OliveDrab"]
```

## __NBR problem__  

Please use Landsat 9 to make a map of the Quebec wildfire scars from the summer of 2023. Your map should accomplish the following:

1. Filters the image collection for:
    1. a poi on "Nutimesanu, QC, Canada",
    2. the year 2023,
    3. the months of August and September,
    4. with less than 20% cloud cover,
    5. with cloudy pixels masked.
2. Flattens the collection to the median image. 
3. Displays the median image with two different false color composites:
    1. A NIR, Red, Green composite.
    2. A SWIR2, NIR, Green composite.  
4. Calculates the NBR of the median image. 
5. Displays the NBR band with the divergent color scheme ```palette_ndvi``` defined below.
6. Reclassifies the NBR band with user-defined thresholds to distinguish three classes:  
    1. Water
    2. Burn scar
    3. Not burned 
7. Adds the reclassified layer to the Map and displays with nominal palette scheme ```palette_reclass``` defined below.
8. Adds legends to the map for both NBR layer and reclassified NBR layer.  

```js

// Palette helpers. 

var palette_nbr = ['purple', 'white', 'green'])
var palette_reclass = ["LightSkyBlue", "DarkOrchid", "YellowGreen"]
```