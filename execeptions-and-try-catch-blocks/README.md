# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to understand `try-catch blocks` to manage checked and unchecked exceptions for effective error handling. 

## Opening (5 min)

We often manually check for code that could cause errors through conditional statements. But Java (as well as many other programming languages) provides a useful tool called a **`try-catch` block**. This helps to not only shape the behavior of our apps if an error occurs but also stop our apps from completely crashing if an error-prone portion of code is used (such as file-streaming or networking operations).

> **Knowledge Check**: Have you encountered any errors with `Exception` as part of their name?

***


## Introduction: Exceptions (5 min)

Before we start talking about the `try-catch` block, we need to talk about exceptions. **Exceptions** are events that occur while a program is running and interrupt the normal flow of the code. These can be null-pointer exceptions, divide-by-zero exceptions, index-out-of-bounds exceptions, and more. You can review many of the built-in exceptions in the [Java documentation](https://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html).

There are two types of exceptions: checked and unchecked. A **checked exception** occurs at compile time, which means a programmer is forced to handle these exceptions; otherwise, the program won't compile. Checked exceptions are subclasses of the `Exception` class. An **unchecked exception** — also known as a **runtime exception** — occurs at the time a program executes. You don't have to handle them, but you can if you'd like.

Below is an illustration of the exception hierarchy. Red denotes unchecked exceptions, while blue denotes checked ones:

![](https://cdn2.howtodoinjava.com/wp-content/uploads/ExceptionHierarchyJava.png)
<sub>[Source](https://howtodoinjava.com/java/exception-handling/checked-vs-unchecked-exceptions-in-java/)</sub>

When an exception occurs, we say that it's **thrown**. This will become important when we look at `try-catch` blocks. While many parts of Java throw exceptions on their own, you can manually throw exceptions as well.

***

## Introduction: `try-catch` Block (10 min)

On their own, exceptions aren't particularly useful, but when paired with a `try-catch` block, they become important. A `try-catch` block looks like this:

```java
try {
  // Your code goes here.
} catch(Exception e) {
  // Execute this code if an error occurs.
}
```

Earlier, we said that exceptions are **thrown**. We also say that they're **caught** in the `catch` statement. `Exception` is the generic type from which all other exceptions are derived, and you can catch multiple types of exceptions from a single block of code.

It's important to note that the code in the `catch` block is only executed if an exception that matches the type of `Exception` declared is thrown.

> **Knowledge Check**: Discuss with the person next to you why we would want to catch multiple types of exceptions.