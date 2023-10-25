# Environment


!!! Note "example title"

    this is an introductory note

## Install Packages with `pip`

```bash
python -m pip install --upgrade pip             # upgrade pip

pip install <package1> <package2> ...           # install a package

pip list                                        # print installed packages in a pretty fashion 
pip freeze                                      # print installed packages readable for the requirements.txt file
pip freeze > requirements.txt                   # write installed packages to the file requirements.txt
python -m site                                  # print the site-packages directories on the drive
pip show <package_name>                         # show package_name info

pip install requests==2.1.0                     # install a package with specific version
pip install "requests>2.4.0,<2.6.0"             # install a package within versions
pip install -r requirements.txt                 # install a package lister par pip freeze dans requirements.txt
```

## Virtual Environment

```bash
pip install venv                                # install venv package
python -m venv <env_name>                       # create a virtual environnement "env_name"
source env/Scripts/activate                     # activate the virtual environment (env/Scripts/activate.bat Windows)
deactivate                                      # deactivate the current virtual environment
```

## Pipenv

Useful to deal with dependencies

Install pipenv
```bash
pip install pipenv --user
```

Create a `.venv` folder *(or put `PIPENV_VENV_IN_PROJECT=1` into a `.env` file that pipenv will load when invoke)*
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

## Environment Variables

```bash
# Linux
export PYTHONPATH=${PYTHONPATH}:${PWD}/src

# Command Prompt
set PYTHONPATH=%PYTHONPATH%;%CWD%\src

# Powershell
$env:PYTHONPATH="$env:PYTHONPATH;${PWD}\src"
```