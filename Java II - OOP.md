# Java Part 2: Object-oriented Programming

### Topics
- Classes - Encapsulation & Abstraction
- Refactoring Towards an Object-oriented Design
- Inheritance & Polymorphism
- Interfaces


## Introduction 

### Programming Paradigms

Two most popular programming paradigms these days:
- Functional
- Object-oriented 

Other paradigms incluede:

- Procedural
- Event-driven
- Logic
- Aspect-oriented

### Benefits of OOP

- Reduce complexity
- Easier maintance
- Code reuse $\rightarrow$ Faster development

## Classes

### Topics

- Encapsulation
- Abstraction
- Constructors
- Getters / Setters
- Method Overloading

A class is a template / a blueprint for creating new objects, while an object is an instance of a class that it was created upon.

### Memory Allocation in Java

Stack

- Primitive variables
- Reference variables
- Local variables
- Pointers to the objects on the heap memory, i.e. memory addresses

Heap

- Objects


Deallocation

- Memory in stack is cleaned up when the method returns.
- Garbge collection is automatically done in Java to clean up the heap memory.

### Encapsulation

Main idea:
Bundle the data and the methods that operate on the data in a single unit.

 
### Abstraction

Main idea:
Reduce complexity by hiding unnecessary details, e.g. implementation details of a class method.

### Coupling

The level of dependency between classes.

Decoupling methods, e.g.

- Make unused methods private


## Interfaces

- What interfaces are?
- Why we need them?
- How to use them?
- Dependency injection

We use interfaces to build loosely-coupled, extensible, testable applications.

```java
public interface Draggable() {
	void drag();
}
```


An interface defines what should be done.

A class defines how should be done. 

 Interfaces in `Java` are like header files in `C++`.

## Revision Questions

1. What are the six common programming paradigms these days?





## References






> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDY5MzY4NzMwLDQ1NzM3NDY5MSwtNjMxNz
MxMDc3LC0yMTE2MjUyNDM4LDg0MjgzNjYwNCwtMTYzOTMyNzkx
MSwxMjk4NTc4NDIzLDIwMjk0Mzg4NzYsLTUxNjU4NzcyMCwxMz
c2Nzg3MjIsMTQ3MjI3ODc0NiwtMjc4NTkxMjY5LDc2OTMwOTYx
MiwxNjM1MjgyMzgyLDE1NTEyMTQxNzIsOTEyMjY1ODI0LC0xOT
A4NDY0NTU5XX0=
-->