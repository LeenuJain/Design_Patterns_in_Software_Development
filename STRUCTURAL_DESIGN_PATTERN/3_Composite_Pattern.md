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

The mechanic should be able to call the **same method**, like `.get_weight()`, on **both**.

That’s the **Composite Pattern** in action.

---

## 🔹 Key Idea

Create a **common interface** for both:

- **Leaf objects** → individual items  
- **Composite objects** → groups of items

---

## 🔹Examples

#### 🔹 Example 1: Grocery Shopping Bag

Imagine you're doing grocery shopping.

You buy individual items like:

- 🔹 Milk  
- 🔹 Bread  
- 🔹 Cheese  

You also buy a pack of fruits — a box containing:

- 🔹 Apple  
- 🔹 Banana  
- 🔹 Grapes  

Now you put everything into **one shopping bag**.

- **Leaf nodes**: Milk, Bread, Cheese, Apple, Banana, Grapes  
- **Composite node**: Fruit Pack (contains multiple items)  
- **Another Composite**: Shopping Bag (contains both individual items and packs)

**🐍 Python Code Example**
```python
# Base Component
class Item:
    def show(self):
        pass

# Leaf items
class Milk(Item):
    def show(self):
        print("Milk")

class Bread(Item):
    def show(self):
        print("Bread")

class Cheese(Item):
    def show(self):
        print("Cheese")

class Apple(Item):
    def show(self):
        print("Apple")

class Banana(Item):
    def show(self):
        print("Banana")

# Composite: Fruit Pack
class FruitPack(Item):
    def __init__(self):
        self.fruits = []

    def add(self, fruit: Item):
        self.fruits.append(fruit)

    def show(self):
        print("Fruit Pack:")
        for fruit in self.fruits:
            fruit.show()

# Composite: Shopping Bag
class ShoppingBag(Item):
    def __init__(self):
        self.items = []

    def add(self, item: Item):
        self.items.append(item)

    def show(self):
        print("Shopping Bag contains:")
        for item in self.items:
            item.show()

# Usage
milk = Milk()
bread = Bread()
cheese = Cheese()

fruit_pack = FruitPack()
fruit_pack.add(Apple())
fruit_pack.add(Banana())

bag = ShoppingBag()
bag.add(milk)
bag.add(bread)
bag.add(cheese)
bag.add(fruit_pack)

bag.show()
```

**Output:**
Shopping Bag contains:
Milk
Bread
Cheese
Fruit Pack:
Apple
Banana

So, when the cashier asks:

> “Show me what’s in your bag.”

You can just say:

```python
bag.show_items()
```

And whether it's a single item or a group (like the fruit pack), it’ll handle both uniformly. That’s Composite Pattern in real life!

---

#### 🔹 Example 2: File System (Folders & Files)

This is the classic example of the **Composite Pattern**:

- 🔹 **File** = Leaf  
- 🔹 **Folder** = Composite (can contain files or other folders)

When you call methods like `.open()` or `.get_size()` on a folder or a file, it works the **same way** — even though a folder might have **more content inside**.

You can loop through MyDocuments.show_all() and not worry about what’s inside — it handles both files and folders the same way.

**🐍 Python Code Example**
```python
# Base Component
class FileSystemItem:
    def show(self, indent=0):
        pass

# Leaf: File
class File(FileSystemItem):
    def __init__(self, name):
        self.name = name

    def show(self, indent=0):
        print("  " * indent + f"📄 {self.name}")

# Composite: Folder
class Folder(FileSystemItem):
    def __init__(self, name):
        self.name = name
        self.items = []

    def add(self, item: FileSystemItem):
        self.items.append(item)

    def show(self, indent=0):
        print("  " * indent + f"📁 {self.name}")
        for item in self.items:
            item.show(indent + 1)

# Usage
resume = File("resume.docx")
cover_letter = File("coverletter.pdf")
degree = File("degree.pdf")
internship = File("internship.pdf")

certificates = Folder("Certificates")
certificates.add(degree)
certificates.add(internship)

my_documents = Folder("MyDocuments")
my_documents.add(resume)
my_documents.add(cover_letter)
my_documents.add(certificates)

my_documents.show()
```

**Output:**
```python
📁 MyDocuments
  📄 resume.docx
  📄 coverletter.pdf
  📁 Certificates
    📄 degree.pdf
    📄 internship.pdf
```

---

## 🔹 Why Use It?

| **Benefit**             |  **Description**                                                |
|----------------------------|--------------------------------------------------------------------|
| ✅ **Uniformity**          | Treat individual and group objects the same                        |
| ✅ **Scalability**         | Add/remove parts easily                                            |
| ✅ **Hierarchical Structures** | Great for trees, folders, GUIs, car components, etc.            |

---

