# Strategy Design Pattern

## 🔹 What is the Strategy Pattern?

The **Strategy Pattern** allows you to **define a family of algorithms**, put each one in a **separate class**, and make them **interchangeable at runtime**.

It’s all about **choosing the right behavior dynamically**, without modifying the object that uses it.

---

## 🔹 Real-World Analogy: Google Maps Routes

When you're traveling from **Point A to B**, Google Maps offers you:

- Fastest route 🚗  
- Avoid tolls route 🛣️  
- Walk or cycle route 🚶‍♀️🚴‍♂️  

You (**the context**) can **switch between strategies** without changing how Google Maps works.

That’s Strategy Pattern: the **routing algorithm is selected at runtime** based on your preference.

---

## 🔹 Purpose

- Enable **easy swapping** of different algorithms or behaviors  
- Follow **Open/Closed Principle** – extend with new strategies, without changing the original code  
- Reduce **if-else clutter** when many variations of behavior exist  

---

## 🐍 Python Code Example : Google Maps Route Selector

```python
# Define the Strategy Interface
from abc import ABC, abstractmethod

class RouteStrategy(ABC):
    @abstractmethod
    def calculate_route(self, start, end):
        pass

# Create Concrete Strategies
class FastestRoute(RouteStrategy):
    def calculate_route(self, start, end):
        print(f"Calculating fastest route from {start} to {end} via highways.")

class ShortestRoute(RouteStrategy):
    def calculate_route(self, start, end):
        print(f"Calculating shortest route from {start} to {end} via local roads.")

class ScenicRoute(RouteStrategy):
    def calculate_route(self, start, end):
        print(f"Calculating scenic route from {start} to {end} through parks and lakes.")

# Context Class (Google Maps)
class GoogleMapsNavigator:
    def __init__(self, strategy: RouteStrategy):
        self.strategy = strategy

    def set_strategy(self, strategy: RouteStrategy):
        self.strategy = strategy

    def get_directions(self, start, end):
        self.strategy.calculate_route(start, end)

# Using the Strategy Pattern
# User selects fastest route
navigator = GoogleMapsNavigator(FastestRoute())
navigator.get_directions("Home", "Office")

# User changes preference to shortest route
navigator.set_strategy(ShortestRoute())
navigator.get_directions("Home", "Office")

# User changes to scenic route
navigator.set_strategy(ScenicRoute())
navigator.get_directions("Home", "Office")
```

**Output:**
```python
Calculating fastest route from Home to Office via highways.
Calculating shortest route from Home to Office via local roads.
Calculating scenic route from Home to Office through parks and lakes.
```

This is Strategy Pattern in action — dynamically switching algorithms (routes) **without modifying the navigator class**.

