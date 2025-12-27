# Packages:-
Packages are containers for classes. They are used to keep the class name space compartmentalized.
For example, a package allows you to create a class named List, which you can store in your own package without
concern that it will collide with some other class named List stored elsewhere. Packages are stored in a hierarchical
manner and are explicitly imported into new class definitions.

The package is both a naming and a visibility control mechanism.

The following statement creates a package called MyPackage: package MyPackage;

Java uses file system directories to store packages. For example, the .class files for any classes you declare to be
part of MyPackage must be stored in a directory called MyPackage. Remember that case is significant, and the directory
name must match the package name exactly.

A package hierarchy must be reflected in the file system of your Java development system.
For example, a package declared as

    package java.awt.image;

needs to be stored in java\awt\image in a Windows environment. Be sure to choose your package names carefully.
You cannot rename a package without renaming the directory in which the classes are stored.

How does the Java run-time system know where to look for packages that you create? The answer has three parts.
- First, by default, the Java run-time system uses the current working directory as its starting point.
Thus, if your package is in a subdirectory of the current directory, it will be found.
- Second, you can specify a directory path or paths by setting the CLASSPATH environmental variable.
- Third, you can use the -classpath option with java and javac to specify the path to your classes.

When a package is imported, only those items within the package declared as public will be available to non-subclasses
in the importing code.

---
# Static Keyword:-
Understanding static:

When a member is declared static, it can be accessed before any objects of its class are created,
and without reference to any object. You can declare both methods and variables to be static.
The most common example of a static member is main( ).
main( ) is declared as static because it must be called before any objects exist.
Static method in Java is a method which belongs to the class and not to the object.

A static method can access only static data. It cannot access non-static data (instance variables)
A non-static member belongs to an instance. It's meaningless without somehow resolving which instance of a class you
are talking about. In a static context, you don't have an instance, that's why you can't access a non-static member
without explicitly mentioning an object reference.
In fact, you can access a non-static member in a static context by specifying the object reference explicitly :
public class Human {

    String message = "Hello World";

    public static void display(Human human){
        System.out.println(human.message);
    }

    public static void main(String[] args) {
        Human kunal = new Human();
        kunal.message = "Kunal's message";
        Human.display(kunal);
    }

}

A static method can call only other static methods and cannot call a non-static method from it.
A static method can be accessed directly by the class name and doesn’t need any object
A static method cannot refer to "this" or "super" keywords in anyway

If you need to do computation in order to initialize your static variables,
you can declare a static block that gets executed exactly once, when the class is first loaded.

// Demonstrate static variables, methods, and blocks.
     class UseStatic {
       static int a = 3;
       static int b;
       static void meth(int x) {
         System.out.println("x = " + x);
         System.out.println("a = " + a);
         System.out.println("b = " + b);
       }
       static {
         System.out.println("Static block initialized.");
         b = a * 4;
        }
       public static void main(String args[]) {
         meth(42);
    }
}

As soon as the UseStatic class is loaded, all of the static statements are run. First, a is set to 3,
then the static block executes, which prints a message and then initializes b to a*4 or 12. Then main( ) is called,
which calls meth( ), passing 42 to x. The three println( ) statements refer to the two static variables a and b,
as well as to the local variable x.

Here is the output of the program:
Static block initialized. x = 42
a = 3
b = 12
Note: main method is static, since it must be accessible for an application to run, before any instantiation takes place.

NOTE: Only nested classes can be static.
NOTE: Static inner classes can have static variables

You cant override the inherited static methods, as in java overriding takes place by resolving the type of object at
run-time and not compile time, and then calling the respective method.
Static methods are class level methods, so it is always resolved during compile time.
Static INTERFACE METHODS are not inherited by either an implementing class or a sub-interface.

NOTE:
public class Static {

    // class Test  // ERROR
    static class Test{
        String name;

        public Test(String name) {
            this.name = name;
        }
    }

    public static void main(String[] args) {
        Test a = new Test("Kunal");

        Test b = new Test("Rahul");

        System.out.println(a.name); // Kunal
        System.out.println(b.name); // Rahul
    }
}
Because :
The static keyword may modify the declaration of a member type C within the body of a non-inner class or interface T.
Its effect is to declare that C is not an inner class. Just as a static method of T has no current instance of T in its
body, C also has no current instance of T, nor does it have any lexically enclosing instances.
Here, test does not have any instance of it's outer class Static. Neither does main.
But main & Test can have instances of each other.

---
# Singleton class:-
🔒 Singleton Class in Java
📌 What is a Singleton Class?

A Singleton class is a class that allows only ONE object (instance) to be created during the entire execution of a program.

👉 No matter how many times you try to create the object, the same single object is reused.

# 🧠 Real-Life Example

Printer → Only one printer spooler

Database Connection → Only one connection manager

Logger → One log file handler

#  How to Create a Singleton Class in Java
✅ Steps to create Singleton:

Make constructor private
→ So no one can create object using new

Create a private static object
→ Holds the single instance

Provide a public static method
→ Returns the same instance every time

# Java Codes of it:-
🧩 1️⃣ Eager Initialization (Simple & Common)
📌 Object created at class loading time
```java
class Singleton {

    // Step 1: private static instance
    private static Singleton instance = new Singleton();

    // Step 2: private constructor
    private Singleton() {
        System.out.println("Singleton object created");
    }

    // Step 3: public static method
    public static Singleton getInstance() {
        return instance;
    }
}
🔍 Usage:
public class Main {
    public static void main(String[] args) {

        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();

        System.out.println(s1 == s2); // true
    }
}
```

📌 Only one object is created

🧩 2️⃣ Lazy Initialization (Object created when needed)
📌 Object created only when requested
```java
class Singleton {

    private static Singleton instance;

    private Singleton() {
        System.out.println("Singleton object created");
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
✔ Saves memory
❌ Not thread-safe

🧩 3️⃣ Thread-Safe Singleton (Synchronized Method)
```java
class Singleton {

    private static Singleton instance;

    private Singleton() {}

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

```
✔ Thread safe
❌ Slower due to synchronization

🧩 4️⃣ Best Approach — Double Checked Locking
```java
class Singleton {

    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```
