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

.

