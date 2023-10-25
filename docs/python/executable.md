# Create an Executable

## Install with python 2

```bash
sudo apt-get install python-dev
pip install cx_Freeze
```

## Install with python 3

- Download `cx_Freeze` library et extract it
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

## Setup

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

## Build

```bash
python setup.py build

```