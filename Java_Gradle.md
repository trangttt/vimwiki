# Java Build Tool
## Groovy syntax
- f-string similar to python
```groovy
def name="Trang"
println "My name is $name"
```
- List
```groovy
def myList = [ "Gradle", "Groovy", "Android" ]

def printItem = { item -> println "List item: $item" }
myList.each(printItem)
```

- delegate
```python
    class GroovyGreeter {
        String greeting = "Default greeting"
        def printGreeting(){
            println "Greeting: $greeting"
        }
    }
    
    def myGroovyGreeter = new GroovyGreeter()
   
   def greetingClosure = {
        greeting = "Setting the greeting from a closure"
        printGreeting()
   }
   
   greetingClosure.delegate = myGroovyGreeter
   greetingClosure()
```
## Java gradle
### Java Plugin
- Dependencise
```groovy
dependencies {
    <configuration> 'artifacts'
}

dependencies {
    compile 'com.google.guava:guava:18.0'
    compile files('lib/foo.jar', 'lib/bar.jar')
    compile fileTree(dir: 'lib', include: '*.jar')
}
```
- check dependencies
```groovy
gradle dependencies

gradle dependencies --configuration <name>

gradle dependencyInsight --dependencies <name of libraries>

```
###

