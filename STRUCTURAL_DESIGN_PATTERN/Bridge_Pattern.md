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



