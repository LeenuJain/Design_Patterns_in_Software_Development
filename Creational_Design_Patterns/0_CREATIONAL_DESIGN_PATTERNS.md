# 🧱 What are Creational Design Patterns?

Creational design patterns deal with **object creation mechanisms**, trying to create objects in a manner suitable to the situation.

They help:

- Hide the **creation logic**
- Increase **flexibility** and **reuse**
- Avoid **tight coupling** between classes and the objects they create

---

## 🧩 Types of Creational Design Patterns

There are **five main types**:  
![Creational Design Patterns](Images/Creational_Design_Patterns.webp)  

| Pattern              | Purpose                                                                 | Example Use Case                          | Notes Link                                |
|----------------------|-------------------------------------------------------------------------|--------------------------------------------|--------------------------------------------|
| **1. Singleton**      | Ensures a class has only one instance, and provides global access to it | Database connection, logger                | [View Notes](2_Singleton_Design_Pattern.md)  |
| **2. Factory Method** | Lets subclasses decide which class to instantiate                       | GUI buttons for different OS               | [View Notes](3_Factory_Method_&_Abstract_Factory.md) |
| **3. Abstract Factory** | Creates families of related objects without specifying concrete classes | UI themes, cross-platform UI kits          | [View Notes](3_Factory_Method_&_Abstract_Factory.md) |
| **4. Builder**         | Separates complex object construction from its representation           | Building a house or creating an HTML page  | [View Notes](4_Builder_Design_Pattern.md)    |
| **5. Prototype**       | Creates new objects by copying an existing object (clone)               | Copying game characters, settings profiles | [View Notes](5_Prototype_Design_Pattern.md)  |

