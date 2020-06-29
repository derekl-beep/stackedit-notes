
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
 - `Head`: first node
 - `Tail`: last node
 
 ### Time Complexity

LOOK UP
- By value: $\text{O}(n)$
- By index: $\text{O}(n)$

INSERTION
- At the beginning: $\text{O}(1)$ with a head pointer
- At the end: $\text{O}(1)$ with a tail pointer
- In the middle: $\text{O}(n)$, involved a searching step

DELETION
- From the beginning: $\text{O}(1)$ with a head pointer
- From the end: $\text{O}(n)$ even with a tail pointer; involved searching of the second last node
- From the middle: $\text{O}(n)$, involved a searching step








> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMzY0Nzk1NzIsLTIwNDk5NzgyODddfQ
==
-->