__SOLUTIONS__

# __*Error Glossary*__  

This page shows some error messages that you may receive while using Earth Engine and provides some tips on how you might be able to resolve them.  

## __geometry errors__  

The error message indicates a problem with the .geometry of an object.  

### __collection.geometry__  

![geom1] 

EE complains because you are asking it to do too much. The proximate cause is likely from a collection that you are using as an input to an operation. If the step that made this collection was a filter, then check to make sure the filter worked as you thought it would.  

_Make self checks a habit; at each step of a problem, check your results to see if they match what you think they should be._  



## __invalid type__  

The error message indicates a problem with the data type associated with a data object.  

### __Feature, argument 'geometry'__  

![iType]  

EE complains because you are asking it to do something with the wrong kind of thing. This happens when you try to use a method with arguments of the wrong data type. In the above example, the method expected a feature's geometry but found an image.  

Fixing these problems often requires tracing back several steps. In the above example, EE threw the error when it was asked to display a Map layer, but the ```Map.addLayer()``` did not cause the error. Rather, the cause occurred a step of two earlier when EE was asked to use a method with an argument of the wrong type.    

_Check each output you get from an operation by printing the result to the Console. This will help you identify if the operation worked before you go too far downstream._  

---  

[geom1]: http://geography.middlebury.edu/howarth/ee_edu/eePatterns/errorGlossary/geometry-too-many-vertices.png
[iType]: http://geography.middlebury.edu/howarth/ee_edu/eePatterns/errorGlossary/invalid-type-01.png

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>
