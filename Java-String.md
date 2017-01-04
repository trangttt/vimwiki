## String

- StringJoiner
- Collectors.joining()
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
