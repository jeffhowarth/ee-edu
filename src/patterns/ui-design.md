__PATTERNS__  

# __*user interface design*__  

## __wipe map with side bar layout__  

The patterns below provide a template for a wipe map with a side bar for title, subtitle, documentation, and credits. 

### __make layout__  

```js
// Initialize side bar.

var side_bar = ui.Panel({
  layout: ui.Panel.Layout.flow('vertical'),
  style: {width: "20%"}
});

// Initialize two new maps.

var left_Map = ui.Map();
var right_Map = ui.Map();

// Initialize wipe map with left and right maps.

var wipe_map = ui.SplitPanel(        // Initialize split panel.
  left_Map,                             // Put on left side of panel.
  right_Map,                            // Put on right side of panel.
  'horizontal',                         // Arrange split in horizontal direction.
  true                                  // Make a WIPE transition.
  )
;

// Link maps together.

ui.Map.Linker([
    left_Map, 
    right_Map
  ])
;

// Initialize a panel to hold wipe map.

var wipe_map_panel = ui.Panel(
  {
    widgets: [wipe_map]
  });

// Initialize layout with side bar and wipe map

var layout = ui.SplitPanel(
  {
    firstPanel: side_bar,
    secondPanel: wipe_map_panel, 
    orientation: 'horizontal',
    wipe: false
  }
);

// Add layout to root. 

ui.root.clear();
ui.root.setLayout(ui.Panel.Layout.flow('horizontal'));
ui.root.add(layout);

```

---  


### __add labels for maps__  

```js


// -------------------------------------------------------------
//  Make left and right map labels.
// -------------------------------------------------------------

var style_label_map = 
  {
    fontSize: '18px',
    fontWeight: 'bold',
    fontFamily: 'Helvetica, sans-serif',
  }
;

var label_map_left = ui.Label({
  value: 'label for left map',
  style: style_label_map,
  }
);

label_map_left.style().set({
  position: 'bottom-left',
});

var label_map_right = ui.Label({
  value: 'label for right map',
  style: style_label_map,
  }
);

label_map_right.style().set({
  position: 'bottom-right',
});

left_Map.add(label_map_left);
right_Map.add(label_map_right);

```

### __add title__ 

```js
// -------------------------------------------------------------
//  Add Title
// -------------------------------------------------------------

var style_title = 
  {
    fontSize: '24px',
    fontWeight: 'bold',
    fontFamily: 'Helvetica, sans-serif',
    whiteSpace: 'wrap'
  }
;

var title = ui.Label({
  value: "Layout title",
  style: style_title,
  }
);

side_bar.add(title);

```

---  

### __add subtitle__  

```js

// -------------------------------------------------------------
//  Add Subtitle
// -------------------------------------------------------------

var style_subtitle = 
  {
    fontSize: '18px',
    fontWeight: 'bold',
    fontFamily: 'Helvetica, sans-serif',
    color: 'OliveDrab',
    whiteSpace: 'pre'
  }
;

var subtitle = ui.Label({
  value: "Place\n(start-end)",
  style: style_subtitle,
  }
);

side_bar.add(subtitle);


```

### __add documentation__   

```js  

// -------------------------------------------------------------
//  Add documentation.
// -------------------------------------------------------------

var style_docs = 
  {
    fontSize: '12px',
    fontFamily: 'Helvetica, sans-serif',
    position: 'bottom-right'
  }
;

var docs = ui.Label({
  value: 'more information',
  style: style_docs,
  targetUrl: 'link to google doc'       // Change sharing to "Anyone with the link"
  }
);

side_bar.add(docs);

```

---  

### __add credits__  

```js

// -------------------------------------------------------------
//  Add credits 
// -------------------------------------------------------------

var style_credits = 
  {
    fontSize: '10px',
    fontFamily: 'Helvetica, sans-serif',
    position: 'bottom-right'
  }
;

var credits = ui.Label({
  value: 'Your Name',
  style: style_credits,
  targetUrl: 'link to portfolio or online presence'
  }
);

side_bar.add(credits);


```

---

## __add interactivity__   

These patterns provide tools that allow the user to interact with the layout.  

---

### __select places of interest__  

```js
// -------------------------------------------------------------
//  Select places of interest
// -------------------------------------------------------------

//  Make dictionary of places of interest. 

var places = {
  
// "Place name": [longitude, latitude, zoom]
  "Atwater Lot": [-73.17655, 44.01282, 18],
  "Full Extent": [-73.17661, 44.01243, 14],

};

var select = ui.Select({
  items: Object.keys(places),
  placeholder: "Choose a location",
  onChange: function(key) {
    
    // This will recenter the map to the place of interest. 
    
    left_Map.setCenter(places[key][0], places[key][1], places[key][2]);
    
  }
});

// Add the widget to the side bar.

side_bar.add(select);

```

---  

### __layer visibility checkbox__  

```js
// -------------------------------------------------------------
//  Checkbox for layer visibility.
// -------------------------------------------------------------

// Initialize a checkbox with a label and check the box by default. 

var checkbox = ui.Checkbox('Label', true);

// Define what happens when you check the box. 

checkbox.onChange(function(checked) {
  
  // Show or hide the first map layer (controlled by index) based on the checkbox's value.
  
  left_Map.layers().get(0).setShown(checked);
  right_Map.layers().get(0).setShown(checked);
});

// Add the checkbox to the side panel.  

side_bar.add(checkbox);

```




---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>