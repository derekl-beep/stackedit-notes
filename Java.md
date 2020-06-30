
## Java Project Structure

Project folder
`src`: source file folder
`com.xxxx`: package folder
`Main.java`: main file


## Linked List

### Properties

A linked list

- consists of a group of nodes in sequence
 - grows and shrinks dynamically
 - is made up of two parts: data and reference to the next node
 
 `Head`: first node
 `Tail`: last node
 
 ### Time Complexity

LOOK UP
- By value: $\text{O}(n)$
- By index: $\text{O}(n)$

INSERTION
- At the beginning: $\text{O}(1)$ with a head pointer
- At the end: 
	- $\text{O}(1)$ with a tail pointer
	- $\text{O}(n)$ without a tail pointer
- In the middle: $\text{O}(n)$, involved a searching step

DELETION
- From the beginning: $\text{O}(1)$ with a head pointer
- From the end: 
	- Singly linked list: $\text{O}(n)$ even with a tail pointer; involved searching of the second last node
	- Doubly linked list: $\text{O}(1)$
- From the middle: $\text{O}(n)$, involved a searching step


### Linked List in Java

`java.util.LinkedList` includes the implementation of `LinkedList` in java.

```java
package com.derek;  
  
import java.util.Arrays;  
import java.util.LinkedList;  
  
public class Main {  
	public static void main(String[] args) {  
		
		// Create a linked list object using the java util  
		LinkedList list = new LinkedList();  
		
		// Add nodes to the end of the list  
		list.addLast(10);  
		list.addLast(20);  
		list.addLast(30);  

		System.out.println(list);  

		// Look up by value  
		System.out.println(list.contains(10));  
		System.out.println(list.indexOf(20));  

		System.out.println(list.size());  

		// Cast to an array structure  
		var array = list.toArray();  
		System.out.println(Arrays.toString(array));  
	}  
}
```

Comparison with `Array`

Space Complexity

- Static arrays have a fixed size.
- Dynamic arrays gro 




> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk5MzUwNTQ2Nyw5OTM4NTgzMzQsNjE5Nz
k5MzE2LDMyMTI0NzMwNCwtMjEzNjQ3OTU3MiwtMjA0OTk3ODI4
N119
-->