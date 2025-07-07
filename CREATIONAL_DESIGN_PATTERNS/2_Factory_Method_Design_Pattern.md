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
### 1. Encapsulation of Object Creation
- You hide the logic of how objects are created.
- The client code doesn't need to know the exact class name or how to instantiate it.
### 2. Loose Coupling
- The client code depends on an interface or abstract class, not on specific implementations.
- This makes your code easier to change or extend.
### 3. Easier to Add New Types
- You can add new product types (e.g., new notification types) without changing existing code.
- This follows the Open/Closed Principle — open for extension, closed for modification.
### 4. Improved Maintainability
- Centralizes object creation logic in one place (the factory).
- Makes the codebase cleaner and easier to manage.

---

## 🔹 Factory Method in Code (Python Example)

### 1. Building a **logistics system** that can deliver by **truck** or **ship**.

**Step 1: Define the Product Interface**

```python
class Transport:
    def deliver(self):
        pass
``` 
**Step 2 : Step 2: Create Concrete Products**
```python
class Truck(Transport):
    def deliver(self):
        return "Delivering by land in a truck."

class Ship(Transport):
    def deliver(self):
        return "Delivering by sea in a ship."
```
**Step 3 : Create the Factory**
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
**Step 4 : Client Code**
```python
def plan_delivery(logistics: Logistics):
    transport = logistics.create_transport()
    print(transport.deliver())

# Usage
plan_delivery(RoadLogistics())  # Output: Delivering by land in a truck.
plan_delivery(SeaLogistics())   # Output: Delivering by sea in a ship.
```
  
**Why This is Useful:**
- The client code uses the **factory method**, not the **constructor**.   
- You can add new product types without changing the client code.   
- It follows the Open/Closed Principle — open for extension, closed for modification.     

---

### 2. Location services
A real-world implementation of the Factory Method pattern for location services, allowing seamless switching between different mapping providers.

```python
from abc import ABC, abstractmethod

# Abstract Product
class LocationService(ABC):
    @abstractmethod
    def get_coordinates(self, address):
        pass
    
    @abstractmethod
    def get_address(self, lat, lng):
        pass

# Concrete Products
class GoogleMapsService(LocationService):
    def get_coordinates(self, address):
        print(f"Getting coordinates for {address} using Google Maps API")
        # Actual implementation would call Google Maps API
        return (37.7749, -122.4194)  # Example coordinates
    
    def get_address(self, lat, lng):
        print(f"Getting address for coordinates ({lat}, {lng}) using Google Maps API")
        # Actual implementation would call Google Maps API
        return "123 Example St, San Francisco, CA"

class OpenStreetMapService(LocationService):
    def get_coordinates(self, address):
        print(f"Getting coordinates for {address} using OpenStreetMap API")
        # Actual implementation would call OpenStreetMap API
        return (37.7749, -122.4194)  # Example coordinates
    
    def get_address(self, lat, lng):
        print(f"Getting address for coordinates ({lat}, {lng}) using OpenStreetMap API")
        # Actual implementation would call OpenStreetMap API
        return "123 Example St, San Francisco, CA"

# Abstract Creator
class LocationServiceFactory(ABC):
    @abstractmethod
    def create_location_service(self):
        pass
    
    def get_location_service(self):
        service = self.create_location_service()
        return service

# Concrete Creators
class GoogleMapsServiceFactory(LocationServiceFactory):
    def create_location_service(self):
        return GoogleMapsService()

class OpenStreetMapServiceFactory(LocationServiceFactory):
    def create_location_service(self):
        return OpenStreetMapService()

# Client code
def client_code(factory):
    location_service = factory.get_location_service()
    coords = location_service.get_coordinates("1600 Amphitheatre Parkway, Mountain View, CA")
    address = location_service.get_address(37.7749, -122.4194)
    print(f"Coordinates: {coords}")
    print(f"Address: {address}")

# Usage
if __name__ == "__main__":
    print("Using Google Maps:")
    client_code(GoogleMapsServiceFactory())
    
    print("\nUsing OpenStreetMap:")
    client_code(OpenStreetMapServiceFactory())
```

**output:**
```python
Using Google Maps:
Getting coordinates for 1600 Amphitheatre Parkway, Mountain View, CA using Google Maps API
Getting address for coordinates (37.7749, -122.4194) using Google Maps API
Coordinates: (37.7749, -122.4194)
Address: 123 Example St, San Francisco, CA

Using OpenStreetMap:
Getting coordinates for 1600 Amphitheatre Parkway, Mountain View, CA using OpenStreetMap API
Getting address for coordinates (37.7749, -122.4194) using OpenStreetMap API
Coordinates: (37.7749, -122.4194)
Address: 123 Example St, San Francisco, CA
```
   
**Benefits for Location Services**
- **API Independence**: Your application isn't tied to a specific location service provider.   
- **Easy to Switch Providers**: If Google Maps changes pricing or you want to use a different service, you can switch by creating a new concrete implementation.  
- **Testing Simplified**: You can create mock location services for testing.  
- **Feature Consistency**: All location services implement the same interface, ensuring consistent functionality.  
- **Configuration Flexibility**: You can determine which service to use at runtime based on user preferences, availability, or cost considerations.  

---

## 🔹Common Use Cases
- When a class can't anticipate the type of objects it needs to create
- When you want subclasses to specify the objects they create
- When you need to delegate responsibility to helper subclasses
  
---

## 🔹 Real-World Applications
- Multi-provider support: Allow users to choose their preferred mapping service  
- Fallback mechanisms: If one location service is down, automatically switch to another  
- Regional optimization: Use different services based on geographic region for better accuracy  
- Cost optimization: Use free tiers of different services before incurring charges     

---  
