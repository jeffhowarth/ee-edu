# __import assets__  

## Import shapefile  

The video below shows you how to import a shapefile into Earth Engine. In the example shown, the shapefile lacks a .prj file, which often happens in whitebox models, so the worked example involves defining the shapefile's projection prior to importing. If you do not upload a .prj file with your shapefile, Earth Engine will assume the coordinates reference WGS84 and this can cause alignment issues.  

---  

<iframe width="720" height="405" src="https://www.youtube.com/embed/DQPZtRUPL5M?si=yrXeOEvYb4wM8bd7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>  

---

## Import raster  

The video below shows you how to import a raster into Earth Engine. The example shows how to import a raster of discrete integer values, which requires the modal method for making pyramids. For continuous values (elevation, slope, hillshade, etc), you should use the mean method. 

---  

<center>

![Pyramid structure](https://developers.google.com/static/earth-engine/images/Pyramids.png)  

</center>  

---  

<iframe width="720" height="405" src="https://www.youtube.com/embed/7iyqFRlCP-U?si=74tcrFHbmcWP_bYI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---  
