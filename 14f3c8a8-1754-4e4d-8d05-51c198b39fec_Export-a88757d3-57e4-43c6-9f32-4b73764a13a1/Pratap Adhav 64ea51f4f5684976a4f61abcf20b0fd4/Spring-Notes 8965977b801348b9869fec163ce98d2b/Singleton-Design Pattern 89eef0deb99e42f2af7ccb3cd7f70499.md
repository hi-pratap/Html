# Singleton-Design Pattern

Created: June 26, 2023 10:18 PM
Select: Design-Pattern

<aside>
💡

The Singleton Design Pattern is a creational design pattern that ensures a class has only one instance, and provides a global point of access to that instance. This pattern is useful when you need to restrict the instantiation of a class to a single object, which can be shared across the entire application.

In Java, the Singleton Design Pattern typically involves the following characteristics:

1. **Private constructor**: The class's constructor is made private to prevent direct instantiation of objects from outside the class.
2. **Static instance**: The class maintains a static reference to the single instance of itself.
3. **Static method**: A static method is provided to access the single instance, typically named `getInstance()`. This method checks if an instance exists and either creates a new instance or returns the existing one.

Let's see an example to illustrate the Singleton Design Pattern in Java:

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Private constructor to prevent instantiation.
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void doSomething() {
        System.out.println("Singleton instance is doing something.");
    }
}

```

In this example, the `Singleton` class has a private constructor, preventing direct instantiation from outside the class. The `getInstance()` method provides the global point of access to the single instance of the `Singleton` class. If no instance exists, it creates a new one; otherwise, it returns the existing instance.

You can use the `getInstance()` method to access the single instance of the `Singleton` class from anywhere in your code, like this:

```java
public class Main {
    public static void main(String[] args) {
        Singleton singleton = Singleton.getInstance();
        singleton.doSomething(); // Output: Singleton instance is doing something.
    }
}

```

In this example, calling `getInstance()` returns the same instance of the `Singleton` class every time it is invoked. This ensures that there is only one instance of the class throughout the application's lifecycle.

The Singleton Design Pattern is commonly used in scenarios where a single object needs to coordinate actions across the system, such as managing resources or maintaining a central configuration. However, it's important to consider the potential drawbacks and thread-safety concerns when using the Singleton pattern in a multi-threaded environment.

</aside>