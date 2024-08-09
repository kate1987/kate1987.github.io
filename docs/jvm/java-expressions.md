# Java Expressions

Lightrun supports the usage of Java expressions in multiple scenarios. Specifically, it supports the following:

* Log format - when adding a log an expression can appear inside curly braces (`{}`) e.g. `My variable value is {myVar} and my method returned {myMethod()}` which will print out the value of the actual variable. 
* Conditions which are standard boolean expressions e.g. `myVar > 20`.
* Watch expressions which represent a value we query e.g. `myVar`.

All of these can be added when creating a respective action. In this section we'll discuss the limits of these expressions.

## Read-Only

All expressions are evaluated by the Lightrun agent. If an expression modifies state it will fail. E.g. an expression such as `{myMethod()}` will fail if the code for this method looks like this:

```java
public int myMethod() {
    if(thisIsNeverTrue) {
        myVar = 10;
    }
    return myVar;
}
```

Lightrun doesn't do complex runtime static analysis (for performance). If an assignment exists but isn't reachable then it will fail the read-only test. 

## Throttling

Lightrun throttles slow code or code that's excessively used. Complex expressions just won't work e.g. a log such as `This is my list of objects {list}` will fail even for a relatively small list.

However, printing an individual entry will work much better e.g.: `This is the object from my list {list.get(offset)}`

!!! tip
    Use a simple constraint to limit over logging or snapshots.

## Syntax Limitations

Lightrun always uses Java syntax for expressions. Even when working with other JVM languages such as Kotlin, Scala etc. 

The syntax has some restrictions due to the way Java bytecode works. Some information isn't available in the agent and some restrictions are there for performance.

### 256 Characters

An expression can't exceed 256 characters. Notice that Lightrun throttles complex expressions anyway, so long expressions might be irrelevant. 

However, if you create exceptionally long variable names you might run into this limit.

### Erasures

Let's review the following Java code:

```java
List<MyObject> myList = new ArrayList<>();
```

Let's say I want to add the following log statement: `My first list object is: {myList.get(0).myMethod()}`. 

This will fail. To understand why we need to understand that Java generics are a compile time construct. The compiler strips away the type and converts it to a cast, as such the agent has no idea what the type is.

The solution is simple: `My first list object is: {((MyObject)myList.get(0)).myMethod()}`.

## Name Resolution

Java handles name spaces/collisions very well thanks to the package and module systems. Java `import` statements are used to resolve fully qualified names in your Java applications. This resolution is done during compile time, the class file has no bytecode equivalent of the import statement.

E.g. code like this:

```java
import java.util.List;
public class MyClass {
    public static void main(String[] args) {
        List<String> myList = new ArrayList<>();
        // ...
    }
}
```

Is compiled by `javac` to:

```java
public class MyClass {
    public static void main(String[] args) {
        java.util.List<String> myList = new java.util.ArrayList<>();
        // ...
    }
}
```

This is important because Java also has a `java.awt.List` class and collision with `java.util.List` is a real problem!

If I add an expression such as: `((List)object).size()` it's possible that it will fail. Lightrun will try to find the correct class but might accidentally pick the AWT class instead of the util class.

The solution is to use the fully qualified name: `((java.util.List)object).size()`.