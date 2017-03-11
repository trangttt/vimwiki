# Python Coroutines
## Generators
```python
def my_gen(n):
    for i in range(n):
        yield i*2

gen = my_gen(5)
next(gen)
next(gen)
```
## Yield as an expression
```python
def my_grep(pattern):
    print("Looking for", pattern)
    while True:
        line = (yield)
        if pattern in line:
            print(line)

mg = my_grep("Python")  #Initialize generator
my_grep.next() #Fire generator

my_grep.send("This is Python") # >> This is Python
my_grep.send("This is something else") # [ print out nothing ]
```

## Coroutine
### Generator-based coroutine
```python
import asyncio

@asyncio.coroutine
def my_grep(number):
    yield from asyncio.sleep(1) 

g = my_grep("Python")
```
- is a generator-based coroutine, not a generator, `yield from` requires another coroutine or future
- `await` is not allowed
- distinguishing with native coroutine
### Native coroutine
- available since Python 3.5
```python
async def function(args):
    await couroutine
```
- native coroutine, allow using `await` not `yield from`
- since Python 3.6, allow asynchronous generators. Allows using `yield` inside `async def`
## Event Loop
```python
import asyncio
loop = asyncio.get_event_loop()
task = asyncio.ensure_future(coroutine)
loop.run_until_complete(task)
result = task.result()
loop.close()

loop.call_soon()
loop.call_later()
loop.call_task()
loop.ensure_future()

tasks = [ loop.create_task(coroutine(args)) for args in list ]
loop.run_until_complete(asyncio.wait(tasks))
```
## Debug
```PYTHONASYNCIODEBUG=1 python3 <file>```
## Supported libraries
### asyncio.subprocess
### iohttp
### iopg
### aiomysql
### uvloop: faster event loop
### Others
https://github.com/python/asyncio/wiki/ThirdParty


docopt
namespace
signal handler
kill child process with parent
using python3.5
write unittests
setup debugging
import gc; gc.set_debug()
do not use stopiteration
pep479
