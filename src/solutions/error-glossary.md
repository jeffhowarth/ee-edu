__SOLUTIONS__

# __*Error Glossary*__  

This page shows some error messages that you may receive while using Earth Engine and provides some tips on how you might be able to resolve them.  

## __geometry errors__  

The error message indicates a problem with the .geometry of an object.  

### __collection.geometry__  

![geom1] 

EE complains because you are asking it to do too much. The proximate cause is likely from a collection that you are using as an input to an operation. If the step that made this collection was a filter, then check to make sure the filter worked as you thought it would.  

_Make self checks a habit; at each step of a problem, check your results to see if they match what you think they should be._  

[geom1]: http://geography.middlebury.edu/howarth/ee_edu/eePatterns/errorGlossary/geometry-too-many-vertices.png


