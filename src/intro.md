# __introduction__  

This book aims to help you create __geospatial workflows__ with Google Earth Engine.  

In general, these workflows grab geographic data stored in the cloud, alter it (with purpose), and then visualize the results as map layers.  

<center>

``` mermaid
graph LR
  step01[("GEOGRAPHIC\nDATA\n\n stored in cloud")] ;
  step02>"GEOSPATIAL WORKFLOW\n\n alter and visualize"] ;

  step01 --> step02

  classDef store fill:#4AA8A0,stroke-width:0px,color:#FFFFFF; 
  classDef transform fill:#4A92A8,stroke-width:0px,color:#FFFFFF;

  class step01 store; 
  class step02 transform;

 
```

</center>

To do this, we will use a web-based Integrated Development Environment (IDE) for the Earth Engine Javascript Application Programming Interface (API). That is a mouthful, but in practical terms it means that __we will create workflows by writing scripts with javascript__.   

## __data transformation__   

The basic element of all geospatial workflows is a three step process that Waldo Tobler called a __cartographic transformation__: you start with geographic data in a certain state (input), you do something to alter the data (method), and you store the result (output). Often but not always, one or more options (arguments) constrain how a method alters the input.   

<center>

``` mermaid
graph LR

  input["INPUT"] ;
  method("METHOD") ;
  output[/"OUTPUT"/]  ;

  input --> method --> output
  
  arg["argument"] ;
  
  arg --o method

  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class input in-out; 
  class method op;
  class output in-out;
  class arg arg; 
```

</center>

## __statements__

With JavaScript, we transform geographic data by writing a __statement__. The syntax generally takes this form:

```js

var output = input.method(argument);

```

The general pattern is that you start by defining a name for a container that you would like to make so that you can store the output. This container of data is called a __variable__ that you create with the keyword ```var```. You then say that this container will contain ```=``` what results from taking the input and applying a method to it ```.``` with one or more arguments ```()```. A semicolon ```;``` punctuates a statement like a period (or wink :wink:).  

## __task tree__

Workflows are a means to achieving an end. When you sit down to write a workflow, you have some goal state for the data in mind. Your problem is to figure out how to change the data from their original condition to the goal state in your head.  

Most workflows can be decomposed into a __task tree__: at the top, a (big) problem  may be broken down into a sequence of smaller tasks, each of these tasks may be broken down into smaller subtasks.    


``` mermaid
graph TD

  L01("PROBLEM") ;
  L11["TASK 1"] ;
  L12["TASK 2"] ;
  L21["SUBTASK 1"] ;
  L22["SUBTASK 2"] ;
  L23["SUBTASK 3"] ;
  L24["SUBTASK 4"] ;

  L01 --- L11 
  L01 --- L12
  L11 --- L21
  L11 --- L22
  L12 --- L23
  L12 --- L24

  classDef L0 fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef L1 fill:#CCCCCC,stroke-width:0px,color:#000000;
  classDef L2 fill:#000000,stroke-width:0px,color:#FFFFFF;  

  class L01 L0; 
  class L11 L1;
  class L12 L1;
  class L21 L2;
  class L22 L2;
  class L23 L2;
  class L24 L2;

 
```


</center>


## __task chain__  

The lowest branches of the tree are individual transformations, the foundational elements of a workflow. Higher branches of the tree often require linking together two or more transformations as a __task chain__, where the output of one transformation becomes the input of another. 

<center>

``` mermaid
graph LR
  step01("INPUT") ;
  step02["METHOD"] ;
  step03("OUTPUT")  ;
  step04["METHOD_2"] ;
  step05("OUTPUT_2")  ;
  arg01("argument") ;
  arg02("argument_2") ;

  step01 --> step02 --> step03 --> step04 --> step05
  arg01 --- step02
  arg02 --- step04


  classDef in-out fill:#FFFFFF,stroke-width:1px,stroke: #000000, color:#000000; 
  classDef op fill:#000000,stroke-width:0px,color:#FFFFFF;
  classDef arg fill:#CCCCCC,stroke-width:0px,color:#000000;
  

  class step01 in-out; 
  class step02 op;
  class step03 in-out;
  class step04 op;
  class step05 in-out;
  class arg01 arg;
  class arg02 arg;

 
```

</center>

## __summary__

If this all sounds a bit wonky, do not worry too much. We will get to examples that illustrate all of this soon. For now, I just want you to know:  

1. a workflow is a chain of input-method-output transformations 
2. you can think of a workflow visually (as a flow diagram) and verbally (as javascript).  
3. visually, a workflow contains a vertical hierarchy of purpose (task tree) and a horizontal sequence of transformations (task chains). 

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>