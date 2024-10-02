# __export data__  

Earth Engine does not permanently store the data objects that you make in your workflows unless you specifically ask it to do so. The patterns below deal with two different scenarios:  

1. exporting data to a cloud asset
2. exporting data to a cloud drive

---  

## __to cloud asset__  

Whenever you pan your Map or zoom in and out of your Map, Earth Engine will run through all the steps required to make your data layers at the scale and extent that you are requesting.  

Because of this, it is common to get to the point in a workflow where two things happen:  

1. Earth Engine starts to balk at the amount of work you are asking it to do and throws __time out__ or __tile__ errors.  

2. You get impatient waiting for Earth Engine to process a long workflow just to zoom in and out and pan around your map. (When the slippy map gets sticky, it is like watching a game or movie that keeps buffering.)  

At this point, I tend to export my data as an asset so that I can just call the result directly. This is analogous to __saving a copy of your data__ in the cloud. The asset will have a cloud address that you can then use to gather the data back into your workflow with a constructor like ```ee.Image()```.   

Please note that when you export data as cloud assets, you are no longer storing it as a variable. So these patterns do not begin by declaring a variable. They simply execute a function.   


### __export fc__   

This method will __create a task__ that will export a feature collection as a Google Earth Engine asset. You will need to go to the __task tab__ and run the task. When it is complete, you can access the asset through the __asset tab__. Open the asset (double-click) and then copy the asset id. You can then use this address in a [data gathering pattern](../patterns/gather-vector-data.md#accessing-data-from-cloud) for vector data.

```js
geo.fcExport.toCloudAsset(fc, "asset_name");

```

---  

<center>

| ARGUMENT              | DESCRIPTION           |
| :--                   | :--                   |
| __fc__                | A feature collection to export.  |
| __"asset_name"__      | A name for the asset. |

</center>

---  

### __export image__  

This method will __create a task__ that will export an image as a Google Earth Engine asset. You again will need to go to the __task tab__ and run the task. When it is complete, you can access the asset through the __asset tab__. Open the asset (double-click) and then copy the asset id. You can then use this address in a [data gathering pattern](../patterns/gather-raster-data.md/#accessing-images-from-cloud) for raster data.


```js
geo.iExport.toCloudAsset(
  image, 
  "asset_name",
  extent, 
  "pyramiding"
);

```

---  

<center>

| ARGUMENT                  | DESCRIPTION           |
| :--                       | :--                   |
| __image__                 | An image to export.   |
| __"asset_name"__          | A name for the asset. |  
| __extent__                | The area of interest or study region to define the bounds of the image. |  
| "pyramiding"              | The method for generating pyramid layers to display in slippy map. Use "mode" for boolean, categorical, and object rasters and "mean" for field rasters.  |  

</center>

---  

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>