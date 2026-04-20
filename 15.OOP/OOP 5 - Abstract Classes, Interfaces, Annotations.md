# OOP - 5:-
![t](images/oops_5.png)
# Abstract Classes:-
Sometimes you will want to create a superclass that only defines a generalized form that will be shared by all of its
subclasses, leaving it to each subclass to fill in the details. Such a class determines the nature of the methods that
the subclasses must implement.
You may have methods that must be overridden by the subclass in order for the subclass to have any meaning.
In this case, you want some way to ensure that a subclass does, indeed, override all necessary methods. Java’s solution
to this problem is the abstract method.
You can require that certain methods be overridden by subclasses by specifying the abstract type modifier.

        abstract type name(parameter-list);

These methods are sometimes referred to as subclass's responsibility because they have no implementation specified in
the superclass.
Thus, a subclass must override them—it cannot simply use the version defined in the superclass.

Any class that contains one or more abstract methods must also be declared abstract.
# There can be no objects of an abstract class.
# You cannot declare abstract constructors, or abstract static methods.
# You can declare static methods in abstract class.
Because there can be no objects for abstract class. If they had allowed to call abstract static methods,
it would that mean we are calling an empty method (abstract) through classname because it is static.
Any subclass of an abstract class must either implement all of the abstract methods in the superclass,
or be declared abstract itself.
Abstract classes can include as much implementation as they see fit i.e.there can be concrete methods(methods with body)
in abstract class.

Although abstract classes cannot be used to instantiate objects, they can be used to create object references,
because Java’s approach to run-time polymorphism is implemented through the use of superclass references.

A public constructor on an abstract class doesn't make any sense because you can't instantiate an abstract class directly 
(can only instantiate through a derived type that itself is not marked as abstract)
Check: https://stackoverflow.com/questions/260666/can-an-abstract-class-have-a-constructor


Abstract class vs Interface:

Type of methods:
Interface can have only abstract methods.
Abstract class can have abstract and non-abstract methods. From Java 8, it can have default and static methods also.

Final Variables:
Variables declared in a Java interface are by default final.
An abstract class may contain non-final variables.

Type of variables:
Abstract class can have final, non-final, static and non-static variables.
Interface has only static and final variables.(hence you have to intialize declared variable anyway.)

Implementation:
Abstract class can provide the implementation of interface.
Interface can’t provide the implementation of abstract class.

Inheritance vs Abstraction:
A Java interface can be implemented using keyword “implements”
and abstract class can be extended using keyword “extends”.

Multiple implementation:
An interface can extend another Java interface only,
an abstract class can extend another Java class and implement(i.e.extend) multiple Java interfaces.

Accessibility of Data Members:
Members of a Java interface are public by default.(as if you declare them as private then you can't use those in their child classes,and even if you can use them in that interface what's the point of using them as interfaces can have only var and not body of any function->hence private members are not allowed in interfaces)
A Java abstract class can have class members like private, protected, etc.(as abstract class can have methods having concrete body,hence you can use those and access those private variables in the same class and can make some use of it..)

# Interfaces:-
Multiple inheritance is not available in java.
(Same functions in 2 classes it will skip that hence no multiple inheritance)

Instead we have java interfaces. they have abstract functions (no body of functions)

Interface is like class but not completely. it is like an abstract class.
By default functions are public and abstract in interface.
variables are final and static by default in interface.

Interfaces specify only what the class is doing, not how it is doing it.
The problem with MULTIPLE INHERITANCE is that two classes may define different ways of doing the same thing,
and the subclass can't choose which one to pick.

Key difference between a class and an interface: a class can maintain state information
(especially through the use of instance variables), but an interface cannot.

Using interface, you can specify a set of methods that can be implemented by one or more classes.
Although they are similar to abstract classes, interfaces have an additional capability:
A class can implement more than one interface. By contrast, a class can only inherit a single superclass
(abstract or otherwise).

Using the keyword interface, you can fully abstract a class’ interface from its implementation.
That is, using interface, you can specify what a class must do, but not how it does it.

Interfaces are syntactically similar to classes, but they lack instance variables(
- static variable → ❌ NOT an instance variable
- final variable → ✅ CAN be an instance variable
- static final variable → ❌ NOT an instance variable
), and, as a general rule,
their methods are declared without any body.

By providing the interface keyword, Java allows you to fully utilize the “one interface, multiple methods”
aspect of polymorphism.

NOTE: Interfaces are designed to support dynamic method resolution at run time.
Normally, in order for a method to be called from one class to another, both classes need to be present at compile time
so the Java compiler can check to ensure that the method signatures are compatible. This requirement by itself makes for
a static and nonextensible classing environment. Inevitably in a system like this, functionality gets pushed up higher
and higher in the class hierarchy so that the mechanisms will be available to more and more subclasses. Interfaces are
designed to avoid this problem. They disconnect the definition of a method or set of methods from the inheritance
hierarchy. Since interfaces are in a different hierarchy from classes, it is possible for classes that are unrelated
in terms of the class hierarchy to implement the same interface. This is where the real power of interfaces is realized.
- e.g.A obj = new B();-> obj.start();
- e.g.Engine car = new PowerEngine();
-In short you need ref type(superclass-A) and obj type(subclass-B) classes at compile time in order to call overriden methods,to resolve whether over-riden methods have same signature or not? but in interfaces ref type class needs should resolve at compile time(Engine car) and we know that all the methods in an parent class have been over-riden by child child class for sure hence no need to have child class at the same time as obj type(new PowerEngine()) will get resolved at runtime in Interfaces)

Beginning with JDK 8, it is possible to add a default implementation to an interface method.
Thus, it is now possible for interface to specify some behavior.However, default methods constitute what is, in essence,
a special-use feature, and the original intent behind interface still remains.

Variables can be declared inside of interface declarations.
NOTE: They are implicitly final and static, meaning they cannot be changed by the implementing class.
They must also be initialized. All methods and variables are implicitly public.

NOTE: The methods that implement an interface must be declared public. Also, the type signature of the implementing
method must match exactly the type signature specified in the interface definition.

It is both permissible and common for classes that implement interfaces to define additional members of their own.

NOTE:
You can declare variables as object references that use an interface rather than a class type.
This process is similar to using a superclass reference to access a subclass object.
Any instance of any class that implements the declared interface can be referred to by such a variable.
When you call a method through one of these references, the correct version will be called based on the actual instance
of the interface being referred to. Called at run time by the type of object it refers to.
The method to be executed is looked up dynamically at run time, allowing classes to be created later than the code which
calls methods on them.
The calling code can dispatch through an interface without having to know anything about the “callee.” (callee-obj type class or RHS)

CAUTION: Because dynamic lookup of a method at run time incurs a significant overhead when compared with the normal
method invocation in Java, you should be careful not to use interfaces casually in performance-critical code.


Nested Interfaces:

An interface can be declared a member of a class or another interface. Such an interface
is called a member interface or a nested interface. A nested interface can be declared as public, private, or protected.
This differs from a top-level interface, which must either be declared as public or use the default access level.

// This class contains a member interface.
class A {
  // this is a nested interface
  public interface NestedIF {
    boolean isNotNegative(int x);
  }
}
// B implements the nested interface.
class B implements A.NestedIF {
  public boolean isNotNegative(int x) {
    return x < 0 ? false: true;
  }
}
class NestedIFDemo {
  public static void main(String args[]) {
    // use a nested interface reference
    A.NestedIF nif = new B();
    if(nif.isNotNegative(10))
      System.out.println("10 is not negative");
    if(nif.isNotNegative(-12))
      System.out.println("this won't be displayed");
  }
}

Interfaces Can Be Extended:
One interface can inherit another by use of the keyword extends. The syntax is the same as for inheriting classes.
Any class that implements an interface must implement all methods required by that interface, including any that are
inherited from other interfaces.


Default Interface Methods (aka extension method) :
A primary motivation for the default method was to provide a means by which interfaces could be expanded without breaking existing code.
i.e. suppose you add another method without body in an interface. Then you will have to provide the body of that method
in all the classes that implement that interface.
Ex:
 default String getString() {
    return "Default String";
 }

For example, you might have a class that implements two interfaces.
If each of these interfaces provides default methods, then some behavior is inherited from both.
# In all cases, a class implementation takes priority over an interface default implementation.
# In cases in which a class implements two interfaces that both have the same default method, but the class does not
override that method, then an error will result.
# In cases in which one interface inherits another, with both defining a common default method, the inheriting
interface’s version of the method takes precedence.

NOTE: static interface methods are not inherited by either an implementing class or a subinterface.
i.e. static interface methods should have a body! They cannot be abstract. 

NOTE : when overriding methods, the access modifier should be same or better i.e. if in Parent Class it was protected, then overridden should be either protected or public.

# Imp example:-
📌 Interfaces in Java – Engine, Media, Brake (Car Example):-
Suppose we have multiple interfaces with same method names:
```java
interface Engine {
    void start();
    void stop();
}

interface Media {
    void start();
    void stop();
}

interface Brake {
    void brake();
}
// Car class implementing BOTH Engine & Media
class Car implements Engine, Media {

    @Override
    public void start() {
        System.out.println("Car started (Engine + Media together)");
    }

    @Override
    public void stop() {
        System.out.println("Car stopped (Engine + Media together)");
    }
}

// Using car.start()
public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.start();   // Which start? Engine or Media?->Car started (Engine + Media together)
    }
}
```
If one class implements both Engine and Media, calling:
car.start();
* Ambiguous meaning
- Should it start "engine" ❓
-Or start "media system" ❓
- Java does NOT know which behavior you want logically, even though method signatures match.
```java
// Interfaces
interface Engine {
    void start();
    void stop();
}

interface Media {
    void start();
    void stop();
}

interface Brake {
    void brake();
}

// Engine implementation
class PowerEngine implements Engine {
    public void start() {
        System.out.println("Engine started");
    }
    public void stop() {
        System.out.println("Engine stopped");
    }
}

// Media implementation
class MusicPlayer implements Media {
    public void start() {
        System.out.println("Music started");
    }
    public void stop() {
        System.out.println("Music stopped");
    }
}

// Interface extending interface
interface AdvancedEngine extends Engine {
    void turbo();
}

// Using composition (BEST DESIGN)
class NiceCar {
    private Engine engine;
    private Media media;

    NiceCar() {
        engine = new PowerEngine();
        media = new MusicPlayer();
    }

    void startEngine() {
        engine.start();
    }

    void stopEngine() {
        engine.stop();
    }

    void startMedia() {
        media.start();
    }

    void stopMedia() {
        media.stop();
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        NiceCar car = new NiceCar();
        car.startEngine(); // Engine started
        car.startMedia();  // Music started
    }
}
```

# Annotations:-
📌 Java Annotations – 
🔹 What are Annotations in Java?

Annotations are metadata added to Java code that provide extra information to:

Compiler

JVM

Frameworks (Spring, Hibernate, JUnit, etc.)

👉 They do not change program logic directly, but influence behavior at compile-time or runtime.

@Override
void show() { }

🔹 Why Annotations are Used?

To avoid errors (compile-time checking)

To replace XML configuration

To provide instructions to compiler / framework

To improve code readability and maintainability

🔹 Syntax of Annotation
```java
@AnnotationName
```

Example:
```java
@Override
```
🔹 Types of Annotations in Java

1️⃣ Built-in Annotations
2️⃣ Meta-Annotations
3️⃣ Custom Annotations

1️⃣ Built-in Annotations

These are provided by Java.

- 🔸 @Override

Ensures method correctly overrides parent method

Gives compile-time error if method signature is wrong
```java
class Parent {
    void show() {}
}

class Child extends Parent {
    @Override
    void show() {}
}

```
✔ Prevents mistakes
✔ Improves code safety

- 🔸 @Deprecated
Marks method/class as old

Compiler gives warning

Still works, but not recommended
```java
@Deprecated
void oldMethod() {}
```

Used when:

Better alternative exists/

Method will be removed in future

- 🔸 @SuppressWarnings

Suppresses compiler warnings
```java
@SuppressWarnings("unchecked")
```

Common values:

"unchecked"

"deprecation"

"rawtypes"

- 🔸 @FunctionalInterface

Ensures interface has only one abstract method

Used in Lambda Expressions
```java
@FunctionalInterface
interface Test {
    void show();
}
```

❌ More than one abstract method → compile-time error

2️⃣ Meta-Annotations

Meta-annotations are annotations used on other annotations.

- 🔸 @Target

Defines where annotation can be applied.
```java
@Target(ElementType.METHOD)
```

Common values:

TYPE → class, interface

METHOD

FIELD

CONSTRUCTOR

PARAMETER

- 🔸 @Retention

Defines how long annotation is available.
```java
@Retention(RetentionPolicy.RUNTIME)
```
- Policy-Available Till
- SOURCE-Source code only
- CLASS-Bytecode
- RUNTIME- Runtime (JVM)
  -🔸 @Documented

Annotation appears in JavaDoc

```java
@Documented
```
- 🔸 @Inherited

Child class inherits annotation from parent class
```java
@Inherited
```
3️⃣ Custom Annotations (User-Defined)

You can create your own annotation.

🔹 Syntax to Create Annotation
```java
@interface MyAnnotation {
    String value();
}
```

Usage:
```java
@MyAnnotation(value = "Hello")
class Test {}
```
🔹 Annotation with Default Value
```java
@interface Info {
    String name() default "Java";
}
```

Usage:
```java
@Info
class Demo {}
```
🔹 Annotations with Methods (Elements)
```java
@interface Details {
    int id();
    String name();
}
```

Usage:
```java
@Details(id = 1, name = "Gauri")
class Student {}
```
