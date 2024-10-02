# __documentation key__  



``` mermaid
graph LR

      input[INPUT]:::raster
      method("<b>.method()<b>"):::method 
      output[OUTPUT]:::raster  
      input --> method --> output

    subgraph ARGUMENTS[" "]
      arg["argument 1"]:::raster
    end

    ARGUMENTS:::arg --o method



  classDef fc fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  classDef raster color:#000000,fill:#d9d9d9,stroke-width:12px,stroke:#d9d9d9
  classDef vector color:#5A660A,fill:#DEE6AC,stroke-width:0px,stroke:#DEE6AC
  classDef string color:#660A2A,fill:#E6ACC0,stroke-width:0px
  classDef number color:#0A2366,fill:#ACBCE6,stroke-width:0px
  classDef list color:#664C0A,fill:#E6D5AC,stroke-width:0px
  classDef dict color:#662F0A,fill:#E6C3AC,stroke-width:0px
  classDef method color:#230A66,fill:#BBACE6,stroke-width:0px
  classDef arg color:#230A66,fill:#BBACE600,stroke-width:4px,stroke:#BBACE6
```

## __data types__  

The pictures below illustrate the colors and shapes of nodes in the pattern flow diagrams.  

---  

``` mermaid
graph LR

  i[this is an image]:::raster 
  ic{this is an\n image collection}:::raster 

  f([this is feature]):::vector 
  fc((this is a\n feature collection)):::vector

  s{{this is a string}}:::string
  n{{this is a number}}:::number
  l{{this is a list}}:::list
  d{{this is a dictionary}}:::dict


  classDef raster color:#000000,fill:#d9d9d9,stroke-width:12px,stroke:#d9d9d9
  classDef vector color:#5A660A,fill:#DEE6AC,stroke-width:0px,stroke:#DEE6AC
  classDef string color:#660A2A,fill:#E6ACC0,stroke-width:0px
  classDef number color:#0A2366,fill:#ACBCE6,stroke-width:0px
  classDef list color:#664C0A,fill:#E6D5AC,stroke-width:0px
  classDef dict color:#662F0A,fill:#E6C3AC,stroke-width:0px
  classDef method color:#230A66,fill:#BBACE6,stroke-width:0px


```

---  
