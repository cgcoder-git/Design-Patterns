# Design-Patterns
- Before diving into the actual definition, let me first explain the concept of design patterns. It follows the idea of **"Why reinvent the wheel?"** —meaning, if something has already been developed and refined by others, why go through the hassle of creating it from scratch? Similarly, **design patterns** are tried-and-tested solutions to common design problems faced by engineers. These solutions have been documented, refined, and standardized over time, forming what we call design patterns —a collection of best practices to streamline software development.
- It's not mandatory that you will encounter only these specific problems, but learning design patterns can significantly enhance your understanding of software design. They help you approach problem-solving more effectively and rethink your architecture with better clarity. In simple terms, mastering design patterns gives you an edge in writing scalable and maintainable code
## Definition: 
Design patterns are typical solutions to commonly occurring problems in software design. They are like pre-made blueprints that you can customize to solve a recurring design problem in your code.

## Types of Design Patterns
1. Creational Design Patterns
2. Structural Design Patterns
3. Behavioral Design Pattrens

## Diagram :
  
![image](https://github.com/user-attachments/assets/94237aa0-c083-47da-b22d-aca36bf3ff6c)

# Creational Design Pattern
- As name suggest Creational Design pattern mainly deal with the creation of the object.
A creational design pattern is a type of design pattern in software engineering that deals with object creation mechanisms, aiming to create objects in a manner suitable to the situation. These patterns help make a system independent of how its objects are created, composed, and represented, while also promoting flexibility and reuse of code.

## Let's see Creational Design Patterns - 
1. Singleton Pattern
2. Factory Method Pattern
3. Abstract Factory Pattern
4. Builder Pattern
5. Prototype Pattern

## Singleton Pattern
- Singleton suggest that, **one and only one** object/instance should be created.
- The Singleton Pattern restricts a class to a single instance and provides a way to access that instance globally.
- Think of this like, there is a centralized printer which is accessible by every department, so provides a global access but only one instance can use it at a time.

**There are two ways mainly, one is using static methods and another is using decorator**
```python
class Singleton:
    pass
```
