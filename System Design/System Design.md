# System Design Interview Preparation Guide

**Last Updated:** December 2024
**Purpose:** Comprehensive guide for system design interviews (SDE-2 to Senior levels)

## 📋 Table of Contents

### **Part I: Fundamentals**
1. [System Design Overview](#system-design-overview)
2. [Low-Level Design (LLD) Fundamentals](#low-level-design-lld-fundamentals)
3. [Design Patterns](#design-patterns)
4. [High-Level Design (HLD) Introduction](#high-level-design-introduction)

### **Part II: Core Concepts**
5. [Web Applications & Architecture](#web-applications--architecture)
6. [Distributed Systems](#distributed-systems)
7. [Databases & Storage](#databases--storage)
8. [Scalability & Performance](#scalability--performance)
9. [Caching Strategies](#caching-strategies)
10. [Load Balancing](#load-balancing)

### **Part III: Advanced Topics**
11. [Microservices Architecture](#microservices-architecture)
12. [Message Queues & Event-Driven Architecture](#message-queues--event-driven-architecture)
13. [Content Delivery Networks (CDN)](#content-delivery-networks-cdn)
14. [Security & Authentication](#security--authentication)
15. [Monitoring & Observability](#monitoring--observability)

### **Part IV: Interview Preparation**
16. [System Design Interview Framework](#system-design-interview-framework)
17. [Common System Design Questions](#common-system-design-questions)
18. [Case Studies](#case-studies)
19. [Best Practices & Tips](#best-practices--tips)

---

---

## System Design Overview

System design is the process of defining the architecture, components, modules, interfaces, and data for a system to satisfy specified requirements. It bridges the gap between problem definition and implementation.

### **🎯 What is System Design?**

System design involves two main levels:
- **High-Level Design (HLD):** Architecture overview, component interactions, data flow
- **Low-Level Design (LLD):** Detailed implementation, classes, methods, data structures

### **🔍 Problem Identification & Requirements**

**Real-world applications solve various problems:**
- **Transportation:** Uber, Lyft, Ola
- **E-commerce:** Amazon, Flipkart, eBay
- **Social Media:** Facebook, Twitter, Instagram
- **Streaming:** Netflix, YouTube, Spotify
- **Communication:** WhatsApp, Slack, Zoom
- **Food Delivery:** DoorDash, Zomato, Swiggy

**Requirements Sources:**
- **Functional Requirements:** What the system should do
- **Non-Functional Requirements:** How the system should perform
- **Business Requirements:** Market needs and constraints
- **Technical Requirements:** Platform and technology constraints

### **📋 System Design Process**

```
1. Requirements Gathering → 2. Capacity Estimation → 3. System Interface Definition
         ↓                           ↓                           ↓
4. High-Level Design → 5. Database Design → 6. Detailed Component Design
         ↓                           ↓                           ↓
7. Scalability → 8. Security → 9. Monitoring → 10. Deployment
```

### **🚀 Product Development Lifecycle**

**MVP Development Flow:**
```
Idea → Market Research → POC → Prototype → MVP → Product → Scale
```

- **POC (Proof of Concept):** Validates technical feasibility
- **Prototype:** Early model to test concepts
- **MVP (Minimal Viable Product):** Simplest version with core features
- **Product:** Full-featured version
- **Scale:** Optimized for growth

**Feature Roadmap Example (Social Media App):**
- **Phase 1:** User registration, profiles, basic posting
- **Phase 2:** Friend connections, likes, comments
- **Phase 3:** Real-time chat, notifications
- **Phase 4:** Media upload, stories, advanced features

### **🏗️ Infrastructure Components**

Every system relies on three fundamental pillars:

1. **Compute:** Processing power and application logic
   - Application servers, microservices
   - Background job processors
   - Real-time processing engines

2. **Storage:** Data persistence and retrieval
   - Databases (SQL/NoSQL)
   - File storage systems
   - Data warehouses

3. **Network:** Communication and connectivity
   - Load balancers
   - CDNs (Content Delivery Networks)
   - API gateways

### **📊 Scale Considerations**

**User Scale Examples:**
- **Small:** 1K-10K users (single server)
- **Medium:** 10K-1M users (multiple servers, load balancer)
- **Large:** 1M-10M users (microservices, caching, CDN)
- **Massive:** 10M+ users (distributed systems, global infrastructure)

---

## Low-Level Design (LLD) Fundamentals

Low-Level Design focuses on the detailed design of individual components, classes, and their interactions. It's crucial for creating maintainable, scalable, and robust software systems.

### **🎯 LLD Objectives**

- **Maintainability:** Easy to modify and extend
- **Reusability:** Components can be reused across projects
- **Testability:** Easy to write unit tests
- **Readability:** Code is self-documenting and clear
- **Performance:** Efficient algorithms and data structures

### **🏗️ Object-Oriented Programming (OOP) Concepts**

#### **Core OOP Principles:**

1. **Classes & Objects**
   ```java
   // Class - Blueprint
   public class Car {
       private String model;
       private String color;

       public void start() { /* implementation */ }
       public void stop() { /* implementation */ }
   }

   // Object - Instance
   Car myCar = new Car();
   ```

2. **Encapsulation**
   - Bundle data and methods together
   - Control access through access modifiers
   - Hide internal implementation details

3. **Inheritance**
   - Code reuse through parent-child relationships
   - "IS-A" relationship
   ```java
   public class Vehicle { /* base class */ }
   public class Car extends Vehicle { /* derived class */ }
   ```

4. **Polymorphism**
   - **Compile-time:** Method overloading
   - **Runtime:** Method overriding, interface implementation

5. **Abstraction**
   - Hide complex implementation details
   - Provide simple interfaces
   - Use abstract classes and interfaces

### **📐 Design Principles**

#### **SOLID Principles:**

1. **Single Responsibility Principle (SRP)**
   - A class should have only one reason to change
   - Each class should have a single, well-defined purpose

2. **Open/Closed Principle (OCP)**
   - Open for extension, closed for modification
   - Use interfaces and inheritance for extensibility

3. **Liskov Substitution Principle (LSP)**
   - Subtypes must be substitutable for their base types
   - Derived classes should extend, not replace, base functionality

4. **Interface Segregation Principle (ISP)**
   - Clients shouldn't depend on interfaces they don't use
   - Create specific, focused interfaces

5. **Dependency Inversion Principle (DIP)**
   - Depend on abstractions, not concretions
   - High-level modules shouldn't depend on low-level modules

#### **Additional Principles:**

- **DRY (Don't Repeat Yourself):** Eliminate code duplication
- **YAGNI (You Aren't Gonna Need It):** Don't add functionality until needed
- **KISS (Keep It Simple, Stupid):** Prefer simple solutions
- **Composition over Inheritance:** Favor object composition over class inheritance

### **S - Single Responsibility Principle (SRP):**

- **Concept:** A class should have only one reason to change. This means a class should have only one responsibility or one function.
- **Analogy:** A "Doctor" class might be too broad; it should be broken down into `General Physicians (MBBS)` and `Specialists (Masters)`.
- **Violation Example (Java Code):**

    ```java
    import java.util.Date;

    //this is a class violating SRP
    public class Employee {
        private int id;
        private String name;
        private Date doj;

    		//constructor
        public Employee(int id, String name, Date doj) {
            this.id = id;
            this.name = name;
            this.doj = doj;
        }

        //Decided by company board of directors
        public void calculateSalary() {
            System.out.println("Logic for calculating salary.");
        }

        //Decided by HR team
        public void hireEmployee() {
            System.out.println("Logic for hiring employee.");
        }

        //Decided by Managers and evaluation team
        public void evaluateEmployee() {
            System.out.println("Logic for evaluating team.");
        }

        public int getId() {
            return id;
        }

        public void setId(int id) {
            this.id = id;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public Date getDoj() {
            return doj;
        }

        public void setDoj(Date doj) {
            this.doj = doj;
        }
    }

    public class Program {
        public static void main(String[] args) {
            Employee emp = new Employee(1, "abc", new Date());
            System.out.println("Employee id : " + emp.getId());
            System.out.println("Employee name : " + emp.getName());
            System.out.println("Employee date of joining : " + emp.getDoj());

            // here the class hae more than one function
            emp.hireEmployee();
            emp.calculateSalary();
            emp.evaluateEmployee();
        }
    }
    ```

    Java*Output:*

    ```
    Employee id : 1
    Employee name : abc
    Employee date of joining : <current_date_and_time>
    Logic for hiring employee.
    Logic for calculating salary.
    Logic for evaluating team.
    ```

- **SRP Following Example (Java Code):**

    ```java
    import java.util.Date;

    //this is a class following SRP because it just contains the employee information
    public class Employee {
        private int id;
        private String name;
        private Date doj;

        public Employee(int id, String name, Date doj) {
            this.id = id;
            this.name = name;
            this.doj = doj;
        }

        public int getId() {
            return id;
        }

        public void setId(int id) {
            this.id = id;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public Date getDoj() {
            return doj;
        }

        public void setDoj(Date doj) {
            this.doj = doj;
        }
    }

    public class SalaryCalculator {
        //Decided by company board of directors
        public void calculateSalary(Employee emp) {
            System.out.println("Logic for calculating salary.");
        }
    }

    public class EmployeeEvaluator {
        //Decided by Managers and evaluation team
        public void evaluateEmployee(Employee emp) {
            System.out.println("Logic for evaluating team.");
        }
    }

    public class EmployeeHiring {
        //Decided by HR team
        public void hireEmployee(Employee emp) {
            System.out.println("Logic for hiring employee.");
        }
    }

    public class Program {
        public static void main(String[] args) {
            Employee emp = new Employee(1, "abc", new Date(122, 6, 16)); // Date(year, month, day) - year is 1900 + year
            System.out.println("Employee id : " + emp.getId());
            System.out.println("Employee name : " + emp.getName());
            System.out.println("Employee date of joining : " + emp.getDoj());

            SalaryCalculator salaryCalculator = new SalaryCalculator();
            salaryCalculator.calculateSalary(emp);
            EmployeeHiring employeeHiring = new EmployeeHiring();
            employeeHiring.hireEmployee(emp);
            EmployeeEvaluator employeeEvaluator = new EmployeeEvaluator();
            employeeEvaluator.evaluateEmployee(emp);
        }
    }
    ```

    Java*Output:*

    ```
    Employee id : 1
    Employee name : abc
    Employee date of joining : Sat Jul 16 00:00:00 IST 2022
    Logic for calculating salary.
    Logic for hiring employee.
    Logic for evaluating team.
    ```


### **O - Open/Closed Principle (OCP):**

- **Concept:** Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.
- **Example (Java Code for OCP concept demonstration:**

    ```java
    public interface IAnimal {
        public void feed();
    }

    public class Dog implements IAnimal {
        @Override
        public void feed() {
            System.out.println("Feeding dog");
        }
    }

    public class Cat implements IAnimal {
        @Override
        public void feed() {
            System.out.println("Feeding cat");
        }
    }

    public class AnimalFeeder {
        public void feedAnimal(IAnimal animal) {
            animal.feed();
        }
    }

    public class Program {
        public static void main(String[] args) {
            AnimalFeeder animalFeeder = new AnimalFeeder();
            animalFeeder.feedAnimal(new Dog());
            animalFeeder.feedAnimal(new Cat());
        }
    }
    ```

    - Java*Output:*

    ```
    Feeding dog
    Feeding cat
    ```

- ***Explanation for OCP**:* The `AnimalFeeder` class is "closed for modification" because you don't need to change its `feedAnimal` method to add new animal types. It's "open for extension" because you can add new `IAnimal` implementations (e.g., `Lion`, `Horse`) without altering existing code in `AnimalFeeder`.

### **L - Liskov Substitution Principle (LSP):**

- **Concept:** Objects of a superclass should be replaceable with objects of its subclasses without breaking the application.

### **I - Interface Segregation Principle (ISP):**

- **Concept:** Clients should not be forced to depend on interfaces they do not use. Better to have many small, specific interfaces rather than one large, general-purpose interface.

### **D - Dependency Inversion Principle (DIP):**

- **Concept:** High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.

---

## Design Patterns

Design patterns are reusable solutions to commonly occurring problems in software design. They represent best practices and provide a common vocabulary for developers.

### **📚 Pattern Categories**

1. **Creational Patterns:** Object creation mechanisms
2. **Structural Patterns:** Object composition and relationships
3. **Behavioral Patterns:** Object interaction and responsibility distribution

### **🏭 Creational Patterns**

#### **1. Singleton Pattern**
**Purpose:** Ensure only one instance of a class exists globally

**Use Cases:**
- Database connections
- Logging services
- Configuration managers
- Cache managers

**Implementation Approaches:**
- **Eager Initialization:** Instance created at class loading
- **Lazy Initialization:** Instance created when first requested
- **Thread-Safe:** Using synchronization for multi-threading
- **Enum Singleton:** Most robust approach in Java

### **Singleton Design Pattern**

- **Purpose:** Ensures that a class has only one instance and provides a global point of access to that instance.
- **Analogy:** Imagine a single logging mechanism (`App.Log`) that all components (C1, C2, C3, etc.) within an application need to use to perform tasks like logging. Instead of each component creating its own logging object, they all access a single, shared logging object.

![image.png](image%201.png)

- **How to Create a Singleton:**
    1. **Private Constructor:** Make the constructor private to prevent direct instantiation of the class from outside.
    2. **Private Static Attribute of the Same Class:** Create a private static instance of the class itself within the class.
    3. **Public Static Method:** Provide a public static method (`getInstance()`) that returns the single instance of the class.
- **Implementation Examples:**
    - **Early Loading (Eager Initialization):** The instance is created when the class is loaded, even if it's not immediately needed.

        ```java
        public class SingletonExample {
            private SingletonExample() {
                System.out.println("Private Constructor");
            }
        		 // public static SingletonExample getInstance() { // return instance; //
            private static SingletonExample instance = new SingletonExample();

            public void printMessage(String message) {
                System.out.println("Message: " + message);
            }
        }

        public class Program {
            public static void main(String[] args) {
                SingletonExample se = SingletonExample.getInstance();
                se.printMessage("Hello world");
            }
        }
        ```

        *Output:*

        ```
        Private Constructor
        Message: Hello world
        ```

        *Explanation:* When `SingletonExample.getInstance()` is first called, the `instance` variable is already initialized, creating the "Private Constructor" output. Subsequent calls to `getInstance()` will return the same object without calling the constructor again.

    - **Comparison with Non-Singleton Class (for understanding):**

        ```java
        public class Demo {
            public Demo() {
                System.out.println("Demo: constructor");
            }

            public void printDemo() {
                System.out.println("Print demo");
            }
        }

        // SingletonExample class (same as above - Early Loading)
        public class SingletonExample {
            private SingletonExample() {
                System.out.println("Private Constructor");
            }

            private static SingletonExample instance = new SingletonExample();

            public static SingletonExample getInstance() {
                return instance;
            }

            public void printMessage(String message) {
                System.out.println("Message: " + message);
            }

            public static void printStaticMessage(String message) { //
                System.out.println("Static Message: " + message); //
            }
        }

        public class Program {
            public static void main(String[] args) {
                // multiple instances of Demo class
                Demo obj1 = new Demo(); //
                Demo obj2 = new Demo(); //
                Demo obj3 = new Demo(); //
                obj1.printDemo(); //
                System.out.println();

                // single instance of SingletonExample class
                SingletonExample se1 = SingletonExample.getInstance(); //
                SingletonExample se2 = SingletonExample.getInstance(); //
                SingletonExample se3 = SingletonExample.getInstance(); //
                se1.printMessage("Sample message for a non static method"); //
                SingletonExample.printStaticMessage("Static message example"); //
            }
        }
        ```

        *Output:*

        ```
        Demo: constructor
        Demo: constructor
        Demo: constructor
        Print demo

        Private Constructor
        Message: Sample message for a non static method
        Static Message: Static message example
        ```

        *Explanation:* Notice how "Demo: constructor" prints three times because three `Demo` objects are created. "Private Constructor" for `SingletonExample` prints only once, confirming a single instance.

    - **Lazy Loading (On-Demand Loading - Non-Thread Safe):** The instance is created only when it's first requested. This version is *not* thread-safe.

        ```java
        public class SingletonExample {
            private SingletonExample() {
                System.out.println("Private Constructor");
            }

            private static SingletonExample instance = null;
            public static SingletonExample getInstance() {
        			if (instance == null) {
        				instance = new SingletonExample();
              }
              return instance;
            }

            public void printMessage(String message) { //
                System.out.println("Message: " + message); //
            }

            public static void printStaticMessage(String message) { //
                System.out.println("Static Message: " + message); //
            }
        }

        public class Program {
            public static void main(String[] args) {
                SingletonExample se1 = SingletonExample.getInstance(); //
                SingletonExample se2 = SingletonExample.getInstance(); //
                SingletonExample se3 = SingletonExample.getInstance(); //

                se1.printMessage("Sample message for a non static method"); //
                SingletonExample.printStaticMessage("Static message example"); //
            }
        }
        ```

        *Output:*

        ```
        Private Constructor
        Message: Sample message for a non static method
        Static Message: Static message example
        ```

        *Explanation:* The constructor is called only when `getInstance()` is first invoked because `instance` is initially `null`. In a single-threaded environment, this works correctly.

    - **Lazy Loading (Non-Thread-Safe Issue Demonstration):** When multiple threads try to access `getInstance()` simultaneously, it can lead to multiple instances being created.

        ```java
        import java.util.concurrent.ExecutorService; // import java.util.concurrent.Executors; // public class SingletonExample {
            private SingletonExample() { //
                System.out.println("Private constructor"); //
            }

            private static SingletonExample instance = null; // public static SingletonExample getInstance() { // if (instance == null) { //
                    instance = new SingletonExample(); //
                }
                return instance; //
            }

            public void print(String message) { //
                System.out.println("Message: " + message); //
            }
        }

        public class Program {
            private static void printFirstMessage() { //
                SingletonExample obj1 = SingletonExample.getInstance(); //
                obj1.print("Message from obj 1"); //
            }

            private static void printSecondMessage() { //
                SingletonExample obj3 = SingletonExample.getInstance(); //
                obj3.print("Message from obj 2"); //
            }

            private static void printThirdMessage() { //
                SingletonExample obj1 = SingletonExample.getInstance(); //
                obj1.print("Message from obj 3"); //
            }

            public static void main(String[] args) {
                ExecutorService executorService = Executors.newCachedThreadPool(); //

                Runnable createFirstObj = () -> printFirstMessage(); //
                executorService.execute(createFirstObj); //

                Runnable createSecondObj = () -> printSecondMessage(); //
                executorService.execute(createSecondObj); // // inline
                executorService.execute(() -> printThirdMessage()); //

                executorService.shutdown(); //
            }
        }
        ```

        *Output (may vary due to thread scheduling, but will show multiple constructor calls):*

        ```
        Private constructor
        Private constructor
        Message: Message from obj 1
        Message: Message from obj 2
        Message: Message from obj 3
        ```

        *Explanation:* In a multi-threaded environment, if `getInstance()` is called by multiple threads when `instance` is `null`, race conditions can occur. Both threads might enter the `if (instance == null)` block and try to create a new instance, leading to multiple `Private constructor` outputs and breaking the singleton guarantee.

    - **Lazy Loading (Thread-Safe - Double-Checked Locking):** This approach makes the lazy initialization thread-safe by using `synchronized` blocks and `volatile` keyword.

        ```java
        import java.util.concurrent.ExecutorService; // import java.util.concurrent.Executors; // public class SingletonExample {
            private SingletonExample() { //
                System.out.println("Private constructor"); //
            }

            private static volatile SingletonExample instance; // `volatile` ensures visibility of writes across threads private static Object object = new Object(); // Lock object for synchronization public static SingletonExample getInstance() { //
                SingletonExample singletonExample = instance; // First check (no lock) if (singletonExample == null) { // If instance is null, acquire lock synchronized (object) { //
                        singletonExample = instance; // Second check (inside lock) if (singletonExample == null) { //
                            instance = singletonExample = new SingletonExample(); // Instance created
                        }
                    }
                }
                return singletonExample; //
            }

            public void print(String message) { //
                System.out.println("Message: " + message); //
            }
        }

        public class Program {
            private static void printFirstMessage() { //
                SingletonExample obj1 = SingletonExample.getInstance(); //
                obj1.print("Message from obj 1"); //
            }

            private static void printSecondMessage() { //
                SingletonExample obj3 = SingletonExample.getInstance(); //
                obj3.print("Message from obj 3"); // Note: original code prints "obj 3", but for consistency with previous print obj 2 is taken
            }

            private static void printThirdMessage() { //
                SingletonExample obj1 = SingletonExample.getInstance(); //
                obj1.print("Message from obj 1"); //
            }

            public static void main(String[] args) {
                ExecutorService executorService = Executors.newCachedThreadPool(); //

                Runnable createFirstObj = () -> printFirstMessage(); //
                executorService.execute(createFirstObj); //

                Runnable createSecondObj = () -> printSecondMessage(); //
                executorService.execute(createSecondObj); // // inline
                executorService.execute(() -> printThirdMessage()); //

                executorService.shutdown(); //
            }
        }
        ```

        *Output (consistent, only one constructor call):*

        ```
        Private constructor
        Message : Message from obj 1
        Message : Message from obj 3
        Message : Message from obj 1
        ```

        *Explanation:* The double-checked locking ensures that the instance is created only once, even with multiple threads. The `volatile` keyword ensures that changes to `instance` are immediately visible to all threads.

    - **Enum Type Singleton:** This is often considered the most robust and simplest way to implement a thread-safe singleton in Java. It inherently handles serialization and reflection issues.

        ```java
        // SingletonEnumExample.java
        public enum SingletonEnumExample { // // the variable INSTANCE shall be compiled to a public static final field of type SingletonEnumEx
            INSTANCE; // private String message; // public void SetMessage(String message) { // this.message = message; //
            }

            public void PrintDetails() { //
                System.out.println("Message : " + message); //
            }
        }

        // Demo.java (Main class to use the enum singleton)
        public class Demo {
            public static void main(String[] args) {
                // access instance of SingletonCls using getInstance() method
                SingletonEnumExample.INSTANCE.SetMessage("This message is set in main function"); //
                SingletonEnumExample.INSTANCE.PrintDetails(); //
            }
        }
        ```

        *Output:*

        ```
        Message : This message is set in main function
        ```

        *Explanation:* By declaring an enum with a single instance, `INSTANCE`, Java guarantees that only one instance of the enum type exists. This is automatically thread-safe and handles many complexities of singleton implementation.


---

# Design Patterns - II

### Factory Design Pattern

-

    **Purpose:** The Factory design pattern is a creational pattern used for the mass production of similar kinds of products1.

-

    **Analogy:** A car factory creates large numbers of similar cars, such as basic and sports cars2. The factory itself is responsible for creating different types of cars3.

- **Key Components:**
    1.

        **Interface:** An interface is used to define the actual products4444. This leverages OOP principles like inheritance and polymorphism5.

    2.

        **Child Classes:** Concrete classes are created that implement the interface6666.

    3.

        **Factory Class:** A factory class is created which is responsible for creating the objects of the different child classes7777. The client interacts with the factory to get the desired product, abstracting away the creation logic8.

- **Example: Credit Card Factory**Java
    -

        **`ICreditCard` Interface:** Defines methods for `GetCardType()`, `GetAnnualFee()`, and `GetCardLimit()`9.

    -

        **`PlatinumCard` and `TitaniumCard` Classes:** Implement `ICreditCard` with specific values for each card type10101010.

        -

            `PlatinumCard`: Annual Fee is 100, Card Limit is 1000011111111.

        -

            `TitaniumCard`: Annual Fee is 500, Card Limit is 4000012121212.

    -

        **`CreditCardFactory` Class:** Has a static method `GetCreditCardDetails(String cardType)` that returns the appropriate `ICreditCard` object based on the `cardType` string13131313.

    -

        **`Demo` Class:** Shows how a client can get a credit card object by calling the factory method without knowing the specific implementation details of the `PlatinumCard` or `TitaniumCard` classes14.


    **Code Example:**

    #

    `public interface ICreditCard {
      public String GetCardType();
      public int GetAnnualFee();
      public int GetCardLimit();
    }

    public class PlatinumCard implements ICreditCard {
      @Override
      public String GetCardType() {
        return "Platinum";
      }
      @Override
      public int GetAnnualFee() {
        return 100;
      }
      @Override
      public int GetCardLimit() {
        return 10000;
      }
    }

    public class TitaniumCard implements ICreditCard {
      @Override
      public String GetCardType() {
        return "Titanium";
      }
      @Override
      public int GetAnnualFee() {
        return 500;
      }
      @Override
      public int GetCardLimit() {
        return 40000;
      }
    }

    public class CreditCardFactory {
      public static ICreditCard GetCreditCardDetails(String cardType) {
        ICreditCard creditCard = null;
        if (cardType == "Platinum") {
          creditCard = new PlatinumCard();
        } else if (cardType == "Titanium") {
          creditCard = new TitaniumCard();
        } else {
          System.out.println("Invalid card");
        }
        return creditCard;
      }
    }

    public class Demo {
      public static void main(String[] args) {
        var creditCard = CreditCardFactory.GetCreditCardDetails("Platinum");
        if (creditCard != null) {
          System.out.println(creditCard.GetAnnualFee());
          System.out.println(creditCard.GetCardLimit());
        }
      }
    }`


### Abstract Factory Design Pattern

-

    **Purpose:** The Abstract Factory pattern is a "super factory" or "factory of factories"15151515. It is used to create families of related or dependent objects without specifying their concrete classes16.

- **Advantages:**
    -

        **Isolation:** It isolates the client code from the concrete implementation logic17.

    -

        **Consistency:** It ensures consistency among different objects18.

- **Steps to Implement:**
    1.

        **Create an Interface:** Define an interface for the products (e.g., `IAnimal` with `Speak()` and `Type()` methods)19.

    2.

        **Create Concrete Classes:** Implement the interface with specific classes (e.g., `Cat`, `Lion`, `Shark`, `Octopus`)20.

    3.

        **Create an Abstract Factory Class:** Define an abstract factory class (`AnimalFactory`) with an abstract method to get an animal (`GetAnimal`) and a static method to create the appropriate factory (`CreateAnimalFactory`)21212121.

    4.

        **Create Factory Classes:** Extend the abstract factory to create concrete factories (e.g., `LandAnimalFactory`, `SeaAnimalFactory`) that are responsible for creating objects of the concrete classes222222222222222222.

    5.

        **Factory Producer:** A class to get factories based on the type requested23.

- **Example: Animal Factory**Java
    -

        **`IAnimal` Interface:** Defines `Speak()` and `Type()` methods24.

    -

        **Concrete Animal Classes:** `Cat`, `Lion`, `Shark`, `Octopus` implement `IAnimal`25252525252525252525252525252525.

    -

        **`AnimalFactory` Abstract Class:** Has `GetAnimal(String animalType)` and `CreateAnimalFactory(String factoryType)` static method that returns a `LandAnimalFactory` or `SeaAnimalFactory`26262626.

    -

        **`LandAnimalFactory` and `SeaAnimalFactory` Classes:** Extend `AnimalFactory` and implement `GetAnimal()` to return a specific land or sea animal object27272727.

    -

        **`Demo` Class:** Shows how a client gets an animal object by first getting the correct factory and then using that factory to create the animal28.


    **Code Example:**

    #

    `public interface IAnimal {
        public String Speak();
        public String Type();
    }

    public class Cat implements IAnimal {
        @Override
        public String Speak() {
            return "Meow";
        }
        @Override
        public String Type() {
            return "Cat";
        }
    }

    public class Lion implements IAnimal {
        @Override
        public String Speak() {
            return "Roar";
        }
        @Override
        public String Type() {
            return "Lion";
        }
    }

    public class Shark implements IAnimal {
        @Override
        public String Speak() {
            return "Cannot speak";
        }
        @Override
        public String Type() {
            return "Shark";
        }
    }

    public class Octopus implements IAnimal {
        @Override
        public String Speak() {
            return "SQUAWCK";
        }
        @Override
        public String Type() {
            return "Octopus";
        }
    }

    public abstract class AnimalFactory {
        public abstract IAnimal GetAnimal(String animalType);
        public static AnimalFactory CreateAnimalFactory(String factoryType) {
            if (factoryType == "Sea") {
                return new SeaAnimalFactory();
            } else {
                return new LandAnimalFactory();
            }
        }
    }

    public class LandAnimalFactory extends AnimalFactory {
        @Override
        public IAnimal GetAnimal(String animalType) {
            if (animalType == "Cat") {
                return new Cat();
            } else if (animalType == "Lion") {
                return new Lion();
            }
            return null;
        }
    }

    public class SeaAnimalFactory extends AnimalFactory {
        @Override
        public IAnimal GetAnimal(String animalType) {
            if (animalType == "Shark") {
                return new Shark();
            } else if (animalType == "Octopus") {
                return new Octopus();
            }
            return null;
        }
    }

    public class Demo {
        public static void main(String[] args) {
            IAnimal animal = null;
            AnimalFactory animalFactory = AnimalFactory.CreateAnimalFactory("Sea");
            animal = animalFactory.GetAnimal("Shark");
            System.out.println("Animal factory type : " + animal.Type() + ", Speak : " + animal.Speak());
            animal = animalFactory.GetAnimal("Octopus");
            System.out.println("Animal factory type : " + animal.Type() + ", Speak : " + animal.Speak());
            animalFactory = AnimalFactory.CreateAnimalFactory("Land");
            animal = animalFactory.GetAnimal("Cat");
            System.out.println("Animal factory type : " + animal.Type() + ", Speak : " + animal.Speak());
        }
    }`


---

## Design Pattern - III

### Observer Design Pattern 🧐

The **Observer design pattern** is a behavioral pattern that establishes a one-to-many dependency between objects. When one object, the

**Subject**, changes its state, all of its dependents, the **Observers**, are notified and updated automatically111111111. This pattern is a form of

**asynchronous** or **non-blocking communication**222222.

- **Analogy:** The document uses two analogies to explain this concept:
    1. **Phone call vs. Sending letters**: A phone call is a synchronous (blocking) communication where both parties must be actively engaged. Sending letters is an asynchronous (non-blocking) communication where a person can send a message and continue with other tasks, with the recipient receiving the message later3333333333333333.
    2.

        **Course recordings**: Instead of students repeatedly "pulling" or asking for a class update (polling), they can "subscribe" to a system design course4444. When new recordings are available, the system "pushes" or "passes" the data to all subscribed students, notifying them of the change555555555.

- **Real-world examples**:
    - **Amazon stock notifications**: When a product, like a phone, is out of stock, customers can register to be notified. When the product becomes available, all registered customers receive an email notification666666666.
- **Implementation Actors**: The pattern involves three main actors:
    1.

        **Subject**: The object that maintains a list of observers and notifies them of state changes7777777.

    2.

        **Observer**: The dependent object that gets notified by the subject8.

    3.

        **Client**: The class that creates and uses the subject and observer objects9.


---

### Code Example: Batch & Student 🧑‍🎓

The example illustrates a system where students register for a class batch. When a new study topic is added to the batch, all registered students are notified.

**Interfaces:**

-

    `ISession` (Subject): An interface that defines methods for `register()`, `unregister()`, `notifyStudents()`, and `getUpdate()`10101010101010101010101010101010101010101010101010.

-

    `IObserverStudent` (Observer): An interface with methods `update()`, `setClass()`, and `getName()`11111111111111111111111111111111.


**Concrete Classes:**

- `Batch` (Concrete Subject): This class implements `ISession` and maintains a list of `IObserverStudent` objects. When a new study topic is added via the

    `addStudyTopic()` method, it calls `notifyStudents()`, which in turn iterates through its list of observers and calls their `update()` method121212121212121212.

- `BatchSubscriber` (Concrete Observer): This class implements `IObserverStudent`. Its

    `update()` method fetches the new session plan from the subject using the `getUpdate()` method13131313.


Program (Client) Class:

This class demonstrates the usage. It creates a Batch subject and several BatchSubscriber observer objects. It then registers the students with the batch and sets the class for each student. Finally, when a study topic is added to the batch, the output shows that all registered students are notified automatically.

Java

#

`public interface ISession {
    public void register(IObserverStudent student);
    public void unregister(IObserverStudent student);
    public void notifyStudents();
    public String getUpdate(IObserverStudent student);
}

public interface IObserverStudent {
    public void update();
    public void setClass(ISession session);
    public String getName();
}

// Concrete Subject
public class Batch implements ISession {
    List<IObserverStudent> registeredStudents = new ArrayList<>();
    private String studyTopic;

    @Override
    public void register(IObserverStudent student) {
        System.out.println("Registering student : " + student.getName());
        this.registeredStudents.add(student);
    }

    // other methods like unregister, notifyStudents, getUpdate...

    public void addStudyTopic(String studyTopic) {
        System.out.println("Added the study topic: " + studyTopic);
        this.studyTopic = studyTopic;
        notifyStudents();
    }
}

// Concrete Observer
public class BatchSubscriber implements IObserverStudent {
    private String name;
    private ISession session;

    public BatchSubscriber(String name) {
        this.name = name;
    }

    @Override
    public void update() {
        String sessionPlan = session.getUpdate(this);
        System.out.println("Fetched the session plan of the class");
    }

    // other methods like setClass, getName...
}

// Client
public class Program {
    public static void main(String[] args) {
        Batch batch = new Batch();
        IObserverStudent student1 = new BatchSubscriber("StudentName1");
        IObserverStudent student2 = new BatchSubscriber("StudentName2");
        batch.register(student1);
        batch.register(student2);
        student1.setClass(batch);
        student2.setClass(batch);
        batch.addStudyTopic("Observer pattern");
    }
}`

---

### Strategy Design Pattern ♟️

The

**Strategy design pattern** allows you to define a family of algorithms, put each one into a separate class, and make their objects interchangeable15. It lets the algorithm vary independently from the clients that use it16. The document provides an example of different payment strategies for an e-commerce cart.

- **Key Components**:
    1.

        **Interface**: A common interface is created for all strategies (e.g., `IWalletStrategy`)17.

    2.

        **Concrete Classes**: Multiple classes implement the strategy interface, each representing a specific algorithm (e.g., `GooglePay`, `PhonePay`)18.

    3. **Context Class**: A class that uses a strategy object. It has a reference to the strategy interface and provides a method to execute the strategy (e.g.,

        `AmazonCart`)19. The client can pass a concrete strategy object to the context class.

- **Code Example: Amazon Cart Payment**
    -

        **`IWalletStrategy` Interface**: Defines a `pay()` method20.

    -

        **`GooglePay` and `PhonePay` Classes**: Implement `IWalletStrategy`, each with its own `pay()` method logic21.

    -

        **`AmazonCart` Context Class**: Holds a `Product` and a `IWalletStrategy` object22. Its

        `pay()` method delegates the payment logic to the held strategy object23.

    - **`Program` Client Class**: Creates a `Product` and an `AmazonCart`. It provides the `GooglePay` strategy to the `AmazonCart` at the time of creation. This shows how the client can choose a payment strategy at runtime24.

Java

#

`// Step 1: Create an interface
public interface IWalletStrategy {
    public void pay(int amount);
}

// Step 2: Create concrete classes
public class GooglePay implements IWalletStrategy {
    @Override
    public void pay(int amount) {
        System.out.println("Paying by google pay, amount : " + amount);
    }
}

public class PhonePay implements IWalletStrategy {
    @Override
    public void pay(int amount) {
        System.out.println("Paying by phone pay, amount : " + amount);
    }
}

// Step 3: Create Context Class
public class AmazonCart {
    private Product product;
    private IWalletStrategy walletStrategy;

    public AmazonCart(Product product, IWalletStrategy walletStrategy) {
        this.product = product;
        this.walletStrategy = walletStrategy;
    }

    public void pay() {
        this.walletStrategy.pay(product.getProductPrice());
    }
}

// Step 4: Use the Context with a chosen strategy
public class Program {
    public static void main(String[] args) {
        Product product = new Product("Phone", 10000);
        AmazonCart amazonCart = new AmazonCart(product, new GooglePay());
        amazonCart.pay(); // Output: "Paying by google pay, amount : 10000"
    }
}`

---

## Case Study: Web crawler & Amazon cart services

### Web Crawler System Design 🌐

A **web crawler** is a program that systematically browses the World Wide Web, typically for the purpose of web indexing. A web crawler starts with a set of URLs and then downloads the content of those web pages1. It then identifies all the hyperlinks on those pages and adds them to a queue of URLs to visit2. This process is repeated to crawl a large number of web pages.

- **Process:**
    1.

        **Starts with a URL**: The crawler begins with a starting URL, such as `Microsoft.com`3.

    2.

        **Downloads Content**: It downloads all the content from that webpage4.

    3.

        **Extracts Links**: The crawler extracts all the links on the page, which may include links to other sites like LinkedIn, Google, or Wikipedia5.

    4.

        **Stores and Computes**: All the downloaded data is saved to storage and can be used for various computations6.

- **Data Size Estimation**:
    -

        **Total Websites**: There are approximately 2 billion websites7.

    -

        **Average Pages per Website**: Assuming an average of 100 pages per website, the total number of pages would be 200 billion8888.

    -

        **Average Page Size**: The average size of a web page is about 100 KB9999.

    -

        **Total Content Size**: The total size of all web content is estimated by multiplying the total number of pages by the average page size10.

        -

            200 billion pages×100 KB 11

        -

            =200×109×100×103 Bytes 12

        - =2×1013 Bytes
        -

            =2×1010 GB 13

        -

            =2×107 TB 14

        -

            =2×104 PB 15

        -

            =20 PB 16

    -

        **Storage and Machines**: To store 20 PB of data, if each machine has 1 TB of storage, you would need 20,000 machines171717171717171717.

- **System Design Process**:
    1.

        **Requirement Gathering**: Understand the purpose and scale of the crawler18181818181818.

    2.

        **Scoping**: Define the boundaries and constraints of the system19191919191919.

    3.

        **Estimation of Data Size**: Perform calculations to estimate the required storage and compute resources20202020202020.

    4.

        **Planning**: Create a high-level plan for the system21.


---

### Amazon Cart Service 🛒

Designing an Amazon Cart service involves a set of interconnected services that work together to handle the process of a user buying an item22. When a user adds an item to their cart and proceeds to checkout, a sequence of microservices is involved23232323.

- **Process Flow**:
    1.

        **Adding to Cart**: A user adds an item to their cart, which is handled by the **Cart Service**24242424.

    2.

        **Initiating Checkout**: The user initiates the checkout process25252525.

    3.

        **Authentication**: The **Authentication Service** verifies the user's identity262626262626262626262626262626.

    4.

        **Inventory Check**: The **Inventory Service** checks if the item is available in stock272727272727272727272727272727.

    5.

        **Payment Processing**: The **Payment Service** handles the payment for the order282828282828282828.

    6.

        **Shipping**: The **Shipping Service** processes the order for shipment292929292929292929.

- **Design Steps**:
    1.

        **Requirement Gathering**: Collect all requirements for the system30303030.

    2.

        **Scoping**: Define the system boundaries and features to be included31313131.

    3.

        **Estimation**: Estimate the necessary resources like storage and compute power32323232.

    4.

        **Components**: Identify all the necessary components or microservices33.

    5.

        **Implementation**: Build the system based on the design34.

    6.

        **Testing**: Verify that the system works as expected35.

    7.

        **Deployment**: Launch the system for user access36.

- **System Design Levels**:
    -

        **High-Level Design**: Focuses on the overall architecture and how different components interact37.

    -

        **Low-Level Design**: Focuses on the detailed design of individual components and their internal workings38.


---

## Interview Preparedeness - LLD

### Low-Level Design (LLD) Interview Preparation 📝

Low-Level Design (LLD) is a crucial part of the software development life cycle and a common topic in technical interviews. It focuses on the detailed, component-level design of a system. A typical LLD interview round lasts between 45 and 60 minutes1111.

---

### Interview Approach & Process 🧑‍💻

The goal of an LLD interview is to design a specific system, such as a movie booking application like BookMyShow2. The process generally follows these steps:

1.

    **Problem Statement**: The interviewer will provide a problem statement, which often involves designing a system for a specific company or product3.

2. **Scope**: Define the scope of the design. This can be broken down into different phases (e.g., Phase 1, Phase 2, etc.) to manage the complexity4.
3. **Component Identification**: Identify the key components or classes required for the system. The document provides examples of classes for a movie booking app, such as:
    -

        **`Movie`**: with attributes like `id` (Long), `name` (String), `description` (String), `duration` (Double), `release date` (Date Time), `cast` (String), and `Language` (Enum)5.

    -

        **`Customer`**: with attributes like `id`, `name`, `Address`, and `Phone Numbers`666666666.

    -

        **`Admin`**: with attributes like `id`, `name`, `Address`, `Phone number`, and `Emp Id`7777777.

4. **Approaches to Class Design**: The notes suggest two approaches for designing user-related classes:
    -

        **Approach 1 (Inheritance)**: Create a base `User` class and have `Customer` and `Admin` classes extend it888888888. The

        `Customer` class might have additional attributes like `coupons`, `Referral Id`, and `support`9999. The

        `Admin` class might have an `Emp Id`10.

    -

        **Approach 2 (Enumeration)**: Create a single `User` class with a `UserType` enum (e.g., `Customer`, `Admin`) to differentiate between user types11. This is often a more flexible approach.

5. **Implementation**: Once the design is finalized, you may need to implement some of the key methods to demonstrate your coding skills.

---

### High-Level vs. Low-Level Design 📐

The document outlines the difference between High-Level Design (HLD) and Low-Level Design (LLD) and how the focus on each changes with experience:

-

    **2-3 years of experience**: The focus is approximately 70% on coding skills (DSA) and 30% on design skills12. The LLD is a greater focus than HLD13.

-

    **2-7 years of experience**: The skills are typically balanced at 50% coding and 50% design14.

-

    **7+ years of experience**: The focus shifts to 70% design skills and 30% coding skills15. The emphasis is more on HLD than LLD16.


---

### Design Patterns for LLD 🧩

A strong LLD requires a good understanding of design patterns. The user's previous notes and documents cover several key patterns that are highly relevant to LLD.

-

    **Factory & Abstract Factory Patterns**: These are creational patterns used to create objects in a flexible way17171717. The Factory pattern creates objects without exposing the creation logic, while the Abstract Factory is a "factory of factories" that creates families of related objects without specifying their concrete classes18181818. Using these patterns can help to isolate client code from implementation details and ensure consistency among objects191919191919191919.

-

    **Observer Pattern**: This behavioral pattern is for one-to-many dependencies20. A

    **Subject** maintains a list of **Observers** (dependents) and notifies them automatically when its state changes21212121. This is used for systems where a change in one object should trigger a change in others without the objects being tightly coupled22.

-

    **Strategy Pattern**: This is a behavioral pattern that allows you to define a family of algorithms, encapsulate each one, and make them interchangeable23. This lets the algorithm vary independently from the client that uses it. For example, in a payment system, you can have different payment strategies (GooglePay, PhonePay) that can be swapped out easily24242424.


A successful LLD interview demonstrates a solid grasp of these design principles and the ability to apply them to solve a given problem.

---

## High-Level Design Introduction

High-Level Design (HLD) provides a bird's-eye view of the system architecture, focusing on major components, their interactions, and data flow patterns.

### **🎯 HLD vs LLD Comparison**

| Aspect | High-Level Design (HLD) | Low-Level Design (LLD) |
|--------|-------------------------|------------------------|
| **Focus** | System architecture & components | Classes, methods, algorithms |
| **Audience** | Architects, stakeholders | Developers, implementers |
| **Abstraction** | High-level overview | Detailed implementation |
| **Decisions** | Technology stack, databases | Data structures, algorithms |
| **Artifacts** | Architecture diagrams, APIs | Class diagrams, code |

### **📈 Career Focus by Experience**

- **0-3 years:** 70% Coding + 30% Design (LLD focus)
- **3-7 years:** 50% Coding + 50% Design (Balanced)
- **7+ years:** 30% Coding + 70% Design (HLD focus)

### **🔄 HLD Process Framework**

```
1. Requirements Analysis → 2. Capacity Planning → 3. API Design
         ↓                        ↓                    ↓
4. Database Design → 5. High-Level Architecture → 6. Component Design
         ↓                        ↓                    ↓
7. Scalability Planning → 8. Security Design → 9. Monitoring Strategy
```

### **📋 HLD Deliverables**

1. **Architecture Diagrams**
   - System overview
   - Component interactions
   - Data flow diagrams

2. **API Specifications**
   - REST/GraphQL endpoints
   - Request/response formats
   - Authentication methods

3. **Database Schema**
   - Entity relationships
   - Indexing strategy
   - Partitioning approach

4. **Infrastructure Plan**
   - Server requirements
   - Network topology
   - Deployment strategy

---

## Microservices Architecture

Microservices architecture breaks down applications into small, independent services that communicate over well-defined APIs.

### **🏗️ Microservices vs Monolith**

| Aspect | Monolithic | Microservices |
|--------|------------|---------------|
| **Deployment** | Single unit | Independent services |
| **Scaling** | Scale entire app | Scale individual services |
| **Technology** | Single tech stack | Polyglot architecture |
| **Team Structure** | Single team | Multiple small teams |
| **Complexity** | Simple initially | Complex coordination |

### **✅ Microservices Benefits**

- **Independent Deployment:** Services can be deployed separately
- **Technology Diversity:** Different services can use different technologies
- **Fault Isolation:** Failure in one service doesn't crash entire system
- **Team Autonomy:** Teams can work independently on different services
- **Scalability:** Scale only the services that need it

### **❌ Microservices Challenges**

- **Network Complexity:** Inter-service communication overhead
- **Data Consistency:** Distributed transactions are complex
- **Operational Overhead:** More services to monitor and maintain
- **Testing Complexity:** Integration testing across services
- **Debugging Difficulty:** Tracing issues across multiple services

### **🔧 Microservices Patterns**

1. **API Gateway Pattern**
   - Single entry point for all client requests
   - Handles routing, authentication, rate limiting

2. **Service Discovery Pattern**
   - Services register themselves in a registry
   - Clients discover services dynamically

3. **Circuit Breaker Pattern**
   - Prevents cascading failures
   - Fails fast when downstream service is unavailable

4. **Saga Pattern**
   - Manages distributed transactions
   - Compensating actions for rollbacks

---

## Message Queues & Event-Driven Architecture

Message queues enable asynchronous communication between services, improving system resilience and scalability.

### **📨 Message Queue Benefits**

- **Decoupling:** Services don't need to know about each other
- **Reliability:** Messages persist until processed
- **Scalability:** Handle traffic spikes by queuing requests
- **Fault Tolerance:** System continues working if some services are down

### **🔄 Communication Patterns**

1. **Point-to-Point (Queue)**
   - One producer, one consumer
   - Message consumed once
   - Example: Order processing

2. **Publish-Subscribe (Topic)**
   - One producer, multiple consumers
   - Message delivered to all subscribers
   - Example: Notifications

3. **Request-Reply**
   - Synchronous-like communication over async channels
   - Correlation IDs to match requests with responses

### **⚡ Popular Message Queue Systems**

- **Apache Kafka:** High-throughput, distributed streaming
- **RabbitMQ:** Feature-rich, supports multiple protocols
- **Amazon SQS:** Managed queue service
- **Redis Pub/Sub:** In-memory messaging
- **Apache Pulsar:** Multi-tenant, geo-replication

### **🎯 Event-Driven Architecture**

**Event Sourcing:**
- Store events instead of current state
- Rebuild state by replaying events
- Complete audit trail

**CQRS (Command Query Responsibility Segregation):**
- Separate read and write models
- Optimize each for its specific use case
- Often used with event sourcing


---

## Web Applications & Architecture

Web applications are interactive software programs that run on web servers and are accessed through web browsers.

### **🌐 Websites vs Web Applications**

| Aspect | Websites | Web Applications |
|--------|----------|------------------|
| **Content** | Static content | Dynamic, interactive content |
| **User Interaction** | Read-only (informational) | Read-write (transactional) |
| **Complexity** | Simple HTML/CSS | Complex business logic |
| **Examples** | Blogs, news sites, portfolios | Gmail, Facebook, Netflix, Uber |
| **Updates** | Content updates | Feature updates & data changes |

### **🏗️ Three-Tier Architecture**

#### **1. Presentation Layer (Frontend)**
- **Technologies:** HTML, CSS, JavaScript, React, Angular, Vue.js
- **Responsibilities:** User interface, user experience, client-side validation
- **Deployment:** CDN, web servers, mobile apps

#### **2. Application Layer (Backend)**
- **Technologies:** Java, Python, Node.js, C#, Go, Ruby
- **Responsibilities:** Business logic, API endpoints, authentication
- **Components:** Web servers, application servers, microservices

#### **3. Data Layer (Database)**
- **Technologies:** MySQL, PostgreSQL, MongoDB, Redis, Elasticsearch
- **Responsibilities:** Data storage, retrieval, consistency, backup
- **Types:** RDBMS, NoSQL, In-memory, Search engines

### **🏢 Monolithic Architecture**

**Characteristics:**
- Single deployable unit
- Shared database
- Single technology stack
- Centralized business logic

**Advantages:**
- **Simple Development:** Single codebase, easy to understand
- **Easy Testing:** Straightforward integration testing
- **Simple Deployment:** Single artifact to deploy
- **Performance:** No network latency between components

**Disadvantages:**
- **Scalability Issues:** Must scale entire application
- **Technology Lock-in:** Difficult to adopt new technologies
- **Team Dependencies:** Teams must coordinate changes
- **Deployment Risk:** Single point of failure for deployments

**When to Use Monoliths:**
- Small to medium applications
- Simple business domains
- Small development teams
- Rapid prototyping
- Limited operational expertise

### **🔧 Modern Architecture Patterns**

#### **1. Layered Architecture**
```
┌─────────────────┐
│ Presentation    │
├─────────────────┤
│ Business Logic  │
├─────────────────┤
│ Data Access     │
├─────────────────┤
│ Database        │
└─────────────────┘
```

#### **2. Hexagonal Architecture (Ports & Adapters)**
- Core business logic at center
- External dependencies as adapters
- Ports define interfaces

#### **3. Event-Driven Architecture**
- Components communicate via events
- Loose coupling between services
- Asynchronous processing

---

## Content Delivery Networks (CDN)

CDNs are geographically distributed networks of servers that deliver web content to users based on their location.

### **🌍 How CDNs Work**

1. **Content Caching:** Static content cached at edge servers
2. **Geographic Distribution:** Servers placed globally
3. **Intelligent Routing:** Users directed to nearest server
4. **Cache Management:** Content updated and invalidated as needed

### **📈 CDN Benefits**

- **Reduced Latency:** Content served from nearby locations
- **Improved Performance:** Faster page load times
- **Reduced Bandwidth:** Less load on origin servers
- **High Availability:** Redundancy across multiple servers
- **DDoS Protection:** Distributed infrastructure absorbs attacks
- **Global Reach:** Serve users worldwide efficiently

### **🔧 CDN Types**

1. **Push CDNs**
   - Content uploaded to CDN manually
   - Good for sites with infrequent updates
   - More control over content

2. **Pull CDNs**
   - Content pulled from origin on first request
   - Good for sites with frequent updates
   - Automatic content management

### **⚡ CDN Use Cases**

- **Static Assets:** Images, CSS, JavaScript files
- **Video Streaming:** Adaptive bitrate streaming
- **Software Distribution:** Downloads, updates
- **API Acceleration:** Caching API responses
- **Security:** Web Application Firewall (WAF)

### **🏢 Popular CDN Providers**

- **Cloudflare:** Global network, security features
- **Amazon CloudFront:** AWS integration, edge computing
- **Akamai:** Enterprise focus, advanced features
- **Google Cloud CDN:** GCP integration, global infrastructure
- **Azure CDN:** Microsoft ecosystem integration


---

## Distributed System - I

### Distributed Systems Notes 🌐

A distributed system involves a

**service requester** (or data requester) and a **service provider** (or data provider)111111111. Communication between them can be either unidirectional or bidirectional2222.

-

    **Unidirectional Data Transfer**: This is a one-way transfer where a notification is sent from one service to another3333.

-

    **Bidirectional Data Transfer**: This is a two-way transfer where a request is sent, and a response is received4444. An example is checking a score, where you send a request and the service replies with the score5.


### RPC (Remote Procedure Call)

RPC is a protocol that allows a program to request a service from a program located on another computer on a network without the need to understand the network's details6. The notes highlight an example where both the requester (Service A) and the provider (Service B) are written in Java and can use RPC to communicate directly7777.

### SOAP (Simple Object Access Protocol)

SOAP is a protocol for exchanging structured information in the implementation of web services8. It uses an XML document to send a request, and the recipient processes the XML and sends back a response, also in XML9999999999999999.

**Key characteristics of SOAP from the notes:**

- It is considered

    **slow, heavy, and complex** due to the use of XML tags10101010.

- It is

    **language-neutral**, which means a Java application can communicate with a C# application using SOAP11111111.


---

### Code Examples for Distributed Systems

While the provided notes don't include code, here are simplified examples of how you might implement these concepts in a real-world scenario.

### RPC Example (Java)

This is a conceptual example showing how a client calls a remote method as if it were a local method.

**Server-side (Remote Interface):**

Java

#

`// Remote interface
public interface ICalculator {
    public int add(int a, int b) throws RemoteException;
}

// Server implementation
public class CalculatorImpl extends UnicastRemoteObject implements ICalculator {
    public CalculatorImpl() throws RemoteException {
        super();
    }
    public int add(int a, int b) {
        return a + b;
    }
}`

**Client-side:**

Java

#

`// Client code to call the remote method
public class CalculatorClient {
    public static void main(String[] args) {
        try {
            ICalculator calculator = (ICalculator) Naming.lookup("rmi://localhost/CalculatorService");
            int sum = calculator.add(10, 20);
            System.out.println("Sum is: " + sum);
        } catch (Exception e) {
            System.err.println("Client exception: " + e.toString());
            e.printStackTrace();
        }
    }
}`

### SOAP Example

This is a conceptual example of a SOAP request and response using XML.

**SOAP Request (XML):**

XML

#

`<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Body>
  <m:add xmlns:m="http://www.example.org/stock">
    <m:a>10</m:a>
    <m:b>20</m:b>
  </m:add>
</soap:Body>

</soap:Envelope>`

**SOAP Response (XML):**

XML

#

`<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Body>
  <m:addResponse xmlns:m="http://www.example.org/stock">
    <m:Result>30</m:Result>
  </m:addResponse>
</soap:Body>

</soap:Envelope>`

---

## Distributed System - II

These notes provide an overview of **REST (Representational State Transfer)**, a software architectural style for creating distributed systems.

---

### Key Concepts of REST

-

    **Definition**: REST is an architectural style for distributed systems, often used for web services1. The full name is

    **Representational State Transfer**2222.

-

    **Data Representation**: Data is often transferred between applications as **JSON (JavaScript Object Notation)**, which can be thought of as a Python class or object333333333. The JSON object is converted into a byte stream of 0s and 1s for transmission4.

-

    **Statelessness**: REST services are **stateless**5. This means that the server doesn't store any information about the client's state between requests. Every request from a client to the server must contain all the information needed to understand the request6.

-

    **Wide Adoption**: REST is widely adopted for communication between front-end and back-end systems using **HTTP** (Hypertext Transfer Protocol)7777.

-

    **Resources**: In REST, everything is treated as a **resource**, which is identified by a **URI (Uniform Resource Identifier)**8888888888888888888888888. Resources are typically named using nouns, such as "Movie" or "Theater"9.


---

### Advantages of REST

-

    **Lightweight**: REST is considered a lightweight protocol10.

-

    **Faster Performance**: It offers faster performance11.

-

    **Flexibility**: REST provides flexibility in its use12.

-

    **Ease of Use**: It's easy to use13131313.

-

    **Statelessness**: Its stateless nature is a key advantage14.

-

    **Wide Adoption**: It has wide adoption across the industry15.


---

### HTTP Methods and CRUD Operations

REST uses standard HTTP methods to perform actions on resources. These methods map to the standard **CRUD** (Create, Read, Update, Delete) operations:

-

    **Create (C)**: Uses the **`POST`** method1616. For example, a

    `POST` request to `/movies` creates a new movie171717171717171717.

-

    **Read (R)**: Uses the **`GET`** method18181818. A

    `GET` request to `/movies/123` would retrieve the movie with ID `123`1919191919.

-

    **Update (U)**: Uses the **`PUT`** or **`PATCH`** methods20202020.

-

    **Delete (D)**: Uses the **`DELETE`** method21212121.


---

### URI Naming Standards

To create effective and predictable RESTful APIs, there are two important standards for naming URIs:

1.

    **Use Nouns, Not Verbs**: The URI should describe the resource itself, not the action being performed on it22222222. For example, use

    `/movies` instead of `/createMovies`23. The action is specified by the HTTP method (

    `GET`, `POST`, `PUT`, `DELETE`), not in the URI24.

2.

    **Use Plurals**: Always use the plural form for resource names in the URI, like `/movies` instead of `/movie`2525252525.


For example, a URI for a movie booking application might look like this:

`192.168.1.100:8080/mba/v1/movies/123`26262626.

-

    **`192.168.1.100`**: The IP address of the server272727272727272727.

-

    **`8080`**: The port number of the application28282828282828282828282828282828.

-

    **`/mba/v1`**: The application identifier and version number29292929292929292929292929292929.

-

    **`/movies`**: The collection of movie resources303030303030303030.

-

    **`/123`**: The specific identifier for a movie resource313131313131313131.


---

## Time

### Notes on Distributed System Clocks

The notes you provided cover two types of clocks used in distributed systems: **physical clocks** and **logical clocks**. The primary challenge in a distributed system is that each machine has its own clock, and these clocks can drift, making it difficult to establish a global, consistent order of events. Logical clocks were developed to address this problem by focusing on the causal relationship between events rather than on physical time.

---

### Physical Clocks

- **Definition**: These are the real-time clocks found in computer systems, which track time using hardware-based mechanisms like a quartz crystal oscillator.
- **Problem**: Physical clocks in different machines can drift over time, leading to inconsistencies. Perfectly synchronizing them is very difficult.

---

### Logical Clocks

- **Definition**: Logical clocks are a software-based counter used to order events in a distributed system based on their causal relationship, or "happens before" relationship, which is denoted as A → B.
- **Key Principle**: If event A happens before event B, then the logical timestamp of A will be less than the logical timestamp of B.

---

### Lamport's Logical Clock

This is a specific type of logical clock that follows a set of rules to ensure event ordering.

### Rules:

1. **Local Events**: Each process (a separate, running program) maintains its own counter, which is the logical clock. The counter is incremented by one before any local event occurs.
2. **Sending Messages**: When a process sends a message, it includes its current logical clock value (timestamp) with the message.
3. **Receiving Messages**: When a process receives a message, it updates its own logical clock to be the maximum of its current clock value and the timestamp received in the message. It then increments its clock by one.

### Example Calculation:

Let's consider an example with three processes: P1, P2, and P3, where each has a local counter (logical clock). Initially, all clocks are at 0.

- **P1 Local Event**: P1's clock increments from 0 to **1**. P1 then sends a message (M1) to P2 with the timestamp `1`.
- **P2 Local Event**: P2's clock increments from 0 to **1**. P2 then sends a message (M2) to P3 with the timestamp `1`.
- **P3 Local Event**: P3's clock increments from 0 to **1**.
- **P2 Receives M1**: P2 receives the message from P1 with a timestamp of `1`. P2's current clock is `1`. It applies the `max(local, received_timestamp) + 1` rule: `max(1, 1) + 1 = 2`. P2's clock is now **2**.
- **P1 Receives M2**: P1 receives the message from P2 with a timestamp of `1`. P1's current clock is `1`. It applies the `max(local, received_timestamp) + 1` rule: `max(1, 1) + 1 = 2`. P1's clock is now **2**.
- **P2 Local Event**: P2's clock increments from `2` to **3**. P2 then sends a message (M3) to P3 with the timestamp `3`.
- **P3 Receives M3**: P3 receives the message from P2 with a timestamp of `3`. P3's current clock is `1`. It applies the `max(local, received_timestamp) + 1` rule: `max(1, 3) + 1 = 4`. P3's clock is now **4**.

This example shows how Lamport's algorithm provides a partial ordering of events. The logical timestamps ensure that if an event happened before another, its timestamp will be smaller, regardless of physical time. However, concurrent events (events that are not causally related) might end up with the same timestamp, as seen in the notes.

---

### Vector Clocks

- **Definition**: Vector clocks are a more advanced type of logical clock that extends Lamport's concept. Instead of a single integer, each process maintains a vector (an array) with one element for each process in the system. This allows them to not only order events but also to detect concurrent events.

---

**Note:** The notes you provided only included examples and calculations for Lamport's Logical Clock. If you need a detailed example of a vector clock, additional information would be required.

---

## Databases

### **Database Fundamentals**

- A database is a system used for storing and retrieving data1111. The diagram suggests that 90% of data is stored for the "last couple years only"2.
- The process involves capturing information and using it later3.
- A

    **distributed system** handles big data4444.


### **Historical Context: File-Based Storage Systems (FBSS)**

- The earliest form of storage mentioned is the

    **File-Based Storage System (FBSS)**, which existed around the 1950s5. This system stored individual documents, like .txt or .doc files, in folders6.


### **Limitations of FBSS:**

- It required programmers to manage the data7.
- Data could be duplicated, leading to

    **data redundancy**8888.

- Deleting data was difficult9.
- It often resulted in

    **inconsistent data**10.


### **Database Management Systems (DBMS)**

- A **Database Management System (DBMS)** is a system for managing databases. It is composed of two parts: the physical database itself and a management system, which acts as a software layer11111111.
- Examples of a DBMS include Oracle and MySQL12.
- A key feature of a DBMS is the use of

    **SQL (Structured Query Language)**, which allows users to interact with the database using a language similar to English13.


---

### **Types of Databases**

### **Relational Database Management Systems (RDBMS)**

- RDBMS is a type of DBMS where data is organized into

    **tables**14141414.

- Tables are linked together using

    **primary keys (Pk)** and **foreign keys (FK)**15151515.

- RDBMS uses a

    **fixed schema**, meaning the number of rows and columns is predetermined16161616. Examples include bank data and e-commerce product catalogs171717171717171717.

- RDBMS provides **ACID** properties, ensuring transaction integrity. This means transactions are either fully completed or not at all (

    **"all or nothing"**)18181818.


### **NoSQL Databases**

-

    **NoSQL** databases, such as **MongoDB**, use a **dynamic schema**, allowing for flexible document-based data structures191919191919191919. This is different from the fixed schema of RDBMS20202020.


---

### **Storage and Computation**

- The document also briefly mentions the concepts of

    **storage** and **computation**21212121.

- A computational engine processes data22.

---

## Scalability

Scalability is the ability of an application to handle an increased number of users or transactions without a drop in performance1111. This is considered a good problem to have as it indicates a positive sign of growth, meaning more users are engaging with the application2222.

## Types of Scaling

There are two primary methods to achieve scalability:

**Vertical Scaling** and **Horizontal Scaling**3.

### Vertical Scaling (Scaling Up)

Vertical scaling involves increasing the resources of a single server4. This can be done by adding more storage, RAM, or CPU to the existing machine555555555. The main limitations of vertical scaling are:

-

    **Hardware limitations**: There's a physical limit to how much you can upgrade a single machine (e.g., a phone might only have two memory card slots)6.

-

    **Cost consideration**: At a certain point, the cost of increasing performance outweighs the benefits, leading to diminishing returns on investment7777777777777777777777777. Companies must find a trade-off between cost and performance to remain profitable8888888888888888.

-

    **Single point of failure**: If the single, centralized system fails due to issues like a power outage, the entire application goes down9999999999999999999999.


---

### Horizontal Scaling (Scaling Out)

Horizontal scaling involves adding more machines to a system instead of increasing the resources of a single one10101010101010101010101010101010. This is also known as a

**distributed system** and involves using a cluster of multiple machines to handle the load11111111. This approach offers

**flexibility** and avoids the single point of failure inherent in vertical scaling because if one machine fails, others can continue to operate12121212.

---

## Optimisation of Databases

Optimization involves improving an application's performance, often when it becomes slow despite having sufficient resources like free storage111111111. A common cause for poor performance is improper database indexing2.

---

### Database Indexing

A database index is a data structure used to improve the speed of data retrieval operations3333. It works by creating a copy of a specific column, sorting the values in that copy, and storing it in a separate location on the hard disk4. This sorted copy allows for faster searching5555. Instead of scanning the entire table (a process with a time complexity of

O(n)) 6666, a query can use the index, which is often structured as a balanced binary search tree, to find data with a time complexity of

O(logn)7.

-

    **Example**: When you search for a specific name like "abc" in a user table, a query without an index would have to check every single row8888. With an index on the "name" column, the database can quickly locate "abc" using an efficient search algorithm on the sorted index9.

-

    **Data Structure**: Balanced Binary Search Trees (BST), like the **Red-Black Tree**, are commonly used for database indexing because they maintain a balanced structure, ensuring that search, insertion, and deletion operations all have a time complexity of O(logn)10. This is particularly useful for applications with constantly changing data, such as tracking dynamic locations in Google Maps or Uber11111111.

-

    **Best Practices**: Indexing is most effective for applications that are **read-heavy**12. It speeds up read operations but can slow down write operations because the index also needs to be updated13. Therefore, indexes should only be applied to columns that are frequently queried14.

-

    **Text-based Queries**: Standard indexing is not suitable for text-heavy queries (e.g., using `LIKE` with wildcards)151515151515151515. For these, specialized databases like

    **Elasticsearch** are optimized to handle text-based searches efficiently16.


---

### Horizontal Partitioning (Sharding)

Partitioning is another optimization technique that involves dividing a large database into smaller, more manageable parts17.

**Horizontal partitioning**, also known as **sharding**, divides a database table's rows into separate, smaller tables based on a defined range18.

- **Example**: A database with millions of user records and zip codes can be partitioned. Records with zip codes from 1 to 500 can be stored on one machine, those from 501 to 5000 on a second, and so on19. This distributes the data and load across multiple machines, which is a characteristic of a distributed system20.
-

    **Vertical partitioning** also exists but works by dividing a table's columns into separate tables21.


---

## Scalability & Performance

Scalability is the ability of a system to handle increased load by adding resources. Performance optimization ensures efficient resource utilization and fast response times.

### **📈 Types of Scaling**

#### **Vertical Scaling (Scale Up)**
- **Definition:** Increase resources of existing servers
- **Methods:** Add CPU, RAM, storage to single machine
- **Advantages:** Simple, no code changes, strong consistency
- **Disadvantages:** Hardware limits, single point of failure, expensive
- **Use Cases:** Databases, legacy applications

#### **Horizontal Scaling (Scale Out)**
- **Definition:** Add more servers to handle load
- **Methods:** Distribute load across multiple machines
- **Advantages:** No hardware limits, fault tolerance, cost-effective
- **Disadvantages:** Complex, eventual consistency, network overhead
- **Use Cases:** Web servers, microservices, distributed systems

### **⚖️ Load Balancing**

Load balancers distribute incoming requests across multiple servers to ensure optimal resource utilization and prevent overload.

#### **Load Balancing Algorithms**

1. **Round Robin:** Requests distributed sequentially
2. **Weighted Round Robin:** Servers assigned weights based on capacity
3. **Least Connections:** Route to server with fewest active connections
4. **Least Response Time:** Route to server with fastest response
5. **IP Hash:** Route based on client IP hash
6. **Geographic:** Route based on client location

#### **Load Balancer Types**

| Type | Layer | Features | Use Cases |
|------|-------|----------|-----------|
| **L4 (Transport)** | TCP/UDP | Fast, simple routing | High throughput |
| **L7 (Application)** | HTTP/HTTPS | Content-based routing | Complex routing rules |
| **Hardware** | Physical | High performance | Enterprise, high load |
| **Software** | Virtual | Flexible, cost-effective | Cloud, startups |

#### **Load Balancer Placement**

```
Internet → L7 Load Balancer → L4 Load Balancer → Application Servers
                ↓                    ↓
           SSL Termination    Connection Pooling
           Content Routing    Health Checks
```

### **🚀 Performance Optimization Techniques**

#### **1. Caching Strategies**

**Cache Levels:**
- **Browser Cache:** Client-side caching
- **CDN Cache:** Edge server caching
- **Reverse Proxy Cache:** Server-side caching
- **Application Cache:** In-memory caching
- **Database Cache:** Query result caching

**Cache Patterns:**

1. **Cache-Aside (Lazy Loading)**
   ```
   if (data not in cache):
       data = fetch_from_database()
       cache.set(key, data)
   return cache.get(key)
   ```

2. **Write-Through**
   ```
   cache.set(key, data)
   database.save(data)
   ```

3. **Write-Behind (Write-Back)**
   ```
   cache.set(key, data)
   // Asynchronously write to database later
   ```

4. **Refresh-Ahead**
   ```
   // Proactively refresh cache before expiration
   if (cache.ttl(key) < threshold):
       background_refresh(key)
   ```

#### **2. Database Optimization**

**Indexing Strategies:**
- **B-Tree Indexes:** General purpose, range queries
- **Hash Indexes:** Exact match queries
- **Bitmap Indexes:** Low cardinality data
- **Composite Indexes:** Multiple column queries

**Query Optimization:**
- Use EXPLAIN plans
- Avoid N+1 queries
- Implement connection pooling
- Use prepared statements

**Partitioning:**
- **Horizontal (Sharding):** Split rows across databases
- **Vertical:** Split columns across databases
- **Functional:** Split by feature/service

#### **3. Application-Level Optimization**

**Code Optimization:**
- Algorithm efficiency (O(n) complexity)
- Memory management
- Asynchronous processing
- Connection pooling

**Resource Optimization:**
- Image compression
- Minification (CSS, JS)
- Gzip compression
- Lazy loading

---

## Caching Strategies

Caching is a technique to store frequently accessed data in fast storage to reduce latency and improve performance.

### **🎯 Cache Benefits**

- **Reduced Latency:** Faster data access
- **Lower Database Load:** Fewer database queries
- **Improved Scalability:** Handle more concurrent users
- **Cost Reduction:** Less expensive than scaling databases
- **Better User Experience:** Faster page loads

### **📊 Cache Types by Location**

1. **Client-Side Cache**
   - Browser cache, mobile app cache
   - Controlled by cache headers
   - Reduces network requests

2. **CDN Cache**
   - Geographic distribution
   - Static content caching
   - Reduces origin server load

3. **Reverse Proxy Cache**
   - Nginx, Varnish, CloudFlare
   - Caches dynamic content
   - SSL termination

4. **Application Cache**
   - In-memory stores (Redis, Memcached)
   - Session storage
   - Temporary data storage

5. **Database Cache**
   - Query result caching
   - Buffer pools
   - Materialized views

### **⏰ Cache Invalidation Strategies**

1. **TTL (Time To Live)**
   - Automatic expiration after set time
   - Simple but may serve stale data

2. **Write-Through Invalidation**
   - Update cache when data changes
   - Ensures consistency but adds latency

3. **Event-Based Invalidation**
   - Invalidate based on specific events
   - More precise but complex to implement

4. **Manual Invalidation**
   - Explicit cache clearing
   - Full control but requires careful management

### **🔧 Popular Caching Solutions**

- **Redis:** In-memory data structure store
- **Memcached:** High-performance distributed memory caching
- **Hazelcast:** Distributed in-memory computing platform
- **Apache Ignite:** Distributed database and caching platform
- **Ehcache:** Java-based caching solution


---

## NoSQL

### NoSQL Databases

**NoSQL** (short for "not only SQL") databases are non-relational databases that store data in a non-tabular format, unlike traditional relational databases (RDBMS). They use a flexible schema model that is well-suited for unstructured and semi-structured data. The notes you provided indicate that NoSQL databases complement SQL databases and address issues with the latter, such as problems with fixed schemas, transaction support, and scalability as data volume increases.

---

### Types of NoSQL Databases

Your notes identify four main types of NoSQL databases.

1. **Key-Value Based Databases**: This is the simplest type of NoSQL database, where data is stored in pairs of unique keys and values. The key is used as a unique identifier to retrieve the associated value. The notes you provided describe how data is stored in pairs, with an example of a key-value pair for "Salary," where "A" is the key and "90,000" is the value. The notes also highlight advantages like simplicity, ease of implementation, scalability, and efficiency. Examples of key-value stores include Redis, Couchbase, and Memcached. They are commonly used for use cases such as user preferences, shopping carts, and caching.
2. **Document-Based Databases**: These databases store data in a flexible, JSON-like format. The notes you provided give an example of a JSON document with fields like "id," "name," "age," and "gender". These databases are ideal for storing semi-structured data and are often used in content management systems, e-commerce applications, and for managing sensor data. They are designed for flexibility and can handle a wide variety of data types, including complex nested structures.
3. **Columnar Databases**: These databases organize and store data in columns rather than rows. This structure is optimized for analytical queries and large datasets. By storing data column by column, the database can quickly access and retrieve only the necessary data for a query, which reduces I/O operations and enhances performance. They are particularly well-suited for data warehousing, business intelligence (BI), and real-time analytics.
4. **Graph Databases**: These databases use a model based on nodes and edges to represent and store data. Nodes represent entities (like people or accounts), and edges represent the relationships between them. This model is highly effective for visualizing and querying highly interconnected data. Graph databases excel at finding relationships and patterns, making them ideal for use cases like social media analysis, recommendation engines, and fraud detection.

---

### When to Choose NoSQL Over RDBMS

Based on the provided information, NoSQL databases are a good choice when you need:

- **Flexibility and a Dynamic Schema**: If your data is semi-structured or unstructured and the schema may change frequently, NoSQL databases are ideal because they do not require a fixed, predefined schema.
- **Horizontal Scalability**: NoSQL databases are designed to handle large, complex datasets and can scale out horizontally by adding more servers. This is beneficial for applications with unpredictable and high-volume workloads, such as IoT and device sensor applications.
- **High Availability**: Many NoSQL databases are distributed by design, which means there is no single point of failure. They are well-suited for applications with geographically distributed users that require low-latency data access.
- **Performance**: They are optimized for fast querying and do not typically require complex joins, which makes them a strong choice for applications requiring real-time analytics.

---

## Security & Authentication

Security is a critical aspect of system design that must be considered at every layer of the architecture.

### **🔐 Authentication vs Authorization**

- **Authentication:** Verifying who the user is (login)
- **Authorization:** Verifying what the user can do (permissions)

### **🎫 Authentication Methods**

#### **1. Session-Based Authentication**
```
1. User logs in with credentials
2. Server creates session, stores in database
3. Server sends session ID to client (cookie)
4. Client sends session ID with each request
5. Server validates session ID
```

**Pros:** Simple, server controls sessions
**Cons:** Not scalable, server state required

#### **2. Token-Based Authentication (JWT)**
```
1. User logs in with credentials
2. Server generates JWT token
3. Client stores token (localStorage/cookie)
4. Client sends token in Authorization header
5. Server validates token signature
```

**Pros:** Stateless, scalable, cross-domain
**Cons:** Token size, revocation complexity

#### **3. OAuth 2.0 / OpenID Connect**
- **OAuth 2.0:** Authorization framework
- **OpenID Connect:** Authentication layer on top of OAuth 2.0
- **Use Cases:** Third-party login (Google, Facebook, GitHub)

### **🛡️ Security Best Practices**

#### **Input Validation & Sanitization**
- Validate all user inputs
- Use parameterized queries (prevent SQL injection)
- Sanitize HTML content (prevent XSS)
- Implement rate limiting

#### **Data Protection**
- **Encryption at Rest:** Database encryption, file encryption
- **Encryption in Transit:** HTTPS/TLS, VPN
- **Hashing:** Passwords (bcrypt, scrypt, Argon2)
- **Salting:** Prevent rainbow table attacks

#### **Network Security**
- **Firewalls:** Control network traffic
- **VPC/Subnets:** Network isolation
- **API Gateway:** Centralized security policies
- **DDoS Protection:** Rate limiting, traffic filtering

### **🔒 Common Security Vulnerabilities**

1. **SQL Injection:** Use parameterized queries
2. **Cross-Site Scripting (XSS):** Sanitize inputs, CSP headers
3. **Cross-Site Request Forgery (CSRF):** CSRF tokens
4. **Insecure Direct Object References:** Access control checks
5. **Security Misconfiguration:** Regular security audits
6. **Sensitive Data Exposure:** Encryption, secure storage

---

## Monitoring & Observability

Monitoring and observability are essential for maintaining system health and debugging issues in production.

### **📊 The Three Pillars of Observability**

#### **1. Metrics**
- **Definition:** Numerical measurements over time
- **Examples:** CPU usage, memory consumption, request rate, error rate
- **Tools:** Prometheus, Grafana, CloudWatch, DataDog

#### **2. Logs**
- **Definition:** Discrete events with timestamps
- **Types:** Application logs, access logs, error logs, audit logs
- **Tools:** ELK Stack (Elasticsearch, Logstash, Kibana), Splunk, Fluentd

#### **3. Traces**
- **Definition:** Request journey through distributed system
- **Purpose:** Track request flow, identify bottlenecks
- **Tools:** Jaeger, Zipkin, AWS X-Ray, OpenTelemetry

### **📈 Key Metrics to Monitor**

#### **Application Metrics**
- **Request Rate:** Requests per second
- **Response Time:** Latency percentiles (p50, p95, p99)
- **Error Rate:** Percentage of failed requests
- **Throughput:** Data processed per unit time

#### **Infrastructure Metrics**
- **CPU Utilization:** Processor usage
- **Memory Usage:** RAM consumption
- **Disk I/O:** Read/write operations
- **Network I/O:** Bandwidth utilization

#### **Business Metrics**
- **User Engagement:** Active users, session duration
- **Conversion Rate:** Goal completion percentage
- **Revenue Metrics:** Sales, subscriptions
- **Feature Usage:** Feature adoption rates

### **🚨 Alerting Strategies**

#### **Alert Types**
1. **Threshold Alerts:** Metric exceeds/falls below threshold
2. **Anomaly Detection:** Unusual patterns in metrics
3. **Composite Alerts:** Multiple conditions combined
4. **Predictive Alerts:** Forecasting potential issues

#### **Alert Best Practices**
- **Actionable:** Every alert should require action
- **Contextual:** Provide relevant information
- **Escalation:** Define escalation paths
- **Runbooks:** Document response procedures

### **🔍 Distributed Tracing**

**Benefits:**
- End-to-end request visibility
- Performance bottleneck identification
- Error root cause analysis
- Service dependency mapping

**Implementation:**
```
1. Instrument code with tracing libraries
2. Generate trace IDs for requests
3. Propagate trace context across services
4. Collect and analyze trace data
```

---

## System Design Interview Framework

A structured approach to tackle system design interviews effectively.

### **🎯 Interview Process (45-60 minutes)**

#### **Phase 1: Requirements Clarification (5-10 minutes)**
1. **Functional Requirements**
   - What features should the system support?
   - What are the core use cases?
   - Who are the users?

2. **Non-Functional Requirements**
   - How many users?
   - What's the expected read/write ratio?
   - What's the expected response time?
   - What's the availability requirement?

3. **Constraints & Assumptions**
   - Budget constraints
   - Technology preferences
   - Compliance requirements

#### **Phase 2: Capacity Estimation (5-10 minutes)**

**Traffic Estimation:**
```
Daily Active Users (DAU): 100M
Average requests per user per day: 10
Total requests per day: 1B
Requests per second: 1B / (24 * 3600) ≈ 11.6K RPS
Peak traffic (3x average): 35K RPS
```

**Storage Estimation:**
```
Average data per user: 1KB
Total users: 1B
Total storage: 1B * 1KB = 1TB
With replication (3x): 3TB
Growth over 5 years (2x per year): 3TB * 32 = 96TB
```

**Bandwidth Estimation:**
```
Average request size: 1KB
Average response size: 10KB
Incoming: 35K RPS * 1KB = 35 MB/s
Outgoing: 35K RPS * 10KB = 350 MB/s
```

#### **Phase 3: System Interface Design (5-10 minutes)**

**API Design:**
```
POST /api/v1/users
GET /api/v1/users/{userId}
PUT /api/v1/users/{userId}
DELETE /api/v1/users/{userId}

POST /api/v1/posts
GET /api/v1/posts/{postId}
GET /api/v1/users/{userId}/posts
```

**Data Models:**
```
User {
  userId: string
  username: string
  email: string
  createdAt: timestamp
}

Post {
  postId: string
  userId: string
  content: string
  createdAt: timestamp
  updatedAt: timestamp
}
```

#### **Phase 4: High-Level Design (15-20 minutes)**

**Basic Architecture:**
```
Client → Load Balancer → Web Servers → Application Servers → Database
                    ↓
                   CDN
```

**Component Breakdown:**
1. **Load Balancer:** Distribute traffic
2. **Web Servers:** Handle HTTP requests
3. **Application Servers:** Business logic
4. **Database:** Data persistence
5. **Cache:** Improve performance
6. **CDN:** Static content delivery

#### **Phase 5: Detailed Design (10-15 minutes)**

**Database Design:**
- Choose between SQL/NoSQL
- Design schema/document structure
- Plan for sharding/partitioning
- Consider indexing strategy

**Caching Strategy:**
- What to cache (hot data)
- Cache levels (browser, CDN, application)
- Cache invalidation strategy
- Cache consistency

**Scalability Considerations:**
- Horizontal vs vertical scaling
- Database scaling (read replicas, sharding)
- Microservices decomposition
- Asynchronous processing

#### **Phase 6: Scale & Optimize (5-10 minutes)**

**Bottleneck Identification:**
- Database becomes bottleneck
- Single points of failure
- Network bandwidth limits
- Storage capacity limits

**Solutions:**
- Database optimization (indexing, query optimization)
- Caching layers
- Content delivery networks
- Microservices architecture
- Message queues for async processing

### **💡 Interview Tips**

#### **Do's:**
- ✅ Ask clarifying questions
- ✅ Start simple, then add complexity
- ✅ Think out loud
- ✅ Consider trade-offs
- ✅ Draw diagrams
- ✅ Discuss alternatives
- ✅ Address scalability and reliability

#### **Don'ts:**
- ❌ Jump into solution immediately
- ❌ Over-engineer from the start
- ❌ Ignore non-functional requirements
- ❌ Forget about failure scenarios
- ❌ Use technologies you don't understand
- ❌ Be silent for long periods

#### **Common Mistakes:**
- Not asking enough questions
- Designing for current scale only
- Ignoring data consistency
- Forgetting about monitoring
- Not considering security
- Over-complicating the design

---

## Common System Design Questions

Practice these frequently asked system design interview questions.

### **🌐 Social Media & Communication**

#### **1. Design Twitter/X**
**Key Features:** Tweet posting, timeline, following, trending topics
**Challenges:** High read/write ratio, real-time updates, celebrity users
**Focus Areas:** Fan-out strategies, timeline generation, caching

#### **2. Design WhatsApp/Messenger**
**Key Features:** Real-time messaging, group chats, media sharing, online status
**Challenges:** Real-time communication, message delivery, encryption
**Focus Areas:** WebSockets, message queues, end-to-end encryption

#### **3. Design Instagram**
**Key Features:** Photo/video upload, feed, stories, likes, comments
**Challenges:** Media storage, image processing, recommendation algorithm
**Focus Areas:** CDN, image optimization, timeline ranking

#### **4. Design LinkedIn**
**Key Features:** Professional profiles, connections, job postings, feed
**Challenges:** Professional networking, job matching, content relevance
**Focus Areas:** Graph database, recommendation systems, search

### **🎥 Media & Entertainment**

#### **5. Design YouTube**
**Key Features:** Video upload, streaming, recommendations, comments
**Challenges:** Video encoding, global distribution, recommendation accuracy
**Focus Areas:** Video processing pipeline, CDN, ML recommendations

#### **6. Design Netflix**
**Key Features:** Video streaming, recommendations, user profiles, offline viewing
**Challenges:** Global content delivery, personalization, content licensing
**Focus Areas:** Adaptive streaming, recommendation algorithms, CDN

#### **7. Design Spotify**
**Key Features:** Music streaming, playlists, recommendations, social features
**Challenges:** Music licensing, real-time streaming, discovery
**Focus Areas:** Audio streaming, recommendation engine, social graph

### **🛒 E-commerce & Marketplace**

#### **8. Design Amazon**
**Key Features:** Product catalog, shopping cart, payments, recommendations
**Challenges:** Inventory management, order processing, fraud detection
**Focus Areas:** Microservices, inventory systems, payment processing

#### **9. Design Uber**
**Key Features:** Ride booking, real-time tracking, payments, driver matching
**Challenges:** Real-time location, driver-rider matching, surge pricing
**Focus Areas:** Geospatial indexing, real-time updates, pricing algorithms

#### **10. Design Airbnb**
**Key Features:** Property listings, booking, reviews, payments
**Challenges:** Search and discovery, trust and safety, global operations
**Focus Areas:** Search algorithms, review systems, payment processing

### **🔧 Infrastructure & Tools**

#### **11. Design URL Shortener (bit.ly)**
**Key Features:** URL shortening, custom aliases, analytics, expiration
**Challenges:** High read/write ratio, global distribution, analytics
**Focus Areas:** Base62 encoding, caching, analytics pipeline

#### **12. Design Chat System (Slack)**
**Key Features:** Channels, direct messages, file sharing, integrations
**Challenges:** Real-time messaging, message history, scalability
**Focus Areas:** WebSockets, message storage, notification system

#### **13. Design Search Engine (Google)**
**Key Features:** Web crawling, indexing, ranking, search results
**Challenges:** Web scale, relevance ranking, real-time updates
**Focus Areas:** Distributed crawling, inverted index, PageRank

### **📊 Analytics & Monitoring**

#### **14. Design Analytics System**
**Key Features:** Event tracking, real-time dashboards, data aggregation
**Challenges:** High write volume, real-time processing, data retention
**Focus Areas:** Event streaming, time-series databases, data pipeline

#### **15. Design Notification System**
**Key Features:** Push notifications, email, SMS, in-app notifications
**Challenges:** Delivery guarantees, rate limiting, user preferences
**Focus Areas:** Message queues, delivery tracking, template management
---

## Case Studies

Detailed walkthroughs of popular system design problems.

### **📱 Case Study 1: Design WhatsApp**

#### **Requirements Clarification**
**Functional Requirements:**
- Send/receive messages (text, media)
- Group messaging (up to 256 members)
- Online/offline status
- Message delivery status (sent, delivered, read)
- Media sharing (images, videos, documents)

**Non-Functional Requirements:**
- 2 billion users globally
- 100 billion messages per day
- Real-time message delivery (<100ms)
- 99.9% availability
- End-to-end encryption

#### **Capacity Estimation**
```
Users: 2B total, 500M daily active
Messages per user per day: 50
Total messages per day: 25B
Messages per second: 25B / 86400 ≈ 290K
Peak traffic (3x): 870K messages/second

Storage per message: 100 bytes (text) + metadata
Daily storage: 25B * 100 bytes = 2.5TB
With media (10% of messages, 1MB average): +2.5TB
Total daily storage: 5TB
```

#### **High-Level Architecture**
```
Mobile Apps → Load Balancer → API Gateway → Message Service
                                              ↓
WebSocket Servers ← Message Queue ← Notification Service
        ↓                              ↓
   User Sessions              Push Notification Service
        ↓                              ↓
   Message Storage                 Media Storage
```

#### **Detailed Design**

**Message Flow:**
1. User A sends message via WebSocket
2. Message service validates and stores message
3. Message queued for delivery to User B
4. If User B online: deliver via WebSocket
5. If User B offline: store for later delivery
6. Send push notification to User B

**Database Design:**
```sql
-- Users table
Users {
  user_id: UUID PRIMARY KEY
  phone_number: VARCHAR(15) UNIQUE
  username: VARCHAR(50)
  last_seen: TIMESTAMP
  created_at: TIMESTAMP
}

-- Messages table (partitioned by chat_id)
Messages {
  message_id: UUID PRIMARY KEY
  chat_id: UUID
  sender_id: UUID
  content: TEXT
  message_type: ENUM('text', 'image', 'video')
  timestamp: TIMESTAMP
  delivery_status: ENUM('sent', 'delivered', 'read')
}

-- Chats table
Chats {
  chat_id: UUID PRIMARY KEY
  chat_type: ENUM('direct', 'group')
  created_by: UUID
  created_at: TIMESTAMP
  last_message_at: TIMESTAMP
}
```

**Scalability Solutions:**
- **Database Sharding:** Partition by chat_id
- **Message Queues:** Apache Kafka for reliable delivery
- **Caching:** Redis for active user sessions
- **CDN:** Media file distribution
- **Microservices:** Separate services for messaging, media, notifications

### **🎬 Case Study 2: Design YouTube**

#### **Requirements Clarification**
**Functional Requirements:**
- Upload videos (multiple formats, sizes)
- Watch videos (streaming, different qualities)
- Search videos
- Like/dislike, comments, subscriptions
- Video recommendations

**Non-Functional Requirements:**
- 2 billion logged-in users monthly
- 500 hours of video uploaded per minute
- 1 billion hours watched daily
- Global content delivery
- 99.9% availability

#### **Capacity Estimation**
```
Video uploads: 500 hours/minute = 30K hours/hour
Average video size: 1GB/hour
Storage needed: 30K * 1GB = 30TB/hour = 720TB/day

Video views: 1B hours/day
Concurrent viewers: 1B / 24 ≈ 42M
Peak concurrent: 42M * 3 = 126M

Bandwidth for streaming:
- 1080p: 5 Mbps
- 720p: 2.5 Mbps
- 480p: 1 Mbps
Average: 3 Mbps per stream
Peak bandwidth: 126M * 3 Mbps = 378 Tbps
```

#### **High-Level Architecture**
```
Users → CDN → Load Balancer → API Gateway
                                  ↓
Video Upload Service → Video Processing Pipeline → Video Storage
                                  ↓
Search Service ← Metadata Database → Recommendation Service
                                  ↓
Analytics Service ← User Activity → Notification Service
```

#### **Video Processing Pipeline**
```
Raw Video Upload → Validation → Transcoding → Quality Variants
                                     ↓
Thumbnail Generation → Metadata Extraction → CDN Distribution
                                     ↓
Search Index Update → Recommendation Update → Analytics Update
```

**Database Design:**
```sql
-- Videos table
Videos {
  video_id: UUID PRIMARY KEY
  user_id: UUID
  title: VARCHAR(255)
  description: TEXT
  duration: INTEGER
  upload_date: TIMESTAMP
  view_count: BIGINT
  like_count: INTEGER
  dislike_count: INTEGER
}

-- Video Files table
VideoFiles {
  file_id: UUID PRIMARY KEY
  video_id: UUID
  quality: ENUM('144p', '240p', '360p', '480p', '720p', '1080p', '4K')
  format: ENUM('mp4', 'webm', 'avi')
  file_size: BIGINT
  cdn_url: VARCHAR(500)
}
```

**Key Components:**

1. **Video Upload Service**
   - Chunked upload for large files
   - Upload progress tracking
   - Virus scanning and validation

2. **Video Processing Service**
   - Transcoding to multiple formats/qualities
   - Thumbnail generation
   - Metadata extraction (duration, resolution)

3. **Content Delivery Network**
   - Global distribution of video files
   - Adaptive bitrate streaming
   - Edge caching for popular content

4. **Recommendation Engine**
   - Collaborative filtering
   - Content-based filtering
   - Machine learning models for personalization

5. **Search Service**
   - Elasticsearch for video search
   - Auto-complete suggestions
   - Trending topics
---

## Best Practices & Tips

### **📚 Study Resources**

#### **Essential Books**
1. **"Designing Data-Intensive Applications" by Martin Kleppmann**
   - Deep dive into distributed systems
   - Data modeling and storage
   - Consistency and consensus

2. **"System Design Interview" by Alex Xu**
   - Practical interview preparation
   - Step-by-step problem solving
   - Real-world examples

3. **"Building Microservices" by Sam Newman**
   - Microservices architecture
   - Service decomposition
   - Operational considerations

#### **Online Resources**
- **High Scalability:** Architecture case studies
- **AWS Architecture Center:** Cloud design patterns
- **Google Cloud Architecture Framework:** Best practices
- **Microsoft Azure Well-Architected Framework:** Design principles

#### **YouTube Channels**
- **Gaurav Sen:** System design concepts
- **Tech Dummies:** Interview preparation
- **System Design Interview:** Mock interviews

### **🎯 Practice Strategy**

#### **Week 1-2: Fundamentals**
- Study basic concepts (scalability, databases, caching)
- Understand trade-offs
- Learn about different architectures

#### **Week 3-4: Common Patterns**
- Load balancing strategies
- Database scaling techniques
- Caching patterns
- Message queue patterns

#### **Week 5-6: Practice Problems**
- Start with simple problems (URL shortener)
- Progress to complex systems (social media)
- Focus on end-to-end design

#### **Week 7-8: Mock Interviews**
- Practice with peers or online platforms
- Time yourself (45-60 minutes)
- Get feedback on your approach

### **🔧 Tools for Practice**

- **Draw.io:** Create architecture diagrams
- **Lucidchart:** Professional diagramming
- **Miro/Mural:** Collaborative whiteboarding
- **Excalidraw:** Simple sketching tool

### **📈 Continuous Learning**

- Follow engineering blogs of major tech companies
- Attend system design meetups and conferences
- Read about new technologies and trends
- Practice explaining complex systems simply

---

## Quick Reference

### **📊 Numbers Every Engineer Should Know**

```
L1 cache reference:                 0.5 ns
Branch mispredict:                  5 ns
L2 cache reference:                 7 ns
Mutex lock/unlock:                  25 ns
Main memory reference:              100 ns
Compress 1K bytes with Zippy:       10,000 ns = 10 μs
Send 1K bytes over 1 Gbps network:  10,000 ns = 10 μs
Read 4K randomly from SSD:          150,000 ns = 150 μs
Read 1 MB sequentially from memory: 250,000 ns = 250 μs
Round trip within same datacenter:  500,000 ns = 500 μs
Read 1 MB sequentially from SSD:    1,000,000 ns = 1 ms
Disk seek:                          10,000,000 ns = 10 ms
Read 1 MB sequentially from disk:   30,000,000 ns = 30 ms
Send packet CA→Netherlands→CA:      150,000,000 ns = 150 ms
```

### **🎯 System Design Cheat Sheet**

#### **Scalability Patterns**
- **Load Balancing:** Distribute traffic across servers
- **Caching:** Store frequently accessed data
- **Database Scaling:** Read replicas, sharding, partitioning
- **CDN:** Global content distribution
- **Microservices:** Service decomposition

#### **Database Choices**
- **RDBMS:** ACID properties, complex queries, structured data
- **NoSQL Document:** Flexible schema, JSON documents
- **NoSQL Key-Value:** Simple operations, high performance
- **NoSQL Column:** Analytics, time-series data
- **NoSQL Graph:** Relationships, social networks

#### **Communication Patterns**
- **Synchronous:** REST APIs, GraphQL
- **Asynchronous:** Message queues, event streaming
- **Real-time:** WebSockets, Server-Sent Events

#### **Consistency Models**
- **Strong Consistency:** All nodes see same data simultaneously
- **Eventual Consistency:** Nodes will eventually converge
- **Weak Consistency:** No guarantees about when data will be consistent

---

*This guide provides a comprehensive foundation for system design interviews. Remember to practice regularly, stay updated with industry trends, and focus on understanding trade-offs rather than memorizing solutions.*

**Good luck with your system design interviews! 🚀**