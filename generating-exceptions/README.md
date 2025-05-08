<h1>
  <span class="headline">Java Exception Handling</span>
  <span class="subhead"><code>Generating Exceptions</code></span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to generate Java exceptions in their code using the `throw` keyword.

## Why would you want to throw an exception?

We know that an exception is an unexpected and unintentional error event that can happen during the execution of a program and disrupt its normal flow. While building Java applications, there might be situations where we might have to intentionally stop the user from proceeding further because something has gone wrong.

One of the choices with you as a programmer is to reuse Java's way of stopping further code execution using exceptions. To generate our own exceptions, we need to understand how Java Runtime Engine (JRE) throws an exception and mimic it.

## How Java throws an exception

 Unintended events in Java can arise from different situations, such as wrong data entered by the user, hardware failure, network connection failure, or a database server being down. Java creates an exception object when an error occurs while executing a statement.

The exception object contains a lot of debugging information, such as method hierarchy (call stack), the line number where the exception occurred, and the type of exception. Here's the sequence of how an exception is generated in Java:

- **Step 1**: An unexpected runtime event occurs while executing a particular statement in a program.

- **Step 2**: An exception object is automatically created by choosing the most accurate class that defines the current event, from a pre-defined list of `Exception` classes, and instantiating an `Exception` object. It is populated with all the required information.

- **Step 3**: This `Exception` object is then handed over to the JRE.

- **Step 4**: JRE halts the normal execution flow of the program and sends the information in the `Exception` object in a structured way to output medium. (For a developer, the IDE's console panel is the output medium, which is where this error information is displayed as a stack trace message.)

The process of creating an `Exception` object from one of the `Exception` classes and handing it over to the JRE is called **throwing an exception**.

## Programmatic exception throwing

Exceptions can be created using the `throw` statement in Java.

Syntax:

```java
throw new ExceptionType("Error message");
```

- `throw`: The keyword used to throw an exception.
- `new`: The keyword used to create an instance of the exception class.
- `ExceptionType`: The type (class) of exception to be thrown (like `IllegalArgumentException`, `IOException`, `ArithmeticException`, etc.).
- **"Error message"**: (Optional) A developer-programmed message describing the exception to provide additional context to the user about what went wrong.

Let's look at an example code to enforce a business rule that customers cannot withdraw more than their account balance amount.

```java
public void processWithdrawl(double amount, double balance) {
    if (amount > balance) {
        throw new IllegalArgumentException("Insufficient funds for transaction.");
    }
}
```

<div class="activity solo-exercise">
  <h2 class="title"><code>ExceptionType</code> research</h2>
  <span class="minutes">8 min</span>
</div>

Research and find various built-in exceptions that can be used for `ExceptionType` in the `throw` statement.
