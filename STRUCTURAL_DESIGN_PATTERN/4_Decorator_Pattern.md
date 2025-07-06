# 🔹 Decorator Pattern

## 🔹 What is it?

The **Decorator Pattern** allows you to add **new behavior or responsibilities** to objects at **runtime**, without modifying their existing code.

> It’s like adding layers — or toppings — to something without changing the original.

---

## 🔹 Real-World Analogy: Ice Cream Shop

Imagine you buy a basic scoop of ice cream 🍨  
Now you can add:

- 🔹 Chocolate syrup  
- 🔹 Strawberries  
- 🔹 Nuts  

Each topping **decorates** the ice cream, adding new features — but the original scoop stays **unchanged underneath**.

That’s exactly how the **Decorator Pattern** works.

---

## 🔹 Key Idea

Instead of **modifying** a class, we **wrap** it with other classes that add functionality.

- These **wrappers** implement the **same interface** as the original object.
- You can add **multiple layers** dynamically and flexibly.

---

## 🐍 Python Code Example: Car Wash Services

Let’s say you have a **basic car wash service**, and you can decorate it with:

-  Wax coating  
-  Interior cleaning  
-  Tire polishing  

```python
# Base Interface
class CarService:
    def get_description(self):
        pass

    def get_cost(self):
        pass

# Concrete Component (basic wash)
class BasicWash(CarService):
    def get_description(self):
        return "Basic Car Wash"

    def get_cost(self):
        return 300

# Decorators
class ServiceDecorator(CarService):
    def __init__(self, service: CarService):
        self.service = service

class WaxCoating(ServiceDecorator):
    def get_description(self):
        return self.service.get_description() + ", Wax Coating"

    def get_cost(self):
        return self.service.get_cost() + 150

class InteriorCleaning(ServiceDecorator):
    def get_description(self):
        return self.service.get_description() + ", Interior Cleaning"

    def get_cost(self):
        return self.service.get_cost() + 200

# Usage
# Base service
service = BasicWash()

# Add wax coating
service = WaxCoating(service)

# Add interior cleaning
service = InteriorCleaning(service)

print("Service:", service.get_description())
print("Total Cost: ₹", service.get_cost())
```

**Output**
```python
Service: Basic Car Wash, Wax Coating, Interior Cleaning
Total Cost: ₹ 650
```

---

# ---

# 🔹 Python Decorator vs Decorator Pattern

The term **"decorator"** in Python can refer to **two different concepts**:

---

#### 🔹 1. Design Pattern: Decorator Pattern

- The one you're learning now — a **Structural Design Pattern**
- It’s **language-agnostic** (used in Java, C++, etc.)
- It involves **wrapping objects** at runtime to **add behavior**

---

#### 🔹 2. Python’s `@decorator` Syntax

- This is **Python-specific syntax sugar**
- Used to **wrap functions or methods** to add behavior (like logging, timing, validation)
- Looks like this:

```python
@my_decorator
def say_hello():
    print("Hello!")
```

---

## 🔹 Are They Related?

✅ Yes — in concept, they’re **similar**:

-  Both **wrap something** (object or function)
-  Both **add new behavior** without changing the original code

But they are used in **different ways**:

---

### 🔹 Comparison Table

| **Feature**      | **Design Pattern Decorator**      | **Python `@decorator`**                      |
|---------------------|---------------------------------------|-------------------------------------------------|
| Used On             | Objects / Classes                     | Functions / Methods                             |
| Purpose             | Add behavior at **runtime**           | Add behavior at **definition time**             |
| Syntax              | Manually wrapping classes             | `@decorator` syntax                             |
| Common Use          | Car wash, GUI elements, I/O streams   | Logging, authentication, caching                |

---

### 🔹 Can We Use Python’s `@decorator` for the Decorator Pattern?

- **Not directly.**

Because:

- Python decorators (`@`) work on **functions or methods** — not on objects
- But if your goal is to **decorate behavior**, Python decorators can **simulate similar behavior** — at the **function level**

---

## 🔹 Final Takeaway

- Use Python decorators (`@`) when you're decorating functions.
- Use the Decorator Design Pattern when you're decorating objects/classes.
- They’re conceptually similar, but technically different tools.

---
