# OOP 7:-
![p](images/oops_7.png)

---
# Collections Framework

- Java Collections Framework is a predefined architecture.
- It provides ready-made data structures.
- Helps store, manipulate, retrieve, and process data efficiently.
- Consists of:
- Interfaces
- Classes
- Algorithms
- Reduces programming effort.
- Ensures consistency across different data structures.

# Need of Collection Framework in Java

- Arrays have limitations:
- Fixed size
- No built-in methods for insertion, deletion, searching
- Different data structures were implemented separately earlier.
- Collection Framework provides:
- Standardization
- Reusability
- Common interfaces
- Same operations (add, remove, search) apply to all collections.
- Improves code maintainability and readability.

# Understanding Collection Framework
🔹 Core Interfaces
- Collection: Root interface.
- List: Ordered, allows duplicates.
- Set: Unordered, no duplicates
- Queue: FIFO-based processing
- Map: Key-value pairs (not part of Collection interface)

🔹 Key Characteristics
- Dynamic resizing
- Multiple implementations for different needs
- Interfaces define behavior
- Classes define implementation

🔹 Advantages
- Faster development
- Optimized performance
- Reduced coding errors
- Unified architecture

#### Vector Class:-
- Vector is a legacy class.
- Present since Java 1.0.
- Implements List interface.
- Uses dynamic array internally.
- Allows duplicate elements.

##### Vector Synchronization
- Vector is synchronized by default.(i.e.only one thread can access object of type vector at a time.but if 2 threads want to access same obj vector type obj. then while first thread is working on the obj other one have to wait to access that obj)
- Thread-safe(synchronized): multiple threads can access safely.
- Every method of vaector is synchronized.
- Leads to performance overhead.
- Slower compared to ArrayList.

– Vector Code Example
```java
import java.util.Vector;


class Test {
    public static void main(String[] args) {
        Vector<Integer> v = new Vector<>();
        v.add(10);
        v.add(20);
        v.add(30);
        System.out.println(v);
    }
}
```
- Demonstrates object creation and insertion.
- Vector maintains insertion order.
- If you are not dealing with multi-threading applications then use an ArrayList/List to reduce time complexity/performance overhead.

### Enums in Java
- Enum = fixed set of constants or group of variables which you can't change(it's like a constant)
- Used when values are predefined.
- Improves type safety.
```java
🔹 Example
enum Day {
    MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```
🔹 Why Enums?
- Replaces integer constants
- More readable and maintainable
- Compile-time checking

##### Enum Inheritance
- Enums cannot extend other classes.
- Enums implicitly extend java.lang.Enum.
- Multiple inheritance is not allowed.
- Enums can implement interfaces.

🔹 Key Rules
- Enum constructors are private.
- Enum constants are public, static, final.
- Enum values are created internally by JVM.

---

# Enums in Java:-
An enumeration is a list of named constants.
In Java, an enumeration defines a class type.
By making enumerations into classes, the capabilities of the enumeration are greatly expanded.

An enumeration is created using the enum keyword.
Enum declaration can be done outside a Class or inside a Class but not inside a Method
We can declare main() method inside enum. Hence we can invoke enum directly from the Command Prompt.

/* internally above enum Color is converted to (Check Example.java)
class Color
{
     public static final Color Red = new Color();
     public static final Color Blue = new Color();
     public static final Color Green = new Color();
}*/

Enum and Inheritance :
-All enums implicitly extend java.lang.Enum class. As a class can only extend one parent in Java,
so an enum cannot extend anything else.
-An enum cannot be a superclass.
-toString() method is overridden in java.lang.Enum class, which returns enum constant name.
-enum can implement many interfaces at the same time.(so that you can over-ride methods in an interface in enum which is implementing that interface)

Two enumeration constants can be compared for equality by using the == relational operator.

values(), ordinal() and valueOf() methods :
These methods are present inside java.lang.Enum.
-values() method can be used to return all values present inside enum.
-Order is important in enums.By using ordinal() method, each enum constant index can be found,
just like array index.
-valueOf() method returns the enum constant of the specified string value, if exists.(e.g. Week.valueOf("Monday")=>o/p=>Monday)

enum and constructor :
-enum can contain constructor and it is executed separately for each enum constant at the time
of enum class loading.
-We can’t create enum objects explicitly and hence we can’t invoke(call) enum constructor directly.(instantiate means call a constructor)
-And the constructor cannot be the public or protected it must have private or default modifiers.
-Why? if we create public or protected, it will allow initializing more than one objects.
-This is totally against enum concept.

enum and methods :
enum can contain concrete methods only i.e. no any abstract method.

You can compare for equality an enumeration constant with any other object by using equals( ),
which overrides the equals( ) method defined by Object.
Although equals( ) can compare an enumeration constant to any other object, those two objects
will be equal only if they both refer to the same constant,within the same enumeration.
Simply having ordinal values in common will not cause equals( ) to return true if the two constants
are from different enumerations. Remember, you can compare two enumeration references for equality by using ==.

# MyCode for Enum :-
```java
package Cloning;

public class Enum {

    // Enum declaration
    enum Week {

        // These are enum constants
        Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday;

        /*
         * IMPORTANT ENUM PROPERTIES:
         * --------------------------------
         * 1. Every enum type (Week) is implicitly:
         *    - public
         *    - static
         *    - final
         *
         * 2. Every enum constant (Monday, Tuesday, ...) is implicitly:
         *    - public
         *    - static
         *    - final
         *
         * 3. The type of each constant is the enum itself.
         *    Example:
         *      Monday is of type Week
         */

        /*
         * Enum Constructor
         * ----------------
         * - Enum constructors are ALWAYS:
         *      private or default (implicitly private)
         * - You CANNOT make them public or protected.
         *
         * WHY?
         * ----
         * Because enum objects are NOT created by the programmer.
         * JVM creates all enum constants internally.
         * Allowing public constructors would allow creation of new objects,
         * which breaks the idea of a fixed set of constants.
         */
        Week() {
            System.out.println("Constructor called for " + this.toString());
        }

        /*
         * WHAT DOES THIS MEAN INTERNALLY?
         * --------------------------------
         * When you write:
         *
         * enum Week { Monday, Tuesday }
         *
         * The compiler internally converts it roughly into:
         *
         * public final class Week extends java.lang.Enum<Week> {
         *
         *     public static final Week Monday = new Week();
         *     public static final Week Tuesday = new Week();
         *
         *     private Week() { }
         * }
         *
         * So:
         * - Each enum constant is a STATIC FINAL object
         * - Objects are created ONCE when the enum class is loaded
         * - That is why constructors run for ALL constants together
         */

        /*
         * ABSTRACT METHODS IN ENUM?
         * -------------------------
         * - Enums are implicitly final
         * - Final methods cannot be overridden
         * - Hence abstract methods generally don't make sense in enums
         *   (unless each constant provides its own implementation)
         */
    }

    public static void main(String[] args) {

        // Declaring a reference of enum type
        Week week;

        /*
         * Accessing ONE enum constant
         * ----------------------------
         * Even though we access only Week.Monday,
         * ALL enum constants are created when the enum class loads.
         */
        week = Week.Monday;

        /*
         * OUTPUT (constructor calls):
         * ----------------------------
         * Constructor called for Monday
         * Constructor called for Tuesday
         * Constructor called for Wednesday
         * Constructor called for Thursday
         * Constructor called for Friday
         * Constructor called for Saturday
         * Constructor called for Sunday
         */

        // Prints the enum constant
        System.out.println(week);
        // Output:
        // Monday

        /*
         * ordinal()
         * ----------
         * Returns the position of the enum constant
         * Index starts from 0
         */
        System.out.println(week.ordinal());
        // Output:
        // 0

        /*
         * values()
         * --------
         * Returns an array of all enum constants
         */
        for (Week day : Week.values()) {
            System.out.println(day);
        }
        /*
         * Output:
         * Monday
         * Tuesday
         * Wednesday
         * Thursday
         * Friday
         * Saturday
         * Sunday
         */

        /*
         * valueOf(String name)
         * --------------------
         * Converts String into corresponding enum constant
         * Must match EXACT name (case-sensitive)
         */
        System.out.println(Week.valueOf("Monday"));
        // Output:
        // Monday
    }
}
```
---
