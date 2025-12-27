# OOP 3:-
![r](images/oops_31.png)
![t](images/oops_32.png)
![y](images/oops_33.png)
![e](images/oops_34.png)
# OOP :-
1. Introduction to OOP = Object Oriented Programming
Programming is divided into classes and objects

Focus is on real-life modeling
Improves:
Code security
Code reuse
Maintainability

2. Principles of OOP (Mentioned in Video)
Encapsulation
Inheritance
Polymorphism
Abstraction

# Inheritance :-
3. What is Inheritance?
Inheritance means child class acquires properties of parent class
Parent class = Base class / Super class
Child class = Derived class / Sub class

Real-life Example :-
Parents pass:
Money
Values
Habits
Properties
Similarly, a class passes variables and methods to another class

4. Basic Definition (Programming)
One class is created
Another class extends it

Child class can use:
Variables
Methods
Functions of parent class

5. Syntax of Inheritance (Java)
class Parent {
    int x;
}

class Child extends Parent {
    int y;
}

extends keyword is used
Child class gets access to parent members

6. Parent & Child Class Relationship
Parent class:
Contains common properties
Child class:
Contains parent properties
Plus its own additional properties

Example :-
Base class: Box

parent properties:-length, width, height

Child class:
Inherits dimensions
Adds extra features

7. Constructors in Inheritance
Constructors are not inherited
When child object is created:
Parent constructor executes first
Then child constructor executes
Important Rule
Parent constructor must be called
If not written explicitly, Java calls it automatically

8. super Keyword
Used to:
Call parent constructor
- Access parent variables
- Access parent methods
- Example Meaning:-
super.variable → parent variable
- super() → parent constructor

9. Access Modifiers & Inheritance
- private Keyword
- private members:
❌ NOT accessible in child class
- Even though child inherits the class, private data is hidden

Important Statement :-
“Private members belong only to that class, not even child class can access them directly.”

10. Reference Variable Concept (Important)
- Access depends on reference type, not object type
- Example meaning from video:
- Parent obj = new Child();

Accessible:
- Parent class members
Not accessible:
- Child-specific members

11. Types of Inheritance (Video Mentions)
*Single Inheritance
- One parent → one child
- Most commonly used
- Fully supported in Java
- class A { }
- class B extends A { }

# Key Points Repeated in Video
- Inheritance promotes code reuse
- Child class automatically gets parent features
- Constructors are special, not inherited
- super connects child to parent
- private restricts access
- Java follows class hierarchy
- Inheritance uses extends
- Parent constructor executes first
- Private members are not inherited
- Access is decided by reference type
- Java supports single inheritance using classes

Multiple Inheritance (Java)
*Multiple Inheritance means:
One child class inherits from more than one parent class
*Example idea:
Class C extends A, B   ❌ (Not allowed in Java)

Why Multiple Inheritance is NOT Supported in Java (Classes):-
- Causes ambiguity problem
- If both parent classes have:
Same method name, Same signature(if they share the same method name and the exact same parameter list (same number, type, and order of parameters). The return type and access modifiers are not considered part of the method signature for this purpose.)
→ Java cannot decide which method to call
- This is called:
Diamond Problem, Leads to conflicts
- Java’s Decision
❌ Multiple inheritance using classes is not allowed
✅ Achieved using interfaces

How Java Supports Multiple Inheritance:-
- Using Interfaces
- Interfaces contain:
Method declarations (no implementation)
Hence, no ambiguity

Hierarchical Inheritance
Meaning
One parent class
Multiple child classes

-Structure
Parent class can have 3 inherited child classes.

Key Points
- All child classes inherit:
- Same properties of parent
- Very simple
- Fully supported in Java

Hybrid Inheritance
Combination of:
Single inheritance
Multiple inheritance

Important Point
Hybrid inheritance involves multiple inheritance
Therefore:
❌ Not allowed using classes
✅ Achieved using interfaces

---
# KK notes:-
## Inheritance-
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

Interfaces are syntactically similar to classes, but they lack instance variables, and, as a general rule,
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
The calling code can dispatch through an interface without having to know anything about the “callee.”

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

NOTE : when overriding methods, the access modifier should be same or better i.e. if in Parent Class it was protected, then then overridden should be either protected or public.

---
# Polymorphism
Meaning
Poly = many
Morph = forms
One entity behaving in multiple forms
Simple Definition
Representing the same thing in different ways

## Types of Polymorphism
1️⃣ Compile-Time Polymorphism (Static)
Achieved by:
Method Overloading.
i.e. Same method name &
Different:
Number of parameters
Type of parameters
Order of parameters

add(int a, int b)
add(double a, double b)

Key Points
Decided at compile time
Return type alone cannot differentiate methods
Java does not support operator overloading

2️⃣ Runtime Polymorphism (Dynamic)
Achieved by:
Method Overriding
- Method Overriding
Child class provides its own implementation
Method must have:
Same name
Same parameters
Same return type

class Shape {
    void area() { }
}

class Circle extends Shape {
    void area() { }
}

Key Rule
Method call depends on:
Object type, not reference type

How Java Decides Which Method to Call?
Rule
Java uses Dynamic Method Dispatch
Decision happens at runtime

Shape s = new Circle();
s.area();   // Circle's area() is called

Why?
Object is of type Circle
Reference is of type Shape

## Overloading vs Overriding 
- Feature	           -  Overloading	-  Overriding
- Polymorphism type	 -  Compile-time-  	Runtime
- Method name	       -  Same	        - Same
- Parameters	       - Different	  -  Same
- Inheritance needed -❌ No    	    - ✅ Yes
- Binding	           - Early	      - Late

## final Keyword (From Transcript)
- Uses of final
- Prevent overriding
- Prevent inheritance
- Prevent modification

## Final Method
- Cannot be overridden
- Final Class
- Cannot be inherited

## Important points
- Multiple inheritance using classes is not supported in Java
- Java supports multiple inheritance using interfaces
- Overloading → Compile time polymorphism
-Overriding → Runtime polymorphism
- Method selection depends on object type
- final prevents overriding

---
# Over-riding(KK notes):-
In a class hierarchy, when a method in a subclass has the same name and type signature as a method in its superclass,
then the method in the subclass is said to override the method in the superclass. When an overridden method is called
from within its subclass, it will always refer to the version of that method defined by the subclass. The version of the
method defined by the superclass will be hidden.

Method overriding occurs only when the names and the type signatures of the two methods are identical.
If they are not, then the two methods are simply overloaded.

(Check display functions in box classes)

Dynamic Method Dispatch:

Dynamic method dispatch is the mechanism by which a call to an overridden method is resolved at run time, rather than
compile time. Dynamic method dispatch is important because this is how Java implements run-time polymorphism.
Let’s begin by restating an important principle: a superclass reference variable can refer to a subclass object.
When an overridden method is called through a superclass reference, Java determines which version of that method to
execute based upon the type of the object being referred to at the time the call occurs. Thus, this determination is
made at run time.
In other words, it is the type of the object being referred to (not the type of the reference variable)
that determines which version of an overridden method will be executed.

If B extends A then you can override a method in A through B with changing the return type of method to B.

---

# Encapsulation and Abstraction:-
![r](images/AbstractionVsEncapsulation.png)
