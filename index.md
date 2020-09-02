This document presents a set of guidelines for developing applications using Python. These guidelines aim to enhance readability and consistency of the code, enabling also its effective reuse and extension for new applications. 

## Imports

All imports should be on the top of the script file and should be on separate lines. 

```python
# good
import os
import sys

# bad
import os, sys
```
Sub-package imports should also be included along with the rest of the imports.

```python
# good
from package1 import subpackage1, subpackage2
a = subpackage1.do_something()

# bad
import package1
a = package1.subpackage1.do_something()
```

## Modules

When importing a module, all code at the top level will be executed. It is very important, even for files that are meant to be executables only, to include the main functionality within one or more functions and always perform the check ```if __name__ == '__main__'``` before executing the main program. 

```python
def fun1():
    ...
  
if __name__ == "__main__": 
    results = fun1() 
```

This way, ```fun1()``` from the example script above can also be imported in another script if needed.

```python

from abc import fun1

def fun2(results):
    ...
  
if __name__ == "__main__":
    results = fun1()
    fun2(results) 
```

## Naming

Guidelines derived from Guido’s Recommendations (PEP 8 Style Guide):

Type | Format
------------ | -------------
Packages | ```lower_with_under``` 
Modules | ```lower_with_under``` 
Classes | ```CapWords``` 
Exceptions | ```CapWords``` 
Functions | ```lower_with_under()``` 
Global/Class Constants | ```CAPS_WITH_UNDER``` 
Global/Class Variables | ```lower_with_under``` 
Instance Variables | ```lower_with_under``` 
Method Names | ```lower_with_under()``` 
Function/Method Parameters | ```lower_with_under``` 
Local Variables | ```lower_with_under```

Function names, variable names, and filenames should be descriptive and they should start with a lowercase character. Class names should normally use the CapWords convention. Always use a .py filename extension.

```python
# good
def multiply_by_4(x):
    return x * 4

# bad
def fun(x):
    return x * 4   
```

## Declaring List and Dictionary variables

When declaring a list variable it is convenient to use the following format: 

```python
my_list = [
    "element1",
    "element2",
    "element3"
]
```

Furthermore, using a comma after the last list element can be helpful when adding new elements or when a version control system is used to review code changes that include modifications in the list. 

If you use this pattern, each value must be placed on a line by itself and the close parenthesis/bracket/brace on the next line.

```python
# good
my_list = [
    "element1",
    "element2",
    "element3", 
]

# bad
my_list = ["element1", "element2",]
```

Use similar format when declaring a dictionary variable:

```python
my_dict = {
    "key1": {
        "subkey1": "value1"
    },
    "key2": "value2",
    "key3": "value3"
}
```

## Indentation

Indent your code blocks with 4 spaces.


In case of long function names, align the arguments on the next line after the open parenthesis or bracket on the first line.

```python
# good
def long_function_with_lots_of_arguments(argument1, argument2, argument3,
                                         argument4, argument5, argument6):
    ...

# bad
def long_function_with_lots_of_arguments(argument1, argument2, argument3,
         argument4, argument5, argument6):
    ...

```

## Whitespace

Do not use whitespace before a comma, semicolon, or colon. Avoid trailing whitespace anywhere.

Do use a whitespace after a comma, semicolon or colon. In order to enhance readability, use a whitespace before and after equality sign (=) and number sign (#) in case of comments.

```python
# good
get_order_info(orders[0], {id: "1234"})
my_list = []
i = i + 1

# bad
get_order_info( orders[ 0 ], { id: "1234" } )
my_list=[]
i=i+1
```

## Comments and Docstrings

Write docstrings for all public modules, functions, classes, and methods. Docstrings should provide a brief description of the general functionality, along with the description and type of the input and return values.  

Always use the three double-quote """ format for docstrings (PEP 257).

Docstrings should follow the Sphinx docstring format in order be able to automatically generate Sphinx documentation for the module.

```python
def sample_function(ParamName):
    """
    [Summary]

    :param [ParamName]: [ParamDescription], defaults to [DefaultParamVal]
    :type [ParamName]: [ParamType](, optional)
    ...
    :raises [ErrorType]: [ErrorDescription]
    ...
    :return: [ReturnDescription]
    :rtype: [ReturnType]
    """
    
    ...
```

Comments should be complete sentences that have a clear and easily understandable explanation. It is important to include a few lines of comments before complicated operations. 

In case inline comments are used, they should start at least 2 spaces away from the code with the comment character #, followed by at least one space before the text of the comment itself. In general, you should avoid using inline comments too often.

```python
l = [1, 2, 3, 4]
l = l[::-1]  # Reverse the order of the elements in the list
```

## Line length

Maximum line length is 79 characters. 

Regarding docstrings or comments, the line length should be limited to 72 characters. 

```python
# good
sample_fun(parm1, param2, param3="test", param4=None,
           param5=None, param6=0)

if (param1 == 0 and param2 == 0 and
    param3 == 2 and param4 == 5):
    
    ...
```
Exceptions to this rule include long URLs or pathnames (if it is possible put them in a seperate line).

```python
# you can find the documentation here:
# https://example.com/api/documentation/v2.0/swagger.html
```

Use parenthesis when separating a long string in multiple lines.  

```python
s = ("this is my really, really, really, "  
     "really long string that I'd like to split.")
```

Surround top-level function and class definitions with two blank lines. 
Method definitions inside a class are surrounded by a single blank line.

## Statements

Do not use multiple statements on the same line. 

```python
# good
if condition:
    do_something()

for order in orders:
    process_orders()

# bad
if condition: do_something
for order in orders: process_order(order)
do_something(); do_another_thing();
```
