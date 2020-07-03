
# Java Project Structure

Project folder
`src`: source file folder
`com.xxxx`: package folder
`Main.java`: main file


# Data Structures

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

`java.util.LinkedList` includes the implementation of `LinkedList` in java. This implements a doubly linked list.

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

### Comparison with `Array`

#### Space Complexity

- Static arrays have a fixed size.
- Dynamic arrays grow by 50% - 100%.
- Linked lists don't waste memory


#### Time Complexity

// TBC

### Types of Linked List

Singly linked list

Doubly linked list

- Delete from end operation improves to $\text{O}(1)$ from $\text{O}(n)$, but takes more spaces.
- `LinkedList()` class in Java is an implementation of the doubly linked list.

Circular linked list

- e.g. music playlists, sign-in form input boxes


### Advanced Methods

`list.reverse()`

`list.getKthFromTheEnd(int k)`

`list.printMiddle()`

`list.hasLoop()`


## Hash Tables

### Properties

- To store key/value pairs
- Insert, remove, lookup run in $\text{O}(1)$
- Hash function
- Collision
	- Chaining, using `LinkedList`
	- Open addressing
		- Linear probing, `(hash1 + i) % table_size`
		- Quadratic probing, `(hash1 + i * i) % table_size`
		- Double hash probing, `(hash1 + i * hash2) % table_size`

### Implementations in JAVA

```java
HashMap<Character, Integer> map = new HashMap<>();
```

```java
HashSet<Integer> set = new HashSet<>();
```


## Heaps

- A complete tree. Levels are filled from the left to the right.
- Heap property
	- Max heap: `parent.value() >= child.value()`
	- Min heap: `parent.value() <= child.value()`

### Applications

- Sorting: HeapSort
- Graph algorithms: shortest path
- Priority queues
- Finding the k-th smallest/largest value

### Complexity

INSERT: $\text{O}(\text{log} \ n)$
DELETE: $\text{O}(\text{log}\  n)$

### Implementation of Heaps










> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA5NTYxNzA1MCwtNjQ2ODUzMjcxLDgwOT
UxMzQ5OSwtMTMyMjkxNTM0OSwxNjc4ODkwNzM4LC00ODczMjM1
MzgsNjUzOTAzOTg2LDEwNDMyMjI2MTEsMTIwMzM0NzAyOCwtMT
I4NjA4MTAzMywtMTI4NjA4MTAzMywxMDIwNjA5NzA5LDEwODgw
MTY3MDIsOTkzODU4MzM0LDYxOTc5OTMxNiwzMjEyNDczMDQsLT
IxMzY0Nzk1NzIsLTIwNDk5NzgyODddfQ==
-->