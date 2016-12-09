# CONCURRENCY

## Primitives
### Synchronized, Lock, Semaphore
`synchronized`
`atomic`
`volatile` : all read and write to a *volatile* variable is always directly through memory. useful for flag.
`Lock`
`ReentrantLock`
`ReadWriteLock`
`Semaphore`

### ConcurrentMap
- `ConcurrentLinkedQueue`
- `ArrayBlockingQueue`
- `LinkedBlockingQueue`
- `PriorityBlockingQueue`
- `SynchronousQueue`
- `DelayQueue`
 
## Executor Service

### Callable & Runnable

- Callable :
```java
Callable<T> task = () -> { ...; ..; return T; };
```
    
- Runnable :
```java
Runnable task = () -> { ..; ..; ..; return; };
```

- Future
```java
Future<T> future = executor.submit(task);
future.get([time], [TimeUnit.SECONDS]);
future.cancel();
future.isCancelled();
future.isDone();
```

### Executor Service
Remember to **shut down** executor otherwise the program won't stop.
 
- submit
```java
    ExecutorService = executor.newFixedThreadPool(4);
    executor.submit(() -> {
        String threadName = Thread.currentThread.getName();
        System.out.println("Hello" + threadName);
    });
```

- invokeAny
```java
    List<Callable<T>> tasks = new ArrayList<Callable<T>>();
    T result = executor.invokeAny(tasks)
```

- invokeAll
```java
    List<Callable<T>> tasks = new ArrayList<Callable<T>>();
    List<Future<T>> results = executor.invokeAll(tasks);
```
 
- ThreadPool
  - `Executors.newFixThreadPool(<number of threads>);`: fixed number of threads
  - `Executors.newSingleThreadPool();`: single thread pool
  - `Executors.newScheduledThreadPool(<number of threads>)`: fixed number of scheduled threads. 
    - `ScheduledFuture<T> results = (ScheduledExcutor)executor.schedule(tasks, initialDelay, TimeUnit.SECONDS)`
    - `result.getDelay()`
    - `executor.scheduleAtFixedRate(task, intialDelay, rate, TimeUnit.SECONDS)`
    - `executor.scheduleAtFixedDelay(task, initialDelay, interval, TimeUnit.SECONDS)`
     
     
## JoinFork Framework

### ForkJoinTask, RecursiveAction, RecursiveTask
`ForkJoinTask` is an abstract class for `RecursiveAction` and `RecursiveTask`. 

Subclass either `RecursiveAction` or `RecursiveTask` to implement tasks to be submitted to `ForkJoinPool`. 
```java
class MyRecursiveTask extends RecursiveTask<T>{
    @Override
    protected T compute(){

    }
}
```
- `fork`: is forked, can used in the main function or in another task
- `join`: wait until completion and return result.
- `get(Time, TimeUnit.SECONDS)`: inherited from Callable.
- `isDone`:
- `isCancelled`:
- `isCompletedNormally`:
- `isCompletedabnormally`:
 

### ForkJoinPool
`ForkJoinPool` is a specialized implementation of `ExecutorService`, implementing work-stealing algorithim.

- `execute`
- `submit`
- `invoke`
 
## Stream, Lambda

### Lambda expression
Lambda expression is a *Functional Interface*, anotated as `@FuntionalInterface`, a single abstract method type.
Notes: JDK8 introduces default method and static method for interface. Default method for interface allows multiple inheritance of behaviour.

- `() -> System.out.println("Hello World")`
- `x -> x + 10`
- `(int x, int y) ->  x + y;` 

### Function packages
### Method references
Format : `target_reference::method_name`. Three kinds of method references:
- `Class::staticMethod`. Ex: `str -> System.out.println(str)` ->  `System.out::println`
- `Class::instanceMethod`. Ex: `(arg0, rest) -> arg0.instanceMethod(rest)` -> `ClassName::instanceMethod`
- `Instance:instanceMethod`. Ex: `a -> getLength(a)` -> `this::getLength`
- `Constructor`  Ex: `Factory<List<String>> fac = () -> ArrayList<String>()` -> `Factory<List<String>> fac = ArrayList<String>::new`

### Closure
Lambda expression can refer to *effectively final* variable from the surrounding scope.

Closure on value not on variable.
# NESTED CLASS
## Static nested class
## Inner Class
## Shadowing
