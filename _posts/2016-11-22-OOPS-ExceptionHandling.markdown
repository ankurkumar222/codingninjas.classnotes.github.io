---
layout: post
title:  "Exception Handling"
date:   2016-10-22 06:08:02 +0530
---



An exception is an event, which occurs during the execution of a program, that
disrupts the normal flow of the program's instructions. The exception handling in java is one of the powerful mechanism to handle the runtime errors so that normal
flow of the application can be maintained.
When an error occurs within a method, the method creates an object and hands it off to the runtime system. The object, called an exception object, contains
information about the error, including its type and the state of the program when
the error occurred. Creating an exception object and handing it to the runtime
system is called throwing an exception.
After a method throws an exception, the runtime system attempts to find
something to handle it.
When an exception occurs the run time system first tries to find
an exception handler in the method where the exception occurred and then
searches the methods in the reverse order in which they were called for the
exception handler. The list of methods is known as the call stack(shown below). If no method handles the exception then exception appears on the console (like we
see ArrayIndexOutOfBoundsException etc)
 exception handler.
The block of code that handles an exception is called
 Types of Exception
## Checked Exceptions :
> These are exceptional conditions that we can
anticipate when user makes mistake . For example computing factorial of a
negative number. A well-written program should catch this exception and
notify the user of the mistake, possibly prompting for a correct input. Checked
exceptions are subject to the Catch or Specify Requirement i.e either the
function where exception can occur should handle or specify that it can throw
an exception (We will look into it in detail later).

## Error :
> These are exceptional conditions that are external to the application, and that the application usually cannot anticipate or recover from. For example, suppose that an application successfully opens a file for input, but is unable to read the file because of a hardware or system malfunction.

## Exception Handling
> Exception handling is achieved by using try catch and/or finally block.
#### Try block -
The code which can cause an exception is enclosed within try block.
#### Catch block -
The action to be taken when an exception has occurred is done in catch block. It must be used after the try block only.
#### Finally block -
Java finally block is a block that is used to execute important code such as closing connection, stream etc. Java finally block is always executed whether exception is handled or not.
Here is a sample code to explain the same.
~~~java
public static void main(String[] args){
        Scanner s = new Scanner(System.in);
        System.out.println("Enter dividend ");
        int dividend = s.nextInt();
        System.out.println("Enter divisor ");
        int divisor = s.nextInt();
        try{
            int data= dividend/divisor; System.out.println(data);
        }
        catch(ArithmeticException e){
            System.out.println(“Divide by zero error”);
        }
        finally{
            System.out.println("finally block is always executed");
        }
        System.out.println("rest of the code...");
}
~~~
Note :
> * Whenever an exception occurs statements in the try block after the
statement in which exception occurred are not executed
> * For each try block there can be zero or more catch blocks, but only one finally block.
 Unchecked Exception : These are exceptional conditions that might occur at
 runtime but we don’t expect them to occur while writing code. These usually
 indicate programming bugs, such as logic errors or improper use of an API.
 For example StackOverflowException.

### Creating an Exception / User Defined Exceptions
A user defined exception is a sub class of the exception class. For creating an exception you simply need to extend Exception class as shown below :
~~~java
public class InvalidInputException extends Exception {
  private static final long serialVersionUID = 1L;
}
~~~
Throwing an Exception
Sometimes, it's appropriate for code to catch exceptions that can occur within it. In other cases, however, it's better to let a method further up the call stack handle the exception. For example if input to the factorial method is a negative number, then it makes more sense for the factorial to throw an exception and the method that has called factorial method to handle the exception.
Here is the code for the factorial method :
~~~java
public static int fact(int n) throws InvalidInputException{
    if(n < 0){
      InvalidInputException e = new InvalidInputException();
      throw e;
    }
    if(n == 0){
         return 1;
    }
    return n*fact(n-1);
}
~~~
The fact method throws an InvalidInputException that we created above and we will handle the exception in main.
~~~java
public static void main(String[] args) {
      Scanner s = new Scanner(System.in);
      System.out.println("Enter number ");
      int n = s.nextInt();
      int a = 10;
      try{
          System.out.println(fact(n));
          a++;
      }
      catch(InvalidInputException e)
      {
          System.out.println("Invalid Input !! Try again");
          return;
      }
}
~~~
