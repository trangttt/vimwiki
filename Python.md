# Virtual Environments 

## virtualenv 
virtualenv : python package to create an isolated Python environments. To isolate dependencies and python version. 
- `virtualenv -p <path to python executable> <env name>`: create a new virtual env with python executable path.
- `source <env name>/bin/activate`: activate virtual env.
- `source deactivate`: deactivate a virtual env.


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
4. Os name
```python
import os 
os.name # posix

import platform 
platform.system() # Darwin
platform.release() # release version
platform.platform() # Darwin_15....
platform.machine() # x86_64
platform.architecture() # 64bit
platform.mac_version() # 10.11..

import sys; 
sys.platform # darwin
```
5. 


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
### What to mock
- instance
```python
    def f(s):
        return s.message
        
   
    m = Mock(message="123")
    assert f(m) == "123" 
```
- class method
- object method
### unittest.mock Python3 and mock Python2
```python
try :
	import mock # for python 2
except ImportError:
	from unittest import mock

##########
# Function mock
#########
## function.py

def square(s):
	return s * s

def cube(s):
	return s * s * s

def main(s):
	return square(s) + cube(s)

###############

from function import square, main

class TestABC(unittest.TestCase):
	# Mock function inside another call.
	@mock.patch('function.square')
	@mock.patch('function.cube')
	def test_main(self, mocked_square, mocked_cube):
		mocked_square.return_value = 1
		mocked_cube.return_value = 1
		main(5)
		mocked_square.assert_called_once_with(5)
		mocked_cube.assert_called_once_with(5)

	# Mock functions in this file
	@mock.patch('__main__.square', return_value=5)
	def test_square(self, mocked_square):
		assertEquals(square(5), 5)

#############
# Class mock
#############
## square.py
Class Square(object):
	def __init__(self, s):
		self.s = s

	def calculate_area(self):
		return self.s * self.s 
########

from square import Square

class TestSquare(unittest.TestCase):
	@mock.patch('__main__.Square')
	def	test_square(self, mocked_square):
		mocked_instance = mocked_square.return_value
		mocked_instance.calculate_area.return_value = 5
		sq = Square(100)
		self.assertEquals(sq.calculate_area(), 5)
		
	@mock.patch.object(Square, 'calculate_area'):
	def test_calculate_area(self, mocked_method):
		mocked_method.return_value = 5
		self.assertEquals(Square(100).calculate_area(), 5)
		
	def test_magic_mock(self):
		sq = Square(100)
		
	
```
#### Mock
#### patcher
#### MagicMock
### pytest monkeypatch, mock
```python
def get_ssh():
    return os.path.join(os.path.expanduser("~admin"), '.ssh')
    
def test_function(monkeypatch):
    def mockreturn(path):
        return '/abc'
    monkeypatch.setattr(os.path, "expanduser", mockereturn)
    
    x = getssh()
    return x == '/abc/.ssh'
```
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
    pytest --fixtures #names of defined fixtures
    pytest --durations=3 # profiling three slowest tests
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
 
6. Ignore test
```python
pytest --collect-only
pytest -k stringexpr # MyClass and not method , test MyClass.other_method not MyClass.method
pytest test_mod.py::test_func
pytest test_mode.py::TestClass::test_method

import pytest.mark.skip
skip(reason="")
def test():
    pass

pytest.mark.skipif(condition, reason="")

```
7. Pytest exception test
```python
with raise(Exception, message="Failuer Message"):
    test
```
8. Pytest parameterize
```python
@pytest.mark.parameterize("var1, var2",[
    (var1, var2),
    (var1, var2),
    (var1, var2),
    pytest.mark.xfail("condition")((var1, var2))
])
def test_func(var1, var2):
    assert .....
```
9. monkeypatching 
```python
def test_f(monkeypatch):
    monkeypatch.setattr(module, "method/variable", value)
```
```python
Class MonkeyPatching
setattr/delattr : object
setitem/delitem : dict
setenv/delenv : set environment variable
```

10. Request object
```python
class FixtureRequest:
- config: pytest config object associate with this request
- cls
- function
- scope
- instance
- session

```
11. Comparing floating point
```python
from pytest import approx
```
12. 
```python
slow = pytest.mark.skipif(
    not pytest.config.getoption("--run-slow"),
    reason="need --runslow optiont to run"
)

@slow
def test_a():
    pass
```

13. Pytest skip incremental test 
14. Pytest - Postprocess test results/failures 


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
# Docstring, Sphinx
## `docstring`: :
## Sphinx
- `sphinx-quickstart`  to generate `conf.py`
- syntax
- running
## Python command line
### Making a package executable: `__main__.py`
### Argparse
```python
import argparse
arparser = argparse.ArgumentParser(
    prog="python -m appname",
    description="Program description"
)
```
# Decorators:
- normal decorator
```python
from functools import wraps

def decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        do_something()
        func(*args, **kwargs)
    return wrapper
```
- decorator with arguments
```python
def decorator_with_args(*args):
    doing something()
    def decorator(func):
        def wrapper(*args, **kwargs):
            doing something()
            func(*args, **kwargs)
            doing something()
        return wrapper
    return decorator
```

- decorator ultilizes annotation
```python
def store_args(func):
    @wraps(func):
    def wrapper(self, **kwargs):
        for name, value in kwargs.items():
            type = func.__annotations__.get(name)
            if not isinstance(value, type):
                value = type(value)
            if isinstance(name, str):
                setattr(self, name, value)
        return func(**kwargs)
    return wrapper
    
    
class Test:
    @store_args
    def __init__(self, attr1 : int, attr2: str):
        pass
```
- decorator for class
```python
```
# Context manager
- functin version
```python
import contextlib
@contextlib.contextmanager
def before_and_after():
    print("Before")
    try:
        yield (lambda: print("during"))
    finally:
        print("After")
        
with before_and_after() as during:
    print("MIDDLE")
    during()
    
    
Before
MIDDLE
during
After
```

- class version ( synchronous vs asynchronous )
```python
class SomethingContextManager:
    def __init__(self, *args):
        return self
        
    def __enter/aenter__(self):
        return something
        
    def __exit/aexit__(self, exc_type, exc_val, tb):
        doing_something()

something = SomethingContextManager(args)
with something as st:
    doing_something()
```
# Descriptors
- Using `@property`
```python
class MyClass:
    @property
    def member(self):
        print("This is a getter method.")
        return self._member
        
    @member.setter
    def member(self, value):
        print("This is a setter method.")
        self._member = value
        
    
    @member.deletter
    def member(self):
        print("This is a deletter method.")
        del self._member
```
- Descriptor class
```python
Class Member(object):
    def __init__(self, value):
        self.value = value
        
    def __get__(self, instance, owner):
        return self.value
        
    def __set__(self, instance, value):
        self.value = value
        
    def __delete__(self, instance):
        self.value = 0
        
class MyClass(object):
    member1 = Member(val1)
    
mc = MyClass()

mc.member1 # Using Member.__get__
mc.member1 == 2 # Using Member.__set__
```
