# 🧱 Builder Design Pattern   

The **Builder Pattern** is used to construct **complex objects step-by-step**.

- Separates object construction from its representation.
- Allows building different variations of the same object.

---

## 🧠 Real-World Analogy: Ordering Pizza 🍕

Imagine you’re ordering a custom pizza:

1. Choose the **size** (small, medium, large)  
2. Choose the **crust** (thin, thick)  
3. Add **toppings** (cheese, mushrooms, olives)  
4. Add **extras** (basil, sauces)

You make choices step-by-step — the pizza is built progressively.

➡️ This is how the **Builder Pattern** works.

---

## 🧩 Key Concepts

- **Product**  
  The object being built (e.g., `Pizza`, `Button`, `Car`)  
  Contains many parts or attributes.

- **Builder**  
  Defines step-by-step methods to configure parts  
  (e.g., `set_size()`, `set_color()`)

- **build()**  
  Final method to return the completed object.

- **Director (optional)**  
  Coordinates the building process (not always required).

---

## 🔄 Why Use Builder?

| Problem                             | Builder Helps By                      |
|-------------------------------------|----------------------------------------|
| Too many constructor parameters     | Step-by-step building methods          |
| Need to configure only some fields  | Skip unnecessary steps                 |
| Want more readable construction     | Fluent and expressive method chaining  |
| Complex object initialization logic | Keeps logic separated from the object  |

---

## 📌 Benefits

- ✅ Clean and readable object creation  
- ✅ Avoids huge messy constructors  
- ✅ Supports optional and required fields  
- ✅ Works well with complex objects  
- ✅ Promotes immutability (if used wisely)

---

## ❗ When NOT to Use

- Object is simple and doesn't need customization  
- Only a few attributes are needed  
- Constructor alone is enough

---
## Example in python
Lets consider again an exmaple to create and customize GUI components like a Button.  
```python
class Button:
    def __init__(self):
        self.color = "default"
        self.size = "medium"
        self.shape = "rectangle"
        self.text = "Button"

    def display(self):
        print(f"Displaying a {self.size} {self.shape} button in {self.color} with text '{self.text}'")

# 🔹 Concrete Products
class WindowsButton(Button):
    def display(self):
        print(f"[Windows] Displaying a {self.size} {self.shape} button in {self.color} with text '{self.text}'")

class MacButton(Button):
    def display(self):
        print(f"[Mac] Displaying a {self.size} {self.shape} button in {self.color} with text '{self.text}'")

# 🔹 Builder Class
class ButtonBuilder:
    def __init__(self, button: Button):
        self.button = button

    def set_color(self, color):
        self.button.color = color
        return self

    def set_size(self, size):
        self.button.size = size
        return self

    def set_shape(self, shape):
        self.button.shape = shape
        return self

    def set_text(self, text):
        self.button.text = text
        return self

    def build(self):
        return self.button

# 🔹 Factory Method - Creator
class Dialog:
    def create_button(self) -> Button:
        pass

    def create_and_display_button(self, color, size, shape, text):
        print("\n🔧 create_and_display_button() called")
        print("→ Creating button using factory...")
        button = self.create_button()
        print(f"✔ Got button of type: {type(button).__name__}")

        print("→ Customizing button using builder...")
        builder = ButtonBuilder(button)
        custom_button = (
            builder
            .set_color(color)
            .set_size(size)
            .set_shape(shape)
            .set_text(text)
            .build()
        )

        print("→ Finally displaying the customized button:")
        custom_button.display()

# 🔹 Concrete Factories
class WindowsDialog(Dialog):
    def create_button(self) -> Button:
        print("🏭 Factory: Creating WindowsButton")
        return WindowsButton()

class MacDialog(Dialog):
    def create_button(self) -> Button:
        print("🏭 Factory: Creating MacButton")
        return MacButton()

# 🔹 Client Code
if __name__ == "__main__":
    os_type = "Mac"  # Try "Windows" or "Mac"

    print(f"\n🌐 OS Type: {os_type}")
    dialog = WindowsDialog() if os_type == "Windows" else MacDialog()

    # ✅ User specifies what kind of button they want
    dialog.create_and_display_button(
        color="green",
        size="small",
        shape="square",
        text="Cancel"
    )
```

### 🔍 What This Code Does

- `Button` is the base class with default styles and a `display()` method.
- `WindowsButton` and `MacButton` are concrete subclasses with OS-specific display logic.
- `ButtonBuilder` allows setting properties of a button step-by-step using method chaining.
- `Dialog` is the creator (abstract factory) that defines a method `create_button()` to be implemented by concrete factories.
- `WindowsDialog` and `MacDialog` implement `create_button()` and return platform-specific button objects.
- `create_and_display_button()` method combines both patterns — it creates a button (Factory Method) and then customizes it (Builder Pattern).
- The **client** decides what kind of button they want and passes those details as arguments.

---

### Note:

This example demonstrates how the Builder Pattern and Factory Method Pattern can be used together to create and customize GUI components like a Button.    
- The Factory Method Pattern helps determine which type of button to create (WindowsButton or MacButton) based on the platform.   
- The Builder Pattern allows the client to customize the button's attributes like color, size, shape, and text step-by-step in a clean and flexible way.  

---
