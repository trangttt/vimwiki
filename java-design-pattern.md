# Creational
## Factory method
## Abstract Factory
- create objects with multiple properties related or dependent to each other.
```java
[abstract](abstract) class AbstractFactory {
    default Factory getFactory(type){
        switch ( case ) {
            return; //corresponding factory
        }
    }
  
    Product createProduct(ProductType type);
}

class Factory1 extends AbstractFactory {
    Product1 createProduct(ProductType type){};
}

class Factory2 extends AbstractFactory {
    Product2 createProduct(ProductType type){};
}

interface Product {};
interface ProductType {};

class Product1ProductType1 implements Product;
class Product2ProductType2 implements Product;

class ProductType1 implements ProductType;
class ProductType2 implements ProductType;

```
## Prototype
- used when there are many properties needed to set to create certain object
```java
interface Prototype {
    Prototype clone();
}

class Product1 implements Prototype {
    Prototype clone(){

    }
}

class Product2 implements Prototype {
    Prototype clone(){

    }
}
```
- avoid using "new", -> create a new instance without knowing that class, instead only knows interface
```java
Product i = product.clone();
```
- allows to create new object at run-time 
- avoid extra classes as in Factory
## Builder
- Delay generating objects when all properties are know, at that time, at the ability of checking the correctness of all properties
```java
class Product {
    class Builder {
        public Builder (){
            return this;
        }
        public A(A a);
        public B(B b);
        
        public Produc build(){
            return Product(a, b);
        }
    }
}
```
## Singleton
# Structural
## Adapter
- Create a unique class that can convert interfaces/classes to another classes/interfaces that client expects.
## Bridge
- Bridge the gap between abstract/interface and actual implementation. Then, abstract and implementation can elvove independently.
## Proxy
## Flyweight
## Facade
- Acts as a representative to another subsystem
```java
class SubsystemFacade {
    Part1 p1;
    Part2 p2;
    ...
    void act1() {
        p1.act1();
    }
    
    void act2(){
        p2.act2();
    }
}
```
## Composite
- Compose objects into a tree structures to represent a whole-part hierarchies.
- each parts behave like a composite. A composite can contain another composite.
```java
interface Graphic {
    void draw();
} ;

class Line implements Graphic;
class Triangle implements Graphics;

class Graph implements Graphic {
    List<Graphic> items = { Line, Triangle }
    
    void draw(
        for(item: items)
            item.draw();
    );
}
```
## Decorator
# Behavioral
## Chain of responsibility
```java
class Handler {
    Handler nextHandler;
    
    void handle(){
        if ( canHandle ){
            handle();
        }
        else {
            nextHandler.handle();
        }
    }
}
```
## Command
```java
interface Command {
    publci void execute(){

    }
}
```
- decouple the object that invokes the operations from the one that know how to perform it.
- command is a first-class object. You can extended and be manipulated.
- command can be assemble into a composite command.
- easy to add new command.
## State
```java
class Item {
    private State current_state;
    public Item(){
        current_state = new State1();
    }
    
    public void doSmething(){
        current_state.doSomething();
    }
}

interface State {
    public void doSomething(){
    }
}

class State1{
    public void doSomething(){};
}

class State2{
    public void doSomething(){};
}
```
## Memento
## Strategy
```java
interface Strategy {
    public void solve();
}

abstract class SolvingMethodTemplate implements Strategy {
    public void solve(){
        step1();
        step2();
        step3();
    } 
    
    protected abstract void step1();
    protected abstract void step2();
    protected abstract void step3();
}


class SolvingMethod1 extends SolvingMethodTemplate {
    protected void step1(){}
    protected void step2(){}
    protected void step3(){};
}

class SolvingMethod2 extends SolvingMethodTemplate {
    protected void step1();
    protected void step2();
    protected void step3();
}
```
## Visitor
- Represents a type of operation performed on group of elements.
- Let you define operations on an instance without changing the class.
- Do the right thing based on the type of the instance.
```java
interface Element{
    public void accept(Visitor v);
}
interface Visitor {
    void visit(Element e);
}

class Element1 implements Element {
    public void accept(Visitor v){
        v.visit(this);
    }
    
    public void e1();
}

class Element2 implements Element {
    public void accept(Visitor v){
        v.visit(this);
    }
    public void e2();
}


class UpVisitor implements Visitor {
    
    public void visit(Element1 e){
        going_up();
        e.e1();
    }
    
    public void visit(Element2 e){
        going_up();
        e.e2();
    }
}

class DownVisitor implements Visitor {
    public void visit(Element1 e){
        going_down();
        e.e1();
    }
    
    public void visit(Element2 e){
        going_down();
        e.e2();
    }
}
```

## Observer
```java
interface Observer {
    public void update();
}

class Observer1 implements Observer {
    public void update();
}

class Observer2 implements Observer {
    public void udpate();
}

class Item {
    Observer[] observers;
    
    public void notify(Event e){
        for(Observer o: observers)
            o.update();
    }
}
```
