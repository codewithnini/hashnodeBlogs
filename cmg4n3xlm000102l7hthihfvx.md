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

## **Singleton pattern example:**

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1759168351970/1872aae1-8884-4227-bded-e60077d615b2.png align="center")

## **Singleton pattern used in Selenium**

## Example: UseCase 01

```java
package SingletonPatternWebDriver;

import java.time.Duration;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class DriverManager {
	 // 1️ Private static instance of WebDriver
    private static WebDriver driver;

    // 2️ Private constructor so no one can create object
    private DriverManager() {}

    // 3️ Public static method to provide global access
    public static WebDriver getDriver() {
        if (driver == null) {
//            System.setProperty("webdriver.chrome.driver", "drivers/chromedriver.exe"); // // No need to set System.setProperty in Selenium >4.6 versio 
            driver = new ChromeDriver();
            driver.manage().window().maximize();
            driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
        }
        return driver;
    }

    // 4️  Quit driver and reset instance
    public static void quitDriver() {
        if (driver != null) {
            driver.quit();
            driver = null;
        }
    }
}
```

```java
package SingletonPatternWebDriver;

import org.openqa.selenium.WebDriver;

public class LoginTest {
    public static void main(String[] args) {
        // Get driver from Singleton class
        WebDriver driver = DriverManager.getDriver();
        driver.get("https://codewithnini-web-modules.netlify.app/");
        System.out.println("Page Title: " + driver.getTitle());

        // Quit after test
        DriverManager.quitDriver();
    }
}
```

```bash

Page Title: CodeWithNini-Web-Automation-Module
```

## **Note:**

## ⚡ If You’re Using Selenium &lt; 4.6

You **still need** the `System.setProperty()` line:

```java
System.setProperty("webdriver.chrome.driver", "drivers/chromedriver.exe");
```

Make sure:

* Your `chromedriver.exe` is **compatible with Chrome version**.
    
* Path is correct (`drivers/chromedriver.exe` should exist).
    

---

## 🔧 If Error Still Persists

1. Check Selenium version:
    
    ```java
    <!-- pom.xml -->
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.24.0</version> <!-- or latest -->
    </dependency>
    ```
    
2. Ensure Chrome is installed and updated.
    
3. Run a simple test to confirm driver works without Singleton:
    

```java
public class TestChrome {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://google.com");
        System.out.println(driver.getTitle());
        driver.quit();
    }
}
```

---

## **⚡ Extra Note for Frameworks: hybrid/data-driven frameworks**

  
In **hybrid/data-driven frameworks**, instead of hardcoding `ChromeDriver`, you usually read the browser type (`chrome`, `firefox`, `edge`) from a [`config.properties`](http://config.properties) file, and create driver accordingly.

Let’s make a **production-ready Singleton WebDriver** that supports **multiple browsers (Chrome, Firefox, Edge)** using a [`config.properties`](http://config.properties) file. This is **exactly how automation frameworks implement it** and interviewers love this answer.

---

## Example: UseCase 02

## **1️⃣** [**config.properties**](http://config.properties)

Create a file in your project (`src/test/resources/`[`config.properties`](http://config.properties)):

```java
browser=chrome
url=https://codewithnini-web-modules.netlify.app/
```

---

## **2️⃣ Config Reader Utility**

Reads values from the [`config.properties`](http://config.properties) file.

```java
package SingletonPatternWedDriverWithDataDrivenAproach;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Properties;

public class ConfigReader {
	private static Properties properties;

	static {
		try {
			FileInputStream fis = new FileInputStream("./src/main/resources/config.properties");
			properties = new Properties();
			properties.load(fis);
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

	public static String getProperty(String key) {
		return properties.getProperty(key);
	}
}
```

---

## **3️⃣ DriverManager (Singleton WebDriver)**

```java
package SingletonPatternWedDriverWithDataDrivenAproach;



import java.time.Duration;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;

public class DriverManager {

    private static WebDriver driver;

    // private constructor
    private DriverManager() {}

    public static WebDriver getDriver() {
        if (driver == null) {
            String browser = ConfigReader.getProperty("browser").toLowerCase();

            switch (browser) {
                case "chrome":
                    driver = new ChromeDriver();  // Selenium Manager auto-handles driver
                    break;

                case "firefox":
                    driver = new FirefoxDriver();
                    break;

                case "edge":
                    driver = new EdgeDriver();
                    break;

                default:
                    throw new IllegalArgumentException("Invalid browser: " + browser);
            }

            driver.manage().window().maximize();
            driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
        }
        return driver;
    }

    public static void quitDriver() {
        if (driver != null) {
            driver.quit();
            driver = null;
        }
    }
}

```

---

## **4️⃣ Usage in Test**

```java
package SingletonPatternWedDriverWithDataDrivenAproach;

import org.openqa.selenium.WebDriver;

public class BrowserTest {
    public static void main(String[] args) {
        WebDriver driver = DriverManager.getDriver();

        driver.get(ConfigReader.getProperty("url"));
        System.out.println("Page Title: " + driver.getTitle());

        DriverManager.quitDriver();
    }
}
```

---

**OUTPUT:**

```bash
Page Title: CodeWithNini-Web-Automation-Module
```

# **5️⃣ How It Works**

* `ConfigReader` reads `browser=chrome` (or firefox, edge).
    
* `DriverManager` creates the **singleton WebDriver** only once.
    
* If tests request `getDriver()`, they all share the **same instance**.
    
* After execution, `quitDriver()` closes and resets it.
    

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