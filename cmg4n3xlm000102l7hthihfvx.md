---
title: "Java Complex Topic"
datePublished: Mon Sep 29 2025 04:40:06 GMT+0000 (Coordinated Universal Time)
cuid: cmg4n3xlm000102l7hthihfvx
slug: java-complex-topic
tags: codewithnini

---

# **Singleton in Java**

## **1️⃣ What is Singleton in Java**

A **Singleton Class** is a class that **can have only one instance/object** in the **entire Java application**.  
It provides a **global point of access** to that instance.

**Key points:**

* Only **one object** of the class is created.
    
* Constructor is **private**.
    
* Accessed via a **static method**.
    

---

## **2️⃣ Why Use Singleton?**

We use Singleton when we want:

1. **Single point of control** for a resource.
    
2. **Save memory** by avoiding multiple object creation.
    
3. **Global access** to a single instance.
    
4. Ensure **thread safety** in multi-threaded apps (if required).
    

**Examples of where it’s useful:**

* Logger class (single log object across the app)
    
* Configuration or properties manager
    
* Database connection pool
    
* Thread pool manager
    
* Caching objects
    

---

## **3️⃣ Features of Singleton**

| Feature | Description |
| --- | --- |
| Single Instance | Only one object is created. |
| Private Constructor | Prevents external instantiation. |
| Global Access | Accessed via `getInstance()` method. |
| Lazy/Eager Init | Can initialize instance when needed or at class loading. |
| Thread-Safe | Can make thread-safe for multi-threaded apps. |

---

## **4️⃣ Types of Singleton in Java**

### **A. Eager Initialization**

* ### Instance is created **at class loading time**.
    
* Simple, but instance created even if not needed.
    

```java
class EagerSingleton {
    private static final EagerSingleton instance = new EagerSingleton();

    private EagerSingleton() {}  // private constructor

    public static EagerSingleton getInstance() {
        return instance;
    }
}

// Usage
EagerSingleton obj = EagerSingleton.getInstance();
```

---

### **B. Lazy Initialization**

* Instance is created **when needed**.
    
* Not thread-safe.
    

```java
class LazySingleton {
    private static LazySingleton instance;

    private LazySingleton() {}

    public static LazySingleton getInstance() {
        if (instance == null) {
            instance = new LazySingleton();
        }
        return instance;
    }
}
```

---

### **C. Thread-Safe Singleton (Synchronized Method)**

* Safe in multi-threaded environments.
    
* Slightly slower due to `synchronized`.
    

```java
class ThreadSafeSingleton {
    private static ThreadSafeSingleton instance;

    private ThreadSafeSingleton() {}

    public static synchronized ThreadSafeSingleton getInstance() {
        if (instance == null) {
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }
}
```

---

### **D. Double-Checked Locking**

* Thread-safe **and fast**.
    
* Reduces overhead of `synchronized`.
    

```java
class DoubleCheckedSingleton {
    private static volatile DoubleCheckedSingleton instance;

    private DoubleCheckedSingleton() {}

    public static DoubleCheckedSingleton getInstance() {
        if (instance == null) {
            synchronized (DoubleCheckedSingleton.class) {
                if (instance == null) {
                    instance = new DoubleCheckedSingleton();
                }
            }
        }
        return instance;
    }
}
```

---

### **E. Bill Pugh Singleton (Recommended)**

* Uses **inner static helper class**.
    
* Thread-safe and lazy-loaded.
    
* No `synchronized` overhead.
    

```java
class BillPughSingleton {
    private BillPughSingleton() {}

    private static class SingletonHelper {
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }

    public static BillPughSingleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}

// Usage
BillPughSingleton obj = BillPughSingleton.getInstance();
```

---

### **F. Enum Singleton**

* Simple, **thread-safe by default**, prevents serialization/deserialization issues.
    

```java
enum EnumSingleton {
    INSTANCE;

    public void showMessage() {
        System.out.println("Enum Singleton example");
    }
}

// Usage
EnumSingleton.INSTANCE.showMessage();
```

---

## **5️⃣ Use Cases of Singleton**

| Use Case | Description |
| --- | --- |
| **Logger** | Only one logger instance used across app. |
| **Database Connection Pool** | Single DB connection object, reused. |
| **Configuration Manager** | Load config from file once, share globally. |
| **Thread Pool** | Single thread pool manager instance. |
| **Caching** | Single cache manager instance. |
| **Registry / Factory** | Centralized registry/factory object. |

---

## **6️⃣ Example: Logger Singleton**

```java
class Logger {
    private static Logger logger;

    private Logger() {}

    public static Logger getInstance() {
        if (logger == null) {
            logger = new Logger();
        }
        return logger;
    }

    public void log(String message) {
        System.out.println("LOG: " + message);
    }
}

// Usage
public class TestSingleton {
    public static void main(String[] args) {
        Logger log1 = Logger.getInstance();
        Logger log2 = Logger.getInstance();

        log1.log("First message");
        log2.log("Second message");

        System.out.println(log1 == log2); // true
    }
}
```

✅ Output:

```java
LOG: First message
LOG: Second message
true
```

* Only **one instance** of Logger exists.
    

---

## **7️⃣ Advantages**

1. Saves memory by **restricting object creation**.
    
2. Provides **global access point**.
    
3. Useful for **shared resources**.
    
4. Can be made **thread-safe**.
    
5. Works well for **logging, caching, configuration**.
    

---

## **8️⃣ Disadvantages / Cautions**

1. Can **hide dependencies** → harder to test.
    
2. Can lead to **tightly coupled code**.
    
3. Enum singleton **best avoids serialization issues**, others may need `readResolve()` for serialization.
    
4. Not suitable if **multiple instances** are needed in the future.