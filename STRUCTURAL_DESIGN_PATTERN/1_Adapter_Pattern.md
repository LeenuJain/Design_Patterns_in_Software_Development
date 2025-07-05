# Adapter Pattern

## 🔹 What is Adapter Pattern?

The Adapter Pattern lets **two incompatible interfaces work together**.
It acts as a **bridge** between an existing class and what the client expects.

Think of it like a **translator** between two people who speak different languages.

---

## 🔹 Real-World Analogy
**Car Charger Example (Automobile Analogy)**
Imagine you have an electric car that supports Type-C charging, but you only have a wall socket charger that outputs regular AC power.
You use a charging adapter that:
- Converts AC to DC
- Fits the Type-C port
So:
- Car expects Type-C interface
- Wall Charger gives AC output
- Adapter bridges this gap

---

## 🔹 Example in Python Example)
Let's say you have an old GPS system in a car that gives location in (x, y) format.
Now your new car system expects location in latitude and longitude.
Here’s how the Adapter pattern helps:
```python
# Existing system (incompatible interface)
class OldGPS:
    def get_coordinates(self):
        return (12345, 67890)  # returns x, y

# Expected interface
class NewCarSystem:
    def display_location(self, lat, lon):
        print(f"Current location: Latitude={lat}, Longitude={lon}")

# Adapter
class GPSAdapter:
    def __init__(self, old_gps):
        self.old_gps = old_gps

    def get_lat_lon(self):
        x, y = self.old_gps.get_coordinates()
        # Convert x, y to lat, lon (just for demo, using dummy conversion)
        lat = x / 1000.0
        lon = y / 1000.0
        return (lat, lon)

# Usage
old_gps = OldGPS()
adapter = GPSAdapter(old_gps)

car_system = NewCarSystem()
lat, lon = adapter.get_lat_lon()
car_system.display_location(lat, lon)
```

### 🔹 Understanding the Adapter Pattern with the Car GPS Example

It is also defined as:  
**“The Adapter Pattern translates one interface into another so that classes can work together without changing their existing code.”**

The following example demonstrates how this definition applies in practice:

To relate this definition to our example:

- `OldGPS` has a method: `get_coordinates()` → returns `(x, y)`
- `NewCarSystem` expects a method like: `display_location(latitude, longitude)`

These interfaces **don’t match**.

Hence, we introduce the **`GPSAdapter`**:

- `GPSAdapter` **wraps** the `OldGPS` class.
- It exposes a **new interface**: `get_lat_lon()`, which is compatible with what the `NewCarSystem` expects.
- Internally, it **translates** the incompatible `(x, y)` coordinates to `(latitude, longitude)`.


The best part is:  
- We **did not modify** the existing `OldGPS` or `NewCarSystem` classes.  
- The adapter allows them to **work together seamlessly** without altering their original code.





