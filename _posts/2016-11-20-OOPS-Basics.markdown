---
layout: post
title:  "OOPS fundamentals"
date:   2016-10-19 06:08:02 +0530
---
Topic :	Object	Oriented	Programming
### Objects ###
Objects are the real world entities about which we code. Objects have
properties and they perform functions. For example in a student management system the real world entities about which the system revolves are – students, instructor, course, batch etc.

### A Class ###
Class is a template or a blue print and the objects are specific copies of it. For example a Vehicle class might look like :
~~~java
public class Vehicle {
    public String brand;
    protected String model;
    private double price;
    int numWheels;
    int yearOfManufactor;
    String color;
    public double getPrice(){
      return price;
    }
    public void printDescription(){
      System.out.println(brand +" " + model +" "+price+" "+numWheels);
    }
}
~~~
Now each vehicle will be a specific copy of this template. The syntax to create an object of vehicle is as follows :
~~~java
 public static void main(String args[]){
Vehicle v = new Vehicle();
//v.fieldName – will give access to this vehicle’s
// fields
}
~~~

### Constructors ###

Constructor is a special method that is called when an object
is instantiated i.e created. It is used to initialize an object. Its name is same as
the class name. Even though in the above vehicle example we haven’t created
an explicit constructor there is a default constructor implicitly there. We can
create our own constructor as well. Also we can define multiple constructors
in a class as well. E.g :

~~~java
public Vehicle(Double price){
this.price = price;
}
~~~

Here this is a keyword that refers to current object, So this.price refers to the
data member (i.e. price) of this object and not the argument variable price.
One important point to note here is that as soon as we create our
constructor the default constructor goes off.
Now when we have defined the above constructor and if it is the only
constructor in the class, then we can’t create any object of Vehicle without
giving its price. In a way we can actually restrict users that they can’t create a
vehicle without giving its price.
We can have more than one constructors within the same class (i.e
constructor overloading), which constructor will be called will be decided on
runtime depending on the type and number of arguments specified while
creating the object.

# Modifiers
#### Static and Non-Static :
> Static properties are those that belong to the
class rather each specific object. So their separate copies aren’t
created. They are shared by all the objects of the class. You need to
write static keyword before it in order to make it static.
For e.g :
static int numStudents;
Here number of students in a batch is a property that isn’t specific
to each student and hence is static.
Whereas properties like name, rollNumber etc can have different
values for each object and are object specific and thus are non static.

# Access Modifiers

* #### Private :
> It is visible only within the class i.e it can be accessed
by and through the methods of the same class. So we can provide
setters and getters function through which they can be accessed
outside the class. For e.g the datafield price in the vehicle class
shown above. So we can have getter and setter function for it .
~~~java
public double getPrice(){
    return price;
}
public void setPrice(double price){
    if(price < 5000){
        return;
    }
    this.price = price;
}
~~~

* #### Default :
> When we explicitly don’t write any modifier it is default .
This modifier is package friendly i.e it can be accessed within the
same package.

* #### Protected :
> It is accessible within the same package and outside
the package but only through inheritance.

* #### Public :
> It is accessible everywhere.
An important point to note here is that its better to make a variable
private and then provide getters and setters in case we wish allow
others to view and change it than making the variable public. Because
by provding setter we can actually add constraints to the function and
update value only if they are satisfied (say vehicle price can’t be
updated if its less than 5k).

## Final Keyword :
> Final keyword can be applied before a variable,
method and a class. A final variable is one whose value can’t be
changed. So we can either initialise a final variable at the time of
declaration or in a constructor. A final method is one that can’t be
overriden. Making a class final means it can’t be inherited. (E.g : String
class in java is final)

## Abstract :
> An abstract method is one which does not have
implementation.
E.g
abstract void getType();
A class having even one abstract method has to be declared abstract,
and since a abstract class is incomplete so you cannot create an
instance of abstract class, but it can be extended. Also we can create
reference of an abstract class. We will discuss more about in
polymorphism.

# Components Of OOPS
#### Encapsulation -
 > Binding (or wrapping) code and data together into a single
unit i.e a class is known as encapsulation. It lets us hide the implementation details using different access modifiers. Also it lets us change the implementation without breaking the code of users.

#### Inheritance –
> Inheritance is a mechanism by which one class can extend
functionality from an existing class. It provides code reusability. The derived class inherits the states and behaviors from the base class. The derived class can add its own additional variables and methods. Syntax for inheritance is shown below –

~~~java
public class Car extends Vehicle {
      private int numDoors;
      String company;
      public int numDoors(){
          return numDoors;
      }
}
~~~
Here car (sub class) extends Vehicle (base class / super class) since every car
is a vehicle. So car will now have all the properties and functions that a vehicle
has except the private fields of vehicle class(since they are not inherited , but
they can be accessed via functions of base class that aren’t private).
• What if both the base class and sub class have function with same signature
i.e same name and arguments ? Say even car has a printDescription function
as in vehicle.
~~~java
public void printDescription(){
    System.out.println("Car :" + company +" " + model +"
    "+getPrice()+" "+numDoors);
    }
    then
    Car c = new Car();
    c.printDescription(); // This will call car’s printDescription
~~~
If we wish to call base class printDescription inside Car’s printDescription then
“super “ keyword should be used.
super.printDescription(); // This will call Vehicle’s printDescription
• Constructors – Suppose Vehicle has one constructor as shown below
:

~~~java
public Vehicle(Double price){
    this.price = price;
}
~~~
then Car, which extends Vehicle needs to have a constructor that passes value
to the vehicle constructor which is implicitly called when we create an object
of car.
~~~java
 public Car(double price){
    super(price); // should be the first line
    numWheels = 4;
    company = "";
 }
~~~

### Polymorphism –
>It refers to one thing taking multiple forms. Following are
different types of polymorphism that we should know about :

* Ability of a variable to take different forms – A base class’ reference can refer to the object of its sub class i.e we can do something like this –
~~~java
Vehicle v = new Car(1000);
~~~
Since every car is a vehicle so a vehicle(i.e. reference of type vehicle) can refer to a car. And not just the car, reference “v” here can refer to object of any other class that extends vehicle. But through this refernce “v” we can access only those properties of car which even a vehicle has i.e.
~~~java
v.numDoors = 4; // This will give error as numDoors is
// car’s specific property
~~~
* Overriding the base class functions(Virtual Functions) – We have already seen its example above in inheritance. When both base class and sub class have functions of same signature then base class’ function is overriden by the subclass’ function.
~~~java
Vehicle v1 = new Vehicle();
Vehicle v2 = new Car(1000);
v1.printDescription(); // Will call vehicle's printDescription
v2.printDescription(); // Will call car's printDescription
~~~
In case of v2, which printDescription should be called is decided on runtime (Runtime Polymorphism) based on the type of the object and not the type of reference. Same is the case with abstract class, a reference of abstract class can refer to objects of all its sub classes which themselves aren’t abstract.
3.3. Ability of a function to behave differently on basis of different parameters.
#### Function Overloading
~~~java
public int add(int a,int b){
    return a+b;
}
public double add(double a,double b){
    return a+b;
}
public char add(char a,char b){
    return (char)(a+b);
}
~~~
Amongst these three add functions which add will be called finally, will
be decided on runtime based on the type of parameters.

#### Constructor Overloading
>Constructor overloading is similar to function overloading. At runtime
while creating an object the number and type of parameters passed will
decide that which constructor will be called.

~~~java
 public Vehicle(String color, double price){
    this.color = "white";
    this.price = price;
  }
  public Vehicle(double price){
    this.price = price;
  }
  public Vehicle(){

  }
~~~
3.4. Ability of a function to work with parameters of subtypes – This one is just an extension of first type.
~~~java
public void print(Vehicle v){
    v.printDescription();
}
~~~
This print function expects a vehicle, so we can pass a car(or object of any
of its subtype) to it i.e.
~~~java
  Car c = new Car();
  print(c);
~~~
