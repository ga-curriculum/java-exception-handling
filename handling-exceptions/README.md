<h1>
  <span class="headline">Java Exception Handling</span>
  <span class="subhead">Handling Exceptions</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be code exception handling statements using `try-catch-finally` statement blocks

## The `try-catch-finally` block

Java provides a sequential structure to handle exceptions:

```java
try {
    // Code that has the probability to throw an exception needs to be enclosed inside this block
} catch (ExceptionType e) {
    // Code to handle the exception encountered in try block needs to reside in this block
} finally {
    // An optional block that contains code that will always run, whether or not an exception occurred.
}
```

## Control flow of the `try-catch-finally` block

### Exception occurance flow
1. The program execution enters the `try` block.
2. If an exception occurs, the remaining code in the `try` block is skipped.
3. The program execution jumps to the `catch` block.
4. After the `catch` block executes, the program moves to the `finally` block (if it exists).

### Exception non-occurance flow
1. The program execution enters the `try` block.
2. Executes all the code in the `try` block.
3. Skips the `catch` block.
4. Executes the `finally` block (if it exists).

## Demo of `try-catch-finally` block
Here is a program that gracefully handles an `ArithmeticException` (division by zero) gracefully using `try-catch-finally` block.

```java
public class SafeDivision {
    public static void main(String[] args) {
        int a = 15;
        int b = 0;

        try {
            System.out.println("Attempting to divide " + a + " by " + b);
            int result = a / b;
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero.");
        } finally {
            System.out.println("End of division operation.");
        }
    }
}
```

## Independent Practice
(10 minutes)

Using the sample code given in this lesson, try to find answers for the following questions?
1. Can we have a `catch` or `finally` block without a `try` block?
2. Can we have a `try` block without a `catch` or `finally` block?
3. Can we code any statements in the space between the `try`, `catch` and `finally` blocks?
4. Can we have multiple `catch` blocks for a single `try` block?
