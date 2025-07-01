
# Singleton Design Pattern

## 🔹 What is the Singleton Pattern?

The **Singleton Pattern** is a **creational design pattern** that ensures a class has **only one instance** and provides a **global point of access** to that instance.

Think of it like a **manager** in a company — there should be only **one manager** for a department, and everyone should refer to the **same manager**.

---

## 🔹 Real-World Analogy
Imagine a water tank in a building. If every apartment builds its own tank, it wastes space, money, and water pressure. Instead, having one shared tank is efficient and manageable — just like a singleton database connection.   

---

## 🔹 Why Use Singleton?

- To **control access** to shared resources (like a database or a file).
- To **save memory** by avoiding multiple instances.
- To ensure **consistent behavior** across the application.
- Use case : a logging system, configuration manager, or connection pool is often implemented using Singleton.

---

## 🔹 Singleton in Code (Python Example)

### 1. Simple example:

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            print("Creating new instance...")
            cls._instance = super(Singleton, cls).__new__(cls)
        return cls._instance

# Usage
obj1 = Singleton()
obj2 = Singleton()

print(obj1 is obj2)  # True

```
**Output:**   
Creating new instance...    
True
   
Even though we tried to create two objects, both obj1 and obj2 point to the same instance.   
   
### 2. Database connection example:   
```python
import sqlite3

class DatabaseManager:
    # Class variable to hold our single instance
    _instance = None
    
    def __new__(cls):
        # If we don't have an instance yet, create one
        if cls._instance is None:
            print("Creating a new DatabaseManager instance")
            # Create the instance using the parent class's __new__
            cls._instance = super().__new__(cls)
            # Initialize the connection to None
            cls._instance.connection = None
        return cls._instance
    
    def connect(self):
        """Connect to the database if not already connected"""
        if self.connection is None:
            print("Creating a new database connection")
            self.connection = sqlite3.connect("example.db")
            # Create a cursor for executing SQL commands
            cursor = self.connection.cursor()
            # Create a table if it doesn't exist
            cursor.execute('''
                CREATE TABLE IF NOT EXISTS users (
                    id INTEGER PRIMARY KEY,
                    name TEXT,
                    email TEXT
                )
            ''')
            self.connection.commit()
        return self.connection
    
    def add_user(self, name, email):
        """Add a user to the database"""
        conn = self.connect()
        cursor = conn.cursor()
        cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", (name, email))
        conn.commit()
        print(f"Added user: {name} with email: {email}")
    
    def get_all_users(self):
        """Get all users from the database"""
        conn = self.connect()
        cursor = conn.cursor()
        cursor.execute("SELECT * FROM users")
        return cursor.fetchall()
    
    def close(self):
        """Close the database connection"""
        if self.connection:
            self.connection.close()
            self.connection = None
            print("Database connection closed")
```

**Usage**
```python
def register_user(name, email):
    print("\n--- Registering User ---")
    db = DatabaseManager()
    print(f"In register_user(), db object ID: {id(db)}")
    db.add_user(name, email)

def list_all_users():
    print("\n--- Listing All Users ---")
    db = DatabaseManager()
    print(f"In list_all_users(), db object ID: {id(db)}")
    users = db.get_all_users()
    print(f"Found {len(users)} users")

def shutdown_app():
    print("\n--- Shutting Down App ---")
    db = DatabaseManager()
    print(f"In shutdown_app(), db object ID: {id(db)}")
    db.close()

# Let's demonstrate
if __name__ == "__main__":
    register_user("Alice", "<EMAIL_ADDRESS>")
    register_user("Bob", "<EMAIL_ADDRESS>")
    list_all_users()
    shutdown_app()
    
    db1 = DatabaseManager()
    print(f"db1 object ID: {id(db1)}")
    
    db2 = DatabaseManager()
    print(f"db2 object ID: {id(db2)}")
    
    print(f"Are all objects the same? {id(db1) == id(db2)}")

```
**Output**
```python
--- Registering User ---
Creating a new DatabaseManager instance
Instance ID: 140362541235680
In register_user(), db object ID: 140362541235680
Creating a new database connection
Added user: Alice with email: <EMAIL_ADDRESS>

--- Registering User ---
Reusing existing instance with ID: 140362541235680
In register_user(), db object ID: 140362541235680
Added user: Bob with email: <EMAIL_ADDRESS>

--- Listing All Users ---
Reusing existing instance with ID: 140362541235680
In list_all_users(), db object ID: 140362541235680
Found 2 users

--- Shutting Down App ---
Reusing existing instance with ID: 140362541235680
In shutdown_app(), db object ID: 140362541235680
Database connection closed

Reusing existing instance with ID: 140362541235680
db1 object ID: 140362541235680

Reusing existing instance with ID: 140362541235680
db2 object ID: 140362541235680

Are all objects the same? True

```
**What's Happening**   
- The first time DatabaseManager() is called in register_user(), a new instance is created  
- Every subsequent call to DatabaseManager() returns that same instance   
- All the object IDs are identical because they are the same object in memory 

**Note**    
- There are several ways to implement the Singleton Design Pattern, depending on the programming language and specific requirements like thread safety, lazy initialization, and performance.  
- Foucusing on python above example we were using __new__ Method. we can also achieve using decorator, metaclass, module etc.

---

## 🔹 What Happens If a Database Object Is Created Multiple Times?    
If you create multiple instances of a database connection object, several problems can occur:   
**1. Resource Overload**     
Each database connection consumes memory, CPU, and network resources.      
Creating many connections can overload the database server, leading to slower performance or even crashes.   
**2. Inconsistent Data**   
If different parts of your application use different connections, they might not see the same data at the same time.   
For example, one connection might not see changes made by another until a transaction is committed.   
**3. Connection Limits**       
Most databases have a maximum number of connections allowed.   
If your app creates a new connection every time, you might hit that limit, and new requests will fail.   
**4. Harder to Manage**   
Debugging and managing multiple connections is complex.   
It’s harder to track issues, log activity, or close connections properly.   

---

## 🔹 Why Use a Singleton for Database Connections?   
Using a Singleton ensures that:  
✅ Only one connection is created and reused.  
✅ It’s efficient — saves memory and CPU.  
✅ It’s safe — avoids hitting connection limits.  
✅ It’s consistent — all parts of the app use the same connection.  

---

## 🔹 Key Points
- The constructor is private or controlled.   
- A static method or class method is used to get the instance.   
- Only one object is created and reused.   

---

# Factory Method Pattern

## 🔹 What is the Factory Method Pattern?

The **Factory Method Pattern** is a **creational design pattern** that provides an **interface for creating objects**, but **allows subclasses to alter the type of objects that will be created**.

Instead of calling a constructor directly to create an object, you use a **factory method**. This helps in **decoupling the object creation logic** from the code that uses the object.

---

## 🔹 Real-Life Analogy

Imagine a **pizza store**. You don’t make the pizza yourself — you just **order** it. The store decides **how** to make it based on the type you asked for (Margherita, Pepperoni, etc.).

The **pizza store** is the **factory**, and the **pizza** is the **product**.

---

## 🔹 Why Use Factory Method?

- To **encapsulate object creation logic**.
- To **promote loose coupling** between client code and concrete classes.
- To make code **easier to maintain and extend**.

---

## 🔹 Factory Method in Code (Python Example)

### 1. Building a **logistics system** that can deliver by **truck** or **ship**.

### Step 1: Define the Product Interface

```python
class Transport:
    def deliver(self):
        pass
``` 
### Step 2 : Step 2: Create Concrete Products
```python
class Truck(Transport):
    def deliver(self):
        return "Delivering by land in a truck."

class Ship(Transport):
    def deliver(self):
        return "Delivering by sea in a ship."
```
### Step 3 : Create the Factory
```python
class Logistics:
    def create_transport(self):
        pass

class RoadLogistics(Logistics):
    def create_transport(self):
        return Truck()

class SeaLogistics(Logistics):
    def create_transport(self):
        return Ship()
```
### Step 4 : Client Code
```python
def plan_delivery(logistics: Logistics):
    transport = logistics.create_transport()
    print(transport.deliver())

# Usage
plan_delivery(RoadLogistics())  # Output: Delivering by land in a truck.
plan_delivery(SeaLogistics())   # Output: Delivering by sea in a ship.
```
### Why This is Useful
- The client code uses the **factory method**, not the **constructor**.   
- You can add new product types without changing the client code.   
- It follows the Open/Closed Principle — open for extension, closed for modification.    


### 2.  Building a Notification System. 
- Depending on the user's preference, the system should send a notification via Email, SMS, or Push Notification.    
- Now, instead of writing if-else everywhere to decide which notification to send, we use the Factory Method Pattern to make the code clean, flexible, and easy to extend.   

### Step 1: Create a Common Interface   
All notification types should have a common method, like notify().   
```python
class Notification:
    def notify(self, message):
        pass
```
### Step 2: Create Concrete Classes   
Each class implements the notify() method in its own way.   
```python
class EmailNotification(Notification):
    def notify(self, message):
        print(f"Sending Email: {message}")

class SMSNotification(Notification):
    def notify(self, message):
        print(f"Sending SMS: {message}")

class PushNotification(Notification):
    def notify(self, message):
        print(f"Sending Push Notification: {message}")
```
### Step 3: Create the Factory   
This factory decides which notification object to create.  
```python
class NotificationFactory:
    def create_notification(self, channel):
        if channel == "email":
            return EmailNotification()
        elif channel == "sms":
            return SMSNotification()
        elif channel == "push":
            return PushNotification()
        else:
            raise ValueError("Unknown notification channel")
```
### Step 4: Client Code (You Use the Factory)
```python
# Client code
factory = NotificationFactory()

# Let's say user wants SMS
user_preference = "sms"
notifier = factory.create_notification(user_preference)
notifier.notify("Your order has been shipped!")
```
**Output:**
Sending SMS: Your order has been shipped!

### Why This is Useful   
- You don’t need to change the client code if a new notification type is added.   
- You avoid messy if-else or switch statements everywhere.   
- You follow the Open/Closed Principle: open for extension, closed for modification.   


