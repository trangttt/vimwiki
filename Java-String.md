## String

- StringJoiner ; add single item
- Collectors.joining(); String.join( delimeter, list/charsequence );
- Constructor: `""`  or `new String()`
```java
String a = "abcd";
String b = "abcd";
System.out.println(a == b);  // True
System.out.println(a.equals(b)); // True
 
String c = new String("abcd");
String d = new String("abcd");
System.out.println(c == d);  // False
System.out.println(c.equals(d)); // True

String a = "abc";
String c = "bdc";
a.compareTo(c);

```
- Repeat string n times
```java
String result = new String(new char[n]).replace("\0", s);
```
- Convert String to Date
```java
String str = "Jul 16, 1985";
Date date = new SimpleDateFormat("MMMM d, yy", LOCALE.English).parse(str);
```
- Count number of occurences
```java
int count = line.length() - line.replace(<character to count>).length();
```

## String format
```java
String.format("%[-: left justified, default is right justified][padding character][width].[precision][formatter: f/d/s] [%n - new line]", *args);
```
## Array
- Declare
```java
String[] arr1 = new String[5];
String[] arr2 = new String[]{"1", "2", "3"};
String[] arr3 = {"1", "2", "3"};
```
- Print
```java
int[] arr = {1, 2, 3};
String s = Array.toString(arr);

System.out.println(arr); // this will print references value
System.out.println(s);
```

- Create ArrayList from Array
```java
String[] sa = {"1", "2", "3"};
ArrayList al = new ArrayList<String>(Arrays.asList(sa));
```
NOTE: changing al, also changing sa. al contains reference pointer to sa.
- Check if Array contains a value
```java
String[] a = {"1", "2", "3"};
Arrays.asList(a).contains("2");
```
- Concatenate two arrays
```java
length = src.length() + dest.length();
T[] result = Arrays.copyOf(arr, length)
System.arraycopy(src, index_src, dest, index_dest, length)
```

- Declare an array inline
```java
method(new String[]{"1", "2", "3"});
```
- Convert ArrayList to Array
```java
ArrayList<String> arrl = Arrays.asList("1", "2", "3");
String[] arr = new String[arrl.size()];
arrl.toArray(arr);
``` 
- Array to Set
```java
HashSet<String> set = new HashSet<String>(Arrays.asList(array));
```
- Remove element from array
```java
List<String> arrL = new ArrayList<String>(Arrays.asList(array));
arrL.remove/removeAll(element);
arr = list.toArray(arr);
``` 
- Convert Int to Byte array
- Reverse an array
```java
Collections.reverse(Arrays.asList(array));
```
## Generics
1. Unbounded wild card, raw type, Object
- Using raw type: skip checking generic type
```java
//Raw type
List list = new ArrayList<String>();
list.add("aString");
list.add(1); //compile and produce runtime error

//Unbounded wild card
List<?> list = new ArrayList<String>();
list.add("aString"); //compile error since type is unknown
list.size(); //this works as type is not need to known. Methods don't require type works as usual.

//Object type
List<Object> list = new ArrayList<String>();
list.add("aString"); // compile and run ok
list.add(1); // compile and run ok

void appendNew(List<Object> list){

}
List<String> list = new ArrayList<String>();
appendNew(list); // compile error. List<String> is not subtype of List<Object>

//fix
void appendNew(List<?> list){
    //only methods don't require type.
    //Getting element, cast to Object
    for (Object o: list){
        ....
    }
}
``` 
- 
2. Static method with generic. Define generic type in that method
```java
class A {
    public static T method(T t){

    }
}
```
3. 

## Collections
### List
```java
list.add
list.contains
list.containsAll
list.size
```
- `LinkedList`: `subList(start, stop)`
### HashMap
```java
map.containsKey/containsValue
map.put
```
## Java regex
### Predefined Character Classes
- `\d` : a digit [0-9]
- `\D` : a non digit [^0-9]
- `\s` : a whitespace character
- `\S` : a non whitespace character
- `\w` : a word character
- `\W` : a word character
### Simple usage
```java
Pattern p = Pattern.compile(<pattern String>);
Matcher m = p.matcher(str);
boolean b = m.matches()
boolean b = Pattern.matches(pattern, string);
while (m.find()){
    m.group()
}
```
## Nested Class

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
## Files

```java
try ( BufferedReader br = Files.NewBufferedReader(Paths.get("file")) ) {
    br.lines() // Stream<String>
}
catch (IOException ioe){

}
```

## Java Logging
### Native logging 
```java
import java.util.logging.Logger;

Logger lg = Logger.getLogger(this.getClass().getName());
FileHandler fh = new FileHandler("name-%g.txt", true);
fh.setFormatter(new SimpleFormatter());

```
- `%u`: unique number to avoid name collision
- `%g`: generated number to distinguish the rotated log files
- `%t`: the temp directory of the system
- `%h`: user home directory of the system

- Formatter
```java
class MyFormatter extends Formatter {
    @Override
    public String format(LogRecord record){
        DateFormatter fm = new SimpleDateFormatter("dd/MM/yyyy HH:mm:ss");
        return fm.format(new Date()) + record.getLevel() + " - " + record.getMessage() + "\n";
    }
}
```
- properties file
```java
try ( FileInputStream fi = new FileInputStream(getClass().getClassLoader().getResource("FileName").getPath())  ){
    LogManager lm = LogManager.getManager();
    lm.readConfiguration(fi);
}
catch (IOException io){
    logger.log(Level.SEVERE, "Message", io);
}
```

```java properties examples file
handlers=java.util.logging.FileHandler, java.util.logging.ConsoleHandler
.level=ALL

java.util.logging.FileHandler.level=ALL
java.util.logging.FileHandler.formatter=java.util.logging.SimpleFormatter
java.util.logging.FileHandler.pattern=log-%u-%g.txt

java.util.logging.ConsoleHandler.level=ALL
```
### SLF4J logging interface
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

Logger logger = LoggerFactory.getLogger(class);
//No logger.fatal
logger.error()
logger.warn()
logger.info()
logger.debug()
logger.trace()
```

- Native `java.util.logging...`: adding `slf4j-api-xx.jar` and `slf4j-jdk-xx.jar`. Adding `-Djava.util.logging.config.file=[path to file from the root directory]`
- Log4j: adding `slf4j-api-xx.jar` and `slf4j-jdk-xx.jar`
- NOTES:
    - Logging exception: `logger.error( "message {}", exception );`. Do NOT use `exception.message()`

### LOG4J
- appender
    - FileAppender
        + Threshold: `debug`, `info`, `warning`
        + Append: `true` or `false`. Default is `true`.
        + ImmediateFlush. `true` (default) or `false`.
        + File: file name + location from project dir
        + layout :
            - DateLayout
            - HTMLLayout
            - PatternLayout
                + conversionPattern :
                    + default: `Default is %r [%t] %p %c %x - %m%n`
                    + `c`: category. Ex: category `a.b.c`, for `%c{2}` output `b.c`
                    + `C`: Class: Ex: category `class1.class2.class3`, for `%C{1}`, output `C`
                    + `d{}`: date. Ex `d{dd MMM yyyy HH:mm:ss,SSS}`
                    + `m`: message
                    + `M`: Method Name
                    + `l`: full Location information: class, (file: line number)
                    + `L`: Line number
                    + `p`: priority event
                    + `r`: elapsed time since beginning
                    + `n`: new line independent platform `%n`
                    + `x`: nested diagnostic context `NDC.push(<String: context>)` when entering context and `NDC.pop()` when exit.
                    + `X`: Mapped Diagnostic Context http://veerasundar.com/blog/2009/11/log4j-mdc-mapped-diagnostic-context-example-code/
                            `MDC.put(key, value)` and `MDC.remove(key)`
            - SimpleLayout
            - XMLLayout
    - RollingFileAppender
        + MaxFileSize
        + MaxBackupIndex
    - DailyRollingFileAppender
        + DatePattern: '.' yyyy-MM: rolling every month. https://www.tutorialspoint.com/log4j/log4j_logging_files.htm
- 

## JAVA 7
- `static` Static initializer
- instance field initializer
- Member class
- Local Inner Class
- Anonymous Inner class
- Enumeration class
```java
public enum EnumName {
    val1("name1"), val2("name2"), val3("name3");
    
    private String name;
    private EnumName(String name){
        this.name = name;
    }
    
    @Override
    String toString(){
        return this.name;
    }
}
```
- Set: `HashSet`, `TreeSet`. `TreeSet` implements ordering. Required Object put into Set implementing `Comparable` interface.
- LinkedList: `addFirst`, `addLast`
- `Queue` operation: `peek`, `poll`. vs `remove`, `element`. `peek`, `poll` return `null` if queue is empty. `remove`, `element` throws exception `NoSuchElemenException`
- Java New IO package
    - `java.nio.file.Path` and `java.nio.file.Paths`
    - `Path path  = Paths.get(<file>);`
    - `Files.copy, Files.delete, Files.move(source, target, StandardCopyOption.XXX)`
    - `Path.resolve`
- `WatchService`: watching event happens
- `FileInputStream`, `FileOutputStream`
- `FileReader`, `FileWriter`
- `BufferedReader(FileReader())`, `BufferedWriter(FileWriter())`
- `byte[] Files.readAllBytes(Path path)`
- `List<String> Files.readAllLines(Path path, Charset cs)`
- `Stream<String> Files.lines(Path path, Charset cs)`
- `Stream<Path> Files.list(Path dir)`
- 
## JAVA BASIC
- Scanner
- `static` block
- 
