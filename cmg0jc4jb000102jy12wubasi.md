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

# `WebDriver` **(Interfaces)**

> Base interface for controlling browsers.  
> ✅ Implemented by `ChromeDriver`, `FirefoxDriver`, `EdgeDriver`, etc.

## **1\.** `get(String url)`

* **Description:** Opens the specified URL in the browser.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
driver.get("https://example.com");
```

* **Possible Exceptions:**
    
    * `TimeoutException` – If page load takes longer than `pageLoadTimeout`.
        
    * `WebDriverException` – If the browser fails to start or navigate.
        

---

## **2\.** `getTitle()`

* **Description:** Returns the title of the current page.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String title = driver.getTitle();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If the browser is closed or session ended.
        

---

## **3\.** `getCurrentUrl()`

* **Description:** Returns the URL of the current page as a `String`.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String url = driver.getCurrentUrl();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If the browser is closed or session ended.
        

---

## **4\.** `getPageSource()`

* **Description:** Returns the source code of the current page.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String source = driver.getPageSource();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If browser session is invalid.
        

---

## **5\.** `close()`

* **Description:** Closes the current browser window.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
driver.close();
```

* **Possible Exceptions:**
    
    * `NoSuchWindowException` – If there is no window to close.
        

---

## **6\.** `quit()`

* **Description:** Closes all browser windows and ends the WebDriver session.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
driver.quit();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If the browser is already closed or session invalid.
        

---

## **7\.** `findElement(By by)`

* **Description:** Finds the first element using the given locator.
    
* **Return Type:** `WebElement`
    
* **Usage:**
    

```java
WebElement button = driver.findElement(By.id("submitBtn"));
```

* **Possible Exceptions:**
    
    * `NoSuchElementException` – If element is not found.
        
    * `StaleElementReferenceException` – If element is no longer attached to DOM.
        
    * `InvalidSelectorException` – If locator syntax is invalid.
        

---

## **8\.** `findElements(By by)`

* **Description:** Finds all elements matching the locator.
    
* **Return Type:** `List<WebElement>` (empty list if none found)
    
* **Usage:**
    

```java
List<WebElement> links = driver.findElements(By.tagName("a"));
```

* **Possible Exceptions:**
    
    * `InvalidSelectorException` – If locator is invalid.
        

---

## **9\.** `getWindowHandle()`

* **Description:** Returns the unique identifier (handle) of the current window.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String mainWindow = driver.getWindowHandle();
```

* **Possible Exceptions:**
    
    * `NoSuchWindowException` – If window no longer exists.
        

---

## **10\.** `getWindowHandles()`

* **Description:** Returns a `Set<String>` of all open window handles.
    
* **Return Type:** `Set<String>`
    
* **Usage:**
    

```java
Set<String> allWindows = driver.getWindowHandles();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If session is invalid or browser closed.
        

---

## **11\.** `switchTo()`

* **Description:** Returns a `TargetLocator` to switch between windows, frames, or alerts.
    
* **Return Type:** `WebDriver.TargetLocator`
    
* **Usage:**
    

```java
driver.switchTo().frame("frame1");    // Switch to frame
driver.switchTo().window("windowHandle");  // Switch to window
driver.switchTo().alert().accept();   // Switch to alert
```

* **Possible Exceptions:**
    
    * `NoSuchFrameException` – If frame not found.
        
    * `NoSuchWindowException` – If window not found.
        
    * `NoAlertPresentException` – If alert not found.
        

---

## **12\.** `manage()`

* **Description:** Returns an `Options` interface to manage cookies, timeouts, and window.
    
* **Return Type:** `WebDriver.Options`
    
* **Usage:**
    

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
driver.manage().window().maximize();
driver.manage().deleteAllCookies();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If session is invalid or browser closed.
        

---

## **13\.** `navigate()`

* **Description:** Returns a `Navigation` interface to control browser history.
    
* **Return Type:** `WebDriver.Navigation`
    
* **Usage:**
    

```java
driver.navigate().to("https://example.com");
driver.navigate().back();
driver.navigate().forward();
driver.navigate().refresh();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If navigation fails or browser session is invalid.
        

Here’s a **complete Selenium WebDriver Methods Cheat-Sheet** with **method, description, return type, usage, and possible exceptions** for quick reference:

| Method | Description | Return Type | Usage Example | Possible Exceptions |
| --- | --- | --- | --- | --- |
| `get(String url)` | Opens the specified URL | `void` | `driver.get("`[`https://example.com`](https://example.com)`");` | `TimeoutException`, `WebDriverException` |
| `getTitle()` | Returns the page title | `String` | `String title = driver.getTitle();` | `WebDriverException` |
| `getCurrentUrl()` | Returns current URL | `String` | `String url = driver.getCurrentUrl();` | `WebDriverException` |
| `getPageSource()` | Returns page HTML source | `String` | `String src = driver.getPageSource();` | `WebDriverException` |
| `close()` | Closes current browser window | `void` | `driver.close();` | `NoSuchWindowException` |
| `quit()` | Closes all browser windows & ends session | `void` | `driver.quit();` | `WebDriverException` |
| `findElement(By by)` | Finds first matching element | `WebElement` | `WebElement btn = driver.findElement(`[`By.id`](http://By.id)`("submit"));` | `NoSuchElementException`, `StaleElementReferenceException`, `InvalidSelectorException` |
| `findElements(By by)` | Finds all matching elements | `List<WebElement>` | `List<WebElement> links = driver.findElements(By.tagName("a"));` | `InvalidSelectorException` |
| `getWindowHandle()` | Returns current window handle | `String` | `String mainWin = driver.getWindowHandle();` | `NoSuchWindowException` |
| `getWindowHandles()` | Returns all window handles | `Set<String>` | `Set<String> windows = driver.getWindowHandles();` | `WebDriverException` |
| `switchTo()` | Switches focus to window/frame/alert | `WebDriver.TargetLocator` | `driver.switchTo().frame("frame1"); driver.switchTo().window("handle"); driver.switchTo().alert().accept();` | `NoSuchFrameException`, `NoSuchWindowException`, `NoAlertPresentException` |
| `manage()` | Access browser options (timeouts, cookies, window) | `WebDriver.Options` | `driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10)); driver.manage().window().maximize();` | `WebDriverException` |
| `navigate()` | Browser navigation (to, back, forward, refresh) | `WebDriver.Navigation` | `driver.navigate().to("`[`https://example.com`](https://example.com)`"); driver.navigate().back(); driver.navigate().forward(); driver.navigate().refresh();` | `WebDriverException` |

---

✅ **Tips:**

* Always use `quit()` at the end to release resources.
    
* `findElement()` throws an exception if not found; `findElements()` returns an empty list instead.
    
* `switchTo()` is necessary for frames, alerts, and multiple windows.
    
* `manage().timeouts()` is useful for implicit waits and page load timeouts.