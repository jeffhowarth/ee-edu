# __geo module__

The geo module is a collection of methods that I am writing and packaging in a way that will allow you to use the methods without having to write them from scratch. 

I wrote these methods for two reasons:    

1. Each represents a recurring task of geospatial analysis that is supported by other geographic information systems (like QGIS or ArcGIS).

2. Each requires a chain of transformations to make in Earth Engine which can be conceptually confusing and technically difficult for novices to do.    

My hope is that providing ready-made methods may help you focus on how different methods of spatial analysis and cartography work conceptually in workflows without having to get bogged down in writing complicated task chains for common tools.  

---  

## __import module__  

__To use the module, create a container and require the module.__  

```js
var geo = require("users/jhowarth/eePatterns:modules/geo.js");

print("geo methods dictionary", geo.help);    // Prints dictionary of all tools in module.  
print("geo palettes", geo.iPalettes);         // Prints dictionary of all palettes in module. 
```

The code block above will import the module and print the module's help dictionary and palette dictionary to the Console. The help dictionary lists all methods and url links to their docs. The palette dictionary lists all palettes in the module. You only need to import the module once in a script that calls a method or palette from the module. I usually place the above code snippet near the top of my script (under the header).  

---  

## __docs in eePatterns__  

__A globe icon :earth_americas: identifies methods from module.__  

In the METHODS documentation, the :earth_americas: symbol identifies a method that requires the geo module. To use any of these methods, you will need to include the [import module](#import-module) in your script prior to calling the method. 

---  

## __peak under hood__

__Add module to your READER tray if you want to see the underlying code to any method.__

The module only hides the code from you if you do not want to see it. If you would like to look under the hood, I have made the code for the module public and you can add it to the READER tray of the IDE by [__clicking here__](https://code.earthengine.google.com/?accept_repo=users/jhowarth/eePatterns){target=_blank}. 

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>
