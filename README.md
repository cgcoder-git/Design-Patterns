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
    # global private variable
    _instance = None

    """
    Handle conditions:
    1. Globaly accessible private variable
    1. if no instance initialized, init one
    2. if already an instance exist, return the existing one
    """
    def __new__(cls):
        if cls._instance == None:
            # instance not initialized
            cls._instance = super().__new__(cls)
            print("Initialized")
            return cls._instance
        else:
            # if already initialized
            print("Already there, So Returning existing one")
            return cls._instance
        
    @staticmethod
    def calculate_area():
        print("Area Calculated")

if __name__ == "__main__":
    obj1 = Singleton()
    obj1.calculate_area()
    obj2 = Singleton()
    obj2.calculate_area()

"""
Initialized
Area Calculated
Already there, So Returning existing one
Area Calculated
"""
```
**Using Decorators**
Decorators allow us to wrap another function in order to extend the behavior of the wrapped function.

```python
def singleton_wrap(cls):
    _instance = {}
    def set_instance():
        if cls not in _instance:
            _instance[cls] = cls()
            print("Instance Initialized")
        else:
            print("Already Initialized")
    return set_instance


@singleton_wrap
class SingletonDecor:
    def __init__(self):
        print("Instance Created")
    
if __name__ == "__main__":
    obj1 = SingletonDecor()
    obj2 = SingletonDecor()

"""
Instance Created
Instance Initialized
Already Initialized
"""
```

**Singleton & Multithreading** : 
when dealing with multithreading in singleton,it's pretty tricky, as the concept is to have a one and only one instance/object at a time, multithreading breaks it , as it create two instance at the same time, to prevent that we need to take certain measures. here is the example - 1st without handling & 2nd with handling.

```python
from threading import Thread
import time

class Singleton:
    # global private variable
    _instance = None
    """
    Handle conditions:
    1. Globaly accessible private variable
    1. if no instance initialized, init one
    2. if already an instance exist, return the existing one
    """
    def __new__(cls):
        if cls._instance == None:
            # instance not initialized
            time.sleep(0.1)
            cls._instance = super().__new__(cls)
            print("Initialized")
            return cls._instance
        else:
            # if already initialized
            print("Already there, So Returning existing one")
            return cls._instance
        
    @staticmethod
    def calculate_area():
        print("Area Calculated")

def create_instance():
    sq = Singleton()
    print(f"instance id : {id(sq)}")

if __name__ == "__main__":
    threads  =[]
    for _ in range(3):
        t = Thread(target=create_instance)
        threads.append(t)
        t.start()
    
    for t in threads:
        t.join()

"""
Initialized
instance id : 1827982004432
Initialized
instance id : 1827982004096
Initialized
instance id : 1827982004288
"""
```
- Added sleep time because adding a delay forces the issue and shows that multiple instances can be created.
- Without sleep your code might not fail due to GIL(Global interpreter Lock) & thread Scheduling.
- to Resolve this we can use lock (threading.Lock()) to properly synchronize instance creation, but it is costly as its a system call.
**With Lock**

```python
from threading import Thread, Lock
import time

class Singleton:
    # global private variable
    _instance = None
    _lock = Lock()

    """
    Handle conditions:
    1. Globaly accessible private variable
    1. if no instance initialized, init one
    2. if already an instance exist, return the existing one
    """
    def __new__(cls):
        with cls._lock:
            if cls._instance == None:
                # instance not initialized
                time.sleep(0.1)
                cls._instance = super().__new__(cls)
                print("Initialized")
            else:
                # if already initialized
                print("Already there, So Returning existing one")
        return cls._instance
        
    @staticmethod
    def calculate_area():
        print("Area Calculated")

def create_instance():
    sq = Singleton()
    print(f"instance id : {id(sq)}")

if __name__ == "__main__":
    threads  =[]
    for _ in range(3):
        t = Thread(target=create_instance)
        threads.append(t)
        t.start()
    
    for t in threads:
        t.join()

"""
Initialized
instance id : 2964932973136
Already there, So Returning existing one
instance id : 2964932973136
Already there, So Returning existing one
instance id : 2964932973136
"""
```
Lock() ensures that only one thread can enter the __new__() method at a time. if one is already inside, others will wait until it finishes.
