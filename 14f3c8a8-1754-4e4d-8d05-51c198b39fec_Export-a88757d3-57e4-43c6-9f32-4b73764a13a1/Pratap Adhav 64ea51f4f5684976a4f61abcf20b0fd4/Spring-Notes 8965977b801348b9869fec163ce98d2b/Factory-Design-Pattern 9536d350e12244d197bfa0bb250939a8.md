# Factory-Design-Pattern

Created: June 26, 2023 10:14 PM
Date: June 26, 2023
Select: Design-Pattern

<aside>
💡

Certainly! The Factory Design Pattern is a creational design pattern that provides an interface for creating objects, but allows subclasses to decide which class to instantiate. It encapsulates the object creation logic, making it easier to manage and maintain your code.

In Java, the Factory Design Pattern typically involves the following components:

1. **Product**: This is the common interface or abstract class that represents the objects the factory creates.
2. **Concrete Products**: These are the specific implementations of the Product interface or abstract class.
3. **Factory**: This is the class responsible for creating objects based on a given input or condition. It typically contains a factory method that returns an instance of the Product.

Let's see an example to illustrate the Factory Design Pattern in Java. Suppose we have a simple interface called `Shape`:

```java
public interface Shape {
    void draw();
}

```

Now, we can define concrete implementations of the `Shape` interface, such as `Circle`, `Rectangle`, and `Square`:

```java
public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle.");
    }
}

public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle.");
    }
}

public class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a square.");
    }
}

```

Next, we create a factory class called `ShapeFactory` that encapsulates the object creation logic:

```java
public class ShapeFactory {
    public Shape createShape(String shapeType) {
        if (shapeType.equalsIgnoreCase("circle")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("rectangle")) {
            return new Rectangle();
        } else if (shapeType.equalsIgnoreCase("square")) {
            return new Square();
        }
        return null; // Return null or throw an exception for unsupported shape types.
    }
}

```

Finally, we can use the `ShapeFactory` to create instances of different shapes:

```java
public class Main {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();

        Shape circle = factory.createShape("circle");
        circle.draw(); // Output: Drawing a circle.

        Shape rectangle = factory.createShape("rectangle");
        rectangle.draw(); // Output: Drawing a rectangle.

        Shape square = factory.createShape("square");
        square.draw(); // Output: Drawing a square.
    }
}

```

In this example, the `ShapeFactory` acts as the factory, and it decides which concrete implementation of the `Shape` interface to create based on the input string. This way, the client code (in the `Main` class) does not need to be concerned with the details of object creation.

The Factory Design Pattern provides a flexible and extensible way to create objects. If

</aside>