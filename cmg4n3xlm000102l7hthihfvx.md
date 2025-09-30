---
title: "Java Complex Topic"
datePublished: Mon Sep 29 2025 04:40:06 GMT+0000 (Coordinated Universal Time)
cuid: cmg4n3xlm000102l7hthihfvx
slug: java-complex-topic
tags: codewithnini

---

# **Topic\_01: Singleton Class in Java**

## **1.What is Singleton in Java**

A **Singleton Class** is a class that **can have only one instance/object** in the **entire Java application**.  
It provides a **global point of access** to that instance.

**Key points:**

* Only **one object** of the class is created.
    
* Constructor is **private**.
    
* Accessed via a **static method**.
    

---

## **2\. Why Use Singleton?**

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

## **3\. Features of Singleton**

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

### **1️⃣** [**config.properties**](http://config.properties)

Create a file in your project (`src/test/resources/`[`config.properties`](http://config.properties)):

```java
browser=chrome
url=https://codewithnini-web-modules.netlify.app/
```

---

### **2️⃣ Config Reader Utility**

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

### **3️⃣ DriverManager (Singleton WebDriver)**

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

### **4️⃣ Usage in Test**

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

### **5️⃣ How It Works**

* `ConfigReader` reads `browser=chrome` (or firefox, edge).
    
* `DriverManager` creates the **singleton WebDriver** only once.
    
* If tests request `getDriver()`, they all share the **same instance**.
    
* After execution, `quitDriver()` closes and resets it.
    

## **4\. Types of Singleton in Java**

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
    

# **Topic\_02: Serializable Interface in Java**

`Serializable` interface is a Java core concept, and in automation frameworks (Selenium, TestNG, Cucumber), it has some **very practical use cases**. Let’s break it down clearly for **interview + real framework usage**.

---

# **1️⃣ What is** `Serializable` Interface in Java?

* `Serializable` is a **marker interface** (i.e., no methods inside).
    
* It tells the **JVM** that objects of a class can be **converted into a byte stream**.
    
* This byte stream can then be:
    
    * Stored in a **file** (persistence)
        
    * Sent over a **network**
        
    * Transferred between **JVMs/threads**
        

👉 Once serialized, the object can later be **deserialized** (reconstructed back into an object).

---

# **2️⃣ Why use** `Serializable`?

* Needed when we want to **share objects across different layers** of a framework or across JVMs.
    
* Prevents **loss of object state**.
    
* Especially useful in frameworks where objects are **passed around during parallel execution** (TestNG, Selenium Grid, Cucumber).
    

---

# **3️⃣ How to Use** `Serializable`?

### Example: Making a class serializable

```bash
import java.io.Serializable;

public class UserData implements Serializable {
    private static final long serialVersionUID = 1L;  // version control

    private String username;
    private String password;

    public UserData(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public String getUsername() { return username; }
    public String getPassword() { return password; }
}
```

👉 This class can now be **serialized and deserialized**.

---

# **4️⃣ Serialization Example**

```bash
import java.io.*;

public class SerializationDemo {
    public static void main(String[] args) throws Exception {
        UserData user = new UserData("nini", "pass123");

        // Serialize (write object to file)
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("user.ser"));
        oos.writeObject(user);
        oos.close();

        // Deserialize (read object back)
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("user.ser"));
        UserData deserializedUser = (UserData) ois.readObject();
        ois.close();

        System.out.println("Username: " + deserializedUser.getUsername());
        System.out.println("Password: " + deserializedUser.getPassword());
    }
}
```

---

# **5️⃣ Use Cases in Automation Frameworks**

### ✅ (a) **TestNG Parallel Execution**

* TestNG allows passing custom parameters using `ITestContext` or `@DataProvider`.
    
* If you pass a **custom object** (like `UserData`), it must be `Serializable` so TestNG can move it across threads safely.
    

---

### ✅ (b) **Selenium Grid / RemoteWebDriver**

* When tests run on a **remote Selenium Grid**, commands and objects are **serialized to JSON** and sent over the network.
    
* Example: `Capabilities` objects implement `Serializable`.
    

---

### ✅ (c) **Cucumber Scenario Context**

* In BDD frameworks, testers often create a **ScenarioContext** (to share test data across steps).
    
* If Cucumber runs scenarios in parallel, the context object should be `Serializable` so it can be passed between threads safely.
    

---

### ✅ (d) **Page Objects / Data Models**

* Sometimes frameworks persist **page states, test data, or API responses** into files.
    
* If your POJO (Plain Old Java Object) implements `Serializable`, you can easily **save and reload** states.
    

---

# **6️⃣ Why It’s Important in Interviews**

* Interviewers ask this to test **your understanding of parallel execution, object handling, and test data sharing**.
    
* Best way to answer:
    
    > "`Serializable` is a marker interface in Java that allows converting objects into a byte stream. In automation frameworks, it’s used in parallel test execution (TestNG), Selenium Grid for remote communication, and in Cucumber to share test context safely between steps or threads."
    

---

# **7️⃣ Key Notes**

* Always add `serialVersionUID` → prevents version mismatch issues.
    
* Not all objects should be serialized (e.g., WebDriver itself is not serializable). Instead, you serialize supporting objects (data, configs).
    

---

Perfect 👌 — now let’s see how `Serializable` comes into play in **RestAssured frameworks**.  
You won’t often see people talk about it directly, but it’s hidden under the hood in many cases.

---

# **1️⃣ Why** `Serializable` in RestAssured?

* RestAssured uses **POJOs** (Plain Old Java Objects) to:
    
    * Send request payloads (`.body(object)`)
        
    * Deserialize responses into objects (`.as(Class<T>)`)
        
* These POJOs sometimes need to be `Serializable` if:
    
    * You want to **cache/save request/response** for debugging or reporting
        
    * You are **reusing objects across threads** in parallel test execution
        
    * You need to **log/persist request/response** into a file (JSON, .ser, etc.)
        

---

# **2️⃣ Example: POJO with Serializable for Request Body**

### [`User.java`](http://User.java)

```bash
import java.io.Serializable;

public class User implements Serializable {
    private static final long serialVersionUID = 1L;

    private String name;
    private String job;

    public User(String name, String job) {
        this.name = name;
        this.job = job;
    }

    public String getName() { return name; }
    public String getJob() { return job; }
}
```

---

# **3️⃣ Using Serializable POJO in RestAssured**

### [`RestAssuredTest.java`](http://RestAssuredTest.java)

```bash
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class RestAssuredTest {
    public static void main(String[] args) {
        User user = new User("Nini", "QA Automation");

        // Send request with Serializable POJO
        Response res = RestAssured.given()
                .baseUri("https://reqres.in")
                .basePath("/api/users")
                .contentType("application/json")
                .body(user)   // <-- POJO used as body
                .post();

        System.out.println("Response: " + res.asPrettyString());

        // Deserialize response back into User class
        User responseUser = res.as(User.class);
        System.out.println("Deserialized Name: " + responseUser.getName());
    }
}
```

✔️ Here, the **POJO (**`User`) is serializable →

* Can be written to a file for debugging (`ObjectOutputStream`)
    
* Can be shared across **parallel tests** if needed
    

---

# **4️⃣ Use Cases in Automation Frameworks (RestAssured)**

✅ **a. Request/Response Logging & Saving**

* Sometimes we log full request/response objects into reports (Extent, Allure).
    
* If POJOs are `Serializable`, we can easily **save them in files** (`.ser`, JSON, etc.) for later debugging.
    

✅ **b. Test Data Reuse**

* If your test data comes from an external file (Excel/JSON), you load it into a POJO.
    
* Marking it `Serializable` allows **storing and reusing** across multiple test cases.
    

✅ **c. Parallel Execution in TestNG**

* When running multiple API tests in parallel, TestNG may pass POJOs (test data) to different threads.
    
* Making them `Serializable` avoids **thread-safety issues**.
    

✅ **d. Distributed Execution (Jenkins + Selenium Grid)**

* If API + UI tests are combined, `Serializable` allows **sending POJOs between modules**.
    

---

# **5️⃣ Quick Example: Save RestAssured Response as Serialized Object**

```bash
import io.restassured.RestAssured;
import io.restassured.response.Response;
import java.io.*;

public class SaveResponse {
    public static void main(String[] args) throws Exception {
        Response res = RestAssured.get("https://reqres.in/api/users/2");

        // Serialize response body into a file
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("response.ser"));
        oos.writeObject(res.asString());  // saving as serialized string
        oos.close();

        // Deserialize later
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("response.ser"));
        String responseBody = (String) ois.readObject();
        ois.close();

        System.out.println("Recovered Response: " + responseBody);
    }
}
```

---

✅ **Interview Answer (RestAssured context):**

> "`Serializable` in RestAssured is mainly used when we create POJOs for request/response payloads. Marking them serializable ensures we can save them, transfer them across threads in parallel execution, or log them for debugging. For example, if I create a `User` POJO for request body, making it `Serializable` allows me to reuse it across tests, save response objects in files, and ensure thread safety during parallel API testing."

---

Got it 👍 Let’s make it very **simple English** for you.

---

## 🔹 What is `Serializable`?

* `Serializable` is a **marker interface** in Java.
    
* It tells Java: *“This object can be converted into a byte stream (saved into a file, sent over network, or reused later).”*
    

Think of it like **packing your object into a box** so you can store it or send it anywhere.

---

## 🔹 Why do we use it in **RestAssured**?

In API automation we often create **POJO classes** (simple Java classes with variables) to send or receive JSON data.  
Example:

```bash
{ "name": "Nini", "job": "QA" }
```

We create a `User` POJO for this.  
If we mark it as `Serializable`:

* We can **save it** in a file for debugging.
    
* We can **reuse it** in multiple test cases.
    
* We can **share it safely** when running tests in parallel (multi-threading).
    

---

## 🔹 How do we use it?

Example:

### 1\. Create POJO

```bash
import java.io.Serializable;

public class User implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private String job;

    public User(String name, String job) {
        this.name = name;
        this.job = job;
    }
}
```

### 2\. Use it in RestAssured

```bash
User user = new User("Nini", "QA Engineer");

RestAssured.given()
        .baseUri("https://reqres.in")
        .contentType("application/json")
        .body(user)  // POJO as request body
        .post("/api/users")
        .then()
        .statusCode(201);
```

---

## 🔹 Use cases in automation framework

1. **Request Payloads** – Send API request body as a `Serializable` POJO.
    
2. **Response Mapping** – Convert API response JSON into a `Serializable` POJO.
    
3. **Parallel Execution** – Share test data across threads safely.
    
4. **Save/Log Data** – Save request/response objects into a file or report.
    

---

✅ **Simple Interview Answer**

> In RestAssured, we often use POJO classes for request and response bodies. If we make them `Serializable`, we can store, reuse, or share them easily across multiple tests or threads. It helps in saving responses for debugging, running tests in parallel, and keeping data reusable.