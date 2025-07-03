
## ❓ What is the Prototype Pattern?

The **Prototype Pattern** is used when you want to create a **copy (clone)** of an existing object instead of building it from scratch.

This is especially useful when:

- Object creation is **expensive or slow**
- You want many **similar objects**, with small changes

---

## 🧠 Real-World Analogy

### 🧸 Example: Making Toy Models

Imagine a toy company makes a prototype of a new toy car.  
Instead of designing each new car from scratch, they just **clone the prototype** and slightly modify the copies (color, wheels, etc.).

---

## 🔁 Key Idea

- Instead of calling `new`, we call `.clone()`
- We **copy an existing object** instead of creating a fresh one

---

## 🧩 Components in Prototype Pattern

| **Concept**        | **Description**                                      |
|--------------------|------------------------------------------------------|
| `Prototype`        | Interface or base class with a `clone()` method      |
| `ConcretePrototype`| Actual class that implements cloning logic           |
| `Client`           | Uses the prototype to create a copy                  |

---

## 🚗 Real-Time Analogy (Automobile Example)

### 🏎️ Example 1: Car Manufacturing Molds

In automobile factories, once a prototype car body is designed and finalized, a **mold** is created.  
Rather than designing and welding a new car body each time from scratch, the company **clones** that body using the mold.

This saves time and cost while allowing **custom variations** like paint color, trims, or interior features.

**Prototype Pattern = Using a car body mol**

### Example 2: Making an ID Card
You don’t print and cut a new card every time from scratch.
You just photocopy a template and change name/photo.

- 🖨️ Photocopy = fast
- 👷 Building new from scratch = slow, repetitive, error-prone

---

## 🔹 Singleton in Code (Python Example)

### 1. Simple example:
```python
import copy

# 🔹 Prototype Base Class
class Prototype:
    def clone(self):
        return copy.deepcopy(self)

# 🔹 Concrete Class
class Document(Prototype):
    def __init__(self, title, content, author):
        self.title = title
        self.content = content
        self.author = author

    def display(self):
        print(f"Title  : {self.title}")
        print(f"Author : {self.author}")
        print(f"Content: {self.content}")
        print("-" * 30)

# 🔹 Client Code
if __name__ == "__main__":
    # Create an original document (a template)
    template_doc = Document("Newsletter Template", "This is a template", "Admin")

    print("📄 Original Document:")
    template_doc.display()

    # Clone it and modify a few fields
    user_doc = template_doc.clone()
    user_doc.title = "July Newsletter"
    user_doc.author = "Leenu"
    user_doc.content = "Welcome to the July edition!"

    print("📄 Cloned & Customized Document:")
    user_doc.display()
    template_doc.display()
```
**Output:**
```python
📄 Original Document:
Title  : Newsletter Template
Author : Admin
Content: This is a template
------------------------------
📄 Cloned & Customized Document:
Title  : July Newsletter
Author : Leenu
Content: Welcome to the July edition!
------------------------------
Title  : Newsletter Template
Author : Admin
Content: This is a template
```

### 🧠 What Happened?

- We created a `Document` instance → `template_doc`
- We called `.clone()` → got a deep copy
- Then changed `title`, `author`, and `content` → without affecting the original

This is the **Prototype Pattern** in action.

---


