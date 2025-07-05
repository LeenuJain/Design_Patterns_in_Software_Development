# Bridge Design Pattern

## 🔹 What is the Bridge Design Pattern?

The **Bridge Pattern** is used to *decouple an abstraction from its implementation*, so that the two can vary independently.

In simple terms:

> It lets you change what something does (**abstraction**) and *how* it does it (**implementation**) without affecting each other.

---

## 🔹 Real-World Analogy
**Car & Remote Control Analogy**
You can use the same **remote control** to start different types of cars — petrol, electric, hybrid.

- The **remote** is the **abstraction**.
- The **internal engine type** is the **implementation**.

**So:**
> You can add new remotes (abstractions) or new car types (implementations) *without changing the other*.

---

## 🔹 Why Use Bridge Pattern?

Because **inheritance can get messy fast**.

Let’s say you have:

- `Car` and `Bike`
- `ManualControl` and `AutoControl`

If you use inheritance, you end up with **4 classes**:

- `ManualCar`
- `AutoCar`
- `ManualBike`
- `AutoBike`

Using **Bridge**, you can separate:

- **Vehicle Type** from
- **Control System**

Now you only need:

- 2 vehicle types 
- 2 control types  
→ Combine them **flexibly**!

---

## 🐍 Python Code Example

```Python
# Implementation Interface
class Engine:
    def start_engine(self):
        pass

# Concrete Implementations
class PetrolEngine(Engine):
    def start_engine(self):
        print("Starting petrol engine...")

class ElectricEngine(Engine):
    def start_engine(self):
        print("Starting electric engine...")

# Abstraction
class Vehicle:
    def __init__(self, engine: Engine):
        self.engine = engine

    def start(self):
        print("Starting vehicle:")
        self.engine.start_engine()

# Refined Abstractions
class Car(Vehicle):
    def start(self):
        print("Car:")
        self.engine.start_engine()

class Truck(Vehicle):
    def start(self):
        print("Truck:")
        self.engine.start_engine()

# Using Bridge
petrol_car = Car(PetrolEngine())
electric_truck = Truck(ElectricEngine())

petrol_car.start()
electric_truck.start()
```

**Output:**
```python
Car:
Starting petrol engine...
Truck:
Starting electric engine...
```

---

## 🔹 Understanding "Abstraction" vs "Implementation" in the Bridge Pattern

In the **Bridge Pattern**, the term **"Abstraction"** doesn't always mean an *abstract class*, and **"Implementation"** doesn't always mean an *interface* or *low-level code* in the traditional OOP sense.

Let’s break this down clearly using the example we’ve been working with 👇

#### 🔹 Abstraction

- **Definition:** The high-level control layer or client-facing interface — what users interact with.
- **In Code:** `Vehicle`, `Car`, `Truck`
- **Responsibility:** Defines *what* we want to do — e.g., `"Start a vehicle"`

```python
class Vehicle:
    def __init__(self, engine: Engine):
        self.engine = engine

    def start(self):
        self.engine.start_engine()
```

**So here:**

- `Vehicle` is the **abstraction**
- It knows about the `Engine` (**implementation**)
- But it **doesn’t care how the engine actually works**


#### 🔹 Implementation

- **Definition:** The lower-level classes that actually do the work
- **In Code:** `Engine`, `PetrolEngine`, `ElectricEngine`
- **Responsibility:** Defines *how* the engine starts

```python
class Engine:
    def start_engine(self):
        pass

class PetrolEngine(Engine):
    def start_engine(self):
        print("Starting petrol engine...")
```

---

####  🔹 Putting It All Together
> “Let me connect the **abstraction layer** (like `Vehicle`) to the **implementation layer** (like `Engine`), so I can mix and match them without changing either side.”

---

## 🔹 Summary Table

| **Term**         | **In Our Code**                            | **Responsibility**                                |
|------------------|--------------------------------------------|---------------------------------------------------|
| **Abstraction**  | `Vehicle`, `Car`, `Truck`                  | What the object does — e.g., start a vehicle      |
| **Implementation** | `Engine`, `PetrolEngine`, `ElectricEngine` | How it is done — how the engine starts            |
| **Bridge**       | `Vehicle` holds an instance of `Engine`    | Connects both worlds                              |

---

## 🔹 Without the Bridge Pattern (Using Inheritance Only)

If we didn’t use the **Bridge Pattern**, we'd likely rely on **inheritance** to combine engine types with vehicle types.  
That means creating a new subclass for every combination, like:

- `PetrolCar`
- `ElectricCar`
- `PetrolTruck`
- `ElectricTruck`

This quickly leads to a bloated and rigid class hierarchy.

## 🐍 Python Code Example
```python
# Not using Bridge — Tight coupling via inheritance

# Base class
class Vehicle:
    def start(self):
        pass

# Subclasses for each combo
class PetrolCar(Vehicle):
    def start(self):
        print("Petrol Car: Starting petrol engine...")

class ElectricCar(Vehicle):
    def start(self):
        print("Electric Car: Starting electric engine...")

class PetrolTruck(Vehicle):
    def start(self):
        print("Petrol Truck: Starting petrol engine...")

class ElectricTruck(Vehicle):
    def start(self):
        print("Electric Truck: Starting electric engine...")
```
**Usage**
```python
car1 = PetrolCar()
truck1 = ElectricTruck()

car1.start()
truck1.start()
```

## 🔹 Downsides (Without Bridge)

| **Problem**         | **Why It Matters**                                                                 |
|---------------------|-------------------------------------------------------------------------------------|
| ❌ Class Explosion   | Adding a new vehicle type (e.g., `Bus`) or new engine type (e.g., `Hybrid`) creates tons of new classes |
| ❌ Tight Coupling    | Vehicle and Engine logic are tied together — harder to manage or test independently |
| ❌ Less Flexible     | Can't switch engine types at runtime — they're hardcoded in class names            |
| ❌ Poor Reuse        | Can't reuse engine logic across vehicles — duplicated `print` code everywhere       |

---


