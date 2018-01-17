---
layout: single
title:  "Java Trivia Questions"
date:   2017-09-25 10:13:06 -0500
categories: Tech
toc: true
toc_label: "On this page"
toc_icon: "gear"
---

Notes taken from: [JavaTpoint](https://www.javatpoint.com/corejava-interview-questions)

{:toc}

### Side Notes:

- No need to remove unreferenced objects because there is Automatic Garbage Collection in java.
- Java is secured because:
  1. No explicit pointer
  2. Java Programs run inside virtual machine sandbox
  3. There is exception handling and type checking mechanism in java (Java is a statically typed language). 
- In C programming, int data type occupies 2 bytes of memory for 32-bit architecture and 4 bytes of memory for 64-bit architecture. But in java, it occupies 4 bytes of memory for both 32 and 64 bit architectures.
- Whenever you write java command on the command prompt to run the java class, an instance of JVM is created.
- Java Stack stores frames.It holds local variables and partial results, and plays a part in method invocation and return. Each thread has a private JVM stack, created at the same time as thread. A new frame is created each time a method is invoked. A frame is destroyed when its method invocation completes.
- **There are three types of variables in java: local, instance and static.**
- In java programming, multiple and hybrid inheritance is supported through interface only
- super() can be used to invoke immediate parent class constructor.
- **super() is added in each class constructor automatically by compiler if there is no super() or this().**
- **Runtime polymorphism can't be achieved by data members.**
- An object is an instance of particular java class, but it is also an instance of its superclass.
- I**f there is any abstract method in a class, that class must be abstract.**
- **If you are extending any abstract class that have abstract method, you must either provide the implementation of the method or make this class abstract.**
- Abstraction in Java can be achieved through abstract classes or interfaces. Interface provides full abstraction because it is just a blueprint and all methods are abstract. In an abstract class, some methods may not be abstract.
- **Since Java 8, interface can have default and static methods**
- **The java compiler adds public and abstract keywords before the interface method. More, it adds public, static and final keywords before data members.**
- Since Java 8, we can have method body in interface. But we need to make it default method.
- Since Java 8, we can have static method in interface.
- **If you don't handle exception, before terminating the program, JVM executes finally block(if any).**
- For each try block there can be zero or more catch blocks, but only one finally block.
- **The finally block will not be executed if program exits(either by calling System.exit() or by causing a fatal error that causes the process to abort).**
- String objects are stored in a special memory area known as string constant pool.
- To create the singleton class, we need to have static member of class, private constructor and static factory method.

### Object-oriented

Object-oriented means we organize our software as a combination of different types of objects that incorporates both data and behaviour.
Object-oriented programming(OOPs) is a methodology that simplify software development and maintenance by providing some rules.

Basic concepts of OOPs are:
- Object
- Class
- Inheritance
- Polymorphism
- Abstraction
- Encapsulation

### Platform-Independent
A platform is the hardware or software environment in which a program runs.

There are two types of platforms software-based and hardware-based. Java provides software-based platform.

The Java platform differs from most other platforms in the sense that it is a software-based platform that runs on the top of other hardware-based platforms. It has two components:
1. Runtime Environment
2. API(Application Programming Interface)

Java code can be run on multiple platforms e.g. Windows, Linux, Sun Solaris, Mac/OS etc. Java code is compiled by the compiler and converted into bytecode. This bytecode is a platform-independent code because it can be run on multiple platforms i.e. Write Once and Run Anywhere(WORA).

### Multi-threading in Java

A thread is like a separate program, executing concurrently. We can write Java programs that deal with many tasks at once by defining multiple threads. The main advantage of multi-threading is that it doesn't occupy memory for each thread. It shares a common memory area.

### Diff between C++ and Java
https://www.javatpoint.com/cpp-vs-java

### Q.  What happens at runtime and compile time?

### Q. **Comparison of JRE, JDK, JVM

### Q. Why char uses 2 byte in java and what is \u0000 ?

It is because java uses Unicode system than ASCII code system. The \u0000 is the lowest range of Unicode system.

### What is difference between object oriented programming language and object based programming language?

Object based programming languages follow all the features of OOPs except Inheritance. Examples of object based programming languages are JavaScript, VBScript etc.

###  What is constructor?

Constructor is just like a method that is used to initialize the state of an object. It is invoked at the time of object creation.

### **Does constructor return any value?

Yes, that is current class instance (You cannot use return type yet it returns a value).

### **What is a Java static block?

Is used to initialize the static data member.
It is executed before main method at the time of classloading.

### What is Inheritance?
- Inheritance in java is a mechanism in which one object acquires all the properties and behaviors of parent object.
- The idea behind inheritance in java is that you can create new classes that are built upon existing classes. When you inherit from an existing class, you can reuse methods and fields of parent class, and you can add new methods and fields also.
- Inheritance represents the IS-A relationship, also known as parent-child relationship.

### What is Aggregation?
Has-A relationship. When an object of one class is instantiated in another class.

### When use Aggregation?
Code reuse is best achieved by aggregation when there is no is-a relationship.
Inheritance should be used only if the relationship is-a is maintained throughout the lifetime of the objects involved; otherwise, aggregation is the best choice.

### Method Overriding
If subclass (child class) has the same method as declared in the parent class, it is known as method overriding in java.

### Can we override static method?
No, you can't override the static method because they are the part of class not object.

### What is covariant return type?
- overriding a method by just changing the return type. (when return type is non-primitive).

### Java final variable
If you make any variable as final, you cannot change the value of final variable(It will be constant).

### Java final method
If you make any method as final, you cannot override it.

### Java final class
If you make any class as final, you cannot extend it.

### **What is blank or uninitialized final variable?

A final variable that is not initialized at the time of declaration is known as blank final variable.

If you want to create a variable that is initialized at the time of creating object and once initialized may not be changed, it is useful. For example PAN CARD number of an employee.

It can be initialized only in constructor.

### **What is static blank final variable

A static final variable that is not initialized at the time of declaration is known as static blank final variable. It can be initialized only in static block.

### What is Polymorphism?
Polymorphism in java is a concept by which we can perform a single action by different ways.

There are two types of polymorphism in java: compile time polymorphism and runtime polymorphism. We can perform polymorphism in java by method overloading and method overriding.

** **If you overload static method in java, it is the example of compile time polymorphism. Here, we will focus on runtime polymorphism in java**

Runtime polymorphism or Dynamic Method Dispatch is a process in which a call to an overridden method is resolved at runtime rather than compile-time

### Upcasting
When reference variable of Parent class refers to the object of Child class, it is known as upcasting

**Upcasting + overriding = runtime polymorphism**

Java Runtime Polymorphism with Data Member

** _Method is overridden not the datamembers, so runtime polymorphism can't be achieved by data members.
In the example given below, both the classes have a datamember speedlimit, we are accessing the datamember by the reference variable of Parent class which refers to the subclass object. Since we are accessing the datamember which is not overridden, hence it will access the datamember of Parent class always._

### Static binding
When type of the object is determined at compiled time(by the compiler), it is known as static binding.

If there is any private, final or static method in a class, there is static binding.

### Dynamic binding
When type of the object is determined at run-time, it is known as dynamic binding.

### Abstract class in Java

A class that is declared with abstract keyword, is known as abstract class in java. It can have abstract and non-abstract methods (method with body).

It needs to be extended and its method implemented. **It cannot be instantiated.**

### Abstract method

A method that is declared as abstract and does not have implementation is known as abstract method.

### Interface in Java
- An interface in java is a blueprint of a class. It has static constants and abstract methods.
- The interface in java is a mechanism to achieve abstraction. 
- There can be only abstract methods in the java interface not method body.
- It is used to achieve abstraction and multiple inheritance in Java.
- Java Interface also represents IS-A relationship.
  -** It cannot be instantiated just like abstract class.**

### Q. Why use Java interface?

There are mainly three reasons to use interface:

1. It is used to achieve abstraction.
2. By using interface, we can support the functionality of multiple inheritance.
3. It can be used to achieve loose coupling.

### Q. Can you declare an interface method static?

No, because methods of an interface is abstract by default, and **static and abstract keywords can't be used together**.

### Multiple inheritance in Java by interface

If a class implements multiple interfaces, or an interface extends multiple interfaces i.e. known as multiple inheritance.

### Multiple inheritance is not supported through class in java but it is possible by interface, why?

As we have explained in the inheritance chapter, multiple inheritance is not supported in case of class because of ambiguity. But it is supported in case of interface because there is no ambiguity as implementation is provided by the implementation class.

### Q. **Can we define private and protected modifiers for variables in interfaces?

**No, they are implicitly public.**

### Q. When can an object reference be cast to an interface reference?

**An object reference can be cast to an interface reference when the object implements the referenced interface.**

### Q. What is package?

A package is a group of similar type of classes, interfaces and sub-packages. It provides access protection and removes naming collision.

### **What is the difference between import and static import?

The import allows the java programmer to access classes of a package without package qualification whereas the static import feature allows to access the static members of a class without the class qualification. The import provides accessibility to classes and interface whereas static import provides accessibility to static members of the class.

### Q. What is Exception Handling?
Exception Handling is a mechanism to handle runtime errors.

### Java finally block
- Java finally block follows try or catch block.
- Java finally block is always executed whether exception occurs or not and whether it is handled or not.
- Java finally block is a block that is used to execute important code such as closing connection, stream etc.

### Q. **Why are string objects immutable in Java?  

Because java uses the concept of string literal. Suppose there are 5 reference variables, all refer to one object "sachin".If one reference variable changes the value of the object, it will be affected to all the reference variables. That is why string objects are immutable in java.

### Each time you create a string literal, the JVM checks the string constant pool first. If the string already exists in the pool, a reference to the pooled instance is returned. If string doesn't exist in the pool, a new string instance is created and placed in the pool. For example:

String s1="Welcome";  
String s2="Welcome";//will not create new instance  

### Q. Why java uses concept of string literal?

To make Java more memory efficient

### By new keyword

String s=new String("Welcome"); //creates two objects and one reference variable  

In such case, JVM will create a new string object in normal(non pool) heap memory and the literal "Welcome" will be placed in the string constant pool. The variable s will refer to the object in heap(non pool).

### StringBuffer
Java StringBuffer class is thread-safe i.e. multiple threads cannot access it simultaneously (synchronized). So it is safe and will result in an order.

### StringBuilder
The Java StringBuilder class is same as StringBuffer class except that it is non-synchronized. It is also more efficient than StringBuffer.

### **Multi-threading
Multithreading in java is a process of executing multiple threads simultaneously.

Thread is basically a lightweight sub-process, a smallest unit of processing. Multiprocessing and multithreading, both are used to achieve multitasking.

_But we use multithreading than multiprocessing because threads share a common memory area. They don't allocate separate memory area so saves memory, and context-switching between the threads takes less time than process._

### Life-cycle of threads
The life cycle of the thread in java is controlled by JVM. The java thread states are as follows:
- New
- Runnable
- Non-Runnable (Blocked)
- Terminated

### How to create thread

There are two ways to create a thread:

1. By extending Thread class
2. By implementing Runnable interface. (If you are not extending the Thread class,your class object would not be treated as a thread object.So you need to explicitely create Thread class object.We are passing the object of your class that implements Runnable so that your class run() method may execute)

### **What if we call run() method directly instead start() method?

Each thread starts in a separate call stack.
Invoking the run() method from main thread, the run() method goes onto the current call stack rather than at the beginning of a new call stack.

refer this: https://www.javatpoint.com/what-if-we-call-run()-method-directly

### Points to remember for Daemon Thread in Java

- It provides services to user threads for background supporting tasks. 
- It has no role in life than to serve user threads.
- Its life depends on user threads.
- It is a low priority thread.
- If you want to make a user thread as Daemon, it must not be started otherwise it will throw IllegalThreadStateException.

### Java Thread pool represents a group of worker threads that are waiting for the job and reuse many times.

In case of thread pool, a group of fixed size threads are created. A thread from the thread pool is pulled out and assigned a job by the service provider. After completion of the job, thread is contained in the thread pool again.

### Advantage of Java Thread Pool

Better performance It saves time because there is no need to create new thread.

### Java Garbage Collection

- In java, garbage means unreferenced objects.
- Garbage Collection is process of reclaiming the runtime unused memory automatically. 
- In other words, it is a way to destroy the unused objects.

- **The finalize() method is invoked each time before the object is garbage collected. This method can be used to perform cleanup processing.**
- The Garbage collector of JVM collects only those objects that are created by new keyword. So if you have created any object without new, you can use finalize method to perform cleanup processing
- The gc() method is used to invoke the garbage collector to perform cleanup processing.

### Synchronization in Java

Synchronization in java is the capability to control the access of multiple threads to any shared resource.

Java Synchronization is better option where we want to allow only one thread to access the shared resource.

1. Mutual Exclusive

  - Mutual Exclusive helps keep threads from interfering with one another while sharing data. This can be done by three ways in java:
    1. by synchronized method
    2. by synchronized block
    3. by static synchronization

### Concept of Lock in Java

Synchronization is built around an internal entity known as the lock or monitor. Every object has an lock associated with it. By convention, a thread that needs consistent access to an object's fields has to acquire the object's lock before accessing them, and then release the lock when it's done with them.

### Synchronized block in java

Synchronized block can be used to perform synchronization on any specific resource of the method.

Suppose you have 50 lines of code in your method, but you want to synchronize only 5 lines, you can use synchronized block.

### Advantage of static synchronization method

If you make any static method as synchronized, the lock will be on the class not on object.

Suppose there are two objects of a shared class(e.g. Table) named object1 and object2.In case of synchronized method and synchronized block there cannot be interference between t1 and t2 or t3 and t4 because t1 and t2 both refers to a common object that have a single lock.But there can be interference between t1 and t3 or t2 and t4 because t1 acquires another lock and t3 acquires another lock.I want no interference between t1 and t3 or t2 and t4.Static synchronization solves this problem.

### *Enums in Java
https://www.javatpoint.com/enum-in-java

### Garbage Collection in Java
- Garbage collection is the phrase used to describe automatic memory management in Java.
- it’s typical for memory to be used to create a stack, a heap, in Java’s case constant pools, and method areas. The **heap** is that part of memory where Java objects live, and **it’s the one and only part of memory that is in any way involved in the garbage collection process.**
 - When the garbage collector runs, its purpose is to find and delete objects that cannot be reached.
 - An object is eligible for garbage collection when no live thread can access it.