
# Topics

- Exceptions
- Generics
- Collections
- Lambda Expressions & Functional Interfaces
- Streams
- Multi-threading
- Asynchronous Programming

# Exceptions


- Types of Exceptions
- Handling Exceptions
- Custom Exceptions
- Chaining Exceptions

## Types of Exceptions

In Java, exceptions can be categorised as 

- Checked exceptions (checked at compile time)
- Unchecked exceptions (run-time), e.g.
	- `NullPointerException`
	- `ArithmeticException`
	- `IllegalArgumentException`
	- `IndexOutOfBoundsException`
	- `IllegalStateException`
- Errors, e.g.
	- `StackOverflowError`
	- `OutOfMemoryError`

## Catching Exceptions

```java
try {
	var reader = new FileReader("file.txt");
	System.out.println("File opened.");
} catch (FileNotFoundException ex) {
	System.out.println("File does not exist.");
	System.out.println(ex.getMessage());
}
```

## Catching Multiple Types of Exceptions

```java
try {
	var reader = new FileReader("file.txt");
	System.out.println("File opened.");
} catch (FileNotFoundException ex) {
	System.out.println("File does not exist.");
} catch (IOException ex) {
	System.out.println("Could not read data.");
}
```






# References



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzMxMTYyNjgsNDQ0NjMzNzU3LC0xOTAzNz
c1OTYzLDE0NTE5NzUwODZdfQ==
-->