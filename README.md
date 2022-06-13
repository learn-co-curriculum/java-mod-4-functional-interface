# Functional Interface

## Learning Goals

- Understand what is meant by a functional interface.
- Create and annotate functional interfaces.

## What is a Functional Interface?

A functional interface is an interface which has only one abstract method.

**NOTE:** Interface methods are `abstract` and `public` by default.

```java
// src/Example.java

interface Greeter {
    void display();
}

class MyGreet implements Greeter {
    @Override
    public void display() {
        System.out.println("Hello! How are you doing?");
    }
}

public class Example {
    public static void main(String[] args) {
        Greeter obj = new MyGreet();
        obj.display();
    }
}
```

A functional interface works exactly the same as any other interface. The only
difference is that it doesn’t allow more than one abstract method.

But there is no way to tell from the above code that `Greeter` is a functional
interface. So how do we tell the compiler that an interface is functional?

## The `@FunctionalInterface` Annotation

If we add another abstract method to the `Greeter` interface, we won’t get any
errors even though it’s not a functional interface anymore.

```java
// this is NOT a functional interface
// but it won't throw any errors
interface Greeter {
  void display();
  void sayHi();
}
```

If we annotate the `Greeter` interface with `@FunctionalInterface`, we’ll get an
error if another abstract method is added.

```java
// src/Example.java

@FunctionalInterface
interface Greeter {
    void display();
    void sayHi();
}

class MyGreet implements Greeter {
    @Override
    public void display() {
        System.out.println("Hello! How are you doing?");
    }
}

public class Example {
    public static void main(String[] args) {
        Greeter obj = new MyGreet();
        obj.display();
    }
}
```

Running the above code will cause the following error:

```plaintext
java: Unexpected @FunctionalInterface annotation
  Greeter is not a functional interface
    multiple non-overriding abstract methods found in interface Greeter
```

It’s best practice to always annotate functional interfaces to prevent
accidental addition of abstract methods.
