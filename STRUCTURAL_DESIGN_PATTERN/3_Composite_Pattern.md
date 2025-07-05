# 🔹Composite Design Pattern

## 🔹 What is it?

The **Composite Pattern** lets you treat **individual objects** and **groups of objects** in the same way.

It’s like saying:

> “I don’t care whether it’s a single item or a group — I’ll handle them the same.”

---

## 🔹 Real-World Analogy: Car Parts

Imagine a car:

- You have simple parts like **nuts and bolts**
- You have assemblies like the **engine**, which itself contains many parts

Now if a mechanic wants to *“inspect a part”* or *“get weight of a part”*, it **shouldn’t matter whether it’s**:

- A single part (e.g., a **bolt**), or
- A group of parts (e.g., the **engine**)

✅ The mechanic should be able to call the **same method**, like `.get_weight()`, on **both**.

That’s the **Composite Pattern** in action.

---

## 🔹 Key Idea

Create a **common interface** for both:

- **Leaf objects** → individual items  
- **Composite objects** → groups of items

---

## 🐍 Python Code Example
```python
# Component Interface
class CarComponent:
    def show_details(self):
        pass

# Leaf Classes (individual parts)
class Wheel(CarComponent):
    def show_details(self):
        print("Wheel")

class Engine(CarComponent):
    def show_details(self):
        print("Engine")

#  Composite Class (group of parts)
class Car(CarComponent):
    def __init__(self):
        self.parts = []

    def add_part(self, part: CarComponent):
        self.parts.append(part)

    def show_details(self):
        print("Car parts:")
        for part in self.parts:
            part.show_details()

# Usage
wheel1 = Wheel()
wheel2 = Wheel()
engine = Engine()

my_car = Car()
my_car.add_part(wheel1)
my_car.add_part(wheel2)
my_car.add_part(engine)

my_car.show_details()
```

**Output:**
```python
Car parts:
Wheel
Wheel
Engine
```

---

## 🔹 Why Use It?

| **Benefit**             |  **Description**                                                |
|----------------------------|--------------------------------------------------------------------|
| ✅ **Uniformity**          | Treat individual and group objects the same                        |
| ✅ **Scalability**         | Add/remove parts easily                                            |
| ✅ **Hierarchical Structures** | Great for trees, folders, GUIs, car components, etc.            |

