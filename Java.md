# CONCURRENCY
## Primitives
### Synchronized, Lock, Semaphore
- `synchronized`
- `atomic`
- `volatile` : all read and write to a *volatile* variable is always directly through memory. useful for flag.
- `Lock`
- `ReentrantLock`
- `ReadWriteLock`
- `Semaphore`
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
- Define using lambda `BiFuntion`, `Predicate`. method to use lambda in definition `apply`

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

- `this` refer to the enclosing object, not the lambda itself.
- Referencing instance variables.
```java
class DataProcessor {
    int currentValue;
    public void process(){
        DataSet d;
        d.forEach( d-> d.use(currentValue) ); 
    }
}
```
`currentValue` is not an *effectively final* variable. Yet it works in this case, as the compiler silently inserts `this`.
`currentValue` -> `this.currentValue`

### List, Map methods can use lambda
`List.removeIf` `List.replaceAll` `List.forEach` 
`Map.forEach`

### Stream Generating 
-  Object stream to Primitive stream
`mapToInt`, `mapToLong`, `mapToDouble`, `mapToLong`
-  Stream source:
    - `Collection` interface: `stream()` or `parallelStream()`
    - `File` class: 
      - `find(Path, BiPredicate, FileVisitOption)`: stream of `File` references that match a given `BiPredicate`.
      - `list(Path)`: stream of entries from a given directory.
      - `lines(Path)`: stream of strings that are lines from a given file.
      - `walk(Path, FileVisitOption)`: stream of `Filea` references walking from a Path.
    - Random number: `ints()`,`double()`, `long()`
    - JarFile/Zip File: `stream()`
    - BufferedReader: `lines()`
    - Pattern: `splitAsStream()`
    - CharSequence: `chars()`, `codePoints()`
    - BitSet
- Stream static method: `IntStream`, `LongStream`, `DoubleStream`
    - `of(stream, stream)`
    - `of(T...values)`
    - `range(int, int)`, `rangeClosed(int, int)`
    - `generate(IntSupplier)`, `iterate(int, IntUnaryOperator)`

### Intermediate operation
- Filtering, Mapping:
  - `distinct()`
  - `filter(Predicate p)`
  - `map(Function f)`
  - `mapToInt()`, `mapToLong()`, `mapToDouble()`
- FlatMap:
   - `flatMap(Function f)`
- Restrict size of a stream:
  - `skip(long n)`
  - `limit(long n)`
- Sorting and Unsorting:
  - `sort(Comparator c)`
  - `unordered()`
- Examining stream
  - `peek(Consummer c)`
### Terminal operation:
- Matching elements:
  - `findFirst(Predicate p)`
  - `findAny(Predicate p)`: similar `findFrist` for parallel stream.
  - `boolean allMatch(Predicate p)`
  - `boolean anyMatch(Predicate p)`
  - `boolean noneMatch(Predicate p)`
- Collectiong results:
  - `collect(Collector c)`: 
      - `Collectors.joining()`, `Collector.joining(CharSequence delimeter)`, `Collector.joining(CharSequence delimeter, CharSequence prefix, CharSequence suffix)`
      - `Collectors.reducing(BinaryOperator o)`
      - `Collectors.reducing(U identity, Function mapper, BinaryOperator o)`
      - `Collector.averagingInt(ToIntFunction)`, `Collectors.summarizingInt(ToIntFunction)`, `Collectors.summingInt(ToIntFunction)`, `Collectors.maxBy(Comparator c)`, `Collector.minBy(Comparator c)`
      - `Collectors.toList()`, `Collector.toSet()`
      - `Collectors.toMap(Function keyMapper, Function valueMapper)`
      - `Collectors.toMap(Funciton keyMapper, Function valueMapper, BinaryOperator mergeFunction, Supplier mapSupplier)`: mergeFunction used to resolve collisions between values associated with the same key.
      - `Collectors.toCollection()`
      - `Collectors.groupingBy(Function<T, K> classifier)`: grouping stream of element of type T by key K.
      - `Collectors.groupingBy(Function<T, K> classifier, Collector c)`: like above and then apply Collector c to each set of key K.
      - `Collectors.groupingBy(Function<T, K> classifier, Supplier<M> mapFactory, Collector c)`: supple the type of returned Map using mapFactory.
      - `Collectors.mapping(Function mapper, Collector c)`
      - `Collectors.partitioningBy(Predicatep )`
  - `toArray`
- Numerical results:
  - `count()`
  - `max(Comparator c)`, `min(Comparator c)`
  - `average()`
  - `sum()`
- Iteration:
  - `forEach(Consumer c)`
  - `forEachOrdered(Consumer c)`
- Folding a stream:
  - `reduce(BinaryOperator accumulator)`
### Optional class
```java
Optional<T> t
t.filter(), t.map()
t.flatMap()
Optional.ofNullable() //initialize
t.ifPresent()
t.orElse()
```
### Reducing operator
- Finding a single result, thinking about using `reducing`
- Ex: Finding the length of the longest line of a file
```java
Path file = Path.get("file");
String longestLine = Files.lines(file)
                    .reduce( (x,y) -> {
                    if ( x.length() > y.length() )
                        return x;
                    return y;
                        } ).get();

//Simple
int len = Files.lines(file).max(Comparator.comparingInt(String::length));
```
-
# NESTED CLASS

```java
class A {
    class InnerClass {

    }
    static StaticClass {

    }
}

A.InnerClass item = new A().new InnerClass();
A.StaticClass item = new A.StaticClass();
```
## Static nested class
## Inner Class
## Shadowing
When inner class has the same name with some outer class.
```java
class A {
    public void m(){

    }
}

class OuterClass {
    class A {
        public void m(){

        }

    }
}
```
# JAVA 8
## default method for interface
```java
public interface A {
    public void method1();
    
    default public void method2(){
        System.out.println("aaaa");
    }
}
```
- Default method vs static method
  + Default method : 
      + Usage: `new Class().defaultMethod()`
      + Know about `this` variable.
  + Static method :
      + Usage: `Class.staticMethod()`
      + Cannot know about `this` variable.
## Lambda expression
## Functional interfaces: must contain exactly one abstract method declaration
```java
@FunctionalInterface
interface Converter<F, T>{
    T convert(F from);
}
```
## Method and Constructore references
```java
//class
Class::method
//instance
object::method
//constructor
class::new
```
## Lambda scopes
- Local variables: variabls must declare `final` or behave as `final`
- Local variables can be read from but not written to
```java
final int localVar;
Function<F, T> f = (from) -> {
    // can read from localVar
    // cannot write to localVar 
} 
```
- Accessing fields and static variables. Can read from and write to both static variables and fields.
```java
class A {
    static int sVar;
    int field;
    
    void method(){
        Function<F, T> f = (from) -> {
            //can read from and write too sVar and field;
        }
    }
}
```
- Default method: since there is no way to create an object from interface, cannot access default method. NOTE: static method is otherwise accessible.
## Common Functional Interface
- `Predicate`: `Predicate<T> p -> Boolean`
- `Function` : `Function<F, T> f`
- `Supplier` :  `Supplier<T>` no argument, return object of type T
- `Consumer`
- `Optional`

## JAVA LOGGING
### SLF4J 
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

private final static Logger logger = LoggerFactory.getLogger( <class> );
logger.info()
logger.debug()
```
- Native `java.util.logging...`: adding `slf4j-api-xx.jar` and `slf4j-jdk-xx.jar`. Adding `-Djava.util.logging.config.file=[path to file from the root directory]`
- Log4j: adding `slf4j-api-xx.jar` and `slf4j-jdk-xx.jar`
- NOTES:
    - Logging exception: `logger.error( "message {}", exception );`. Do NOT use `exception.message()`

