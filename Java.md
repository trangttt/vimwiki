# CONCURRENCY

## Callable & Runnable

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
## Executor Service
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

## Stream, Lambda
