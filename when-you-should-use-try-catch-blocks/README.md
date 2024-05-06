# ![[tktk Module Name] - tktk Microlesson Name](./assets/when-you-should-use-trycatch-blocks.png)

**Learning objective:** By the end of this lesson, students will be able to utlize `try-catch` blocks and the `throws` and `throw` keywords to handle and manage exceptions. 

## When You Should Use `try-catch` Blocks (10 min)

In most situations, `try-catch` blocks aren't mandatory, so using them is completely up to you. If you expect that a certain error has a decent chance of occurring, you can add a `try-catch` block to handle it.

However, there are times when you're absolutely required to have `try-catch` blocks, such as with file reading and writing and networking. Let's look at a few lines of code that force us to use `try-catch`. You can use any open Java project to add these two lines of code:

```java
import java.net.URL;
import java.net.HttpURLConnection;

public static void main(String[] args) {
    URL url = new URL("http://www.google.com"); // This will be underlined in red
    HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection(); // As will this
}
```
After importing the dependencies, you'll see that the IDE is still showing a compiler error. If you hover over the error, you'll see two options: surround the code with `try-catch` OR add a `throws` declaration. Let's go with `try-catch` for now, then we'll discuss the other option later.

We can consolidate the two `try-catch` blocks like this:

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
> Both `IOException` and `MalformedURLException` are examples of checked exceptions. You have to handle them for the program to compile.

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

...instead of `try-catch`, we could have used the `throws` keyword.

Again, you can use any open project to write this code:

```java
public static void connectToURL() throws IOException {
	URL url = new URL("http://www.google.com");
	HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
}
```
Now, whichever method will call `connectToURL()` can either handle the exception there or throw it to the calling method.

The biggest advantage of using this keyword is having all exception handling in one place as your application grows and becomes more complex. Also, it helps declutter your code.

### `throw` keyword
We use this keyword to throw an exception manually from anywhere in the code. This concept is best explained through an example. 

In this example, we'll be looking at a program that divides two numbers for us and displays the result. Open up the [`DivisionExample` starter code](https://git.generalassemb.ly/GA-Cognizant/foundational-java/tree/master/java-basics/exception-handling-lesson/starter-code/DivisionExample).

> **Knowledge Check**: Take two minutes to look at the code and determine how to handle the error if it occurs.

The program runs smoothly if you use any value higher than zero as a divisor. But, as soon as you input zero as a divisor, the program fails with the exception `/ by zero`. This is a type of [`ArithmeticException`](https://docs.oracle.com/javase/8/docs/api/?java/lang/ArithmeticException.html).

In this case, in the `division()` method, we need to check if the divisor is zero, then throw an exception. We can handle this exception by surrounding our code with a `try-catch` block, but this time we'll let the calling method — in our case `main()` — handle the exception:

```java
public static void division(int numerator, int divisor) {
		
	if(divisor == 0)
		throw new ArithmeticException("Divisor is 0");
	
	float result = numerator/divisor;
	System.out.println("Result of the division is: " + result);
}
```

We need to put the actual division operation inside the `try` block, because that's where the error is actually going to happen. In our `catch` block, we let the user know they can't use zero as a divisor.

```
public static void main(String[] args) {
...
	try {
		division(numerator, divisor);
	} catch(ArithmeticException e) {
		System.out.println("Error: Divisor must be greater than 0");
	}
}
```

> **Knowledge Check**: Is it better to check for division by zero with an exception or manually check to see if the divisor is zero?

***

## Conclusion (5 min)

Exceptions are an important part of keeping our apps running when problems occur. Sometimes, these problems — such as certain file I/O or networking situations — are out of our hands, and we need to be prepared to handle them.