# __explain code__

Always write your code for two main audiences: 

1. a __computer__ that will compile and execute your code;
2. a __person__ who will read your code and try to make sense of it. 

The second audience may be yourself in the future, when you return to a script that you wrote after some time has passed. It may be an instructor in this course who wants to help you troubleshoot something in your script that is not working. Or it may be someone you have never met who is looking to adapt and recycle parts of your script for a slightly different purpose. Whoever the reader may be, you should always aim to help people read your code by placing explanations directly in your workflow. 

The patterns below describe different ways to explain your code and make it more readable for a human audience. 

## __script header__

 __Write a header at the top of your script.__

At a minimum, the header should identify who wrote the script, when they wrote it, and why they wrote it. This is also where many authors will define the license for the script.  

I usually include a couple lines of repeating symbols to visually block the header and separate it from the rest of the script.  

```js
/*    
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

    AUTHOR:   
    DATE:     
    TITLE:  

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
*/

```

## __task description__

__Write a line comment before each major task in your workflow.__

Describe what you are doing or why you are doing it. Use full sentences and correct punctuation (start each comment with a capital letter and end each comment with a period).  

I usually include a line of repeating symbols above and below the task description to help visually separate the code into discrete chunks.  

```js
// -------------------------------------------------------------
//  To illustrate a task description.
// -------------------------------------------------------------
```

[script header]: ../patterns/explain-code.md#script-header
[task description]: ../patterns/explain-code.md#task-description

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>