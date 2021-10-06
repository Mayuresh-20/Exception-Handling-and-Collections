# Exception-Handling-and-Collections

Why do we need Exception Handling?
►We don’t like exceptions but we always have to deal with them. The great news is that Exception handling in Java is extremely robust and easy to understand and use. Exceptions in java can arise from different kinds of situations such as wrong data entered by the user, hardware failure, network connection failure, Database server down, etc. The code that specifies what to do in specific exception scenarios is called exception handling.

How Java Handles Exception?
►Java is an object-oriented programming language. So whenever an error occurs while executing a statement, it creates an exception object. The normal flow of the program halts and JRE tries to find someone that can handle the raised exception.

The exception object contains a lot of debugging information such as method hierarchy, line number where the exception occurred, type of exception, etc. When the exception occurs in a method, the process of creating the exception object and handing it over to the runtime environment is called “throwing the exception”.

Once runtime receives the exception object, it tries to find the handler for the exception. Exception Handler is the block of code that can process the exception object.

The logic to find the exception handler is simple – starting the search in the method where the error occurred, if no appropriate handler found, then move to the caller method and so on. So if methods call stack is A->B->C and exception is raised in method C, then the search for the appropriate handler will move from C->B->A.

If an appropriate exception handler is found, the exception object is passed to the handler to process it. The handler is said to be “catching the exception”. If there is no appropriate exception handler found then the program terminates and prints information about the exception to the console.

Java Exception handling framework is used to handle runtime errors only. The compile-time errors have to be fixed by the developer writing the code else the program won’t execute.

• Java Exception Handling Keywords
Java provides specific keywords for exception handling purposes.

►throw – We know that if an error occurs, an exception object is getting created and then Java runtime starts processing to handle them. Sometimes we might want to generate exceptions explicitly in our code, for example in a user authentication program we should throw exceptions to clients if the password is null. The throw keyword is used to throw exceptions to the runtime to handle it.

►throws – When we are throwing an exception in a method and not handling it, then we have to use the throws keyword in the method signature to let the caller program know the exceptions that might be thrown by the method. The caller method might handle these exceptions or propagate them to its caller method using the throws keyword. We can provide multiple exceptions in the throws clause and it can be used with the main() method also.

►try-catch – We use try-catch block for exception handling in our code. try is the start of the block and catch is at the end of the try block to handle the exceptions. We can have multiple catch blocks with a try block. The try-catch block can be nested too. The catch block requires a parameter that should be of type Exception.

►finally – the finally block is optional and can be used only with a try-catch block. Since exception halts the process of execution, we might have some resources open that will not get closed, so we can use the finally block. The finally block gets executed always, whether an exception occurred or not.
Exception Handling Example Program
package com.journaldev.exceptions;
 
import java.io.FileNotFoundException;
import java.io.IOException;
 
public class ExceptionHandling {
 
    public static void main(String[] args) throws FileNotFoundException, IOException {
        try{
            testException(-5);
            testException(-10);
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            System.out.println("Releasing resources");          
        }
        testException(15);
    }
     
    public static void testException(int i) throws FileNotFoundException, IOException{
        if(i < 0){
            FileNotFoundException myException = new FileNotFoundException("Negative Integer "+i);
            throw myException;
        }else if(i > 10){
            throw new IOException("Only supported for index 0 to 10");
        }
    }
}
Output:►

java.io.FileNotFoundException: Negative Integer -5
    at com.journaldev.exceptions.ExceptionHandling.testException(ExceptionHandling.java:24)
    at com.journaldev.exceptions.ExceptionHandling.main(ExceptionHandling.java:10)
Releasing resources
Exception in thread "main" java.io.IOException: Only supported for index 0 to 10
    at com.journaldev.exceptions.ExceptionHandling.testException(ExceptionHandling.java:27)
    at com.journaldev.exceptions.ExceptionHandling.main(ExceptionHandling.java:19)

• Java Exception Hierarchy
As stated earlier, when an exception is raised an exception object is getting created. Java Exceptions are hierarchical and inheritance is used to categorize different types of exceptions. Throwable is the parent class of Java Exceptions Hierarchy and it has two child objects – Error and Exception. Exceptions are further divided into checked exceptions and runtime exceptions.

►Errors: Errors are exceptional scenarios that are out of the scope of application and it’s not possible to anticipate and recover from them. For example, hardware failure, JVM crash, or out-of-memory error. That’s why we have a separate hierarchy of errors and we should not try to handle these situations. Some of the common Errors are OutOfMemoryError and StackOverflowError.

►Checked Exceptions: Checked Exceptions are exceptional scenarios that we can anticipate in a program and try to recover from it. For example, FileNotFoundException. We should catch this exception and provide a useful message to the user and log it properly for debugging purposes. The Exception is the parent class of all Checked Exceptions. If we are throwing a checked exception, we must catch it in the same method or we have to propagate it to the caller using the throws keyword.

►Runtime Exception: Runtime Exceptions are caused by bad programming. For example, trying to retrieve an element from the Array. We should check the length of the array first before trying to retrieve the element otherwise it might throw ArrayIndexOutOfBoundException at runtime. RuntimeException is the parent class of all runtime exceptions. If we are throwing any runtime exception in a method, it’s not required to specify them in the method signature throws clause. Runtime exceptions can be avoided with better programming.
![image](https://user-images.githubusercontent.com/91977965/136163088-a783c8f5-9000-4fa2-8a79-e2f4fc9054bc.png)
►If you are catching a lot of exceptions in a single try block, you will notice that the catch block code looks very ugly and mostly consists of redundant code to log the error. Java 7 one of the feature was improved catch block where we can catch multiple exceptions in a single catch block. The catch block with this feature looks like below:

catch(IOException | SQLException ex){
     logger.error(ex);
     throw new MyException(ex.getMessage());
}


►Java 7 one of the improvements was try-with-resources where we can create a resource in the try statement itself and use it inside the try-catch block. When the execution comes out of the try-catch block, the runtime environment automatically closes these resources. Sample of the try-catch block with this improvement is:

try (MyResource mr = new MyResource()) {
            System.out.println("MyResource created in try-with-resources");
        } catch (Exception e) {
            e.printStackTrace();
        }
        
 • Collections in Java

►Any group of individual objects which are represented as a single unit is known as the collection of the objects. In Java, a separate framework named the “Collection Framework” has been defined in JDK 1.2 which holds all the collection classes and interface in it.

The Collection interface (java.util.Collection) and Map interface (java.util.Map) are the two main “root” interfaces of Java collection classes.

• What is a Framework?
►A framework is a set of classes and interfaces which provide a ready-made architecture. In order to implement a new feature or a class, there is no need to define a framework. However, an optimal object-oriented design always includes a framework with a collection of classes such that all the classes perform the same kind of task.

Need for a Separate Collection Framework

Before Collection Framework(or before JDK 1.2) was introduced, the standard methods for grouping Java objects (or collections) were Arrays or Vectors or Hashtables. All of these collections had no common interface. Therefore, though the main aim of all the collections are same, the implementation of all these collections were defined independently and had no correlation among them. And also, its very difficult for the users to remember all the different methods, syntax and constructors present in every collection class.

• Advantages of the Collection Framework: Since the lack of a collection framework gave rise to the above set of disadvantages, the following are the advantages of the collection framework.

►Consistent API: The API has a basic set of interfaces like Collection, Set, List, or Map, all the classes (ArrayList, LinkedList, Vector, etc) that implement these interfaces have some common set of methods.

►Reduces programming effort: A programmer doesn’t have to worry about the design of the Collection but rather he can focus on its best use in his program. Therefore, the basic concept of Object-oriented programming (i.e.) abstraction has been successfully implemented.

►Increases program speed and quality: Increases performance by providing high-performance implementations of useful data structures and algorithms because in this case, the programmer need not think of the best implementation of a specific data structure. He can simply use the best implementation to drastically boost the performance of his algorithm/program.

• Hierarchy of the Collection Framework
The utility package, (java.util) contains all the classes and interfaces that are required by the collection framework. The collection framework contains an interface named an iterable interface which provides the iterator to iterate through all the collections. This interface is extended by the main collection interface which acts as a root for the collection framework. All the collections extend this collection interface thereby extending the properties of the iterator and the methods of this interface. The following figure illustrates the hierarchy of the collection framework.

![image](https://user-images.githubusercontent.com/91977965/136164060-f848a4da-450c-4fbc-9f19-2adfb0062770.png)

Interfaces which extend the Collections Interface
The collection framework contains multiple interfaces where every interface is used to store a specific type of data. The following are the interfaces present in the framework.

1. Iterable Interface: This is the root interface for the entire collection framework. The collection interface extends the iterable interface. Therefore, inherently, all the interfaces and classes implement this interface. The main functionality of this interface is to provide an iterator for the collections. Therefore, this interface contains only one abstract method which is the iterator. It returns the Iterator iterator();

2. Collection Interface: This interface extends the iterable interface and is implemented by all the classes in the collection framework. This interface contains all the basic methods which every collection has like adding the data into the collection, removing the data, clearing the data, etc. All these methods are implemented in this interface because these methods are implemented by all the classes irrespective of their style of implementation. And also, having these methods in this interface ensures that the names of the methods are universal for all the collections. Therefore, in short, we can say that this interface builds a foundation on which the collection classes are implemented.

3. List Interface: This is a child interface of the collection interface. This interface is dedicated to the data of the list type in which we can store all the ordered collection of the objects. This also allows duplicate data to be present in it. This list interface is implemented by various classes like ArrayList, Vector, Stack, etc. Since all the subclasses implement the list, we can instantiate a list object with any of these classes.
