# Abstract Factory Design Pattern

## 🔹 What is the Abstract Factory Design Pattern?

The Abstract Factory pattern is a creational design pattern that provides an **interface for creating families of related or dependent objects** without specifying their concrete classes. It's like a factory of factories!

---

## 🔹 Real-World Analogy
Think of a furniture manufacturer that makes both modern and vintage furniture:
- They produce chairs, tables, and sofas (product families)
- Each piece comes in modern or vintage style (variants)
- You want complete sets in the same style (related objects)

---

## 🔹 Why use Abstract Factory?

- When your system needs to be independent of how its products are created
- When you need to create families of related products that should be used together
- When you want to provide a class library of products, revealing only their interfaces
- When you need to enforce constraints on product combinations

---

## 🔹 Example in Python

#### 🔹 Product Interfaces

```python
class Button:
    def render(self):
        pass

class Checkbox:
    def render(self):
        pass
```

#### 🔹 Concrete Products
```python
class WindowsButton(Button):
    def render(self):
        print("Rendering Windows-style Button.")

class MacButton(Button):
    def render(self):
        print("Rendering Mac-style Button.")

class WindowsCheckbox(Checkbox):
    def render(self):
        print("Rendering Windows-style Checkbox.")

class MacCheckbox(Checkbox):
    def render(self):
        print("Rendering Mac-style Checkbox.")
```

#### 🔹 Abstract Factory
```python
class GUIFactory:
    def create_button(self) -> Button:
        pass

    def create_checkbox(self) -> Checkbox:
        pass
```

#### 🔹 Concrete Factories
```python
class WindowsFactory(GUIFactory):
    def create_button(self) -> Button:
        return WindowsButton()

    def create_checkbox(self) -> Checkbox:
        return WindowsCheckbox()

class MacFactory(GUIFactory):
    def create_button(self) -> Button:
        return MacButton()

    def create_checkbox(self) -> Checkbox:
        return MacCheckbox()
```

#### 🔹 Client Code
```python
def render_ui(factory: GUIFactory):
    button = factory.create_button()
    checkbox = factory.create_checkbox()
    button.render()
    checkbox.render()

# Usage
os_type = "Mac"  # or "Windows"
factory = MacFactory() if os_type == "Mac" else WindowsFactory()
render_ui(factory)
```

---

### 🔹 Summary

Here, you're creating a **family of products** (`Button` + `Checkbox`) that are consistent with the same OS look-and-feel.

- This promotes **compatibility** between related UI components.
- New OS-specific components can be added by just implementing a **new concrete factory**.

---

## 🔹 Real-World Examples
- UI Toolkits: Creating UI elements for different operating systems
- Database Access: Creating connection objects for different database systems
- Vehicle Manufacturing: Creating parts for different vehicle models
- Cross-Platform Applications: Creating platform-specific components

---

## 🔹 Abstract Factory vs. Factory Method
- Factory Method: Creates a single product
- Abstract Factory: Creates entire families of related products

---
