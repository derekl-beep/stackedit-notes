
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
- Priority queues
	- task scheduling based on priority
- Finding the k-th smallest/largest value
- Graph algorithms: shortest path



### Complexity

INSERT: $\text{O}(\text{log} \ n)$
DELETE: $\text{O}(\text{log}\  n)$

### Implementation of Heaps

A heap can be implemented as an array in memory.

#### Index relationship
`left = parent * 2 + 1`
`right = parent * 2 + 2`
`parent = (index - 1) / 2`




## Graph

### Adjacency Matrix

#### Complexity

`V`: vectices
`E`: edges

Space: $\text{O}(n^2)$
Add Node: $\text{O}(V^2)$
Remove Node: $\text{O}(V^2)$







> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ4NTYyMzQxOCwxNjIwNjkzNTEsNTYyMT
UzMTE3LC0xMDg0NjA4MDk3LC02NDY4NTMyNzEsODA5NTEzNDk5
LC0xMzIyOTE1MzQ5LDE2Nzg4OTA3MzgsLTQ4NzMyMzUzOCw2NT
M5MDM5ODYsMTA0MzIyMjYxMSwxMjAzMzQ3MDI4LC0xMjg2MDgx
MDMzLC0xMjg2MDgxMDMzLDEwMjA2MDk3MDksMTA4ODAxNjcwMi
w5OTM4NTgzMzQsNjE5Nzk5MzE2LDMyMTI0NzMwNCwtMjEzNjQ3
OTU3Ml19
-->