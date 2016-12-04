# Virtual Environments 

## virtualenv 
virtualenv : python package to create an isolated Python environments. To isolate dependencies and python version. 


- `virtualenv -p <path to python executable> <env name>`: create a new virtual env with python executable path.
- `source <env name>/bin/activate`: activate virtual env.
- `deactivate`: deactivate a virtual env.


## pyenv 
- pyenv: to manage multiple python installments. 
- `pyenv install <version>`: install a version of python.
- `pyenv uninstall <version>:` uninstall a version of python.
- `pyenv versions:` list all installed python versions.
- `pyenv version`: list current python version.
- `pyenv shell <version>`: set python version for current shell.
- `pyenv global <version1> <version2>`: set python versions for whole system. <version1> is preferred over <version2>
- `pyenv local <version1> <version2>:` set python versions for current directory. Automatically trigger python version when enter dir.
- `pyenv whence <command>:` list all the verions where the given command is installed.
- `pyenv which <command>`: show the fullpath of the executable that pyenv will invoke if you execute a command.


## pyenv-virtualenv
- pyenv : used to manage virtual envs.
- `pyenv virtualenv <version> <env name>`: create a virtual env <env name> from python version <version>. if <version> is not given, current python version is used.
- `pyenv virtualenvs`: list all virtual envs.
- `pyenv local <env name>`: set virtual env for current directory.
- `pyenv local --unset`: unset local python virtual env.
- `pyenv activate <env name>`: activate <env name> for current shell.

