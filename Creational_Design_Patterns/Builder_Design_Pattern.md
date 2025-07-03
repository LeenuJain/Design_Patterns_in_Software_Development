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

## 📦 Summary

> **Builder Pattern** helps construct complex objects **step-by-step** while hiding the construction logic from the user.
