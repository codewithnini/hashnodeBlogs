---
title: "Selenium With Java"
datePublished: Fri Sep 26 2025 07:43:25 GMT+0000 (Coordinated Universal Time)
cuid: cmg0jc4jb000102jy12wubasi
slug: selenium-with-java
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1759081249818/197acbd8-0b6d-462b-880f-28dc74e83318.png
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

# 1️⃣ **Browser Launch**

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

# 2️⃣ **Find Elements**

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

# 3️⃣ **Send Keys / Click / Get Text**

```java
driver.findElement(By.id("username")).sendKeys("admin");
driver.findElement(By.id("password")).sendKeys("admin123");
driver.findElement(By.id("loginBtn")).click();
String text = driver.findElement(By.id("msg")).getText();
```

# 4.🕐 **WAIT STATEMENTS in Selenium**

Waiting is one of the **most important synchronization mechanisms** in Selenium to make sure the script and browser execute in sync.

---

## 🔹 Why Wait Is Needed

* Selenium executes faster than browser rendering.
    
* If element loads late → `NoSuchElementException`.
    
* Wait helps Selenium **pause until element or condition is ready**.
    

---

## 🧭 **Types of Waits**

| Type | Nature | Package | Used for |
| --- | --- | --- | --- |
| **1\. Implicit Wait** | Global wait | `org.openqa.selenium` | Waits for element presence |
| **2\. Explicit Wait** | Conditional wait | [`org.openqa.selenium.support`](http://org.openqa.selenium.support)`.ui.WebDriverWait` | Waits for specific condition |
| **3\. Fluent Wait** | Advanced explicit wait | [`org.openqa.selenium.support`](http://org.openqa.selenium.support)`.ui.FluentWait` | Custom interval + exceptions |
| **4\. Thread.sleep()** | Static wait (Java) | `java.lang.Thread` | Forcefully pause code |

---

## 🔸 1️⃣ Implicit Wait

**Definition:**  
Sets a default wait time for the WebDriver to search for elements before throwing an exception.

**Syntax:**

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
```

**Usage:**

* Applies globally to all elements.
    
* Waits till element appears in DOM (not necessarily visible).
    

**Example:**

```java
WebDriver driver = new ChromeDriver();
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
driver.get("https://example.com");
WebElement element = driver.findElement(By.id("username"));  // waits up to 10s
```

**⚠️ Limitations:**

* Not condition-based.
    
* Only works for element presence, not for alert, URL, frame, etc.
    
* Not recommended to mix with Explicit Wait.
    

---

## 🔸 2️⃣ Explicit Wait

**Definition:**  
Waits until a specific condition is true (like element visible, clickable, alert present, title, etc.)

**Class:** `WebDriverWait`  
**Extends:** `FluentWait`

**Syntax:**

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(20));
WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

---

### 🔹 Common ExpectedConditions:

| Condition | Method | Description |
| --- | --- | --- |
| Element visible | `visibilityOf(element)` / `visibilityOfElementLocated(locator)` | Element must be visible |
| Element clickable | `elementToBeClickable(locator)` | Wait until clickable |
| Element present | `presenceOfElementLocated(locator)` | Exists in DOM |
| Element invisible | `invisibilityOfElementLocated(locator)` | Wait until disappears |
| Alert present | `alertIsPresent()` | Wait for alert popup |
| Frame available | `frameToBeAvailableAndSwitchToIt(locator)` | Wait + switch to frame |
| Text present | `textToBePresentInElement(locator, text)` | Wait for text |
| Title condition | `titleIs(String)` / `titleContains(String)` | Check page title |
| URL condition | `urlContains(String)` / `urlToBe(String)` | Wait for navigation |

**Example:**

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(ExpectedConditions.elementToBeClickable(By.id("loginBtn"))).click();
```

---

## 🔸 3️⃣ Fluent Wait

**Definition:**  
Customizable explicit wait that defines:

* Timeout duration
    
* Polling frequency
    
* Ignored exceptions
    

**Class:** `FluentWait<T>`

**Syntax:**

```java
Wait<WebDriver> wait = new FluentWait<>(driver)
        .withTimeout(Duration.ofSeconds(30))
        .pollingEvery(Duration.ofSeconds(5))
        .ignoring(NoSuchElementException.class);

WebElement element = wait.until(driver -> driver.findElement(By.id("username")));
```

**✅ Advantages:**

* Checks repeatedly until timeout.
    
* Flexible — you can ignore exceptions or adjust polling rate.
    

---

## 🔸 4️⃣ Thread.sleep()

**Definition:**  
A **hard wait** — Java thread pauses for a fixed duration.

**Syntax:**

```java
Thread.sleep(5000);  // 5 seconds
```

**Drawback:**

* Not intelligent (always waits full duration).
    
* Slows down test execution.
    
* Use only for temporary debugging.
    

---

## ⚙️ **Combining Waits – Best Practice Example**

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(5)); // for general load
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));

// Login scenario
driver.get("https://app.example.com");
wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username"))).sendKeys("admin");
wait.until(ExpectedConditions.elementToBeClickable(By.id("loginBtn"))).click();
```

---

## 📋 **Cheat Sheet Summary Table**

| Type | Class / Method | Example | Best Use Case |
| --- | --- | --- | --- |
| **Implicit Wait** | `driver.manage().timeouts().implicitlyWait()` | Global 10s wait | Page element load |
| **Explicit Wait** | `new WebDriverWait(driver, Duration.ofSeconds(x)).until(ExpectedConditions...)` | Conditional wait | Element clickable / visible |
| **Fluent Wait** | `new FluentWait(driver).withTimeout().pollingEvery().ignoring()` | Custom polling | Dynamic AJAX elements |
| **Thread.sleep()** | `Thread.sleep(ms)` | Fixed pause | Temporary debugging |

---

## 🚀 **Advanced Tip — Custom ExpectedCondition**

You can create your own condition:

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(15));
wait.until(driver -> driver.findElement(By.id("status")).getText().equals("Ready"));
```

---

## 🧩 **In Frameworks (Usage)**

| Layer | Where Used | Why |
| --- | --- | --- |
| **BaseTest / DriverManager** | `implicitWait` setup | Global setting |
| **PageObject (POM)** | `explicitWait` inside methods | Wait per element action |
| **ReusableUtils** | `FluentWait` utility | For dynamic components |
| **TestNG Hooks** | beforeMethod setup | Configure wait globally |

```java
driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

// Explicit wait
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

---

# 5️⃣ **Dropdowns (Select Class)**

```java
WebElement dropdown = driver.findElement(By.id("country"));
Select select = new Select(dropdown);
select.selectByVisibleText("India");
select.selectByValue("IND");
select.selectByIndex(2);
```

---

# 6️⃣ **Alerts**

```java
Alert alert = driver.switchTo().alert();
alert.accept();      // OK
alert.dismiss();     // Cancel
alert.sendKeys("text"); // Enter text
String msg = alert.getText();
```

---

# 7️⃣ **Frames**

```java
driver.switchTo().frame("frameName");
driver.switchTo().frame(0);
driver.switchTo().frame(driver.findElement(By.xpath("//iframe")));
driver.switchTo().defaultContent(); // Back to main page
```

---

# 8\. **Windows / Tabs**

```java
String parent = driver.getWindowHandle();
Set<String> allWindows = driver.getWindowHandles();
for (String win : allWindows) {
    driver.switchTo().window(win);
}
driver.switchTo().window(parent); // Back to parent window
```

---

# 9\. **Actions Class (Mouse/Keyboard)**

```java
Actions actions = new Actions(driver);
actions.moveToElement(driver.findElement(By.id("menu"))).perform(); // Hover
actions.doubleClick(driver.findElement(By.id("btn"))).perform();
actions.contextClick(driver.findElement(By.id("btn"))).perform();  // Right-click
actions.dragAndDrop(src, dest).perform();
actions.sendKeys(Keys.ENTER).perform();
```

---

# 10\. **JavaScript Executor**

---

## 1️⃣ What is JavascriptExecutor?

**JavascriptExecutor** is an **interface** provided by Selenium WebDriver that allows us to **run JavaScript code directly within the browser** from our Java (or other language) Selenium code.

---

## 2️⃣ Why Use JavascriptExecutor?

Sometimes **normal WebDriver methods fail**, especially in cases like:

* Elements are **hidden, disabled, or behind overlays**
    
* Scrolling is needed to bring an element **into view**
    
* A click doesn't work due to **JavaScript event handling**
    
* WebDriver **cannot access certain DOM elements** directly
    

In these situations, **JavaScriptExecutor gives direct access to the webpage's DOM**, allowing more control.

---

## 3️⃣ How to Use JavascriptExecutor

> JavascriptExecutor is an **interface**, not a class.  
> You need to **cast your WebDriver instance** to JavascriptExecutor.

**Syntax:**

```java
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("your JavaScript code here");
```

You can also **pass arguments** to your script:

```java
js.executeScript("arguments[0].click();", element);
```

---

## 4️⃣ Common JavascriptExecutor Use Cases

### 4.1 Clicking an Element

Sometimes [`element.click`](http://element.click)`()` **doesn't work** (like hidden buttons).

```java
WebElement element = driver.findElement(By.id("submit"));
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("arguments[0].click();", element);
```

---

### 4.2 Typing Text into Input Field

```java
WebElement input = driver.findElement(By.id("username"));
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("arguments[0].value='testuser';", input);
```

---

### 4.3 Scrolling the Page

**Scroll down by pixels:**

```java
js.executeScript("window.scrollBy(0,500)");
```

**Scroll to the bottom of the page:**

```java
js.executeScript("window.scrollTo(0, document.body.scrollHeight)");
```

**Scroll to a specific element:**

```java

// Scroll down by 500px
js.executeScript("window.scrollBy(0,500)");

// Scroll to bottom
js.executeScript("window.scrollTo(0, document.body.scrollHeight)");

// Scroll to element
WebElement element = driver.findElement(By.id("footer"));
js.executeScript("arguments[0].scrollIntoView(true);", element);
```

---

### 4.4 Getting the Page Title

```bash
String title = (String) js.executeScript("return document.title;");
System.out.println("Page title is: " + title);
```

---

### 4.5 Getting the Entire Page Text

```bash
String text = (String) js.executeScript("return document.documentElement.innerText;");
System.out.println(text);
```

---

### 4.6 Highlighting an Element (For Debugging)

```bash
WebElement button = driver.findElement(By.id("login"));
js.executeScript("arguments[0].style.border='3px solid red';", button);
```

---

## Common Use Cases (With Visuals)

| Use Case | Java Code | Visual Explanation |
| --- | --- | --- |
| **Click Element** | `js.executeScript("arguments[0].click();", element);` | Element clicked even if hidden/overlayed |
| **Type in Input** | `js.executeScript("arguments[0].value='testuser';", input);` | Input box filled via JS |
| **Scroll Page** | `js.executeScript("window.scrollBy(0,500)");` | Scroll page down by 500px |
| **Scroll to Element** | `js.executeScript("arguments[0].scrollIntoView(true);", element);` | Scroll page to element |
| **Get Page Title** | `String title = (String) js.executeScript("return document.title;");` | Retrieve browser title |
| **Get Page Text** | `String text = (String) js.executeScript("return document.documentElement.innerText;");` | Full page text |
| **Highlight Element** | `js.executeScript("arguments[0].style.border='3px solid red';", element);` | For debugging visual cue |

## 5️⃣ What Happens Behind the Scenes?

* The `executeScript()` method sends **JavaScript code** to the browser.
    
* The **browser runs it**, just like in the console.
    
* You can **read, write, and modify DOM elements directly** using this method.
    
* **Mastering JavascriptExecutor** can unlock hidden power in Selenium automation.
    

---

## 6️⃣ Best Practices

* Use JavascriptExecutor **only when WebDriver methods fail**.
    
* Avoid overusing it; prefer **WebDriver native methods** first.
    
* Always **pass elements as arguments** instead of hardcoding them in JS.
    
* Combine with **Explicit Waits** for better stability.
    

```java
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("window.scrollBy(0,500)");
js.executeScript("arguments[0].click();", element);
js.executeScript("arguments[0].value='Selenium';", element);
```

---

# 11\. **Screenshots**

A screenshot is a **picture of the page or element**.

**Why we need it:**

* See what went wrong when a test fails.
    
* Attach to bug reports.
    
* Add to test reports for clarity.
    
* Check page layout or design.
    
* Help in automated pipelines (like Jenkins).
    

📸 **Why Screenshots Are Needed in Selenium**

* **Debugging:** Screenshots help developers and testers see exactly what was on the screen when a test failed.
    
* **Proof for Bugs:** You can attach screenshots to bug reports (like in JIRA) to show the problem.
    
* **Better Reports:** Screenshots make test reports (like Extent, Allure, or TestNG reports) easier to understand.
    
* **Validation:** They can be used to check how the page looks, such as layout or design.
    
* **CI/CD:** In automated pipelines (like Jenkins), screenshots help find out why a test failed without opening the computer manually.
    

## **TakesScreenshot Interface Can Take 3 Ways**

### 🔹 1. As ***FILE*** (Most Common) **Browser Screenshot**

* **What:** Captures the **entire visible part of the browser window**.
    
* **How:** Using `TakesScreenshot` interface.
    
* **Use Case:** Debugging, attaching to reports, CI/CD pipelines.
    

### 🔹 2. **As Base64 String** (useful in reports like Extent/Allure)

* **What:** Captures screenshot as a **Base64-encoded string**.
    
* **Use Case:**
    
    * Embed directly into **Extent Reports, Allure, or HTML reports**.
        
    * Avoid saving a physical file.
        
* **Tip:** Can be converted back to a file if needed.
    

➡ Advantage: Easy to **embed directly** into HTML/PDF reports without saving a file.

### 🔹 3. **As Byte Array** (useful in APIs / custom reports)

* **What:** Captures screenshot as a **byte array**.
    
* **Use Case:**
    
    * Store in memory, attach to **Allure reports**, or save in **databases**.
        

### **All 3 ways code you can see below.**

```java
package screenshotsWay;

import java.io.File;
import java.io.FileOutputStream;
import java.time.Duration;
import java.util.Arrays;
import java.util.Base64;

import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.Test;

public class ScreenshotTest {

	// using File output commonScreenShot
	@Test
	public void commonScreenShot() throws Throwable {
		WebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

		driver.get("https://www.google.com/");
		TakesScreenshot ts = (TakesScreenshot) driver;
		File src = ts.getScreenshotAs(OutputType.FILE);
		File dest = new File("./screenshots/commonScreenShot.png");
		org.openqa.selenium.io.FileHandler.copy(src, dest);

		driver.close();
		driver.quit();
	}

	// using Base64 output base64ScreenShot
	@Test
	public void base64ScreenShot() throws Throwable {
		WebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

		driver.get("https://www.google.com/");
		TakesScreenshot ts = (TakesScreenshot) driver;
		String src = ts.getScreenshotAs(OutputType.BASE64);

		byte[] dest = Base64.getDecoder().decode(src); // Base64 class from (java.util) decode to byte Array

		System.out.println(Arrays.toString(dest)); // this only for checking what the output in console

		FileOutputStream fos = new FileOutputStream(new File("./screenshots/base64ScreenShot.png"));
		fos.write(dest);
		fos.close();

		driver.close();
		driver.quit();
	}

	// using byte[] output ByteArrayScreenShot
	@Test
	public void ByteArrayScreenShot() throws Throwable {
		WebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

		driver.get("https://www.google.com/");
		TakesScreenshot ts = (TakesScreenshot) driver;
		byte[] src = ts.getScreenshotAs(OutputType.BYTES);

		System.out.println(Arrays.toString(src)); // this only for checking what the output in console

		FileOutputStream fos = new FileOutputStream(new File("./screenshots/ByteArrayScreenShot.png"));
		fos.write(src);
		fos.close();

		driver.close();
		driver.quit();
	}

}
```

## 📸 **Types of Screenshots in Selenium**

### 1\. **Full Page / Browser Screenshot**

* **What:** Captures the **entire visible part of the browser window**.
    
* **How:** Using `TakesScreenshot` interface.
    
* **Use Case:** Debugging, attaching to reports, CI/CD pipelines.
    

---

### 2\. **Element Screenshot**

* **What:** Captures **only a specific web element** (like a button, logo, or form).
    
* **How:** Call `getScreenshotAs` on the WebElement.
    
* **Use Case:** When only part of the page matters (e.g., validating a form or logo).
    

---

```java
package screenshotsTypes;

import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Files;
import java.time.Duration;
import java.util.Arrays;
import java.util.Base64;

import javax.imageio.ImageIO;

import org.openqa.selenium.By;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.devtools.v137.page.model.Screenshot;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.firefox.FirefoxOptions;
import org.openqa.selenium.remote.RemoteWebDriver;
import org.testng.annotations.Test;

import ru.yandex.qatools.ashot.AShot;
import ru.yandex.qatools.ashot.shooting.ShootingStrategies;

public class ScreenshotTypesTest {

	// using File output commonScreenShot viewPortScreenShot
	@Test
	public void viewPortScreenShot() throws Throwable {
		WebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

		driver.get("https://www.flipkart.com/");
		TakesScreenshot ts = (TakesScreenshot) driver;
		File src = ts.getScreenshotAs(OutputType.FILE);
		File dest = new File("./screenshots/types/viewPortScreenShot.png");
		org.openqa.selenium.io.FileHandler.copy(src, dest);

		driver.close();
		driver.quit();
	}
	
	// using File output   commonScreenShot elementScreenShot
		@Test
		public void elementScreenShot() throws Throwable {
			RemoteWebDriver driver = new ChromeDriver();
			driver.manage().window().maximize();
			driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
			driver.get("https://www.flipkart.com/");
			WebElement eleemnt = driver.findElement(By.xpath("//img[@src='https://rukminim2.flixcart.com/fk-p-flap/1620/270/image/f16ce51e6dd8a20c.jpg?q=90']"));
			File src = eleemnt.getScreenshotAs(OutputType.FILE);
			File dest = new File("./screenshots/types/elementScreenShot.png");
			org.openqa.selenium.io.FileHandler.copy(src, dest);

			driver.close();
			driver.quit();
		}

	// using File output  and RempoteWebdriver Class Take viewPortScreenShot
	@Test
	public void viewPortScreenShotWithRemoteWebdriverClass() throws Throwable {
		RemoteWebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
		driver.get("https://www.flipkart.com/");
		File viewPort = driver.getScreenshotAs(OutputType.FILE);
		File dest = new File("./screenshots/types/viewPortScreenShotWithRemoteWebdriverClass.png");
		org.openqa.selenium.io.FileHandler.copy(viewPort, dest);

		driver.close();
		driver.quit();
	}
	
	// using File output  and RempoteWebdriver Class Take elementScreenShot
		@Test
		public void elementScreenShotWithRemoteWebdriverClass() throws Throwable {
			RemoteWebDriver driver = new ChromeDriver();
			driver.manage().window().maximize();
			driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
			driver.get("https://www.flipkart.com/");
			
			WebElement eleemnt = driver.findElement(By.xpath("//img[@src='https://rukminim2.flixcart.com/fk-p-flap/1620/270/image/f16ce51e6dd8a20c.jpg?q=90']"));
			File src = eleemnt.getScreenshotAs(OutputType.FILE);
			File dest = new File("./screenshots/types/elementScreenShotWithRemoteWebdriverClass.png");
			org.openqa.selenium.io.FileHandler.copy(src, dest);

			driver.close();
			driver.quit();
		}
		
}
```

---

## 📸 **Other use cases of Screenshots in Selenium**

### 3\. **Full Page Screenshot Using AShot**

* **What:** Captures the **entire web page**, including parts **not visible** on the screen.
    
* **How:** Using **AShot library**.
    
* **Use Case:** Long pages with scroll, visual testing, layout validation.
    

Selenium’s native `TakesScreenshot` only captures the visible viewport.  
For **full-page screenshots**:

```java
<!-- pom.xml -->
<dependency>
    <groupId>ru.yandex.qatools.ashot</groupId>
    <artifactId>ashot</artifactId>
    <version>1.5.4</version>
</dependency>
```

```java
Screenshot screenshot = new AShot().shootingStrategy(ShootingStrategies.viewportPasting(1000))
        .takeScreenshot(driver);
ImageIO.write(screenshot.getImage(), "PNG", new File("./fullpage.png"));
```

---

### 4\. **OS-Level Screenshot Using Robot Class**

* **What:** Captures **the entire screen**, including **OS popups, alerts, or dialogs**.
    
* **How:** Using Java’s `Robot` class.
    

```java
Robot robot = new Robot();
Rectangle screenRect = new Rectangle(Toolkit.getDefaultToolkit().getScreenSize());
BufferedImage screenFullImage = robot.createScreenCapture(screenRect);
ImageIO.write(screenFullImage, "png", new File("robot_screenshot.png"));
```

* **Use Case:** For **file upload/download dialogs**, system alerts, or anything outside the browser.
    

---

### 5\. **Screenshots With Event Listeners (on failure automatically)**

* **What:** Capture screenshots automatically whenever a test fails using **TestNG Listeners**.
    
* **How:** Call screenshot methods in `onTestFailure()` in `ITestListener`.
    
* **Use Case:** Debugging failed tests, CI/CD reporting.
    

---

### 6\. **RemoteWebDriver (Selenium Grid / Cloud providers like BrowserStack)**

When running in Selenium Grid / BrowserStack, you can still use:

➡ Screenshot will be captured from the remote machine.

## 📌 Summary Table

| Screenshot Type | Captures | Output Type | Use Case |
| --- | --- | --- | --- |
| Full Page / Browser | Entire visible browser window | File, Base64, Bytes | Debugging, Reports |
| Element | Specific WebElement | File, Base64, Bytes | Element validation |
| Base64 | Entire page / element | Base64 String | Embed in reports |
| Byte Array | Entire page / element | byte\[\] | Reports, DB, in-memory |
| Full Page (AShot) | Entire scrollable page | BufferedImage/File | Visual testing |
| OS-Level (Robot) | Full screen including OS popups | BufferedImage/File | Alerts, dialogs, system testing |
| Auto on Test Failure | Page at point of failure | File/Base64/Bytes | CI/CD & reporting |

## 🔹📌 Where Screenshots Are Used in Frameworks

* **TestNG Listeners / @AfterMethod** → Capture screenshot on failure.
    
* **Extent Reports / Allure Reports** → Attach screenshots for failed steps.
    
* **CI/CD Pipelines (Jenkins)** → Store screenshots as artifacts for debugging.
    
* **Page Object Model** → Utility class (e.g., `ScreenshotUtility.capture(driver, "filename")`).
    

---

## ✅ Best Practices

1. Always store screenshots in a separate `screenshots/` folder.
    
2. Use **unique names** (testName + timestamp).
    
3. Use **Base64** for embedding in reports (lighter & no file handling issues).
    
4. For visual/UI testing, use **AShot** or tools like **Applitools**.
    

# 12\. **Navigation**

```java
driver.navigate().to("https://www.example.com");
driver.navigate().back();
driver.navigate().forward();
driver.navigate().refresh();
```

---

# 13\. **Check Elements**

```java
driver.findElement(By.id("chkbox")).isDisplayed();
driver.findElement(By.id("chkbox")).isEnabled();
driver.findElement(By.id("chkbox")).isSelected();
```

---

# 14\. **Cookies**

```java
driver.manage().getCookies();
driver.manage().addCookie(new Cookie("key", "value"));
driver.manage().deleteCookieNamed("key");
driver.manage().deleteAllCookies();
```

---

# 15\. **Robot Class (Keyboard/Mouse events)**

```java
Robot robot = new Robot();
robot.keyPress(KeyEvent.VK_DOWN);
robot.keyRelease(KeyEvent.VK_DOWN);
robot.keyPress(KeyEvent.VK_ENTER);
robot.keyRelease(KeyEvent.VK_ENTER);
```