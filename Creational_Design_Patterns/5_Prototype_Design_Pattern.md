
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

### 🏎️ Example: Car Manufacturing Molds

In automobile factories, once a prototype car body is designed and finalized, a **mold** is created.  
Rather than designing and welding a new car body each time from scratch, the company **clones** that body using the mold.

This saves time and cost while allowing **custom variations** like paint color, trims, or interior features.

**Prototype Pattern = Using a car body mol**
