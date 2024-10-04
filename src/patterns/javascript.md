__PATTERNS__

# _**JavaScript**_  

Here are some basic patterns for writing in JavaScript.

## __comments__  

__Use comments to explain your code.__

```js
// Line comments start with two forward slashes. Like this line. 

/* Multi-line comments start with a forward slash and a star,
and end with a star and a forward slash. */ 

```

## __variables__

__Use variables to contain (hold, store) data.__  

```js
// Write a statement using the keyword var.

var hello = 'Hello world';    

// Statements should end in a semi-colon, or else the Code Editor complains.

var test = "I feel incomplete..."

// !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
// !! Variable names cannot contain spaces or - dashes - !!
// !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

// Use underscores to separate words in variable names.

var this_is_called_snake_case = 'Hello, snake!';

// Or use capitalizations to separate words:

var thisIsCalledCamelCase = 'Hello, camel!';

```

## __print to console__

__Use print function to print contents of variables and objects to console.__  

```js 
// Use parenthesis to pass arguments to print function.  

print(hello);

// Use commas to pass multiple arguments. 

print('Print test', hello);

```
## __strings__  

__Use strings to store text (character strings).__  

```js

// Use single quotes to define string.

var hello = 'Hello world!'  // This is a string. 

// You can also use double quotes to enclose string.

var obi_one = "Hello there";

// Just do not mix them.

var cranky = "Hello Newman';  // This will throw an error. You will need to match the quotation marks to fix it. 

```

A string has a set of methods that work with that type of data.

```js
// Use a period and parentheses to call a string method.

print(
  hello,                  // Original object that contains a string.
  hello.slice(0,2),       // Keep the first through third characters of the string.
  hello.concat('!'),      // Add an exclamation point after the string.
  hello.toUpperCase()     // Change the case to all upper. 
  )
;
```

## __numbers__

__Use numbers to store numerical data.__  

```js
// These are both numbers. 

var integer = 12;
var decimal = 11.987654321;

print(integer, decimal);              // Print number variables to Console

// You can call some number methods with dot notation.

print(decimal.toFixed(4));  

// Or call Javascript Math method that take number object as argument.

print(Math.round(decimal));           // Round decimal number to integer.
print(Math.floor(decimal));           // Round decimal number DOWN to nearest integer.
print(Math.ceil(decimal));            // Round decimal number UP to nearest integer.

```

## __lists__

__Use lists to store a set of data.__  

```js
// Use square brackets to define a list.

var some_vt_towns = ['Middlebury', 'New Haven', 'Bristol'];

// Use square brackets after lists to select items.

print(some_vt_towns, some_vt_towns[0]);

// Call list methods with dot notation.  

print(some_vt_towns.reverse());
```

## __dictionaries__  

__Use dictionaries to store keys and values.__  

```js
// Use curly brackets (or braces) to define dictionaries.

var midd = {
  "name": "Middlebury",  // Dictionaries are composed of key:value pairs.
  "pop_2010": 8496,
  "pop_2020": 9152
};

print("Middlebury", midd);

// Use dot notation to call the value(s) of a key.

print(midd.name);
```

## __functions__

__Write functions to make chunks of code reuseable.__  

```js

// A simple function the takes a string as an argument.  

var i_love_function = function(some_string) {
  return 'I love '.concat(some_string).concat('!');
};

print(i_love_function('maps'));

```

---

<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>