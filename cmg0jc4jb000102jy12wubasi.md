---
title: "Selenium With Java"
datePublished: Fri Sep 26 2025 07:43:25 GMT+0000 (Coordinated Universal Time)
cuid: cmg0jc4jb000102jy12wubasi
slug: selenium-with-java
tags: codewithnini

---

# 🔹 **Introduction to Selenium**

## ✅ **What is Selenium?**

* Selenium is a **free and open-source automation testing framework** used to automate web applications across different browsers and platforms.
    
* It supports multiple **programming languages** (Java, Python, C#, JavaScript, Ruby, Kotlin).
    
* It is **browser automation only** (not for desktop or mobile apps directly).
    

---

## ✅ **Selenium Components**

1. **Selenium IDE**
    
    * A Chrome/Firefox plugin.
        
    * Record & playback tool for quick test creation.
        
    * Best for beginners, not for complex frameworks.
        
2. **Selenium RC (Remote Control)** ❌ (deprecated)
    
    * Old component, replaced by WebDriver.
        
    * Required a server to interact with browsers.
        
3. **Selenium WebDriver**
    
    * Core & most widely used component.
        
    * Directly interacts with the browser using drivers.
        
    * Supports advanced features (JavaScript execution, waits, etc.).
        
4. **Selenium Grid**
    
    * Used for **parallel and distributed execution**.
        
    * Run tests on multiple machines, OS, and browsers at the same time.
        
    * Latest version: **Grid 4 (W3C compliant)**.
        

---

## ✅ **Advantages of Selenium**

* Open-source (free to use).
    
* Cross-browser testing (Chrome, Firefox, Edge, Safari, Opera).
    
* Cross-platform testing (Windows, Mac, Linux).
    
* Multiple programming language support.
    
* Supports integration with frameworks (TestNG, JUnit, Cucumber).
    
* Works with CI/CD tools (Jenkins, GitHub Actions).
    
* Large active community & constant updates.
    

---

## ✅ **Limitations of Selenium**

* Only for **web applications** (no desktop or mobile apps directly).
    
* No built-in **reporting system** (requires third-party tools).
    
* Cannot handle **Captcha, Barcode, OTP** directly.
    
* Requires external setup for **file upload/download handling**.
    
* Flaky tests if synchronization (waits) is not handled properly.
    

---

## ✅ **Selenium 3 vs Selenium 4**

| Feature | Selenium 3 | Selenium 4 |
| --- | --- | --- |
| **W3C Protocol** | Used JSON Wire Protocol | W3C WebDriver protocol (faster & stable) |
| **Relative Locators** | ❌ Not available | ✅ Introduced (`above`, `below`, `near`) |
| **Grid Architecture** | Hub & Node | Fully distributed, no hub needed |
| **CDP (Chrome DevTools Protocol)** | ❌ Not supported | ✅ Supported (network logs, console logs, geolocation, etc.) |
| **Better IDE** | Basic features | Improved with debugging & control flow |
| **Documentation** | Limited | Modern, detailed docs |

---

## ✅ **Selenium with Different Languages**

Selenium supports multiple languages via **language bindings**:

* **Java** → most popular (TestNG, Maven, Jenkins integration).
    
* **Python** → simple syntax, good for quick automation.
    
* **C#** → widely used in Microsoft environments.
    
* **JavaScript (Node.js)** → for frontend-focused testers.
    
* **Ruby, Kotlin** → less popular but supported.
    

💡 Language choice usually depends on:

* Team expertise
    
* Existing tech stack
    
* CI/CD environment
    

### **1\. Selenium WebDriver Basics**

Selenium WebDriver is a browser automation framework that allows you to execute your tests against different browsers. Unlike Selenium IDE, WebDriver directly communicates with the browser without requiring a separate server.

**Key Points:**

* Supports multiple browsers (Chrome, Firefox, Edge, Safari, etc.).
    
* Uses browser-specific drivers (e.g., `chromedriver`, `geckodriver`).
    
* Works with multiple programming languages (Java, Python, C#, JavaScript, etc.).
    
* Enables automation of web applications for testing purposes.
    

---

### **2\. WebDriver Architecture & W3C Protocol**

**WebDriver Architecture:**

```bash
Test Script (Java/Python/JS)
        |
   Selenium WebDriver API
        |
  Browser-specific Driver
        |
      Browser
```

**Details:**

* **Test Script**: Written in your preferred language (Java, Python, etc.).
    
* **WebDriver API**: Provides methods to interact with web elements and browsers.
    
* **Browser Driver**: Acts as a bridge between your script and the browser.
    
* **Browser**: Executes the commands and returns the response.
    

**W3C WebDriver Protocol:**

* Standard protocol that defines how commands are sent to the browser.
    
* Ensures uniform behavior across different browsers.
    
* Selenium 4 uses the W3C WebDriver protocol by default.
    

---

### **3\. Launching Browsers**

To automate browsers, you need to initialize a WebDriver instance for that browser.

**Example in Java:**

```java
// Chrome
WebDriver driver = new ChromeDriver();

// Firefox
WebDriver driver = new FirefoxDriver();

// Edge
WebDriver driver = new EdgeDriver();
```

> Make sure the respective browser driver (chromedriver/geckodriver/msedgedriver) is in your system PATH or set using `System.setProperty()`.