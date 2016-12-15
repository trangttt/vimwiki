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
- pyenv : used to manage virtual envs. wiki_1, wiki_2 ]
- `pyenv virtualenv <version> <env name>`: create a virtual env <env name> from python version <version>. if <version> is not given, current python version is used.
- `pyenv virtualenvs`: list all virtual envs.
- `pyenv local <env name>`: set virtual env for current directory.
- `pyenv local --unset`: unset local python virtual env.
- `pyenv activate <env name>`: activate <env name> for current shell.

# Useful libraries
## argparse
`parser = ArgumentParser(description="xxx", epilog="xxxx")`

```python
parser.add_argument("-x",
                    action=[(store)/store_true/store_false/append/],
                    required=[True/(False)],
                    nargs=[ int (0) ],
                    type=[ function to convert string to suitable type ],
                    choices=[ list of selectable values ],
                    default=[ default value ],
                    help="string to print with --h")
```
Options that conflicts:
```python
group = parser.add_mutually_exclusive_group()
group.add_argument(....)
```

## defaults
1. `eval`
2. `any`
3. `all`
4. `filter` 
5. `map`
6. `enumerate`
7. `zip`

## collections
1. `ChainMap`
    ```python
    total_dict = ChainMap(dict1, dict2, dict3, dict4)
    ```
3. `defaultdict`
4. `dequeue`
5. `namedtuple`
6. `OrderedDict`
7. `Counter`

## itertools
1. `count`
2. `cycle`
3. `repeat`
4. `chain`
5. `accumulate`
6. `dropwhile`
7. `takewhile`
8. `compress`
9. `startmap`
10. `filterfalse`
11. `tee`
12. `groupby`

## functools
1. wraps
2. partial


# Idioms

1. Context Manager
```python
class MyTimer:
    def __init__(self):
        pass
    
    def __enter__(self):
        return <something: self/ filedescriptor/...>
    
    def __exit__(self, exc_type, exc_val, exc_tb):
       pass 
```

```python
from contextlib import contextmanager

@contextmanager
def func():
    do_something()
    yield something 
    do_something()
```

2. 
3. 


# Profiling
## cProfile
used to profile functions and overall programs.
```python
python -m cProfile <file>
```

## line_profiler
used to profile line by line of the profiled functions.
Adding `@profile` to function to be profiled.
`kernprof -l <file> <Args>` : resulting a binary-encoded result file .lprof
`python -m line_profile <result_file>`: decode the result file
`kernprof -l -v <file> <args>`: profiling and printing out the result.

## memory_profiler
Adding `@profile` to the to-be-profiled functions.
`python -m memory_profile <file>`: memory_profiling the python file
`mprof <file>`: logging memory usage every .1 seconds, no need `@profile`, remember to remove after memory_profile in previous steps.
`mprof plot`: using matplotlib to create graph

## profilehooks
`@profile` : profiling function-wise
`@timecall`: timeit
`@coverage`: collect code coverage


# Testing
## doctest
## unittest
## Mock module
## pytest

# Generator
# Metaclass
