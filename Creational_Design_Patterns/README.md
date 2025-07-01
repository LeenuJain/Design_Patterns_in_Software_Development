
# Singleton Design Pattern in Python

## 🔹 What is the Singleton Pattern?

The **Singleton Pattern** is a **creational design pattern** that ensures a class has **only one instance** and provides a **global point of access** to that instance.

Think of it like a **manager** in a company — there should be only **one manager** for a department, and everyone should refer to the **same manager**.

---

## 🔹 Why Use Singleton?

- To **control access** to shared resources (like a database or a file).
- To **save memory** by avoiding multiple instances.
- To ensure **consistent behavior** across the application.

---

## 🔹 Singleton in Code (Python Example)

Here’s a simple Python example:

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            print("Creating new instance...")
            cls._instance = super(Singleton, cls).__new__(cls)
        return cls._instance

# Usage
obj1 = Singleton()
obj2 = Singleton()

print(obj1 is obj2)  # True

```

## Output:
Creating new instance...
True
Even though we tried to create two objects, both obj1 and obj2 point to the same instance.

---

## 🔹 Key Points
The constructor is private or controlled.
A static method or class method is used to get the instance.
Only one object is created and reused.

---


