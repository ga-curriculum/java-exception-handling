<h1>
  <span class="headline">Java Exception Handling</span>
  <span class="subhead">Delegating Exception Handling<code>try</code>-<code>catch</code> Blocks</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be able to write java code in which a called method delegates delegates exception handling responsibilities to a calling method using `throws` keyword 

## Checked and unchecked exceptions
A runtime error or, in other words, an exception is an unexpected event that occurs once we click on the **Run** button on our IDE. If we look a little deeper to understand, there are two steps actually happening in sequence upon hitting that button:

1. **Compile/Build**: The java language code that we can understand is converted into a assembler language code that the Java Virtual Machine (JVM) can understand.
2. **Execution**: The assembler language code is executed on the JVM.

The compile step can finish its task successfully only when all the Java rules and Java statement syntaxes are adhered to. Hence, the compiler **checks** the code to catch such exception-causingerrors. Hence, the exceptions that get caught during the compile step are called **checked exceptions**. Checked exceptions are encounted and displayed to the coder even before the actual execution starts. (For example: missing `{`s or `;`s, IOException, etc.)

In contrast, **unchecked exceptions** are the real runtime exceptions that cannot be caught during compile step and can occur only during the execution step. (for example: FileNotFoundException, ArrayIndexOutOfBoundsException, etc.)

Checked exceptions force the programmer, to either debug the exception or implement error handling using `try-catch` in order to run the progam.

## Error handling deep-dive
We understand that once JRE **catches** an exception that is **thrown** to it, the JRE halts the execution flow of the program and sends the information in the `Exception` object to the output console. There is something interesting that happens between the time JRE catches the exception and JRE halts the execution, which actually makes error handling possible.

Once the JRE catches an exception object:
- **Flow 1**: JRE searcher for a matching error handler (`try-catch` block with the right `ExceptionType` in the `catch` block) inside the method where the exception occured. Once found, JRE invokes the execution of that `catch` block.
- **Flow 2**: If no appropriate error handler is found, JRE searches the immediate calling method in the call stack which called the method in which the error occured to invoke error handling. If no appropriate error handler is found, it keeps moving the seach higher through each method in the call stack until the appropriate `try-catch` block is found.
- **Flow 3**: If no appropriate error handler is foung, then the JRE halts the execution and sends the information in the `Exception` object to the output console.

While coding a method, if we determine that there is a possibility of an exception and determining how to handle that exception within that method is logically impossible, or is out of the functional scope of that method, then we can delegate the error handling responsibility to any method that might call our method during program execution. In Java, this is done using the `throws` keyword.

## The `throws` keyword

Extended syntax for method declaration:
```java
returnType methodName(parameters) throws ExceptionType {
    // Method logic here
}
```
- `throws`: Declares that the execution of this method might cause an exception and there needs to be an error handler in any calling method.
- `ExceptionType`**The type of exception the method might throw.

As you might have guessed it, the `throws` part of a method declaration is optional. However, if declared, it forces the compiler to check for an appropriate error handler in the call stack of the method. If none are found, then a checked exception is generated. It forces the coder to implement the error handling before running the program again.

Usage:
```java
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class ThrowsExample {
    public static void readFile() throws IOException {
        File file = new File("nonexistent.txt");
        FileReader reader = new FileReader(file); // May throw IOException
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("Error: Unable to read the file.");
        }
    }
}
```
## Differentiating `throw` and `throws`
Since these two keywords are so alike, lets conceptually understand the differences between them

|Aspect|`throws`|`throw`|
|:---|:---|:---|
|**Purpose**| Declares exceptions a method might cause.| Generates an exception during program execution.|
|**Usage location**| As a part of method declaration.| Inside any statement block.|























## When you should use `try`-`catch` blocks

In most situations, `try`-`catch` blocks aren't mandatory, so using them is completely up to you. If you expect that a certain error has a decent chance of occurring, you can add a `try`-`catch` block to handle it.

However, there are times when you're absolutely required to have `try`-`catch` blocks, such as with file reading and writing and networking. Let's look at a few lines of code that force us to use `try`-`catch`. You can use any open Java project to add these two lines of code:

```java
import java.net.URL;
import java.net.HttpURLConnection;

public static void main(String[] args) {
    URL url = new URL("http://www.google.com"); // This will be underlined in red
    HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection(); // As will this
}
```

After importing the dependencies, you'll see that the IDE is still showing a compiler error. If you hover over the error, you'll see two options: surround the code with `try`-`catch` OR add a `throws` declaration. Let's go with `try`-`catch` for now, then we'll discuss the other option later.

We can consolidate the two `try`-`catch` blocks like this:

```java
import java.net.URL;
import java.net.HttpURLConnection;
// Import the necessary exceptions
import java.io.IOException;
import java.net.MalformedURLException;

public static void main(String[] args) {
    URL url = null;

    try {
        url = new URL("http://www.google.com"); // This line is now happy
        HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection(); // This line is also happy
    } catch (MalformedURLException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    }

}
```

> 🧠 Both `IOException` and `MalformedURLException` are examples of checked exceptions. You have to handle them for the program to compile.

Post-Java 8, we can combine our `catch` blocks into something like what's shown below. It will do the exact same thing as above but with fewer lines of code:

```java
URL url = null;

try {
    url = new URL("http://www.google.com");
    HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
} catch (MalformedURLException | IOException e) {
    e.printStackTrace();
}
```

### `throws` keyword

Now, let's talk about the other option our IDE was giving us: adding a `throws` declaration. Another way of handling a checked exception is by using the `throws` keyword. We use this keyword to tell the calling method that it's responsible for handling the error this piece of code might throw.

In the previous example where we were trying to connect to a URL...

```java
import java.net.URL;
import java.net.HttpURLConnection;

public static void main(String[] args) {
    URL url = new URL("http://www.google.com"); // This will be underlined in red
    HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection(); // As will this
}
```

...instead of `try`-`catch`, we could have used the `throws` keyword.

Again, you can use any open project to write this code:

```java
public static void connectToURL() throws IOException {
    URL url = new URL("http://www.google.com");
    HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
}
```

Now, whichever method will call `connectToURL()` can either handle the exception there or throw it to the calling method.

The biggest advantage of using this keyword is having all exception handling in one place as your application grows and becomes more complex. Also, it helps de-clutter your code.

### `throw` keyword

We use this keyword to throw an exception manually from anywhere in the code. This concept is best explained through an example.

In this example, we'll be looking at a program that divides two numbers for us and displays the result. Open up the `Division` starter code in the <code class="filepath">./src/main/java/org/example/Division.java</code> file.

> ❓ Take two minutes to look at the code and determine how to handle the error if it occurs.

The program runs smoothly if you use any value higher than zero as a divisor. But, as soon as you input zero as a divisor, the program fails with the exception `/ by zero`. This is a type of [`ArithmeticException`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/ArithmeticException.html).

In this case, in the `division()` method, we need to check if the divisor is zero, then throw an exception. We can handle this exception by surrounding our code with a `try`-`catch` block, but this time we'll let the calling method — in our case `main()` — handle the exception:

```java
public static void division(int numerator, int divisor) {

    if(divisor == 0)
        throw new ArithmeticException("Divisor is 0");

    float result = numerator/divisor;
    System.out.println("Result of the division is: " + result);
}
```

We need to put the actual division operation inside the `try` block, because that's where the error is actually going to happen. In our `catch` block, we let the user know they can't use zero as a divisor.

```java
public static void main(String[] args) {
...
    try {
        division(numerator, divisor);
    } catch(ArithmeticException e) {
        System.out.println("Error: Divisor must be greater than 0");
    }
}
```

> ❓ Is it better to check for division by zero with an exception or manually check to see if the divisor is zero?

## Conclusion

Exceptions are an important part of keeping our apps running when problems occur. Sometimes, these problems — such as certain file I/O or networking situations — are out of our hands, and we need to be prepared to handle them.
