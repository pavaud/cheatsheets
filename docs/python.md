# Python

## Environment
---

```bash
# Upgrade python
upgraded directly from the website : https://www.python.org/downloads/

# upgrade pip:
python -m pip install --upgrade pip

pip install <package1> <package2> ...           # Installer un package
pip freeze                                      # afficher les packages déjà existants

pip list                                        # liste les packages installés sous forme agreable
pip freeze                                      # liste les packages installés sous forme de fichier requirements.txt

python -m site                                  # list the site-packages directories on the drive

pip show package                                # show package info

pip install requests==2.1.0                     # installer package avec version specifique
pip install "requests>2.4.0,<2.6.0"             # installer pac kage avec version comprise
pip install -r requirements.txt                 # installer les package lister par pip freeze dans requirements.txt
   
pip install venv                                # installer venv
python -m venv <environment name>               # créer un environnement virtuel
source env/Scripts/activate                     # activer environnement virtuel (env/Scripts/activate.bat Windows)
                                                # (désactive l'environnement actuel s'il y en a un)
    
deactivate                                      # desactive l'environment actuel depuis nimporte quel dossier
    
rm -r env/                                      # suppression d'un environnement virtuel
 
requirements.txt                                # fichier qui liste les packages à installer pour un projet
```

**environment variables**
```bash
# Linux
export PYTHONPATH=${PYTHONPATH}:${PWD}/src

# Command Prompt
set PYTHONPATH=%PYTHONPATH%;%CWD%\src

# Powershell
$env:PYTHONPATH="$env:PYTHONPATH;${PWD}\src"
```
### Pipenv

Install pipenv
```bash
pip install pipenv --user
```

Create .venv (or put PIPENV_VENV_IN_PROJECT=1 into a .env file that pipenv will load when invoke)
```bash
mkdir .venv                                     # if .venv not created, it installs .venv in ~/.venv (or export PIPENV_VENV_IN_PROJECT=1)
pipenv install [-r requirements.txt]            # if requirements.txt is not provided, install from Pipfile

pipenv install --python=/path/to/python         # use a specific interpreter/version
```

Activate venv
```bash
pipenv shell
```

Install in prod or dev environment 
place the package in the default or dev + defaults section of the Pipfile and Pipfile.lock
```bash
pipenv install <package> [--dev]
```
Generate a `requirements.txt` file (only default, with dev or only dev)
```bash
pipenv lock -r [--dev | --dev-only] > requirements.txt
```

Check for vulnerabilities in dependencies
```bash
pipenv check
```


## Create an Executable

### Install with python 2

```bash
sudo apt-get install python-dev
pip install cx_Freeze
```
### Install with python 3

- Download `cx_Freeze` library et extract
- in `setup.py`, replace the following line:

```python
if not vars.get("Py_ENABLE_SHARED", 0):
```

with:

```python
if True:
```
    
- Compile
```bash
setup.py build
setup.py install
```

### Program

The name must be `setup.py`

```python
from cx_Freeze import setup, Executable

# Call the setup function
setup(
    name = "program_name",
    version = "1",
    description = "Program description",
    executables = [Executable("script_name.py")],
)
```

### Build

```bash
python setup.py build

```

## Project Structure

```
# from Hitchhiker's

README.rst
LICENSE
setup.py
requirements.txt
sample/__init__.py
sample/core.py
sample/helpers.py
docs/conf.py
docs/index.rst
tests/test_basic.py
tests/test_advanced.py


# From Pytest doc

src/
    mypkg/
        __init__.py
        app.py
        view.py
tests/
    test_app.py
    test_view.py
    ...


# Avoid using __init__.py in test folder

new_project
├── antigravity
│   ├── __init__.py         # make it a package
│   └── antigravity.py
└── test
    ├── __init__.py         # also make test a package
    └── test_antigravity.py
    
# deal with relative path 
import os
FILE = os.path.realpath(os.path.join(os.path.dirname(__file__), '..','data', 'api_keys.txt'))
```

**main structure**
```python

#!/usr/bin/env python3
# -*- coding: utf-8 -*- 
#----------------------------------------------------------------------------
# Created By  : name_of_the_creator
# Created Date: date/month/time ..etc
# version ='1.0'
# ---------------------------------------------------------------------------
""" Extraction of all relevant fields in the Datatourisme DB

The script extracts the programmated stream from the Datatourisme website and 
checks for all updated POIs before transforming it and loading it into the 
Agoraa MySQL DB. 

Usage: 
    $ python datatourisme.py
"""

__author__ = "Philippe Vaudin"
__copyright__ = "Copyright 2007, The Cogent Project"
__credits__ = ["Rob Knight", "Peter Maxwell"]
__license__ = "GPL"
__version__ = "1.0.1"
__date__ = 14/03/2023
__maintainer__ = "Philippe Vaudin"
__email__ = "philippe@agoraa.fr"
__status__ = "Production"   # ou 'Development' ou 'Prototype'


import os           # standard library
import sys

import requests     # 3rd party packages

import mypackage    # local source


print("This is my file to demonstrate best practices.")


def process_data(data):
    print("Beginning data processing...")
    modified_data = data + " that has been modified"
    sleep(3)
    print("Data processing finished.")
    return modified_data


def read_data_from_web():
    print("Reading data from the Web")
    data = "Data from the web"
    return data


def write_data_to_database(data):
    print("Writing data to a database")
    print(data)


def main():
    data = read_data_from_web()
    modified_data = process_data(data)
    write_data_to_database(modified_data)

if __name__ == "__main__":
    main()

```

## Create Packages
---
Tout répertoire avec un fichier `__init__.py` est considéré comme un paquet Python

Structure d'un package python (dans le même dossier que le programme):
```
- nom_programme.py
- nom_package/
    - __init__.py
    - nom_module1.py
    - nom_module2.py
    -...
```

## Python Basics

### Operators

| Symbole |     Opération    | Exemple           |
|:-------:|:--------------:|:---------------:|
|    +    |     Addition     | 6+4 renvoie 10    |
|    -    |   Soustraction   | 6-4 renvoie 2     |
|    *    |  Multiplication  | 6*4 renvoie 24    |
|    /    |  Division réelle | 6/4 renvoie 1.5   |
|    //   | Division entière | 6.0//4 renvoie 1  |
|    **   |     Puissance    | 6**4 renvoie 1296 |
|    %    |      Modulo      | 6 % 4 renvoie 2   |

### Assignation

 Symbole |     Opération   
:--------:|:----------------:
    +=   |     Addition    
    -=   |   Soustraction  
    *=   |  Multiplication 
    /=   |  Division réelle
   //=   | Division entière
   **=   |     Puissance 
    %=   |      Modulo     

### Comparison

| Expression | Exemple | Signification                                |
|:----------:|:------:|-----------------------------------------|
| <          |  x < y  | Est-ce que x est strictement inférieur à y ? |
| <=         |  x <= y | Est-ce que x inférieur ou égal à y ?         |
| >          |  x > y  | Est-ce que x est strictement supérieur à y ? |
| >=         |  x >= y | Est-ce que x est supérieur ou égal à y ?     |
| ==         |  x == y | Est-ce que x est égal à y ?                  |
| !=         |  x != y | Est-ce que x est différent de y ?            |

### Logical Comparison

| Opérateur | Exemple | Signification |
|:---------:|:-------:|-----------------------------------------------------------------|
|    and    | P and Q |                       Est-ce que P et Q sont toutes deux vraie ? |
|     or    |  P or Q | Est-ce que au moins une des expressions parmi P et Q est vraie ? |
|    not    |  not P  |                                    La négation de l'expression P |

### Membership

| Expression | Exemple | Signification |
|:----------:|:-----------------------:|-----------------------------------------|
| in         | "France" in extrait     | return true if France is in extrait     |
| not in     | "France" not in extrait | return true if France is not in extrait |

### Variable Names Scope

- `variable_name` : normal variable

- `_single_leading_underscore` : weak **module internal use** indicator.
    
    > E.g. : `from M import *` **does not import** objects whose name starts with an underscore.

- `single_trailing_underscore_`: used by convention to avoid conflicts with Python keyword.

    > E.g.: Tkinter.Toplevel(master, class_='ClassName')

- `__double_leading_underscore`: when naming a class attribute, invokes `name mangling`
 (inside class FooBar, __boo becomes _FooBar__boo; see below).

- `__double_leading_and_trailing_underscore__`: “magic” objects or attributes that live in user-controlled namespaces. 
    
    > E.g. `__init__`, `__import__` or `__file__`. Never invent such names; only use them as documented.



### Control Structures

```python
# normal control
if condition:
    statment
elif condition:
    statment
else:
    statment

# conditionnal assignment 
redouble = True if moyenne < 10 else False
```

### Loops

```python

while condition:
    statment

for item in sequence:                           # sequence can be range, list/dict/tuple
    statment

for item in range(start, end, step):            # sequence can be a range
    statment                                    # 'end' is exclusive, step not necessary (1 by default)
                                                # range(n) -> goes from 0 to n-1

ma_liste = [i**2 for i in range(10)]            # list comprehension (can be used for generator with "()" instead of "[]")
liste_pairs = ["pair" if n%2 == 0 else "impair" for n in liste_nombres]

for index, element in enumerate(sequence):      # enumerate returns item and index of item

for item1, item2 in zip(seq1, seq2, ...)        # zip iterates on multiple sequences at a time
```

### Types

```python
type(var)                                       # type of variable var
id(a)                                           # This is the address of the object in memory 
```

#### String

```python
s.split(sep,maxsplit)                           # sep default is space ans maxsplit is the number of splits to do. default is -1 which splits all the items.
'-'.join([la,bas])                              # returns "la-bas"
s.strip()                                       # remove all right and left spaces from s
s.strip("()")                                   # remove all ( and ) from s on right and left
s.lower()
s.upper()
s.swapcase()
s.count('c')                                    # count number of 'c' character in s
sorted(s, reverse=True)                         # permet de trier les caractères de s
```

#### Format-String

```python
print(f"{DEBUG = }")                # print DEBUG = False 

f'{nombre : >+20_.4f} {nombre2 : >+20_.4f}')
3.1415926	    {:.2f}	3.14	    Format float 2 decimal places
3.1415926	    {:+.2f}	+3.14	    Format float 2 decimal places with sign
-1	            {:+.2f}	-1.00	    Format float 2 decimal places with sign
2.71828	        {:.0f}	3	        Format float with no decimal places
4	            {:0>2d}	04	        Pad number with zeros (left padding, width 2)
4	            {:x<4d}	4xxx	    Pad number with x’s (right padding, width 4)
10	            {:x<4d}	10xx	    Pad number with x’s (right padding, width 4)
1000000	        {:,}	1,000,000	Number format with comma separator
0.35	        {:.2%}	35.00%	    Format percentage
1000000000	    {:.2e}	1.00e+09	Exponent notation
11	            {:11d}	11	        Right-aligned (default, width 10)
11	            {:<11d}	11	        Left-aligned (width 10)
11	            {:^11d}	11	        Center aligned (width 10)
```

`[[fill]align][sign][#][0][minimumwidth][.precision][type]`

```
# align and fill
'<' - left-aligned within the available space (This is the default.)
'>' - right-aligned within the available space.
'^' - centered within the available space.
'=' - (for numeric types) Forces the padding to be placed after the sign (if any)
      but before the digits.  This is used for printing fields
      in the form '+000000120'.
```
```
# sign option just for numeric types
'+'  - sign should be used for both positive and negative numbers
'-'  - sign should be used only for negative numbers (default)
' '  - leading space should be used on positive numbers
```
```
'b' - Binary. Outputs the number in base 2.
'c' - Character. Converts the integer to the corresponding Unicode character before printing.
'd' - Decimal Integer. Outputs the number in base 10.
'o' - Octal format. Outputs the number in base 8.
'x' - Hex format. Outputs the number in base 16, using lower-case letters for the digits above 9.
'X' - Hex format. Outputs the number in base 16, using upper-case letters for the digits above 9.
'n' - Number. This is the same as 'd', with current locale setting to insert the appropriate number separator characters.
'' (None) - the same as 'd'
```
```
'e' - Exponent notation.
'E' - Exponent notation. Same as 'e' except it converts the number to uppercase.
'f' - Fixed point. Displays the number as a fixed-point number.
'F' - Fixed point. Same as 'f' except it converts the number to uppercase.
'g' - General format. fixed-point number, unless the number is too large, in which case it switches to 'e'
'G' - General format. Same as 'g' except switches to 'E' if the number gets to large.
'n' - Number. This is the same as 'g', with current locale setting to insert the appropriate number separator characters.
'%' - Percentage. Multiplies the number by 100 and displays in fixed ('f') format, followed by a percent sign.
'' (None) - similar to 'g', except that it prints at least one digit after the decimal point.
```

#### Regex

```python
import re


```

#### Lists []

```python
# processing
my_list.pop(1)                                  # remove item at index 1
my_list.remove(value)                           # remove first occurence of value
my_list.append(x)                               # append x to the end of the list
my_list.insert(1,x)                             # insert x at the index 1 in the list
my_list.extend(my_other_list)                   # extend ma_liste with my_other_list
my_list.sort()                                  # sort list (reversed=True for reverse order)
sorted(my_list)                                 # même effet que pour sort() mais s'utilise aussi sur les string
my_list.reverse()                               # (In-place) reverse all element of my_list
my_list.clear()                                 # remove all item from list
my_list.index(value)                            # return first index of value
my_list.copy()                                  # copy of my_list

# slicing
my_list[start:end:step]                         # end is exclusive, step not necessary (1 by default) 
my_list[0]                                      # first element
my_list[-1]                                     # last element
my_list[0:2:-1]                                 # 
my_list[::-1]                                   # reverted order
my_list[...,0]                                  # [:, :, :, 0], […, 0] and [Ellipsis, 0] are equivalent
```

#### Tuples ()

```python
un_tuple = "Bonjour", -1, 133
x, y, z = un_tuple                              # Tuple assignment (number of variable = number of item in tuple)
a, b = b, a                                     # value swapping instead of tmp variable
```

#### Dictionaries {key: value}

```python
my_dict = {"age":25,"taille":183,"sexe":"F"}
my_dict = {x: x ** 2 for x in range(10)}
dict([('foo', 100), ('bar', 200)])

my_dict["new_key"] = "value"                    # add new key with value
my_dict.pop("new_key")                          # remove new_key.
my_dict.clear()	                                # Removes all the elements from the dictionary
my_dict.copy()	                                # Returns a copy of the dictionary
my_dict.fromkeys()	                            # Returns a dictionary with the specified keys and value
my_dict.get('key')	                            # Returns the value of the specified 'key'
my_dict.items()	                                # Returns a list containing a tuple for each key value pair
my_dict.keys()	                                # Returns a list containing the dictionary's keys
my_dict.values()	                            # Returns a list of all the values in the dictionary
my_dict.pop()	                                # Removes the last element if no key specified
my_dict.popitem()	                            # Removes the last inserted key-value pair
my_dict.setdefault()	                        # Returns the value of the specified key. If the key does not exist: insert the key, with the specified value
my_dict.update()	                            # Updates the dictionary with the specified key-value pairs
del my_dict["xxx"]                              # remove key "xxx" from dict
```

*shallow vs. deep copy*

```python
import copy

original_dict = {'key1': [1, 2, 3], 'key2': {'a': 1, 'b': 2}}
shallow_copy = original_dict.copy()
deep_copy = copy.deepcopy(original_dict)
assign_copy = original_dict

# Modifying the inner list
original_dict['key1'].append(4)

print(f"Id : {id(original_dict)}, {original_dict}")         # Id : 1846091003776, {'key1': [1, 2, 3, 4], 'key2': {'a': 1, 'b': 2}}
print(f"Id : {id(shallow_copy)}, {shallow_copy}")           # Id : 1846090999232, {'key1': [1, 2, 3, 4], 'key2': {'a': 1, 'b': 2}}
print(f"Id : {id(deep_copy)}, {deep_copy}")                 # Id : 1846090994432, {'key1': [1, 2, 3], 'key2': {'a': 1, 'b': 2}}
print(f"Id : {id(assign_copy)}, {assign_copy}")             # Id : 1846091003776, {'key1': [1, 2, 3, 4], 'key2': {'a': 1, 'b': 2}}
```
#### Sets {}

```python
# Set creation
{'jack', 'sjoerd'}
{c for c in 'abracadabra' if c not in 'abc'}
set()
set('foobar')
set(['a', 'b', 'foo'])

# Functions
x = set('abracadabra')                          # return unique letters of 'abracadabra'
y = set('chti')                                 

x.isdisjoint(y)                                 # returns true if x and y have no common element

x.issubset(y)                                   # returns true if all elements of x are in y
x <= y                                          

x.issuperset(y)                                 # returns true if all elements of y are in x
x >= y                                          

x.union(y)                                      # returns new set with all elements from both x and y
x | y                                           

x.intersection(y)                               # returns a new set with elements common to x and y
x & y                                           

x.difference(y)                                 # returns a new set with elements in x that are not in y
x - y                                           
```

#### Counter

```python
from collections import Counter

# récupération de toutes les observations
data = list(
    {'key1':value1,'key2':value2}, 
    {'key1':value1,'key2':value2, 'key3':value3}
)

# comptage du nombre de champs par document
fields_count = list(map(lambda x: len(x), data))                # compte les clés de premier niveau seulement

# calcul de la distribution du nombre de champs par document
counter = Counter(fields_count)
# Counter({20: 675, 19: 380, 21: 174, 18: 107, 17: 4})
# Il y a 675 objets de 20 champs etc...

c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)
# Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})

counter.most_common(n)                          # Returns a list of tuples of the n most frequent keys with their value
# [('20', 675), ('19', 380), ('21', 174))]
c.most_common()[:-n-1:-1]                       # n least common elements

counter.total()
# N : sum of all value in the counter

+counter                                        # remove zero and negative counts
```


### Annotations

```python
def une_fonction(a:str='Hello World')->None:    # parameter and return type precised
   print(a)
print(une_fonction.__annotations__)             # display annotations of a function
{'a': str, 'return': None}
```

### Functions

#### Display documentation

```python
help(my_function)
```

#### Definition

```python

def my_function(param1=x, param2, ...):         # parameters can be any type, x is the default value of param1
    
    """short description of the function in one line.
    
    Parameters:
        param1 : la liste à trier.
        param2 : number of items

    Return :
        val_out : return value   
    """
    
    # statments
    ...
    
    # result
    return val1, val2                           # when multiple return -> tuple assignment
```

### Modules, Packages and Librairies

```python
import numpy as np                              # "as np" not necessary, np is an alias
print(numpy.cos(x))                             # if "as np" is not mentionned
print(np.cos(x))                                # if "as np" is mentionned
        
from numpy import cos, sin, exp                 # import only the modules cos, sin, exp
```

### With Statement

```python
with open('file_path', 'w') as file:            # ensure that the process ends properly
    file.write('hello world !')                 # and is equivalent to the try except approach

# try except equivalent
file = open('file_path', 'w')
try:
    file.write('hello world !')
finally:
    file.close()    
```

### Try Except Statement
```python
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")  
```

## POO

### Class Definition

```python
class Car:
    
    """La classe Car permet de construire une voiture.

    Paramètres
    ----------
    color : Chaîne de caractères : Couleur de la voiture.
    model : Chaîne de caractères : Modèle de la voiture.
    horsepower : Entier : Cylindrée de la voiture.

    Example
    -------
    aventador = Car(color = "orange", model = "Aventador", horsepower = 700)
    """

    # Definition of class variable
    n_cars = 0

    # Définition du constructeur de la classe Car
    def __init__(self, color, model, horsepower):
       # Initialisation des attributs de la classe avec les arguments du constructeur
        self.color = color
        self.model = model
        self.horsepower = horsepower

    # Définition d'une méthode permettant de changer la couleur d'une voiture
    def change_color(self, new_color):
        """Modifie la couleur d'une voiture.

        Paramètres
        ----------
        new_color : string : Nouvelle couleur de la voiture.
        """
        self.color = new_color

# instanciation
aventador = Car(color = "orange",               # Création d'un objet de la classe Car
                model = "Aventador",
                horsepower = 700)

# display class documentation
help(Car)

```

### heritage
```python
class Vehicule: 
    def __init__(self, a, b = []):
        self.seats = a 
        self.passengers = b 
        
    def add(self,name):
            self.passengers.append(name)

class Moto(Vehicule): # heritate from Vehicule
    def __init__(self, b, c):
        self.seats = 2
        self.passengers = b
        self.brand = c
```
## polymorphism
```python
class Vehicule: 
    def __init__(self, a, b = []):
        self.seats = a  
        self.passengers = b

    def add(self,name):
            self.passengers.append(name)

class Moto(Vehicule):
    def __init__(self, b, c):
        self.seats = 2
        self.passengers = b
        self.brand = c
        
    def add(self, name): # polymorphism
        if( len(self.passengers) <  self.seats):
            self.passengers.append(name)
            print('Il reste', self.seats - len(self.passengers), 'places')
        else:
            print("Le véhicule est rempli")

```

## built_in
https://docs.python.org/3/library/functions.html
```python
all(iterable)                                   # Return True if all elements of the iterable are true (or if the iterable is empty)
any(iterable)                                   # Return True if any element of the iterable is true. If the iterable is empty, return False.
chr(i)                                          # chr(97) returns the string 'a' (invers of ord())
delattr(object, name)                           # delattr(x, 'foobar') is equivalent to del x.foobar
dict(iterable, **kwarg)                         # Create a new dictionary
dir(list)                                       # displays attributes and methods of object 'list'
help(list)                                      # displays documentation of object 'list'
isinstance(object, classinfo)                   # Return True if the object argument is an instance of the classinfo argument
iter(object[, sentinel])                        # Return an iterator object.
map(function, iterable, ...)                    # Return an iterator that applies function to every item of iterable, yielding the results
ord(c)                                          # ord('a') returns the integer 97 and ord('€') returns 8364
open(file, mode='r',...)                        #
pow(base, exp[,mod])                            # Return base to the power exp; if mod is present, return base to the power exp, modulo mod (computed more efficiently than pow(base, exp) % mod)
zip(*iterables, strict=False)                   # Iterate over several iterables in parallel, producing tuples with an item from each one




'__class__',
 '__delattr__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__lt__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__sizeof__',
 '__str__',                                     # when own class : better than method like afficher() 
 '__subclasshook__'

# redefine built-in
Class Complexe:
    ...
    def mod(self):
        return np.sqrt(self.partie_re**2 +      # renvoie (sqrt(a² + b²))
        self.partie_im**2)
    
    def __lt__(self, other):                    # new built-in method __lt__ redefined
        return self.mod().__lt__(other)
        
z1 = Complexe(3,4)
z2 = Complexe(2,-5)
print(z1<z2)                                    # prints True

```
## decorators

### predefined decorators
```python
@functools.wrap(func)                           # keep properties with func
@functools.lru_cache()                          # speed up execution time



```
### function with **no arguments** and **return nothing**
```python

def do_twice(func):
    def wrapper_do_twice():
        func()
        func()
    return wrapper_do_twice

@do_twice
def say_whee():
    print("Whee!")
    
# results ############################################# 
# Whee!
# Whee!

```


### function with **arguments** and **return nothing**
```python

def do_twice(func):
    def wrapper_do_twice(*args, **kwargs):              # *args, **kwargs added
        func(*args, **kwargs)                           # *args, **kwargs added
        func(*args, **kwargs)                           # *args, **kwargs added
    return wrapper_do_twice

@do_twice
def greet(name):
    print(f"Hello {name}")
    
greet("World")
    
# results ############################################# 
# Hello World
# Hello World

```

### function with **arguments** and **return something**
```python

def do_twice(func):
    def wrapper_do_twice(*args, **kwargs):
        func(*args, **kwargs)
        return func(*args, **kwargs)                    # return added
    return wrapper_do_twice

@do_twice
def return_greeting(name):
    print("Creating greeting")
    return f"Hi {name}"

return_greeting("Adam")

# results ############################################# 
# Creating greeting
# Creating greeting
# 'Hi Adam'                                             # return value of the last execution sent

```

### decorators with **arguments**
```python

def repeat(num_times):
    def decorator_repeat(func):
        @functools.wraps(func)
        def wrapper_repeat(*args, **kwargs):
            for _ in range(num_times):
                value = func(*args, **kwargs)
            return value
        return wrapper_repeat
    return decorator_repeat
    
@repeat(num_times=4)
def greet(name):
    print(f"Hello {name}")

greet("World")

# results ############################################# 
# Hello World
# Hello World
# Hello World
# Hello World
```

### decorators **chained**
```python

def print_before_execution(function):
    def print_then_execute(*args, **kwargs):
        print('voici ce que renvoie la fonction {}'.format(function.__name__))
        function(*args, **kwargs)
    return print_then_execute

def print_after_execution(function):
    def execute_then_print(*args, **kwargs):
        function(*args, **kwargs)
        print('La fonction a fini de tourner')
    return execute_then_print

@print_after_execution
@print_before_execution
def print_hello_world():
    print('hello world')

print_hello_world()

# results ############################################# 
# voici ce que renvoie la fonction print_hello_world
# hello world
# La fonction a fini de tourner
```

## threading
```python
from threading import Thread

def calcul(x):
    x*x

th=Thread(target=calcul,args=(5,))                  # create thread
th.start()                                          # start thread 
th.join()                                           # complétion of thread
    
```

## multiprocessing
```python
from multiprocessing import Pool

def f(x):
    return x*x
if __name__ == '__main__':
    with Pool(5) as p:                              # number of process (max ~ 60x Windows)
        print(p.map(f, [1, 2, 3]))                  # apply f to 1, 2 and 3 on 5 processes      
```

The **Process class** has equivalents of all the methods of **threading.Thread**
```python
from multiprocessing import Process

def f(name):
    print('hello', name)
if __name__ == '__main__':
    p = Process(target=f, args=('bob',))
    p.start()
    p.join()
```

## coroutines/asynchrone

```python
asyncio.run(func())                                 # run coroutine func() This function 
                                                    # always creates a new event loop and closes it at the end. 
                                                    # It should be used as a main entry point for asyncio programs, 
                                                    # and should ideally only be called once

await func()                                        # run coroutine in Jupyter Notebook
await asyncio.gather(nom_async('Daniel'),           # gather async function and run them with await
                     nom_async('Donna'),            # result is an aggregate list of returned values
                     nom_async('Diane'))

asyncio.ensure_future(name_async())                 # create task for concurrency
asyncio.create_task(name_async())                   # create task for concurrency (preferred way)


```

---
# POO CONCEPTS

### GENERIQUE
- classe
- constructeur
- getter et setter
- encapsulation (_ et __ préfixe protégé ou privé mais tout est public en vrai)
- héritage (multiple)
- surcharge de méthode
- polymorphisme
- interface
- collections d'objet
- erreur

### PYTHON
- attribut de classe/instance
- decorateurs
- methode de classe/instance/statique (@classmethod)
- propiété (@property) (getter et setter)

### BONNES PRATIQUES
- TDD
- Design Patterns
- SOLID
- Single responsibility
- Chaque classe ou fonction doit faire une seule chose
- Open/Closed
- Les classes doivent être ouvertes à l’extension, mais fermées à la modification.
- Liskov
- Les sous-classes doivent pouvoir faire tout ce que font leurs classes parentes
- Interface Segregation
- responsabilité unique, appliqué aux interfaces.
- Dependency Inversion
- Les classes parentes ne doivent pas avoir à changer lorsque l’une de leurs sous-classes est modifiée.

### A EVITER
- STUPID
- Singleton.
- Couplage fort (« Tight coupling »).
- Non-testabilité (« Untestability »).
- Optimisation prématurée (« Premature optimization »).
- Nommage non descriptif (« Indescriptive naming »).
- Duplication.

---

# TESTS

### Librairies
- unittest (avec classe)
- pytest (sans classe)
- doctest (standard library)

### Stratégie de test

- Tester l'INTERFACE des objets
- 3 sens de messages : entrants, internes et sortants.
- 2 types : requête et commande
    - entrants:
        - requête > test avec assertions avec ce quelle doivent renvoyer
        - commande > assert avec les changements directs
    - internes:
        - requête > ignorer (car si le test entrant se passe bien > le fonctionnement interne est OK)
        - commande > ignorer
    - sortants:
        - requête > ignorer
        - commande > attendre à envoyer / utiliser des mocks

### Doctest
```python
import doctest

def add(a, b):
    """
    Given two integers, return the sum.

    :param a: int
    :param b: int
    :return: int

    >>> add(2, 3)
    5
    >>> add(3, 3)
    6
    """
    return a + b

doctest.testmod()

###
Output
TestResults(failed=0, attempted=1)
```

- Tester avec : python -m doctest -v program/world.py

- Sinon créer un fichier de test à part:
    - Ecrire d'abord les tests en texte puis implémenter les en classes

### PyTest
- recherche `test_*.py` ou `*_test.py`
- recherche ensuite les fonctions et méthodes en dehors des classes commençant par `test`
- recherche ensuite les fonctions et méthodes préfixer par `test` dans les classes commençant par `Test`
- créer des mock avec monkey...
- setup() : avant test - setup_module(module), setup_method(self, method), setup_function(function)
- teardown() : après test

```python
pip3 install pytest
python3 -m pytest code1_test.py   # python3 -m not mendatory
```
### Coverage
```python
pip install coverage
pip install pytest-cov

pytest --cov=program --cov-report html test_*.py
# crée:
# - 1 fichier HTML "index.html" dans le dossier "htmlcov" qui affiche le tableau de coverage
# - 1 fichier HTML par fichier testé pour le détail
```


---
# LIBRARIES

### os
```
import os

path = "/home/olivier/scripts/cgi-bin/action.py"
os.path.dirname(path)
'/home/olivier/scripts/cgi-bin'

os.path.basename(path)
'action.py'

os.path.join(path, "func")
'/home/olivier/scripts/cgi-bin/action.py/func'

os.path.split(path)
('/home/olivier/scripts/cgi-bin', 'action.py')

os.path.abspath(".")
'/home/olivier'

os.listdir("/home/olivier")
['.bash_history', 'Images', 'script.py']

os.makedirs(path)                                   # Créer récursivement tous les dossiers d'un path si ceux-ci n'existent pas
os.mkdir(path)                                      # Créer le dernier dossier d'un path. Si un des dossiers n'existe pas une erreur est retournée
os.remove(path)                                     # Supprime le fichier / dossier indiqué
os.rename(old, new)                                 # Renomme le fichier / dossier indiqué

FILE = os.path.realpath(os.path.join(os.path.dirname(__file__), '..','data', 'api_keys.txt')) # translate ".." into real path


folder_path = "/mnt/box/files"
for path, dirs, files in os.walk(folder_path):
    for filename in files:
        print(filename)
```

### dotenv
```python
pip install python-dotenv
```

```python
from dotenv import load_dotenv

load_dotenv()  # take environment variables from .env.

# Code of your application, which uses environment variables (e.g. from `os.environ` or
# `os.getenv`) as if they came from the actual environment.
```

```python
from dotenv import dotenv_values

config = dotenv_values(".env")  # config = {"USER": "foo", "EMAIL": "foo@example.org"}
```

```python
import os
from dotenv import dotenv_values

config = {
    **dotenv_values(".env.shared"),  # load shared development variables
    **dotenv_values(".env.secret"),  # load sensitive variables
    **os.environ,  # override loaded values with environment variables
}
```


#### random
Pas pour des projets de sécurité (cf. module "secrets")
```python
random.randint(a, b)
random.choice(seq)                                                  # choose one item among list "seq"
random.choices(population, weights=None,*, cum_weights=None, k=N)   # random draw N item among population
random.shuffle(x[, random])
random.sample(population, k, *, counts=None)
random.random()
random.uniform(a, b)
random.gauss(mu, sigma)
```

### argparse
```python
import argparse

parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                    help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))
```

### logging
```python
import logging

# Logging level
logging.basicConfig(encoding='utf-8', level=logging.DEBUG)

logging.info('Request success : %d', response.status_code)
logging.error('Request failure : %s', str(e))

```

### json
```python
import json

# export to json and format with indent (else just one line)
with open('arrivals.json', 'w') as f:
    json.dump(arr.json(), f, indent=4)

# deal with unicode character
with open("updates.json", "w", encoding="utf-8") as f:
        json.dump(poi_new_schema, f, indent=4, ensure_ascii=False, default=str)   

# export list to JSON file
list = [{'key':'value','key2':'value'},{'key':'value','key2':'value'},...]
with open('arrivals.json', 'w') as f:
    json.dump(list, f, indent=4)

# convert dict to JSON object
obj = json.dumps(market_data, default=pydantic_encoder)

# import json file
with open('departures.json') as f:
    dep = json.load(f)

# string to JSON (plusieurs doc JSON importés depuis un fichier à retransformé
with open('airlines.json','r') as f:
    lines = f.readlines()
    for line in lines:
        l=json.loads(line)          # l est au format JSON et line string
        ...

# Export to JSON 1 line / document
with open('airports.json', 'w') as f:
    for a in airports["Airport"]:
        json.dump(a, f)
        f.write('\n')

# convert string to JSON
index = """
[
  {
    "label": "VILLA GALLO-ROMAINE DU GROSSWALD",
    "lastUpdateDatatourisme": "2023-01-01T05:07:52.747Z",
  },
  {
    "label": "PARC DU TONNEAU",
    "lastUpdateDatatourisme": "2023-01-02T05:07:52.747Z",
  }
]
"""
ind = json.loads(index)
for i in ind:
    print(type(i))                  # i est un dict

     
```

### pickle
**Serializing** : Save the state of an object into memory or a file (.pkl for example)
**Deserializing** : retrieve an object from memory or a file (.pkl for example)

Formats for serializing : `pickle`, `JSON`, `XML`, `HDF5`

Advantages of Pickle :
- can serialize almost every commonly used built-in Python (unlike JSON...)
- good choice when storing recursive structures since it only writes an object once.

Disadvantages of Pickle : 
- unsafe because it can execute malicious Python callables to construct objects.
- Python-specific module, and you may struggle to deserialize pickled objects when using a different language.
- appears to be slower and produces larger serialized values than formats such as JSON and ApacheThrift.

```python
# save object
pickle.dump(obj, file, protocol=None, *, fix_imports=True, buffer_callback=None)
pickle.dumps(obj, protocol=None, *, fix_imports=True, buffer_callback=None)

# retrieve object
pickle.load(file, *, fix_imports=True, encoding='ASCII', errors='strict', buffers=None)
pickle.loads(data, /, *, fix_imports=True, encoding=”ASCII”, errors=”strict”, buffers=None)
```

**Write CSV vs Pickle**
```python
# write to CSV
start = time.time()
df.to_csv('pandas_dataframe.csv')
end = time.time()
print(end - start)
-------
0.19349145889282227


# write to Pickle
start = time.time()
df.to_pickle("my_pandas_dataframe.pkl")
end = time.time()
print(end - start)
-------
0.0059659481048583984
```

**Read CSV vs Pickle**
```python
# Reading the csv file into Pandas:
start1 = time.time()
df_csv = pd.read_csv("my_pandas_dataframe.csv")
end1 = time.time()
print(end - start)
-------
0.00677490234375


# Reading the Pickle file into Pandas:
start2 = time.time()
df_pkl = pd.read_pickle("my_pandas_dataframe.pkl")
end2 = time.time()
print(end2 - start2)
-------
0.0009608268737792969
```

**ML Models**

Pickle allows to serialize machine learning models in their **existing state**.
It makes it possible to use them again as needed.

```python
from sklearn.linear_model import LinearRegression
from sklearn.datasets import make_regression

# generate regression dataset
X, y = make_regression(n_samples=100, n_features=3, noise=0.1, random_state=1)

# train regression model
linear_model = LinearRegression()
linear_model.fit(X, y)

# summary of the model
print('Model intercept :', linear_model.intercept_)
print('Model coefficients : ', linear_model.coef_)
print('Model score : ', linear_model.score(X, y))
------
Model intercept : -0.010109549594702116
Model coefficients :  [44.18793068 98.97389468 58.17121618]
Model score :  0.9999993081899219

# Serializing
with open("linear_regression.pkl", "wb") as f:
    pickle.dump(linear_model, f)
```

```python
# Deserializing
with open("linear_regression.pkl", "rb") as f:
    unpickled_linear_model = pickle.load(f)

# summary of the model
print('Model intercept :', unpickled_linear_model.intercept_)
print('Model coefficients : ', unpickled_linear_model.coef_)
print('Model score : ', unpickled_linear_model.score(X, y))
------
Model intercept : -0.010109549594702116
Model coefficients :  [44.18793068 98.97389468 58.17121618]
Model score :  0.9999993081899219
```

**Speeding up**

*Pickle*
```python
start = time.time()
with open("df1.pkl", "wb") as f:
    pickle.dump(data, f)
end = time.time()
print(end - start)
------
0.006001710891723633
```

*PROTOCOL property*
```python
start = time.time()
with open("df2.pkl", "wb") as f:
    pickle.dump(data, f, protocol=pickle.HIGHEST_PROTOCOL)
    end = time.time()
print(end - start)
------
0.0030384063720703125```

*cPickle*
```python
start = time.time()
with open("df3.pkl", "wb") as f:
    cPickle.dump(data, f)
end = time.time()
print(end-start)
------
0.004027366638183594
```




### numpy
fast numerical calculation
[numpy website](https://numpy.org/doc/stable/reference/)

**create table**
```python
import numpy as np

X = np.zeros(shape = (5, 10))                       # Création d'une matrice de dimensions 5x10 remplie de zéros
X = np.ones(shape = (3, 10, 10))                    # Création d'une matrice à 3 dimensions 3x10x10 remplie de uns
X = np.array([2*i for i in range(10)])              # [0, 2, 4, 6, ..., 18] Création d'un array à partir d'une liste définie en compréhension
X = np.array([[1, 3, 3],                            # Création d'un array à partir d'une liste de listes
              [3, 3, 1],
              [1, 2, 0]])

np.linspace(start = 0.01, stop = 0.15, num = 15))   # [0.01, 0.02, ..., 0.15] define 1D array with number of values


X_1 = np.ones(shape = (2, 3))
X_2 = np.zeros(shape = (2, 3))
X_3 = np.concatenate([X_1, X_2], axis = 0)          # Concatenate arrays with care to dimensions (axis 0 = rows, axis 1 = columns)

# defines array with step size
np.arange(3)                                        # returns array([0, 1, 2])
np.arange(3,7)                                      # returns array([3, 4, 5, 6])
np.arange(3,7,2)                                    # defines array([3, 5]) with step size

x = np.array([0.2, 6.4, 3.0, 1.6])
bins = np.array([0.0, 1.0, 2.5, 4.0, 10.0])
inds = np.digitize(x, bins)                         # inds returns array([1, 4, 3, 2])

```

**select and slicing**
```python
X[4, 3]                                             # affichage de l'élément à l'index (4, 3)
X[1, 5] = -1                                        # assignation de la valeur -1 à l'élément d'index (1, 5)
X[X<0] = 0                                          # conditionnal assignment
X[1:4, 2:9, 5:7]                                    # slicing N dimension (négative possible)


X = np.array([3, -7, -10, 3, 6, 5, 2, 9])
y = np.array([0, 1, 1, 1, 0, 1, 0, 0]) 
X[y == 1] = -1                                      # On assigne la valeur -1 aux éléments de X pour lesquels la valeur de y à l'indice correspondant vaut 1
print(X[y == 0])                                    # Affichage des éléments de X pour lesquels la valeur de y à l'indice correspondant vaut 0
```

**math functions**
```python
np.exp(x)
np.abs(x)
np.log(x)
np.sin(x)
np.cos(x)
np.round(x, decimals = n)
```

**shape**
```python
X.shape                                             # X dimensions ex: (3,4)
X = [1  2  3  4  5  6  7  8  9 10]                  # reshaping (must have same number of elements)
X_reshaped = X.reshape((2, 5))
[[1  2  3  4  5]
  [6  7  8  9 10]]
```
**operations**
```python
M*N                                                 # product element by element wirh *
M.dot(N)                                            # matrix product with dot()

np.where(probs[:,1]>0.4,1,0)                        # returns 1 if probs[:,1]>0.4, 0 else
```

**broadcasting**
```python
# broadcasting matrix and constante
M=[[ 1  2  3  4  5]
  [ 6  7  8  9 10]]
c=4                                                 
M+c                                                 # c is transformed in a matrix of shape M
[[ 5  6  7  8  9]
  [ 10  11  12  13 14]]

# broadcasting matrix and vector (check for same dimension or dimension 1)
M=[[ 3 1 2]
   [-2 1 5]]
v=[[2]    =>    v=[[2 2 2]                          # v is broadcasted on his dimension of size 1
   [5]]            [5 5 5]]
M*v=[[ 6 2 4]
     [-10 5 25]]
u=[[3 4]]
v+u=[[2 2]   +   [[3 4]                             # v and u are broadcasted on their dimension of size 1
     [5 5]]       [3 4]]                                

 # Le broadcasting nous permet de faire cette opération sans boucle for sur les lignes
X_tilde[:, j] = (X[:,j]-min_Xj)/(max_Xj-min_Xj)     # operate on each item of column j 
```

**statistics**
```python

A = np.array([[1, 1, 10],
              [3, 5, 2]])

A.mean(axis=0)                                      # return mean on columns
A.sum(axis=0)                                       # return sum
A.std(axis=0)                                       # return standard deviation
A.min(axis=0)                                       # return min
A.max(axis=0)                                       # return max
A.argmin(axis=0)                                    # return index of min value
A.argmax(axis=0)                                    # return index of max value
```


### pandas
Library for manipulating and analyze data
[pandas website](https://pandas.pydata.org/docs/reference/index.html)

**DataFrame**
> Un DataFrame est une matrice (dont chaque ligne et chaque colonne porte un indice) 
> qui sert à stocker des bases de données.
> La colonne contenant les numérotations des lignes est appelée l'index
> et ne se gère pas de la même façon qu'une colonne du dataset

Indexation :
- par défaut (numéros des lignes)
- une des colonnes du DataFrame
- liste que l'on définit nous-même

Différence avec array Numpy
- un DataFrame est beaucoup plus lisible
- le type des éléments peut varier
- La classe DataFrame contient davantage de méthodes pour la manipulation et le pré-traitement de bases de données

**create df**
```python
import pandas as pd                             # import pandas with alias pd
pd.DataFrame(data, index, columns, ...)         # data = np.array/liste/dict/pd.DataFrame

dictionnaire = {"Produit"          : ['miel', 'farine', 'vin'],
                "Date d'expiration": ['10/08/2025', '25/09/2024', '15/10/2023'],
                "Quantité"         : [100, 55, 1800], 
                "Prix à l'unité"   : [2, 3, 10]}
df = pd.DataFrame(dictionnaire)                 # load data from a dictionary

# load from multipule existing list
df = pd.DataFrame(list(zip(titre_SC,annee_sortie_SC,note_SC)), 
                  columns=["Titre","Annee_sortie_SC","Note_SC"])


df = pd.read_csv(filepath_or_buffer,            # load data with CSV
                 sep = ',',                     # Add ?raw=true at the end of the https:// filename if it fails
                 header = 0,
                 index_col = 0)
                 
                 
pd.set_option('display.max_columns', None)      # set this to see all the columns at a time           
```

**overview of df**
```python
df.dtypes                                       # return columns type 
df.info()                                       # columns infos
pd.to_datetime(df['date_operation'])            # convert column to date type
df.describe()                                   # for the whole dataset
df['col'].value_counts()                        # Counting unique categorical variable. must be done on one column
df['col'].value_counts(dropna=False)            # Counting occurences as well as missing values
df['col'].value_counts(normalize=True)          # get the relative frequency
df.head()                                       # display first rows (5 by default)
df.tail()                                       # display last rows (5 by default)
df.columns                                      # return a list of column
df.columns = [col.lower().replace(" ","_")      # lower column name and replace ' ' by '_'
                for col in df.columns]
df.shape                                        # return a tuple of the shape
len(df)                                         # number of rows
len(df.columns)                                 # number of columns
df.size                                         # number of elements

pd.crosstab(index=df['col1'],                   # table with number of rows containing both item from col1 
            columns=df['col2'],                 # and item from col2
            rownames=None, colnames=None        # name of index and column for the new table
            margins=False,                      # margins count the total amount of one row or column
            margins_name="Total",               #
            dropna=True,                        # 
            normalize=False)                    # percentage of time each combination occurs
                                                # - all or True: from total population,
                                                # - index : will normalize over each row
                                                # - column : will normalize over each row

pd.crosstab(df['col1'],
            [df['col7'],df['col4'],])
```
**statistics**
```python
df.select_dtypes(include='number')              # select only numerical features in df
df.select_dtypes(include='O')                   # select only string features in df
df.mean()                                       # df mean
df.median()                                     # df median
df['col'].quantile(q=[0.25,0.5,0.75])           # col quantiles 
df['col'].std()                                 # col std
df['col'].between(int1,int2).astype(int)        # boolean true if value in col is between int1 and int2 (cast as int)

pd.qcut(df['col'], 4, labels=['q1', 'q2', 'q3', 'q4'])  # Discretize variable into equal-sized buckets based on rank or based on sample quantiles
```

**Select/locate**
Lorsque nous préparons un jeu de données pour l'exploiter plus tard, 
il est préférable de séparer les variables catégorielles des variables quantitatives
```python
# new dataframe df from df transactions
df = transactions['cust_id']                    # extract one column
df = transactions[["cust_id","Qty"]]            # extract multiple column

# select rows from a df with loc (multiple  results if index not unique)
df.loc[index]                                   # index can be list of index or slicing (indexes must be unique in that case)
df.loc[[idx1, idx2, ...]]  
df.loc[[indexrows][columns]]                    # columns to extract
df.loc[(df['col'] == 'toto'),'col']='new_val'   # replace value based on conditions                 

# select rows from a dataframe with iloc (like for a numpy array)
df.iloc[0:4, 0:3]                               # only with numerical index of rows and columns

df1 = df[df.columns[:4]]                        # select first 4 column [0..3]
df2 = df[df.columns[4:]]                        # select from 4th column until last [4..n]
```

**Conditionnal indexing of df**
```python
# 2 way:
df[df['col 2'] == 3]                            # return only a copy. cannot be used for assignment
df.loc[df['col 2'] == 3]                        # must be used if assignment


df[~(df['col']) > 1]                            # not ~
df[(df['col'] < -1) | (df['col'] > 2)]          # or |
df[(df['col'] > -1) & (df['col'] < 2)]          # and &
```

**transform**
```python
df.duplicated()                                 # show duplicates
df.replace('AUS', 1)                            # replace each item 'AUS' with 1
df.loc[(df['col'] == 'toto'),'col']='new_val'   # replace value based on conditions  
df.rename({'old_name': 'new'}, axis = 1)        # rename column 'old_name' with 'new' 
df = df.astype({'col': 'int'})                  # change column type of 'col' to 'int'
df['col'] = df['col'].astype('int')             #
df['col'] = pd.to_numeric(df["col"],errors='X') # convert col type to numeric (float64 or int64 depending on the data supplied) X = 'raise', 'ignore', 'coerce'
df.drop(['price'], axis = 1)                    # remove 'price' column
df = df.drop(df[(df.col == 50) &                # remove lines where col = 50 and col2 = toto
                (df.col2 == 'toto')].index)     # 
df['col1'].apply(func1)                         # apply func1 to every item of col1

# Pay attention with following
df.set_value('row', 'col', value)               # set value to [row,col] item
df.at['row', 'col'] = value                     # set value to [row,col] item

s.str.len()                                     # length of each string element  
s.str.upper()                                   # uppercase letters
s.str.lower()                                   # lowercase letters
s.str.capitalize()                              # Uppercase first letter
s.str.swapcase()                                # swap upper to lower and vice versa
s.str.title()                                   # Uppercase first letter of each word
s.str.strip('%')                                # remove '%' from right and left of s
s.str.join('-')                                 # concatenate list element in Series with '-'. NaN if one element is not a string
s.str.split(',', n=1, expand=True)              # expand lets the split values in separate column
    
# remove accents from column 'Titre'
df["Titre"] = df["Titre"].str.normalize('NFKD').str.encode('ascii', errors='ignore').str.decode('utf-8')

list(df.itertuples(index=False, name=None))     # returns list of tuples (as row of df)

# discretisation
test_gre = pd.cut(x = df['gre'],
                  bins = [200, 450, 550, 620, 800],
                  labels = ['mauvais', 'moyen', 'moyen +', 'bon'])

# dichotomisation / one hot encoding
one_hot = pd.get_dummies(df_items["subtype"], dtype=int, drop_first=False)
df_items_one_hot = df_items.join(one_hot)



```

**missing values**
```python

# detection
df.isna()                                       # return a df with True or false for each value
df.isna().any(axis = 0)                         # columns with at least 1 NaN return true
df.isna().any(axis = 1)                         # rows with at least 1 NaN return true
df[df.isna().any(axis = 1)]                     # conditionnal indexing to return only rows with NaN
df.isnull().sum(axis = 0)                       # number of NaN by column
df.loc[df['col'].isnull(),:]                    # show rows of NaN for 'col'

# Adding missing values
df.loc[[1, 3, 44, 99, 103], ['cp']] = np.NaN    # add 5 NaN in column 'cp'
df.iloc[[1, 3, 44, 99, 103], 12] = np.NaN       # add 5 NaN in 13th column

# replacement   
df.fillna(0)                                    # replace all NaN with 0
df.fillna(df.mean())                            # replace all NaN with df mean (could be median, min,max...)
df['col'].fillna(-1)                            # replace NAN of 'col' by -1
df['col'].mode()[0]                                # mode of'col'
df['col'].fillna(df['col'].mode()[0])           # replace NAN of 'store_type' by his mode
df['col'] = df['col'].replace(np.nan, 0)        # replace NaN of column 'col' by 0
    
# remove    
df.dropna(axis = 0, how = 'any')                # remove rows if at least 1 NaN in the row
df.dropna(axis = 1, how = 'all')                # remove columns if all NaN in the column
df.dropna(axis = 0, how = 'all',                # remove rows if all NaN in the 3 columns
          subset = ['col2','col3','col4'])  
``` 
    
**processing**  
```python   
    
# merge 
pd.concat([df1,df2], axis = 1)                  # concat df1 and df2 horizontally and fill with NaN if not same number of rows
df1.merge(right = df2,                          # right join df1 and df2 on 'col'
          on = 'col', how = 'right')    
df.set_index('Nom')                             # set new index for df with column 'Nom'
df.reset_index()                                # reset default index
df.reset_index(drop=True)                       # reset default index 
df.index                                        # get index of df

# sort
df.sort_values(by = 'col', ascending = True)
df.sort_values(by = ['col1', 'col3'], ascending = True)

# group, agg
functions_to_apply = {
    'col1' : ['min', 'max', 'sum'],
    'col3' : func1
    }
df.groupby('col').agg(functions_to_apply)
df.groupby(['nom_dept']).agg({'count':['sum','mean']})
df.groupby('UTC_Offset').count().sort_values(by='IATA_Airport',ascending=False)[['IATA_Airport']]

# nomalization
normalized_df=(df-df.mean())/df.std()           # mean normalization
normalized_df=(df-df.min())/(df.max()-df.min()) # min-max normalization

```

**plot**
```python
# Diagramme en secteurs
data["categ"].value_counts(normalize=True).plot(kind='pie')
# Cette ligne assure que le pie chart est un cercle plutôt qu'une éllipse
plt.axis('equal') 
plt.show() # Affiche le graphique

# Histogramme
data["montant"].hist(density=True)

# Histogramme plus beau (bin optimal k=[1+log2(n)])
data[data.montant.abs() < 100]["montant"].hist(density=True,bins=20)


```

**evaluate**

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, confusion_matrix

accuracy_score(y_test, y_pred_test)
precision_score(y_test, y_pred_test)


(VN, FP), (FN, VP) = confusion_matrix(y_test, y_pred_test_logr)

pd.crosstab(df['col1'],df['col5'])              # display table with frequency of modality
pd.crosstab(df['col1'],df['col5'],normalize=1)  # display by percentage in the column direction

```

### scipy
```python
from scipy.stats import pearsonr

pearsonr(df['backers'], df['pledged'])          # coefficient de pearson (2 quantitative values)



```
---
### geopandas
```python
import geopandas as pd
import contextly as ctx  # retrieves tile maps from the internet as basemaps for matplotlib 

ctx.add_basemap(ax, crs = meuse.crs.to_string())


```

---
### folium
```pyhton
import folium
map_osm = folium.Map(location=[location.latitude, location.longitude])

for ind, geo, com in df[['geometry', '1_f_commune']].itertuples():
    map_osm.add_child(folium.RegularPolygonMarker(location=[geo.y,geo.x], popup=com,
                       fill_color='#132b5e', radius=5))

map_osm

```

---
### geopy
```python
from geopy.geocoders import Nominatim

# Initialize Nominatim API
geolocator = Nominatim(user_agent="MyApp")

# City as Input
location = geolocator.geocode("Nancy")
print("The latitude of the location is: ", location.latitude)
print("The longitude of the location is: ", location.longitude)

# Latitude & Longitude as Input
coordinates = "17.3850 , 78.4867"
location = geolocator.reverse(coordinates)
city = address.get('city', '')
state = address.get('state', '')
country = address.get('country', '')
```
---
### time
```python
import time

time.time()                                     # Return the time in seconds since the epoch as a floating point number 
                                                # Epoch time on Windows and most Unix : January 1, 1970, 00:00:00 (UTC) 

time.strftime('%X')                             # displays 17:13:52
time.sleep(5)                                   # sleep for 5 sec
time.ctime()                                    # take time in seconds and return 'Sun Jun 20 23:21:05 1993'
time.gmtime(1561541)                            # Convert a time expressed in seconds since the epoch to a struct_time in UTC

```
### datetime
**formats**
%d Day of the month as a zero-padded decimal number.    01, 02, …, 31
%b Month as locale’s abbreviated name.                  Jan, Feb, …, Dec (en_US);
%m Month as a zero-padded decimal number.               01, 02, …, 12
%y Year without century as a zero-padded decimal.       00, 01, …, 99
%Y Year with century as a zero-padded decimal.          2012, 2013, …, 9999
%H Hour (24-hour clock) as a zero-padded decimal.       00, 01, …, 23
%M Minute as a zero-padded decimal number.              00, 01, …, 59
%S Second as a zero-padded decimal number.              00, 01, …, 59
%W Week number of the year (Monday as the first DoW)    00, 01, ..., 53

```python
from datetime import datetime, timedelta

datetime.now()                                  # current date and time
datetime.today()                                # today date

day=datetime.now().strftime("%d")               # 19
month=str(datetime.now().strftime("%b"))        # Oct
year=datetime.now().strftime("%y")              # 22

end_date = datetime.now() + timedelta(days=7)

date_minus_2d = (datetime.now() - timedelta(days=2)) \      # renvoi string ajd - 2jrs formaté
        .strftime("%Y-%m-%dT%H:%M:%S.%f")[:-3] + "Z"

```


### Matplotlib

```python
%matplotlib inline                              # magic function for IPython to choose graphical library (inline = Notebook internal library)
import matplotlib.pyplot as plt

fig = plt.figure()                              # figure container (axes, labels, data, etc..)
ax = plt.axes()                                 # grid above figure
x = np.linspace(0, 10, 1000)
ax.plot(x, np.sin(x));
plt.figure(figsize= (h, l))                     # resize figure

fig, axes = plt.subplots(nrows=1,
                         ncols=2, 
                         figsize=(16, 8)) # display multiple subplots at once 


plt.plot(t,t,'hy')
plt.plot(t,t**2,'g-', linewidth=5)
plt.plot(t,t**3,'b', marker='D')
plt.xlim([0,50])
plt.ylim([0,50])
plt.xlabel('Abscisses')
plt.ylabel('Ordonnees')
plt.title("Un exemple de graphe")               # graph title
plt.axis([-1, 11, -1.5, 1.5]);                  # axis limit x(min,max) and y(min,max)
df = pd.read_csv('sales_data.csv')
plt.plot(df['Month'],df['Product1'])
df.plot(x='Month', y='Prod1', title = "Ventes")
df.plot(x = 'Month', y = ['Product1','Product2'], style = ["m--", "c:."], title = "Ventes par mois");

#############
# graph types
plt.plot(x, np.sin(x - 0),                      # x and y (function)
        color='blue',                           # color (can be : 'blue', 'g', '0.75', '#FF0000')
        linestyle='solid',                      # linestyle ('solid','dashed', 'dashdot', 'dotted')
        label='bleu')                           # legend
plt.bar(x,y,width=1,edgecolor="white")          # bar plot
plt.step(x,y)                                   # step plot
plt.scatter(x,y)                                # scatter plot
plt.errorbar(x, y, yerr=dy, fmt='.k')           # when discrete value, plot error of value (often standard deviation)
plt.show()                                      # Display graph

###########
# bar plots
plt.bar(range(4), [2, 3, 4, 5] , color = 'green', width = 0.6)
plt.bar(x, y2, bottom = y1)                     # superpose les barres
plt.xticks([1,2,3], ['un', 'deux', 'trois'])    # replace 1,2,3 by 'un'... on abscisses axis
df.plot.bar(x = 'Month', y=['Product1', 'Product2', 'Returns'],stacked=True,rot=0)

###############
# scatter plots
plt.scatter(range(0,7), [8,7,6,5,6,7,8], color='red', marker= '*', s=40)

###########
# histogram
plt.hist([0,1,1, 2, 2, 2, 3, 4, 4, 4, 4, 4, 5, 5], range=(0, 6), bins = 6)
plt.hist([0,8,10,13,15,16,16,18,32,36,39,40,43,45,48,49], bins = [0,10,20,40,50])
plt.hist(x, range = (1, 6), 
            bins = 5, 
            color = '#EE3459',
            density = True,
            orientation = 'horizontal', 
            rwidth = 0.6)
plt.hist([df.Product1, df.Product2], 
            bins = 6, color = ['#f27750', '#f7bf59'],
            label = ['Product1', 'Product2'],
            histtype = 'barstacked')           
            
df.plot.hist(y=['Product1', 'Product2'], bins = 7, rwidth = 0.8 , color= ['#0c4c83', '#830c4c'], alpha=0.5);
df.plot.hist(y=['Product1', 'Product2'], bins = 7, subplots=True, rwidth = 0.8 , color= ['#0c4c83', '#830c4c'], alpha=0.5);
df.hist(column=['Product1', 'Product2'], bins = 7, rwidth = 0.8 , color= ['#0c4c83']);
   
###########
# box plots
plt.boxplot([[1, 2, 3, 4, 5], [7, 5, 8, 4, 9, 5, 7]])


df['Mois']= df.Month.apply(lambda x : x[3:])
l=list()
for i in df.Mois.unique():
    l.append(df[df['Mois'] == i]['Turnover'])
plt.boxplot(l)
plt.xticks(range(1,13),df.Mois.unique())
plt.show()


df.boxplot(column= 'Turnover', by='Mois', figsize= (7,7));   

############ 
# Pie Charts       
plt.pie(x, labels = ['A', 'B', 'C', 'D', 'E'])

plt.pie(x = df.head(6).Turnover, 
           labels = ['Janv', 'Fev', 'Mars'],
           colors = ['red', 'orange', 'yellow'],
           explode = [0, 0, 0.2],                       # extract on part
           autopct = lambda x: str(round(x, 2)) + '%',  # format percentage
           pctdistance = 0.7, labeldistance = 1.2,      # distance from center to display percentage
           shadow = True)                               # with shadow or not


# subplots
plt.subplot(221)
plt.bar(range(len(df)), df.Product1, label = 'Product1')
plt.legend()

plt.subplot(222)
plt.scatter(df.Product1, df.Product2, c = 'm', label = "Product2")
plt.legend()

df.plot(y = ['Product1', 'Product2', 'Returns', 'Turnover'], subplots=True, layout= (2,2),
        style = ['b--', 'm:p', 'g-.', 'c-d'], figsize=(7,7));
    
plt.figure(figsize = (7,7))
plt.boxplot(df.Turnover)
plt.title( 'Boxplot')
plt.axes([0.65, 0.65, 0.2, 0.15], facecolor='#ffe5c1')
plt.hist(df.Turnover, color='#FFC575')
plt.xlabel('Distribution')
plt.xticks([])
plt.yticks([]);

################
# figure et axes
fig = plt.figure(figsize=(8,4))
ax1 = fig.add_subplot(121)
ax2 = fig.add_subplot(122)
ax1.plot([0, 2, 3], [1, 3, 2], 'green');
ax2.hist( [1, 2, 2, 2, 3, 3, 4, 5, 5]);

t = ax.set_title('random numbers')

ax3 = fig.add_subplot(223, sharex=ax1)
ax4 = fig.add_subplot(224, sharex=ax2)

fig,axes = plt.subplots(3,2,sharex=True,sharey=True)
for i in range(2):
    for j in range(2):
        axes[i,j].hist(np.random.randn(500), bins=50, color='black', alpha=0.5)

ax1.plot(s1,color='#33CCFF',marker='o',linestyle='-.',label='courbe 1')
ax1.set_xlim([0,21])
ax1.set_ylim([-15,15])

ax1.set_xticks(range(0,21,2))
ax1.set_xticklabels(["j +" + str(l) for l in range(0,21,2)])
ax1.set_xlabel('Durée après le jour j')
ax1.legend(loc='best')

ax1.plot_date(dates, val, linestyle='-');

########
# LateX
ax.text(0.1, 0.5, r"$ f(x,y) = x^2 + 3 \times \cos(y) $", fontsize=22)
ax.set_title('$\sin(2\pi x)\exp(-x)$ et les deux asymptotes $\pm\exp(-x)$')

###############
# contour plots

x , y = np.linspace(-1,1,200), np.linspace(-1,2,200)
X, Y = np.meshgrid(x,y)
Z = (1-X)**2+(Y-X**2)**2
cs = plt.contour(X,Y,Z)
plt.clabel(cs);
plt.contourf(X,Y,Z,20)
plt.colorbar()

############
# polar plot
theta = np.arange(0., 2., 1./180.)*np.pi 
r = np.abs(np.sin(5*theta) - 2.*np.cos(theta))
plt.polar(theta, r)
plt.rgrids(np.arange(0.2, 3.1, .7), angle=0)
plt.thetagrids(np.arange(45, 360, 90) );

ax = plt.subplot(111, projection='polar')

########
# images

heart = plt.imread('heartbeat.png') 
plt.imshow(heart);

# ajouter une image à un graphique
import pandas as pd
hb=pd.read_csv('hb.csv', header=None)
plt.figure(figsize=(8,6))
plt.ylim([0,140])
plt.xlim([-2,260])
plt.plot(hb)
plt.text(95,130,'Electrocardiogramme', style='italic')
plt.imshow(heart, extent = [80,170,60,140]) ;

```

### dash plotly

When to use Graph Objects
https://plotly.com/python/graph-objects/

```python

```



### sockets
```
accept()                                    # accepte une connexion, retourne un nouveau socket et une adresse client 
bind(addr)                                  # associe le socket à une adresse locale
close()                                     # ferme le socket
connect(addr)                               # connecte le socket à une adresse distante 
connect_ex(addr)                            # connect, retourne un code erreur au lieu d'une exception
dup()                                       # retourne un nouveau objet socket identique à celui en cours
fileno()                                    # retourne une description du fichier
getpeername()                               # retourne l'adresse distante
getsockname()                               # retourne l'adresse locale
getsockopt(level, optname[, buflen])        # retourne les options du socket
gettimeout()                                # retourne le timeout ou none
listen(n)                                   # commence à écouter les connexions entrantes
makefile([mode, [bufsize]])                 # retourne un fichier objet pour le socket
recv(buflen[, flags])                       # recoit des données
recv_into(buffer[, nbytes[, flags]])        # recoit des données (dans un buffer)
recvfrom(buflen[, flags])                   # reçoit des données et l'adresse de l'envoyeur
recvfrom_into(buffer[,nbytes,[,flags])      # reçoit des données et l'adresse de l'envoyeur (dans un buffer)
sendall(data[, flags])                      # envoye toutes les données
send(data[, flags])                         # envoye des données mais il se peut que pas toutes le soit
sendto(data[, flags], addr)                 # envoye des données à une adresse donnée
setblocking(0 | 1)                          # active ou désactive le blocage le flag I/O
setsockopt(level, optname, value)           # définit les options du socket
settimeout(None | float)                    # active ou désactive le timeout
shutdown(how)                               # fermer les connexions dans un ou les deux sens.
```

### requests

```python
import requests
r = requests.get('https://api.github.com/events')
r = requests.post('https://httpbin.org/post', data={'key': 'value'})
r = requests.put('https://httpbin.org/put', data={'key': 'value'})
r = requests.delete('https://httpbin.org/delete')
r = requests.head('https://httpbin.org/get')
r = requests.options('https://httpbin.org/get')

url = "https://..."
response = requests.request("GET", url, headers=headers, data=payload)
response.json()['key1']['key2']

```

### other librairies

```python
matplotlib                          # plot graphs
statistics                          # deep into statistics 
sklearn                             # machine learning
Beautiful Soup                      # Web Scraping static
Selenium                            # Web Scraping dynamic
csv                                 # work with CSV files
re                                  # regex manipulation      
math                                # all math functions (cosinus,sinus,exp,etc.)
sys                                 # sytem functions
os                                  # OS functions
calendar                            # calendar functions
profile                             # analyse function execution
urllib2                             # get internet informations
cv2                                 # computer vision
```
### How to use a library
```python
import random as rd
from randam import choices as ch
```

---
# DOMAIN SPECIFIC

## WEB SCRAPING

### BeautifulSoup

**methods**
```python
pip install beautifulsoup4
from bs4 import BeautifulSoup

# beautifulsoup
soup.title                                              # <title>The Dormouse's story</title>
soup.title.name                                         # u'title'
soup.title.string                                       # u'The Dormouse's story'
soup.p                                                  # <p class="title"><b>The Dormouse's story</b></p>
soup.p['class']                                         # u'title'
soup.title.parent.name                                  # u'head'
soup.head.contents                                      # # [<title>The Dormouse's story</title>]
soup.prettify                                           # align text
soup.get_text()                                         # get all the text in the page
soup.find_all('a')                                      # find all <a> element in the page
soup.find(id="link3")
soup.select("title")                                    # find tags
soup.select("body a")                                   # Find tags beneath other tags (a beneath body)
soup.select("head > title")                             # Find tags directly beneath other tags
soup.select("p > a")                                    # 
soup.select("#link1 ~ .sister")                         # Find siblings tags
soup.select(".sister")                                  # Find tags by CSS class
soup.select("[class~=sister]")                          #
soup.select("#link1")                                   # Find tags by ID
soup.select("#link1,#link2")                            # Find tags that match any selector from a list of selectors
soup.select('a[href="http://example.com/elsie"]')       # Find tags by value

# selenium
# for Colab
!pip install selenium
!apt-get update # to update ubuntu to correctly run apt install
!apt install chromium-chromedriver
!cp /usr/lib/chromium-browser/chromedriver /usr/bin
import sys
sys.path.insert(0,'/usr/lib/chromium-browser/chromedriver')
from selenium import webdriver
chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--no-sandbox')
chrome_options.add_argument('--disable-dev-shm-usage')
wd = webdriver.Chrome('chromedriver',options=chrome_options)
wd.get("https://www.webite-url.com")

# googlesearch
pip install googlesearch                                # pip installation
conda install -c conda-forge googlesearch               # conda installation
search(requête,                                         # (str) la requête que vous voulez exécuter 
       tld='com',                                       # (str) le domaine
       lang='en',                                       # (str) le langage
       tbs='o',                                         # (str) Time limits (i.e “qdr:h” => last hour, “qdr:d” => last 24 hours, “qdr:m” => last month).
       num=10,                                          # (int) nombre de résultat par page
       start=0,                                         # (int) premier résultat à récupérer
       stop=None,                                       # (int) dernier resultat à récupérer. (None = forever)
       pause=2.0,                                       # (float) delai entre les demandes HTTP
      ):
lucky(*args, **kwargs)                                  # Shortcut to single-item search. Same arguments as the main search function, but the return value changes. 
get_tbs(from_date, to_date)                             # Helper function to format the tbs parameter


# NewsPaper
pip install newspaper3k                                 # pip installation
from newspaper import Article
article = Article(url)
article.download()
article.parse()
article.text

# nltk
pip install nltk                                        # pip installation
nltk.download('punkt')                                  # installation package punkt
article.nlp()                                           # make NLP work on 'article'
article.authors                                         # return name of authors
article.publish_date                                    # return published date
article.summary                                         # return summary
article.keywords                                        # return keywords
article.top_image                                       # return top image
article.movies                                          # return 



```

**interpreter example**
```python
pip install beautifulsoup4

# Récupération du titre de la page HTML
>> soup.title
<title><Les chiens les plus mignons></title>

# Récupération de la chaîne de caractères du titre HTML
>> soup.title.string
"Les chiens les plus mignons"

# Trouver tous les éléments avec la balise <a>
>> soup.find_all('a')
[ <a href="http://exemple.com/labradoodle" class="race" id="lien1">LabraDoodle</a>,
<a href="http://exemple.com/retriever" class="race" id="lien2">Golden Retriever</a>,
<a href="http://exemple.com/carlin" class="race" id="lien3">Carlin</a>]

# Trouver les éléments avec l’id du « lien1 »
>> soup.find(id="lien1")
<a href="http://exemple.com/labradoodle" class="race" id="lien1">LabraDoodle</a>

#Trouver tous les éléments p avec la classe « title »
>> soup.find_all("p", class_="title")
"Les meilleures races de chiens"
```

**script example**
```
# 1
import requests
from bs4 import BeautifulSoup
url = "https://www.gov.uk/search/news-and-communications"
page = requests.get(url)
soup = BeautifulSoup(page.content, 'html.parser')

# 2
from urllib.request import urlopen
from bs4 import BeautifulSoup
page_SC = urlopen("https://www.gov.uk/search/news-and-communications")
soup = BeautifulSoup(page_SC, 'html.parser')

# 3
from bs4 import BeautifulSoup
from urllib.request import Request, urlopen
headers = {'User-Agent': 'Mozilla/5.0'}
url = 'https://www.nationsonline.org/oneworld/IATA_Codes/IATA_Code_A.htm'
response = Request(url, headers = headers)
page = urlopen(response)
soup = BeautifulSoup(page, 'html.parser')

titres = soup.find_all("a", classstrip_="gem-c-document-list__item-title")
for title in titres:
    print(title.string,"\n")

# trouve le nom aux balises <a> et classes 'elco-anchor'
noms_SC = soup.findAll(name = 'a', attrs = {'class': 'elco-anchor'})
    
    
    
# Ouvrir fichier avec le package CSV
import csv

with open('couleurs_preferees.csv') as fichier_csv:
   reader = csv.DictReader(fichier_csv, delimiter=',')
   for ligne in reader:
      print(ligne['nom'] + " travaille en tant que " + ligne['metier'] + 
      " et sa couleur préférée est " + ligne['couleur_preferee'])
      `
```




---
# DATA CLEANING

**purpose**
- have a clean dataset to manipulate
- manage missing values (NaN)

**3 categories of transformation**
- manage duplicates *(duplicated, drop_duplicates)*
- modify elements *(replace, rename, astype)*
- operations on DF values *(apply, lambda)*

## duplicates
```python
df.duplicated()
df.duplicated().sum()
df.loc[df[['col1','col2']].duplicated(keep=False),:].sum()      # select all duplicates on columns col1 and col2
df.drop_duplicates(subset=None, keep=first, inplace=False)      # be carful with inplace. let False by default
```

## replacing
```python
df.replace(to_replace, value, ...)

# column renaming
dictionnaire = {'ancien_nom1': 'nouveau_nom1',
                'ancien_nom2': 'nouveau_nom2'}
df = df.rename(dictionnaire, axis = 1)

# change column type 
# Méthode 1 : 
dictionnaire = {'col_1': 'int',
                'col_2': 'float'}
df = df.astype(dictionnaire)
# Méthode 2 : 
df['col_1'] = df['col_1'].astype('int')
```

## operations on values
**apply**
df.apply(func, axis, ...)
```python
# define a function
def get_day(d):
    return d.split('-')[0]
# apply function to column 
days = transactions['tran_date'].apply(get_day)
# create a new column
transactions['day'] = days
```

**lambda**
in combination with *apply*
```python
# normal function
def increment(x): 
   return x+1
# with lambda  
increment = lambda x: x+1

# combining lambda and apply
transactions['day'] = transactions['tran_date'].apply(lambda date: date.split('-')[0])
transactions['prod_cat'] = transactions.astype('str').apply(lambda row: row['prod_cat_code']+'-'+row['prod_subcat_code'],
                                                            axis = 1)
```

## missing values
- detection *(isna,any)*
- replacement *(fillna)*
- remove *(dropna)*

**detection**
```python

df.isna()                                   # return a df with True or false for each value
df.isna().any(axis = 0)                     # columns with at least 1 NaN
df.isna().any(axis = 1)                     # rows with at least 1 NaN
df[df.isna().any(axis = 1)]                 # conditionnal indexing to return only rows with NaN
df.isnull().sum(axis = 0)                   # number of NaN by column
```

**replacement**
- variable of numerical type are often replaced with 
    - mean
    - median
    - min/max
- variable of categorical type are often replaced with 
    - mode
    - arbitrary constante (0, -1)

Be careful to select the right column to replace NaN

**fillna**

```python

df.fillna(0)                                # replace NaN with 0
df.fillna(df.mean())                        # replace NaN with column mean (could be median, min,max...)

# On remplace les NANs de 'prod_subcat_code' par -1
transactions['prod_subcat_code'] = transactions['prod_subcat_code'].fillna(-1)

# On détermine le mode de 'store_type'
store_type_mode = transactions['store_type'].mode()

# On remplace les NANs de 'store_type' par son mode
transactions['store_type'] = transactions['store_type'].fillna(transactions['store_type'].mode()[0])

# On vérifie que ces deux colonnes ne contiennent plus de NANs
transactions[['prod_subcat_code', 'store_type']].isna().sum()

# voir les NaN d'une colonne
customer.loc[customer['city_code'].isnull(),:]

```

**dropna**
removes rows or columns
dropna(axis, how, subset, ..)
- axis : 0 remove rows or 1 remove columns
- how : 'any' at least 1 NaN or 'all' all NaN
- subset : indicates rows/columns in which we search for NaN

```python
df = df.dropna(axis = 0, how = 'any')
df = df.dropna(axis = 1, how = 'all')
df = df.dropna(axis = 0, how = 'all', subset = ['col2','col3','col4'])
```

---
# DATA PROCESSING

**filter, merge, sort et group**

## Filter (indexation conditionnelle)
- 'et' : &
- 'ou' : |
- 'non' : -

```python

# &
print(df[(df['annee'] == 1979) & (df['surface'] > 60)])
# |
print(df[(df['année'] > 1900) | (df['quartier'] == 'Père-Lachaise')])
# -
print(df[-(df['quartier'] == 'Bercy')])
```

## Merge df with concat and merge

### concat
pandas.concat(objs, axis..)
- **obj** : list of df
- **axis** : 0 (verticaly) ou 1 (horizontally)

if dimensions don't match, fill with NaN
```python
part_1 = transactions[transactions.columns[:4]]
part_2 = transactions[transactions.columns[4:]]
union = pd.concat([part_1,part_2], axis = 1)
```

### merge
2 df can be merge if 1 column in common
merge(right, on, how, ...)
- **right** : df to merge on the right with the one calling merge
- **on** : shared column
- **how** : joint (based on SQL)
    - **'inner'**: Default. Not recommended because of data loss but no NaN
    - **'outer'**: Keep all data but generate lot of NaN
    - **'left'** : all left data but only the right that match. Data loss and generate NaN
    - **'right'**: all right data but only the left that match. Data loss and generate NaN

> make a outer/right/left joint with dropna(how = 'any') is equivalent to inner joint

> pay attention to index column that can change or be removed.

```python
# example
Personnes.merge(right = Vehicule, on = 'Voiture', how = 'right')

# set new index for df with column name
df = df.set_index('Nom')

# new index from numpy array or pandas series
new_index = ['10000' + str(i) for i in range(6)]
index_array = np.array(new_index)
index_series = pd.Series(new_index)
df = df.set_index(new_index)
df = df.set_index(index_array)
df = df.set_index(index_series)

# reset default index
df = df.reset_index()

# get index of df
df.index
```

## Sort
sort_values(by, ascending,...)
- by : column to sort
- ascending : (True or False) True by default

```python
df_sorted = df.sort_values(by = 'Points_bonus', ascending = True)
df_sorted = df.sort_values(by = ['Points_bonus', 'Note'], ascending = True)
```

sort_index()
often combined with set_index()

```python
# On définit la colonne 'Note' comme l'index de df
df = df.set_index('Note')
# On trie le DataFrame df selon son index
df = df.sort_index()
```

## group, agg

**groupby** : return a DataFrameGroupBy
operations:
- **split** data
- **apply** function
- **combine** results

**agg** : aggregate data
- dictionary :
    - key : column name
    - value : function to apply

```python
functions_to_apply = {
    # Les méthodes statistiques classiques peuvent être renseignées avec
    # chaines de caractères
    'total_amt' : ['min', 'max', 'sum'],
    'store_type' : n_modalities
    }  
   
transactions.groupby('cust_id').agg(functions_to_apply)

# example
# Quantité maximale
max_qty = lambda qty: qty[qty > 0].max()
# Quantité minimale
min_qty = lambda qty: qty[qty > 0].min()
# Quantité médiane
median_qty = lambda qty : qty[qty > 0].median()
# Définition du dictionnaire de fonctions à appliquer
functions_to_apply = {
    'qty' : [max_qty, min_qty, median_qty]
}
# Operation groupby
qty_groupby = transactions.groupby('cust_id').agg(functions_to_apply)
# Pour un meilleur affichage, on peut renommer les colonnes produite par le groupby
qty_groupby.columns.set_levels(['max_qty', 'min_qty', 'median_qty'], level=1, inplace = True)

```

## crosstab
frequency of modality pairs 
crosstab(colonne1, colonne2, normalize = 1)
- normalize : display percentage  (0:rows, 1:columns) 

```python
colonne1 = transactions['prod_cat_code']
colonne2 = transactions['prod_subcat_code']
pd.crosstab(colonne1, colonne2)


```


---
# EDA
```python

# select country not in subset of valid countries to replace by NaN values
VALID_COUNTRIES = ['France', 'Côte d\'ivoire', 'Madagascar']
mask = ~data['pays'].isin(VALID_COUNTRIES)
data.loc[mask, 'pays'] = np.NaN



```

---
# MACHINE LEARNING : Regression

## ****Régression Linéaire Univariée****

y≈β1x+β0

y = target
x = feature
β = paramètre

## ****Régression Linéaire Multiple****

y≈ β0 + β1x1 + β2x2 + ⋯ + βpxp

≈ β0 + ∑j=1p βjxj

## Problème

trouver les meilleurs β qui minimise l’erreur entre le modèle et les vraies valeurs

### **scikit-learn**

pour résoudre les problèmes de machine learning

## **Étapes** à la base de toute résolution d'un problème de Machine Learning :

- On prépare les données en **séparant** les variables **explicatives** de la variable **cible**.
- On **sépare** le jeu de données en deux (un jeu d'**entraînement** et un jeu de **test**) à l'aide de la fonction `train_test_split` du sous-module `sklearn.model_selection`.
- On **instancie** un modèle comme `LinearRegression` ou `GradientBoostingRegressor` grâce au constructeur de la classe.
- On **entraîne** le modèle sur le jeu de données d'entraînement à l'aide de la méthode **`fit`**.
- On effectue une **prédiction** sur les données de test grâce à la méthode **`predict`**.
- On **évalue les performances** de notre modèle en calculant l'erreur entre ces prédictions et les véritables valeurs de la variable cible des données de **test**.

### Separation colonnes features et target

```python
X = df[df.columns[:15]]
y = df[df.columns[15:]]

ou

# Variables explicatives
X = df.drop(['price'], axis = 1)
# Variable cible
y = df['price']
```

### Separate dataset between train and test dataset

- **train**: find the best β
- **test** : test the trained model to study his capacity to generalize predictions on data never seen befor
    
    ### train_test_split
    
    train_test_split(*arrays*, *test_size=None*, *train_size=None*, *random_state=None*, *shuffle=True*, *stratify=None*)
    
    [https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)
    
    ```python
    from sklearn.model_selection import train_test_split
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 20)
    ```
    
    **test_size** : proportion of test dataset
    
    **random_state :** 
    
    - **‘**None’ for different results for multiple calls.
    - Int for repeatible results

### Create a regression model

```python
from sklearn.linear_model import LinearRegression
```

All model class have 2 methods to train and evaluate model:

- **fit** : train model
- **predict** : predict results from features

```python
# Instantiation du modèle
lr = LinearRegression()

# Entraînement du modèle
lr.fit(X_train, y_train)

# Prédiction de la variable cible pour le jeu de données TRAIN
y_pred_train = lr.predict(X_train)

# Prédiction de la variable cible pour le jeu de données TEST
y_pred_test = lr.predict(X_test)
```

### Evaluate model

**Mean Squared Error**

difficult to interpret

```python
from sklearn.metrics import mean_squared_error
mean_squared_error(y_true = y_test, y_pred = y_pred_test)
```

**Mean Absolute Error**

same scale as target

```python
from sklearn.metrics import mean_absolute_error
mae_train = mean_absolute_error(y_train, y_pred_train)
```

## Overfitting

**GradientBoost** : learn well on train dataset but doesn’t generalize well

```python
gbr = GradientBoostingRegressor(n_estimators = 1000,
                                max_depth = 10000,
                                max_features = 15,
                                validation_fraction = 0)
# Fit
gbr.fit(X_train, y_train)
# Predict train
y_pred_train_gbr = gbr.predict(X_train)
# Predict test
y_pred_test_gbr = gbr.predict(X_test)

# MSE train
mse_train_gbr = mean_squared_error(y_train, y_pred_train_gbr)
# MSE test
mse_test_gbr = mean_squared_error(y_test, y_pred_test_gbr)

# MAE train
mae_train_gbr = mean_absolute_error(y_train, y_pred_train_gbr)
# MAE test
mae_test_gbr = mean_absolute_error(y_test, y_pred_test_gbr)

mean_price_gbr = df['price'].mean()

print("Relative error", mae_test_gbr / mean_price_gbr)

# Results #########################
# MSE train gbr: 25799.588888888888
# MSE test gbr: 2626919.693281389
# MAE train gbr: 32.718518524427424
# MAE test gbr: 1189.7782300506872
# Relative error 0.10394953190531596
```

For **regression** with **`LinearRegression`** we had :

- MAE train lr: 1680.4078748721086
- MAE test lr: 1773.9135394428085

For **regression** with **`GradientBoostingRegressor`** we have :

- MAE train gbr: 20.740740828767215
- MAE test gbr: 1442.6573741134125

**Mean absolute error** for **train** dataset is **too low** compare to **test** dataset **too high.** That ‘s why the performance of the model **must be** evaluated on **test dataset.**

**`GradientBoostingRegressor`** is better than **`LinearRegression`** though.

## ****Polynomiale Regression****

y = β0 + β1x + β2x^2

Order 2

y ≈ β0 + β1x1^2 + β2x2^2+ β3x3^2+ β4x1x2+ β5x2x3 + β6x1x3

When features grow or Order higher, it leads to **overfitting**

```python
from sklearn.preprocessing import PolynomialFeatures

poly_feature_extractor = PolynomialFeatures(degree = 2)

# Application de la transformation sur X_train et X_test
X_train_poly = poly_feature_extractor.fit_transform(X_train)
X_test_poly = poly_feature_extractor.transform(X_test)
```

**poly_feature_extractor** is a `transformer` not a model:

- **fit** : does nothing
- **transform** : apply transformation to dataset

these 2 methods can be replaced by **fit_transform**() directly

```python
# Instantiation d'un modèle de régression linéaire
polyreg = LinearRegression()

# Entraînement du modèle sur les features polynomiaux
polyreg.fit(X_train_poly, y_train)

# Evaluation du modèle sur les données d'entraînement
y_pred_train = polyreg.predict(X_train_poly)
print("MAE Train:", mean_absolute_error(y_train, y_pred_train), '\n')

# Evaluation du modèle sur les données de test
y_pred_test = polyreg.predict(X_test_poly)
print("MAE Test:", mean_absolute_error(y_test, y_pred_test), '\n')

print("Nous sommes absolument dans un régime de surapprentissage.")
print("Le modèle de régression polynomiale est performant sur les données d'entrainement mais pas sur les données de test.")
print("Le modèle de régression polynomiale d'ordre 3 est beaucoup moins performant que la régression linéaire simple.")
```

---

# MACHINE LEARNING : Classification

**Regression :** continuous values (numerical)

**Classification** : discrete values (numerical or litteral)

ex:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5815c037-ed75-4cf0-be92-307dc9366b70/Untitled.png)

Scikit-learn propose de nombreux modèles de classification que l'on peut regrouper en deux familles :

- Les modèles linéaires comme `**LogisticRegression**`.
- Les modèles **non-linéaires** comme **`KNeighborsClassifier`**.

L'utilisation de ces modèles se fait de la même façon pour **tous** les modèles de scikit-learn :

- **Instanciation** du modèle.
- **Entraînement** du modèle : **`model.fit(X_train, y_train)`**.
- **Prédiction** : **`model.predict(X_test)`**.

La prédiction sur le jeu de test nous permet d'**évaluer** la performance du modèle grâce à des **métriques** adaptées.

Les métriques que nous avons vues s'utilisent pour la classification **binaire** et se calculent grâce à 4 valeurs :

- Vrais Positifs : Prédiction = **+** | Réalité = **+**
- Vrais Négatifs : Prédiction = **-** | Réalité = **-**
- Faux Positifs : Prédiction = **+** | Réalité = **-**
- Faux Négatifs : Prédiction = **-**  | Réalité = **+**

Toutes ces valeurs peuvent se calculer à l'aide de la **matrice de confusion** générée par la fonction **`confusion_matrix`** du sous-module `**sklearn.metrics**` ou par la fonction **`pd.crosstab`**.

Grâce à ces valeurs, nous pouvons calculer des **métriques** comme :

- **L'accuracy** : La proportion d'observations correctement classifiées.
- La **précision** : La proportion de vrais positifs parmi toutes les prédictions positives du modèle.
- Le **rappel** : La proportion d'observations réellement positives qui ont été correctement classifiées positives par le modèle.

Toutes ces métriques peuvent s'obtenir à l'aide de la fonction  **`classification_report`** du sous-module **`sklearn.metrics`**.

Le **`F1-Score`** quantifie l'**équilibre** entre ces métriques, ce qui nous donne un critère **fiable** pour **choisir** le modèle le plus adapté à notre problème.

## Linear Classification ****: K-Nearest Neighbors****

for **K=5**, if **5 neighbors** are democrats, the observations **will be classified** as democrats

```python
from sklearn.neighbors import KNeighborsClassifier

# Instanciation du modèle
knn = KNeighborsClassifier(n_neighbors = 6)
# Entraînement du modèle sur le jeu d'entraînement
knn.fit(X_train, y_train)
# Prédiction sur les données de test
y_pred_test_knn = knn.predict(X_test)
# Affichage des 10 premières prédictions
print(y_pred_test_knn[:10])

# Results ############################################################
# array(['democrat', 'democrat', 'democrat', 'democrat', 'democrat',
#       'democrat', 'democrat', 'democrat', 'republican', 'democrat'],
#       dtype=object)
```

## Linear Classification ****: Logistic Regression****

Probability that y = 0 or 1

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/682c92ba-5f61-4e4f-8328-ff58cda6b287/Untitled.png)

f is called the **`sigmoïd function`** or **`logistic function`** 

```python
from sklearn.linear_model import LogisticRegression

# Instanciation du modèle
logreg = LogisticRegression()
# Entraînement du modèle sur le jeu d'entraînement
logreg.fit(X_train, y_train)
# Prédiction sur les données de test
y_pred_test_logreg = logreg.predict(X_test)
# Affichage des 10 premières prédictions
print(y_pred_test_logreg[:10])

# Results ###########################################################
# array(['democrat', 'republican', 'democrat', 'democrat', 'democrat',
#       'democrat', 'democrat', 'democrat', 'republican', 'democrat'],
#       dtype=object)
```

## Evaluate classification model performance

> **n** : number of observations
> 
>
> **VP** : vrai positif, **FP** : faux positif, **VN** : vrai négatif, **FN** : faux négatif
 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/509c81a8-e3bd-4b7e-a656-b750081558af/Untitled.png)

Different **metrics**:

- **`accuracy` : [accuracy_score(y_test, y_pred)]**
    
    *true prediction ratio (most used)* 
    
    good indicator when VP and VN is well balanced
    

$$
\mathrm{accuracy} = \frac{\mathrm{VP} + \mathrm{VN}}{n}
$$

- **`precision` : [precision_score(y_test, y_pred, pos_label)]**
    
    *true prediction among positive prediction*
    
    good indicator when dominant class
    

$$
\mathrm{precision} = \frac{\mathrm{VP}}{\mathrm{VP} + \mathrm{FP}}
$$

- **`recall` : [recall_score(y_test, y_pred, pos_label)]**
    
     *number of true positive classification among all positive*
    
    good indicator when dominant class
    

$$
\mathrm{recall} = \frac{\mathrm{VP}}{\mathrm{VP} + \mathrm{FN}}
$$

- **`confusion matrix` :** calculate all 3 metrics.
    
    **confusion_matrix**(y_true, y_pred)
    
    **pd.crosstab**(y_test, y_pred_test_knn, rownames=['Realité'], colnames=['Prédiction'])
    

$$
\mathrm{Confusion Matrix} = \begin{bmatrix}
                                    \mathrm{VN} & \mathrm{FP} \\
                                    \mathrm{FN} & \mathrm{VP}
                                \end{bmatrix}
$$

```python
from sklearn.metrics import confusion_matrix

# Calcul et affichage de la matrice de confusion
matrice_confusion = confusion_matrix(y_test, y_pred_test_knn)
print("Matrice de Confusion:\n",  matrice_confusion)

print("\nLe modèle knn a fait", matrice_confusion[0, 1], "Faux Positifs.")

# Calcul de l'accuracy, precision et rappel
(VN, FP), (FN, VP) = confusion_matrix(y_test, y_pred_test_knn)
n = len(y_test)

print("\nKNN Accuracy:", (VP + VN) / n)
print("\nKNN Précision:", VP / (VP + FP))
print("\nKNN Rappel:", VP / (VP + FN))

# Results ##########################################################
# Matrice de Confusion:
# [[48  5]
# [ 2 32]]

# Le modèle knn a fait 5 Faux Positifs.
# KNN Accuracy: 0.9195402298850575
# KNN Précision: 0.8648648648648649
# KNN Rappel: 0.9411764705882353
```

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score

# Calcul et affichage de la matrice de confusion
pd.crosstab(y_test, y_pred_test_logreg, rownames=['Realité'], colnames=['Prédiction'])

# Calcul de l'accuracy, precision et rappel
print("\nLogReg Accuracy:", accuracy_score(y_test, y_pred_test_logreg))
print("\nLogReg Précision:", precision_score(y_test, y_pred_test_logreg, pos_label = 'republican'))
print("\nLogReg Rappel:", recall_score(y_test, y_pred_test_logreg, pos_label = 'republican'))

# Results ###########################################################
# LogReg Accuracy: 0.9310344827586207
# LogReg Précision: 0.8888888888888888
# LogReg Rappel: 0.9411764705882353

```

```python
from sklearn.metrics import classification_report

print(classification_report(y_test, y_pred_test_logreg))
print(classification_report(y_test, y_pred_test_knn))

# Results ###########################################################
#               precision    recall  f1-score   support

#    democrat       0.96      0.92      0.94        53
#  republican       0.89      0.94      0.91        34

#    accuracy                           0.93        87
#   macro avg       0.92      0.93      0.93        87
#weighted avg       0.93      0.93      0.93        87

#              precision    recall  f1-score   support

#    democrat       0.96      0.91      0.93        53
#  republican       0.86      0.94      0.90        34

#    accuracy                           0.92        87
#   macro avg       0.91      0.92      0.92        87
#weighted avg       0.92      0.92      0.92        87
```

**`F1-Score` :** for classification problem adequate. Kind of a **mean** of **precision** and **recall**

```python
from sklearn.metrics import f1_score

print(f1_score(y_test, y_pred_test_knn, pos_label = 'republican'))
print(f1_score(y_test, y_pred_test_logreg, pos_label = 'republican'))

# Results ###########################################################
# F1 KNN: 0.9014084507042254
# F1 LogReg: 0.9142857142857143
```

---

# SQL ALCHEMY

```python

engine = create_engine('sqlite:///chinook.db', echo=True)
inspector = inspect(engine)
inspector.get_table_names()
inspector.get_columns(table_name='col')
inspector.get_foreign_keys(table_name='table')
conn = engine.connect()

# request
stmt = text("SELECT Title FROM albums LIMIT 10;")
result = conn.execute(stmt)
result.fetchall() 

# create a table
user = Table('user',metadata_obj,
             Column('user_id', Integer, primary_key=True),
             Column('user_name', String(16), nullable=False),
             Column('email_address', String(60)),
             Column('nickname', String(50), nullable=False)
             ForeignKey("parent.id")
)
# 
metadata_obj.create_all(engine)

# delete table
drop = text('DROP TABLE IF EXISTS name_table;')
result = engine2.execute(drop)

```

# PySpark

**Imports**
```python
# Import PySpark related modules
import pyspark
from pyspark.rdd import RDD
from pyspark.sql import Row
from pyspark.sql import DataFrame
from pyspark.sql import SparkSession
from pyspark.sql import SQLContext
from pyspark.sql import functions
from pyspark.sql.functions import (
    lit, 
    desc, 
    col, 
    size, 
    array_contains,
    isnan, 
    udf, 
    hour, 
    array_min, 
    array_max, 
    countDistinct
from pyspark.sql.types import *
```

**conf**
https://spark.apache.org/docs/latest/configuration.html
```python
# Initialize a spark session.
MAX_MEMORY = '15G'
conf = pyspark.SparkConf().setMaster("local[*]") \
        .set('spark.executor.heartbeatInterval', 10000) \
        .set('spark.network.timeout', 10000) \
        .set("spark.core.connection.ack.wait.timeout", "3600") \
        .set("spark.executor.memory", MAX_MEMORY) \
        .set("spark.driver.memory", MAX_MEMORY)

spark = SparkSession \
    .builder \
    .appName("Pyspark guide") \
    .config(conf=conf) \
    .getOrCreate()

# Load the main data set into pyspark data frame 
df = spark.read.json('file.json', mode="DROPMALFORMED")

```

**overview**
```python
df.dtypes
df.describe(['col1','col2']).toPandas()             # if no col is given then describe all columns
df.limit(2).toPandas()
df.printSchema()                                    # print the schema of df
df.schema                                           # Returns the schema of this DataFrame as a pyspark.sql.types.StructType

df.collect()[:k]                                    # Lazy evaluation 
df.first()                                          # Returns the first row as a Row.
df.head(n)                                          # Returns the first n rows as Rows.
df.show(n)                                          # Returns the first n rows as Rows.
df.take(n)                                          # Returns the first n rows as list of Rows.
df.count()                                          # Count the number of rows in df
df.distinct().count()                               # Count the number of distinct rows in df

```

# Generator

**use cases**
- when dealing with a huge dataset
- scenarios where we do NOT need to reiterate it more than once (can only be iterated once)
- lazy evaluation
- They are a great way to generate **infinite** sequences in a memory-efficient manner

