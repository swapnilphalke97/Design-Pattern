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
interface Shape {
    void draw();
}

// Concrete products
class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
// Factory class
class ShapeFactory {
    public Shape createShape(String type) {
        if (type.equalsIgnoreCase("rectangle")) {
            return new Rectangle();
        } else if (type.equalsIgnoreCase("circle")) {
            return new Circle();
        }
        return null;
    }
}
// Client code
public class Main {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();

        // Create a rectangle
        Shape rectangle = factory.createShape("rectangle");
        rectangle.draw();

        // Create a circle
        Shape circle = factory.createShape("circle");
        circle.draw();
    }
}
```


## Abstract Factory Pattern

### Overview
The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.

### Example
```java
interface Shape {
    void draw();
}

// Concrete products
class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing Square");
    }
}
// Abstract product B
interface Color {
    void fill();
}

// Concrete products
class Red implements Color {
    @Override
    public void fill() {
        System.out.println("Filling with Red color");
    }
}

class Blue implements Color {
    @Override
    public void fill() {
        System.out.println("Filling with Blue color");
    }
}
interface AbstractFactory {
    Shape createShape();
    Color createColor();
}

// Concrete Factory A
class ShapeFactory implements AbstractFactory {
    @Override
    public Shape createShape() {
        return new Circle();
    }

    @Override
    public Color createColor() {
        return new Red();
    }
}
// Concrete Factory B
class ColorFactory implements AbstractFactory {
    @Override
    public Shape createShape() {
        return new Square();
    }

    @Override
    public Color createColor() {
        return new Blue();
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        AbstractFactory shapeFactory = new ShapeFactory();
        Shape shape = shapeFactory.createShape();
        shape.draw();

        AbstractFactory colorFactory = new ColorFactory();
        Color color = colorFactory.createColor();
        color.fill();
    }
}


```

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
java
// Prototype interface
interface Prototype extends Cloneable {
    Prototype clone();
}

// Concrete prototype class
class ConcretePrototype implements Prototype {
    private int number;

    public ConcretePrototype(int number) {
        this.number = number;
    }

    @Override
    public Prototype clone() {
        return new ConcretePrototype(this.number);
    }

    public int getNumber() {
        return number;
    }
}
// Client code
public class Main {
    public static void main(String[] args) {
        ConcretePrototype prototype = new ConcretePrototype(10);
        ConcretePrototype clonedPrototype = (ConcretePrototype) prototype.clone();

        System.out.println("Original Prototype Number: " + prototype.getNumber());
        System.out.println("Cloned Prototype Number: " + clonedPrototype.getNumber());
    }
}
    
```
# Structural Design Patterns in Java

Structural design patterns focus on how classes and objects are composed to form larger structures. They help ensure that if one part of a system changes, the entire system does not need to do so.

## Adapter Pattern

### Overview
The Adapter pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces.

### Example
```java
[source](https://refactoring.guru/design-patterns/adapter)
class RoundHole is
    constructor RoundHole(radius) { ... }
    method getRadius() is
    method fits(peg: RoundPeg) is
        return this.getRadius() >= peg.getRadius()

class RoundPeg is
    constructor RoundPeg(radius) { ... }
    method getRadius() is.

class SquarePeg is
    constructor SquarePeg(width) { ... }

    method getWidth() is

class SquarePegAdapter extends RoundPeg is
    private field peg: SquarePeg

    constructor SquarePegAdapter(peg: SquarePeg) is
        this.peg = peg

    method getRadius() is
        return peg.getWidth() * Math.sqrt(2) / 2

hole = new RoundHole(5)
rpeg = new RoundPeg(5)
hole.fits(rpeg) 

small_sqpeg = new SquarePeg(5)
large_sqpeg = new SquarePeg(10)
hole.fits(small_sqpeg) // (incompatible types)

small_sqpeg_adapter = new SquarePegAdapter(small_sqpeg)
large_sqpeg_adapter = new SquarePegAdapter(large_sqpeg)
hole.fits(small_sqpeg_adapter) // true
hole.fits(large_sqpeg_adapter) // false
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

