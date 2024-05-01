# ![[tktk Module Name] - tktk Microlesson Name](./assets/index-out-of-bounds-exception.png)

**Learning objective:** By the end of this lesson, students will be able to implement error handling to manage `IndexOutofBoundsException` using `try-catch` blocks. 

## Demo: `IndexOutOfBoundsException` (10 min)

Let's take a look at a case where we try to access a value from an array with an index outside of its bounds. Open up the starter code for [`IndexOutOfBounds`](https://git.generalassemb.ly/GA-Cognizant/foundational-java/tree/master/java-basics/exception-handling-lesson/starter-code/IndexOutOfBounds). As you can see, this program has a list of superheroes and lets us enter a number to access our favorite one.

If we run the program and type in a number outside of the bounds of the `ArrayList`, we get an [`IndexOutOfBoundsException`](https://docs.oracle.com/javase/8/docs/api/index.html?java/lang/IndexOutOfBoundsException.html) — an example of an unchecked exception — and everything crashes.

Instead of having the program crash, we can log the error and allow the program to handle the exception gracefully by letting the user know that what they entered isn't valid.

Let's add a `try-catch` block around the code causing the error.

> **Knowledge Check**: Take a minute to discuss what code you think should be inside the `try` block.

```java
try {
	System.out.println(superheroes.get(num));
} catch(IndexOutOfBoundsException e) {
	System.out.println("The number you entered is invalid. Please enter a number from 0 to 2.");
}
```

As you can see, the code causing the error is `superheroes.get(num)`. By placing that inside the `try` block, we can catch the exception and show a message to the user. The program will continue running after the error has occurred, but we know the error occurred.

> **Knowledge Check**: Why didn't we put `Exception` instead of `IndexOutOfBoundsException`?