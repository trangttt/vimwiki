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
pyenv : used to manage virtual envs. 
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
```python
count(start[, step])
count(10, 2) -> 10, 12, 14, 16,...
```
2. `cycle` 
```python
cycle(iterable)
cycle('abcd') -> a, b, c, d, a, b, c, d, ...
```
3. `repeat`
```python
repeat(elem[, times])
repeat(3, 2) -> 3, 3
``` 
4. `chain`
```python
chain(iter1, iter2, ...)
chain('ABC', 'DEF') -> A, B, C, D, E, F

```
5. `chain.from_iterable` 
```python
chain.from_iterable([iter1, iter2,...])
chain.from_iterable(['ABC', 'DEF'])
``` 
6. `accumulate`
8. `dropwhile`
9. `takewhile`
10. `compress`
11. `starmap`
12. `filterfalse`
13. `tee`
14. `groupby`
15. `islice`

## functools
1. `wraps`
2. `partial`
3. `lru_cache`
4. 


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

with MyTimer() as timer:
    do_something()
```

```python
from contextlib import contextmanager

@contextmanager
def func():
    do_something()
    yield something
    do_something()
```

2. "and"
```python
"a" and "b" = "b"
```
3. string * number
```python
"a" * 0 = None
"a" * 1 = "a" 
```
4. 


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
1. Simple test:
```python
    def test_xxx():
        assert()
```
Running:
```python
    python -m pytest <file>
    py.test <file>
    pytest <module>.<file>
    pytest -s <file> #--capture=no print output
    pytest -v <file>
    pytest -q <file>
    pytest --collect-only <file> #only prints out testcase
    pytest -k <testcase> <file> #select testcase
```

Running with verbose
```python
    python -m pytest -v <file> 
    py.test -v <file>
    pytest <module>.<file>
    pytest -s <file> #--capture=no print output
    pytest -v <file>
    pytest -q <file>
```

2. Pytest setup/teardown:
Different setup/teardown level :
- At the beginning and the end of a module( `setup_module`,`teardown_module` )
- At the beginning and the end of a class( `setup_class`,`teardown_class` )
- At the beginning and the end of a function( `setup_function`,`teardown_function` )
- At the beginning and the end of a method( `setup_method`,`teardown_method` )
- Session: defined at conftest.py `pytest_sessionstart(session)`
- alternate style of class level fixtures
- Hooks for session `pytest_sessionstart(session)`, `pytest_sessionfinish(session, exitstatus)`
3. Test discovery
- Name my test modules/files starting with ‘test_’.
- Name my test functions starting with ‘test_’.
- Name my test classes starting with ‘Test’.
- Name my test methods starting with ‘test_’.
- Make sure all packages with test code have an ‘__init__.py’ file.

4. Assert statement
- `assert 0`: gives error
- `assert 1`: pass
- `assert <statement>`: covers all possibilities.
5. Fixtures
- `import pytest`
- `@pytest.fixture`: annotate function
- `scope=[session|module|class]`
- `request` : test context
- `@pytest.fixture(params=[....])`
```python
@pytest.fixture(params=[...])
def fixture(request):
    resquest.param
    pass

def test_func(fixture)
```
- `params`, `ids`: using `ids` to denote id of testcase for select running later
- Using fixtures from class, modules or projects:
  - `@pytest.mark.usefixtures(fixture1, fixture2,...)`
  - Using fixture for whole Project using pytest.ini 
```python
[pytest]
usefixtures = fixture1, fixture2,...
```
- `autouse`: use with care
 
6. "monkeypatch" fixture, for mocking modules
```python
def test_f(monkeypatch):
    monkeypatch.setattr(module, "method/variable", value)
```
```java
Class MonkeyPatching
setattr/delattr : object
setitem/delitem : dict
setenv/delenv : set environment variable
```
7. 


# Generator

# Metaclass
# Regex
## Special characters
- `\d`, `\D`
- `\w`, `\W`
- `\s`, `\S`
- `(?P<name>)`
## Simple usage
```python
pattern = re.compile("patterm");
match = pattern.match(str);
match.groups()/group();
Ex: pattern = re.compile("(\d) (\d) (\d)")
match = pattern.match("1 2 3")
match.groups() == ('1', '2', '3')
```


'a' : 97
'' : 0
'CodeFight': 121
'AAbbb': 98
'codefight' : 121
'<Try to #hardcode_results, do you?>': 41
'Hint: This is a valid test! :-P': 90
