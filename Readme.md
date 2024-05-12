# Design Pattern's Revision 


# Creational Design Patterns in Java

Creational design patterns deal with object creation mechanisms, making the process more flexible and efficient. 

## Singleton Pattern

### Overview
The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.

### Example
```java
 class Singleton {
    private static Singleton instance;
    private Singleton() {}
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
## Factory Method Pattern

### Overview
The Factory Method pattern defines an interface for creating objects but allows subclasses to alter the type of objects that will be created.

### Example
```java
public interface Product {
    void doSomething();
}

public class ConcreteProduct implements Product {
    @Override
    public void doSomething() {
        // Implementation
    }
}

public interface Creator {
    Product createProduct();
}

public class ConcreteCreator implements Creator {
    @Override
    public Product createProduct() {
        return new ConcreteProduct();
    }
}
```

## Abstract Factory Pattern

### Overview
The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.

### Example
```java
public interface AbstractFactory {
    ProductA createProductA();
    ProductB createProductB();
}

public class ConcreteFactory1 implements AbstractFactory {
    @Override
    public ProductA createProductA() {
        return new ConcreteProductA1();
    }

    @Override
    public ProductB createProductB() {
        return new ConcreteProductB1();
    }
}

public class ConcreteFactory2 implements AbstractFactory {
    @Override
    public ProductA createProductA() {
        return new ConcreteProductA2();
    }

    @Override
    public ProductB createProductB() {
        return new ConcreteProductB2();
    }
}
````

## Builder Pattern

### Overview
The Builder pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

### Example
```java
public class Product {
    private String property1;
    private String property2;

    public Product(String property1, String property2) {
        this.property1 = property1;
        this.property2 = property2;
    }
}

public class ProductBuilder {
    private String property1;
    private String property2;

    public ProductBuilder setProperty1(String property1) {
        this.property1 = property1;
        return this;
    }

    public ProductBuilder setProperty2(String property2) {
        this.property2 = property2;
        return this;
    }

    public Product build() {
        return new Product(property1, property2);
    }
}
````

## Prototype Pattern

### Overview
The Prototype pattern allows you to create new objects by cloning existing instances, reducing the need for subclassing.

### Example
```java
public abstract class Prototype implements Cloneable {
    @Override
    public Prototype clone() throws CloneNotSupportedException {
        return (Prototype) super.clone();
    }
}



public class ConcretePrototype extends Prototype {
    // Implementation
}
```
# Structural Design Patterns in Java

Structural design patterns focus on how classes and objects are composed to form larger structures. They help ensure that if one part of a system changes, the entire system does not need to do so.

## Adapter Pattern

### Overview
The Adapter pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces.

### Example
```java
public interface Target {
    void request();
}

public class Adaptee {
    public void specificRequest() {
        // Adaptee's specific request
    }
}

public class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        adaptee.specificRequest();
    }
}
```

## Bridge Pattern

### Overview
The Bridge pattern separates abstraction from implementation, allowing them to vary independently.

### Example
```java
public interface Implementor {
    void operationImpl();
}

public abstract class Abstraction {
    protected Implementor implementor;

    public Abstraction(Implementor implementor) {
        this.implementor = implementor;
    }

    public abstract void operation();
}

public class ConcreteImplementor implements Implementor {
    @Override
    public void operationImpl() {
        // Implementation
    }
}

public class RefinedAbstraction extends Abstraction {
    public RefinedAbstraction(Implementor implementor) {
        super(implementor);
    }

    @Override
    public void operation() {
        implementor.operationImpl();
    }
}
```

## Composite Pattern

### Overview
The Composite pattern composes objects into tree structures to represent part-whole hierarchies. It allows clients to treat individual objects and compositions of objects uniformly.

### Example
```java
public interface Component {
    void operation();
}

public class Leaf implements Component {
    @Override
    public void operation() {
        // Leaf operation
    }
}

public class Composite implements Component {
    private List<Component> children = new ArrayList<>();

    public void add(Component component) {
        children.add(component);
    }

    @Override
    public void operation() {
        for (Component component : children) {
            component.operation();
        }
    }
}
```

## Decorator Pattern

### Overview
The Decorator pattern attaches additional responsibilities to objects dynamically, providing a flexible alternative to subclassing for extending functionality.

### Example
```java
public interface Component {
    void operation();
}

public class ConcreteComponent implements Component {
    @Override
    public void operation() {
        // Original operation
    }
}

public abstract class Decorator implements Component {
    protected Component component;

    public Decorator(Component component) {
        this.component = component;
    }

    @Override
    public void operation() {
        component.operation();
    }
}

public class ConcreteDecorator extends Decorator {
    public ConcreteDecorator(Component component) {
        super(component);
    }

    @Override
    public void operation() {
        super.operation();
        // Additional operation
    }
}
```

## Facade Pattern

### Overview
The Facade pattern provides a unified interface to a set of interfaces in a subsystem, simplifying usage for clients.

### Example
```java
public class Subsystem1 {
    public void operation1() {
        // Subsystem1 operation
    }
}

public class Subsystem2 {
    public void operation2() {
        // Subsystem2 operation
    }
}

public class Facade {
    private Subsystem1 subsystem1;
    private Subsystem2 subsystem2;

    public Facade() {
        subsystem1 = new Subsystem1();
        subsystem2 = new Subsystem2();
    }

    public void operation() {
        subsystem1.operation1();
        subsystem2.operation2();
    }
}
```

## Flyweight Pattern

### Overview
The Flyweight pattern minimizes memory usage by sharing data with similar objects. It is used when the large number of objects can be replaced with a few shared objects.

### Example
```java
import java.util.HashMap;
import java.util.Map;

public class FlyweightFactory {
    private static final Map<String, Flyweight> flyweights = new HashMap<>();

    public static Flyweight getFlyweight(String key) {
        if (!flyweights.containsKey(key)) {
            flyweights.put(key, new ConcreteFlyweight());
        }
        return flyweights.get(key);
    }
}

public interface Flyweight {
    void operation();
}

public class ConcreteFlyweight implements Flyweight {
    @Override
    public void operation() {
        // Operation implementation
    }
}

public class Client {
    public void execute() {
        Flyweight flyweight = FlyweightFactory.getFlyweight("shared");
        flyweight.operation();
    }
}
```

## Proxy Pattern

### Overview
The Proxy pattern provides a surrogate or placeholder for another object to control access to it.

### Example
```java
public interface Subject {
    void request();
}

public class RealSubject implements Subject {
    @Override
    public void request() {
        // Real subject request
    }
}

public class Proxy implements Subject {
    private RealSubject realSubject;

    @Override
    public void request() {
        if (realSubject == null) {
            realSubject = new RealSubject();
        }
        realSubject.request();
    }
}
```

These structural design patterns offer solutions for creating larger structures while keeping the individual components flexible and easy to manage
.

