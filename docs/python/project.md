# Project Structure



## From Hitchhiker's

```
README.rst
LICENSE
setup.py
requirements.txt
sample/
    __init__.py
    core.py
    helpers.py
docs/
    conf.py
    index.rst
tests/
    test_basic.py
    test_advanced.py
```

## From Pytest doc

```
src/
    mypkg/
        __init__.py
        app.py
        view.py
tests/
    test_app.py
    test_view.py
    ...
```

Avoid using `__init__.py` in test folder

```
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

## Main Structure

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

All directory with an `__init__.py` file is considered as a package.

Structure of a python package (in the same directory as the said program):
```
- program_name.py
- package_name/
    - __init__.py
    - module1.py
    - module2.py
    -...
```
