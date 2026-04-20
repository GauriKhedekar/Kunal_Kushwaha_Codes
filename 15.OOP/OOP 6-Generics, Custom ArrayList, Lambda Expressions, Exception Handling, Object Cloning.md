# OOP 6:-
![o](images/oops_6.png)

---
# Custom ArrayList using Generics:-
## 🔹 What is Generics?
**Generics in Java** allow you to write **type-safe, reusable code** by specifying the **type of data** a class, interface, or method can work with **at compile time**.

---

## 🔹 Why Generics are Needed?
Before generics:
- Only `Object` type was used
- Required **type casting**
- Errors occurred at **runtime**

With generics:
- **Type safety**
- **No casting**
- **Compile-time error checking**
```java
package Generics;
import java.util.ArrayList;
import java.util.Arrays;
//Class which can only implement int datatype ArrayLists if we had declared all var as int ,hadn't even used <T>-> and for syntax -> CustomArrayList list = new CustomArrayList(); -> it was giving "Raw use of parameterized class 'CustomArrayList'" i.e. we can add ele. of any dtype in that array but should be of same dtype -> if we haven't used <T> while creating "CustomArrayList" class, but we have used Generics here i.e. <T> var to make ArrayList of any datatype which exists.
public class CustomArrayList<T>{
     private Object[] data;
     private static int DEFAULT_SIZE = 10;
     private int size = 0;//size var. is also working as index

     public CustomArrayList(){
         this.data = new Object[DEFAULT_SIZE];
     }

     public void add(T num){
         if(this.isFull()){
             resize();
         }
         data[size++] = (T)num;
     }

     private boolean isFull(){
         return size == data.length;
     }

     private void resize(){
         //Type parameter T can't be "instantiated" directly as byte code has no idea about type<T> hence at runtime it will get confuse,which datatype(class) of obj do you want me to create...
         //hence at RHS using 'T' is not allowed(T[] temp = new T[size * 2];) as on RHS we instantiate/call constructor of class we have declared but as byte code have no idea about 'T' but all the classes have idea about object class, hence we will use object over here
         //but elements in it would be of dataType <T>
         Object[] temp = new Object[size * 2];
         for(int i = 0; i < size; i++){
             temp[i] = (T)data[i];//casting ele. type to T
         }
         data = temp;//here data is now pointing to same array object pointed by temp(as given in above class notes),as resize() function finishes executing temp will go out of scope or removed bcoz of  block scope property;
     }

     public T remove(){
         T removed = (T) data[size--];//cast ele. to T to store it in T datatype var
         return removed;//it will return last element in an arrayList and while adding next element it(next ele.) will override previous last element and will place that last ele. on index where previous last ele. was placed,In this way we will remove last ele.when remove() will be called.
     }

     public int size(){
         return size;
     }

     public void set(int index, T value){
         data[index] = value;
     }

     public String toString(){
         return Arrays.toString(data);
     }
 public static void main(String[] args){
     CustomArrayList<Integer> list = new CustomArrayList();
     list.add(5);
     System.out.println(list);//[5, null, null, null, null, null, null, null, null, null],all the other elements are null as array is of type Object and default value of any object of Object class is null.
 }

}
```
# 📌 Wildcards in Java: are used in Java Generics to make code flexible.
e.g.
```java
//here T should either be number or its subclasses
public class CustomArrayList<T extends Number>{
 public void getList(List<? extends Number> list){
//do something

//here you can pass number as well as its subclasses but id you pass (List<Number> list) then you can pass Number dtype only and not its subclass(Integer/Float)
}
```
 # Comparing objects:-
 Comaparable<T> interface
 ```java
 public interface Comparable<T> {
    public int compareTo(T o);
}
```
Implementing Comaparble<T> interface:-
 ```java
 package Generics.Comparing;
//Comparable<T> is java's inbuilt interface(which comparable interface with generic type)
//to compare objects of only Student dtype we have provided Generics of Student type
public class Student implements Comparable<Student>{
        int rollno;
        float marks;

        public Student(int rollno, float marks){
            this.rollno = rollno;
            this.marks = marks;
        }

        @Override//here var. name (i.e. o) of Student dtype should also be same as there in Comparable<T> method as to override a method we require same signature of parent Interface and child class methods(which we must over-ride).
        public int compareTo(Student o){
            //here if this.marks == o.marks it will return 0
            //if this.marks > o.marks then return +ve value
            //else return -ve value
            //or
            //if diff = 0; means both are equal
            //if diff < 0; means 'o' is bigger
            //else 'o' is smaller
           int diff = (int)(this.marks - o.marks);//Kunal.compareTo(Rahul)=>Kunal = main obj = hence this.marks will be replaced with Kunal.marks and o.marks will be replaced with Rahul.marks...
           return diff;
        }
}
```
Main class:-
```java
package Generics.Comparing;

public class Main {
    public static void main(String[] args){
        Student Kunal = new Student(45, 78.89f);
        Student Rahul = new Student(67, 89.99f);

        if(Kunal.compareTo(Rahul) < 0){
            System.out.println(Kunal.compareTo(Rahul));
            System.out.println("Rahul has more marks");
        }
    }
}
o/p:-
-11
Rahul has more marks
```
# For sorting array of Student class on the basis of marks
Student class for sorting array:-
```java
package Generics.Comparing;
//Comparable<T> is java's inbuilt interface(which comparable interface with generic type)
//to compare objects of only Student dtype we have provided Generics of Student type
public class Student implements Comparable<Student>{
        int rollno;
        float marks;

        public Student(int rollno, float marks){
            this.rollno = rollno;
            this.marks = marks;
        }

    @Override//if we want to compare both marks and roll number
    public String toString() {
        return marks + "";
    }

    @Override//here var. name (i.e. o) of Student dtype should also be same as there in Comparable<T> method as to override a method we require same signature of parent Interface and child class methods(which we must over-ride).
        public int compareTo(Student o){
            //here if this.marks == o.marks it will return 0
            //if this.marks > o.marks then return +ve value
            //else return -ve value
            //or
            //if diff = 0; means both are equal
            //if diff < 0; means 'o' is bigger
            //else 'o' is smaller
           int diff = (int)(this.marks - o.marks);//Kunal.compareTo(Rahul)=>Kunal = main obj = hence this.marks will be replaced with Kunal.marks and o.marks will be replaced with Rahul.marks...
           return diff;
        }
}
```
Main class for sorting array on the basis of marks:-
```java
package Generics.Comparing;

import java.util.Arrays;

public class Main {
    public static void main(String[] args){
       Student Kunal = new Student(45, 78.89f);
        Student Rahul = new Student(67, 89.99f);
        Student Yash = new Student(1, 90.3f);
        Student Gauri = new Student(33, 80.3f);

        Student[] list = new Student[]{Kunal, Rahul, Yash, Gauri};
        System.out.println(Arrays.toString(list));
        //to sort an array of type Student we require compareTo(T o) method in Student class to sort the elements by comparing.
        Arrays.sort(list);
        System.out.println(Arrays.toString(list));
        }
    }
o/p:-
[78.89, 89.99, 90.3, 80.3]
[78.89, 80.3, 89.99, 90.3]
```
# Sorting array directly in Main():-
- take student class as it is from above example.
- Below we have Comparator interface to Override in Main class:-
```java
package java.util;

public interface Comparator<T> {
    int compare(T o1, T o2);
}
```
- Below we have Main class-we won't use implements keyword,we will directly import Comparator interface using import keyword ->import java.util.Comparator;
```java
package Generics.Comparing;

import java.util.Arrays;
import java.util.Comparator;

public class Main {
    public static void main(String[] args){
        Student Kunal = new Student(45, 78.89f);
        Student Rahul = new Student(67, 89.99f);
        Student Yash = new Student(1, 90.3f);
        Student Gauri = new Student(33, 80.3f);

        Student[] list = new Student[]{Kunal, Rahul, Yash, Gauri};
        System.out.println(Arrays.toString(list));
//'list' is the array (or in this case, a List being treated as an array by the method)
// that we want to sort.
// The second argument is a custom Comparator that defines the sorting logic.
        Arrays.sort(list, new Comparator<Student>(){

            // @Override indicates that this method is overriding a method
            // from the Comparator interface.
            @Override
            // The compare method takes two Student objects (o1 and o2) as input
            // and returns an integer indicating their relative order.
            public int compare(Student o1, Student o2){

                // The return value determines the sort order:
                // If the result is negative, o1 comes before o2.
                // If the result is positive, o1 comes after o2.
                // If the result is zero, their order doesn't matter.

                // This specific logic (o1.marks - o2.marks) sorts the students
                // in ascending order of their marks.
                // Since the compare method expects an 'int' return type, we cast
                // the result of the subtraction to an integer.
                return (int)(o1.marks - o2.marks);
                //if we want to sort an array in descending order-> use->return -(int)(o1.marks - o2.marks);
            }
        });
        //or
        // Sorts the 'list' array of 'Student' objects using a concise lambda expression
        /* Arrays.sort(list, (o1, o2) -> (int)(o1.marks - o2.marks));=>this is konwn as lambda          expressio of above form*/

        System.out.println(Arrays.toString(list));
    }
}
o/p:-
[78.8945, 89.9967, 90.31, 80.333]
[78.8945, 80.333, 89.9967, 90.31]
```
# Lambda Expressions:-
# 📌 Java Lambda Expressions – 

This note is written **strictly based on your code** and explains:
- Lambda expressions
- `forEach()` working
- `Consumer` interface
- Custom functional interfaces (`Sum`, `Operation`)
- How lambda connects to interface methods
- Doubts explained clearly (with comments-style explanations)

---

## 🔹 What is a Lambda Expression?

A **lambda expression** is a **short form of writing a method** without:
- method name
- return type
- access modifier
- Lambda expression = implementation of a functional interface’s single abstract method in a compact form.
👉 Used **only with Functional Interfaces**.

### 📌 Functional Interface
An interface that has **exactly one abstract method**.

Examples:
- `Consumer<T>`
- `Comparator<T>`
- Your `Sum`
- Your `Operation`

---

## 🔹 General Syntax of Lambda Expression

```java
(parameters) -> expression
```
OR
```java
(parameters) -> {
    // body
}
```
🔁 Conversion Rule (Very Important)
Interface method:
```java
int sum(int a, int b);
```
Lambda expression:
```java
(a, b) -> a + b;
```
- 👉 Method name is ignored
- 👉 Return type is inferred
- 👉 Only parameters + body matter

🔹 Why Lambda Works Only with Interfaces?
Because:

- Lambda expression provides implementation for the single abstract method of an interface.

- JVM knows which method to attach the lambda body to.

🔹 Your Code Explained Line by Line
- 1️⃣ forEach() Method – How it Works
```java
arr.forEach((item) -> System.out.println(item * 2));
```
- ❓ From where does forEach() come?
- forEach() is a default method of Iterable interface.
  
```java
public interface Iterable<T> {
    default void forEach(Consumer<? super T> action) {
        for (T t : this) {
            action.accept(t);
        }
    }
}
```
- ✔ ArrayList implements Iterable
- ✔ So ArrayList gets forEach() automatically

🔹 Consumer Interface Explained
```java
Consumer<Integer> fun = (item) -> System.out.println(item * 2);
```
📌 Consumer Interface Definition
```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```
🔁 Mapping
- Interface Method => accept(T t)
- Lambda	=> (item) -> System.out.println(item * 2)

👉 Lambda body becomes the implementation of accept()

🔹 Way 1 vs Way 2 (Same Logic):-
```java
arr.forEach((item) -> System.out.println(item * 2));
```
```java
Consumer<Integer> fun = (item) -> System.out.println(item * 2);
arr.forEach(fun);
```
- ✔ Both call accept(item)
- ✔ Difference is storage vs direct usage

🔹 Custom Functional Interface: Sum
```java
interface Sum {
    int sum(int a, int b);
}
```
Lambda Conversion
```java
Sum sum = (a, b) -> a + b;
```
📌 JVM mapping:
```java
int sum(int a, int b) {
    return a + b;
}
```
🔹 Custom Calculator Using Operation:
Interface
```java
interface Operation {
    int operation(int a, int b);
}
```
In Main class's -> main()
```java
Operation add  = (a, b) -> a + b;
Operation prod = (a, b) -> a * b;
Operation sub  = (a, b) -> a - b;
```
- ✔ Each lambda gives different behavior
- ✔ Same interface → multiple implementations

🔹 How operate() Method Works (IMPORTANT FLOW)
```java
private int operate(int a, int b, Operation op) {
    return op.operation(a, b);
}
```
📌 Call Example
```java
myCalculator.operate(5, 8, add);
```
🔁 Flow:
- operate(5, 8, add) is called
- op now refers to add

JVM calls:

```java
add.operation(5, 8)
```
Lambda body runs:

```java
(a, b) -> a + b
```
Result returned

🔹 Important Comment from Your Code (Explained)
```java
// name is not imp. in Lambda expressions
// only parameters and body of the method matters
```
✔ Correct because:

- Lambda does not care about method name

- JVM maps it automatically to the single abstract method

🔹 Doubt 1: How can Interface & Class be in Same File?
```java
public class LambdaFunctions { ... }
interface Sum { ... }
interface Operation { ... }
```
✅ Allowed because:
- Java allows multiple non-public interfaces/classes in one file

- Only one public class

- File name must match public class name

🔹 Why sum() Method Is NOT Overridden?
```java
int sum(int a, int b){
    return a + b;
}
```
- ✔ This is a normal method
- ❌ Not overridden because:

- LambdaFunctions does NOT implement Sum

- No implements Sum

To override:
```java
class LambdaFunctions implements Sum {
    public int sum(int a, int b) {
        return a + b;
    }
}
```
# My Code to understand Lambda Expressions:-can read if you didn't understand above notes otherwise leave it
```javapackage Generics.Comparing;
import java.util.ArrayList;
import java.util.function.Consumer;

public class LambdaFunctions {
    public static void main(String[] args){
     ArrayList<Integer> arr = new ArrayList<>();
     for(int i = 0; i < 5; i++){
         arr.add(i + 1);
     }
     //Way 1:-
     arr.forEach((item) -> System.out.println(item * 2));
     //Way 2:- We can store lambda expression in a variable as well.
     Consumer<Integer> fun = (item) -> System.out.println(item * 2);
     arr.forEach(fun);
     //Sum =>Interface name
        //Give syntax of conversion of interface type + method into Lambda expression.
     Sum sum = (a, b) -> a + b;//here we have converted int sum(int a, int b){return a + b;} into Lambda expression
     //Creating calculator below
     Operation add = (a, b) -> a + b;
     Operation prod = (int a, int b) -> a * b;
     Operation sub = (int a, int b) -> a - b;

     LambdaFunctions myCalculator = new LambdaFunctions();
     System.out.println(myCalculator.operate(5, 8, add));//a = 5, b = 8, op = sum;
        System.out.println(myCalculator.operate(5, 8, prod));
        System.out.println(myCalculator.operate(5, 8, sub));
    }

    //How will you call methods created of type Operation
    private int operate(int a, int b, Operation op){
        //add.operation(a, b) -> will give answer as (a + b)
        //int operation(int a, int b); is an abstract method in an Interface.
        return op.operation(a, b);//name is not imp. in Lambda expressions only parameters and body of the method matters...
    }


    //here sum() is not an over-ridden method as Main function is not a subclass of any class/subclass of any interface
    int sum(int a, int b){
        return a + b;
    }
}

interface Sum{//doubt 1:-how can we create interface and class in same file?
    int sum(int a, int b);
}

interface Operation{
    int operation(int a, int b);
}
//flow of Operation thing,when you call myCalculator.operate(5, 8, add) it will call operate() then it will call op.operation(a, b) which is an abstract method in an interface -> then it will look for its body so it will go to Operation add = (a, b) -> a + b; -> and it will return a + b
o/p:-
2
4
6
8
10
2
4
6
8
10
13
40
-3
```
---
# 📌 Java Exception Handling :


## 🔹 What is an Exception?
An **exception** is an **abnormal condition** that occurs during the execution of a program and disrupts its normal flow.

Most exceptions occur at **runtime**, but some are **checked at compile time** (called checked exceptions).

Examples:
- Dividing by zero (runtime exception)
- Invalid input (runtime exception)
- File not found (compile-time checked exception)
- 
# 1️⃣ try–catch–finally (Using Your First Code)

### 📌 Syntax
```java
try {
    // risky code
}
catch(ExceptionType e) {
    // handling code
}
finally {
    // cleanup code
}
```
🔹 try Block
```java
try {
    divide(a, b);
}
```
✔ Contains code that may cause an exception
✔ Must be followed by catch or finally

🔹 catch Block
```java
catch(ArithmeticException e) {
    System.out.println(e.getMessage());
}
```
- ✔ Handles the exception thrown in try
- ✔ e.getMessage() prints the error message

🔹 finally Block
```java
finally {
    System.out.println("This will always execute");
}
```
- ✔ Executes always
- ✔ Used for:

closing files,

releasing resources,

cleanup code.

🔹 divide() Method Explanation
```java
static int divide(int a, int b) throws ArithmeticException {
    if (b == 0) {
        throw new ArithmeticException("Please do not divide by 0");
    }
    return a / b;
}
```
- ✔ ArithmeticException is an unchecked exception
- ✔ throw is used to manually raise an exception
- ✔ throws declares a possible exception

🔒 More Restrictive vs Less Restrictive Exceptions
- More Restrictive	-> ArithmeticException	-> Handles specific error
- Less Restrictive	-> Exception -> Handles all exceptions

⚠️ Catch Order Rule (Very Important)
```java
catch(ArithmeticException e) { }  // FIRST
catch(Exception e) { }            // LAST
```
- ✔ Always catch specific exceptions first
- ✔ Generic exceptions (Exception) must be last

2️⃣ Custom Exception (Using Your Second Code)
🔹 Creating Custom Exception
```java
public class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}
```
- ✔ Exception → checked exception
- ✔ super(message) sends message to parent class

🔹 Throwing Custom Exception
```java
if (name.equals("Gauri")) {
    throw new MyException("Name is Gauri");
}
```
- ✔ throw creates and raises custom exception

🔹 Catching Custom Exception
```java
catch (MyException e) {
    System.out.println(e.getMessage());
}
```
- ✔ Must be handled using try–catch
- ✔ Should be caught before Exception

🔹 Full Catch Order Used
```java
catch (MyException e)        // most specific
catch (ArithmeticException e)
catch (Exception e)         // most general
```
- ✔ Correct order
- ✔ Prevents unreachable code

🧠 Key Differences
- throw ->	Used to explicitly throw exception
- throws	-> Declares possible exception
- Checked Exception	-> Must be handled (Exception)
- Unchecked Exception -> Optional handling (RuntimeException)
### My code to understand Exception Handling:-can read or leave
```java
//code 1:-MyException.java
package ExceptionHandling;

public class MyException extends Exception{
    public MyException(String message){
        super(message);//to get standard Exception msg from Exception class
    }
}

//code 2:-Main.java
package ExceptionHandling;

public class Main {
    public static void main(String[] args){
        //unchecked exception example
        int a = 8;
        int b = 9;
        try {

            String name = "Gauri";
            if(name.equals("Gauri")){
                throw new MyException("Name is Gauri");
            }
        }
        catch (MyException e) {
            System.out.println(e.getMessage());
        }
        catch (ArithmeticException e) {
            System.out.println(e.getMessage());
        }
        catch (Exception e) {
            System.out.println("Normal Exception");
        }
        finally{
            System.out.println("This will always execute");
        }
    }

}
o/p:-
Name is Gauri
This will always execute
```
---

# Object Cloning:-
```java
// ======================= 1) OBJECT CLONING =======================
// package Cloning;
//
// Object Cloning means creating an exact copy of an existing object.
// Java provides clone() method (from Object class) for this purpose.
// To allow cloning, a class MUST implement the Cloneable interface,
// otherwise JVM throws CloneNotSupportedException.

package Cloning;

// Even though Cloneable interface has no methods,
// implementing it tells JVM that cloning is allowed for this class.
public class Human implements Cloneable {
    int age;
    String name;

    // Normal constructor
    public Human(int age, String name) {
        this.age = age;
        this.name = name;
    }

    // Copy constructor (manual way of copying object)
    // This creates a new object and copies data field-by-field.
    public Human(Human other) {
        this.age = other.age;
        this.name = other.name;
    }

    // Overriding clone() method of Object class
    // super.clone() creates a field-by-field copy of the object
    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone(); // shallow copy by default
    }
}
```
```java
package Cloning;

// Main class to test object cloning
public class Main {
    // If clone() throws an exception, caller must handle or declare it
    public static void main(String[] args) throws CloneNotSupportedException {

        Human Gauri = new Human(60, "Gauri Khedekar");

        // Instead of using copy constructor:
        // Human twin = new Human(Gauri);

        // We use clone() to create a copy
        Human twin = (Human) Gauri.clone();

        // Both objects have same data but are different objects
        System.out.println(twin.age + " " + twin.name);
    }
}
```
```java
// ======================= 2) SHALLOW COPY =======================
// Shallow copy copies:
// - primitive data types (actual values)
// - reference data types (only reference, not the object itself)

package Cloning;

public class Human implements Cloneable {
    int age;
    String name;
    int[] arr; // non-primitive (reference type)

    public Human(int age, String name) {
        this.age = age;
        this.name = name;
        this.arr = new int[]{3, 7, 8, 7};
    }

    // Default clone() creates a shallow copy
    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone(); // primitives copied, references shared
    }
}
```
```java
package Cloning;

import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {

        Human Gauri = new Human(60, "Gauri Khedekar");

        // twin is a shallow copy of Gauri
        Human twin = (Human) Gauri.clone();

        System.out.println(twin.age + " " + twin.name);
        System.out.println(Arrays.toString(twin.arr));

        // Modifying array of twin
        twin.arr[0] = 100;

        // Gauri.arr is ALSO changed because both point to same array
        // This happens because shallow copy copies references only
        System.out.println(Arrays.toString(Gauri.arr));
    }
}
```
```java
// ======================= 3) DEEP COPY =======================
// Deep copy copies:
// - primitive data types
// - AND creates a new copy of referenced objects
// So changes in cloned object do NOT affect original object.

package Cloning;

public class Human implements Cloneable {
    int age;
    String name;
    int[] arr;

    public Human(int age, String name) {
        this.age = age;
        this.name = name;
        this.arr = new int[]{3, 7, 8, 7};
    }

    @Override
    public Object clone() throws CloneNotSupportedException {

        // First create shallow copy
        Human twin = (Human) super.clone();

        // Then manually copy non-primitive fields
        // This ensures deep copy
        twin.arr = new int[this.arr.length];
        for (int i = 0; i < this.arr.length; i++) {
            twin.arr[i] = this.arr[i];
        }

        return twin;
    }
}
```
```java
package Cloning;

import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {

        Human Gauri = new Human(60, "Gauri Khedekar");

        // twin is a deep copy
        Human twin = (Human) Gauri.clone();

        System.out.println(twin.age + " " + twin.name);
        System.out.println("Previous twin: " + Arrays.toString(twin.arr));

        // Modify twin's array
        twin.arr[0] = 100;

        // Only twin changes, original remains unchanged
        System.out.println("Modified twin: " + Arrays.toString(twin.arr));
        System.out.println("Gauri array: " + Arrays.toString(Gauri.arr));
    }
}
```
#### Quick Summary (from comments logic):
- clone() → creates copy of object
- Default clone() → shallow copy
- Primitives → copied
- References → shared
- Deep copy → manually clone referenced objects
- Cloneable → marker interface to allow cloning
---
