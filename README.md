# Functional Interface

## Learning Goals

- Define a functional interface.
- Define `@FunctionalInterface` annotation.
- Create and annotate functional interfaces.

## What is a Functional Interface?

A functional interface: 

- Defines exactly one abstract method (i.e. a single abstract method).  
- May define any number of default and static methods.
- May define abstract methods that override public methods of `java.lang.Object` (i.e. equals, hashCode, etc). 
  - Such methods are not included in the abstract method count.

The `Greeter` interface is a functional interface that defines one abstract method `display()`.

```java
interface Greeter {
    void display();
}
```
**NOTE:** Interface methods are `abstract` and `public` by default.

Any class that implements `Greeter` must override the abstract method, for example:

```java
public class MyGreet implements Greeter {
    @Override
    public void display() {
        System.out.println("Hello! How are you doing?");
    }
}
```

We can assign a `MyGreet` object to a variable declared with type `Greeter` since the
class implements the interface:

```java
public class Example {
    public static void main(String[] args) {
        Greeter obj = new MyGreet();
        obj.display();  //Hello! How are you doing?
    }
}
```

A functional interface works exactly the same as any other interface. The only
difference is that a functional interface should not allow more than one abstract method.

But there is no way to ensure from the above code that `Greeter` is a functional
interface. How do we tell the compiler to check whether an interface is functional?

## The `@FunctionalInterface` Annotation

The `@FunctionalInterface` annotation indicates that an interface
defines a single abstract method.   While the annotation is not mandatory, it is
a good idea to use as it forces the compiler to check for exactly one abstract method.

```java
@FunctionalInterface
interface Greeter {
    void display();
}
```

An error occurs if `@FunctionalInterface` is used
on an interface that defines more than one abstract method.
We will get a compiler error if we add a second abstract method to the `Greeter` interface:

```java
@FunctionalInterface
interface Greeter {
 void display();
 void sayHi();
}
```

Running the above code results in the following error:

```plaintext
java: Unexpected @FunctionalInterface annotation
  Greeter is not a functional interface
    multiple non-overriding abstract methods found in interface Greeter
```

## Summary

A functional interface may define any number of default and static methods,
but it is restricted to defining a single abstract method. 
Abstract methods overriding public methods from `java.lang.Object` (equals, hashCode, etc)
do not count toward the single abstract method count.

It’s best practice to always annotate functional interfaces with `@FunctionalInterface`
to prevent accidental addition of abstract methods.

```java
@FunctionalInterface
interface Greeter {
    void display();
}
```

## Resources

[Java 11 FunctionalInterface](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/FunctionalInterface.html)

[Java 11 Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html)