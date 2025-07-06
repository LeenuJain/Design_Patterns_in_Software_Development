# Proxy Design Pattern

---

## 🔹 What is it?

The **Proxy Pattern** provides a **placeholder or surrogate** for another object to **control access** to it.

In simple words:

> "You don't interact with the real object directly — instead, you go through a proxy that adds control or extra behavior."

---

## 🔹 Real-World Analogy: Credit Card

When you buy something:

- You don’t hand over your **bank account**
- You use a **credit card** — a **proxy** to your account

The card:

- Checks your balance  
- Logs the transaction  
- Provides fraud protection  

But the actual money comes from your account — which is **hidden behind the proxy**.

---

## 🔹 Purpose

To add a layer of **control**, **security**, **logging**, or **delay** between the client and the real object.

---

## 🐍 Python Code Example: Video Downloader (with access control)

```python
# The Real Object (the heavy object)
class RealVideoDownloader:
    def download(self, video_url):
        print(f"📥 Downloading video from {video_url}...")

# Proxy (adds access control)
class ProxyVideoDownloader:
    def __init__(self, user):
        self.user = user
        self.downloader = RealVideoDownloader()

    def download(self, video_url):
        if self.user == "admin":
            self.downloader.download(video_url)
        else:
            print("❌ Access denied. Only admin can download videos.")

# Usage
# Normal user
user1 = ProxyVideoDownloader("guest")
user1.download("https://youtube.com/video1")

# Admin user
user2 = ProxyVideoDownloader("admin")
user2.download("https://youtube.com/video2")
```

**Output:**
```python
❌ Access denied. Only admin can download videos.
📥 Downloading video from https://youtube.com/video2...
```

**Summary:**

| Concept      | Example               |
|--------------|------------------------|
| Real Object  | RealVideoDownloader    |
| Proxy        | ProxyVideoDownloader   |
| Goal         | Control or enhance access to the real object |

---

## 🔹 Use Cases of Proxy Pattern

| Use Case              | Description                                                    |
|------------------------|----------------------------------------------------------------|
| Access Control Proxy   | Control who can use the object (like a gatekeeper)             |
| Virtual Proxy          | Delay object creation until it’s needed (lazy loading)         |
| Logging Proxy          | Add logging or audit trail                                     |
| Remote Proxy           | Handle communication to a remote object (like an API or server)|

---

## 🔹 Real-World Software Examples

- YouTube Premium: Only paying users can download videos → Proxy checks permission  
- Database Pooling: Proxies manage actual DB connections  
- Web Browsers: Use proxy servers to control traffic  
- VPN: Acts as a proxy between you and the internet  

---

---

## 🔹 How VPN Works as a Proxy Pattern

A **VPN acts as a proxy** between your device (client) and the public internet (real object).

Instead of your computer directly interacting with websites and services:
- You connect to the **VPN server** (the proxy)
- The VPN server forwards your request to the actual destination
- The destination server responds to the **VPN**, not to you
- Then the VPN sends the response **back to you**

#### Proxy Pattern Mapping

| Role               | Example                                 |
|--------------------|------------------------------------------|
| Client             | You (your device/browser)               |
| Real Object        | The website or service you're accessing |
| Proxy              | VPN server                              |
| Added Behavior     | Hides your IP, encrypts traffic, bypasses firewalls |

---

#### Why It Fits the Proxy Pattern

- **Control**: The VPN controls and manages your access to websites
- **Security**: It adds encryption and hides your identity
- **Isolation**: The real server never talks to your device directly
- **Extra Behavior**: VPN adds logging, geo-routing, IP masking — all proxy responsibilities

✅ You’re not changing the website — you’re adding a layer between you and it. That’s **exactly what a Proxy does**!

---

