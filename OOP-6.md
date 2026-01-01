# Custom ArrayList using Generics
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
 
