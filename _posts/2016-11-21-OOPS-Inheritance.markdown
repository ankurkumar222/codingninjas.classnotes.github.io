---
layout: post
title:  "Inheritance & Generics"
date:   2016-10-24 06:08:02 +0530
---
# Multiple Inheritance
When one class has more than one super classes then it is called multiple
inheritance.
For e.g.
Teacher Student
TA
Here a TA is both a teacher and a student, it has two parent classes.
Java doesn’t allow multiple inheritence.

### Interfaces
Interfaces in java are pure abstract i.e all methods in an interface are public and
abstract and fileds are public, final and static by default. E.g :
~~~java
public interface VehicleInterface {
    int a = 9;
    public String getType();
}
~~~
A class “implements” an interface. And a class implementing a interface must
implement all its methods otherwise the class will have to be declared abstract.
Also a class can implement multiple interfaces and if it does so then it will have to
implement all the methods in the interfaces that it is implementing.
~~~java
public class Car extends Vehicle implements VehicleInterface{
  int numDoors;
  double mileage;
  public Car(double price){
      super(price);
      numWheels = 4;
      company = "";
  }
  @Override
  public String getType() {
      return "Car";
  }
}
~~~
Thus interfaces serve as a contract, If a non abstract class is implemeting an
interface then without looking into the code of the class we can be sure that the
class must have implemented the methods in the interface, else the class would
have been abstract.

#### Some points about interface :
* We cannot instantiate an interface.
* An interface does not contain any constructors.
* All of the methods in an interface are abstract.
* An interface cannot contain instance fields i.e non static fields. The only fields
that can appear in an interface must be declared both static and final.
* An interface is not extended by a class; it is implemented by a class.
* An interface can extend multiple interfaces.

We can achieve runtime polymorphism in the same manner as discussed above for
classes.
~~~java
VehicleInterface v = new Car(1000);
System.out.println(v.getType());
System.out.println(v.a);
System.out.println(v.numDoors); // error
~~~

# Generics
Suppose we make a pair class to store two ints.
~~~java
public class Pair {
    int first;
    int second;
}
~~~
Now if we want to have a pair of two chars/strings/double then we will have t
create separate pair classes for each of them. Generics allow us to create a single
Pair class that will work for different types.
Creating a generic class
Syntax of a generic Pair class is :
~~~java
 public class Pair<T> {
    T first;
    T second;
 }
~~~
Here <T> represents the type parameter and “T” is an identifier that specifies a
generic type name, it could have been any other letter.
Now if we want to have pair of two ints, then syntax will be :
~~~java
Pair<Integer> pInts = new Pair<Integer>();
Pair<String> pStrings = new Pair<Strings>(); // Pair of two
 // Strings
~~~
Note that type parameters can represent only reference types, not primitive types.
So for primitives int,char etc java has corressponding Wrapper classes Integer,
Character etc.
A Java compiler applies strong type checking to generic code and issues errors if
the code violates type safety
#### Multiple Type Parameters  ####
We can have multiple type parameters as well i.e we can create a pair class where
“first” and “second” can be of different types unlike the Pair class defined above
where both have to be of same type.
~~~java
public class Pair<T,S> {
    T first;
    S second;
}
~~~
Its instance can be created as follows :
~~~java
Pair<Integer,String> pair = new Pair<Integer, String>();
~~~
So here pair.first is a Integer and pair.second is a String.
Multilayer Generic Parameters
The genric parameters can be multiplayered.
~~~java
Pair<Pair<Integer>> pLayered = new Pair<>();
~~~
Here pLayered.first and pLayered.second are themselves pair of Integers.
Similarly we can add multiple layers to the parameters.
Generic Methods
Just like we saw generic classes above, we can make methods also accept generic
parameters. We can make a method generic even when the class isn’t generic.
Here is a sample printArray method that works for generic inputs.
~~~java
public static<T> void printArray(T input[]){
    for(int i = 0; i < input.length; i++){
        System.out.print(input[i] +" ");
    }
}
~~~
### Bounded Type Parameters:
Many a times when you might want to restrict the kinds of types that are allowed
to be passed to a type parameter. Say we want to create a generic sort function.
In order to sort elements we will have to compare them. The “<” or “>” are not
defined for non–primitives. So instead we will have to use compareTo() method
(in Comparable interface) which compares two objects and returns an int based
on result.
Now in our sort function we should allow only those non-primitives who have
compareTo() method defined for them or in other terms who have implemented
the Comparable interface (as interface serves as a contract, so if a non-abstract
class has implemeted has implemented Comparable method then we can be sure
that it has compareTo() method ). We can do this as shown below :
~~~java
public static<T extends Comparable<T>> void sort(T input[]){
    T temp;
    for(int i = 0; i < input.length; i++){
        for(int j = 0; j < input.length - i - 1; j++){
            if(input[j].compareTo(input[j+1])==1){
                temp = input[j+1];
                input[j+1] = input[j];
                input[j] = temp;
            }
        }
    }
}
~~~
When we write <T extends Comparable<T>> this means that only those
parameters are allowed those who have implemented Comparable Interface.
