# 🔹 Flyweight Design Pattern

## 🔹 What is it?

The **Flyweight Pattern** is used to **minimize memory usage** by sharing **common data** between multiple similar objects instead of creating duplicates.

It’s perfect when you have a **large number of objects** that share common properties.

---

## 🔹 Real-World Analogy: Text Editor Characters

Imagine you're typing this sentence:  
**Hello World**
Each letter on the screen is an object, right?
If the system creates a **new object for every letter**, it will waste a lot of memory — especially if letters repeat!

So instead:

- All `'l'` characters **share one object** (the shape/structure of "l")  
- The only thing that changes is **position**, **size**, or **color**

✅ That’s **Flyweight** in action.

---

## 🔹 Core Idea

Separate the **intrinsic state** (shared data) from the **extrinsic state** (unique data per instance).

---

## 🐍 Python Code Example : 
 Car Production System (Color Flyweight)
Imagine a factory that makes thousands of cars, but many cars have the same color.
Instead of storing color info again and again, we reuse it.

```python 
#  Flyweight (shared object)
class CarColor:
    def __init__(self, color_name):
        self.color_name = color_name

    def apply_color(self, car_model):
        print(f"Applying {self.color_name} color to {car_model}")

#  Flyweight Factory 
class ColorFactory:
    _colors = {}

    @classmethod
    def get_color(cls, color_name):
        if color_name not in cls._colors:
            cls._colors[color_name] = CarColor(color_name)
        return cls._colors[color_name]

# Client Code
# Let's create 5 cars
models = ["Sedan", "SUV", "Truck", "SUV", "Sedan"]
colors = ["Red", "Blue", "Red", "Red", "Blue"]

for model, color in zip(models, colors):
    color_obj = ColorFactory.get_color(color)  # Get shared color
    color_obj.apply_color(model)
```

**Output:**
```python
Applying Red color to Sedan
Applying Blue color to SUV
Applying Red color to Truck
Applying Red color to SUV
Applying Blue color to Sedan
```

---

## 🔹 Benefits of Flyweight

| Benefit             | Description                                      |
|---------------------|--------------------------------------------------|
| Low memory          | Reuse objects instead of creating new ones       |
| Better performance  | Less RAM = faster system                         |
| Scalable            | Works great when millions of similar objects are needed |

---

## 🔹 When to Use Flyweight

- When you create a **lot of similar objects**
- When object data is **mostly shared**
- When **performance or memory usage** matters (e.g., games, graphics, editors)

---
