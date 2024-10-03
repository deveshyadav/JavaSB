Question 1: Java 8 features
Java 8 introduced several powerful new features and enhancements that significantly changed the way Java programming is approached. Below are the main features of Java 8 along with explanations:

1. Lambda Expressions
Lambda expressions provide a clear and concise way to represent a method interface using an expression. They help in writing more readable and compact code, especially when used in collection operations.

Syntax Example:
```Java
// Before Java 8: Using an anonymous class
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello from Runnable");
    }
};

// Using Lambda Expression in Java 8
Runnable runnableLambda = () -> System.out.println("Hello from Lambda");


2. Functional Interfaces
Functional interfaces are interfaces with a single abstract method. They can be represented by lambda expressions. 
Java 8 introduced several built-in functional interfaces, such as Predicate, Function, Consumer, etc.

@FunctionalInterface
interface MyFunctionalInterface {
    void doSomething();
}

// Using Lambda Expression
MyFunctionalInterface action = () -> System.out.println("Doing something");
action.doSomething();
