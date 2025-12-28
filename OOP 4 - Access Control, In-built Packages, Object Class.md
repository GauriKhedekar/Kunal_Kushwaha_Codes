# 🔐 Access Modifiers in Java:-
Access Control:

How a member can be accessed is determined by the access modifier attached to its declaration.
Usually, you will want to restrict access to the data members of a class—allowing access only through methods.
Also, there will be times when you will want to define methods that are private to a class.

Java’s access modifiers are public, private, and protected. Java also defines a default access level.
protected applies only when inheritance is involved.

When no access modifier is used, then by default the member of a class is public within its own package,
but cannot be accessed outside of its package.
```java
            │ Class │ Package │ Subclass │ Subclass │ World
            │       │         │(same pkg)│(diff pkg)│(diff pkg & not subclass)
────────────┼───────┼─────────┼──────────┼──────────┼──────────────────────────
public      │   +   │    +    │    +     │     +    │   +
────────────┼───────┼─────────┼──────────┼──────────┼──────────────────────────
protected   │   +   │    +    │    +     │     +    │
────────────┼───────┼─────────┼──────────┼──────────┼──────────────────────────
no modifier │   +   │    +    │    +     │          │
────────────┼───────┼─────────┼──────────┼──────────┼──────────────────────────
private     │   +   │         │          │          │

+ : accessible
blank : not accessible
```
```java
package packageOne;
public class Base
{
    protected void display(){
        System.out.println("in Base");
    }
}
```
```java
package packageTwo;
public class Derived extends packageOne.Base{
    public void show(){
        new Base().display();       // this is not working
        new Derived().display();    // is working
        display();//is working
    }
}
```
protected allows access from subclasses and from other classes in the same package.
We can use child class to use protected member outside the package but only child class object can access it.
That's why any Derived class instance can access the protected method in Base.
The other line creates a Base instance (not a Derived instance!!).
And access to protected methods of that instance is only allowed from objects of the same package.

display();
-> allowed, because the caller, an instance of Derived has access to protected members and fields of its subclasses,
even if they're in different packages


new Derived().display();
-> allowed, because you call the method on an instance of Derived and that instance has access to the protected methods
of its subclasses

new Base().display();
-> not allowed because the caller's (the this instance) class is not defined in the same package like the Base class,
so this can't access the protected method. And it doesn't matter - as we see - that the current subclasses a class from
that package. That backdoor is closed ;)

Remember that any time talks about a subclass having an access to a superclass member, we could be talking about the
subclass inheriting the member, not simple accessing the member through a reference to an instance of the superclass.

```java
class C{
    protected member;
}
```
// in a different package
```java
class S extends C{

    obj.member; // only allowed if type of obj is S or subclass of S
}
```
The motivation is probably as following. If obj is an S, class S has sufficient knowledge of its internals,
it has the right to manipulate its members, and it can do this safely.
If obj is not an S, it's probably another subclass S2 of C, which S has no idea of.
S2 may have not even been born when S is written. For S to manipulate S2's protected internals is quite dangerous.
If this is allowed, from S2's point of view, it doesn't know who will tamper with its protected internals and how,
this makes S2 job very hard to reason about its own state.

Now if obj is D, and D extends S, is it dangerous for S to access obj.member? Not really.
How S uses member is a shared knowledge of S and all its subclasses, including D. S as the superclass has the right to
define behaviours, and D as the subclass has the obligation to accept and conform.

For easier understanding, the rule should really be simplified to require obj's (static) type to be exactly S.
After all, it's very unusual and inappropriate for subclass D to appear in S. And even if it happens,
that the static type of obj is D, our simplified rule can deal with it easily by upcasting: ((S)obj).member

# 📦 Packages in Java
Types:
- User-defined packages
- In-built packages

Common In-built Packages
- java.lang:
Automatically imported,
Contains:
Object, String, Math, Wrapper classes
- java.io:
Input / Output operations
,Files, streams
- java.util:
Data structures & utilities,ArrayList, HashMap, Scanner, Collections
- java.applet (Deprecated):
Applet-based programs
- java.awt:
GUI components, Buttons, Frames
-java.net:
Networking, Internet connection
,URL, sockets

## 🧬 Object Class (`java.lang`)

### 🔹 Basic Facts
- `Object` is the **parent of all Java classes**
- Every class **implicitly extends `Object`**

```java
class A { }   // internally: class A extends Object

🔑 Important Object Class Methods
1️⃣ toString()
Returns string representation of an object 
Default format of which is this : ClassName@HexHashCode
class Student {
    int id = 1;
}
->In main()
Student s = new Student();
System.out.println(s);   // Student@3feba861
->
Overriding toString():created by user
class Student {
    int id = 1;

    public String toString() {
        return "ID = " + id;
    }
}

2️⃣ hashCode()
Returns an integer value representing an object
Used in hash-based collections (HashMap, HashSet)
Equal objects must have same hashCode

Student s1 = new Student();
Student s2 = new Student();

System.out.println(s1.hashCode());
System.out.println(s2.hashCode());

📌 Important Rule:
If equals() is overridden, hashCode() must also be overridden
Reason:
Hash-based collections first compare hashCode(), then equals()

3️⃣ equals(Object obj)
Default equals() compares references
To compare content, we create our own equals() method (override)

class Student {
    int id;

    // Custom equals() method
    public boolean equals(Object obj) {
        Student s = (Student) obj;
        return this.id == s.id;
    }
}

Student s1 = new Student();
Student s2 = new Student();

s1.id = 10;
s2.id = 10;

System.out.println(s1.equals(s2));  // true (content compared)

4️⃣ == Operator
Compares references, not content

Student s1 = new Student();
Student s2 = new Student();

System.out.println(s1 == s2);   // false

5️⃣ instanceof
Checks object type at runtime
Helps avoid ClassCastException

Object obj = new Student();

if (obj instanceof Student) {
    System.out.println("Student object");
}

6️⃣ getClass()
Returns runtime class information
Class metadata is stored in heap memory

Student s = new Student();
System.out.println(s.getClass());

// Output: class com.kunal.access.Student

🧠 Combined equals() + hashCode() (Correct Practice)
class Student {
    int id;

    public boolean equals(Object obj) {
        Student s = (Student) obj;
        return this.id == s.id;
    }

    public int hashCode() {
        return id;
    }
}
```
