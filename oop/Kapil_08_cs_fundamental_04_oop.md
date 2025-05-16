# 04-solid-01.md & # 05-solid-02.md

### SOLID Design Principles and Patterns:
1. The SOLID principles are a set of design principles that help in writing maintainable and scalable code:
- **Single Responsibility Principle (SRP):** A class/method/packages should have only one reason to change, meaning it should have a single responsibility.
- **Open/Closed Principle (OCP):** Software entities should be open for extension but closed for modification.
- **Liskov Substitution Principle (LSP):** Objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program.
- **Interface Segregation Principle (ISP):** Lean interfaces - Clients should not be forced to depend on interfaces they do not use.
- **Dependency Inversion Principle (DIP):** concrete class should depend on interfaces/abstraction rather then concrete class - High-level modules should not depend on low-level modules. Both should depend on abstractions.

*  https://chatgpt.com/c/6814eda2-57e4-8005-aa5f-1ec7d6dd8ec8 

S – Single Responsibility Principle (SRP) - One class should have only one reason to change.

    A class should do one thing and do it well.
    Example: A class that handles both file reading and data parsing should be split into two separate classes.

   <p align="center">
    <img
        src="https://miro.medium.com/max/1400/1*P3oONz9Da3Tc1w97fMV73Q.png"
        alt="Single responsibility principle"
        width="500"
    />
   </p>

O – Open/Closed Principle (OCP) - Software entities should be open for extension, but closed for modification.

    You should be able to add new functionality without changing existing code.
    Achieved via inheritance or interfaces.
    Example: Use interfaces and polymorphism so new behaviors can be added without touching existing logic.

L – Liskov Substitution Principle (LSP) - Subtypes must be substitutable for their base types.

    If class B is a subclass of class A, then A’s objects should be replaceable with B’s without altering program correctness.
    Violations often happen when a subclass overrides a behavior in a way that breaks expectations.

I – Interface Segregation Principle (ISP) - Lean interfaces - Clients should not be forced to depend on interfaces they do not use.

![Interface Segregation Principle](https://www.globalnerdy.com/wordpress/wp-content/uploads/2009/07/interface_segregation_principle_thumb.jpg)

    It's better to have many small, specific interfaces than a large, all-purpose one.
    Example: Bird and Penguin shouldn't implement the same Flyable interface if penguins can't fly.

D – Dependency Inversion Principle (DIP) - concrete class should depend on interfaces/abstraction rather then concrete class - High-level modules should not depend on low-level modules. Both should depend on abstractions.

![Dependency Inversion Principle](https://www.globalnerdy.com/wordpress/wp-content/uploads/2009/07/dependency_inversion_principle_thumb.jpg)

    Use interfaces or abstract classes so high-level components aren't tightly coupled to low-level details.
    In Java, this often involves Dependency Injection frameworks like Spring.



1. Single Responsibility Principle (SRP)

```Java 
        //Bad Example – One class doing too much:
        
        public class Report {
        public String getContent() {
        return "Report Content";
        }
        
            public void saveToFile(String filename) {
                // Code to save to file
            }
        }
        
        //Good Example – Split responsibilities:
        
        public class Report {
        public String getContent() {
        return "Report Content";
        }
        }
        
        public class ReportSaver {
        public void saveToFile(Report report, String filename) {
        // Code to save report content to file
        }
        }
```  

2. Open/Closed Principle (OCP)

```Java
        //Bad Example – Modifying existing code:
        
        public class Shape {
        public double area() {
        return 0;
        }
        }
        
        public class Circle extends Shape {
        public double area() {
            return Math.PI * radius * radius;
        }
        }
        
        //Good Example – Extending functionality:
        
        public abstract class Shape {
            public abstract double area();
        }
        
        public class Circle extends Shape {
            public double area() {
                return Math.PI * radius * radius;
            }
        }
        
        public class Square extends Shape {
            public double area() {
                return side * side;
            }
        }
```

3. Liskov Substitution Principle (LSP)

```Java
        //Bad Example – Violating LSP:
        
        public class Bird {
        public void fly() {
        // Flying logic
        }
        }
        
        public class Ostrich extends Bird {
            @Override
            public void fly() {
                throw new UnsupportedOperationException("Ostrich can't fly");
            }
        }
        
        //Good Example – Correctly using inheritance:
        
        public abstract class Bird {
            public abstract void move();
        }
        
        public class Sparrow extends Bird {
            @Override
            public void move() {
                // Flying logic
            }
        }
        
        public class Ostrich extends Bird {
            @Override
            public void move() {
                // Running logic
            }
        }
```

4. Interface Segregation Principle (ISP)

```Java
            Bad Example – Fat interface:
    
            public interface Worker {
                void work();
                void eat();
            }
            
            public class Robot implements Worker {
                public void work() {}
                public void eat() { /* not applicable */ }
            }
            
            Good Example – Split interfaces:
            
            public interface Workable {
                void work();
            }
            
            public interface Eatable {
                void eat();
            }
            
            public class Human implements Workable, Eatable {
                public void work() {}
                public void eat() {}
            }
            
            public class Robot implements Workable {
                public void work() {}
            }
```

5. Dependency Inversion Principle(DIP)

```Java

       The Problem Without DIP:
        
        If you directly create or depend on low-level classes inside your business logic, any change in the low-level class breaks or requires modification in your core logic.
        ❌ Without DIP (Tightly Coupled):
        
        public class FileLogger {
            public void log(String message) {
                System.out.println("Logging to file: " + message);
            }
        }
        
        public class OrderService {
            private FileLogger logger = new FileLogger();
        
            public void placeOrder() {
                // Order logic
                logger.log("Order placed.");
            }
        }
        
            OrderService is tightly coupled to FileLogger. You can't easily switch to DBLogger, ConsoleLogger, etc.
        
        ✅ With DIP (Loosely Coupled):
        Step 1: Define an abstraction
        
        public interface Logger {
            void log(String message);
        }
        
        Step 2: Create multiple implementations
        
        public class FileLogger implements Logger {
            public void log(String message) {
                System.out.println("Logging to file: " + message);
            }
        }
        
        public class ConsoleLogger implements Logger {
            public void log(String message) {
                System.out.println("Console log: " + message);
            }
        }
        
        Step 3: Depend on abstraction in the high-level module
        
        public class OrderService {
            private Logger logger;
        
            // Constructor Injection (preferred)
            public OrderService(Logger logger) {
                this.logger = logger;
            }
        
            public void placeOrder() {
                // Order logic
                logger.log("Order placed.");
            }
        }
        
        Step 4: Configure in main or via Dependency Injection framework
        
        public class App {
            public static void main(String[] args) {
                Logger logger = new FileLogger(); // or new ConsoleLogger()
                OrderService service = new OrderService(logger);
                service.placeOrder();
            }
        }
```

### OOPS Concepts - fastly read through below .md files
* Java main concepts  
  - Inheritance - 
  - Polymorphism - it achieved through method overloading and method overriding
  - Encapsulation - 
  - Abstraction - it achieved through abstract class and interface

 - 01-oop-introduction.md
 - 02-constructors-inheritance.md
 - 03-polymorphism.md 
 - 04-interfaces-abstract.md

### Design Patterns (GOF)

* GOF - Gang of Four - Design Patterns

##### Creational 
* Creational patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

  * Singleton - 01-singleton-builder.md
  * Builder   - 01-singleton-builder.md
  * Prototype - 02-prototype-factory.md
  * Simple Factory, Factory Method, Abstract Factory -  https://chatgpt.com/c/68261a12-980c-8005-a0e2-a7f37d442319

##### Structural 
* Structural patterns are concerned with how classes and objects are composed to form larger structures

  * Adapter/wrapper - 05-adapter-flyweight.md
  * Facade    - 06-decorator-facade.md  -- Provide a unified and simplified interface to a complex subsystem. It hides the complexities of the system from the client
  * Decorator - 06-decorator-facade.md  -- Attach additional responsibilities to an object dynamically without altering its structure
  * Flyweight - 05-adapter-flyweight.md
  * Proxy - provides a surrogate or placeholder for another object to control access to it.
      * Add additional functionality (e.g., logging, lazy loading, security). 
      * Delay the object’s creation until necessary.
      * Restrict access (e.g., permissions, caching).

##### Behavioral 
* How objects interact and communicate with each other
  * Observer - 07-facade-observer.md
  * Strategy - 08-observer-strategy.md - Define a family of algorithms, encapsulate each one, and make them interchangeable.


### Reading list
* [SOLID - Recap](https://www.cs.odu.edu/~zeil/cs330/latest/Public/solid/)



 