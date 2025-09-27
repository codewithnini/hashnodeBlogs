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

## **1.** `get(String url)`

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

## **2.** `getTitle()`

* **Description:** Returns the title of the current page.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String title = driver.getTitle();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If the browser is closed or session ended.
        

---

## **3.** `getCurrentUrl()`

* **Description:** Returns the URL of the current page as a `String`.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String url = driver.getCurrentUrl();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If the browser is closed or session ended.
        

---

## **4.** `getPageSource()`

* **Description:** Returns the source code of the current page.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String source = driver.getPageSource();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If browser session is invalid.
        

---

## **5.** `close()`

* **Description:** Closes the current browser window.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
driver.close();
```

* **Possible Exceptions:**
    
    * `NoSuchWindowException` – If there is no window to close.
        

---

## **6.** `quit()`

* **Description:** Closes all browser windows and ends the WebDriver session.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
driver.quit();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If the browser is already closed or session invalid.
        

---

## **7.** `findElement(By by)`

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

## **8.** `findElements(By by)`

* **Description:** Finds all elements matching the locator.
    
* **Return Type:** `List<WebElement>` (empty list if none found)
    
* **Usage:**
    

```java
List<WebElement> links = driver.findElements(By.tagName("a"));
```

* **Possible Exceptions:**
    
    * `InvalidSelectorException` – If locator is invalid.
        

---

## **9.** `getWindowHandle()`

* **Description:** Returns the unique identifier (handle) of the current window.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String mainWindow = driver.getWindowHandle();
```

* **Possible Exceptions:**
    
    * `NoSuchWindowException` – If window no longer exists.
        

---

## **10.** `getWindowHandles()`

* **Description:** Returns a `Set<String>` of all open window handles.
    
* **Return Type:** `Set<String>`
    
* **Usage:**
    

```java
Set<String> allWindows = driver.getWindowHandles();
```

* **Possible Exceptions:**
    
    * `WebDriverException` – If session is invalid or browser closed.
        

---

## **11.** `switchTo()`

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

## **12.** `manage()`

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

## **13.** `navigate()`

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
    

# `WebElement` **(Interfaces)**

> Represents an element on the webpage.  
> ✅ Returned by `findElement()`.

### **1.** `getText()`

* **Description:** Returns the visible text of the element.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String text = element.getText();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **2.** `getAttribute(String name)`

* **Description:** Returns the value of the specified attribute of the element.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String value = element.getAttribute("value");
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **3.** `getCssValue(String propertyName)`

* **Description:** Returns the value of a CSS property of the element.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String color = element.getCssValue("color");
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **4.** `getTagName()`

* **Description:** Returns the tag name of the element (e.g., "input", "button").
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String tag = element.getTagName();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **5.** `isDisplayed()`

* **Description:** Checks if the element is visible on the page.
    
* **Return Type:** `boolean`
    
* **Usage:**
    

```java
boolean visible = element.isDisplayed();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **6.** `isEnabled()`

* **Description:** Checks if the element is enabled (e.g., input field or button).
    
* **Return Type:** `boolean`
    
* **Usage:**
    

```java
boolean enabled = element.isEnabled();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **7.** `isSelected()`

* **Description:** Checks if a checkbox, radio button, or option is selected.
    
* **Return Type:** `boolean`
    
* **Usage:**
    

```java
boolean selected = element.isSelected();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **8.** `click()`

* **Description:** Clicks on the element.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
element.click();
```

* **Possible Exceptions:**
    
    * `ElementNotInteractableException`
        
    * `StaleElementReferenceException`
        

---

### **9.** `sendKeys(CharSequence...)`

* **Description:** Types text into the element.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
element.sendKeys("Hello World");
```

* **Possible Exceptions:**
    
    * `InvalidElementStateException`
        
    * `StaleElementReferenceException`
        

---

### **10.** `clear()`

* **Description:** Clears the content of an input field.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
element.clear();
```

* **Possible Exceptions:**
    
    * `InvalidElementStateException`
        
    * `StaleElementReferenceException`
        

---

### **11.** `submit()`

* **Description:** Submits a form element.
    
* **Return Type:** `void`
    
* **Usage:**
    

```java
element.submit();
```

* **Possible Exceptions:**
    
    * `NoSuchElementException`
        
    * `StaleElementReferenceException`
        

---

### **12.** `getLocation()`

* **Description:** Returns the location (x, y) of the element on the page.
    
* **Return Type:** `Point`
    
* **Usage:**
    

```java
Point location = element.getLocation();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **13.** `getSize()`

* **Description:** Returns the width and height of the element.
    
* **Return Type:** `Dimension`
    
* **Usage:**
    

```java
Dimension size = element.getSize();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **14.** `getRect()`

* **Description:** Returns the element’s size and position as a rectangle.
    
* **Return Type:** `Rectangle`
    
* **Usage:**
    

```java
Rectangle rect = element.getRect();
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **15.** `getScreenshotAs(OutputType<T>)`

* **Description:** Captures screenshot of the element.
    
* **Return Type:** `<T>`
    
* **Usage:**
    

```java
File src = element.getScreenshotAs(OutputType.FILE);
```

* **Possible Exceptions:**
    
    * `WebDriverException`
        

---

### **16.** `getDomProperty(String name)`

* **Description:** Returns the DOM property of the element.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String prop = element.getDomProperty("value");
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **17.** `getDomAttribute(String name)`

* **Description:** Returns the DOM attribute of the element.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
String attr = element.getDomAttribute("id");
```

* **Possible Exceptions:**
    
    * `StaleElementReferenceException`
        

---

### **18.** `equals(Object obj)`

* **Description:** Compares two elements.
    
* **Return Type:** `boolean`
    
* **Usage:**
    

```java
boolean same = element.equals(otherElement);
```

* **Possible Exceptions:**
    
    * None
        

---

### **19.** `hashCode()`

* **Description:** Returns hash code of the element.
    
* **Return Type:** `int`
    
* **Usage:**
    

```java
int code = element.hashCode();
```

* **Possible Exceptions:**
    
    * None
        

---

### **20.** `toString()`

* **Description:** Returns string representation of the element.
    
* **Return Type:** `String`
    
* **Usage:**
    

```java
System.out.println(element.toString());
```

* **Possible Exceptions:**
    
    * None
        

## **1\. Text & Attribute Methods**

| Method | Description | Return Type | Example | Possible Exceptions |
| --- | --- | --- | --- | --- |
| `getText()` | Gets visible text of element | `String` | `String text = element.getText();` | `StaleElementReferenceException` |
| `getAttribute(String name)` | Gets value of an attribute | `String` | `String value = element.getAttribute("value");` | `StaleElementReferenceException` |
| `getCssValue(String propertyName)` | Gets CSS property value | `String` | `String color = element.getCssValue("color");` | `StaleElementReferenceException` |
| `getTagName()` | Returns tag name of element | `String` | `String tag = element.getTagName();` | `StaleElementReferenceException` |
| `isDisplayed()` | Checks if element is visible | `boolean` | `boolean visible = element.isDisplayed();` | `StaleElementReferenceException` |
| `isEnabled()` | Checks if element is enabled | `boolean` | `boolean enabled = element.isEnabled();` | `StaleElementReferenceException` |
| `isSelected()` | Checks if checkbox/radio is selected | `boolean` | `boolean selected = element.isSelected();` | `StaleElementReferenceException` |

---

## **2\. Interaction Methods**

| Method | Description | Return Type | Example | Possible Exceptions |
| --- | --- | --- | --- | --- |
| `click()` | Clicks the element | `void` | [`element.click`](http://element.click)`();` | `ElementNotInteractableException`, `StaleElementReferenceException` |
| `sendKeys(CharSequence...)` | Types text into input field | `void` | `element.sendKeys("Hello");` | `InvalidElementStateException`, `StaleElementReferenceException` |
| `clear()` | Clears text input | `void` | `element.clear();` | `InvalidElementStateException`, `StaleElementReferenceException` |
| `submit()` | Submits a form element | `void` | `element.submit();` | `NoSuchElementException`, `StaleElementReferenceException` |

---

## **3\. Advanced Interaction / State Methods**

| Method | Description | Return Type | Example | Possible Exceptions |
| --- | --- | --- | --- | --- |
| `getRect()` | Returns element’s size & position | `Rectangle` | `Rectangle rect = element.getRect();` | `StaleElementReferenceException` |
| `getLocation()` | Returns element’s location (x, y) | `Point` | `Point p = element.getLocation();` | `StaleElementReferenceException` |
| `getSize()` | Returns element’s size (width, height) | `Dimension` | `Dimension d = element.getSize();` | `StaleElementReferenceException` |
| `getScreenshotAs(OutputType<T>)` | Captures screenshot of element | `<T>` | `File src = element.getScreenshotAs(OutputType.FILE);` | `WebDriverException` |

---

## **4\. HTML5 / Form Methods**

| Method | Description | Return Type | Example | Possible Exceptions |
| --- | --- | --- | --- | --- |
| `getDomProperty(String name)` | Gets DOM property of element | `String` | `String prop = element.getDomProperty("value");` | `StaleElementReferenceException` |
| `getDomAttribute(String name)` | Gets DOM attribute value | `String` | `String attr = element.getDomAttribute("id");` | `StaleElementReferenceException` |

---

## **5\. Advanced / Less Common Methods**

| Method | Description | Return Type | Example | Possible Exceptions |
| --- | --- | --- | --- | --- |
| `equals(Object obj)` | Compares two elements | `boolean` | `boolean same = element.equals(otherElement);` | – |
| `hashCode()` | Returns hash code | `int` | `int code = element.hashCode();` | – |
| `toString()` | Returns string representation | `String` | `System.out.println(element.toString());` | – |

---

### **✅ Notes**

1. **All WebElement methods** can throw `StaleElementReferenceException` if the element is no longer attached to DOM.
    
2. **Interaction methods** (`click()`, `sendKeys()`) can throw `ElementNotInteractableException` or `InvalidElementStateException` depending on element state.
    
3. **Form elements** like checkboxes, radio buttons, and input fields use `isSelected()`, `clear()`, `sendKeys()`, `submit()` heavily.
    
4. `getScreenshotAs()` is available for Selenium 4+ and allows capturing a specific element instead of the whole page.
    

### `By`

> Locator class used to find elements.  
> ✅ Static methods:

* [`By.id`](http://by.id/)`(String id)`
    
* [`By.name`](http://by.name/)`(String name)`
    
* `By.className(String className)`
    
* `By.tagName(String tag)`
    
* `By.linkText(String text)`
    
* `By.partialLinkText(String partial)`
    
* `By.cssSelector(String css)`
    
* `By.xpath(String xpath)`
    

---

### `Alert`

> Handle JavaScript popups.

**Key Methods:**

* `accept()`
    
* `dismiss()`
    
* `getText()`
    
* `sendKeys(String keys)`
    

---

### `Navigation` (`driver.navigate()`)

* `to(String url)`
    
* `back()`
    
* `forward()`
    
* `refresh()`
    

---

### `Options` (`driver.manage()`)

* `window()` → returns `Window` interface
    
* `timeouts()` → returns `Timeouts` interface
    
* `deleteAllCookies()`
    
* `deleteCookieNamed(String name)`
    

---

### `Window` (sub-interface of Options)

* `maximize()`
    
* `minimize()`
    
* `fullscreen()`
    
* `setSize(Dimension size)`
    
* `getSize()`
    
* `setPosition(Point position)`
    
* `getPosition()`
    

---

### `Timeouts`

* `implicitlyWait(Duration time)`
    
* `pageLoadTimeout(Duration time)`
    
* `scriptTimeout(Duration time)`
    

---

### `TargetLocator` (`driver.switchTo()`)

* `frame(int index)`
    
* `frame(String nameOrId)`
    
* `frame(WebElement frameElement)`
    
* `parentFrame()`
    
* `defaultContent()`
    
* `alert()`
    
* `window(String handle)`
    

---

## **🔹 Supporting Interfaces / Classes**

### `TakesScreenshot`

* `getScreenshotAs(OutputType<T> target)`
    

---

### `JavascriptExecutor`

* `executeScript(String script, Object... args)`
    
* `executeAsyncScript(String script, Object... args)`
    

---

### `Actions` (Class)

Used for mouse & keyboard actions.

**Methods (all return** `Actions` so you can chain):

* `moveToElement(WebElement target)`
    
* `click()`
    
* `click(WebElement target)`
    
* `doubleClick()`
    
* `doubleClick(WebElement target)`
    
* `contextClick()`
    
* `contextClick(WebElement target)`
    
* `dragAndDrop(WebElement source, WebElement target)`
    
* `dragAndDropBy(WebElement source, int xOffset, int yOffset)`
    
* `keyDown(Keys key)`
    
* `keyUp(Keys key)`
    
* `sendKeys(CharSequence... keys)`
    
* `build()`
    
* `perform()`
    

---

### `Select` (Class)

For dropdowns.

**Key Methods:**

* `selectByIndex(int index)`
    
* `selectByValue(String value)`
    
* `selectByVisibleText(String text)`
    
* `deselectByIndex(int index)`
    
* `deselectByValue(String value)`
    
* `deselectByVisibleText(String text)`
    
* `deselectAll()`
    
* `getOptions()`
    
* `getAllSelectedOptions()`
    
* `getFirstSelectedOption()`
    
* `isMultiple()`
    

---

### `WebDriverWait` (extends FluentWait)

* `until(ExpectedCondition<T> condition)`
    

---

### `FluentWait<T>`

* `withTimeout(Duration time)`
    
* `pollingEvery(Duration interval)`
    
* `ignoring(Class<? extends Throwable> exceptionType)`
    

---

### `ExpectedConditions` (Class)

Common ready-made conditions:

* `visibilityOfElementLocated(By locator)`
    
* `elementToBeClickable(By locator)`
    
* `alertIsPresent()`
    
* `frameToBeAvailableAndSwitchToIt(By locator)`
    
* `titleIs(String title)`
    
* `urlContains(String fraction)`
    

---

### `Keys` (Enum)

Keyboard keys.

* `Keys.ENTER`
    
* [`Keys.TAB`](http://keys.tab/)
    
* `Keys.CONTROL`
    
* `Keys.ARROW_DOWN` etc.
    

---

## **🔹 Driver Classes (implement WebDriver)**

* `ChromeDriver`
    
* `FirefoxDriver`
    
* `EdgeDriver`
    
* `SafariDriver`
    
* `InternetExplorerDriver` (deprecated)
    

All inherit WebDriver’s methods.

---

## **🔹 Utility Classes**

* `Dimension` → window size (`new Dimension(1024, 768)`)
    
* `Point` → window position (`new Point(100, 200)`)
    
* `Rectangle` → element position + size
    
* `Cookie` → browser cookies handling
    

---

# **✅ Summary Table**

| **Category** | **Classes/Interfaces** | **Example Methods** |
| --- | --- | --- |
| Browser Control | WebDriver | get(), close(), quit() |
| Elements | WebElement | click(), sendKeys(), getText() |
| Locators | By | id(), name(), xpath() |
| Navigation | Navigation | back(), forward(), refresh() |
| Alerts | Alert | accept(), dismiss(), getText() |
| Windows/Frames | TargetLocator | frame(), alert(), window() |
| Manage | Options, Window, Timeouts | maximize(), implicitlyWait() |
| Screenshot | TakesScreenshot | getScreenshotAs() |
| JS Execution | JavascriptExecutor | executeScript() |
| User Actions | Actions | dragAndDrop(), doubleClick() |
| Dropdown | Select | selectByValue(), getOptions() |
| Waits | WebDriverWait, FluentWait, ExpectedConditions | until(), visibilityOfElement() |

# Syntax Cheatsheet

---

## 1️⃣ **Browser Launch**

```java
WebDriver driver = new ChromeDriver();   // Launch Chrome
WebDriver driver = new FirefoxDriver();  // Launch Firefox
WebDriver driver = new EdgeDriver();     // Launch Edge
driver.get("https://www.google.com");    // Open URL
driver.manage().window().maximize();     // Maximize window
driver.quit();                           // Close browser (all windows)
driver.close();                          // Close current window
```

---

## 2️⃣ **Find Elements**

```java
driver.findElement(By.id("username"));
driver.findElement(By.name("password"));
driver.findElement(By.className("btn-login"));
driver.findElement(By.tagName("input"));
driver.findElement(By.linkText("Forgot Password?"));
driver.findElement(By.partialLinkText("Forgot"));
driver.findElement(By.cssSelector("input[type='text']"));
driver.findElement(By.xpath("//input[@id='username']"));
```

Multiple elements:

```java
List<WebElement> links = driver.findElements(By.tagName("a"));
```

---

## 3️⃣ **Send Keys / Click / Get Text**

```java
driver.findElement(By.id("username")).sendKeys("admin");
driver.findElement(By.id("password")).sendKeys("admin123");
driver.findElement(By.id("loginBtn")).click();
String text = driver.findElement(By.id("msg")).getText();
```

## 4️⃣ **Waits**

```java
driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

// Explicit wait
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

---

## 5️⃣ **Dropdowns (Select Class)**

```java
WebElement dropdown = driver.findElement(By.id("country"));
Select select = new Select(dropdown);
select.selectByVisibleText("India");
select.selectByValue("IND");
select.selectByIndex(2);
```

---

## 6️⃣ **Alerts**

```java
Alert alert = driver.switchTo().alert();
alert.accept();      // OK
alert.dismiss();     // Cancel
alert.sendKeys("text"); // Enter text
String msg = alert.getText();
```

---

## 7️⃣ **Frames**

```java
driver.switchTo().frame("frameName");
driver.switchTo().frame(0);
driver.switchTo().frame(driver.findElement(By.xpath("//iframe")));
driver.switchTo().defaultContent(); // Back to main page
```

---

## 8️⃣ **Windows / Tabs**

```java
String parent = driver.getWindowHandle();
Set<String> allWindows = driver.getWindowHandles();
for (String win : allWindows) {
    driver.switchTo().window(win);
}
driver.switchTo().window(parent); // Back to parent window
```

---

## 9️⃣ **Actions Class (Mouse/Keyboard)**

```java
Actions actions = new Actions(driver);
actions.moveToElement(driver.findElement(By.id("menu"))).perform(); // Hover
actions.doubleClick(driver.findElement(By.id("btn"))).perform();
actions.contextClick(driver.findElement(By.id("btn"))).perform();  // Right-click
actions.dragAndDrop(src, dest).perform();
actions.sendKeys(Keys.ENTER).perform();
```

---

## 🔟 **JavaScript Executor**

```java
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("window.scrollBy(0,500)");
js.executeScript("arguments[0].click();", element);
js.executeScript("arguments[0].value='Selenium';", element);
```

---

## 1️⃣1️⃣ **Screenshots**

```java
File src = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(src, new File("screenshot.png"));
```

---

## 1️⃣2️⃣ **Navigation**

```java
driver.navigate().to("https://www.example.com");
driver.navigate().back();
driver.navigate().forward();
driver.navigate().refresh();
```

---

## 1️⃣3️⃣ **Check Elements**

```java
driver.findElement(By.id("chkbox")).isDisplayed();
driver.findElement(By.id("chkbox")).isEnabled();
driver.findElement(By.id("chkbox")).isSelected();
```

---

## 1️⃣4️⃣ **Cookies**

```java
driver.manage().getCookies();
driver.manage().addCookie(new Cookie("key", "value"));
driver.manage().deleteCookieNamed("key");
driver.manage().deleteAllCookies();
```

---

## 1️⃣5️⃣ **Robot Class (Keyboard/Mouse events)**

```java
Robot robot = new Robot();
robot.keyPress(KeyEvent.VK_DOWN);
robot.keyRelease(KeyEvent.VK_DOWN);
robot.keyPress(KeyEvent.VK_ENTER);
robot.keyRelease(KeyEvent.VK_ENTER);
```