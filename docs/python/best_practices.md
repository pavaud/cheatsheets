# Best Practices for Python Code (PEP 8 Guidelines)

!!! Note
    
    When writing Python code, it's important to **follow consistent coding standards** to ensure readability and maintainability of your codebase. Python's official style guide, [PEP 8](https://peps.python.org/pep-0008/), provides guidelines for writing clean and Pythonic code. 
    
    Some modules can help you write or format your code according to thes guidelines:
    
    - [`Flake8`](https://flake8.pycqa.org/en/latest/) : lint code
    - [`Black`](https://black.readthedocs.io/en/stable/) : format code
    - [`Isort`](https://pycqa.github.io/isort/) : format only imports
    - [`Mypy`](https://mypy.readthedocs.io/en/stable/) : check typing
    
    Here are some best practices to keep in mind.

## Indentation

- Use 4 spaces per indentation level.
- Avoid tabs (Change in your IDE Settings if needed), and never mix tabs and spaces.

**Bad:**
```python
def my_function():
  print("Indentation is inconsistent.")         # 2 spaces

def my_function():
        print("Indentation is inconsistent.")   # 8 spaces
```

**Good:**
```python
def my_function():
    print("Indentation is inconsistent.")       # 4 spaces
```

## Maximum Line Length

- Limit all lines to a maximum of 79 characters for code and comments.
- Break lines longer than 79 characters into readable, logical continuation lines.

**Bad:**
```python
my_long_variable_name = some_function_with_a_long_name(argument1, argument2, argument3, argument4)
```

**Good:**
```python
my_long_variable_name = some_function_with_a_long_name(
    argument1, argument2, argument3, argument4
)
```

## Imports

- Imports should be on separate lines.
- Imports should usually be grouped in the following order: standard library imports, related third-party imports, and local application/library specific imports.
- Avoid wildcard imports (`from module import *`), it makes it unclear which names are present in the namespace.

**Bad:**
```python
import os, sys
import user_lib
import pandas as pd
from math import *
```

**Good:**
```python
import os                   # standard
import sys
from math import sqrt

import pandas as pd         # 3rd party

import user_lib             # user
```

## Whitespace in Expressions and Statements

Avoid extraneous whitespace in the following situations:

  - Immediately inside parentheses, brackets, or braces.
  - Between a trailing comma and a following close parenthesis.

**Bad:**
```python
print( value1 , value2 )
list1 = [ 1,2 , 3 ,4]
dict1 = { "key1" : val , "key2" : 3 }
```

**Good:**
```python
print(value1, value2)
list1 = [1, 2, 3 , 4]
dict1 = {"key1": val , "key2": 3}
```

## Naming Conventions

- Use **descriptive names** for variables, functions, and modules.
- Use `snake_case` for **function** names and **variable** names.
- Use `CamelCase` for **class** names.
- Use `UPPER_CASE` for **constants** names.

**Bad:**
```python
a = "This is not a good variable name"
constante = 3

def BadFunctionName():
    pass

class bad_class_name():
    pass
```

**Good:**
```python
meaningful_name = "This is a good variable name"
CONSTANTE = 3

def good_function_name():
    pass

class GoodClassName():
    pass
```

## Comments and Documentation

- Use comments sparingly but effectively to explain complex parts of your code.
- Write docstrings for all public modules, functions, classes, and methods.
- Add a space between the `#` sign and the comment

**Bad:**
```python
#bad comment

# x += 1  # Increment x

def function(a):
    a += 1
    return a
```

**Good:**
```python
# good comment
x += 1 # Increment x

def function(a):
    """This function increments a"""
    a += 1
    return a
```

## Function and Method Arguments

- Always put positional arguments before keyword arguments.
- Don't use mutable objects as default values for function or method arguments.

**Bad:**
```python
def my_function(x=[])  # Default value is a mutable list
```

**Good:**
```python
def my_function(x, y, z=None):  # z is a keyword argument with a default value of None
```

## Exception Handling

- Specific exceptions should be caught instead of using a generic `except` clause.
- Avoid using bare `except:` clauses, specify the exception(s) you expect.

**Bad:**
```python
try:
    # some code that might raise an exception
except:
    # handle the exception
```

**Good:**
```python
try:
    # some code that might raise an exception
except ValueError:
    # handle the specific ValueError exception
```

## Development Best Practices

- Keep your code [**DRY** (Don't Repeat Yourself)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) and follow the principle of modularity.
- Write [**unit tests**](https://en.wikipedia.org/wiki/Unit_testing) for your code to ensure its correctness and ease of maintenance.
- Use [**version control systems**](https://en.wikipedia.org/wiki/Version_control) like Git to track changes and collaborate effectively.
- Use [**TDD** (Test Driven Developpement)](https://en.wikipedia.org/wiki/Test-driven_development). Write test before you code the function.
- Use [**Design Patterns**](https://refactoring.guru/design-patterns/python). You are not the first developer, the most common patterns are already documented.

## Linting and Formatting Your Code

